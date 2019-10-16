---
title: Await 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Await
helpviewer_keywords:
- Await operator [Visual Basic]
- Await [Visual Basic]
ms.assetid: 6b1ce283-e92b-4ba7-b081-7be7b3d37af9
ms.openlocfilehash: d3bfafaa696955422c381aa1c17bc96591b44985
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962005"
---
# <a name="await-operator-visual-basic"></a>Await 연산자(Visual Basic)
대기 중인 작업이 완료될 때까지 메서드 실행을 일시 중단하려면 비동기 메서드 또는 람다 식의 피연산자에 `Await` 연산자를 적용합니다. 작업은 진행 중인 작업을 나타냅니다.  
  
 `Await` 이 사용 되는 메서드에는 [비동기](../../../visual-basic/language-reference/modifiers/async.md) 한정자가 있어야 합니다. `Async` 한정자를 사용하여 정의하고 일반적으로 하나 이상의 `Await` 식을 포함하는 이러한 메서드를 *비동기 메서드*라고 합니다.  
  
> [!NOTE]
> `Async` 및 `Await` 키워드는 Visual Studio 2012에서 도입되었습니다. 비동기 프로그래밍에 대 한 소개는 [async 및 wait를 사용한 비동기 프로그래밍](../../../visual-basic/programming-guide/concepts/async/index.md)을 참조 하세요.  
  
 일반적으로 `Await` 연산자를 적용 하는 작업은 [작업 기반 비동기 패턴](https://go.microsoft.com/fwlink/?LinkId=204847)을 구현 하는 메서드 (즉 <xref:System.Threading.Tasks.Task> <xref:System.Threading.Tasks.Task%601>, 또는)에 대 한 호출의 반환 값입니다.  
  
 다음 코드에서 <xref:System.Net.Http.HttpClient> 메서드 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>는 `getContentsTask`, `Task(Of Byte())`를 반환합니다. 이 작업은 작업이 완료될 때 실제 바이트 배열을 생성하기 위한 약속입니다. `Await` 연산자는 `getContentsTask`에 적용되어 `getContentsTask`가 완료될 때까지 `SumPageSizesAsync`의 실행을 일시 중단합니다. 동시에 컨트롤은 `SumPageSizesAsync` 호출자에게 반환됩니다. `getContentsTask`가 완료되면 `Await` 식이 바이트 배열로 계산됩니다.  
  
```vb  
Private Async Function SumPageSizesAsync() As Task  
  
    ' To use the HttpClient type in desktop apps, you must include a using directive and add a   
    ' reference for the System.Net.Http namespace.  
    Dim client As HttpClient = New HttpClient()   
    ' . . .   
    Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)  
    Dim urlContents As Byte() = Await getContentsTask  
  
    ' Equivalently, now that you see how it works, you can write the same thing in a single line.  
    'Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
    ' . . .  
End Function  
```  
  
> [!IMPORTANT]
> 전체 예제를 보려면 [연습: Async 및 Await를 사용하여 웹에 액세스](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)를 참조하세요. 샘플은 Microsoft 웹 사이트의 [Async Sample: Accessing the Web Walkthrough (C# and Visual Basic)](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)(비동기 샘플: 웹 액세스 연습(C# 및 Visual Basic))에서 다운로드할 수 있습니다. 예제는 AsyncWalkthrough_HttpClient 프로젝트에 있습니다.  
  
 `Await`가 `Task(Of TResult)`를 반환하는 메서드 호출의 결과에 적용되는 경우, `Await`식의 형식은 TResult입니다. `Await`가 `Task`를 반환하는 메서드 호출의 결과에 적용되는 경우, `Await`식은 값을 반환하지 않습니다. 다음 예제에서 차이점을 보여 줍니다.  
  
```vb  
' Await used with a method that returns a Task(Of TResult).  
Dim result As TResult = Await AsyncMethodThatReturnsTaskTResult()  
  
' Await used with a method that returns a Task.  
Await AsyncMethodThatReturnsTask()  
```  
  
 `Await` 식 또는 문은 식이 실행되고 있는 스레드를 차단하지 않습니다. 대신 `Await` 식 이후 컴파일러가 대기 중인 작업에서 연속된 작업으로 비동기 메서드의 나머지 부분을 등록하게 됩니다. 그런 다음 컨트롤이 비동기 메서드 호출자에게 반환됩니다. 작업이 완료되면 해당 연속 작업이 호출되고 중단된 비동기 메서드의 실행이 다시 시작됩니다.  
  
 `Await` 식은 `Async` 수정자로 표시된 람다 식 또는 바로 바깥쪽에 있는 메서드의 본문에만 발생할 수 있습니다. *Wait* 라는 용어는 해당 컨텍스트에서만 키워드 역할을 합니다. 다른 컨텍스트에서는 식별자로 해석됩니다. 비동기 메서드 또는 람다 식 `Await` 내에서 식은 쿼리 식 `catch` `finally` 에서 발생할 수 없습니다. [ Catch ... Finally](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md) 문, `For` 또는 `For Each` 루프의 루프 제어 변수 식이나 [SyncLock](../../../visual-basic/language-reference/statements/synclock-statement.md) 문의 본문에 있습니다.  
  
## <a name="exceptions"></a>예외  
 대부분의 비동기 메서드는 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>를 반환합니다. 반환된 작업의 속성은 작업의 완료 여부, 비동기 메서드가 예외를 발생시켰는지 취소되었는지 여부 및 최종 결과 등 해당 상태 및 기록에 대한 정보를 전달합니다. `Await` 연산자는 해당 속성에 액세스합니다.  
  
 예외를 발생시키는 작업 반환 비동기 메서드를 기다릴 경우 `Await` 연산자는 예외를 다시 throw합니다.  
  
 취소된 작업 반환 비동기 메서드를 기다릴 경우 `Await` 연산자는 <xref:System.OperationCanceledException>을 다시 throw합니다.  
  
 오류가 발생한 상태의 단일 작업에는 여러 예외가 반영될 수 있습니다.  예를 들어 작업은 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 호출의 결과일 수 있습니다. 이러한 작업을 기다릴 경우 await 작업에서 예외 중 하나만 다시 throw합니다. 그러나 다시 throw되는 예외를 예측할 수 없습니다.  
  
 비동기 메서드에서 오류 처리에 대 한 예제를 보려면 [Try ... Catch ... Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## <a name="example"></a>예제  
 다음 Windows Forms 예제에서는 비동기 메서드 `WaitAsynchronouslyAsync`에서 `Await`의 사용을 보여 줍니다. 해당 메서드의 동작을 `WaitSynchronously`의 동작과 대조합니다. `Await` 연산자가 없는 경우 `WaitSynchronously`는 해당 정의에 `Async` 수정자가 사용되었고 해당 본문에서 <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> 호출이 있더라도 동기적으로 실행됩니다.  
  
```vb  
Private Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
    ' Call the method that runs asynchronously.  
    Dim result As String = Await WaitAsynchronouslyAsync()  
  
    ' Call the method that runs synchronously.  
    'Dim result As String = Await WaitSynchronously()  
  
    ' Display the result.  
    TextBox1.Text &= result  
End Sub  
  
' The following method runs asynchronously. The UI thread is not  
' blocked during the delay. You can move or resize the Form1 window   
' while Task.Delay is running.  
Public Async Function WaitAsynchronouslyAsync() As Task(Of String)  
    Await Task.Delay(10000)  
    Return "Finished"  
End Function  
  
' The following method runs synchronously, despite the use of Async.  
' You cannot move or resize the Form1 window while Thread.Sleep  
' is running because the UI thread is blocked.  
Public Async Function WaitSynchronously() As Task(Of String)  
    ' Import System.Threading for the Sleep method.  
    Thread.Sleep(10000)  
    Return "Finished"  
End Function  
```  
  
## <a name="see-also"></a>참고자료

- [Async 및 Await를 사용한 비동기 프로그래밍](../../../visual-basic/programming-guide/concepts/async/index.md)
- [연습: Async 및 Await를 사용하여 웹에 액세스](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [비동기](../../../visual-basic/language-reference/modifiers/async.md)
