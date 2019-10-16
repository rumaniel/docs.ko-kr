---
title: nullable 참조 형식을 사용하여 디자인
description: 이 고급 자습서에서는 nullable 참조 형식을 소개합니다. 참조 값이 null일 수 있는 경우에 대한 디자인 의도를 표현하고 컴파일러가 null일 수 없는 경우를 적용하게 하는 방법을 알아봅니다.
ms.date: 02/19/2019
ms.custom: mvc
ms.openlocfilehash: e58f2bac23fabf734df93aa2a643106f1c1bd5f3
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291381"
---
# <a name="tutorial-express-your-design-intent-more-clearly-with-nullable-and-non-nullable-reference-types"></a>자습서: nullable 참조 형식 및 nullable이 아닌 참조 형식을 사용하여 디자인 의도를 보다 명확하게 표현

C# 8.0에서는 nullable 값 형식이 값 형식을 보완하는 것과 동일한 방식으로 참조 형식을 보완하는 [nullable 참조 형식](../nullable-references.md)이 도입되었습니다. 형식에 `?`를 추가하여 변수를 **nullable 참조 형식**으로 선언합니다. 예를 들어 `string?`는 nullable `string`을 나타냅니다. 이러한 새 형식을 사용하여 디자인 의도를 보다 명확하게 표현할 수 있습니다. ‘항상 값이 있어야 하는’ 변수도 있고, ‘값이 누락될 수 있는’ 변수도 있습니다.  

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
>
> - 디자인에 nullable 참조 형식 및 nullable이 아닌 참조 형식 통합
> - 코드 전체에서 nullable 참조 형식 확인을 사용하도록 설정합니다.
> - 컴파일러가 이러한 디자인 결정을 적용하는 코드를 작성합니다.
> - 고유한 디자인에 nullable 참조 기능 사용

## <a name="prerequisites"></a>전제 조건

C# 8.0 컴파일러를 포함하여 .NET Core를 실행하도록 컴퓨터를 설정해야 합니다. C# 8.0 컴파일러는 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 또는 [.NET Core 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0)에서 사용할 수 있습니다.

이 자습서에서는 Visual Studio 또는 .NET Core CLI를 포함하여 C# 및 .NET에 익숙하다고 가정합니다.

## <a name="incorporate-nullable-reference-types-into-your-designs"></a>디자인에 nullable 참조 형식 통합

이 자습서에서는 설문 조사 실행을 모델링하는 라이브러리를 빌드합니다. 코드는 nullable 참조 형식 및 nullable이 아닌 참조 형식을 둘 다 사용하여 실제 세계의 개념을 표현합니다. 설문 조사 질문은 null일 수 없습니다. 응답자는 질문에 응답하지 않을 수 있습니다. 이 경우 응답이 `null`일 수 있습니다.

이 샘플에 대해 작성하는 코드는 해당 의도를 표현하고 컴파일러가 의도를 적용합니다.

## <a name="create-the-application-and-enable-nullable-reference-types"></a>애플리케이션을 만들고 nullable 참조 형식을 사용하도록 설정

Visual Studio 또는 `dotnet new console`을 사용하여 명령줄에서 새로운 콘솔 애플리케이션을 만듭니다. 애플리케이션 이름을 `NullableIntroduction`으로 지정합니다. 애플리케이션을 만든 후에는 전체 프로젝트가 **활성화된 nullable 주석 컨텍스트**에서 컴파일하도록 지정해야 합니다. *.csproj* 파일을 열고 `Nullable` 요소에 `PropertyGroup` 요소를 추가합니다. 해당 값을 `enable`로 설정합니다. C# 8.0 프로젝트에서도 **nullable 참조 형식** 기능을 옵트인해야 합니다. 기능이 켜지고 나면 기존 참조 변수 선언이 **nullable이 아닌 참조 형식**으로 바뀌기 때문입니다. 이러한 의사 결정은 기존 코드에 적절한 null 확인이 없다는 문제를 찾는 데는 도움이 되지만, 원래 설계 의도를 정확하게 반영하지 않을 수 있습니다.

```xml
<Nullable>enable</Nullable>
```

### <a name="design-the-types-for-the-application"></a>애플리케이션의 형식 디자인

이 설문 조사 애플리케이션에서는 다음과 같은 많은 클래스를 만들어야 합니다.

- 질문 목록을 모델링하는 클래스
- 설문 조사를 위해 연락한 사람 목록을 모델링하는 클래스
- 설문 조사를 수행한 사람의 응답을 모델링하는 클래스

이러한 형식은 nullable 참조 형식 및 nullable이 아닌 참조 형식을 둘 다 사용하여 필수 멤버가 선택적 멤버를 표현합니다. nullable 참조 형식은 해당 디자인 의도를 명확하게 전달합니다.

- 설문 조사의 일부인 질문은 null일 수 없습니다. 빈 질문을 하는 것은 타당하지 않습니다.
- 응답자는 null일 수 없습니다. 참여를 거부한 응답자를 포함하여 연락한 사람을 추적하는 것이 좋습니다.
- 질문에 대한 응답은 null일 수 있습니다. 응답자는 일부 또는 모든 질문에 대한 응답을 거부할 수 있습니다.

C#으로 프로그래밍한 경우 `null` 값을 허용하는 참조 형식에 익숙해서 null 허용이 아닌 인스턴스를 선언할 다른 기회를 놓칠 수도 있습니다.

- 질문 컬렉션은 nullable이 아니어야 합니다.
- 응답자 컬렉션은 nullable이 아니어야 합니다.

코드를 작성할 때 null 허용이 아닌 참조 형식을 참조의 기본값으로 사용하면 <xref:System.NullReferenceException>을 발생시킬 수 있는 일반적인 실수를 방지할 수 있습니다. 이 자습서에서 배운 한 가지 교훈은 `null`일 수 있는 변수와 그렇지 않은 변수를 결정하는 것입니다. 이러한 결정을 표현하는 구문은 언어에서 제공하지 않았지만 이제 제공합니다.

빌드할 앱은 다음 단계를 수행합니다.

1. 설문 조사를 만들고 질문을 추가합니다.
1. 설문 조사 응답자의 의사 임의 세트를 만듭니다.
1. 완료된 설문 조사 크기가 목표 수치에 도달할 때까지 응답자에게 연락합니다.
1. 설문 조사 응답에 대한 중요한 통계를 작성합니다.

## <a name="build-the-survey-with-nullable-and-non-nullable-types"></a>nullable 형식과 nullable이 아닌 형식을 사용하여 설문 조사 작성

작성하는 첫 번째 코드에서 설문 조사를 만듭니다. 설문 조사 질문과 설문 조사 실행을 모델링하는 클래스를 작성합니다. 설문 조사에는 다음 응답 형식으로 구분되는 세 가지 질문 유형이 있습니다. 예/아니요 응답, 숫자 응답, 텍스트 응답. `public SurveyQuestion` 클래스를 만듭니다.

```csharp
namespace NullableIntroduction
{
    public class SurveyQuestion
    {
    }
}
```

컴파일러가 모든 참조 형식 변수 선언을 활성화된 nullable 주석 컨텍스트에 있는 코드의 **nullable이 아닌** 참조 형식으로 해석합니다. 다음 코드에 표시된 대로 질문 텍스트 및 질문 유형의 속성을 추가하여 첫 번째 경고를 표시할 수 있습니다.

```csharp
namespace NullableIntroduction
{
    public enum QuestionType
    {
        YesNo,
        Number,
        Text
    }

    public class SurveyQuestion
    {
        public string QuestionText { get; }
        public QuestionType TypeOfQuestion { get; }
    }
}
```

`QuestionText`를 초기화하지 않았기 때문에 컴파일러에서 nullable이 아닌 속성이 초기화되지 않았다는 경고를 실행합니다. 디자인에 따라 질문 텍스트는 null이 아니어야 하므로 초기화할 생성자와 `QuestionType` 값도 추가합니다. 완성된 클래스 정의는 다음 코드와 같습니다.

[!code-csharp[DefineQuestion](~/samples/csharp/NullableIntroduction/NullableIntroduction/SurveyQuestion.cs)]

생성자를 추가하면 경고가 제거됩니다. 생성자 인수도 nullable이 아닌 참조 형식이므로 컴파일러에서 경고를 실행하지 않습니다.

`SurveyRun`이라는 `public` 클래스를 만듭니다. 이 클래스에는 다음 코드에 표시된 것처럼 설문 조사에 질문을 추가하는 메서드 및 `SurveyQuestion` 개체 목록이 포함되어 있습니다.

```csharp
using System.Collections.Generic;

namespace NullableIntroduction
{
    public class SurveyRun
    {
        private List<SurveyQuestion> surveyQuestions = new List<SurveyQuestion>();

        public void AddQuestion(QuestionType type, string question) =>
            AddQuestion(new SurveyQuestion(type, question));
        public void AddQuestion(SurveyQuestion surveyQuestion) => surveyQuestions.Add(surveyQuestion);
    }
}
```

이전과 마찬가지로, 목록 개체를 null이 아닌 값으로 초기화해야 합니다. 초기화하지 않으면 컴파일러에서 경고를 실행합니다. `AddQuestion`의 두 번째 오버로드에는 null 확인이 없습니다. 왜냐하면 해당 변수를 nullable이 아닌 것으로 선언했기 때문입니다. 해당 값은 `null`일 수 있습니다.

편집기에서 *Program.cs*로 전환하고 `Main`의 내용을 다음 코드 줄로 바꿉니다.

[!code-csharp[AddQuestions](~/samples/csharp/NullableIntroduction/NullableIntroduction/Program.cs#AddQuestions)]

프로젝트 전체가 활성화된 nullable 주석 컨텍스트이므로 nullable이 아닌 참조 형식을 기대하고 메서드로 `null`을 전달하면 경고가 발생합니다. 다음 줄을 `Main`에 추가하여 시도해 보세요.

```csharp
surveyRun.AddQuestion(QuestionType.Text, default);
```

## <a name="create-respondents-and-get-answers-to-the-survey"></a>응답자를 만들고 설문 조사에 대한 응답 받기

다음으로, 설문 조사에 대한 응답을 생성하는 코드를 작성합니다. 이 프로세스에는 몇 개의 작은 작업이 포함됩니다.

1. 응답자 개체를 생성하는 메서드를 빌드합니다. 이러한 개체는 설문 조사를 작성하도록 요청된 사람을 나타냅니다.
1. 응답자에게 질문하고 응답을 수집하거나 응답자가 응답하지 않았음을 확인하는 과정을 시뮬레이션하는 논리를 빌드합니다.
1. 충분한 응답자가 설문 조사에 응답할 때까지 반복합니다.

설문 조사 응답을 나타낼 클래스가 필요하므로 지금 추가합니다. nullable 지원을 사용하도록 설정합니다. 다음 코드에 표시된 대로 `Id` 속성 및 이 속성을 초기화하는 생성자를 추가합니다.

```csharp
namespace NullableIntroduction
{
    public class SurveyResponse
    {
        public int Id { get; }

        public SurveyResponse(int id) => Id = id;
    }
}
```

다음으로, `static` 메서드를 추가해서 임의 ID를 생성하여 새 참가자를 만듭니다.

[!code-csharp[GenerateRespondents](~/samples/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#Random)]

이 클래스의 주요 책임은 설문 조사의 질문에 대한 참가자의 응답을 생성하는 것입니다. 이 책임에는 몇 가지 단계가 있습니다.

1. 설문 조사에 참여하도록 요청합니다. 개인이 동의하지 않을 경우 missing(또는 null) 응답을 반환합니다.
1. 각 질문을 하고 응답을 기록합니다. 각 응답도 missing(또는 null)일 수 있습니다.

`SurveyResponse` 클래스에 다음 코드를 추가합니다.

[!code-csharp[AnswerSurvey](~/samples/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#AnswerSurvey)]

설문 조사 응답의 스토리지는 `Dictionary<int, string>?`로, null일 수 있음을 나타냅니다. 새 언어 기능을 사용하여 컴파일러 및 나중에 코드를 읽는 모든 사람에게 디자인 의도를 선언하고 있습니다. 먼저 `null` 값을 확인하지 않고 `surveyResponses`를 역참조하는 경우 컴파일러 경고가 표시됩니다. 위에서 `surveyResponses` 변수가 null이 아닌 값으로 설정되었음을 컴파일러가 판별할 수 있으므로 `AnswerSurvey` 메서드에 경고가 표시되지 않습니다.

누락된 응답을 확인하기 위해 `null`을 사용하는 것에서 nullable 참조 형식을 사용할 때 유의해야 할 중요한 점을 확인할 수 있습니다. 즉, 프로그램에서 `null` 값을 모두 제거하는 것이 목표가 되어서는 안 됩니다. 내가 작성하는 코드가 내 설계 의도를 그대로 표현하고 있는지 확인하는 것이 목표가 되어야 합니다. 누락된 값은 코드에서 반드시 표현해야 하는 개념입니다. `null` 값은 누락된 값을 분명하게 표현할 수 있는 방법입니다. `null` 값을 모두 제거하는 것을 목표로 하면 `null`을 사용하지 않고 누락된 값을 표현할 다른 방법을 정의해야 할 뿐입니다.

다음으로, `SurveyRun` 클래스에 `PerformSurvey` 메서드를 작성해야 합니다. `SurveyRun` 클래스에 다음 코드를 추가합니다.

[!code-csharp[PerformSurvey](~/samples/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#PerformSurvey)]

여기서 다시, nullable `List<SurveyResponse>?` 선택은 응답이 null일 수 있음을 나타냅니다. 이는 설문 조사가 아직 어떠한 응답자에게도 제공되지 않았음을 나타냅니다. 충분한 응답자가 동의할 때까지 응답자가 추가됩니다.

설문 조사를 실행하는 마지막 단계는 `Main` 메서드의 끝에 설문 조사를 수행할 호출을 추가하는 것입니다.

[!code-csharp[RunSurvey](~/samples/csharp/NullableIntroduction/NullableIntroduction/Program.cs#RunSurvey)]

## <a name="examine-survey-responses"></a>설문 조사 응답 조사

마지막 단계는 설문 조사 결과를 표시하는 것입니다. 작성한 여러 클래스에 코드를 추가합니다. 이 코드는 nullable 참조 형식과 nullable이 아닌 참조 형식 구분의 가치를 보여 줍니다. 먼저 다음 두 개의 식 본문 멤버를 `SurveyResponse` 클래스에 추가합니다.

[!code-csharp[ReportResponses](~/samples/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#SurveyStatus)]

`surveyResponses`는 null이 가능한 참조 형식이므로 역참조하기 전에 null 확인이 필요합니다. `Answer` 메서드는 null 허용이 아닌 문자열을 반환하므로 null 병합 연산자를 사용하여 누락된 답변의 사례를 포함해야 합니다.

다음 세 개의 식 본문 멤버를 `SurveyRun` 클래스에 추가합니다.

[!code-csharp[ReportResults](~/samples/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#RunReport)]

`respondents` 변수는 null일 수 있지만 반환 값은 null일 수 없음을 `AllParticipants` 멤버가 고려해야 합니다. `??` 및 뒤에 오는 빈 시퀀스를 제거하여 해당 식을 변경하면 컴파일러에서 메서드가 `null`을 반환할 수 있고 해당 반환 시그니처가 nullable이 아닌 형식을 반환한다고 경고합니다.

마지막으로, `Main` 메서드의 맨 아래에 다음 루프를 추가합니다.

[!code-csharp[DisplaySurveyResults](~/samples/csharp/NullableIntroduction/NullableIntroduction/Program.cs#WriteAnswers)]

모두 nullable이 아닌 참조 형식을 반환하도록 기본 인터페이스를 디자인했기 때문에 이 코드에는 `null` 확인이 필요하지 않습니다.

## <a name="get-the-code"></a>코드 가져오기

[csharp/NullableIntroduction](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction) 폴더의 [samples](https://github.com/dotnet/samples) 리포지토리에서 완료된 자습서의 코드를 가져올 수 있습니다.

nullable 참조 형식과 nullable이 아닌 참조 형식 간에 형식 선언을 변경하여 실험합니다. 실수로 `null`을 역참조하지 않도록 어떻게 다양한 경고를 생성하는지 확인합니다.

## <a name="next-steps"></a>다음 단계

nullable 참조 형식을 사용할 수 있도록 기존 애플리케이션을 마이그레이션하여 자세히 알아보세요.
> [!div class="nextstepaction"]
> [Upgrade an application to use nullable reference types](upgrade-to-nullable-references.md)(nullable 참조 형식을 사용할 수 있도록 애플리케이션 업그레이드)
