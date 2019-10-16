---
title: bindingFailure MDA
ms.date: 03/30/2017
helpviewer_keywords:
- binding failure
- binding, failures
- MDAs (managed debugging assistants), binding failures
- assemblies [.NET Framework], binding failures
- managed debugging assistants (MDAs), binding failures
- BindingFailure MDA
ms.assetid: 26ada5af-175c-4576-931a-9f07fa1723e9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 93c426cce792c8f30a3551e2d4626736dd67278f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052953"
---
# <a name="bindingfailure-mda"></a>bindingFailure MDA

`bindingFailure` MDA(관리 디버깅 도우미)는 어셈블리 로드에 실패할 때 활성화됩니다.

## <a name="symptoms"></a>증상

코드에서 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 또는 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 같은 로더 메서드 중 하나 또는 정적 참조를 사용하여 어셈블리를 로드하려고 했습니다. 어셈블리가 로드되지 않고 <xref:System.IO.FileNotFoundException> 또는 <xref:System.IO.FileLoadException> 예외가 throw됩니다.

## <a name="cause"></a>원인

바인딩 실패는 런타임이 어셈블리를 로드할 수 없는 경우에 발생합니다. 바인딩 실패는 다음과 같은 상황 중 하나의 결과일 수 있습니다.

- CLR(공용 언어 런타임)이 요청된 어셈블리를 찾을 수 없습니다. 이 문제는 어셈블리가 설치되지 않음, 애플리케이션이 어셈블리를 찾도록 올바르게 구성되지 않음 등 여러 가지 이유로 발생할 수 있습니다.

- 일반적인 문제 시나리오는 다른 애플리케이션 도메인에 형식을 전달하여 CLR이 다른 애플리케이션 도메인에서 해당 형식을 포함하는 어셈블리를 로드해야 하는 경우입니다. 다른 애플리케이션 도메인이 원래 애플리케이션 도메인과 다르게 구성된 경우 런타임이 어셈블리를 로드하지 못할 수 있습니다. 예를 들어 두 애플리케이션 도메인이 서로 다른 <xref:System.AppDomain.BaseDirectory%2A> 속성 값을 가질 수 있습니다.

- 요청된 어셈블리가 손상되었거나 어셈블리가 아닙니다.

- 어셈블리를 로드하려는 코드에 어셈블리를 로드할 수 있는 올바른 코드 액세스 보안 권한이 없습니다.

- 사용자 자격 증명이 파일을 읽는 데 필요한 권한을 제공하지 않습니다.

## <a name="resolution"></a>해결

첫 번째 단계는 CLR이 요청된 어셈블리에 바인딩할 수 없는 이유를 확인하는 것입니다. 런타임이 원인 섹션에 나열된 시나리오 같이 요청된 어셈블리를 찾거나 로드할 수 없는 많은 이유가 있습니다. 바인딩 실패의 원인을 제거하기 위해 다음 작업이 권장됩니다.

- `bindingFailure` MDA에서 제공하는 데이터를 사용하여 원인 확인:

  - [Fuslogvw.exe(어셈블리 바인딩 로그 뷰어)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md)를 실행하여 어셈블리 바인더를 통해 생성된 오류 로그를 확인합니다.

  - 어셈블리가 요청된 위치에 있는지 확인합니다. <xref:System.Reflection.Assembly.LoadFrom%2A> 및 <xref:System.Reflection.Assembly.LoadFile%2A> 메서드의 경우 요청된 위치를 쉽게 확인할 수 있습니다. 어셈블리 ID를 사용하여 바인딩하는 <xref:System.Reflection.Assembly.Load%2A> 메서드의 경우 애플리케이션 도메인의 <xref:System.AppDomain.BaseDirectory%2A> 속성 프로브 경로와 전역 어셈블리 캐시에서 해당 ID와 일치하는 어셈블리를 찾아야 합니다.

- 위의 확인에 따라 원인을 해결합니다. 가능한 해결 옵션은 다음과 같습니다.

  - 전역 어셈블리 캐시에 요청된 어셈블리를 설치하고 <xref:System.Reflection.Assembly.Load%2A> 메서드를 호출하여 ID로 어셈블리를 로드합니다.

  - 요청된 어셈블리를 애플리케이션 디렉터리에 복사하고 <xref:System.Reflection.Assembly.Load%2A> 메서드를 호출하여 ID로 어셈블리를 로드합니다.

  - <xref:System.AppDomain.BaseDirectory%2A> 속성을 변경하거나 전용 검색 경로를 추가하여 바인딩 실패가 발생한 응용 프로그램 도메인에 어셈블리 경로가 포함되도록 다시 구성합니다.

  - 로그온한 사용자가 파일을 읽을 수 있도록 파일에 대한 액세스 제어 목록을 변경합니다.

## <a name="effect-on-the-runtime"></a>런타임에 대한 영향

이 MDA는 CLR에 아무런 영향을 미치지 않습니다. 바인딩 실패에 대한 데이터를 보고만 합니다.

## <a name="output"></a>출력

MDA가 요청된 경로 및/또는 표시 이름, 바인딩 컨텍스트, 로드가 요청된 애플리케이션 도메인, 실패 이유를 포함하여 로드하지 못한 어셈블리를 보고합니다.

CLR이 해당 데이터를 사용할 수 없는 경우 표시 이름이나 요청된 경로가 비어 있을 수 있습니다. <xref:System.Reflection.Assembly.Load%2A> 메서드 호출이 실패한 경우 런타임이 어셈블리의 표시 이름을 확인할 수 없어 실패했을 가능성이 큽니다.

## <a name="configuration"></a>구성하기

```xml
<mdaConfig>
  <assistants>
    <bindingFailure />
  </assistants>
</mdaConfig>
```

## <a name="example"></a>예제

다음 코드 예제에서는 이 MDA를 활성화할 수 있는 상황을 보여 줍니다.

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.Reflection;
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // This call attempts to load a nonexistent assembly.
            // The call will throw a System.IO.FileNotFound exception
            // and cause the activation of the bindingFailure MDA
            // if it is registered.
            Assembly.Load("NonExistentAssembly");
        }
    }
}
```

## <a name="see-also"></a>참고자료

- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
