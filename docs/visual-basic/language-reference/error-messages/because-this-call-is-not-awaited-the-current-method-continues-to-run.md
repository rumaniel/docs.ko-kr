---
title: 이 호출이 대기되지 않으므로 호출이 완료되기 전에 현재 메서드가 계속 실행됩니다.
ms.date: 07/20/2015
f1_keywords:
- bc42358
- vbc42358
helpviewer_keywords:
- BC42358
ms.assetid: 43342515-c3c8-4155-9263-c302afabcbc2
ms.openlocfilehash: 6ceebc3af01c13474affa6e728c49d6d246eb331
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701193"
---
# <a name="because-this-call-is-not-awaited-the-current-method-continues-to-run-before-the-call-is-completed"></a>이 호출이 대기되지 않으므로 호출이 완료되기 전에 현재 메서드가 계속 실행됩니다.
이 호출이 대기되지 않으므로 호출이 완료되기 전에 현재 메서드가 계속 실행됩니다. 'Await' 연산자는 호출 결과에 적용하는 것이 좋습니다.  
  
 현재 메서드는 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 을 반환하는 비동기 메서드를 호출하고 결과에 [Await](../../../visual-basic/language-reference/operators/await-operator.md) 연산자를 적용하지 않습니다. 비동기 메서드 호출이 비동기 작업을 시작합니다. 그러나 `Await` 연산자가 적용되지 않기 때문에 프로그램이 작업이 완료될 때까지 기다리지 않고 계속됩니다. 대부분의 경우 예상대로 동작하지 않습니다. 대개 호출 메서드의 다른 부분은 호출의 결과에 따라 다르거나, 최소한 호출을 포함하는 메서드에서 돌아오기 전에 호출된 메서드가 완료되어야 합니다.  
  
 호출된 비동기 메서드에서 발생하는 예외로 인해 어떤 상황이 발생하는지도 중요한 문제입니다. <xref:System.Threading.Tasks.Task> 또는  <xref:System.Threading.Tasks.Task%601> 를 반환하는 메서드에서 발생하는 예외는 반환된 작업에 저장됩니다. 작업을 기다리지 않거나 예외를 명시적으로 확인하지 않는 경우 예외가 손실됩니다. 작업을 기다리는 경우 예외가 다시 throw됩니다.  
  
 가장 좋은 방법은 항상 호출을 기다리는 것입니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42358  
  
### <a name="to-address-this-warning"></a>이 경고를 해결하려면  
  
- 비동기 호출이 완료될 때까지 기다리지 않으려고 하거나 호출된 메서드가 예외를 발생시키지 않는 경우에만 경고가 표시되지 않게 해야 합니다. 이 경우 변수에 호출의 작업 결과를 할당하여 경고가 표시되지 않게 할 수 있습니다.  
  
     다음 예제는 경고를 발생시키는 방법, 경고가 표시되지 않게 하는 방법 및 호출을 대기하는 방법을 보여줍니다.  
  
    ```vb  
    Async Function CallingMethodAsync() As Task  
  
        ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
        ' Variable delay is used to slow down the called method so that you  
        ' can distinguish between awaiting and not awaiting in the program's output.   
        ' You can adjust the value to produce the output that this topic shows   
        ' after the code.  
        Dim delay = 5000  
  
        ' Call #1.  
        ' Call an async method. Because you don't await it, its completion isn't   
        ' coordinated with the current method, CallingMethodAsync.  
        ' The following line causes the warning.  
        CalledMethodAsync(delay)  
  
        ' Call #2.  
        ' To suppress the warning without awaiting, you can assign the   
        ' returned task to a variable. The assignment doesn't change how  
        ' the program runs. However, the recommended practice is always to  
        ' await a call to an async method.  
        ' Replace Call #1 with the following line.  
        'Task delayTask = CalledMethodAsync(delay)  
  
        ' Call #3  
        ' To contrast with an awaited call, replace the unawaited call   
        ' (Call #1 or Call #2) with the following awaited call. The best   
        ' practice is to await the call.  
  
        'Await CalledMethodAsync(delay)  
  
        ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
        ' continues to run and, in this example, finishes its work and returns  
        ' to its caller.  
        ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
    End Function  
  
    Async Function CalledMethodAsync(howLong As Integer) As Task  
  
        ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
        ' Slow the process down a little so you can distinguish between awaiting  
        ' and not awaiting. Adjust the value for howLong if necessary.  
        Await Task.Delay(howLong)  
        ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
    End Function  
    ```  
  
     이 예제에서는 Call #1 또는 Call #2를 선택할 경우 해당 호출자(`CalledMethodAsync`)와 호출자의 호출자(`CallingMethodAsync`)가 모두 완료된 후 기다리지 않는 비동기 메서드(`StartButton_Click`)가 끝납니다. 다음 출력의 마지막 줄은 호출된 메서드가 끝나는 시기를 보여줍니다. 전체 예제에서 `CallingMethodAsync` 를 호출하는 이벤트 처리기의 시작과 종료가 출력에 표시되어 있습니다.  
  
    ```console  
    Entering the Click event handler.  
      Entering calling method.  
        Entering called method, starting and awaiting Task.Delay.  
      Returning from calling method.  
    Exiting the Click event handler.  
        Task.Delay is finished--returning from called method.  
    ```  
  
## <a name="example"></a>예제  
 다음 Windows Presentation Foundation(WPF) 애플리케이션은 이전 예제의 메서드를 포함합니다. 다음 단계는 애플리케이션을 설정합니다.  
  
1. WPF 애플리케이션을 만들고 이름을 `AsyncWarning`으로 지정합니다.  
  
2. Visual Studio 코드 편집기에서 **MainWindow.xaml** 탭을 선택합니다.  
  
     탭이 표시되지 않는 경우 **솔루션 탐색기**에서 MainWindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택합니다.  
  
3. MainWindow.xaml의 **XAML** 보기에서 코드를 다음 코드로 바꿉니다.  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="StartButton_Click" />  
            <TextBox x:Name="ResultsTextBox" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
        </Grid>  
    </Window>  
    ```  
  
     단추와 텍스트 상자가 포함된 간단한 창이 MainWindow.xaml의 **디자인** 뷰에 나타납니다.  
  
     XAML 디자이너에 대한 자세한 내용은 [Visual Studio에서 XAML 디자이너를 사용하여 UI 만들기](/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio)를 참조하세요. 간단한 UI를 직접 빌드하는 방법에 대한 자세한 내용은 "WPF 애플리케이션을 만들려면" 섹션과 "간단한 WPF MainWindow를 디자인하려면" 섹션인 [연습: Async 및 Await를 사용하여 웹에 액세스](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)를 참조하세요.  
  
4. MainWindow.xaml.vb의 코드를 다음 코드로 바꿉니다.  
  
    ```vb  
    Class MainWindow   
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
            ResultsTextBox.Text &= vbCrLf & "Entering the Click event handler."  
            Await CallingMethodAsync()  
            ResultsTextBox.Text &= vbCrLf & "Exiting the Click event handler."  
        End Sub  
  
        Async Function CallingMethodAsync() As Task  
  
            ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
            ' Variable delay is used to slow down the called method so that you  
            ' can distinguish between awaiting and not awaiting in the program's output.   
            ' You can adjust the value to produce the output that this topic shows   
            ' after the code.  
            Dim delay = 5000  
  
            ' Call #1.  
            ' Call an async method. Because you don't await it, its completion isn't   
            ' coordinated with the current method, CallingMethodAsync.  
            ' The following line causes the warning.  
            CalledMethodAsync(delay)  
  
            ' Call #2.  
            ' To suppress the warning without awaiting, you can assign the   
            ' returned task to a variable. The assignment doesn't change how  
            ' the program runs. However, the recommended practice is always to  
            ' await a call to an async method.  
  
            ' Replace Call #1 with the following line.  
            'Task delayTask = CalledMethodAsync(delay)  
  
            ' Call #3  
            ' To contrast with an awaited call, replace the unawaited call   
            ' (Call #1 or Call #2) with the following awaited call. The best   
            ' practice is to await the call.  
  
            'Await CalledMethodAsync(delay)  
  
            ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
            ' continues to run and, in this example, finishes its work and returns  
            ' to its caller.  
            ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
        End Function  
  
        Async Function CalledMethodAsync(howLong As Integer) As Task  
  
            ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
            ' Slow the process down a little so you can distinguish between awaiting  
            ' and not awaiting. Adjust the value for howLong if necessary.  
            Await Task.Delay(howLong)  
            ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
        End Function  
  
    End Class  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    '     Task.Delay is finished--returning from called method.  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '     Task.Delay is finished--returning from called method.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    ```  
  
5. F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다.  
  
     예상 출력이 코드의 끝에 나타납니다.  
  
## <a name="see-also"></a>참조

- [Await 연산자](../../../visual-basic/language-reference/operators/await-operator.md)
- [Async 및 Await를 사용한 비동기 프로그래밍](../../../visual-basic/programming-guide/concepts/async/index.md)
