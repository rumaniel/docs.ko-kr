---
title: reentrancy MDA
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged code, debugging
- transitioning threads unmanaged to managed code
- reentrancy MDA
- reentrancy without an orderly transition
- managed debugging assistants (MDAs), reentrancy
- illegal reentrancy
- MDAs (managed debugging assistants), reentrancy
- threading [.NET Framework], managed debugging assistants
- managed code, debugging
- native debugging, MDAs
ms.assetid: 7240c3f3-7df8-4b03-bbf1-17cdce142d45
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d14ba8724659172711da44e7bb249e9d20768dbc
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052333"
---
# <a name="reentrancy-mda"></a>reentrancy MDA
이전에 수행된 관리 코드에서 네이티브 코드로의 전환이 순서대로 수행되지 않은 경우 네이티브 코드에서 관리 코드로 전환하려고 하면 `reentrancy` MDA(관리 디버깅 도우미)가 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 네이티브 코드에서 관리 코드로 전환할 때 개체 힙이 손상되었거나 다른 심각한 오류가 발생합니다.  
  
 네이티브 코드와 관리 코드 사이에서 임의 방향으로 전환되는 스레드는 순차적 전환을 수행해야 합니다. 그러나 벡터화된 예외 처리기와 같이 운영 체제의 특정한 하위 수준 확장 지점을 사용하면, 순차적 전환을 수행하지 않고도 관리 코드에서 네이티브 코드로 전환할 수 있습니다.  이러한 전환은 CLR(공용 언어 런타임) 제어가 아니라 운영 체제의 제어에 따라 수행됩니다.  이러한 확장 지점 내에서 실행되는 모든 네이티브 코드는 관리 코드로 다시 호출되지 않아야 합니다.  
  
## <a name="cause"></a>원인  
 관리 코드를 실행하는 중에 벡터화된 예외 처리기와 같은 하위 수준 운영 체제 확장 지점이 활성화되었습니다.  확장 지점을 통해 호출된 애플리케이션 코드에서 관리 코드를 다시 호출하려고 합니다.  
  
 이 문제는 항상 애플리케이션 코드 때문에 발생합니다.  
  
## <a name="resolution"></a>해결  
 이 MDA가 활성화된 스레드의 스택 추적을 검사합니다.  스레드에서 관리 코드를 올바르지 않게 호출하려고 합니다.  스택 추적은 이 확장 지점, 이 확장 지점을 제공하는 운영 체제 코드 및 확장 지점으로 인해 중단된 관리 코드를 사용하여 애플리케이션 코드를 표시해야 합니다.  
  
 예를 들어 벡터화된 예외 처리기에서 관리 코드를 호출하려고 시도할 때 MDA가 활성화됩니다.  스택에 운영 체제 예외 처리 코드와 <xref:System.DivideByZeroException> 또는 <xref:System.AccessViolationException> 등의 예외를 트리거하는 관리 코드가 일부 표시됩니다.  
  
 이 예에서는 비관리 코드에서 완전히 벡터화된 예외 처리기를 구현하는 것이 올바른 해결 방법입니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 MDA에서 잘못된 재진입이 시도되고 있음을 보고합니다.  스레드 스택을 검사하여 이 문제가 발생하는 이유와 문제를 정정하는 방법을 판별해야 합니다. 다음은 샘플 출력입니다.  
  
```output
Additional Information: Attempting to call into managed code without   
transitioning out first.  Do not attempt to run managed code inside   
low-level native extensibility points. Managed Debugging Assistant   
'Reentrancy' has detected a problem in 'D:\ConsoleApplication1\  
ConsoleApplication1\bin\Debug\ConsoleApplication1.vshost.exe'.  
```  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    <reentrancy />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 코드 예제는 <xref:System.AccessViolationException>가 throw되는 원인이 됩니다.  따라서 벡터화된 예외 처리를 지원하는 Windows 버전에서 관리되는 벡터화된 예외 처리기가 호출됩니다.  `reentrancy` MDA가 사용되면 운영 체제의 벡터화된 예외 처리 지원 코드에서 `MyHandler`를 호출하려는 동안 MDA가 활성화됩니다.  
  
```csharp
using System;  
public delegate int ExceptionHandler(IntPtr ptrExceptionInfo);  
  
public class Reenter   
{  
    public static ExceptionHandler keepAlive;  
  
    [System.Runtime.InteropServices.DllImport("kernel32", ExactSpelling=true,   
        CharSet=System.Runtime.InteropServices.CharSet.Auto)]  
    public static extern IntPtr AddVectoredExceptionHandler(int bFirst,   
        ExceptionHandler handler);  
  
    static int MyHandler(IntPtr ptrExceptionInfo)   
    {  
        // EXCEPTION_CONTINUE_SEARCH  
        return 0;  
    }  
    void Run() {}  
  
    static void Main()   
    {  
        keepAlive = new ExceptionHandler(Reenter.MyHandler);  
        IntPtr ret = AddVectoredExceptionHandler(1, keepAlive);  
        try   
        {  
            // Dispatch on null should AV.  
            Reenter r = null;   
            r.Run();  
        }   
        catch { }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
