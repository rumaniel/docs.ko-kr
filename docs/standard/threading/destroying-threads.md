---
title: 스레드 제거
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- destroying threads
- threading [.NET Framework], destroying threads
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 986b4dee17c41928327e7b2672d641bbb8b16f1d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960084"
---
# <a name="destroying-threads"></a>스레드 제거
<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 메서드는 관리되는 스레드를 영구적으로 중지하는 데 사용됩니다. <xref:System.Threading.Thread.Abort%2A>를 호출할 때 공용 언어 런타임이 대상 스레드에서 <xref:System.Threading.ThreadAbortException>을 throw하며, 대상 스레드가 이를 catch할 수 있습니다. 자세한 내용은 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>을 참조하세요.  
  
> [!NOTE]
> <xref:System.Threading.Thread.Abort%2A> 메서드가 호출될 때 스레드가 비관리 코드를 실행하는 경우 런타임은 이를 <xref:System.Threading.ThreadState.AbortRequested?displayProperty=nameWithType>로 표시합니다. 스레드가 관리 코드로 돌아오면 예외가 throw됩니다.  
  
 스레드가 중단되면 다시 시작할 수 없습니다.  
  
 대상 스레드가 <xref:System.Threading.ThreadAbortException>를 catch하고 `finally` 블록에서 임의의 코드를 실행할 수 있으므로 <xref:System.Threading.Thread.Abort%2A> 메서드로 인해 스레드가 즉시 중단되지 않습니다. 스레드가 종료될 때까지 기다려야 하는 경우 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>을 호출할 수 있습니다. <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>은 스레드가 실제로 실행을 중지했거나 선택적 시간 제한 간격이 경과할 때까지 반환하지 않는 차단 호출입니다. 중단된 스레드는 <xref:System.Threading.Thread.ResetAbort%2A> 메서드를 호출하거나 `finally` 블록에서 제한 없는 처리를 수행할 수 있으므로 제한 시간을 지정하지 않으면 대기가 종료되지 않습니다.  
  
 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 메서드 호출을 대기 중인 스레드는 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>을 호출하는 다른 스레드에 의해 중단될 수 있습니다.  
  
## <a name="handling-threadabortexception"></a>ThreadAbortException 처리  
 자체 코드에서 <xref:System.Threading.Thread.Abort%2A>를 호출한 결과로 또는 스레드가 실행 중인 애플리케이션 도메인을 언로드한(<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType>에서 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>를 사용하여 스레드 종료) 결과로 스레드가 중단될 것으로 예상되는 경우 스레드에서 <xref:System.Threading.ThreadAbortException>을 처리하고 다음 코드와 같이 `finally` 절에서 최종 처리를 수행해야 합니다.  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.   
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception   
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try   
{  
    // Code that is executing when the thread is aborted.  
}   
catch (ThreadAbortException ex)   
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.   
}  
// Do not put clean-up code here, because the exception   
// is rethrown at the end of the Finally clause.  
```  
  
 <xref:System.Threading.ThreadAbortException>이 `finally` 절의 끝에서 또는 `finally` 절이 없는 경우 `catch` 절의 끝에서 시스템을 통해 다시 throw되므로 정리 코드가 `catch` 절 또는 `finally` 절에 있어야 합니다.  
  
 <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=nameWithType> 메서드를 호출하여 시스템이 예외를 다시 throw하지 않도록 할 수 있습니다. 그러나 사용자의 코드가 <xref:System.Threading.ThreadAbortException>을 발생시킨 경우에만 이를 수행해야 합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.ThreadAbortException>
- <xref:System.Threading.Thread>
- [스레드 및 스레딩 사용](../../../docs/standard/threading/using-threads-and-threading.md)
