---
title: Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)
ms.date: 07/20/2015
ms.assetid: bd7e462b-583b-4395-9c36-45aa9e61072c
ms.openlocfilehash: 9632ee7d275e6641bcd334aa12cded44920d2fda
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291661"
---
# <a name="asynchronous-programming-with-async-and-await-visual-basic"></a>Async 및 Wait를 사용한 비동기 프로그래밍 (Visual Basic)

비동기 프로그래밍을 사용하여 성능 병목 현상을 방지하고 애플리케이션의 전체적인 응답성을 향상할 수 있습니다. 그러나 비동기 애플리케이션을 쓰는 일반적인 기술이 복잡하여 해당 애플리케이션을 쓰고, 디버깅하고, 유지 관리하기 어려울 수 있습니다.

Visual Studio 2012에는 Windows 런타임 뿐 아니라 .NET Framework 4.5 이상의 비동기 지원을 활용하는 간단한 비동기 프로그래밍 접근 방법이 도입되었습니다. 컴파일러는 개발자가 하던 어려운 작업을 수행하고, 애플리케이션은 동기 코드와 비슷한 논리 구조를 유지합니다. 따라서 약간의 노력만으로도 비동기 프로그래밍의 모든 장점을 누릴 수 있습니다.

이 항목에서는 비동기 프로그래밍을 사용하는 시기 및 방법에 대한 개요를 제공하고 특정 세부 정보 및 예제가 포함된 지원 항목에 대한 링크가 포함되어 있습니다.

## <a name="BKMK_WhentoUseAsynchrony"></a> 반응성을 향상시키는 비동기

비동기는 애플리케이션이 웹에 액세스하는 경우와 같이 차단 가능성이 있는 작업에 반드시 필요합니다. 웹 리소스에 대한 액세스 속도가 느리거나 지연됩니다. 동기 프로세스 안에서 이러한 활동이 차단되면 전체 애플리케이션이 기다려야 합니다. 비동기 프로세스에서 애플리케이션은 잠재적인 차단 작업이 완료될 때까지 웹 리소스에 의존하지 않는 다른 작업을 계속 수행할 수 있습니다.

다음 표에는 비동기 프로그래밍으로 응답성이 향상되는 일반적인 영역이 나와 있습니다. .NET Framework 4.5 및 Windows 런타임에서 나열된 API에는 비동기 프로그래밍을 지원하는 메서드가 포함되어 있습니다.

|애플리케이션 영역|비동기 메서드를 포함하는 API 지원|
|----------------------|------------------------------------------------|
|웹 액세스|<xref:System.Net.Http.HttpClient>, <xref:Windows.Web.Syndication.SyndicationClient>|
|파일 작업|<xref:Windows.Storage.StorageFile>, <xref:System.IO.StreamWriter>, <xref:System.IO.StreamReader>, <xref:System.Xml.XmlReader>|
|이미지 작업|<xref:Windows.Media.Capture.MediaCapture>, <xref:Windows.Graphics.Imaging.BitmapEncoder>, <xref:Windows.Graphics.Imaging.BitmapDecoder>|
|WCF 프로그래밍|[동기 및 비동기 작업](../../../../framework/wcf/synchronous-and-asynchronous-operations.md)|
|||

모든 UI 관련 작업이 대체로 스레드 한 개를 공유하므로 비동기는 특히 UI 스레드에 액세스하는 애플리케이션의 변수를 증명합니다. 동기 애플리케이션에서 임의의 프로세스가 차단되면 모든 프로세스가 차단됩니다. 애플리케이션이 응답을 중지하면 기다리지 않고 애플리케이션이 실패한 것으로 결론을 내릴 것입니다.

비동기 메서드를 사용하면 애플리케이션이 UI에 계속 응답합니다. 예를 들어 창의 크기를 조정하거나 최소화할 수 있습니다. 또는 애플리케이션이 완료될 때까지 기다리고 싶지 않다면 애플리케이션을 종료할 수 있습니다.

비동기 기반 접근 방식을 사용하면 비동기 작업을 디자인할 때 선택할 수 있는 옵션 목록에 자동 전송과 동일한 기능을 추가할 수 있습니다. 즉, 더 적은 개발자의 노력으로 기존 비동기 프로그래밍의 이점을 모두 활용할 수 있습니다.

## <a name="BKMK_HowtoWriteanAsyncMethod"></a> 작성이 간편한 비동기 메서드

Visual Basic의 [Async](../../../../visual-basic/language-reference/modifiers/async.md) 및 [Await](../../../../visual-basic/language-reference/operators/await-operator.md) 키워드는 비동기 프로그래밍의 핵심입니다. 이 키워드 두 개를 사용하면 .NET Framework 또는 Windows 런타임의 리소스를 사용하여 동기 메서드를 만드는 것만큼 쉽게 비동기 메서드를 만들 수 있습니다. `Async` 및 `Await`를 사용하여 정의하는 비동기 메서드를 비동기 메서드라고 합니다.

다음 예제에서는 비동기 메서드를 보여줍니다. 코드의 거의 모든 내용이 익숙할 것입니다. 주석은 비동기를 만들 때 추가하는 기능을 호출합니다.

이 항목의 마지막에 완전한 WPF(Windows Presentation Foundation) 예제 파일이 있으며, [비동기 샘플: "Async 및 Await를 사용하는 비동기 프로그래밍"의 예제](https://docs.microsoft.com/samples/dotnet/samples/async-and-await-vb/)에서 샘플을 다운로드할 수 있습니다.

```vb
' Three things to note about writing an Async Function:
'  - The function has an Async modifier. 
'  - Its return type is Task or Task(Of T). (See "Return Types" section.)
'  - As a matter of convention, its name ends in "Async".
Async Function AccessTheWebAsync() As Task(Of Integer)
    Using client As New HttpClient()
        ' Call and await separately. 
        '  - AccessTheWebAsync can do other things while GetStringAsync is also running.
        '  - getStringTask stores the task we get from the call to GetStringAsync. 
        '  - Task(Of String) means it is a task which returns a String when it is done.
        Dim getStringTask As Task(Of String) =
            client.GetStringAsync("https://docs.microsoft.com/dotnet")
        ' You can do other work here that doesn't rely on the string from GetStringAsync.
        DoIndependentWork()
        ' The Await operator suspends AccessTheWebAsync.
        '  - AccessTheWebAsync does not continue until getStringTask is complete.
        '  - Meanwhile, control returns to the caller of AccessTheWebAsync.
        '  - Control resumes here when getStringTask is complete.
        '  - The Await operator then retrieves the String result from getStringTask.
        Dim urlContents As String = Await getStringTask
        ' The Return statement specifies an Integer result.
        ' A method which awaits AccessTheWebAsync receives the Length value.
        Return urlContents.Length
        
    End Using
    
End Function
```

`AccessTheWebAsync`에 `GetStringAsync` 호출과 해당 완료 대기 사이에 수행할 수 있는 작업이 없는 경우 다음 단일 문을 호출하고 대기하여 코드를 단순화할 수 있습니다.

```vb
Dim urlContents As String = Await client.GetStringAsync()
```

 다음 특징은 이전 예제에서 비동기 메서드를 만드는 것을 요약 한 것입니다.

- 메서드 시그니처에 `Async` 한정자가 포함됩니다.
- 비동기 메서드의 이름은 규칙에 따라 "Async" 접미사로 끝납니다.
- 반환 형식은 다음 형식 중 하나입니다.

  - 메서드에 연산자 형식이 TResult인 Return 문이 있는 경우 <xref:System.Threading.Tasks.Task%601>입니다.
  - 메서드에 반환 문이 포함되지 않았거나 피연산자가 없는 반환 문이 포함된 경우 <xref:System.Threading.Tasks.Task>입니다.
  - 비동기 이벤트 처리기를 작성하는 경우 [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)입니다.

  자세한 내용은 이 항목 뒷부분의 "반환 형식 및 매개 변수"를 참조하세요.

- 메서드는 일반적으로 비동기 작업이 완료될 때까지 메서드가 계속될 수 없는 지점을 표시하는 하나 이상의 대기 표현을 포함하고 있습니다. 한편, 메서드가 일시 중단되고 컨트롤이 메서드의 호출자로 반환됩니다. 이 항목의 다음 단원은 일시 중단 지점에서 발생하는 상황을 보여줍니다.

비동기 메서드에서는 제공된 키워드 및 형식을 사용해서 수행하려는 작업을 나타내고, 컴파일러는 일시 중단된 메서드에서 컨트롤이 대기 지점으로 반환될 때 수행되어야 하는 항목을 추적하는 등의 나머지 작업을 수행합니다. 루프 및 예외 처리와 같은 일부 루틴 프로세스는 기존의 비동기 코드에서 처리하기 어려울 수 있습니다. 비동기 메서드에서는 동기 솔루션에서와 같이 필요한 만큼 이러한 요소를 작성하여 문제를 해결합니다.

이전 버전의 .NET Framework의 비동기에 대한 자세한 내용은 [TPL 및 일반적인 .NET Framework 비동기 프로그래밍](../../../../standard/parallel-programming/tpl-and-traditional-async-programming.md)을 참조하세요.

## <a name="BKMK_WhatHappensUnderstandinganAsyncMethod"></a>비동기 메서드에서 수행 되는 작업

비동기 프로그래밍을 이해하는 데 있어 가장 중요한 점은 메서드에서 메서드로 제어 흐름을 이동하는 방법입니다. 다음 다이어그램에서 과정을 안내합니다.

![비동기 프로그램 추적을 보여 주는 다이어그램입니다.](./media/index/navigation-trace-async-program.png)

다이어그램의 숫자는 다음 단계에 해당 합니다.

1. 이벤트 처리기는 `AccessTheWebAsync` 비동기 메서드를 호출 하 고 기다립니다 합니다.

2. `AccessTheWebAsync`는 <xref:System.Net.Http.HttpClient> 인스턴스를 만들고 <xref:System.Net.Http.HttpClient.GetStringAsync%2A> 비동기 메서드를 호출하여 웹 사이트의 내용을 문자열로 다운로드합니다.

3. `GetStringAsync`에서 특정 작업이 발생하여 진행이 일시 중단됩니다. 웹 사이트에서 다운로드 또는 다른 차단 작업을 수행할 때까지 기다려야 할 수 있습니다. 리소스를 차단하지 않기 위해 `GetStringAsync`는 해당 호출자인 `AccessTheWebAsync`에 제어 권한을 양도합니다.

     `GetStringAsync`는 TResult가 문자열인 <xref:System.Threading.Tasks.Task%601>를 반환하고 `AccessTheWebAsync`는 `getStringTask` 변수에 작업을 할당합니다. 이 작업은 작업이 완료될 때 실제 문자열 값을 생성하기 위한 코드와 함께 `GetStringAsync`를 호출하는 지속적인 프로세스를 나타냅니다.

4. `getStringTask`가 아직 대기되지 않았으므로 `AccessTheWebAsync`가 `GetStringAsync`의 최종 결과에 무관한 다른 작업을 계속할 수 있습니다. 이 작업은 동기 메서드 `DoIndependentWork`를 호출하여 나타냅니다.

5. `DoIndependentWork`는 작업을 수행하고 호출자에게 반환하는 동기 메서드입니다.

6. `AccessTheWebAsync`에 `getStringTask` 결과 없이 수행할 수 있는 작업이 없습니다. 다음으로 `AccessTheWebAsync`는 다운로드한 문자열의 길이를 계산하여 반환하려 하지만, 메서드가 문자열을 확인할 때까지 해당 값을 계산할 수 없습니다.

     따라서 `AccessTheWebAsync`는 await 연산자를 사용해서 해당 프로세스를 일시 중단하고 `AccessTheWebAsync`를 호출한 메서드에 제어 권한을 양도합니다. `AccessTheWebAsync`는 호출자에게 `Task<int>`(Visual Basic의 `Task(Of Integer)`)를 반환합니다. 작업은 다운로드한 문자열의 길이인 정수 결과를 만든다는 약속을 나타냅니다.

    > [!NOTE]
    > `GetStringAsync`가 대기하기 전에 `getStringTask`(및 `AccessTheWebAsync`)가 완료되면 `AccessTheWebAsync`에 컨트롤이 유지됩니다. 일시 중단 및 `AccessTheWebAsync`의 반환 비용은 호출된 비동기 프로세스(`getStringTask`)가 이미 완료되었고 AccessTheWebSync가 최종 결과를 기다릴 필요가 없다면 낭비됩니다.

     호출자(이 예제의 이벤트 처리기) 내에서 처리 패턴이 계속됩니다. 호출자가 해당 결과를 기다리거나 즉시 기다리기 전에 `AccessTheWebAsync`에서 결과에 의존하지 않는 다른 작업을 수행할 수 있습니다.   `AccessTheWebAsync`에 대한 이벤트가 대기 중이며 `AccessTheWebAsync`가 `GetStringAsync`를 대기 중입니다.

7. `GetStringAsync`가 완료되고 문자열 결과를 생성합니다. `GetStringAsync`를 호출할 경우 문자열 결과가 예상대로 반환되지 않습니다. (메서드가 이미 3단계에서 작업을 반환했습니다.) 대신 문자열 결과가 메서드 `getStringTask`의 완료를 나타내는 작업에 저장됩니다. await 연산자가 `getStringTask`에서 결과를 검색합니다. 할당 문은 검색된 결과를 `urlContents`에 할당합니다.

8. `AccessTheWebAsync`에 문자열 결과가 있는 경우 메서드가 문자열 길이를 계산할 수 있습니다. 그런 다음 `AccessTheWebAsync` 작업도 완료되고 대기 이벤트 처리기를 다시 시작할 수 있습니다. 이 항목 뒷부분의 전체 예에서는 이벤트 처리기가 길이 결과 값을 검색하고 출력하는지 확인할 수 있습니다.

비동기 프로그래밍을 처음 접하는 사용자인 경우 동기 동작과 비동기 동작의 차이점을 살펴보세요. 비동기 메서드는 작업이 완료될 때 반환되지만(5단계) 비동기 메서드는 작업이 일시 중단될 때 반환됩니다. 비동기 메서드가 해당 작업을 완료하면 작업이 완료된 것으로 표시되고 결과가 있을 경우 작업에 저장됩니다.

제어 흐름에 대한 자세한 내용은 [비동기 프로그램의 제어 흐름(Visual Basic)](control-flow-in-async-programs.md)을 참조하세요.

## <a name="BKMK_APIAsyncMethods"></a> API Async 메서드

`GetStringAsync`와 같이 비동기 프로그래밍을 지원하는 메서드를 어디에서 검색해야 할지 궁금했을 것입니다. .NET Framework 4.5 이상에는 `Async` 및 `Await`과 작동 하는 많은 멤버가 포함 되어 있습니다. 멤버 이름에 연결 된 "Async" 접미사와 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>의 반환 형식으로 이러한 멤버를 인식할 수 있습니다. 예를 들어, `System.IO.Stream` 클래스는 동기 메서드인 <xref:System.IO.Stream.CopyTo%2A>, <xref:System.IO.Stream.Read%2A> 및 <xref:System.IO.Stream.Write%2A>와 함께 <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.ReadAsync%2A> 및 <xref:System.IO.Stream.WriteAsync%2A>와 같은 메서드를 포함합니다.

Windows 런타임에는 Windows 앱에서 `Async` 및 `Await`와 함께 사용할 수 있는 많은 메서드도 포함되어 있습니다. 자세한 내용 및 예제 메서드를 보려면 [또는 Visual Basic에서 C# 비동기 api 호출](/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic), [비동기 프로그래밍 (Windows 런타임 앱)](https://docs.microsoft.com/previous-versions/windows/apps/hh464924(v=win.10))및 @no__t/3 ... 모든 항목을 참조 하세요. .NET Framework와 Windows 런타임 @ no__t 간 브리징-0.

## <a name="BKMK_Threads"></a> 스레드

비동기 메서드는 비차단 작업으로 의도되었습니다. 비동기 메서드의 `Await` 식은 대기 작업이 실행 되는 동안 현재 스레드를 차단 하지 않습니다. 대신에 이 식은 메서드의 나머지를 연속으로 등록하고 제어 기능을 비동기 메서드 호출자에게 반환합니다.

`Async` 및 `Await` 키워드로 인해 추가 스레드가 생성되지 않습니다. 비동기 메서드는 자체 스레드에서 실행 되지 않으므로 비동기 메서드는 다중 스레딩을 필요로 하지 않습니다. 메서드는 현재 동기화 컨텍스트에서 실행되고 메서드가 활성화된 경우에만 스레드에서 시간을 사용합니다. <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType>을 사용하여 CPU 바인딩 작업을 백그라운드 스레드로 이동할 수 있지만 백그라운드 스레드는 결과를 사용할 수 있을 때까지 기다리는 프로세스를 도와주지 않습니다.

비동기 프로그래밍에 대한 비동기 기반 접근 방법은 거의 모든 경우에 기존 방법보다 선호됩니다. 특히이 방법은 코드가 더 간단 하 고 경합 상태를 방지할 필요가 없기 때문에 i/o 바인딩된 작업에 대 한 <xref:System.ComponentModel.BackgroundWorker> 보다 좋습니다. 비동기 프로그래밍은 코드 실행에 대한 조합 세부 정보를 <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType>이 스레드 풀로 변환하는 작업과 구분하기 때문에 <xref:System.ComponentModel.BackgroundWorker>을 함께 사용하는 비동기 프로그래밍은 CPU 바인딩 작업을 위한 `Task.Run`보다 효과가 뛰어납니다.

## <a name="BKMK_AsyncandAwait"></a> Async 및 Await

[Async](../../../../visual-basic/language-reference/modifiers/async.md) 한정자를 사용해서 메서드를 비동기 메서드로 지정하면 다음 두 기능이 활성화됩니다.

- 표시된 비동기 메서드는 [Await](../../../../visual-basic/language-reference/operators/await-operator.md)를 사용하여 일시 중단 지점을 지정할 수 있습니다. Await 연산자는 비동기 프로세스가 완료될 때까지 비동기 메서드가 해당 지점을 계속할 수 없다고 지시합니다. 한편, 컨트롤이 비동기 메서드의 호출자로 반환됩니다.

  @No__t-0 식에서 비동기 메서드를 일시 중단 해도 메서드에서 종료 되는 것이 아니라 `Finally` 블록이 실행 되지 않습니다.

- 표시된 비동기 메서드는 이 메서드를 호출한 다른 메서드에 의해 대기할 수 있습니다.

비동기 메서드는 일반적으로 `Await` 연산자를 하나 이상 포함 하지만 `Await` 식이 없으면 컴파일러 오류가 발생 하지 않습니다. 비동기 메서드가 `Await` 연산자를 사용 하 여 일시 중단 지점을 표시 하지 않는 경우 메서드는 `Async` 한정자에도 불구 하 고 동기 메서드를 실행 합니다. 컴파일러는 해당 메서드에 대해 경고를 표시합니다.

`Async` 및 `Await`은 상황별 키워드입니다. 자세한 내용 및 예제는 다음 항목을 참조하십시오.

- [비동기](../../../../visual-basic/language-reference/modifiers/async.md)
- [Await 연산자](../../../../visual-basic/language-reference/operators/await-operator.md)

## <a name="BKMK_ReturnTypesandParameters"></a> 반환 형식 및 매개 변수

.NET Framework 프로그래밍에서 비동기 메서드는 일반적으로 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>를 반환합니다. 비동기 메서드 내에서 `Await` 연산자는 호출에서 다른 비동기 메서드로 전환되는 작업에 적용됩니다.

메서드에 `TResult` 형식의 피연산자를 지정하는 [Return](../../../../visual-basic/language-reference/statements/return-statement.md) 문이 포함되어 있을 경우 <xref:System.Threading.Tasks.Task%601>를 반환 형식으로 지정합니다.

메서드에 return 문이 없거나 피연산자를 반환하지 않는 return 문이 있을 경우 반환 형식으로 `Task`를 사용합니다.

다음 예제에서는 <xref:System.Threading.Tasks.Task%601> 또는 <xref:System.Threading.Tasks.Task>을 반환 하는 메서드를 선언 하 고 호출 하는 방법을 보여 줍니다.

```vb
' Signature specifies Task(Of Integer)
Async Function TaskOfTResult_MethodAsync() As Task(Of Integer)

    Dim hours As Integer
    ' . . .
    ' Return statement specifies an integer result.
    Return hours
End Function

' Calls to TaskOfTResult_MethodAsync
Dim returnedTaskTResult As Task(Of Integer) = TaskOfTResult_MethodAsync()
Dim intResult As Integer = Await returnedTaskTResult
' or, in a single statement
Dim intResult As Integer = Await TaskOfTResult_MethodAsync()

' Signature specifies Task
Async Function Task_MethodAsync() As Task

    ' . . .
    ' The method has no return statement.
End Function

' Calls to Task_MethodAsync
Task returnedTask = Task_MethodAsync()
Await returnedTask
' or, in a single statement
Await Task_MethodAsync()
```

반환된 각 작업은 진행 중인 작업을 나타냅니다. 작업은 비동기 프로세스 상태에 대한 정보를 캡슐화하며, 결과적으로 프로세스의 최종 결과 또는 성공하지 못한 경우 프로세스가 발생시키는 예외에 대한 정보를 캡슐화합니다.

또한 비동기 메서드는 `Sub` 메서드일 수도 있습니다. 이 반환 형식은 기본적으로 반환 형식이 필요할 때 이벤트 처리기를 정의하는 데 사용합니다. 비동기 이벤트 처리기는 비동기 프로그램의 시작점 역할을 하는 경우가 많습니다.

@No__t-0 프로시저 인 비동기 메서드는 대기 수 없으며 호출자는 메서드가 throw 하는 예외를 catch 할 수 없습니다.

비동기 메서드는 모든 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 매개 변수를 선언할 수 없지만, 이러한 매개 변수가 있는 메서드를 호출할 수는 있습니다.

자세한 내용과 예제는 [비동기 반환 형식(Visual Basic)](async-return-types.md)을 참조하세요. 비동기 메서드에서 예외를 catch하는 방법에 대한 자세한 내용은 [Try...Catch...Finally 문](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)을 참조하세요.

Windows 런타임 프로그래밍의 비동기 API에는 작업과 유사한 다음 반환 형식 중 하나가 있습니다.

- <xref:System.Threading.Tasks.Task%601>에 해당하는 <xref:Windows.Foundation.IAsyncOperation%601>
- <xref:System.Threading.Tasks.Task>에 해당하는 <xref:Windows.Foundation.IAsyncAction>
- <xref:Windows.Foundation.IAsyncActionWithProgress%601>
- <xref:Windows.Foundation.IAsyncOperationWithProgress%602>

자세한 내용 및 예제는 [또는 Visual Basic에서 C# 비동기 api 호출](/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)을 참조 하세요.

## <a name="BKMK_NamingConvention"></a> 명명 규칙

규칙에 따라 `Async` 한정자가 있는 메서드 이름에 "Async"를 추가합니다.

여기서 이벤트, 기본 클래스 또는 인터페이스 계약으로 다른 이름을 제안하는 규칙을 무시할 수 있습니다. 예를 들어 `Button1_Click`과 같은 공용 이벤트 처리기의 이름을 바꿀 수 없습니다.

## <a name="BKMK_RelatedTopics"></a> 관련 항목 및 샘플(Visual Studio)

|제목|설명|예제|
|-----------|-----------------|------------|
|[연습: Async 및 Wait (Visual Basic)를 사용 하 여 웹에 액세스 ](walkthrough-accessing-the-web-by-using-async-and-await.md)|동기 WPF 솔루션을 비동기 WPF 솔루션으로 변환하는 방법을 보여줍니다. 이 애플리케이션은 일련의 웹 사이트를 다운로드합니다.|[비동기 샘플: 웹 연습에 액세스](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)|
|[방법: 작업을 사용 하 여 비동기 연습 확장 (Visual Basic) ](how-to-extend-the-async-walkthrough-by-using-task-whenall.md)|이전 연습에 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>을 추가합니다. `WhenAll`을 사용하면 모든 다운로드가 동시에 시작됩니다.||
|[방법: Async 및 Wait (Visual Basic)를 사용 하 여 여러 웹 요청을 병렬로 수행 ](how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)|동시에 여러 작업을 시작하는 방법을 보여줍니다.|[비동기 샘플: 병렬로 여러 웹 요청 만들기](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e)|
|[비동기 반환 형식(Visual Basic)](async-return-types.md)|비동기 메서드에서 반환할 수 있는 형식을 설명하고 각 형식이 언제 적절한가를 설명합니다.||
|[비동기 프로그램의 제어 흐름(Visual Basic)](control-flow-in-async-programs.md)|비동기 프로그램에서 연속적 await 표현을 통한 컨트롤의 흐름을 자세히 추적합니다.|[비동기 샘플: 비동기 프로그램의 제어 흐름](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0)|
|[Async 애플리케이션 미세 조정(Visual Basic)](fine-tuning-your-async-application.md)|비동기 솔루션에 다음과 같은 기능을 추가하는 방법을 보여줍니다.<br /><br /> - [비동기 작업 또는 작업 목록 취소(Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md)<br />- [일정 기간 이후 비동기 작업 취소(Visual Basic)](cancel-async-tasks-after-a-period-of-time.md)<br />- [비동기 작업 하나가 완료되면 남은 비동기 작업 취소(Visual Basic)](cancel-remaining-async-tasks-after-one-is-complete.md)<br />- [비동기 작업을 여러 개 시작하고 완료될 때마다 처리(Visual Basic)](start-multiple-async-tasks-and-process-them-as-they-complete.md)|[비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)|
|[비동기 응용 프로그램에서 재진입 처리(Visual Basic)](handling-reentrancy-in-async-apps.md)|활성 비동기 작업을 실행 하는 동안 다시 시작 되는 경우를 처리 하는 방법을 보여 줍니다.||
|[WhenAny: .NET Framework와 Windows 런타임 간 브리징](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/jj635140(v=vs.120))|Windows 런타임 메서드에 <xref:System.Threading.Tasks.Task.WhenAny%2A>를 사용할 수 있도록 .NET Framework의 작업 형식과 Windows 런타임의 IAsyncOperations를 연결하는 방법을 보여 줍니다.|[비동기 샘플: .NET 및 Windows 런타임 간 연결(AsTask 및 WhenAny)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/jj635140(v=vs.120))|
|비동기 취소: .NET Framework와 Windows 런타임 간 브리징|Windows 런타임 메서드에 <xref:System.Threading.CancellationTokenSource>를 사용할 수 있도록 .NET Framework의 작업 형식과 Windows 런타임의 IAsyncOperations를 연결하는 방법을 보여 줍니다.|[비동기 샘플: .NET 및 Windows 런타임 간 연결(AsTask & 취소)](https://code.msdn.microsoft.com/Async-Sample-Bridging-9479eca3)|
|[파일 액세스에 Async 사용(Visual Basic)](using-async-for-file-access.md)|async 및 await를 사용하여 파일에 액세스하는 이점을 나열하고 보여줍니다.||
|[TAP(작업 기반 비동기 패턴)](../../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)|.NET Framework의 새로운 비동기 패턴에 대해 설명합니다. 패턴은 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 형식을 기반으로 합니다.||
|[비동기 Channel 9 비디오](https://channel9.msdn.com/search?term=async+&type=All)|비동기 프로그래밍에 대한 다양한 비디오로 연결되는 링크를 제공합니다.||

## <a name="BKMK_CompleteExample"></a> 전체 예제

다음 코드는 이 항목에서 설명하는 WPF(Windows Presentation Foundation) 애플리케이션의 MainWindow.xaml.vb 파일입니다. [비동기 샘플: "Async 및 Await를 사용하는 비동기 프로그래밍"의 예제](https://docs.microsoft.com/samples/dotnet/samples/async-and-await-vb/)에서 샘플을 다운로드할 수 있습니다.

[!code-vb[async](~/samples/async/async-and-await/vb/MainWindow.xaml.vb)]

## <a name="see-also"></a>참조

- [Await 연산자](../../../../visual-basic/language-reference/operators/await-operator.md)
- [비동기](../../../../visual-basic/language-reference/modifiers/async.md)
