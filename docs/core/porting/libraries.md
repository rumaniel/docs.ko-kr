---
title: .NET Core로 라이브러리 포팅
description: .NET Framework에서 .NET Core로 라이브러리 프로젝트를 이식하는 방법에 관해 알아봅니다.
author: cartermp
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: 3e3c613f6be50ae5ff2b07052c7c1bced2047855
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70105297"
---
# <a name="port-net-framework-libraries-to-net-core"></a>.NET Core로 .NET Framework 라이브러리 포팅

.NET Framework 라이브러리 코드를 .NET Core로 포팅하고, 플랫폼 간에 실행하고, 코드를 사용하는 앱의 도달 범위를 확장하는 방법을 알아봅니다.

## <a name="prerequisites"></a>전제 조건

이 문서에서는 다음을 전제로 합니다.

- 사용자가 Visual Studio 2017 이상을 사용합니다.
  - .NET Core는 이전 버전의 Visual Studio에서 지원되지 않습니다.
- 사용자가 [권장 이식 프로세스](index.md)를 이해합니다.
- 사용자가 [타사 종속성](third-party-deps.md)과 관련된 문제를 모두 해결했습니다.

또한 다음 항목의 내용을 숙지해야 합니다.

[.NET 표준](../../standard/net-standard.md)\
이 항목에서는 모든 .NET 구현에서 사용할 수 있는 .NET API의 공식 사양에 관해 설명합니다.

[패키지, 메타패키지 및 프레임워크](../packages.md)   
이 문서에서는 .NET Core가 패키지를 정의하고 사용하는 방법과 패키지가 여러 .NET 구현에서 실행되는 코드를 지원하는 방법에 관해 설명합니다.

[플랫폼 간 도구로 라이브러리 개발](../tutorials/libraries.md)   
이 항목에서는 플랫폼 간 CLI 도구를 사용하여 .NET용 라이브러리를 작성하는 방법에 관해 설명합니다.

[.NET Core용 *csproj* 형식에 대한 추가 사항](../tools/csproj.md)   
이 문서에서는 *csproj* 및 MSBuild로 프로젝트 시스템을 전환함에 따라 프로젝트 파일에 추가된 변경 내용을 간략하게 설명합니다.

[.NET Core로 이식 - 타사 종속성 분석](third-party-deps.md)   
이 항목에서는 타사 종속성의 이식성 및 .NET Core에서 NuGet 패키지 종속성이 실행되지 않는 경우 해야 할 작업에 관해 설명합니다.

## <a name="retargeting-your-net-framework-code-to-net-framework-472"></a>.NET Framework 4.7.2로 .NET Framework 코드 대상 다시 지정

코드가 .NET Framework 4.7.2를 대상으로 하지 않는 경우 .NET Framework 4.7.2로 대상을 다시 지정하는 것이 좋습니다. 그러면 .NET 표준에서 기존 API를 지원할 수 없는 경우 최신 API를 대신 사용할 수 있습니다.

Visual Studio에서 이식하려는 각 프로젝트에 대해 다음을 수행합니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
1. **대상 프레임워크** 드롭다운에서 **.NET Framework 4.7.2**를 선택합니다.
1. 프로젝트를 다시 컴파일합니다.

프로젝트가 .NET Framework 4.7.2를 대상으로 하기 때문에 해당 버전의 .NET Framework를 코드 포팅의 기반으로 사용합니다.

## <a name="determining-the-portability-of-your-code"></a>코드의 이식성 확인

다음 단계에서는 API Portability Analyzer(ApiPort)를 실행하여 분석을 위한 이식성 보고서를 생성합니다.

[API 이식성 도구(ApiPort)](../../standard/analyzers/portability-analyzer.md)를 이해하고 .NET Core를 대상으로 하는 이식성 보고서를 생성할 수 있어야 합니다. 이 작업을 수행하는 방법은 요구 사항 및 개인적 취향에 따라 달라질 수 있습니다. 다음은 몇 가지 서로 다른 접근 방식입니다. 코드가 어떻게 구성되어 있는가에 따라 이러한 접근 방식의 단계를 혼합하여 사용할 수 있습니다.

### <a name="dealing-primarily-with-the-compiler"></a>주로 컴파일러 처리

이 접근 방식은 작은 프로젝트 또는 많은 .NET Framework API를 사용하지 않는 프로젝트에 가장 적합할 수 있습니다. 접근 방식은 간단합니다.

1. 필요에 따라 프로젝트에서 ApiPort를 실행합니다. ApiPort를 실행하는 경우 해결해야 할 문제에 대한 보고서에서 정보를 가져오세요.
1. 모든 코드를 새 .NET Core 프로젝트에 복사합니다.
1. 이식성 보고서(생성된 경우)를 참조하면서 프로젝트가 완전히 컴파일될 때까지 컴파일러 오류를 해결합니다.

이 접근 방식은 구조적이지는 않지만 코드 중심 접근 방식을 사용하면 종종 문제를 신속하게 해결할 수 있으므로 더 작은 프로젝트나 라이브러리에 가장 적합한 방법이 될 수 있습니다. 데이터 모델만 포함하는 프로젝트가 이 접근 방식에 적합한 후보가 될 수 있습니다.

### <a name="staying-on-the-net-framework-until-portability-issues-are-resolved"></a>이식성 문제가 해결될 때까지 .NET Framework 유지

이 접근 방식은 전체 프로세스 중에 컴파일되는 코드를 선호하는 경우 적합할 수 있습니다. 이 접근 방식은 다음과 같습니다.

1. 프로젝트에서 ApiPort를 실행합니다.
1. 이식 가능한 다른 API를 사용하여 문제를 해결합니다.
1. 직접적인 대안을 사용할 수 없는 영역을 기록해 둡니다.
1. 각 프로젝트를 새 .NET Core 프로젝트에 복사할 준비가 되었다고 확신할 때까지 이식하려는 모든 프로젝트에 대해 이전 단계를 반복합니다.
1. 새 .NET Core 프로젝트에 코드를 복사합니다.
1. 직접적인 대안이 없는 것으로 기록해 둔 문제를 해결합니다.

이 신중한 접근 방식은 단순히 컴파일러 오류를 해결하는 것보다는 구조적이지만 비교적 코드 중심적이며 컴파일되는 코드가 항상 있다는 장점이 있습니다. 다른 API를 사용하여 해결할 수 없는 특정 문제를 해결하는 방법은 현저하게 달라집니다. 특정 프로젝트에 대해 보다 포괄적인 계획을 개발해야 할 수 있으며, 이는 다음 접근 방식에서 설명합니다.

### <a name="developing-a-comprehensive-plan-of-attack"></a>포괄적인 공격 계획 개발

이 접근 방식은 .NET Core를 지원하기 위해 코드를 재구성하거나 코드의 특정 영역을 완전히 다시 작성해야 할 수 있는 더 크고 더 복잡한 프로젝트에 가장 적합할 수 있습니다. 이 접근 방식은 다음과 같습니다.

1. 프로젝트에서 ApiPort를 실행합니다.
1. 이식 불가능한 각 형식이 사용되고 있는 위치 및 해당 형식이 전체 이식성에 어떻게 영향을 주는지를 파악합니다.
   - 해당 형식의 특성을 이해합니다. 수는 적은데 자주 사용되나요? 아니면 수는 많지만 자주 사용되지 않나요? 집중적으로 사용되나요? 아니면 코드 전체에 분산되어 있나요?
   - 이식할 수 없는 코드는 격리가 쉬우므로 더 효과적으로 처리할 수 있나요?
   - 코드를 리팩터링해야 하나요?
   - 이식할 수 없는 해당 형식에 대해 동일한 작업을 수행하는 다른 API가 있나요? 예를 들어 <xref:System.Net.WebClient> 클래스를 사용하고 있는 경우 <xref:System.Net.Http.HttpClient> 클래스를 대신 사용할 수 있습니다.
   - 드롭인 대체가 아닌 경우에도 작업을 수행하는 데 사용할 수 있는 이식 가능한 다른 API가 있나요? 예를 들어 <xref:System.Xml.Schema.XmlSchema>를 사용하여 XML을 구문 분석하지만 XML 스키마 검색이 필요하지 않은 경우, API를 사용하는 대신 <xref:System.Xml.Linq> API를 사용하고 직접 구문 분석을 구현할 수 있습니다.
1. 이식하기 어려운 어셈블리가 있는 경우 지금은 .NET Framework에 유지하는 것이 나을까요? 다음과 같은 몇 가지 사항을 고려해야 합니다.
   - .NET Framework 또는 Windows 관련 기능을 너무 많이 사용하기 때문에 .NET Core와 호환되지 않는 일부 기능이 라이브러리에 있을 수 있습니다. 기능 이식을 위해 리소스를 사용할 수 있을 때까지 임시로 해당 기능을 유지하고 당분간은 기능이 더 적은 라이브러리의 .NET Core 버전을 릴리스하는 것이 더 나을까요?
   - 리팩터링이 도움이 될까요?
1. 사용할 수 없는 .NET Framework API의 고유한 구현을 작성하는 것이 합리적일까요?
   [.NET Framework 참조 소스](https://github.com/Microsoft/referencesource)에서 코드를 복사, 수정 및 사용하는 것이 좋을 수 있습니다. 참조 소스 코드는 [MIT 라이선스](https://github.com/Microsoft/referencesource/blob/master/LICENSE.txt)에 따라 라이선스가 부여되므로, 소스를 자신의 코드에 대한 기초로 매우 자유롭게 사용할 수 있습니다. 코드에서 Microsoft 특성을 제대로 지정하기만 하면 됩니다.
1. 필요에 따라 다른 프로젝트에 대해 이 프로세스를 반복합니다.
 
분석 단계는 코드베이스의 크기에 따라 다소 시간이 걸릴 수 있습니다. 이 단계에서 시간을 할애하여 필요한 변경의 범위를 철저하게 이해하고 계획을 개발하면 장기 실행, 특히 복잡한 코드베이스가 있는 경우 일반적으로 시간이 절약됩니다.

계획에 코드베이스의 중요한 변경 작업을 포함하는 동시에 .NET Framework 4.7.2를 계속 대상으로 지정할 수 있으므로 이전 접근 방식보다 더 구조화된 버전으로 만들 수 있습니다. 계획 실행을 시작하는 방법은 코드베이스에 따라 달라집니다.

### <a name="mixing-approaches"></a>접근 방식 혼합

위의 접근 방식을 프로젝트 단위로 혼합하여 사용할 수 있습니다. 사용자 및 코드베이스에 가장 적합한 방법을 수행해야 합니다.

## <a name="porting-your-tests"></a>테스트 이식

코드를 이식한 경우 모든 항목이 제대로 작동하는지 확인하는 가장 좋은 방법은 .NET Core에 이식할 때 코드를 테스트하는 것입니다. 이렇게 하려면 .NET Core에 대한 테스트를 빌드하고 실행하는 테스트 프레임워크를 사용해야 합니다. 현재는 다음과 같은 세 가지 옵션이 있습니다.

- [xUnit](https://xunit.github.io/)
  - [시작](https://xunit.github.io/docs/getting-started-dotnet-core.html)
  - [MSTest 프로젝트를 xUnit으로 변환하는 도구](https://github.com/dotnet/codeformatter/tree/master/src/XUnitConverter)
- [NUnit](https://nunit.org/)
  - [시작](https://github.com/nunit/docs/wiki/Installation)
  - [MSTest에서 NUnit으로 마이그레이션에 대한 블로그 게시물](https://www.florian-rappl.de/News/Page/275/convert-mstest-to-nunit)
- [MSTest](https://docs.microsoft.com/visualstudio/test/unit-test-basics)

## <a name="recommended-approach-to-porting"></a>이식에 권장되는 접근 방식

궁극적으로 이식 작업은 .NET Framework 코드가 구성된 방법에 따라 크게 달라집니다. 코드를 이식하는 좋은 방법은 코드의 기본 구성 요소인 라이브러리의 *기본*으로 시작하는 것입니다. 이는 다른 모든 항목에서 직접적으로나 간접적으로 사용하는 데이터 모델이나 일부 다른 기본 클래스 및 메서드가 될 수 있습니다.

1. 현재 이식하고 있는 라이브러리의 계층을 테스트하는 테스트 프로젝트를 이식합니다.
1. 라이브러리의 기본을 새 .NET Core 프로젝트에 복사하고 지원하려는 .NET 표준의 버전을 선택합니다.
1. 코드를 컴파일하는 데 필요한 대로 내용을 변경합니다. 이 작업의 많은 부분에서 NuGet 패키지 종속성을 *csproj* 파일에 추가해야 할 수 있습니다.
1. 테스트를 실행하고 필요에 따라 조정합니다.
1. 이식할 다음 코드 계층을 선택하고 이전 단계를 반복합니다.

라이브러리의 기본으로 시작하고 기본에서 바깥쪽으로 이동하면서 필요에 따라 각 계층을 테스트하면, 이식은 한 번에 하나의 코드 계층으로 문제가 격리되는 체계적인 프로세스가 됩니다.

>[!div class="step-by-step"]
>[다음](project-structure.md)
