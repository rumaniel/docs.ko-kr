---
title: .NET Core에서 어셈블리 언로드 기능을 사용하고 디버그하는 방법
description: 수집 가능한 AssemblyLoadContext를 사용하여 관리형 어셈블리를 로드하고 언로드하는 방법과 언로드를 성공하지 못하게 하는 문제를 디버그하는 방법을 알아봅니다.
author: janvorli
ms.author: janvorli
ms.date: 02/05/2019
ms.openlocfilehash: 52cd864393342e2bc31f872b9d09cb484c2c8463
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972494"
---
# <a name="how-to-use-and-debug-assembly-unloadability-in-net-core"></a>.NET Core에서 어셈블리 언로드 기능을 사용하고 디버그하는 방법

.NET Core 3.0부터 어셈블리 집합을 로드하고 나중에 언로드하는 기능이 지원됩니다. .NET Framework에서 사용자 지정 앱 도메인은 이러한 용도로 사용되지만 .NET Core에서는 단일 기본 앱 도메인만 지원합니다.

.NET Core 3.0 이상 버전에서는 <xref:System.Runtime.Loader.AssemblyLoadContext>를 통해 언로드 가능성을 지원합니다. 어셈블리 집합을 수집 가능한 `AssemblyLoadContext`에 로드하고, 해당 어셈블리에서 메서드를 실행하거나 리플렉션을 사용하여 검사만 한 다음, 마지막으로 `AssemblyLoadContext`를 언로드할 수 있습니다. 그러면 해당 `AssemblyLoadContext`에 로드된 어셈블리를 언로드합니다.

`AssemblyLoadContext`를 사용하여 언로드하는 것과 AppDomain을 사용하여 언로드하는 데는 중요한 차이점이 있습니다. AppDomain을 사용하면 언로드가 강제로 적용됩니다. 언로드 시 대상 AppDomain에서 실행 중인 모든 스레드가 중단되고 대상 AppDomain에서 만들어진 관리형 COM 개체가 제거됩니다. `AssemblyLoadContext`에서 언로드는 “협조적”입니다. <xref:System.Runtime.Loader.AssemblyLoadContext.Unload%2A?displayProperty=nameWithType> 메서드를 호출하면 언로드를 시작하기만 합니다. 다음과 같은 경우 언로드가 완료됩니다.

- 호출 스택에서 `AssemblyLoadContext`에 로드된 어셈블리의 메서드가 있는 스레드가 없습니다.
- `AssemblyLoadContext`에 로드된 어셈블리의 유형, 해당 유형의 인스턴스 및 `AssemblyLoadContext` 외부의 어셈블리는 다음에서 참조하지 않습니다.
  - 약한 참조(<xref:System.WeakReference> 또는 <xref:System.WeakReference%601>)를 제외한 `AssemblyLoadContext` 외부의 참조.
  - 강력한 GC 핸들(<xref:System.Runtime.InteropServices.GCHandleType>.<xref:System.Runtime.InteropServices.GCHandleType.Normal> 또는 <xref:System.Runtime.InteropServices.GCHandleType>.<xref:System.Runtime.InteropServices.GCHandleType.Pinned>) - 모두 `AssemblyLoadContext`의 내부 및 외부 모두에 있습니다.

## <a name="use-collectible-assemblyloadcontext"></a>수집 가능한 AssemblyLoadContext 사용

이 섹션에는 .NET Core 애플리케이션을 수집 가능한 `AssemblyLoadContext`에 로드하고, 진입점을 실행한 다음, 언로드하는 간단한 방법을 보여주는 자세한 단계별 자습서가 포함되어 있습니다. [https://github.com/dotnet/samples/tree/master/core/tutorials/Unloading](https://github.com/dotnet/samples/tree/master/core/tutorials/Unloading)에서 전체 샘플을 찾을 수 있습니다.

### <a name="create-a-collectible-assemblyloadcontext"></a>수집 가능한 AssemblyLoadContext 만들기

<xref:System.Runtime.Loader.AssemblyLoadContext>에서 클래스를 파생시키고 <xref:System.Runtime.Loader.AssemblyLoadContext.Load%2A?displayProperty=nameWithType> 메서드를 오버로드해야 합니다. 이 메서드는 해당 `AssemblyLoadContext`에 로드된 어셈블리의 종속 항목인 모든 어셈블리의 참조를 확인합니다.
다음 코드는 가장 간단한 사용자 지정 `AssemblyLoadContext`의 예입니다.

[!code-csharp[Simple custom AssemblyLoadContext](~/samples/snippets/standard/assembly/unloading/simple_example.cs#1)]

여기에서 볼 수 있듯이 `Load` 메서드는 `null`을 반환합니다. 즉, 모든 종속성 어셈블리가 기본 컨텍스트에 로드되고 새 컨텍스트에는 명시적으로 로드된 어셈블리만 포함됩니다.

종속 항목의 일부 또는 전체를 `AssemblyLoadContext`에 로드하려는 경우 `Load` 메서드에서 `AssemblyDependencyResolver`를 사용할 수 있습니다. `AssemblyDependencyResolver`는 컨텍스트에 로드된 기본 어셈블리의 디렉터리에 포함된 *.deps.json* 파일을 사용하고 해당 디렉터리의 어셈블리 파일을 사용하여 어셈블리 이름을 절대 어셈블리 파일 경로로 확인합니다.

[!code-csharp[Advanced custom AssemblyLoadContext](~/samples/snippets/standard/assembly/unloading/complex_assemblyloadcontext.cs)]

### <a name="use-a-custom-collectible-assemblyloadcontext"></a>수집 가능한 사용자 지정 AssemblyLoadContext 사용

이 섹션에서는 `TestAssemblyLoadContext`의 간단한 버전을 사용한다고 가정합니다.

사용자 지정 `AssemblyLoadContext`의 인스턴스를 만들고 다음과 같이 어셈블리를 로드할 수 있습니다.

[!code-csharp[Part 1](~/samples/snippets/standard/assembly/unloading/simple_example.cs#3)]

로드된 어셈블리에서 참조하는 각 어셈블리에 대해 `TestAssemblyLoadContext.Load` 메서드를 호출하므로, `TestAssemblyLoadContext`에서 어셈블리를 가져올 위치를 결정할 수 있습니다. 이 경우 `null`을 반환하여, 런타임에서 기본적으로 어셈블리를 로드하는 데 사용하는 위치에서 기본 컨텍스트에 로드되어야 함을 나타냅니다.

이제 어셈블리가 로드되었으므로 여기에서 메서드를 실행할 수 있습니다. 다음과 같이 `Main` 메서드를 실행합니다.

[!code-csharp[Part 2](~/samples/snippets/standard/assembly/unloading/simple_example.cs#4)]

`Main` 메서드가 리턴하고 나면 사용자 지정 `AssemblyLoadContext`에서 `Unload` 메서드를 호출하거나 `AssemblyLoadContext`에 대한 참조를 제거하여 언로드를 시작할 수 있습니다.

[!code-csharp[Part 3](~/samples/snippets/standard/assembly/unloading/simple_example.cs#5)]

그러면 테스트 어셈블리를 언로드할 수 있습니다. `TestAssemblyLoadContext`, `Assembly` 및 `MethodInfo`(`Assembly.EntryPoint`)가 스택 슬롯 참조를 통해 활성 상태를 유지할 수 없도록(real 또는 Jit 도입 로컬) 인라인화할 수 없는 개별 메서드로 이 모두를 통합해 보겠습니다. 그러면 `TestAssemblyLoadContext`를 활성 상태로 유지하고 언로드를 방지할 수 있습니다.

또한 나중에 언로드 완료를 검색하는 데 사용할 수 있도록 `AssemblyLoadContext`의 약한 참조를 반환합니다.

[!code-csharp[Part 4](~/samples/snippets/standard/assembly/unloading/simple_example.cs#2)]

이제 이 함수를 실행하여 어셈블리를 로드, 실행 및 언로드할 수 있습니다.

[!code-csharp[Part 5](~/samples/snippets/standard/assembly/unloading/simple_example.cs#6)]

그러나 언로드는 즉시 완료되지 않습니다. 앞에서 설명한 것처럼 GC를 사용하여 테스트 어셈블리에서 모든 개체를 수집합니다. 대부분의 경우 언로드가 완료될 때까지 기다릴 필요가 없습니다. 그러나 언로드가 완료되었음을 확인하는 것이 유용한 경우도 있습니다. 예를 들어, 디스크에서 사용자 지정 `AssemblyLoadContext`로 로드된 어셈블리 파일을 삭제할 수 있습니다. 이 경우 다음 코드 조각을 사용할 수 있습니다. GC를 트리거하고 사용자 지정 `AssemblyLoadContext`에 대한 약한 참조가 `null`로 설정되어 대상 개체가 수집되었음을 나타낼 때까지 루프에서 보류 중인 종료자를 대기합니다. 대부분의 경우 루프를 한 번만 통과하면 됩니다. 그러나 `AssemblyLoadContext`에서 실행 중인 코드를 통해 만든 개체에 종료자가 있는 복잡한 경우에는 추가 통과가 필요합니다.

[!code-csharp[Part 6](~/samples/snippets/standard/assembly/unloading/simple_example.cs#7)]

### <a name="the-unloading-event"></a>언로딩 이벤트

이 이벤트는 경우에 따라 언로드를 시작할 때 일부 정리를 수행하기 위해 사용자 지정 `AssemblyLoadContext`에 로드된 코드에 필요할 수 있습니다. 예를 들어 스레드를 중지하고, 몇 가지 강력한 GC 핸들을 정리해야 할 수 있습니다. 이 경우 `Unloading` 이벤트를 사용할 수 있습니다. 필요한 정리를 수행하는 처리기를 이 이벤트에 연결할 수 있습니다.

### <a name="troubleshoot-unloadability-issues"></a>로드 불가능 문제 해결

언로드의 협조적 특성 때문에 수집 가능한 `AssemblyLoadContext`의 요소가 활성 상태를 유지하게 하고 언로드를 방지하는 참조를 잊기 쉽습니다. 다음은 참조를 보유할 수 있는 사항(일부는 명확하지 않음)의 요약입니다.

- 수집 가능한 `AssemblyLoadContext`의 외부에서 보유하며, 스택 슬롯 또는 프로세서 레지스터(사용자 코드를 사용하여 명시적으로 만들거나 JIT에서 내재적으로 생성하는 메서드 로컬), 정적 변수 또는 강력한/고정 GC 핸들에 저장되며 다음을 가리키는 일반 참조.
  - 수집 가능한 `AssemblyLoadContext`에 로드된 어셈블리.
  - 이러한 어셈블리의 형식입니다.
  - 이러한 어셈블리에 있는 형식의 인스턴스입니다.
- 수집 가능한 `AssemblyLoadContext`에 로드된 어셈블리의 스레드 실행 코드.
- 수집 가능한 `AssemblyLoadContext` 내부에서 만들어진 수집 불가능한 사용자 지정 `AssemblyLoadContext` 형식의 인스턴스
- 콜백이 사용자 지정 `AssemblyLoadContext`의 메서드로 설정된 보류 중인 <xref:System.Threading.RegisteredWaitHandle> 인스턴스

개체를 루팅하는 스택 슬롯 및 프로세서 레지스터를 찾기 위한 힌트:

- 사용자가 만든 지역 변수가 없더라도 함수 호출 결과를 다른 함수에 직접 전달하면 루트가 생성될 수 있습니다.
- 메서드의 임의 지점에서 개체에 대한 참조를 사용할 수 있는 경우 JIT는 현재 함수에서 원하는 기간 동안 참조를 스택 슬롯/프로세서 레지스터에 유지하도록 결정할 수 있습니다.

## <a name="debug-unloading-issues"></a>디버그 언로드 문제

언로드 관련 문제를 디버깅하는 것이 지루한 작업이 될 수 있습니다. `AssemblyLoadContext`를 활성 상태로 유지할 수 있는 항목을 알 수 없지만 언로드가 실패하는 상황이 발생할 수 있습니다.
이 문제를 해결하는 가장 좋은 방법은 SOS 플러그 인을 사용하는 WinDbg(Unix의 LLDB)입니다. 특정 `AssemblyLoadContext`에 속한 `LoaderAllocator`를 활성 상태로 유지하는 사항을 찾아야 합니다.
이 플러그 인을 사용하면 GC 힙 개체, 해당 계층 구조 및 루트를 확인할 수 있습니다.
플러그 인을 디버거로 로드하려면 디버거 명령줄에서 다음 명령을 입력합니다.

WinDbg의 경우(.NET Core 애플리케이션으로 분리될 때 WinDbg가 자동으로 수행함):

```console
.loadby sos coreclr
```

LLDB에서:

```console
plugin load /path/to/libsosplugin.so
```

언로드에 문제가 있는 예제 프로그램을 디버깅해 보겠습니다. 소스 코드는 아래 포함되어 있습니다. WinDbg에서 실행하면 언로드 성공 여부를 확인한 후 즉시 프로그램이 디버거를 시작합니다. 그런 다음 원인을 검색하기 시작할 수 있습니다.

Unix에서 LLDB를 사용하여 디버깅하는 경우 다음 예의 SOS 명령 앞에 `!`가 없습니다.

```console
!dumpheap -type LoaderAllocator
```

이 명령은 GC 힙에 있는 `LoaderAllocator`를 포함하는 형식 이름을 사용하는 모든 개체를 덤프합니다. 예를 들면 다음과 같습니다.

```console
         Address               MT     Size
000002b78000ce40 00007ffadc93a288       48     
000002b78000ceb0 00007ffadc93a218       24     

Statistics:
              MT    Count    TotalSize Class Name
00007ffadc93a218        1           24 System.Reflection.LoaderAllocatorScout
00007ffadc93a288        1           48 System.Reflection.LoaderAllocator
Total 2 objects
```

아래 “통계” 파트에서 주의해야 할 개체인 `System.Reflection.LoaderAllocator`에 속한 `MT`(`MethodTable`)을 확인합니다. 그런 다음 시작 부분에 있는 목록에서 해당 항목과 일치하는 `MT`가 있는 항목을 찾아 개체 자체의 주소를 가져옵니다. 이 경우 “000002b78000ce40”임

이제 `LoaderAllocator` 개체의 주소를 알고 있으므로 다른 명령을 사용하여 GC 루트를 찾을 수 있음

```console
!gcroot -all 0x000002b78000ce40 
```

이 명령은 `LoaderAllocator` 인스턴스를 초래하는 개체 참조의 체인을 덤프합니다. 이 목록은 `LoaderAllocator`를 활성 상태로 유지하므로 디버깅하는 문제의 핵심이 되는 엔터티인 루트로 시작합니다. 루트는 스택 슬롯, 프로세서 레지스터, GC 핸들 또는 정적 변수일 수 있습니다.

다음은 `gcroot` 명령 출력의 예입니다.

```console
Thread 4ac:
    000000cf9499dd20 00007ffa7d0236bc example.Program.Main(System.String[]) [E:\unloadability\example\Program.cs @ 70]
        rbp-20: 000000cf9499dd90
            ->  000002b78000d328 System.Reflection.RuntimeMethodInfo
            ->  000002b78000d1f8 System.RuntimeType+RuntimeTypeCache
            ->  000002b78000d1d0 System.RuntimeType
            ->  000002b78000ce40 System.Reflection.LoaderAllocator

HandleTable:
    000002b7f8a81198 (strong handle)
    -> 000002b78000d948 test.Test
    -> 000002b78000ce40 System.Reflection.LoaderAllocator

    000002b7f8a815f8 (pinned handle)
    -> 000002b790001038 System.Object[]
    -> 000002b78000d390 example.TestInfo
    -> 000002b78000d328 System.Reflection.RuntimeMethodInfo
    -> 000002b78000d1f8 System.RuntimeType+RuntimeTypeCache
    -> 000002b78000d1d0 System.RuntimeType
    -> 000002b78000ce40 System.Reflection.LoaderAllocator

Found 3 roots.
```

이제 해결할 수 있도록 루트의 위치를 파악해야 합니다. 가장 쉬운 사례는 루트가 스택 슬롯 또는 프로세서 레지스터인 경우입니다. 이 경우 `gcroot`는 프레임에 해당 함수를 실행하는 루트 및 스레드가 포함된 함수의 이름을 표시합니다. 루트가 정적 변수이거나 GC 핸들인 경우 해결하기가 어렵습니다. 

이전 예제에서 첫 번째 루트는 `rbp-20` 주소(여기서 `rbp`는 프로세서 레지스터 `rbp`이고 -20은 해당 레지스터로부터의 16진수 오프셋임)에서 `example.Program.Main(System.String[])` 함수의 프레임에 저장된 `System.Reflection.RuntimeMethodInfo` 형식의 로컬입니다.

두 번째 루트는 `test.Test` 클래스의 인스턴스에 대한 참조를 보유하는 기본 (강력) `GCHandle`입니다. 

세 번째 루트는 고정된 `GCHandle`입니다. 실제로는 정적 변수입니다. 아쉽게도 확인할 방법이 없습니다. 참조 형식의 정적은 내부 런타임 구조체의 관리형 개체 배열에 저장됩니다.

`AssemblyLoadContext`를 언로드하지 못하게 하는 또 다른 경우는 스레드에 스택의 `AssemblyLoadContext`에 로드된 어셈블리의 메서드 프레임이 있는 경우입니다. 모든 스레드의 관리형 호출 스택을 덤프하여 확인할 수 있습니다.

```console
~*e !clrstack
```

명령은 “모든 스레드에 `!clrstack` 명령 적용”을 의미합니다. 다음은 예제에 대한 해당 명령의 출력입니다. 안타깝게도 Unix의 LLDB에서는 모든 스레드에 명령을 적용할 수 있는 방법이 없으므로 수동으로 스레드를 전환하고 `clrstack` 명령을 반복해야 합니다.
디버거가 “관리형 스택을 탐색할 수 없습니다”라고 표시하는 경우 모든 스레드를 무시합니다.

```console
OS Thread Id: 0x6ba8 (0)
        Child SP               IP Call Site
0000001fc697d5c8 00007ffb50d9de12 [HelperMethodFrame: 0000001fc697d5c8] System.Diagnostics.Debugger.BreakInternal()
0000001fc697d6d0 00007ffa864765fa System.Diagnostics.Debugger.Break()
0000001fc697d700 00007ffa864736bc example.Program.Main(System.String[]) [E:\unloadability\example\Program.cs @ 70]
0000001fc697d998 00007ffae5fdc1e3 [GCFrame: 0000001fc697d998] 
0000001fc697df28 00007ffae5fdc1e3 [GCFrame: 0000001fc697df28] 
OS Thread Id: 0x2ae4 (1)
Unable to walk the managed stack. The current thread is likely not a 
managed thread. You can run !threads to get a list of managed threads in
the process
Failed to start stack walk: 80070057
OS Thread Id: 0x61a4 (2)
Unable to walk the managed stack. The current thread is likely not a 
managed thread. You can run !threads to get a list of managed threads in
the process
Failed to start stack walk: 80070057
OS Thread Id: 0x7fdc (3)
Unable to walk the managed stack. The current thread is likely not a 
managed thread. You can run !threads to get a list of managed threads in
the process
Failed to start stack walk: 80070057
OS Thread Id: 0x5390 (4)
Unable to walk the managed stack. The current thread is likely not a 
managed thread. You can run !threads to get a list of managed threads in
the process
Failed to start stack walk: 80070057
OS Thread Id: 0x5ec8 (5)
        Child SP               IP Call Site
0000001fc70ff6e0 00007ffb5437f6e4 [DebuggerU2MCatchHandlerFrame: 0000001fc70ff6e0] 
OS Thread Id: 0x4624 (6)
        Child SP               IP Call Site
GetFrameContext failed: 1
0000000000000000 0000000000000000 
OS Thread Id: 0x60bc (7)
        Child SP               IP Call Site
0000001fc727f158 00007ffb5437fce4 [HelperMethodFrame: 0000001fc727f158] System.Threading.Thread.SleepInternal(Int32)
0000001fc727f260 00007ffb37ea7c2b System.Threading.Thread.Sleep(Int32)
0000001fc727f290 00007ffa865005b3 test.Program.ThreadProc() [E:\unloadability\test\Program.cs @ 17]
0000001fc727f2c0 00007ffb37ea6a5b System.Threading.Thread.ThreadMain_ThreadStart()
0000001fc727f2f0 00007ffadbc4cbe3 System.Threading.ExecutionContext.RunInternal(System.Threading.ExecutionContext, System.Threading.ContextCallback, System.Object)
0000001fc727f568 00007ffae5fdc1e3 [GCFrame: 0000001fc727f568] 
0000001fc727f7f0 00007ffae5fdc1e3 [DebuggerU2MCatchHandlerFrame: 0000001fc727f7f0] 

```

여기에서 볼 수 있듯이 마지막 스레드에는 `test.Program.ThreadProc()`가 있습니다. 이 함수는 `AssemblyLoadContext`에 로드된 어셈블리의 함수이므로 `AssemblyLoadContext`를 활성 상태로 유지합니다.

## <a name="example-source-with-unloadability-issues"></a>로드 불가능 문제가 있는 소스 예제

다음 코드는 이전 디버깅 예제에서 사용됩니다.

### <a name="main-testing-program"></a>기본 테스트 프로그램

[!code-csharp[Main testing program](~/samples/snippets/standard/assembly/unloading/unloadability_issues_example_main.cs)]

## <a name="program-loaded-into-the-testassemblyloadcontext"></a>TestAssemblyLoadContext에 로드된 프로그램

다음 코드는 기본 테스트 프로그램의 `ExecuteAndUnload` 메서드에 전달되는 *test.dll*을 나타냅니다.

[!code-csharp[Program loaded into the TestAssemblyLoadContext](~/samples/snippets/standard/assembly/unloading/unloadability_issues_example_test.cs)]
