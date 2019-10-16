---
title: async 및 await를 사용한 TAP(작업 비동기 프로그래밍) 모델(C#)
ms.date: 05/22/2017
ms.assetid: 9bcf896a-5826-4189-8c1a-3e35fa08243a
ms.openlocfilehash: 3ced168bada4167418bf27861c5b8666b02aa70e
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291332"
---
# <a name="task-asynchronous-programming-model"></a>작업 비동기 프로그래밍 모델

비동기 프로그래밍을 사용하여 성능 병목 현상을 방지하고 애플리케이션의 전체적인 응답성을 향상할 수 있습니다. 그러나 비동기 애플리케이션을 쓰는 일반적인 기술이 복잡하여 해당 애플리케이션을 쓰고, 디버깅하고, 유지 관리하기 어려울 수 있습니다.

[C# 5](../../../whats-new/csharp-version-history.md#c-version-50)에는 .NET Framework 4.5 이상, .NET Core 및 Windows 런타임의 비동기 지원을 활용하는 간단한 비동기 프로그래밍 접근 방법이 도입되었습니다. 컴파일러는 개발자가 하던 어려운 작업을 수행하고, 애플리케이션은 동기 코드와 비슷한 논리 구조를 유지합니다. 따라서 약간의 노력만으로도 비동기 프로그래밍의 모든 장점을 누릴 수 있습니다.

이 항목에서는 비동기 프로그래밍을 사용하는 시기 및 방법에 대한 개요를 제공하고 특정 세부 정보 및 예제가 포함된 지원 항목에 대한 링크가 포함되어 있습니다.

## <a name="BKMK_WhentoUseAsynchrony"></a> 반응성을 향상시키는 비동기

비동기는 웹 액세스와 같이 차단 가능성이 있는 작업에 반드시 필요합니다. 웹 리소스에 대한 액세스 속도가 느리거나 지연됩니다. 동기 프로세스 안에서 이러한 활동이 차단되면 전체 애플리케이션이 기다려야 합니다. 비동기 프로세스에서 애플리케이션은 잠재적인 차단 작업이 완료될 때까지 웹 리소스에 의존하지 않는 다른 작업을 계속 수행할 수 있습니다.

다음 표에는 비동기 프로그래밍으로 응답성이 향상되는 일반적인 영역이 나와 있습니다. .NET 및 Windows 런타임에서 나열된 API에는 비동기 프로그래밍을 지원하는 메서드가 포함되어 있습니다.

| 애플리케이션 영역    | 비동기 메서드가 있는 .NET 형식     | 비동기 메서드가 있는 Windows 런타임 형식  |
|---------------------|-----------------------------------|-------------------------------------------|
|웹 액세스|<xref:System.Net.Http.HttpClient>|<xref:Windows.Web.Syndication.SyndicationClient>|
|파일 작업|<xref:System.IO.StreamWriter>, <xref:System.IO.StreamReader>, <xref:System.Xml.XmlReader>|<xref:Windows.Storage.StorageFile>|
|이미지 작업||<xref:Windows.Media.Capture.MediaCapture>, <xref:Windows.Graphics.Imaging.BitmapEncoder>, <xref:Windows.Graphics.Imaging.BitmapDecoder>|
|WCF 프로그래밍|[동기 및 비동기 작업](../../../../framework/wcf/synchronous-and-asynchronous-operations.md)||

모든 UI 관련 작업이 대체로 스레드 한 개를 공유하므로 비동기는 특히 UI 스레드에 액세스하는 애플리케이션의 변수를 증명합니다. 동기 애플리케이션에서 임의의 프로세스가 차단되면 모든 프로세스가 차단됩니다. 애플리케이션이 응답을 중지하면 기다리지 않고 애플리케이션이 실패한 것으로 결론을 내릴 것입니다.

비동기 메서드를 사용하면 애플리케이션이 UI에 계속 응답합니다. 예를 들어 창의 크기를 조정하거나 최소화할 수 있습니다. 또는 애플리케이션이 완료될 때까지 기다리고 싶지 않다면 애플리케이션을 종료할 수 있습니다.

비동기 기반 접근 방식을 사용하면 비동기 작업을 디자인할 때 선택할 수 있는 옵션 목록에 자동 전송과 동일한 기능을 추가할 수 있습니다. 즉, 더 적은 개발자의 노력으로 기존 비동기 프로그래밍의 이점을 모두 활용할 수 있습니다.

## <a name="BKMK_HowtoWriteanAsyncMethod"></a> 작성이 간편한 비동기 메서드

C#의 [async](../../../language-reference/keywords/async.md) 및 [await](../../../language-reference/operators/await.md) 키워드는 비동기 프로그래밍의 핵심입니다. 이 두 개의 키워드를 사용하면 .NET Framework, .NET Core 또는 Windows 런타임의 리소스를 사용하여 동기 메서드를 만드는 것만큼 쉽게 비동기 메서드를 만들 수 있습니다. `async` 키워드를 사용하여 정의하는 비동기 메서드를 *비동기 메서드*라고 합니다.

다음 예제에서는 비동기 메서드를 보여줍니다. 코드의 거의 모든 내용이 익숙할 것입니다.

이 항목의 마지막에 완전한 WPF(Windows Presentation Foundation) 예제 파일이 있으며, [비동기 샘플: "Async 및 Await를 사용하는 비동기 프로그래밍"의 예제](https://docs.microsoft.com/samples/dotnet/samples/async-and-await-cs/)에서 샘플을 다운로드할 수 있습니다.

```csharp
async Task<int> AccessTheWebAsync()
{ 
    // You need to add a reference to System.Net.Http to declare client.
    var client = new HttpClient();

    // GetStringAsync returns a Task<string>. That means that when you await the
    // task you'll get a string (urlContents).
    Task<string> getStringTask = client.GetStringAsync("https://docs.microsoft.com/dotnet");

    // You can do work here that doesn't rely on the string from GetStringAsync.
    DoIndependentWork();

    // The await operator suspends AccessTheWebAsync.
    //  - AccessTheWebAsync can't continue until getStringTask is complete.
    //  - Meanwhile, control returns to the caller of AccessTheWebAsync.
    //  - Control resumes here when getStringTask is complete. 
    //  - The await operator then retrieves the string result from getStringTask.
    string urlContents = await getStringTask;

    // The return statement specifies an integer result.
    // Any methods that are awaiting AccessTheWebAsync retrieve the length value.
    return urlContents.Length;
}
```

위의 샘플에서 몇 가지 사례를 알아볼 수 있습니다. 메서드 서명부터 시작해봅시다. 여기에는 `async` 한정자가 포함됩니다. 반환 형식은 `Task<int>`입니다(추가 옵션은 "반환 형식" 섹션 참조). 메서드 이름은 `Async`로 끝납니다. 메서드의 본문에서 `GetStringAsync`가 `Task<string>`을 반환합니다. 즉, 작업을 `await`하는 경우 `string`을 받게 됩니다(`urlContents`).  작업을 대기하기 전에 `GetStringAsync`의 `string`을 사용하지 않는 작업을 수행할 수 있습니다.

`await` 연산자에 주의하세요. `AccessTheWebAsync`를 일시 중단합니다.

- `AccessTheWebAsync`는 `getStringTask`가 완료될 때까지 계속할 수 없습니다.
- 반면 제어는 `AccessTheWebAsync`의 호출자에 반환됩니다.
- `getStringTask`가 완료되면 컨트롤이 다시 시작됩니다.
- 그런 다음, `await` 연산자가 `getStringTask`에서 `string` 결과를 검색합니다.

반환 문은 정수 결과를 지정합니다. `AccessTheWebAsync`를 대기하는 메서드는 길이 값을 검색합니다.

`AccessTheWebAsync`에 `GetStringAsync` 호출과 해당 완료 대기 사이에 수행할 수 있는 작업이 없는 경우 다음 단일 문을 호출하고 대기하여 코드를 단순화할 수 있습니다.

```csharp
string urlContents = await client.GetStringAsync("https://docs.microsoft.com/dotnet");
```

이전 예제가 비동기 메서드인 이유는 다음과 같은 특성 때문입니다.

- 메서드 시그니처에 `async` 한정자가 포함됩니다.
- 비동기 메서드의 이름은 규칙에 따라 "Async" 접미사로 끝납니다.
- 반환 형식은 다음 형식 중 하나입니다.

  - 메서드에 연산자 형식이 `TResult`인 Return 문이 있는 경우 <xref:System.Threading.Tasks.Task%601>입니다.
  - 메서드에 반환 문이 포함되지 않았거나 피연산자가 없는 반환 문이 포함된 경우 <xref:System.Threading.Tasks.Task>입니다.
  - 비동기 이벤트 처리기를 작성하는 경우 `void`입니다.
  - `GetAwaiter` 메서드가 포함된 모든 기타 형식(C# 7.0부터).

  자세한 내용은 [반환 형식 및 매개 변수](#BKMK_ReturnTypesandParameters) 섹션을 참조하세요.

- 메서드는 일반적으로 비동기 작업이 완료될 때까지 메서드가 계속될 수 없는 지점을 표시하는 하나 이상의 `await` 표현을 포함하고 있습니다. 한편, 메서드가 일시 중단되고 컨트롤이 메서드의 호출자로 반환됩니다. 이 항목의 다음 단원은 일시 중단 지점에서 발생하는 상황을 보여줍니다.

비동기 메서드에서는 제공된 키워드 및 형식을 사용해서 수행하려는 작업을 나타내고, 컴파일러는 일시 중단된 메서드에서 컨트롤이 대기 지점으로 반환될 때 수행되어야 하는 항목을 추적하는 등의 나머지 작업을 수행합니다. 루프 및 예외 처리와 같은 일부 루틴 프로세스는 기존의 비동기 코드에서 처리하기 어려울 수 있습니다. 비동기 메서드에서는 동기 솔루션에서와 같이 필요한 만큼 이러한 요소를 작성하여 문제를 해결합니다.

이전 버전의 .NET Framework의 비동기에 대한 자세한 내용은 [TPL 및 일반적인 .NET Framework 비동기 프로그래밍](../../../../standard/parallel-programming/tpl-and-traditional-async-programming.md)을 참조하세요.

## <a name="BKMK_WhatHappensUnderstandinganAsyncMethod"></a> 비동기 메서드에서 수행되는 작업

비동기 프로그래밍을 이해하는 데 있어 가장 중요한 점은 메서드에서 메서드로 제어 흐름을 이동하는 방법입니다. 다음 다이어그램에서 과정을 안내합니다.

![비동기 프로그램 추적](./media/task-asynchronous-programming-model/navigation-trace-async-program.png "NavigationTrace")

다이어그램의 숫자는 다음 단계에 해당하고 사용자가 "시작" 단추를 클릭할 때 시작됩니다.

1. 이벤트 처리기가 호출되어 `AccessTheWebAsync` 비동기 메서드를 기다립니다.

2. `AccessTheWebAsync`는 <xref:System.Net.Http.HttpClient> 인스턴스를 만들고 <xref:System.Net.Http.HttpClient.GetStringAsync%2A> 비동기 메서드를 호출하여 웹 사이트의 내용을 문자열로 다운로드합니다.

3. `GetStringAsync`에서 특정 작업이 발생하여 진행이 일시 중단됩니다. 웹 사이트에서 다운로드 또는 다른 차단 작업을 수행할 때까지 기다려야 할 수 있습니다. 리소스를 차단하지 않기 위해 `GetStringAsync`는 해당 호출자인 `AccessTheWebAsync`에 제어 권한을 양도합니다.

     `GetStringAsync`는 `TResult`가 문자열인 <xref:System.Threading.Tasks.Task%601>를 반환하고, `AccessTheWebAsync`는 `getStringTask` 변수에 작업을 할당합니다. 이 작업은 작업이 완료될 때 실제 문자열 값을 생성하기 위한 코드와 함께 `GetStringAsync`를 호출하는 지속적인 프로세스를 나타냅니다.

4. `getStringTask`가 아직 대기되지 않았으므로 `AccessTheWebAsync`가 `GetStringAsync`의 최종 결과에 무관한 다른 작업을 계속할 수 있습니다. 이 작업은 동기 메서드 `DoIndependentWork`를 호출하여 나타냅니다.

5. `DoIndependentWork`는 작업을 수행하고 호출자에게 반환하는 동기 메서드입니다.

6. `AccessTheWebAsync`에 `getStringTask` 결과 없이 수행할 수 있는 작업이 없습니다. 다음으로 `AccessTheWebAsync`는 다운로드한 문자열의 길이를 계산하여 반환하려 하지만, 메서드가 문자열을 확인할 때까지 해당 값을 계산할 수 없습니다.

     따라서 `AccessTheWebAsync`는 await 연산자를 사용해서 해당 프로세스를 일시 중단하고 `AccessTheWebAsync`를 호출한 메서드에 제어 권한을 양도합니다. `AccessTheWebAsync`는 `Task<int>`를 호출자에게 반환합니다. 작업은 다운로드한 문자열의 길이인 정수 결과를 만든다는 약속을 나타냅니다.

    > [!NOTE]
    > `AccessTheWebAsync`가 대기하기 전에 `GetStringAsync`(및 `getStringTask`)가 완료되면 `AccessTheWebAsync`에서 컨트롤이 유지됩니다. 일시 중단 및 `AccessTheWebAsync`의 반환 비용은 호출된 비동기 프로세스(`getStringTask`)가 이미 완료되었고 `AccessTheWebAsync`가 최종 결과를 기다릴 필요가 없다면 낭비됩니다.

     호출자(이 예제의 이벤트 처리기) 내에서 처리 패턴이 계속됩니다. 호출자가 해당 결과를 기다리거나 즉시 기다리기 전에 `AccessTheWebAsync`에서 결과에 의존하지 않는 다른 작업을 수행할 수 있습니다.   `AccessTheWebAsync`에 대한 이벤트가 대기 중이며 `AccessTheWebAsync`가 `GetStringAsync`를 대기 중입니다.

7. `GetStringAsync`가 완료되고 문자열 결과를 생성합니다. `GetStringAsync`를 호출할 경우 문자열 결과가 예상대로 반환되지 않습니다. (메서드가 이미 3단계에서 작업을 반환했습니다.) 대신 문자열 결과가 메서드 `getStringTask`의 완료를 나타내는 작업에 저장됩니다. await 연산자가 `getStringTask`에서 결과를 검색합니다. 할당 문은 검색된 결과를 `urlContents`에 할당합니다.

8. `AccessTheWebAsync`에 문자열 결과가 있는 경우 메서드가 문자열 길이를 계산할 수 있습니다. 그런 다음 `AccessTheWebAsync` 작업도 완료되고 대기 이벤트 처리기를 다시 시작할 수 있습니다. 이 항목 뒷부분의 전체 예에서는 이벤트 처리기가 길이 결과 값을 검색하고 출력하는지 확인할 수 있습니다.
비동기 프로그래밍을 처음 접하는 사용자인 경우 동기 동작과 비동기 동작의 차이점을 살펴보세요. 비동기 메서드는 작업이 완료될 때 반환되지만(5단계) 비동기 메서드는 작업이 일시 중단될 때 반환됩니다. 비동기 메서드가 해당 작업을 완료하면 작업이 완료된 것으로 표시되고 결과가 있을 경우 작업에 저장됩니다.

제어 흐름에 대한 자세한 내용은 [비동기 프로그램의 제어 흐름(C#)](control-flow-in-async-programs.md)을 참조하세요.

## <a name="BKMK_APIAsyncMethods"></a> API 비동기 메서드

`GetStringAsync`와 같이 비동기 프로그래밍을 지원하는 메서드를 어디에서 검색해야 할지 궁금했을 것입니다. .NET Framework 4.5 이상 및 .NET Core에는 `async` 및 `await`에 작동하는 많은 멤버가 포함되어 있습니다. 멤버 이름에 붙는 “Async” 접미사와 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>의 반환 형식으로 멤버를 인식할 수 있습니다. 예를 들어, `System.IO.Stream` 클래스는 동기 메서드인 <xref:System.IO.Stream.CopyTo%2A>, <xref:System.IO.Stream.Read%2A> 및 <xref:System.IO.Stream.Write%2A>와 함께 <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.ReadAsync%2A> 및 <xref:System.IO.Stream.WriteAsync%2A>와 같은 메서드를 포함합니다.

Windows 런타임에는 Windows 앱에서 `async` 및 `await`와 함께 사용할 수 있는 많은 메서드도 포함되어 있습니다. 자세한 내용은 UWP 개발의 경우 [스레딩 및 비동기 프로그래밍](/windows/uwp/threading-async/)을 참조하세요. Windows 런타임 이전 버전을 사용하는 경우 [비동기 프로그래밍(Windows 스토어 앱)](https://docs.microsoft.com/previous-versions/windows/apps/hh464924(v=win.10)) 및 [빠른 시작: C# 또는 Visual Basic에서 비동기 API 호출](https://docs.microsoft.com/previous-versions/windows/apps/hh452713(v=win.10))을 참조하세요.

## <a name="BKMK_Threads"></a> 스레드

비동기 메서드는 비차단 작업으로 의도되었습니다. 비동기 메서드의 `await` 식은 대기한 작업이 실행되는 동안 현재 스레드를 차단하지 않습니다. 대신에 이 식은 메서드의 나머지를 연속으로 등록하고 제어 기능을 비동기 메서드 호출자에게 반환합니다.

`async` 및 `await` 키워드로 인해 추가 스레드가 생성되지 않습니다. 비동기 메서드는 자체 스레드에서 실행되지 않으므로 다중 스레드가 필요하지 않습니다. 메서드는 현재 동기화 컨텍스트에서 실행되고 메서드가 활성화된 경우에만 스레드에서 시간을 사용합니다. <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType>을 사용하여 CPU 바인딩 작업을 백그라운드 스레드로 이동할 수 있지만 백그라운드 스레드는 결과를 사용할 수 있을 때까지 기다리는 프로세스를 도와주지 않습니다.

비동기 프로그래밍에 대한 비동기 기반 접근 방법은 거의 모든 경우에 기존 방법보다 선호됩니다. 특히, 이 접근 방식은 코드가 더 간단하고 경합 조건을 방지할 필요가 없기 때문에 I/O 바인딩 작업의 <xref:System.ComponentModel.BackgroundWorker> 클래스보다 효과적입니다. 비동기 프로그래밍은 코드 실행에 대한 조합 세부 정보를 `Task.Run`가 스레드 풀로 변환하는 작업과 구분하기 때문에 <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> 메서드를 함께 사용하는 비동기 프로그래밍은 CPU 바인딩 작업을 위한 <xref:System.ComponentModel.BackgroundWorker>보다 효과가 뛰어납니다.

## <a name="BKMK_AsyncandAwait"></a> async 및 await

[async](../../../language-reference/keywords/async.md) 한정자를 사용해서 메서드를 비동기 메서드로 지정하면 다음 두 기능이 활성화됩니다.

- 표시된 비동기 메서드는 [Await](../../../language-reference/operators/await.md)를 사용하여 일시 중단 지점을 지정할 수 있습니다. `await` 연산자는 대기된 비동기 프로세스가 완료될 때까지 비동기 메서드가 해당 지점을 지나 계속할 수 없도록 컴파일러에 지시합니다. 한편, 컨트롤이 비동기 메서드의 호출자로 반환됩니다.

     `await` 식에서 비동기 메서드를 일시 중단하더라도 메서드가 종료되지는 않으며 `finally` 블록이 실행되지 않습니다.

- 표시된 비동기 메서드는 이 메서드를 호출한 다른 메서드에 의해 대기할 수 있습니다.

비동기 메서드는 일반적으로 `await` 연산자를 하나 이상 가지고 있지만, `await` 식이 없는 경우 컴파일러 오류가 발생하지는 않습니다. 비동기 메서드에서 `await` 연산자를 사용하여 일시 중단 시점을 표시하지 않는 경우 메서드가 `async` 한정자에 상관없이 동기 메서드가 실행되는 방식으로 실행됩니다. 컴파일러는 해당 메서드에 대해 경고를 표시합니다.

`async` 및 `await`은 상황별 키워드입니다. 자세한 내용과 예제는 다음 항목을 참조하세요.

- [async](../../../language-reference/keywords/async.md)
- [await](../../../language-reference/operators/await.md)

## <a name="BKMK_ReturnTypesandParameters"></a> 반환 형식 및 매개 변수

비동기 메서드는 일반적으로 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>를 반환합니다. 비동기 메서드 내에서 `await` 연산자는 호출에서 다른 비동기 메서드로 전환되는 작업에 적용됩니다.

메서드에 `TResult` 형식의 피연산자를 지정하는 [`return`](../../../language-reference/keywords/return.md) 문이 포함되어 있을 경우 <xref:System.Threading.Tasks.Task%601>를 반환 형식으로 지정합니다.

메서드에 return 문이 없거나 피연산자를 반환하지 않는 return 문이 있을 경우 반환 형식으로 <xref:System.Threading.Tasks.Task>를 사용합니다.

C# 7.0부터는 형식에 `GetAwaiter` 메서드가 포함된 경우 다른 반환 형식을 지정할 수도 있습니다. <xref:System.Threading.Tasks.ValueTask%601>가 이러한 형식의 예입니다. [System.Threading.Tasks.Extension](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) NuGet 패키지에서 사용할 수 있습니다.

다음 예제는 <xref:System.Threading.Tasks.Task%601> 또는 <xref:System.Threading.Tasks.Task>를 반환하는 메서드를 선언하고 호출하는 방법을 보여줍니다.

```csharp
// Signature specifies Task<TResult>
async Task<int> GetTaskOfTResultAsync()
{
    int hours = 0;
    await Task.Delay(0);
    // Return statement specifies an integer result.
    return hours;
}

// Calls to GetTaskOfTResultAsync
Task<int> returnedTaskTResult = GetTaskOfTResultAsync();
int intResult = await returnedTaskTResult;
// or, in a single statement
int intResult = await GetTaskOfTResultAsync();

// Signature specifies Task
async Task GetTaskAsync()
{
    await Task.Delay(0);
    // The method has no return statement.
}

// Calls to GetTaskAsync
Task returnedTask = GetTaskAsync();
await returnedTask;
// or, in a single statement
await GetTaskAsync();
```

반환된 각 작업은 진행 중인 작업을 나타냅니다. 작업은 비동기 프로세스 상태에 대한 정보를 캡슐화하며, 결과적으로 프로세스의 최종 결과 또는 성공하지 못한 경우 프로세스가 발생시키는 예외에 대한 정보를 캡슐화합니다.

비동기 메서드의 반환 형식은 `void`일 수 있습니다. 이 반환 형식은 기본적으로 `void` 반환 형식이 필요할 때 이벤트 처리기를 정의하는 데 사용합니다. 비동기 이벤트 처리기는 비동기 프로그램의 시작점 역할을 하는 경우가 많습니다.

`void` 반환 형식을 가진 비동기 메서드는 대기할 수 없습니다. 또한 void를 반환하는 메서드의 호출자는 메서드가 throw하는 예외를 catch할 수 없습니다.

비동기 메서드는 모든 [in](../../../language-reference/keywords/in-parameter-modifier.md), [ref](../../../language-reference/keywords/ref.md) 또는 [out](../../../language-reference/keywords/out-parameter-modifier.md) 매개 변수를 선언할 수 없지만, 이러한 매개 변수가 있는 메서드를 호출할 수는 있습니다. 마찬가지로 비동기 메서드는 참조 반환 값을 사용하여 메서드를 호출할 수 있지만 참조를 통해 값을 반환할 수 없습니다.

자세한 내용과 예제는 [비동기 반환 형식(C#)](./async-return-types.md)을 참조하세요. 비동기 메서드에서 예외를 처리하는 방법에 대한 자세한 내용은 [try-catch](../../../language-reference/keywords/try-catch.md)를 참조하세요.

Windows 런타임 프로그래밍의 비동기 API에는 작업과 유사한 다음 반환 형식 중 하나가 있습니다.

- <xref:System.Threading.Tasks.Task%601>에 해당하는 <xref:Windows.Foundation.IAsyncOperation%601>
- <xref:System.Threading.Tasks.Task>에 해당하는 <xref:Windows.Foundation.IAsyncAction>
- <xref:Windows.Foundation.IAsyncActionWithProgress%601>
- <xref:Windows.Foundation.IAsyncOperationWithProgress%602>

## <a name="BKMK_NamingConvention"></a> 명명 규칙

규칙에 따라 일반적으로 대기 가능한 형식(예: `Task`, `Task<T>`, `ValueTask`, `ValueTask<T>`)을 반환하는 메서드에는 "Async"로 끝나는 이름을 사용해야 합니다. 비동기 작업을 시작하지만 대기 가능한 형식을 반환하지 않는 메서드는 "Async"로 끝나는 이름을 사용하지 않아야 하지만, "Begin", "Start" 또는 일부 다른 동사로 시작하여 이 메서드가 작업 결과를 반환하거나 예외가 발생하지 않음을 알려야 합니다.

여기서 이벤트, 기본 클래스 또는 인터페이스 계약으로 다른 이름을 제안하는 규칙을 무시할 수 있습니다. 예를 들어, `Button1_Click`과 같은 공용 이벤트 처리기의 이름을 변경할 수 없습니다.

## <a name="BKMK_RelatedTopics"></a> 관련 항목 및 샘플(Visual Studio)

|제목|설명|예제|
|-----------|-----------------|------------|
|[연습: async 및 await를 사용하여 웹에 액세스(C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md)|동기 WPF 솔루션을 비동기 WPF 솔루션으로 변환하는 방법을 보여줍니다. 이 애플리케이션은 일련의 웹 사이트를 다운로드합니다.|[비동기 샘플: 웹 연습에 액세스](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)|
|[방법: Task.WhenAll을 사용하여 비동기 연습 확장(C#)](./how-to-extend-the-async-walkthrough-by-using-task-whenall.md)|이전 연습에 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>을 추가합니다. `WhenAll`을 사용하면 모든 다운로드가 동시에 시작됩니다.||
|[방법: async 및 await를 사용하여 병렬로 여러 웹 요청 만들기(C#)](./how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)|동시에 여러 작업을 시작하는 방법을 보여줍니다.|[비동기 샘플: 병렬로 여러 웹 요청 만들기](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e)|
|[비동기 반환 형식(C#)](./async-return-types.md)|비동기 메서드에서 반환할 수 있는 형식을 설명하고 각 형식이 언제 적절한가를 설명합니다.||
|[비동기 프로그램의 제어 흐름(C#)](./control-flow-in-async-programs.md)|비동기 프로그램에서 연속적 await 표현을 통한 컨트롤의 흐름을 자세히 추적합니다.|[비동기 샘플: 비동기 프로그램의 제어 흐름](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0)|
|[Async 애플리케이션 미세 조정(C#)](./fine-tuning-your-async-application.md)|비동기 솔루션에 다음과 같은 기능을 추가하는 방법을 보여줍니다.<br /><br /> - [비동기 작업 또는 작업 목록 취소(C#)](./cancel-an-async-task-or-a-list-of-tasks.md)<br />- [일정 기간 이후 비동기 작업 취소(C#)](./cancel-async-tasks-after-a-period-of-time.md)<br />- [비동기 작업 하나가 완료되면 남은 비동기 작업 취소(C#)](./cancel-remaining-async-tasks-after-one-is-complete.md)<br />- [비동기 작업을 여러 개 시작하고 완료될 때마다 처리(C#)](./start-multiple-async-tasks-and-process-them-as-they-complete.md)|[비동기 샘플: 애플리케이션 미세 조정](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)|
|[비동기 앱에서 재진입 처리(C#)](./handling-reentrancy-in-async-apps.md)|비동기 작업이 실행되는 동안 현재 비동기 작업을 다시 시작하는 경우 처리 방법을 보여줍니다.||
|[WhenAny: .NET Framework와 Windows 런타임 간 브리징](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/jj635140(v=vs.120))|Windows 런타임 메서드에 <xref:System.Threading.Tasks.Task.WhenAny%2A>를 사용할 수 있도록 .NET Framework의 작업 형식과 Windows 런타임의 IAsyncOperations를 연결하는 방법을 보여 줍니다.|[비동기 샘플: .NET 및 Windows 런타임 간 연결(AsTask 및 WhenAny)](https://code.msdn.microsoft.com/Async-Sample-Bridging-d6a2f739)|
|비동기 취소: .NET Framework와 Windows 런타임 간 브리징|Windows 런타임 메서드에 <xref:System.Threading.CancellationTokenSource>를 사용할 수 있도록 .NET Framework의 작업 형식과 Windows 런타임의 IAsyncOperations를 연결하는 방법을 보여 줍니다.|[비동기 샘플: .NET 및 Windows 런타임 간 연결(AsTask & 취소)](https://code.msdn.microsoft.com/Async-Sample-Bridging-9479eca3)|
|[파일 액세스에 Async 사용(C#)](./using-async-for-file-access.md)|async 및 await를 사용하여 파일에 액세스하는 이점을 나열하고 보여줍니다.||
|[TAP(작업 기반 비동기 패턴)](../../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)|.NET Framework의 새로운 비동기 패턴에 대해 설명합니다. 패턴은 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 형식을 기반으로 합니다.||
|[비동기 Channel 9 비디오](https://channel9.msdn.com/search?term=async%20&type=All#pubDate=year&ch9Search&lang-en=en)|비동기 프로그래밍에 대한 다양한 비디오로 연결되는 링크를 제공합니다.||

## <a name="BKMK_CompleteExample"></a> 전체 예제

다음 코드는 이 문서에서 설명하는 WPF 애플리케이션의 *MainWindow.xaml.cs* 파일입니다. [비동기 샘플: "Async 및 Await를 사용하는 비동기 프로그래밍"의 예제](https://docs.microsoft.com/samples/dotnet/samples/async-and-await-cs/)에서 샘플을 다운로드할 수 있습니다.

[!code-csharp[async](~/samples/async/async-and-await/cs/MainWindow.xaml.cs)] 

## <a name="see-also"></a>참고 항목

- [async](../../../language-reference/keywords/async.md)
- [await](../../../language-reference/operators/await.md)
- [비동기 프로그래밍](../../../async.md)
- [비동기 개요](../../../../standard/async.md)
 
