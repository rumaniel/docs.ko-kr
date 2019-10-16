---
title: Async(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Async
helpviewer_keywords:
- Async [Visual Basic]
- Async keyword [Visual Basic]
ms.assetid: 1be8b4b5-9689-41b5-bd33-b906bfd53bc5
ms.openlocfilehash: 6a3d9c8eb8e5929796683bd0bb50159ca0c69f1f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959865"
---
# <a name="async-visual-basic"></a>Async(Visual Basic)
한정자 `Async` 는 수정 하는 메서드 또는 [람다 식이](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md) 비동기 임을 나타냅니다. 이러한 메서드를 *비동기 메서드*라고 합니다.  
  
 비동기 메서드는 호출자의 스레드를 차단하지 않고 오래 실행될 수 있는 작업을 수행하는 편리한 방법을 제공합니다. 비동기 메서드의 호출자는 비동기 메서드가 완료 될 때까지 기다리지 않고 작업을 다시 시작할 수 있습니다.  
  
> [!NOTE]
> `Async` 및 `Await` 키워드는 Visual Studio 2012에서 도입되었습니다. 비동기 프로그래밍에 대 한 소개는 [async 및 wait를 사용한 비동기 프로그래밍](../../../visual-basic/programming-guide/concepts/async/index.md)을 참조 하세요.  
  
 다음 예제에서는 비동기 메서드의 구조를 보여줍니다. 규칙에 따라 비동기 메서드는 "Async"로 끝납니다.  
  
```vb  
Public Async Function ExampleMethodAsync() As Task(Of Integer)  
    ' . . .  
  
    ' At the Await expression, execution in this method is suspended and,  
    ' if AwaitedProcessAsync has not already finished, control returns  
    ' to the caller of ExampleMethodAsync. When the awaited task is   
    ' completed, this method resumes execution.   
    Dim exampleInt As Integer = Await AwaitedProcessAsync()  
  
    ' . . .  
  
    ' The return statement completes the task. Any method that is   
    ' awaiting ExampleMethodAsync can now get the integer result.  
    Return exampleInt  
End Function  
```  
  
 일반적으로 `Async` 키워드에 의해 수정 된 메서드에 하나 이상의 [wait](../../../visual-basic/language-reference/modifiers/async.md) 식 또는 문이 포함 됩니다. 대기 중인 작업이 완료될 때까지 일시 중단된 지점인 첫 번째 `Await`에 도달할 때까지 이 메서드는 동기적으로 실행됩니다. 그리고 메서드의 호출자로 컨트롤이 반환됩니다. 메서드에 `Await` 식 혹은 문이 포함되지 않은 경우에는 메서드가 일시 중단되지 않고 동기 메서드와 같은 방식으로 실행됩니다. 이러한 상황에서 오류가 발생할 수 있으므로가 포함 `Await` 되지 않은 모든 비동기 메서드에 대 한 컴파일러 경고가 표시 됩니다. 자세한 내용은 [컴파일러 오류](../../../visual-basic/language-reference/error-messages/because-this-call-is-not-awaited-the-current-method-continues-to-run.md)를 참조 하세요.  
  
 `Async` 키워드는 예약되지 않은 키워드입니다. 이 키워드는 메서드 또는 람다 식을 수정할 때의 키워드입니다. 다른 모든 컨텍스트에서는 식별자로 해석됩니다.  
  
## <a name="return-types"></a>반환 형식  
 비동기 메서드는 [Sub](../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 프로시저 이거나 <xref:System.Threading.Tasks.Task> 반환 형식이 또는 <xref:System.Threading.Tasks.Task%601>인 [함수](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md) 프로시저입니다. 메서드는 [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) 매개 변수를 선언할 수 없습니다.  
  
 메서드의 [return](../../../visual-basic/language-reference/statements/return-statement.md) 문에 TResult 형식의 피연산자가 있는 경우 비동기 메서드의 반환 형식으로 `Task(Of TResult)`를 지정합니다. 메서드가 완료되었을 때 의미 있는 값이 반환되지 않을 경우 `Task`를 사용합니다. 즉, 메서드를 호출하면 `Task`가 반환되지만 `Task`가 완료된 경우 `Await`를 대기 중인 모든 `Task` 문이 결과 값을 생성하지 않습니다.  
  
 비동기 서브루틴은 `Sub` 프로시저가 필요한 이벤트 처리기를 정의하는 데 주로 사용됩니다. 비동기 서브 루틴의 호출자는 이를 기다릴 수 없으며, 메서드가 throw하는 예외를 catch할 수 없습니다.  
  
 자세한 내용과 예제는 [비동기 반환 형식](../../../visual-basic/programming-guide/concepts/async/async-return-types.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제는 비동기 이벤트 처리기, 비동기 람다 식 및 비동기 메서드를 보여줍니다. 이러한 요소를 사용 하는 전체 예제를 보려면 [연습: Async 및 Await를 사용하여 웹에 액세스](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)를 참조하세요. [Async Sample: Accessing the Web Walkthrough (C# and Visual Basic)](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)(비동기 샘플: 웹 액세스 연습(C# 및 Visual Basic))에서 연습 코드를 다운로드할 수 있습니다.  
  
```vb  
' An event handler must be a Sub procedure.  
Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
    textBox1.Clear()  
    ' SumPageSizesAsync is a method that returns a Task.  
    Await SumPageSizesAsync()  
    textBox1.Text = vbCrLf & "Control returned to button1_Click."  
End Sub  
  
' The following async lambda expression creates an equivalent anonymous  
' event handler.  
AddHandler button1.Click, Async Sub(sender, e)  
                              textBox1.Clear()  
                              ' SumPageSizesAsync is a method that returns a Task.  
                              Await SumPageSizesAsync()  
                              textBox1.Text = vbCrLf & "Control returned to button1_Click."  
                          End Sub  
  
' The following async method returns a Task(Of T).  
' A typical call awaits the Byte array result:  
'      Dim result As Byte() = Await GetURLContents("https://msdn.com")  
Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
  
    ' The downloaded resource ends up in the variable named content.  
    Dim content = New MemoryStream()  
  
    ' Initialize an HttpWebRequest for the current URL.  
    Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
    ' Send the request to the Internet resource and wait for  
    ' the response.  
    Using response As WebResponse = Await webReq.GetResponseAsync()  
        ' Get the data stream that is associated with the specified URL.  
        Using responseStream As Stream = response.GetResponseStream()  
            ' Read the bytes in responseStream and copy them to content.    
            ' CopyToAsync returns a Task, not a Task<T>.  
            Await responseStream.CopyToAsync(content)  
        End Using  
    End Using  
  
    ' Return the result as a byte array.  
    Return content.ToArray()  
End Function  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [Await 연산자](../../../visual-basic/language-reference/operators/await-operator.md)
- [Async 및 Await를 사용한 비동기 프로그래밍](../../../visual-basic/programming-guide/concepts/async/index.md)
- [연습: Async 및 Await를 사용하여 웹에 액세스](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
