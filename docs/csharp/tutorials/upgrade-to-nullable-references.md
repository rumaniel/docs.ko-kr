---
title: nullable 참조 형식을 사용하여 디자인
description: 이 고급 자습서에서는 nullable 참조 형식을 소개합니다. 참조 값이 null일 수 있는 경우에 대한 디자인 의도를 표현하고 컴파일러가 null일 수 없는 경우를 적용하게 하는 방법을 알아봅니다.
ms.date: 02/19/2019
ms.custom: mvc
ms.openlocfilehash: 842b1bb6e0d3032c6181cccf77934541754ff8ec
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332327"
---
# <a name="tutorial-migrate-existing-code-with-nullable-reference-types"></a>자습서: nullable 참조 형식이 있는 기존 코드 마이그레이션

C# 8에서는 nullable 값 형식이 값 형식을 보완하는 것과 동일한 방식으로 참조 형식을 보완하는 **nullable 참조 형식**이 도입되었습니다. 형식에 `?`를 추가하여 변수를 **nullable 참조 형식**으로 선언합니다. 예를 들어 `string?`는 nullable `string`을 나타냅니다. 이러한 새 형식을 사용하여 디자인 의도를 보다 명확하게 표현할 수 있습니다. ‘항상 값이 있어야 하는’ 변수도 있고, ‘값이 누락될 수 있는’ 변수도 있습니다.   참조 형식을 갖는 기존 변수는 모두 nullable이 아닌 참조 형식으로 해석됩니다. 

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
>
> - 코드를 작업할 때 null 참조 검사를 활성화합니다.
> - null 값과 각종 경고를 진단하고 수정합니다.
> - nullable이 활성화된 컨텍스트와 nullable이 비활성화된 컨텍스트 간의 인터페이스를 관리합니다.
> - nullable 주석 컨텍스트를 제어합니다.

## <a name="prerequisites"></a>전제 조건

C# 8.0 컴파일러를 포함하여 .NET Core를 실행하도록 머신을 설정해야 합니다. C# 8 컴파일러는 [Visual Studio 2019 버전 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 또는 [.NET CORE 3.0 SDK](https://dotnet.microsoft.com/download)부터 사용할 수 있습니다.

이 자습서에서는 Visual Studio 또는 .NET Core CLI를 포함하여 C# 및 .NET에 익숙하다고 가정합니다.

## <a name="explore-the-sample-application"></a>샘플 애플리케이션 살펴보기

여기서 마이그레이션할 샘플 애플리케이션은 RSS 피드 리더기 웹앱입니다. 이 애플리케이션은 하나의 RSS 피드를 읽고 가장 최근 기사의 요약을 표시합니다. 표시되는 기사를 클릭하여 사이트를 방문할 수 있습니다. 이 애플리케이션은 비교적 최근에 작성되었지만, nullable 참조 형식을 사용할 수 있기 전에 작성되었습니다. 이 애플리케이션에는 바람직한 설계 원칙이 적용되었지만, 이 중요한 언어 기능을 남용하지는 마시기 바랍니다.

샘플 애플리케이션에는 앱의 주요 기능의 유효성을 검사하는 단위 테스트 라이브러리가 포함되어 있습니다. 생성되는 경고에 따라 구현을 조금이라도 변경하는 경우, 이 프로젝트를 사용하여 안전하게 업그레이드할 수 있습니다. 시작 코드는 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/nullable-reference-migration/start) GitHub 리포지토리에서 다운로드할 수 있습니다.

프로젝트를 마이그레이션할 때 목표는 변수의 nullable 여부를 어떻게 설정할지 명확히 표현할 수 있도록 새로운 언어 기능을 활용하고, nullable 주석 컨텍스트와 nullable 경고 컨텍스트를 `enabled`로 설정할 때 컴파일러에서 경고가 생성되지 않도록 하는 것이 되어야 합니다.

## <a name="upgrade-the-projects-to-c-8"></a>프로젝트를 C# 8로 업그레이드

첫 번째 단계로 마이그레이션 작업의 범위를 확인하는 것이 좋습니다. 시작하려면 먼저 프로젝트를 C# 8.0(이상)으로 업그레이드합니다. 웹 프로젝트의 csproj 파일과 단위 테스트 프로젝트의 csproj 파일에 각각 `LangVersion` 요소를 추가합니다.

```xml
<LangVersion>8.0</LangVersion>
```

언어 버전을 업그레이드하면 C# 8.0이 선택되지만, nullable 주석 컨텍스트와 nullable 경고 컨텍스트가 활성화되지는 않습니다. 프로젝트를 다시 빌드하여 경고 없이 빌드되는지 확인합니다.

다음 단계로 nullable 주석 컨텍스트를 켜고 경고가 몇 개나 생성되는지 살펴보는 것이 좋습니다. 솔루션의 두 csproj 파일에서 `LangVersion` 요소 아래에 각각 다음 요소를 추가합니다.

```xml
<Nullable>enable</Nullable>
```

테스트 빌드를 수행하고 경고 목록을 살펴봅니다. 이 작은 애플리케이션에서 컴파일러가 경고를 5개 생성하는 것을 볼 수 있습니다. 여기서는 nullable 주석 컨텍스트를 활성화 상태로 두고 프로젝트 전체의 경고를 수정할 수 있습니다.

이 방법은 규모가 작은 프로젝트에서만 사용할 수 있습니다. 규모가 큰 프로젝트에서는 전체 코드베이스에서 nullable 주석 컨텍스트를 활성화하여 생성되는 경고의 개수가 많기 때문에 경고를 체계적으로 수정하기가 어렵습니다. 규모가 큰 엔터프라이즈 프로젝트에서는 한 번에 프로젝트 하나씩 마이그레이션하는 것이 좋습니다. 각 프로젝트에서 한 번에 하나의 클래스 또는 파일을 마이그레이션합니다.

## <a name="warnings-help-discover-original-design-intent"></a>원래의 설계 의도를 파악하는 데 도움이 되는 경고

2개의 클래스에서 여러 개의 경고가 생성되었습니다. `NewsStoryViewModel` 클래스부터 시작합니다. 경고의 범위를 현재 작업 중인 코드 섹션으로 한정할 수 있도록 두 csproj 파일에서 각각 `Nullable` 요소를 제거합니다. *NewsStoryViewModel.cs* 파일을 열고 다음 지시문을 추가하여 `NewsStoryViewModel`에서 nullable 주석 컨텍스트를 활성화하고 클래스 정의 후에 이를 복원합니다.

```csharp
#nullable enable
public class NewsStoryViewModel
{
    public DateTimeOffset Published { get; set; }
    public string Title { get; set; }
    public string Uri { get; set; }
}
#nullable restore
```

위의 2개의 지시문은 마이그레이션 노력을 집중하는 데 도움이 됩니다. 현재 작업 중인 코드 영역에 해당하는 nullable 경고가 생성되었습니다. 프로젝트 전체에서 경고를 켤 준비가 될 때까지 일단 그대로 둡니다. 나중에 프로젝트 전체에서 nullable 주석을 켰을 때 컨텍스트가 실수로 비활성화되지 않도록 `disable` 값 대신 `restore` 값을 사용해야 합니다. 프로젝트 전체에서 nullable 주석 컨텍스트를 켠 후에 해당 프로젝트에서 모든 `#nullable` pragma를 제거할 수 있습니다.

`NewsStoryViewModel` 클래스는 DTO(데이터 전송 개체)로, 2개의 속성이 읽기/쓰기 문자열입니다.

[!code-csharp[InitialViewModel](~/samples/csharp/tutorials/nullable-reference-migration/start/SimpleFeedReader/ViewModels/NewsStoryViewModel.cs#StarterViewModel)]

이 2개의 속성 때문에 `CS8618`, “Non-nullable property is uninitialized”(nullable이 아닌 속성이 초기화되지 않았습니다.)가 발생합니다. 2개의 `string` 속성 모두 `NewsStoryViewModel`이 생성될 때 기본값이 `null`이므로 원인을 쉽게 파악할 수 있습니다. 이때 중요한 것은 `NewsStoryViewModel` 개체가 어떻게 생성되는지 알아내는 것입니다. 클래스를 살펴봐도 `null` 값이 설계의 일부인지 아니면 이러한 개체가 생성될 때마다 해당 개체가 null이 아닌 값으로 설정되는 것인지 파악하기가 어렵습니다. 뉴스 기사는 `NewsService` 클래스의 `GetNews` 메서드에서 생성됩니다.

[!code-csharp[StarterCreateNewsItem](~/samples/csharp/tutorials/nullable-reference-migration/start/SimpleFeedReader/Services/NewsService.cs#CreateNewsItem)]

위 코드 블록에서는 몇 가지 작업이 진행되고 있습니다. 이 애플리케이션은 [AutoMapper](https://automapper.org/) NuGet 패키지를 사용하여 `ISyndicationItem`으로부터 뉴스 항목을 생성합니다. 이 하나의 문에서 뉴스 기사 항목이 생성되고 속성이 설정된다는 사실을 파악했습니다. 따라서 `NewsStoryViewModel`의 설계 의도는 이러한 속성이 `null` 값을 갖지 않도록 하는 것임을 알 수 있습니다. 이러한 속성은 **nullable이 아닌 참조 형식**이 되어야 합니다. 이렇게 해야 원래 설계 의도가 가장 잘 표현됩니다. 실제로 모든 `NewsStoryViewModel`이 null이 아닌 값으로 올바르게 인스턴스화되었습니다.  그렇다면 다음과 같은 초기화 코드가 유효한 수정이 될 수 있습니다.

```csharp
public class NewsStoryViewModel
{
    public DateTimeOffset Published { get; set; }
    public string Title { get; set; } = default!;
    public string Uri { get; set; } = default!;
}
```

`Title`과 `Uri`에 `default`(`string` 형식의 경우 `null`)를 할당해도 프로그램의 런타임 동작이 변경되지 않습니다. `NewsStoryViewModel`은 전과 동일하게 null 값으로 생성되지만, 이제 컴파일러가 경고를 보고하지 않습니다. `default` 식 뒤에 **null 허용 연산자**인 `!` 문자가 오기 때문에 컴파일러는 선행 식이 null이 아님을 알 수 있습니다. 이 방법은 다른 변경 사항을 수행하는 경우 코드 베이스에 훨씬 더 많은 변경이 적용될 때는 유용하게 사용할 수 있지만, 이 애플리케이션에서는 보다 빠르고 효과적인 솔루션이 있습니다. 바로 `NewsStoryViewModel`을 모든 속성이 생성자에서 설정되는, 변경이 불가능한 형식으로 만드는 것입니다. `NewsStoryViewModel`에 다음 변경 내용을 적용합니다.

[!code-csharp[FinishedViewModel](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/ViewModels/NewsStoryViewModel.cs#FinishedViewModel)]

그런 다음, AutoMapper를 구성하는 코드가 속성을 설정하는 대신 생성자를 사용하도록 수정해야 합니다. `NewsService.cs`를 열고 파일 하단에서 다음 코드를 찾습니다.

[!code-csharp[StarterAutoMapper](~/samples/csharp/tutorials/nullable-reference-migration/start/SimpleFeedReader/Services/NewsService.cs#ConfigureAutoMapper)]

이 코드는 `ISyndicationItem` 개체의 속성을 `NewsStoryViewModel` 속성에 매핑합니다. AutoMapper가 대신 생성자를 사용하여 매핑을 수행하도록 수정해야 합니다. 위 코드를 다음 automapper 구성으로 바꿉니다.

[!code-csharp[FinishedViewModel](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Services/NewsService.cs#ConfigureAutoMapper)]

이 클래스는 규모가 작고 신중히 검사했기 때문에 이 클래스 선언 위에서 `#nullable enable` 지시문을 켜야 합니다. 생성자를 변경한 결과 무언가 잘못되었을 수 있으므로 계속 진행하기 전에 먼저 모든 테스트를 실행하여 애플리케이션을 테스트하는 것이 좋습니다.

지금까지의 작업을 통해 원래 설계 의도가 변수를 `null`로 설정하지 않는 것인지 확인하는 방법을 알아보았습니다. 이 방법을 **correct by construction**(생성에 의한 올바름)이라고 부릅니다. 개체와 개체의 속성을 생성할 때 이것이 `null`이 될 수 없다고 선언하는 것입니다. 컴파일러는 해당 속성이 생성 후에 `null`로 설정되지 않도록 흐름 분석을 수행합니다. 이 생성자는 외부 코드에 의해 호출되는 것을 볼 수 있는데, 이 코드는 **nullable 감지 불가**입니다. 새로운 구문에서는 런타임 검사를 제공하지 않습니다. 따라서 외부 코드가 컴파일러의 흐름 분석을 피해갈 수 있습니다. 

클래스의 구조가 설계 의도에 대한 또 다른 힌트를 주는 경우도 있습니다. *Pages* 폴더에서 *Error.cshtml.cs* 파일을 엽니다. `ErrorViewModel`에 다음 코드가 포함되어 있습니다.

[!code-csharp[StarterErrorModel](~/samples/csharp/tutorials/nullable-reference-migration/start/SimpleFeedReader/Pages/Error.cshtml.cs#StartErrorModel)]

클래스 선언 앞에 `#nullable enable` 지시문을 추가하고, 클래스 선언 뒤에 `#nullable restore` 지시문을 추가합니다. `RequestId`가 초기화되지 않았다는 경고가 표시됩니다. 클래스를 살펴보니 `RequestId` 속성은 경우에 따라 null이 되어야 한다는 사실을 알 수 있습니다. `ShowRequestId` 속성이 존재한다는 사실이 누락된 값이 있을 수 있음을 나타냅니다. `null`이 유효하므로 `string` 형식에 `?`을 추가하여 `RequestId` 속성이 ‘nullable 참조 형식’임을 나타냅니다.  다음은 완성된 클래스입니다.

[!code-csharp[FinishedErrorModel](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Pages/Error.cshtml.cs#ErrorModel)]

속성이 사용되는 방식을 살펴보면 표시에서 속성이 렌더링되기 전에 연결된 페이지에서 속성이 null인지 검사되는 것을 알 수 있습니다. 이처럼 nullable 참조 형식이 안전하게 사용되고 있으므로 이 클래스는 완성되었습니다.

## <a name="fixing-nulls-causes-change"></a>null을 수정하면 변경이 발생하는 경우

하나의 경고 세트를 수정하면 관련 코드에서 새로운 경고가 생성되는 경우가 있습니다. `index.cshtml.cs` 클래스를 수정하여 실제로 경고를 살펴보겠습니다. `index.cshtml.cs` 파일을 열고 코드를 살펴봅니다. 이 파일에는 인덱스 페이지를 구동하는 코드가 포함되어 있습니다.

[!code-csharp[StarterIndexModel](~/samples/csharp/tutorials/nullable-reference-migration/start/SimpleFeedReader/Pages/Index.cshtml.cs#IndexModelStart)]

`#nullable enable` 지시문을 추가하면 `ErrorText` 속성과 `NewsItems` 속성이 초기화되지 않았다는 2개의 경고를 볼 수 있습니다. 이 클래스를 살펴보면 두 속성 모두 nullable 참조 형식이 되어야 한다는 사실을 알 수 있습니다. 두 속성 모두 private setter를 갖고 있기 때문입니다. `OnGet` 메서드에서 정확히 1개가 할당되어 있습니다. 변경을 수행하기 전에 두 속성을 사용하는 주체를 찾아보겠습니다. 페이지에서 오류 표시가 생성되기 전에 `ErrorText`가 null에 대해 검사됩니다. `NewsItems` 컬렉션이 `null`에 대해 검사되고, 컬렉션에 항목이 있는지도 검사됩니다. 두 속성을 모두 nullable 참조 형식으로 만들어서 빠르게 수정할 수도 있지만, 이보다 나은 방법은 컬렉션을 nullable이 아닌 참조 형식으로 만들고, 뉴스를 가져올 때 기존 컬렉션에 항목을 추가하는 것입니다. 먼저 `ErrorText`의 `string` 형식에 `?`를 추가합니다.

[!code-csharp[UpdateErrorText](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Pages/Index.cshtml.cs#UpdateErrorText)]

이 `ErrorText` 속성에 대한 모든 액세스가 이미 null 검사에 의해 보호되었으므로 이 변경 사항은 다른 코드로 전파되지 않습니다. 다음으로 `NewsItems` 목록을 초기화하고 속성 setter를 제거하여 읽기 전용 속성으로 만듭니다.

[!code-csharp[InitializeNewsItems](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Pages/Index.cshtml.cs#InitializeNewsItems)]

이렇게 하면 경고는 해결되지만 오류가 발생합니다. `NewsItems` 목록은 이제 **correct by construction**(생성에 의한 올바름)이지만, `OnGet`에서 목록을 설정하는 코드가 새 API에 대응되도록 변경해야 합니다. 할당을 사용하는 대신 `AddRange`를 호출하여 기존 목록에 뉴스 항목을 추가합니다.

[!code-csharp[AddRange](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Pages/Index.cshtml.cs#AddRange)]

할당 대신 `AddRange`를 사용한다는 것은 `GetNews` 메서드가 `List` 대신 `IEnumerable`을 반환할 수 있음을 의미합니다. 이렇게 하면 할당이 하나 절약됩니다. 다음 코드 샘플과 같이 메서드의 시그니처를 변경하고 `ToList` 호출을 제거합니다.

[!code-csharp[GetNews](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Services/NewsService.cs#GetNewsFinished)]

시그니처를 변경하면 테스트 중 하나도 중단됩니다. `SimpleFeedReader.Tests` 프로젝트의 `Services` 폴더에서 `NewsServiceTests.cs` 파일을 엽니다. `Returns_News_Stories_Given_Valid_Uri` 테스트로 이동하고 `result` 변수의 형식을 `IEnumerable<NewsItem>`으로 변경합니다. 형식을 변경한다는 것은 `Count` 속성을 더 이상 사용할 수 없음을 의미하므로, `Assert`의 `Count` 속성을 `Any()` 호출로 변경합니다.

[!code-csharp[FixTests](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader.Tests/Services/NewsServiceTests.cs#FixTestSignature)]

파일의 시작 부분에 `using System.Linq` 문도 추가해야 합니다.

지금까지 제네릭 인스턴스화를 포함하는 코드를 업데이트할 때 특히 유의해야 하는 고려 사항을 살펴보았습니다. 목록과 목록의 요소는 모두 nullable이 아닌 형식입니다. 둘 중 하나 또는 둘 다 nullable 형식이 될 수 있습니다. 다음 지시문이 모두 허용됩니다.

- `List<NewsStoryViewModel>`: nullable이 아닌 보기 모델의 nullable이 아닌 목록
- `List<NewsStoryViewModel?>`: nullable 보기 모델의 nullable이 아닌 목록
- `List<NewsStoryViewModel>?`: nullable이 아닌 보기 모델의 nullable 목록
- `List<NewsStoryViewModel?>?`: nullable 보기 모델의 nullable 목록

## <a name="interfaces-with-external-code"></a>외부 코드와의 인터페이스

지금까지 `NewsService` 클래스를 변경했습니다. 이번에는 이 클래스에서 `#nullable enable` 주석을 켭니다. 이렇게 해도 새로운 경고가 생성되지 않습니다. 그렇지만 클래스를 주의 깊게 살펴보면 컴파일러의 흐름 분석에 어떤 제한이 있는지 알 수 있습니다. 생성자를 살펴봅니다.

[!code-csharp[ServiceConstructor](~/samples/csharp/tutorials/nullable-reference-migration/finished/SimpleFeedReader/Services/NewsService.cs#ServiceConstructor)]

`IMapper` 매개 변수는 nullable이 아닌 참조 형식입니다. ASP.NET Core 인프라 코드에 의해 호출되므로, 컴파일러는 `IMapper`가 null이 될 수 없다는 것을 알지 못합니다. 기본적인 ASP.NET Core DI(종속성 주입) 컨테이너는 필수 서비스를 확인할 수 없는 경우 예외를 throw하므로 이 코드는 올바릅니다. nullable 주석 컨텍스트를 활성화한 상태로 코드를 컴파일하더라도 컴파일러는 모든 공용 API 호출의 유효성을 검사할 수 없습니다. 또한, nullable 참조 형식을 사용하도록 설정되지 않은 프로젝트에 의해 라이브러리가 과도하게 사용될 수 있습니다. nullable이 아닌 형식으로 선언한 경우에도 공용 API의 입력은 유효성을 검사해야 합니다.

## <a name="get-the-code"></a>코드 가져오기

초기 테스트 컴파일에서 확인한 경고를 모두 수정했으므로 이제 두 프로젝트에서 모두 nullable 주석 컨텍스트를 켤 수 있습니다. 프로젝트를 다시 빌드하면 컴파일러에서 생성하는 경고가 없는 것을 볼 수 있습니다. 완성된 프로젝트의 코드는 [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/nullable-reference-migration/finished) GitHub 리포지토리에서 가져올 수 있습니다.

nullable 참조 형식을 지원하는 새로운 기능을 사용하면 코드에서 `null` 값을 처리하는 방식의 잠재적인 오류를 찾아서 수정할 수 있습니다. nullable 주석 컨텍스트를 활성화하면 어떤 변수는 null이 되면 안 되고, 어떤 변수는 null 값을 포함해도 된다는 설계 의도를 원하는 대로 표현할 수 있습니다. 이러한 기능을 사용하여 설계 의도를 보다 쉽게 드러낼 수 있습니다. 마찬가지로, nullable 경고 컨텍스트는 의도가 위반된 경우 경고를 발생하라고 컴파일러에 알립니다. 이러한 경고를 살펴보고 업데이트하여 코드의 복원력을 높이고 실행 중에 `NullReferenceException`을 throw할 확률을 줄일 수 있습니다. 이러한 컨텍스트의 범위를 제어하여 나머지 코드베이스는 그대로 두고 마이그레이션할 로컬 코드 영역에만 집중할 수 있습니다. 실전에서는 클래스의 정기적인 유지 관리의 일환으로 이러한 마이그레이션 작업을 수행할 수 있습니다. 이 자습서에서는 nullable 참조 형식을 사용하도록 애플리케이션을 마이그레이션하는 과정을 살펴봤습니다. [NodaTime](https://github.com/nodatime/nodatime/pull/1240/commits)에 nullable 참조 형식을 통합하도록 구현된 PR [Jon Skeet](https://github.com/jskeet)에서 더 많은 실제 사례를 참조할 수 있습니다.
