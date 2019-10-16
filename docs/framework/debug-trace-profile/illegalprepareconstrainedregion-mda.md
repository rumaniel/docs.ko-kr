---
title: illegalPrepareConstrainedRegion MDA
ms.date: 03/30/2017
helpviewer_keywords:
- PrepareConstrainedRegions method
- managed debugging assistants (MDAs), illegal PrepareConstrainedRegions
- try/catch exception handling, managed debugging assistants
- IllegalPrepareConstrainedRegions MDA
- MDAs (managed debugging assistants), illegal PrepareConstrainedRegions
ms.assetid: 2f9b5031-f910-4e01-a196-f89eab313eaf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 623aff91eb801b4b32fc180bd97ed3822ad7f163
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052668"
---
# <a name="illegalprepareconstrainedregion-mda"></a>illegalPrepareConstrainedRegion MDA
`illegalPrepareConstrainedRegion` MDA(관리 디버깅 도우미)는 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A?displayProperty=nameWithType> 메서드가 예외 처리기의 `try` 문의 바로 앞에 호출되지 않을 경우 활성화됩니다. 이 제한은 MSIL 수준에 적용되므로 호출과 `try` 사이에 코드가 아닌 생성 소스(예: 주석)를 포함할 수 없습니다.  
  
## <a name="symptoms"></a>증상  
 CER(제약이 있는 실행 영역)이 이와 같이 처리되지 않고 간단한 예외 처리 블록(`finally` 또는 `catch`)으로 처리됩니다. 따라서 메모리 부족 조건 또는 스레드 중단이 발생할 경우 해당 영역이 실행되지 않습니다.  
  
## <a name="cause"></a>원인  
 CER에 대한 준비 패턴을 제대로 따르지 않았습니다.  이것은 오류 이벤트입니다. <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> 블록`catch` 에CER을/ 도입 하는 것 처럼 예외 처리기를 표시 하는 데 사용 되는 메서드 호출은 `finally` / `fault` / `filter` `try` 문.  
  
## <a name="resolution"></a>해결 방법  
 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> 호출이 `try` 문의 바로 앞에 실행되는지 확인합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 MDA는 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> 메서드를 호출하는 메서드 이름, MSIL 오프셋 및 호출이 try 블록 시작 부분의 바로 앞에 실행됨을 나타내는 메시지를 표시합니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <illegalPrepareConstrainedRegion/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 MDA를 활성화하는 패턴을 보여 줍니다.  
  
```csharp
void MethodWithInvalidPCR()  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    Object o = new Object();  
    try  
    {  
        …  
    }  
    finally  
    {  
        …  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
