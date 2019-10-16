---
ms.openlocfilehash: 23501575fb34f0291b3a6b795c197f45a86fd512
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955964"
---
# <a name="contributing"></a>참여

.NET 문서에 기여하는 데 관심을 가져주셔서 감사합니다!

> 가이드라인을 사이트 전반의 기여 가이드로 이동하는 과정에 있습니다.
> 새로운 지침을 보려면 [Microsoft Docs 기여자 가이드 개요](https://docs.microsoft.com/contribute/)를 참조하세요.

이 문서에서는 [.NET 문서 사이트](https://docs.microsoft.com/dotnet)에 호스트된 문서 및 코드 샘플에 기여하는 프로세스를 설명합니다. 기여는 오타 수정만큼 간단하거나 새 문서처럼 복잡할 수 있습니다.

- [기여하는 프로세스](#process-for-contributing)
- [C# 대화형 환경](#the-c-interactive-experience)
- [권고 및 금지](#dos-and-donts)
- [기여자 라이선스 계약](#contributor-license-agreement)

이 리포지토리는 .NET에 대한 개념 설명서를 포함합니다. .NET 문서 사이트는 이 리포지토리 외에도 여러 리포지토리에서 빌드되었습니다.

- [코드 샘플 및 조각](https://github.com/dotnet/samples)  
    이 리포지토리의 문제 및 작업은 [dotnet/docs/issues](https://github.com/dotnet/docs/issues)에서 추적됩니다.
- [.NET API 참조](https://github.com/dotnet/dotnet-api-docs)  
    이 리포지토리의 문제 및 작업은 [dotnet/dotnet-api-docs/issues](https://github.com/dotnet/dotnet-api-docs/issues)에서 추적됩니다.
- [.NET Compiler Platform SDK 참조](https://github.com/dotnet/roslyn-api-docs)  
    이 리포지토리의 문제 및 작업은 [dotnet/docs/issues](https://github.com/dotnet/docs/issues)에서 추적됩니다.

## <a name="process-for-contributing"></a>기여하는 프로세스

[Git 및 GitHub.com](https://guides.github.com/activities/hello-world/)의 기본적인 내용을 이해하고 있어야 합니다.

**1단계:** 소규모 변경(예: 오타를 수정하거나 문서에서 찾은 문제를 해결하기 위해 즉시 끌어오기 요청을 여는 경우)인 경우 이 단계를 건너뜁니다. 새로운 콘텐츠를 작성하거나 기존 콘텐츠를 완전히 수정하려는 경우 원하는 작업을 설명하는 [문제](https://github.com/dotnet/docs/issues)를 엽니다.
*docs* 폴더 내의 콘텐츠는 TOC(목차)에 반영된 섹션으로 구성되어 있습니다. 목차에서 항목을 배치할 위치를 정의합니다. 제안에 대한 피드백을 가져옵니다.

또는

커뮤니티 기여가 요청된 기존 문제 중에서 선택할 수도 있습니다. [.NET 커뮤니티 기여자용 프로젝트](https://github.com/dotnet/docs/projects/35)에는 커뮤니티 기여자가 사용할 수 있는 많은 작업 항목이 나와 있습니다. 관심 및 약정 수준에 따라 다음 범주의 문제에서 선택할 수 있습니다.

- **유지 관리**. 이 범주에는 끊어졌거나 잘못된 링크 수정, 누락된 코드 예제 추가, 제한된 콘텐츠 문제 해결 등 비교적 간단한 기여가 포함됩니다. 이러한 문제가 다수의 파일과 관련된 경우도 있습니다. 이 경우 시작하기 전에 작업할 내용을 Microsoft에 알려야 합니다.

- **콘텐츠 업데이트**. 방대한 문서 집합에서 콘텐츠는 쉽게 구식 버전이 되며 수정이 필요합니다. 또한 다양한 이유로 일부 콘텐츠가 중복 또는 삼중 복제되었습니다. 콘텐츠를 업데이트하려면 개별 항목의 기능 영역에 최신 또는 수정 콘텐츠가 있는지 확인하여 중복을 제거하고 모든 고유 콘텐츠가 더 작은 문서 집합에 보존되도록 해야 합니다.

- **새 콘텐츠 작성**. 고유한 항목 작성에 관심이 있는 경우 이러한 문제는 문서 집합에 추가하고 싶은 항목을 나열합니다. 하지만 항목에 대한 작업을 시작하기 전에 Microsoft에 알려주세요. 여기에 나열되지 않은 항목 작성에 관심이 있는 경우 문제를 엽니다.

[열린 문제](https://github.com/dotnet/docs/issues) 목록을 살펴보고 관심 있는 문제에 대한 작업을 자원할 수도 있습니다. [up-for-grabs](https://github.com/dotnet/docs/labels/up-for-grabs) 레이블을 사용하여 기여와 관련해서 열린 문제에 태그를 지정합니다. 

**2단계:** 필요에 따라 `dotnet/docs`, `dotnet/samples` 또는 `dotnet/dotnet-api-docs` 리포지토리를 포크하고 변경 내용에 대한 분기를 만듭니다.

사소한 변경의 경우 GitHub 웹 인터페이스를 사용할 수 있습니다. 변경하려는 파일에서 **이 프로젝트의 포크에 있는 파일 편집**을 클릭하기만 하면 됩니다. 변경 내용을 제출하면 GitHub에서 자동으로 새 분기를 만듭니다.

**3단계:** 이 새로운 분기를 변경합니다.

새 항목인 경우 이 [템플릿 파일](./styleguide/template.md)을 시작점으로 사용할 수 있습니다. 작성 지침을 포함하고 작성자 정보 등의 각 문서에 필요한 메타데이터도 설명합니다.

1단계의 문서에 대해 결정된 TOC 위치에 해당하는 폴더로 이동합니다.
해당 폴더에는 해당 섹션에 있는 모든 문서의 Markdown 파일이 포함됩니다.
필요한 경우에 콘텐츠에 대한 파일을 배치할 새 폴더를 만듭니다. 해당 섹션의 기본 문서를 *index.md*라고 합니다.
이미지 및 기타 정적 리소스를 위해 문서가 포함된 폴더 안에 *media*라는 하위 폴더를 만듭니다(아직 없는 경우). *media* 폴더 안에 문서 이름의 하위 폴더를 만듭니다(인덱스 파일 제외).
큰 샘플의 경우 리포지토리 루트 아래에 있는 *samples* 폴더에 포함합니다.

적절한 Markdown 구문을 수행해야 합니다. 자세한 내용은 [스타일 가이드](./styleguide/template.md)를 참조하세요.

### <a name="example-structure"></a>예제 구조

```
docs
  /about
  /core
    /porting
      porting-overview.md
      /media
        /porting-overview
            portability_report.png
```

**4단계:** 분기의 PR(끌어오기 요청)을 `dotnet/docs/master`, `dotnet/dotnet-api-docs/master` 또는 `dotnet/samples/master`에 제출합니다.

PR은 *항상* 마스터 분기를 대상으로 지정해야 합니다. 라이브 분기를 대상으로 지정하는 PR을 *절대* 열면 안 됩니다.

일반적으로 각 PR에서 한 번에 하나씩 문제를 해결해야 합니다. PR은 하나 이상의 파일을 수정할 수 있습니다. 여러 파일에서 여러 개의 수정 사항을 처리하는 경우 별도의 PR을 사용하는 것이 좋습니다.

PR에서 기존 문제를 해결하는 경우 커밋 메시지 또는 PR 설명에 `Fixes #Issue_Number` 키워드를 추가합니다. 이렇게 하면 PR이 병합될 때 문제가 자동으로 닫힙니다. 자세한 내용은 [커밋 메시지를 통해 문제 닫기](https://help.github.com/articles/closing-issues-via-commit-messages/)를 참조하세요.

.NET 팀은 PR를 검토하고, 승인을 받는 데 필요한 다른 업데이트/변경 내용이 있을 경우 알려 줍니다.

**5단계:** 팀에서 설명한 대로 분기에 필요한 모든 업데이트를 수행합니다.

피드백이 적용되고 변경 내용이 승인되면 유지 관리자가 PR을 마스터 분기에 병합합니다.

특정 주기에서는 모든 커밋을 마스터 분기에서 라이브 분기로 푸시한 다음, 기여를 https://docs.microsoft.com/dotnet/ 에서 라이브로 글을 확인할 수 있습니다.

### <a name="contributing-to-samples"></a>샘플에 기여

리포지토리에 있는 코드는 다음과 같이 구분됩니다.

- 샘플: 독자가 샘플을 다운로드하고 실행할 수 있습니다. 모든 샘플은 전체 애플리케이션 또는 라이브러리여야 합니다. 샘플에서 라이브러리를 만드는 경우 독자가 코드를 실행할 수 있도록 하는 단위 테스트 또는 애플리케이션을 포함해야 합니다.

- 코드 조각: 더 작은 개념이나 작업을 설명합니다. 컴파일되지만 전체 애플리케이션은 아닙니다.

모든 코드는 [dotnet/samples](https://github.com/dotnet/samples) 리포지토리에 있습니다. samples 폴더 구조가 docs 폴더 구조와 일치하는 모델을 만들기 위해 노력하고 있습니다. 따르는 표준은 다음과 같습니다.

- 최상위 *snippets* 폴더에는 작은 집중 샘플에 대한 코드 조각이 들어 있습니다.
- API 참조 샘플은 다음 패턴을 따르는 폴더에 있습니다. ‘snippets/\<언어>/api/\<네임스페이스>/\<API 이름>’  .
- 다른 최상위 폴더는 *docs* 리포지토리의 최상위 폴더와 일치합니다. 예를 들어 docs 리포지토리에는 *machine-learning/tutorials* 폴더가 있으며, 기계 학습 자습서의 샘플은 *samples/machine-learning/tutorials* 폴더에 있습니다.

또한 *core* 및 *standard* 폴더 아래의 모든 샘플은 .NET Core에서 지원하는 모든 플랫폼에서 빌드 및 실행되어야 합니다. CI 빌드 시스템에서 이 표준을 준수하는지 확인합니다. 최상위 *framework* 폴더에는 Windows에서만 빌드되고 유효성이 검사되는 샘플이 들어 있습니다.

docs 리포지토리에서 새 콘텐츠를 추가함에 따라 이러한 디렉터리가 확장될 수 있습니다. 예를 들어 `xamarin-ios` 및 `xamarin-android` 디렉터리와 같은 Xamarin 디렉터리가 추가됩니다.

만드는 전체 샘플마다 *readme.md* 파일이 포함되어야 합니다. 이 파일에는 샘플에 대한 간단한 설명(한두 개 단락)이 포함되어야 합니다. *readme.md*는 이 샘플을 탐색하여 배울 수 있는 점을 독자에게 설명해야 합니다. *readme.md* 파일에는 [.NET 문서 사이트](https://docs.microsoft.com/dotnet/welcome)의 라이브 문서에 대한 링크도 포함되어야 합니다.
리포지토리의 지정된 파일이 해당 사이트에 매핑되는 위치를 확인하려면 리포지토리 경로의 `/docs`를 `https://docs.microsoft.com/dotnet`로 바꿉니다.

항목에는 샘플에 대한 링크도 포함됩니다. GitHub의 샘플 폴더에 바로 연결됩니다.

자세한 내용은 [샘플 Readme](https://github.com/dotnet/samples/blob/master/README.md)를 참조하세요.

## <a name="the-c-interactive-experience"></a>C# 대화형 환경

C#의 짧은 코드 샘플은 `csharp-interactive` 언어 태그를 사용하여 브라우저에서 실행되는 C# 샘플을 지정할 수 있습니다. 인라인 코드 샘플은 `csharp-interactive` 태그를 사용합니다. 소스에서 포함된 코드 조각의 경우 `code-csharp-interactive` 태그를 사용합니다. 이러한 코드 샘플은 문서에 코드 창과 출력 창을 표시합니다. 사용자가 샘플을 실행하고 나면 출력 창에 대화형 코드 실행에서 생성된 출력이 모두 표시됩니다. 

C# 대화형 환경은 샘플 작업 방법을 변경합니다. 방문자가 샘플을 실행하여 결과를 확인할 수 있습니다. 샘플 또는 해당 텍스트에 출력 정보가 포함되어야 하는지 여부를 판별하는 데 도움이 되는 여러 요인이 있습니다.

### <a name="when-to-display-the-expected-output-without-running-the-sample"></a>샘플을 실행하지 않고 예상 출력을 표시해야 하는 경우

- 초보자용 문서는 독자가 작업 출력을 예상 답변과 비교할 수 있도록 출력을 제공해야 합니다.
- 출력이 항목에 중요한 샘플은 해당 출력을 표시해야 합니다. 예를 들어 서식 있는 텍스트에 대한 문서는 샘플을 실행하지 않고 텍스트 형식을 표시해야 합니다.
- 샘플과 예상 출력이 모두 짧은 경우 출력을 표시하는 것이 좋습니다. 그러면 시간이 약간 절약됩니다.
- 현재 문화권 또는 고정 문화권이 출력에 미치는 영향을 설명하는 문서에서는 예상 출력에 대해 설명해야 합니다. 대화형 REPL(read–eval–print loop)은 Linux 기반 호스트에서 실행됩니다. 기본 문화권 및 고정 문화권은 운영 체제 및 머신마다 다른 출력을 생성합니다. 문서에서 Windows, Linux 및 Mac 시스템의 출력에 대해 설명해야 합니다.

### <a name="when-to-exclude-expected-output-from-the-sample"></a>샘플에서 예상 출력을 제외해야 하는 경우 

- 샘플에서 큰 출력을 생성하는 문서의 경우 주석에 출력을 포함하면 안 됩니다. 샘플이 실행되고 나면 코드가 모호해집니다.
- 샘플이 항목을 설명하지만 출력이 없어도 항목을 이해하는 데 문제가 없는 문서. 예를 들어 LINQ 쿼리를 실행하여 쿼리 구문을 설명한 이후에 출력 컬렉션에 모든 항목을 표시하는 코드입니다.

## <a name="dos-and-donts"></a>권고 및 금지

다음 목록은 .NET 문서에 기여할 때 유의해야 하는 몇 가지 지침 규칙을 보여 줍니다.

- **금지** 대규모 끌어오기 요청을 제공합니다. 대신, 많은 시간을 투자하기 전에 방향에 동의할 수 있도록 문제를 저장하고 토론을 시작합니다.
- **권고** [스타일 가이드](./styleguide/template.md) 및 [어투 및 어조](./styleguide/voice-tone.md) 지침을 참고합니다.
- **권고** [템플릿](./styleguide/template.md) 파일을 작업의 시작점으로 사용합니다.
- **권고** 문서에서 작업하기 전에 포크의 별도 분기를 만듭니다.
- **권고** [GitHub 흐름 워크플로](https://guides.github.com/introduction/flow/)를 수행합니다.
- **권고** 기여에 대해 자주 블로깅하고 트윗(무엇이든)합니다.

> 참고: 현재 일부 항목이 여기 및 [스타일 가이드](./styleguide/template.md)에 지정된 지침을 따르지 않는 것을 확인할 수 있습니다. 사이트 전체에서 일관성을 달성하기 위해 노력하고 있습니다. 특정 목표에 대해 현재 추적 중인 [열린 문제](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Aguidelines-adherence) 목록을 확인하세요.

## <a name="contributor-license-agreement"></a>기여자 라이선스 계약

PR을 병합하기 전에 [.NET Foundation CLA(기여 라이선스 계약)](https://cla.dotnetfoundation.org)에 서명해야 합니다. .NET Foundation의 프로젝트에 대한 일회성 요구 사항입니다. Wikipedia에서 [CLA(기여 라이선스 계약)](https://en.wikipedia.org/wiki/Contributor_License_Agreement)에 대해 참고할 수 있습니다.

계약: [net-foundation-contribution-license-agreement.pdf](https://github.com/dotnet/home/blob/master/guidance/net-foundation-contribution-license-agreement.pdf)

계약서에 미리 서명할 필요가 없습니다. PR을 일반적인 방식으로 복제하고, 포크하고, 제출할 수 있습니다. PR이 만들어지면 CLA 봇에 의해 분류됩니다. 변경 내용이 간단한 경우(예: 오타 수정) PR에 `cla-not-required` 레이블이 지정됩니다. 그렇지 않으면 `cla-required`로 분류됩니다. CLA에 서명하면 현재 및 이후의 모든 끌어오기 요청에 `cla-signed` 레이블이 지정됩니다.
