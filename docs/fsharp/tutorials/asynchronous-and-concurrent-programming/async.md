---
title: 비동기 프로그래밍
description: 에 대해 알아봅니다 하는 방법 F# 는 사용 하기 쉬운 및 언어에 자연 스러운 언어 수준 프로그래밍 모델을 통해 비동기 프로그래밍이 수행 됩니다.
ms.date: 06/20/2016
ms.openlocfilehash: 8cd7d7bcecabe8ea2c33a4787fe9ebbadd67fe67
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753598"
---
# <a name="async-programming-in-f"></a>F #의 비동기 프로그래밍\#

> [!NOTE]
> 이 문서에 일부 잘못 된 검색 된 합니다.  다시 작성 되 고 됩니다.  참조 [문제 #666](https://github.com/dotnet/docs/issues/666) 변경 내용에 대해 자세히 알아보려면 합니다.

비동기 프로그래밍에서 F# 사용은 쉽고 자연 언어 설계 언어 수준 프로그래밍 모델을 통해 수행할 수 있습니다.

비동기 프로그래밍의 핵심 F# 은 `Async<'T>`, 백그라운드에서 실행을 트리거할 수 있는 작업의 표현을 위치 `'T` 특수 통해 형식 반환 됩니다 `return` 키워드 또는 `unit` 하는 경우 비동기 워크플로 반환할 결과가 있습니다.

주요 개념은 비동기 식의 형식이 `Async<'T>`는 단순히 _사양_ 비동기 컨텍스트를 수행 해야 하는 작업입니다. 시작 함수 중 하나를 사용 하 여 명시적으로 시작할 때까지 실행 되지 않습니다 (같은 `Async.RunSynchronously`). 다른 방식으로 작업을 수행 하는 방법에 대 한 생각의 경우에이 결국 실제로 매우 간단 합니다.

예를 들어 주 스레드를 차단 하지 않고 dotnetfoundation.org에서 HTML을 다운로드 하 려 한다고 가정해 보겠습니다. 다음과 같이를 수행할 수 있습니다.

```fsharp
open System
open System.Net

let fetchHtmlAsync url =
    async {
        let uri = Uri(url)
        use webClient = new WebClient()

        // Execution of fetchHtmlAsync won't continue until the result
        // of AsyncDownloadString is bound.
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

let html = "https://dotnetfoundation.org" |> fetchHtmlAsync |> Async.RunSynchronously
printfn "%s" html
```

이제 끝났습니다. 사용 하는 것 외 `async`, `let!`, 및 `return`,이 방금 정상 F# 코드입니다.

주목할 만한는 구문을 몇 가지가 있습니다.

* `let!` (다른 컨텍스트에서 실행)이 표시 되는 비동기 식의 결과 바인딩합니다.
* `use!` 같은 방식으로 작동 `let!`, 하지만 범위를 벗어나면 해당 바인딩된 리소스를 삭제 합니다.
* `do!` 아무 것도 반환 하지 않는 비동기 워크플로 await 됩니다.
* `return` 비동기 식에서 결과 반환 하기만 하면 됩니다.
* `return!` 다른 비동기 워크플로 실행 하 고 해당 반환 값을 결과로 반환 합니다.

또한 정상적인 `let`, `use`, 및 `do` 키워드는 일반 함수 에서처럼 비동기 버전과 함께 사용할 수 있습니다.

## <a name="how-to-start-async-code-in-f"></a>F #의 비동기 코드를 시작 하는 방법\#

앞에서 설명한 대로 비동기 코드는 명시적으로 시작 해야 하는 다른 컨텍스트에서 수행할 작업에 대 한 사양입니다. 이렇게 하려면 두 가지는 다음과 같습니다.

1. `Async.RunSynchronously` 다른 스레드에서 비동기 워크플로 시작 하 고 그 결과 기다립니다.

    ```fsharp
    open System
    open System.Net

    let fetchHtmlAsync url =
        async {
            let uri = Uri(url)
            use webClient = new WebClient()
            let! html = webClient.AsyncDownloadString(uri)
            return html
        }

    // Execution will pause until fetchHtmlAsync finishes
    let html = "https://dotnetfoundation.org" |> fetchHtmlAsync |> Async.RunSynchronously

    // you actually have the result from fetchHtmlAsync now!
    printfn "%s" html
    ```

2. `Async.Start` 비동기 워크플로 다른 스레드에서 시작 되며 됩니다 **되지** 그 결과 기다립니다.

    ```fsharp
    open System
    open System.Net

    let uploadDataAsync url data =
        async {
            let uri = Uri(url)
            use webClient = new WebClient()
            webClient.UploadStringAsync(uri, data)
        }

    let workflow = uploadDataAsync "https://url-to-upload-to.com" "hello, world!"

    // Execution will continue after calling this!
    Async.Start(workflow)

    printfn "%s" "uploadDataAsync is running in the background..."
    ```

보다 구체적인 시나리오에 사용할 수 있는 비동기 워크플로 시작 하는 다른 방법 이며 자세히 설명 [비동기 참조에서](https://msdn.microsoft.com/library/ee370232.aspx)합니다.

### <a name="a-note-on-threads"></a>스레드에 대 한 참고 사항

"다른 스레드에서" 라는 문구는 위에서 언급 한 이지만 사실이 중요 **하기 위한 외관 비동기 워크플로 그렇다고 다중 스레딩**합니다. 워크플로 실제로 "이동" 하는 적은 양의 유용한 작업을 수행 하는 시간에 대 한 이론을 가져와 스레드 간에 합니다. 비동기 워크플로 효과적으로 "대기" (예: 결과를 반환 하는 네트워크 호출에 대 한 대기 중), 다른 유용한 작업 이동 수행까지 시간에 차용 되었습니다 스레드에 해제 됩니다. 가능한 한 효과적으로 실행 하는 시스템을 이용 하는 비동기 워크플로 있으며 특히 고용량 I/O 시나리오에 대 한 강력한 수 있습니다.

## <a name="how-to-add-parallelism-to-async-code"></a>비동기 코드에 병렬 처리를 추가 하는 방법

경우에 따라 필요한 동시에 여러 비동기 작업을 수행 하 해당 결과 수집 하 고 수 있습니다 어떤 방식으로든에서 해석 합니다. `Async.Parallel` 강제 변환할 필요 없이 포함 하는 작업 병렬 라이브러리를 사용 하지 않고도이 작업을 수행할 수 있습니다 `Task<'T>` 고 `Async<'T>` 형식입니다.

다음 예제에서는 사용할지 `Async.Parallel` 를 동시에 4 개의 인기 있는 사이트에서 HTML을 다운로드 하려면 해당 태스크를 완료 하려면 기다린 다음 다운로드 하는 HTML을 인쇄 합니다.

```fsharp
open System
open System.Net

let urlList =
    [ "https://www.microsoft.com"
      "https://www.google.com"
      "https://www.amazon.com"
      "https://www.facebook.com" ]

let fetchHtmlAsync url =
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

let getHtmlList urls =
    urls
    |> Seq.map fetchHtmlAsync   // Build an Async<'T> for each site
    |> Async.Parallel           // Returns an Async<'T []>
    |> Async.RunSynchronously   // Wait for the result of the parallel work

let htmlList = getHtmlList urlList

// We now have the downloaded HTML for each site!
for html in htmlList do
    printfn "%s" html
```

## <a name="important-info-and-advice"></a>중요한 정보 및 조언

* 사용할 수 있는 함수의 끝에 "Async"를 추가

 명명 규칙 일 뿐 이기는 하지만 API 검색 기능 등 쉽게에 해당 합니다. 동일한 루틴의 동기 버전과 비동기 인 경우에 특히 명시적으로 지정 되는 이름을 통해 비동기는 것이 좋습니다.

* 컴파일러에 수신!

F#컴파일러는 매우 엄격한, "async" 코드를 동기적으로 실행 하므로 같은 까다로운 작업을 수행 하는 거의 불가능 합니다. 경고에서 제공 하는 경우 것을 알게 하는 방법을 생각 하는 코드를 실행 하지 않습니다. 즐거운 컴파일러를 만들 수 있는, 경우 예상 대로 코드를 실행할 가능성이 높습니다.

## <a name="for-the-cvb-programmer-looking-into-f"></a>에 대 한는 C#F 살펴볼 /VB 프로그래머가\#

이 섹션에서는 비동기 모델에 익숙한 가정 C#/VB. 그렇지 않은 경우 [의 비동기 프로그래밍 C# ](../../../csharp/async.md) 시작 합니다.

간의 기본적인 차이는 C#/VB 비동기 모델 및 F# 비동기 모델입니다.

반환 하는 함수를 호출 하는 경우는 `Task` 또는 `Task<'T>`, 해당 작업이 이미 실행을 시작 합니다. 반환 된 핸들이 이미 실행 중인 비동기 작업을 나타냅니다. 반면, 호출 하는 경우 비동기 함수 F#의 `Async<'a>` 반환 될 작업을 나타냅니다 **생성** 어느 시점입니다. 비동기 작업의 수 있다는 점에서 강력 하 고는이 모델을 이해 F# 모두 연결 하 여 수월해 조건부로 수행 하 고 세부적인 제어를 시작 합니다.

다른 몇 가지 유사점 및 차이점이 있습니다.

### <a name="similarities"></a>유사성

* `let!`를 `use!`, 및 `do!` 비슷합니다 `await` 내에서 비동기 작업을 호출 하는 경우는 `async{ }` 블록입니다.

  세 개의 키워드 내 에서만 사용할 수는 `async { }` 블록 방법과 유사 `await` 내 에서만 호출할 수는 `async` 메서드. 간단히 말해 `let!` 캡처하고 결과 사용 하려는 경우입니다 `use!` 는 동일 하지만 해당 리소스를 사용 하는 후 정리 해야 무엇 인가 및 `do!` 완료 반환 값이 없는 비동기 워크플로에 대기 하려는 경우에 앞으로 이동 합니다.

* F#비슷한 방식으로 데이터 병렬 처리를 지원합니다.

  매우 다른 방식으로 작동 하지만 `Async.Parallel` 에 해당 `Task.WhenAll` 모두 완료 하는 경우 비동기 작업 집합의 결과 하고자 하는 시나리오에 대 한 합니다.

### <a name="differences"></a>차이점

* 중첩 된 `let!` 허용 되지를 달리 중첩 `await`

  와 달리 `await`는 무기한으로 중첩 될 수 있습니다 `let!` 없으며 다른 내부에서 사용 하기 전에 해당 결과 있어야 합니다. `let!`, `do!`, 또는 `use!`합니다.

* 취소 지원에는 F# 보다 C#/VB.

  작업 중간에 실행 취소를 지 원하는 C#/VB 검사 해야 합니다 `IsCancellationRequested` 속성 또는 호출 `ThrowIfCancellationRequested()` 에 `CancellationToken` 비동기 메서드로 전달 되는 개체.

반면, F# 비동기 워크플로 더 자연스럽 게 취소할 수 있습니다. 취소는 간단한 3 단계로 이루어진 프로세스입니다.

1. 새 `CancellationTokenSource`를 만듭니다.
2. 시작 함수에 전달 합니다.
3. 호출 `Cancel` 토큰에 있습니다.

예제:

```fsharp
open System.Threading

// Create a workflow which will loop forever.
let workflow =
    async {
        while true do
            printfn "Working..."
            do! Async.Sleep 1000
    }

let tokenSource = new CancellationTokenSource()

// Start the workflow in the background
Async.Start (workflow, tokenSource.Token)

// Executing the next line will stop the workflow
tokenSource.Cancel()
```

이제 끝났습니다.

## <a name="further-resources"></a>추가 리소스:

* [MSDN에 대 한 비동기 워크플로](https://msdn.microsoft.com/library/dd233250.aspx)
* [에 대 한 비동기 시퀀스F#](https://fsprojects.github.io/FSharp.Control.AsyncSeq/library/AsyncSeq.html)
* [F#HTTP 데이터 유틸리티](https://fsharp.github.io/FSharp.Data/library/Http.html)
