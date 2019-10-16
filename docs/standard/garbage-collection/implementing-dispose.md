---
title: Dispose 메서드 구현
ms.date: 04/07/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- garbage collection, Dispose method
ms.assetid: eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 964c788c5fc1ac791ed3ddd20c9c5c972d07b2c1
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106883"
---
# <a name="implementing-a-dispose-method"></a>Dispose 메서드 구현

애플리케이션에서 사용되는 관리되지 않는 리소스를 해제하려면 <xref:System.IDisposable.Dispose%2A> 메서드를 구현합니다. .NET 가비지 수집기는 관리되지 않는 메모리를 할당하거나 해제하지 않습니다.  
  
[삭제 패턴](../../../docs/standard/design-guidelines/dispose-pattern.md)이라고도 하는 개체 삭제 패턴에서는 개체의 수명에 순서를 적용합니다. 삭제 패턴은 파일 핸들, 파이프 핸들, 레지스트리 핸들, 대기 핸들 또는 관리되지 않는 메모리의 블록에 대한 포인터와 같이 관리되지 않는 리소스에 액세스하는 개체에만 사용됩니다. 이는 가비지 수집기가 사용되지 않은 관리되는 개체를 회수하는 데 매우 효율적이지만, 관리되지 않는 개체는 회수할 수 없기 때문입니다.  
  
삭제 패턴에는 두 가지 변형이 있습니다.  
  
- 형식이 SafeHandle(즉, <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType>에서 파생된 클래스)에서 사용하는 관리되지 않는 리소스를 각각 래핑합니다. 이 경우 <xref:System.IDisposable> 인터페이스와 추가 `Dispose(Boolean)` 메서드를 구현합니다. 이는 권장되는 변형이며, <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 메서드를 재정의할 필요가 없습니다.  
  
  > [!NOTE]
  > <xref:Microsoft.Win32.SafeHandles?displayProperty=nameWithType> 네임스페이스는 <xref:System.Runtime.InteropServices.SafeHandle>에서 파생된 클래스 집합을 제공합니다(이러한 클래스는 [SafeHandle 사용](#SafeHandles) 섹션에 나열되어 있음). 관리되지 않는 리소스를 해제하는 데 적합한 클래스를 찾을 수 없는 경우 고유한 <xref:System.Runtime.InteropServices.SafeHandle> 서브클래스를 구현할 수 있습니다.  
  
- <xref:System.IDisposable> 인터페이스와 추가 `Dispose(Boolean)` 메서드를 구현하고 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 메서드도 재정의합니다. 형식의 소비자가 <xref:System.Object.Finalize%2A> 구현을 호출하지 않은 경우 관리되지 않는 리소스가 삭제되도록 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>를 재정의해야 합니다. 이전 글머리 기호에 설명된 권장 방법을 사용하는 경우 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 클래스가 사용자 대신 이 작업을 수행합니다.  
  
리소스가 항상 적절하게 정리되게 하려면 예외를 throw하지 않고 <xref:System.IDisposable.Dispose%2A> 메서드를 여러 번 호출해야 합니다.  
  
<xref:System.GC.KeepAlive%2A?displayProperty=nameWithType> 메서드의 코드 예제에서는 적극적인 가비지 수집으로 인해, 회수된 개체의 멤버가 아직 실행되는 동안 종료자가 실행되게 할 수 있는 방법을 보여 줍니다. <xref:System.GC.KeepAlive%2A> 메서드를 오래 실행한 후에는 <xref:System.IDisposable.Dispose%2A> 메서드를 호출하는 것이 좋습니다.  
  
<a name="Dispose2"></a>
## <a name="dispose-and-disposeboolean"></a>Dispose() 및 Dispose(Boolean)  

<xref:System.IDisposable> 인터페이스에서는 매개 변수가 없는 단일 메서드인 <xref:System.IDisposable.Dispose%2A>를 구현해야 합니다. 그러나 삭제 패턴을 사용하려면 다음과 같은 두 가지 `Dispose` 메서드를 구현해야 합니다.  
  
- 매개 변수가 없는 공용 비가상(Visual Basic의 `NonInheritable`) <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 구현  
  
- 시그니처가 다음과 같은 보호된 가상(Visual Basic의 `Overridable`) `Dispose` 메서드:  
  
  [!code-csharp[Conceptual.Disposable#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#8)]
  [!code-vb[Conceptual.Disposable#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#8)]  
  
### <a name="the-dispose-overload"></a>Dispose() 오버로드

공용, 비가상(Visual Basic의 경우 `NonInheritable`), 매개 변수가 없는 `Dispose` 메서드는 형식의 소비자에 의해 호출되므로, 관리되지 않는 리소스를 해제하고 종료자(있는 경우)를 실행할 필요가 없음을 나타내기 위한 것입니다. 이로 인해 다음과 같은 표준 구현이 수행됩니다.  
  
[!code-csharp[Conceptual.Disposable#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#7)]
[!code-vb[Conceptual.Disposable#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#7)]  
  
`Dispose` 메서드가 모든 개체를 정리하므로, 가비지 수집기가 더 이상 개체의 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 재정의를 호출할 필요가 없습니다. 따라서 <xref:System.GC.SuppressFinalize%2A> 메서드를 호출하면 가비지 수집기가 종료자를 실행하지 않도록 방지됩니다. 형식에 종료자가 없는 경우 <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>에 대한 호출이 영향을 미치지 않습니다. `Dispose` 메서드의 두 번째 오버로드에서 실제로 관리되지 않는 리소스를 해제하는 작업이 수행됩니다.  
  
### <a name="the-disposeboolean-overload"></a>Dispose(Boolean) 오버로드

두 번째 오버로드에서 *disposing* 매개 변수는 메서드 호출이 <xref:System.IDisposable.Dispose%2A> 메서드(값은 `true`)에서 수행되는지 또는 종료자(값은 `false`)에서 수행되는지를 나타내는 <xref:System.Boolean>입니다.  
  
메서드 본문은 다음과 같은 두 가지 코드 블록으로 구성됩니다.  
  
- 관리되지 않는 리소스를 해제하는 블록. 이 블록은 `disposing` 매개 변수의 값에 관계없이 실행됩니다.  
  
- 관리되는 리소스를 해제하는 조건부 블록. 이 블록은 `disposing` 값이 `true`인 경우 실행됩니다. 해제되는 관리되는 리소스는 다음과 같습니다.  
  
  **<xref:System.IDisposable>을 구현하는 관리되는 개체.** 조건부 블록을 사용하여 <xref:System.IDisposable.Dispose%2A> 구현을 호출할 수 있습니다. 관리되지 않는 리소스를 래핑하기 위해 SafeHandle을 사용한 경우 여기에서 <xref:System.Runtime.InteropServices.SafeHandle.Dispose%28System.Boolean%29?displayProperty=nameWithType> 구현을 호출해야 합니다.  
  
  **많은 메모리를 사용하거나 부족한 리소스를 사용하는 관리되는 개체.** 이러한 개체를 `Dispose` 메서드에서 명시적으로 해제하면 가비지 수집기에서 명확하지 않게 회수한 경우보다 빠르게 해제할 수 있습니다.  
  
메서드 호출이 종료자에서 나오는 경우, 즉 *disposing*이 `false`인 경우 관리되지 않는 리소스를 해제하는 코드만 실행됩니다. 종료하는 동안 가비지 수집기가 관리되는 개체를 제거하는 순서가 정의되어 있지 않기 때문에 `Dispose` 값으로 이 `false` 오버로드를 호출하면 종료자가 이미 회수된 관리되는 리소스를 해제하려고 시도하지 못합니다.  
  
## <a name="implementing-the-dispose-pattern-for-a-base-class"></a>기본 클래스에 대한 삭제 패턴 구현

기본 클래스에 대한 삭제 패턴을 구현하는 경우 다음을 제공해야 합니다.  
  
> [!IMPORTANT]
> <xref:System.IDisposable.Dispose>을 구현하고 `sealed`(Visual Basic의 경우 `NotInheritable`)가 아닌 모든 기본 클래스에 대해 이 패턴을 구현해야 합니다.  
  
- <xref:System.IDisposable.Dispose%2A> 메서드를 호출하는 `Dispose(Boolean)` 구현  
  
- 실제로 리소스를 해제하는 작업을 수행하는 `Dispose(Boolean)` 메서드  
  
- 관리되지 않는 리소스를 래핑하는 <xref:System.Runtime.InteropServices.SafeHandle>에서 파생된 클래스(권장) 또는 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 메서드 재정의 <xref:System.Runtime.InteropServices.SafeHandle> 클래스는 사용자가 코딩할 필요가 없는 종료자를 제공합니다.  
  
SafeHandle을 사용하는 기본 클래스에 대한 삭제 패턴을 구현하는 일반적인 패턴은 다음과 같습니다.  
  
[!code-csharp[System.IDisposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base1.cs#3)]
[!code-vb[System.IDisposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base1.vb#3)]  
  
> [!NOTE]
> 이전 예제에서는 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 개체를 사용하여 패턴을 보여 줍니다. <xref:System.Runtime.InteropServices.SafeHandle>에서 파생된 개체를 대신 사용할 수 있습니다. 예제에서는 해당 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 개체를 제대로 인스턴스화하지 않습니다.  
  
<xref:System.Object.Finalize%2A?displayProperty=nameWithType>를 재정의하는 기본 클래스에 대한 삭제 패턴을 구현하는 일반적인 패턴은 다음과 같습니다.  
  
[!code-csharp[System.IDisposable#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base2.cs#5)]
[!code-vb[System.IDisposable#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base2.vb#5)]  
  
> [!NOTE]
> C#에서 [소멸자](../../csharp/programming-guide/classes-and-structs/destructors.md)를 정의하여 <xref:System.Object.Finalize%2A?displayProperty=nameWithType>를 재정의합니다.  
  
## <a name="implementing-the-dispose-pattern-for-a-derived-class"></a>파생된 클래스에 대한 삭제 패턴 구현

<xref:System.IDisposable>의 기본 클래스 구현은 파생된 클래스에 의해 상속되므로 <xref:System.IDisposable> 인터페이스를 구현하는 클래스에서 파생된 클래스가 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>을 구현하지 않아야 합니다. 대신 파생된 클래스에 대한 삭제 패턴을 구현하려면 다음을 제공합니다.  
  
- 기본 클래스 메서드를 재정의하고 파생된 클래스의 리소스를 해제하는 실제 작업을 수행하는 `protected Dispose(Boolean)` 메서드. 또한 이 메서드는 기본 클래스의 `Dispose(Boolean)` 메서드를 호출하며 인수에 대해 삭제 중 상태를 전달합니다.  
  
- 관리되지 않는 리소스를 래핑하는 <xref:System.Runtime.InteropServices.SafeHandle>에서 파생된 클래스(권장) 또는 <xref:System.Object.Finalize%2A?displayProperty=nameWithType> 메서드 재정의 <xref:System.Runtime.InteropServices.SafeHandle> 클래스는 사용자가 코딩할 필요가 없는 종료자를 제공합니다. 종료자를 제공하는 경우 *disposing* 인수가 `false`인 `Dispose(Boolean)` 오버로드를 호출해야 합니다.  
  
SafeHandle을 사용하는 파생된 클래스에 대한 삭제 패턴을 구현하는 일반적인 패턴은 다음과 같습니다.  
  
[!code-csharp[System.IDisposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived1.cs#4)]
[!code-vb[System.IDisposable#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived1.vb#4)]  
  
> [!NOTE]
> 이전 예제에서는 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 개체를 사용하여 패턴을 보여 줍니다. <xref:System.Runtime.InteropServices.SafeHandle>에서 파생된 개체를 대신 사용할 수 있습니다. 예제에서는 해당 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 개체를 제대로 인스턴스화하지 않습니다.  
  
<xref:System.Object.Finalize%2A?displayProperty=nameWithType>를 재정의하는 파생된 클래스에 대한 삭제 패턴을 구현하는 일반적인 패턴은 다음과 같습니다.  
  
[!code-csharp[System.IDisposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived2.cs#6)]
[!code-vb[System.IDisposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived2.vb#6)]  
  
> [!NOTE]
> C#에서 [소멸자](../../csharp/programming-guide/classes-and-structs/destructors.md)를 정의하여 <xref:System.Object.Finalize%2A?displayProperty=nameWithType>를 재정의합니다.  
  
<a name="SafeHandles"></a>   
## <a name="using-safe-handles"></a>SafeHandle 사용

개체 종료자에 대한 코드를 작성하는 작업은 올바르게 수행되지 않을 경우 문제를 일으킬 수 있는 복잡한 작업입니다. 따라서 종료자를 구현하는 대신 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 개체를 생성하는 것이 좋습니다.  
  
<xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType> 클래스에서 파생된 클래스는 중단 없이 핸들을 할당 및 해제하여 개체 수명 문제를 단순화합니다. 여기에는 애플리케이션 도메인을 언로드하는 동안 실행이 보장되는 중요한 종료자가 포함됩니다. SafeHandle을 사용하는 이점에 대한 자세한 내용은 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType>를 참조하세요. <xref:Microsoft.Win32.SafeHandles> 네임스페이스에서 다음과 같은 파생된 클래스가 SafeHandle을 제공합니다.  
  
- 파일, 메모리 매핑된 파일 및 파이프에 대한 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>, <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle> 및 <xref:Microsoft.Win32.SafeHandles.SafePipeHandle> 클래스  
  
- 메모리 뷰에 대한 <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle> 클래스  
  
- 암호화 구문에 대한 <xref:Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle>, <xref:Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle> 및 <xref:Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle> 클래스  
  
- 레지스트리 키에 대한 <xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle> 클래스  
  
- 대기 핸들에 대한 <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> 클래스  
  
<a name="base"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-base-class"></a>SafeHandle을 사용하여 기본 클래스에 대한 삭제 패턴 구현

다음 예제는 SafeHandle을 사용하여 관리되지 않는 리소스를 캡슐화하는 기본 클래스에 대한 삭제 패턴인 `DisposableStreamResource`를 보여 줍니다. 이는 `DisposableResource`을 사용하여 열려 있는 파일을 나타내는 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 개체를 래핑하는 <xref:System.IO.Stream> 클래스를 정의합니다. 또한 `DisposableResource` 메서드에는 파일 스트림에서 총 바이트 수를 반환하는 단일 속성인 `Size`도 포함됩니다.  
  
[!code-csharp[Conceptual.Disposable#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/base1.cs#9)]
[!code-vb[Conceptual.Disposable#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/base1.vb#9)]  
  
<a name="derived"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-derived-class"></a>SafeHandle을 사용하여 파생된 클래스에 대한 삭제 패턴 구현

다음 예제는 이전 예제에 제공된 `DisposableStreamResource2` 클래스에서 상속되는 파생된 클래스에 대한 삭제 패턴인 `DisposableStreamResource`를 보여 줍니다. 클래스에서 추가 메서드인 `WriteFileInfo`를 추가하고 <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> 개체를 사용하여 쓰기 가능 파일의 핸들을 래핑합니다.  
  
[!code-csharp[Conceptual.Disposable#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/derived1.cs#10)]
[!code-vb[Conceptual.Disposable#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/derived1.vb#10)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.GC.SuppressFinalize%2A>
- <xref:System.IDisposable>
- <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>
- <xref:Microsoft.Win32.SafeHandles>
- <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=nameWithType>
- <xref:System.Object.Finalize%2A?displayProperty=nameWithType>
- [방법: 클래스 및 구조체 정의 및 사용(C++/CLI)](/cpp/dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli)
- [삭제 패턴](../../../docs/standard/design-guidelines/dispose-pattern.md)
