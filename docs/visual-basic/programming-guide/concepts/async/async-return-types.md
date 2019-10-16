---
title: 비동기 반환 형식 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 07890291-ee72-42d3-932a-fa4d312f2c60
ms.openlocfilehash: 387b75db3078afb92e6fc3ad7607b293abb0c851
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71351951"
---
# <a name="async-return-types-visual-basic"></a>비동기 반환 형식 (Visual Basic)
비동기 메서드에는 세 가지 가능한 반환 형식, 즉 <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task> 및 void가 있습니다. Visual Basic에서 void 반환 형식은 [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 프로시저로 작성합니다. 비동기 메서드에 대 한 자세한 내용은 [async 및 wait를 사용한 비동기 프로그래밍 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)을 참조 하세요.  
  
 다음 섹션 중 하나에서 각 반환 형식을 살펴보고 세 가지 형식 모두를 사용하는 전체 예제는 이 항목의 끝에 나와 있습니다.  
  
> [!NOTE]
> 예제를 실행하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치되어 있어야 합니다.  
  
## <a name="BKMK_TaskTReturnType"></a> Task(T) 반환 형식  
 <xref:System.Threading.Tasks.Task%601>반환 형식은 피연산자의 형식이 `TResult`인 [return](../../../../visual-basic/language-reference/statements/return-statement.md) 문이 포함 된 비동기 메서드에 사용됩니다.  
  
 다음 예제에서 `TaskOfT_MethodAsync` 비동기 메서드는 정수를 반환하는 return 문을 포함합니다. 따라서 메서드 선언은 `Task(Of Integer)`의 반환 형식을 지정해야 합니다.  
  
```vb  
' TASK(OF T) EXAMPLE  
Async Function TaskOfT_MethodAsync() As Task(Of Integer)  
  
    ' The body of an async method is expected to contain an awaited   
    ' asynchronous call.  
    ' Task.FromResult is a placeholder for actual work that returns a string.  
    Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())  
  
    ' The method then can process the result in some way.  
    Dim leisureHours As Integer  
    If today.First() = "S" Then  
        leisureHours = 16  
    Else  
        leisureHours = 5  
    End If  
  
    ' Because the return statement specifies an operand of type Integer, the   
    ' method must have a return type of Task(Of Integer).   
    Return leisureHours  
End Function  
```  
  
 `TaskOfT_MethodAsync`를 await 식 내에서 호출하면 await 식이 `TaskOfT_MethodAsync`에서 반환된 작업에 저장된 정수 값(`leisureHours` 값)을 검색합니다. Wait 식에 대 한 자세한 내용은 [Wait Operator](../../../../visual-basic/language-reference/operators/await-operator.md)를 참조 하세요.  
  
 다음 코드는 `TaskOfT_MethodAsync` 메서드를 호출하고 기다립니다. 결과는 `result1` 변수에 할당됩니다.  
  
```vb  
' Call and await the Task(Of T)-returning async method in the same statement.  
Dim result1 As Integer = Await TaskOfT_MethodAsync()  
```  
  
 다음 코드와 같이 `TaskOfT_MethodAsync` 호출을 `Await`의 적용과 구분하면 이 과정을 더욱 잘 이해할 수 있습니다. 곧바로 대기 상태가 되지 않는 `TaskOfT_MethodAsync` 메서드를 호출하면 메서드 선언에서 예상한 대로 `Task(Of Integer)`를 반환합니다. 예제에서 작업이 `integerTask` 변수에 할당됩니다. `integerTask`가 <xref:System.Threading.Tasks.Task%601>이기 때문에 `TResult` 형식의 <xref:System.Threading.Tasks.Task%601.Result> 속성을 포함합니다. 이 경우 TResult는 정수 형식을 나타냅니다. `Await`가 `integerTask`에 적용되는 경우 await 식은 `integerTask`의 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성 내용으로 평가됩니다. 값은 `result2` 변수에 할당됩니다.  
  
> [!WARNING]
> <xref:System.Threading.Tasks.Task%601.Result%2A> 속성은 차단 속성입니다. 해당 작업이 완료되기 전에 액세스하려고 하면, 작업이 완료되고 값을 사용할 수 있을 때까지 현재 활성화된 스레드가 차단됩니다. 대부분의 경우 속성에 직접 액세스하지 않고 `Await`를 사용하여 값에 액세스해야 합니다.  
  
```vb  
' Call and await in separate statements.  
Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()  
  
' You can do other work that does not rely on resultTask before awaiting.  
textBox1.Text &= String.Format("Application can continue working while the Task(Of T) runs. . . . " & vbCrLf)  
  
Dim result2 As Integer = Await integerTask  
```  
  
 다음 코드의 display 문은 `result1` 변수, `result2` 변수 및 `Result` 속성의 값이 동일한지 확인합니다. `Result` 속성은 차단 속성이므로 해당 작업이 대기 상태가 되기 전에 액세스하지 않아야 합니다.  
  
```vb  
' Display the values of the result1 variable, the result2 variable, and  
' the resultTask.Result property.  
textBox1.Text &= String.Format(vbCrLf & "Value of result1 variable:   {0}" & vbCrLf, result1)  
textBox1.Text &= String.Format("Value of result2 variable:   {0}" & vbCrLf, result2)  
textBox1.Text &= String.Format("Value of resultTask.Result:  {0}" & vbCrLf, integerTask.Result)  
```  
  
## <a name="BKMK_TaskReturnType"></a> Task 반환 형식  
 return 문을 포함하지 않거나 피연산자를 반환하지 않는 return 문을 포함하는 비동기 메서드에는 일반적으로 <xref:System.Threading.Tasks.Task>의 반환 형식이 있습니다. 이러한 메서드는 동기적으로 실행 되도록 작성 된 경우 [하위](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) 프로시저입니다. 비동기 메서드에 대해 `Task` 반환 형식을 사용하는 경우 호출된 비동기 메서드가 완료될 때까지 호출 메서드는 `Await` 연산자를 사용하여 호출자의 완료를 일시 중단할 수 있습니다.  
  
 다음 예제에서는 `Task_MethodAsync` 비동기 메서드가 return 문을 포함하지 않습니다. 따라서 이 메서드에 대해 `Task_MethodAsync`가 대기할 수 있도록 `Task`의 반환 형식을 지정합니다. `Task` 형식의 정의는 반환 값을 저장하기 위한 `Result` 속성을 포함하지 않습니다.  
  
```vb  
' TASK EXAMPLE  
Async Function Task_MethodAsync() As Task  
  
    ' The body of an async method is expected to contain an awaited   
    ' asynchronous call.  
    ' Task.Delay is a placeholder for actual work.  
    Await Task.Delay(2000)  
    textBox1.Text &= String.Format(vbCrLf & "Sorry for the delay. . . ." & vbCrLf)  
  
    ' This method has no return statement, so its return type is Task.   
End Function  
```  
  
 동기 `Sub` 또는 void를 반환하는 메서드에 대한 호출 문과 비슷하게 await 식 대신 await 문을 사용하여 `Task_MethodAsync`가 호출되고 대기됩니다. 이 경우 `Await` 연산자의 응용 프로그램은 값을 생성 하지 않습니다.  
  
 다음 코드는 `Task_MethodAsync` 메서드를 호출하고 기다립니다.  
  
```vb  
' Call and await the Task-returning async method in the same statement.  
Await Task_MethodAsync()  
```  
  
 이전 <xref:System.Threading.Tasks.Task%601> 예제와 같이 다음 코드와 같이 `Await` 연산자의 응용 프로그램 `Task_MethodAsync` 에서 호출을 분리할 수 있습니다. 그러나 `Task`에는 `Result` 속성이 없으므로 await 연산자가 `Task`에 적용될 때 값이 생성되지 않습니다.  
  
 다음 코드는 `Task_MethodAsync`가 반환하는 작업을 대기하는 것에서 `Task_MethodAsync` 호출을 구분합니다.  
  
```vb  
' Call and await in separate statements.  
Dim simpleTask As Task = Task_MethodAsync()  
  
' You can do other work that does not rely on simpleTask before awaiting.  
textBox1.Text &= String.Format(vbCrLf & "Application can continue working while the Task runs. . . ." & vbCrLf)  
  
Await simpleTask  
```  
  
## <a name="BKMK_VoidReturnType"></a> Void 반환 형식  
 프로시저의 `Sub` 주요 용도는 이벤트 처리기에 있습니다. 여기에는 반환 형식 (다른 언어에서는 void 반환 형식 이라고 함)이 없습니다. void 반환은 또한 "실행 후 제거"로 분류할 수 있는 작업을 수행하는 메서드 또는 viod를 반환하는 메서드를 재정의하는 데 사용할 수 있습니다. 하지만 void를 반환하는 비동기 메서드는 대기할 수가 없기 때문에 가능할 때마다 `Task`를 반환하는 것이 좋습니다. 이러한 메서드의 호출자는 호출된 비동기 메서드가 마치는 것을 기다리지 않고 완료될 때까지 계속 진행할 수 있어야 하므로, 해당 호출자는 비동기 메서드가 생성하는 모든 값 또는 예외와 독립되어 있어야 합니다.  
  
 void를 반환하는 비동기 메서드의 호출자는 메서드에서 throw되는 예외를 catch할 수 없으므로 이러한 처리되지 않은 예외를 사용하면 애플리케이션이 실패할 수 있습니다. <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>를 반환하는 비동기 메서드에서 예외가 발생하는 경우 이 예외는 반환된 작업에 저장되고 작업이 대기 상태일 때 다시 throw됩니다. 따라서 예외를 생성할 수 있는 모든 비동기 메서드에 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>의 반환 형식이 있고 메서드 호출이 대기 상태인지 확인해야 합니다.  
  
 비동기 메서드에서 예외를 catch하는 방법에 대한 자세한 내용은 [Try...Catch...Finally 문](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)을 참조하세요.  
  
 다음 코드는 비동기 이벤트 처리기를 정의합니다.  
  
```vb  
' SUB EXAMPLE  
Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
  
    textBox1.Clear()  
  
    ' Start the process and await its completion. DriverAsync is a   
    ' Task-returning async method.  
    Await DriverAsync()  
  
    ' Say goodbye.  
    textBox1.Text &= vbCrLf & "All done, exiting button-click event handler."  
End Sub  
```  
  
## <a name="BKMK_Example"></a> 전체 예제  
 다음 WPF(Windows Presentation Foundation) 프로젝트는 이 항목의 코드 예제를 포함합니다.  
  
 프로젝트를 실행하려면 다음 단계를 수행합니다.  
  
1. Visual Studio를 시작합니다.  
  
2. 메뉴 모음에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.  
  
     **새 프로젝트** 대화 상자가 열립니다.  
  
3. **설치 됨**의 **템플릿** 범주에서 **Visual Basic**를 선택 하 고 **Windows**를 선택 합니다. 프로젝트 형식 목록에서 **WPF 애플리케이션**을 선택합니다.  
  
4. 프로젝트의 이름으로 `AsyncReturnTypes`를 입력한 다음 **확인** 단추를 선택합니다.  
  
     **솔루션 탐색기**에 새 프로젝트가 표시됩니다.  
  
5. Visual Studio 코드 편집기에서 **MainWindow.xaml** 탭을 선택합니다.  
  
     탭이 표시되지 않는 경우 **솔루션 탐색기**에서 MainWindow.xaml의 바로 가기 메뉴를 열고 **열기**를 선택합니다.  
  
6. MainWindow.xaml의 **XAML** 창에서 코드를 다음 코드로 바꿉니다.  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="button1" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="button1_Click"/>  
            <TextBox x:Name="textBox1" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
  
        </Grid>  
    </Window>  
    ```  
  
     텍스트 상자와 단추가 포함된 간단한 창이 MainWindow.xaml의 **디자인** 창에 나타납니다.  
  
7. **솔루션 탐색기**에서 mainwindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택 합니다.  
  
8. MainWindow.xaml.vb의 코드를 다음 코드로 바꿉니다.  
  
    ```vb  
    Class MainWindow  
  
        ' SUB EXAMPLE  
        Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
  
            textBox1.Clear()  
  
            ' Start the process and await its completion. DriverAsync is a   
            ' Task-returning async method.  
            Await DriverAsync()  
  
            ' Say goodbye.  
            textBox1.Text &= vbCrLf & "All done, exiting button-click event handler."  
        End Sub  
  
        Async Function DriverAsync() As Task  
  
            ' Task(Of T)   
            ' Call and await the Task(Of T)-returning async method in the same statement.  
            Dim result1 As Integer = Await TaskOfT_MethodAsync()  
  
            ' Call and await in separate statements.  
            Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()  
  
            ' You can do other work that does not rely on resultTask before awaiting.  
            textBox1.Text &= String.Format("Application can continue working while the Task(Of T) runs. . . . " & vbCrLf)  
  
            Dim result2 As Integer = Await integerTask  
  
            ' Display the values of the result1 variable, the result2 variable, and  
            ' the resultTask.Result property.  
            textBox1.Text &= String.Format(vbCrLf & "Value of result1 variable:   {0}" & vbCrLf, result1)  
            textBox1.Text &= String.Format("Value of result2 variable:   {0}" & vbCrLf, result2)  
            textBox1.Text &= String.Format("Value of resultTask.Result:  {0}" & vbCrLf, integerTask.Result)  
  
            ' Task   
            ' Call and await the Task-returning async method in the same statement.  
            Await Task_MethodAsync()  
  
            ' Call and await in separate statements.  
            Dim simpleTask As Task = Task_MethodAsync()  
  
            ' You can do other work that does not rely on simpleTask before awaiting.  
            textBox1.Text &= String.Format(vbCrLf & "Application can continue working while the Task runs. . . ." & vbCrLf)  
  
            Await simpleTask  
        End Function  
  
        ' TASK(OF T) EXAMPLE  
        Async Function TaskOfT_MethodAsync() As Task(Of Integer)  
  
            ' The body of an async method is expected to contain an awaited   
            ' asynchronous call.  
            ' Task.FromResult is a placeholder for actual work that returns a string.  
            Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())  
  
            ' The method then can process the result in some way.  
            Dim leisureHours As Integer  
            If today.First() = "S" Then  
                leisureHours = 16  
            Else  
                leisureHours = 5  
            End If  
  
            ' Because the return statement specifies an operand of type Integer, the   
            ' method must have a return type of Task(Of Integer).   
            Return leisureHours  
        End Function  
  
        ' TASK EXAMPLE  
        Async Function Task_MethodAsync() As Task  
  
            ' The body of an async method is expected to contain an awaited   
            ' asynchronous call.  
            ' Task.Delay is a placeholder for actual work.  
            Await Task.Delay(2000)  
            textBox1.Text &= String.Format(vbCrLf & "Sorry for the delay. . . ." & vbCrLf)  
  
            ' This method has no return statement, so its return type is Task.   
        End Function  
  
    End Class  
    ```  
  
9. F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다.  
  
     다음과 같은 출력이 표시 됩니다.  
  
    ```console  
    Application can continue working while the Task<T> runs. . . .   
  
    Value of result1 variable:   5  
    Value of result2 variable:   5  
    Value of integerTask.Result: 5  
  
    Sorry for the delay. . . .  
  
    Application can continue working while the Task runs. . . .  
  
    Sorry for the delay. . . .  
  
    All done, exiting button-click event handler.  
    ```  
  
## <a name="see-also"></a>참조

- <xref:System.Threading.Tasks.Task.FromResult%2A>
- [연습: Async 및 Wait (Visual Basic)를 사용 하 여 웹에 액세스](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [비동기 프로그램의 제어 흐름(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)
- [비동기](../../../../visual-basic/language-reference/modifiers/async.md)
- [Await 연산자](../../../../visual-basic/language-reference/operators/await-operator.md)
