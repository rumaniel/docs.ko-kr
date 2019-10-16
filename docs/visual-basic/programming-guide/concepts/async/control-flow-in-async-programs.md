---
title: 비동기 프로그램의 제어 흐름 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: b0443af7-c586-4cb0-b476-742ae4098a96
ms.openlocfilehash: 74942ec3d293485ea6aae3940d1715af8de67c90
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71352121"
---
# <a name="control-flow-in-async-programs-visual-basic"></a>비동기 프로그램의 제어 흐름 (Visual Basic)

`Async` 및 `Await` 키워드를 사용하면 비동기 프로그램을 더 쉽게 쓰고 유지 관리할 수 있습니다. 그러나 프로그램 작동 방식을 이해하지 못한다면 결과에 놀랄 수 있습니다. 이 항목에서는 간단한 비동기 프로그램을 통해 제어 흐름을 추적하여 언제 메서드 간에 제어가 이동되고 매번 어떤 정보가 전달되는지 보여 줍니다.

> [!NOTE]
> `Async` 및 `Await` 키워드는 Visual Studio 2012에서 도입되었습니다.

일반적으로 [비동기 한정자를 사용 하 여 비동기](../../../../visual-basic/language-reference/modifiers/async.md) 코드를 포함 하는 메서드를 표시 합니다. Async 한정자로 표시 된 메서드에서 [wait (Visual Basic)](../../../../visual-basic/language-reference/operators/await-operator.md) 연산자를 사용 하 여 호출 된 비동기 프로세스가 완료 될 때까지 메서드가 일시 중지 될 때까지 대기 하는 위치를 지정할 수 있습니다. 자세한 내용은 [Async 및 wait를 사용한 비동기 프로그래밍 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)을 참조 하세요.

다음 예제에서는 비동기 메서드를 사용하여 지정된 웹 사이트의 콘텐츠를 문자열로 다운로드하고 문자열 길이를 표시합니다. 예제에는 다음 두 가지 메서드가 포함됩니다.

- `startButton_Click` - `AccessTheWebAsync`를 호출하고 결과를 표시합니다.

- `AccessTheWebAsync` - 웹 사이트의 콘텐츠를 문자열로 다운로드하고 문자열의 길이를 반환합니다. `AccessTheWebAsync`는 비동기 <xref:System.Net.Http.HttpClient> 메서드인 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>을 사용하여 콘텐츠를 다운로드합니다.

전체 프로그램에서 전략적 지점에 번호가 매겨진 표시 줄이 나타나 프로그램 실행 방식을 이해하도록 도와주고 표시된 각 지점에서 수행되는 작업을 설명합니다. 표시 줄에는 "ONE"~"SIX"의 레이블이 지정됩니다. 레이블은 프로그램이 이러한 코드 줄에 도달하는 순서를 나타냅니다.

다음 코드에서는 프로그램의 개요를 보여 줍니다.

```vb
Class MainWindow

    Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click

        ' ONE
        Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()

        ' FOUR
        Dim contentLength As Integer = Await getLengthTask

        ' SIX
        ResultsTextBox.Text &=
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)

    End Sub

    Async Function AccessTheWebAsync() As Task(Of Integer)

        ' TWO
        Dim client As HttpClient = New HttpClient()
        Dim getStringTask As Task(Of String) =
            client.GetStringAsync("https://msdn.microsoft.com")

        ' THREE
        Dim urlContents As String = Await getStringTask

        ' FIVE
        Return urlContents.Length
    End Function

End Class
```

"ONE"~"SIX"의 레이블이 지정된 각 위치에는 프로그램의 현재 상태에 대한 정보가 표시됩니다. 다음 출력이 생성됩니다.

```console
ONE:   Entering startButton_Click.
           Calling AccessTheWebAsync.

TWO:   Entering AccessTheWebAsync.
           Calling HttpClient.GetStringAsync.

THREE: Back in AccessTheWebAsync.
           Task getStringTask is started.
           About to await getStringTask & return a Task<int> to startButton_Click.

FOUR:  Back in startButton_Click.
           Task getLengthTask is started.
           About to await getLengthTask -- no caller to return to.

FIVE:  Back in AccessTheWebAsync.
           Task getStringTask is complete.
           Processing the return statement.
           Exiting from AccessTheWebAsync.

SIX:   Back in startButton_Click.
           Task getLengthTask is finished.
           Result from AccessTheWebAsync is stored in contentLength.
           About to display contentLength and exit.

Length of the downloaded string: 33946.
```

## <a name="set-up-the-program"></a>프로그램 설정

이 항목에서 사용하는 코드를 MSDN에서 다운로드하거나 직접 코드를 빌드할 수 있습니다.

> [!NOTE]
> 예제를 실행 하려면 Visual Studio 2012 이상 및 .NET Framework 4.5 이상이 컴퓨터에 설치 되어 있어야 합니다.

### <a name="download-the-program"></a>프로그램 다운로드

[비동기 샘플: 비동기 프로그램의 제어 흐름](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0)에서 이 항목의 애플리케이션을 다운로드할 수 있습니다. 다음 단계에서 프로그램을 열고 실행합니다.

1. 다운로드한 파일의 압축을 풀고 Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **열기**, **프로젝트/솔루션**을 선택합니다.

3. 압축을 푼 샘플 코드가 포함된 폴더로 이동하고, 솔루션(.sln) 파일을 열고, F5 키를 선택하여 프로젝트를 빌드하고 실행합니다.

### <a name="build-the-program-yourself"></a>프로그램 직접 빌드

다음 WPF(Windows Presentation Foundation) 프로젝트는 이 항목의 코드 예제를 포함합니다.

프로젝트를 실행하려면 다음 단계를 수행합니다.

1. Visual Studio를 시작합니다.

2. 메뉴 모음에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.

    **새 프로젝트** 대화 상자가 열립니다.

3. **설치 된 템플릿** 창에서 **Visual Basic**을 선택한 다음 프로젝트 형식 목록에서 **WPF 응용 프로그램** 을 선택 합니다.

4. 프로젝트의 이름으로 `AsyncTracer`를 입력한 다음 **확인** 단추를 선택합니다.

    **솔루션 탐색기**에 새 프로젝트가 표시됩니다.

5. Visual Studio 코드 편집기에서 **MainWindow.xaml** 탭을 선택합니다.

    탭이 표시되지 않는 경우 **솔루션 탐색기**에서 MainWindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택합니다.

6. MainWindow.xaml의 **XAML** 보기에서 코드를 다음 코드로 바꿉니다.

    ```vb
    <Window
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="MainWindow"
        Title="Control Flow Trace" Height="350" Width="525">
        <Grid>
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="221,10,0,0" VerticalAlignment="Top" Width="75"/>
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="510" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" d:LayoutOverrides="HorizontalMargin"/>

        </Grid>
    </Window>
    ```

    텍스트 상자와 버튼이 포함된 간단한 창이 MainWindow.xaml의 **디자인** 보기에 나타납니다.

7. <xref:System.Net.Http>에 대한 참조를 추가합니다.

8. **솔루션 탐색기**에서 mainwindow.xaml의 바로 가기 메뉴를 열고 **코드 보기**를 선택 합니다.

9. Mainwindow.xaml에서 코드를 다음 코드로 바꿉니다.

    ```vb
    ' Add an Imports statement and a reference for System.Net.Http.
    Imports System.Net.Http

    Class MainWindow

        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click

            ' The display lines in the example lead you through the control shifts.
            ResultsTextBox.Text &= "ONE:   Entering StartButton_Click." & vbCrLf &
                "           Calling AccessTheWebAsync." & vbCrLf

            Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()

            ResultsTextBox.Text &= vbCrLf & "FOUR:  Back in StartButton_Click." & vbCrLf &
                "           Task getLengthTask is started." & vbCrLf &
                "           About to await getLengthTask -- no caller to return to." & vbCrLf

            Dim contentLength As Integer = Await getLengthTask

            ResultsTextBox.Text &= vbCrLf & "SIX:   Back in StartButton_Click." & vbCrLf &
                "           Task getLengthTask is finished." & vbCrLf &
                "           Result from AccessTheWebAsync is stored in contentLength." & vbCrLf &
                "           About to display contentLength and exit." & vbCrLf

            ResultsTextBox.Text &=
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)
        End Sub

        Async Function AccessTheWebAsync() As Task(Of Integer)

            ResultsTextBox.Text &= vbCrLf & "TWO:   Entering AccessTheWebAsync."

            ' Declare an HttpClient object.
            Dim client As HttpClient = New HttpClient()

            ResultsTextBox.Text &= vbCrLf & "           Calling HttpClient.GetStringAsync." & vbCrLf

            ' GetStringAsync returns a Task(Of String).
            Dim getStringTask As Task(Of String) = client.GetStringAsync("https://msdn.microsoft.com")

            ResultsTextBox.Text &= vbCrLf & "THREE: Back in AccessTheWebAsync." & vbCrLf &
                "           Task getStringTask is started."

            ' AccessTheWebAsync can continue to work until getStringTask is awaited.

            ResultsTextBox.Text &=
                vbCrLf & "           About to await getStringTask & return a Task(Of Integer) to StartButton_Click." & vbCrLf

            ' Retrieve the website contents when task is complete.
            Dim urlContents As String = Await getStringTask

            ResultsTextBox.Text &= vbCrLf & "FIVE:  Back in AccessTheWebAsync." &
                vbCrLf & "           Task getStringTask is complete." &
                vbCrLf & "           Processing the return statement." &
                vbCrLf & "           Exiting from AccessTheWebAsync." & vbCrLf

            Return urlContents.Length
        End Function

    End Class
    ```

10. F5 키를 선택하여 프로그램을 실행한 다음 **시작** 단추를 선택합니다.

    다음과 같은 출력이 표시 됩니다.

    ```console
    ONE:   Entering startButton_Click.
               Calling AccessTheWebAsync.

    TWO:   Entering AccessTheWebAsync.
               Calling HttpClient.GetStringAsync.

    THREE: Back in AccessTheWebAsync.
               Task getStringTask is started.
               About to await getStringTask & return a Task<int> to startButton_Click.

    FOUR:  Back in startButton_Click.
               Task getLengthTask is started.
               About to await getLengthTask -- no caller to return to.

    FIVE:  Back in AccessTheWebAsync.
               Task getStringTask is complete.
               Processing the return statement.
               Exiting from AccessTheWebAsync.

    SIX:   Back in startButton_Click.
               Task getLengthTask is finished.
               Result from AccessTheWebAsync is stored in contentLength.
               About to display contentLength and exit.

    Length of the downloaded string: 33946.
    ```

## <a name="trace-the-program"></a>프로그램 추적

### <a name="steps-one-and-two"></a>1, 2단계

처음 두 표시 줄은 `startButton_Click`이 `AccessTheWebAsync`를 호출하고, `AccessTheWebAsync`가 비동기 <xref:System.Net.Http.HttpClient> 메서드 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>을 호출할 때 경로를 추적합니다. 다음 그림은 메서드 간의 호출을 간단히 보여 줍니다.

![1단계 및 2단계](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace-ONETWO")

`AccessTheWebAsync` 및 `client.GetStringAsync`의 반환 형식은 둘 다 <xref:System.Threading.Tasks.Task%601>입니다. `AccessTheWebAsync`의 경우 TResult는 정수입니다. `GetStringAsync`의 경우 TResult는 문자열입니다. 비동기 메서드 반환 형식에 대 한 자세한 내용은 [비동기 반환 형식 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)을 참조 하세요.

제어가 다시 호출자로 이동할 때 작업 반환 비동기 메서드는 작업 인스턴스를 반환합니다. 호출된 메서드에서 `Await` 연산자가 발견되거나 호출된 메서드가 종료될 때 제어는 비동기 메서드에서 호출자로 반환됩니다. "THREE"~"SIX"의 레이블이 지정된 표시 줄은 이 프로세스 부분을 추적합니다.

### <a name="step-three"></a>3단계

`AccessTheWebAsync`에서 비동기 메서드 <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>을 호출하여 대상 웹 페이지의 콘텐츠를 다운로드합니다. `client.GetStringAsync`가 반환되면 제어가 `client.GetStringAsync`에서 `AccessTheWebAsync`로 반환됩니다.

`client.GetStringAsync` 메서드는 `AccessTheWebAsync`의 `getStringTask` 변수에 할당된 문자열의 작업을 반환합니다. 예제 프로그램의 다음 줄은 `client.GetStringAsync` 호출 및 할당을 보여 줍니다.

```vb
Dim getStringTask As Task(Of String) = client.GetStringAsync("https://msdn.microsoft.com")
```

작업은 결국 실제 문자열을 생성하기 위한 `client.GetStringAsync`의 약속으로 간주할 수 있습니다. 그리고 `client.GetStringAsync`의 약속된 문자열을 사용하지 않는 작업이 `AccessTheWebAsync`에 있는 경우 `client.GetStringAsync`가 대기하는 동안 해당 작업이 계속될 수 있습니다. 예제에서 "THREE" 레이블이 지정된 다음 출력 줄은 독립 작업을 수행할 기회를 나타냅니다.

```console
THREE: Back in AccessTheWebAsync.
           Task getStringTask is started.
           About to await getStringTask & return a Task<int> to startButton_Click.
```

 다음 문은 `getStringTask`가 대기 상태일 때 `AccessTheWebAsync`의 진행을 일시 중단합니다.

```vb
Dim urlContents As String = Await getStringTask
```

다음 이미지는 `client.GetStringAsync`에서 @no__t에 대 한 할당에 대 한 제어 흐름을 보여 주고, `getStringTask`를 생성 하 여 Wait 연산자를 적용 합니다.

![3단계](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace-Three")

await 식은 `client.GetStringAsync`가 반환될 때까지 `AccessTheWebAsync`를 일시 중단합니다. 그리고 제어는 `AccessTheWebAsync`의 호출자, `startButton_Click`으로 반환됩니다.

> [!NOTE]
> 일반적으로 즉시 비동기 메서드에 대한 호출을 기다립니다. 예를 들어 다음 할당은 `getStringTask`를 만들고 기다리는 이전 코드를 대체할 수 있습니다. `Dim urlContents As String = Await client.GetStringAsync("https://msdn.microsoft.com")`.
>
> 이 항목에서 await 연산자는 나중에 프로그램을 통해 제어 흐름을 표시하는 출력 줄을 수용하기 위해 적용됩니다.

### <a name="step-four"></a>4단계

`AccessTheWebAsync`의 선언된 반환 형식은 `Task(Of Integer)`입니다. 따라서 `AccessTheWebAsync`가 일시 중단될 경우 정수 작업을 `startButton_Click`으로 반환합니다. 반환된 작업이 `getStringTask`가 아니라는 것을 이해해야 합니다. 반환된 작업은 일시 중단된 메서드 `AccessTheWebAsync`에서 수행하도록 남아 있는 작업을 나타내는 새로운 정수 작업입니다. 작업은 작업이 완료될 때 정수를 생성하기 위한 `AccessTheWebAsync`의 약속입니다.

다음 문은 이 작업을 `getLengthTask` 변수에 할당합니다.

```vb
Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()
```

`AccessTheWebAsync`에서처럼 `startButton_Click`은 작업이 대기 상태가 될 때까지 비동기 작업(`getLengthTask`)의 결과를 사용하지 않는 작업을 계속할 수 있습니다. 다음 출력 줄은 해당 작업을 나타냅니다.

```console
FOUR:  Back in startButton_Click.
           Task getLengthTask is started.
           About to await getLengthTask -- no caller to return to.
```

`startButton_Click`의 진행은 `getLengthTask`가 대기 상태일 때 일시 중단됩니다. 다음 대입문은 `AccessTheWebAsync`가 완료될 때까지 `startButton_Click`을 일시 중단합니다.

```vb
Dim contentLength As Integer = Await getLengthTask
```

다음 그림에서 화살표는 `AccessTheWebAsync`의 await 식에서 `getLengthTask`에 대한 값 할당으로의 제어 흐름에 이어 `getLengthTask`가 대기 상태가 될 때까지 `startButton_Click`의 일반적인 처리를 보여 줍니다.

![4단계](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace-FOUR")

### <a name="step-five"></a>5단계

`client.GetStringAsync`가 완료되었음을 알리면 `AccessTheWebAsync` 처리는 일시 중단이 해제되고 await 문을 무시하고 계속 진행될 수 있습니다. 다음 출력 줄은 처리를 다시 시작 하는 것을 나타냅니다.

```console
FIVE:  Back in AccessTheWebAsync.
           Task getStringTask is complete.
           Processing the return statement.
           Exiting from AccessTheWebAsync.
```

return 문의 피연산자, `urlContents.Length`는 `AccessTheWebAsync`가 반환하는 작업에 저장됩니다. await 식은 `startButton_Click`의 `getLengthTask`에서 해당 값을 검색합니다.

다음 그림은 `client.GetStringAsync`(및 `getStringTask`)가 완료된 후 제어의 전송을 보여 줍니다.

![5단계](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "AsyncTrace-FIVE")

`AccessTheWebAsync`는 완료될 때까지 실행되고 제어는 완료를 기다리고 있는 `startButton_Click`으로 반환됩니다.

### <a name="step-six"></a>6단계

`AccessTheWebAsync`가 완료되었음을 알리면 처리는 `startButton_Async`의 await 문을 무시하고 계속 진행될 수 있습니다. 실제로 프로그램에는 추가로 수행할 작업이 없습니다.

다음 출력 줄은 `startButton_Async`의 처리 다시 시작을 나타냅니다.

```console
SIX:   Back in startButton_Click.
           Task getLengthTask is finished.
           Result from AccessTheWebAsync is stored in contentLength.
           About to display contentLength and exit.
```

await 식은 `getLengthTask`에서 `AccessTheWebAsync`에 있는 return 문의 피연산자인 정수 값을 검색합니다. 다음 문은 이 해당 값을 `contentLength` 변수에 할당합니다.

```vb
Dim contentLength As Integer = Await getLengthTask
```

다음 그림은 `AccessTheWebAsync`에서 `startButton_Click`로의 제어 반환을 보여 줍니다.

![6단계](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace-SIX")

## <a name="see-also"></a>참조

- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
- [비동기 반환 형식(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)
- [연습: Async 및 Wait (Visual Basic)를 사용 하 여 웹에 액세스](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [비동기 샘플: 비동기 프로그램의 제어 흐름(C# 및 Visual Basic)](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0)
