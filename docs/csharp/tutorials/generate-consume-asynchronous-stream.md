---
title: 비동기 스트림 생성 및 사용
description: 이 고급 자습서에서는 비동기 스트림을 생성 및 사용하여 비동기적으로 생성될 수 있는 데이터 시퀀스를 사용하는 더 자연스러운 방법을 제공하는 시나리오를 보여 줍니다.
ms.date: 02/10/2019
ms.custom: mvc
ms.openlocfilehash: 04c4fe1c7e33138273c5b49c6985efc60767a724
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216559"
---
# <a name="tutorial-generate-and-consume-async-streams-using-c-80-and-net-core-30"></a>자습서: C# 8.0 및 .NET Core 3.0을 사용하여 비동기 스트림 생성 및 사용

C# 8.0은 데이터 스트림의 요소를 비동기적으로 검색하거나 생성할 수 있는 경우 데이터의 스트리밍 소스를 모델링하는 **비동기 스트림**을 소개합니다. 비동기 스트림은 .NET Standard 2.1에서 도입되고 .NET Core 3.0에서 구현된 새 인터페이스를 사용하여 비동기 스트리밍 데이터 소스의 일반 프로그래밍 모델을 제공합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
>
> - 데이터 요소 시퀀스를 비동기적으로 생성하는 데이터 소스를 만듭니다.
> - 데이터 소스를 비동기적으로 사용합니다.
> - 새 인터페이스 및 데이터 소스가 이전 동기 데이터 시퀀스로 기본 설정되는 경우를 인식합니다.

## <a name="prerequisites"></a>전제 조건

C# 8.0 컴파일러를 포함하여 .NET Core를 실행하도록 머신을 설정해야 합니다. C# 8 컴파일러는 [Visual Studio 2019 버전 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 또는 [.NET CORE 3.0 SDK](https://dotnet.microsoft.com/download)부터 사용할 수 있습니다.

GitHub GraphQL 엔드포인트에 액세스할 수 있도록 [GitHub 액세스 토큰](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/#creating-a-token)을 만들어야 합니다. GitHub 액세스 토큰에 사용할 다음 권한을 선택합니다.

- repo:status
- public_repo

GitHub API 엔드포인트의 액세스 권한을 부여하는 데 사용할 수 있도록 액세스 토큰을 안전한 장소에 보관합니다.

> [!WARNING]
> 개인용 액세스 토큰을 안전하게 보관합니다. 개인용 액세스 토큰이 있는 소프트웨어는 액세스 권한을 사용하여 GitHub API 호출을 수행할 수 있습니다.

이 자습서에서는 Visual Studio 또는 .NET Core CLI를 포함하여 C# 및 .NET에 익숙하다고 가정합니다.

## <a name="run-the-starter-application"></a>시작 애플리케이션 실행

[csharp/tutorials/AsyncStreams](https://github.com/dotnet/samples/tree/master/csharp/tutorials/AsyncStreams/start) 폴더의 [dotnet/samples](https://github.com/dotnet/samples) 리포지토리에서 이 자습서에 사용된 시작 애플리케이션의 코드를 가져올 수 있습니다.

시작 애플리케이션은 [GitHub GraphQL](https://developer.github.com/v4/) 인터페이스를 사용하여 [dotnet/docs](https://github.com/dotnet/docs) 리포지토리에 기록된 최근 문제를 검색하는 콘솔 애플리케이션입니다. 먼저 시작 앱 `Main` 메서드의 다음 코드를 살펴봅니다.

[!code-csharp[StarterAppMain](~/samples/csharp/tutorials/AsyncStreams/start/IssuePRreport/IssuePRreport/Program.cs#StarterAppMain)]

`GitHubKey` 환경 변수를 개인용 액세스 토큰으로 설정하거나, `GenEnvVariable` 호출의 마지막 인수를 개인용 액세스 토큰으로 바꿀 수 있습니다. 소스를 다른 항목과 함께 저장하거나 공유 소스 리포지토리에 넣을 경우에는 액세스 코드를 소스 코드에 넣지 마세요.

GitHub 클라이언트를 만든 후 `Main`의 코드는 진행 보고 개체 및 취소 토큰을 만듭니다. 해당 개체가 만들어지면 `Main`이 `runPagedQueryAsync`를 호출하여 250개의 가장 최근 생성된 문제를 검색합니다. 작업이 완료되면 결과가 표시됩니다.

시작 애플리케이션을 실행할 때 이 애플리케이션의 실행 방식에 대한 몇 가지 중요한 사항을 관찰할 수 있습니다.  GitHub에서 반환된 각 페이지에 대해 보고된 진행 상황이 표시됩니다. GitHub가 각 새로운 문제 페이지를 반환하기 전에 분명한 일시 정지를 관찰할 수 있습니다. 마지막으로 이 문제는 10페이지가 GitHub에서 모두 검색된 후에만 표시됩니다.

## <a name="examine-the-implementation"></a>구현 살펴보기

구현은 이전 섹션에서 설명한 동작을 관찰한 이유를 드러냅니다. `runPagedQueryAsync`에 대한 코드를 검사합니다.

[!code-csharp[RunPagedQueryStarter](~/samples/csharp/tutorials/AsyncStreams/start/IssuePRreport/IssuePRreport/Program.cs#RunPagedQuery)]

앞 코드의 페이징 알고리즘 및 비동기 구조를 중점적으로 살펴보겠습니다. (GitHub GraphQL API에 대한 자세한 내용은 [GitHub GraphQL 설명서](https://developer.github.com/v4/guides/)를 참조하세요.) `runPagedQueryAsync` 메서드는 가장 최근에서 가장 오래된 순서로 문제를 열거합니다. 이 메서드는 페이지당 25개 문제를 요청하고 응답의 `pageInfo` 구조체를 검사하여 이전 페이지를 계속 진행합니다. 다중 페이지 응답에 대한 GraphQL의 표준 페이징 지원을 따릅니다. 응답에는 이전 페이지를 요청하는 데 사용되는 `hasPreviousPages` 값과 `startCursor` 값을 포함하는 `pageInfo` 개체가 포함됩니다. 문제는 `nodes` 배열에 있습니다. `runPagedQueryAsync` 메서드는 모든 페이지의 모든 결과를 포함하는 배열에 해당 노드를 추가합니다.

결과 페이지를 검색 및 복원한 후에 `runPagedQueryAsync`가 진행 상황을 보고하고 취소를 확인합니다. 취소가 요청된 경우 `runPagedQueryAsync`가 <xref:System.OperationCanceledException>을 throw합니다.

이 코드에서 여러 가지 요소를 개선할 수 있습니다. 가장 중요한 것은 `runPagedQueryAsync`가 반환된 모든 문제에 대해 스토리지를 할당해야 한다는 것입니다. 모든 미해결 문제를 검색하면 모든 검색된 문제를 저장하는 데 훨씬 더 많은 메모리가 필요하므로 이 샘플은 250개 문제만 검색합니다. 또한 진행 지원 및 취소 지원 프로토콜로 인해 알고리즘을 처음 읽을 때 이해하기가 더 어려워집니다. 진행이 보고되는 위치를 찾으려면 progress 클래스를 검색해야 합니다. 또한 취소 요청 위치 및 제공 위치를 파악하려면 <xref:System.Threading.CancellationTokenSource> 및 연결된 <xref:System.Threading.CancellationToken>을 통해 통신을 추적해야 합니다.

## <a name="async-streams-provide-a-better-way"></a>더 나은 방법을 제공하는 비동기 스트림

비동기 스트림 및 연결된 언어 지원으로 해당 문제가 모두 해결됩니다. 시퀀스를 생성하는 코드에서 이제 `yield return`을 사용하여 `async` 한정자로 선언된 메서드에서 요소를 반환할 수 있습니다. `foreach` 루프를 통해 시퀀스를 사용하는 것처럼 `await foreach` 루프를 통해 비동기 스트림을 사용할 수 있습니다.

이 새로운 언어 기능은 .NET Standard 2.1에 추가되고 .NET Core 3.0에 구현된 세 가지 새 인터페이스를 사용합니다.

```csharp
namespace System.Collections.Generic
{
    public interface IAsyncEnumerable<out T>
    {
        IAsyncEnumerator<T> GetAsyncEnumerator(CancellationToken cancellationToken = default);
    }

    public interface IAsyncEnumerator<out T> : IAsyncDisposable
    {
        T Current { get; }

        ValueTask<bool> MoveNextAsync();
    }
}

namespace System
{
    public interface IAsyncDisposable
    {
        ValueTask DisposeAsync();
    }
}
```

이 세 가지 인터페이스는 대부분의 C# 개발자에게 익숙합니다. 이 인터페이스는 동기 인터페이스와 유사한 방식으로 작동합니다.

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.IEnumerator%601?displayProperty=nameWithType>
- <xref:System.IDisposable?displayProperty=nameWithType>

익숙하지 않을 수도 있는 하나의 형식은 <xref:System.Threading.Tasks.ValueTask?displayProperty=nameWithType>입니다. `ValueTask` 구조체는 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 클래스에 유사한 API를 제공합니다. `ValueTask`는 성능상의 이유로 해당 인터페이스에서 사용됩니다.

## <a name="convert-to-async-streams"></a>비동기 스트림으로 변환

그런 다음, `runPagedQueryAsync` 메서드를 변환하여 비동기 스트림을 생성합니다. 먼저 `runPagedQueryAsync`의 시그니처를 변경하여 `IAsyncEnumerable<JToken>`을 반환하고 다음 코드에 표시된 대로 매개 변수 목록에서 취소 토큰 및 진행 개체를 제거합니다.

[!code-csharp[FinishedSignature](~/samples/csharp/tutorials/AsyncStreams/finished/IssuePRreport/IssuePRreport/Program.cs#UpdateSignature)]

시작 코드는 다음 코드에 표시된 대로 페이지가 검색될 때 각 페이지를 처리합니다.

[!code-csharp[StarterPaging](~/samples/csharp/tutorials/AsyncStreams/start/IssuePRreport/IssuePRreport/Program.cs#ProcessPage)]

해당 세 줄을 다음 코드로 바꿉니다.

[!code-csharp[FinishedPaging](~/samples/csharp/tutorials/AsyncStreams/finished/IssuePRreport/IssuePRreport/Program.cs#YieldReturnPage)]

이 메서드의 앞부분에 있는 `finalResults` 선언 및 수정한 루프 뒤에 있는 `return` 문을 제거할 수도 있습니다.

비동기 스트림을 생성하기 위한 변경을 완료했습니다. 완료된 메서드는 아래 코드와 같이 표시되어야 합니다.

[!code-csharp[FinishedGenerate](~/samples/csharp/tutorials/AsyncStreams/finished/IssuePRreport/IssuePRreport/Program.cs#GenerateAsyncStream)]

그런 다음, 컬렉션을 사용하는 코드를 변경하여 비동기 스트림을 사용합니다. 문제 컬렉션을 처리하는 `Main`에서 다음 코드를 찾습니다.

[!code-csharp[EnumerateOldStyle](~/samples/csharp/tutorials/AsyncStreams/start/IssuePRreport/IssuePRreport/Program.cs#EnumerateOldStyle)]

해당 코드를 다음 `await foreach` 루프로 바꿉니다.

[!code-csharp[FinishedEnumerateAsyncStream](~/samples/csharp/tutorials/AsyncStreams/finished/IssuePRreport/IssuePRreport/Program.cs#EnumerateAsyncStream)]

[csharp/tutorials/AsyncStreams](https://github.com/dotnet/samples/tree/master/csharp/tutorials/AsyncStreams/finished) 폴더의 [dotnet/samples](https://github.com/dotnet/samples) 리포지토리에서 완료된 자습서의 코드를 가져올 수 있습니다.

## <a name="run-the-finished-application"></a>완료된 애플리케이션 실행

애플리케이션을 다시 실행합니다. 해당 동작을 시작 애플리케이션의 동작과 대조합니다. 결과의 첫 번째 페이지는 사용 가능한 즉시 열거됩니다. 새로운 각 페이지가 요청 및 검색될 때 확인 가능한 일시 정지가 있고 난 뒤 다음 페이지의 결과가 빠르게 열거됩니다. 취소를 처리하는 데는 `try` / `catch` 블록이 필요하지 않습니다. 호출자가 컬렉션의 열거를 중지할 수 있습니다. 각 페이지가 다운로드될 때 비동기 스트림이 결과를 생성하므로 진행이 명확하게 보고됩니다.

코드를 검사하여 향상된 메모리 사용을 확인할 수 있습니다. 열거되기 전에 모든 결과를 저장하기 위해 더 이상 컬렉션을 할당할 필요가 없습니다. 호출자는 결과를 사용하는 방법 및 스토리지 컬렉션이 필요한지 여부를 결정할 수 있습니다.

시작 및 완료된 애플리케이션을 둘 다 실행하고 직접 구현 간 차이를 관찰할 수 있습니다. 완료한 후 이 자습서를 시작할 때 만든 GitHub 액세스 토큰을 삭제할 수 있습니다. 공격자가 해당 토큰의 액세스 권한을 얻으면 사용자의 자격 증명을 사용하여 GitHub API에 액세스할 수 있습니다.
