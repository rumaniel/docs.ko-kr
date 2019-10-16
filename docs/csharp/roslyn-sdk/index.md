---
title: .NET Compiler Platform SDK(Roslyn API)
description: .NET Compiler Platform SDK(Roslyn API라고도 함)를 사용하여 .NET 코드를 이해하고 오류를 찾고 이러한 오류를 수정하는 방법을 알아봅니다.
ms.date: 10/10/2017
ms.custom: mvc
ms.openlocfilehash: ea733d4c5c54c18e510a028f3a724f89490db9dd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61706548"
---
# <a name="the-net-compiler-platform-sdk"></a>.NET Compiler Platform SDK

컴파일러는 애플리케이션 코드의 구문 및 의미 체계의 유효성을 검사할 때 애플리케이션 코드의 세부 모델을 빌드합니다. 컴파일러는 이 모델을 사용하여 소스 코드에서 실행 가능 출력을 빌드합니다. .NET Compiler Platform SDK는 이 모델에 대한 액세스를 제공합니다. 우리는 점점 더 IntelliSense, 리팩터링, 지능형 이름 바꾸기, “모든 참조 찾기” 및 “정의로 이동”과 같은 IDE(통합 개발 환경) 기능에 의존하여 생산성을 높입니다. 또한 코드 분석 도구를 사용하여 코드 품질을 개선하고 코드 생성기를 사용하여 애플리케이션 구성에서 도움을 받습니다. 이러한 도구가 더 스마트해짐에 따라 컴파일러가 애플리케이션 코드를 처리할 때 컴파일러만이 만드는 모델의 점점 더 많은 부분에 이러한 도구가 액세스해야 합니다. 이것이 바로 Roslyn API의 핵심 임무입니다. 블랙 박스를 열고 도구 및 최종 사용자가 컴파일러가 코드에 대해 가진 다양한 정보를 공유할 수 있도록 하는 것 말입니다.
컴파일러는 불투명한 소스 코드 입력 변환기 및 개체 코드 출력 변환기 대신 Roslyn을 통해 플랫폼이 됩니다. 즉, 도구 및 애플리케이션에서 코드 관련 작업에 사용할 수 있는 API입니다.

## <a name="net-compiler-platform-sdk-concepts"></a>.NET Compiler Platform SDK 개념

.NET Compiler Platform SDK는 코드 중심 도구 및 애플리케이션을 만들기 위한 진입에 대한 장벽을 크게 낮춰줍니다. 메타 프로그래밍, 코드 생성 및 변환, C# 및 VB 언어의 대화형 사용, 도메인 특정 언어에서 C# 및 VB 포함과 같은 영역의 혁신을 위한 많은 기회를 만듭니다.

.NET Compiler Platform SDK를 사용하면 코딩 실수를 찾아 수정하는 ***분석기*** 및 ***코드 수정 사항***을 빌드할 수 있습니다. ***분석기***는 코드의 구문 및 구조를 이해하고 수정되어야 하는 습관을 검색합니다. ***코드 수정 사항***은 분석기가 발견한 코딩 실수를 해결하기 위한 한 가지 이상의 제안된 수정 사항을 제공합니다. 일반적으로 분석기 및 연관된 코드 수정 사항은 단일 프로젝트에서 함께 패키지됩니다.

분석기 및 코드 수정 사항은 정적 분석을 사용하여 코드를 이해하며, 코드를 실행하거나 다른 테스트 이점을 제공하지 않습니다. 그러나 흔히 버그로 이어지는 습관, 유지 관리할 수 없는 코드 또는 표준 지침 유효성 검사를 지적할 수 있습니다.

.NET Compiler Platform SDK는 C# 또는 Visual Basic 코드베이스를 검사하고 이해할 수 있게 해주는 단일 API 집합을 제공합니다. 이 단일 코드베이스를 사용할 수 있으므로 .NET Compiler Platform SDK에서 제공하는 구문 및 의미 체계 분석 API를 활용하여 분석기 및 코드 수정 사항을 더 쉽게 작성할 수 있습니다. 컴파일러가 수행한 분석을 복제하는 대규모 작업에서 벗어난 사용자는 프로젝트 또는 라이브러리에 대한 일반적인 코딩 오류를 찾아 수정하는 더 중심이 되는 작업에 집중할 수 있습니다.

작은 이점 한 가지는 사용자가 직접 프로젝트의 코드를 이해하기 위해 자체 코드베이스를 작성하는 경우보다 Visual Studio에 로드되었을 때 분석기 및 코드 수정 사항이 메모리를 훨씬 더 적게 사용하고 규모가 작다는 것입니다. 컴파일러 및 Visual Studio에서 사용되는 것과 같은 클래스를 활용하여 자체 정적 분석 도구를 만들 수 있습니다. 즉, 팀은 IDE 성능에 대한 눈에 띄는 영향 없이 분석기 및 코드 수정 사항을 사용할 수 있습니다.

분석기 및 코드 수정 사항을 작성하는 세 가지 주요 시나리오가 있습니다.

1. [*팀 코딩 표준 적용*](#enforce-team-coding-standards)
1. [*라이브러리 패키지로 지침 제공*](#provide-guidance-with-library-packages)
1. [일반 지침 제공](#provide-general-guidance)

## <a name="enforce-team-coding-standards"></a>팀 코딩 표준 적용

많은 팀에는 다른 팀 구성원과의 코드 검토를 통해 적용되는 코딩 표준이 있습니다. 분석기 및 코드 수정 사항은 이 프로세스를 훨씬 더 효율적으로 만들 수 있습니다. 코드 검토는 개발자가 다른 팀 구성원과 자신의 작업을 공유할 때 발생합니다. 개발자는 의견을 듣기 전에 새로운 기능을 완성하는 데 필요한 모든 시간을 투자했을 것입니다. 개발자가 팀의 습관과 일치하지 않는 습관을 강화하는 동안 몇 주가 흐를 수도 있습니다.

개발자가 코드를 작성할 때 분석기가 실행됩니다. 개발자는 즉시 지침을 따르도록 권장하는 즉각적인 피드백을 받습니다. 개발자는 프로토타입 생성을 시작하는 즉시 규격 코드를 작성하는 습관이 붙게 됩니다. 기능이 사람에 의한 검토를 받을 준비가 되면 모든 표준 지침이 적용된 상태가 되어 있습니다.

팀은 팀 코딩 습관을 위반하는 가장 일반적인 습관을 찾는 분석기 및 코드 수정 사항을 빌드할 수 있습니다. 이러한 분석기 및 코드 수정 사항을 각 개발자의 컴퓨터에 설치하여 표준을 적용할 수 있습니다.

## <a name="provide-guidance-with-library-packages"></a>라이브러리 패키지로 지침 제공

NuGet에는 .NET 개발자가 사용할 수 있는 다양한 라이브러리가 있습니다.
이러한 라이브러리 중 일부는 Microsoft에서 제공한 것이고, 또 다른 일부는 타사에서 제공한 것이며, 나머지는 커뮤니티 회원 및 지원자가 제공한 것입니다. 개발자가 이러한 라이브러리로 성공할 수 있는 경우 해당 라이브러리는 더 많이 채택되고 더 많은 검토를 받게 됩니다.

설명서를 제공하는 것 외에 라이브러리의 일반적인 오용을 찾아 수정하는 분석기 및 코드 수정 사항을 제공할 수 있습니다. 이러한 즉각적인 수정 사항은 개발자가 더 빠르게 성공하도록 도와줍니다.

NuGet의 라이브러리를 사용하여 분석기 및 코드 수정 사항을 패키지할 수 있습니다. 해당 시나리오에서 NuGet 패키지를 설치하는 모든 개발자는 분석기 패키지도 설치합니다. 라이브러리를 사용하는 모든 개발자는 실수 및 제안된 수정 사항에 대한 즉각 적인 피드백의 형태로 팀으로부터 즉시 지침을 받게 됩니다.

## <a name="provide-general-guidance"></a>일반 지침 제공

.NET 개발자 커뮤니티는 잘 작동하는 경험 패턴과 가장 피해야 할 패턴을 간파해왔습니다. 여러 커뮤니티 회원은 이러한 권장 패턴을 적용하는 분석기를 만들었습니다. 자세히 알아보다 보면 항상 새로운 아이디어를 위한 여지가 있음을 알게 됩니다.

이러한 분석기를 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)에 업로드하고 Visual Studio를 사용하는 개발자가 다운로드할 수 있습니다. 언어 및 플랫폼을 처음 사용하는 초보자는 일반적으로 인정된 습관을 신속하게 배우고 .NET 여정에서 조기에 생산성을 높일 수 있습니다. 이러한 습관이 더 널리 사용됨에 따라 커뮤니티에서는 이러한 습관을 채택합니다.

## <a name="next-steps"></a>다음 단계

.NET Compiler Platform SDK에는 코드 생성, 분석 및 리팩터링에 대한 최신 언어 개체 모델이 포함되어 있습니다. 이 섹션에서는 .NET Compiler Platform SDK에 대한 개념적 개요를 제공합니다. 자세한 내용은 빠른 시작, 샘플 및 자습서 섹션에서 확인할 수 있습니다.

다음 다섯 가지 항목에서 .NET Compiler Platform SDK의 개념에 대해 자세히 알아볼 수 있습니다.

- [구문 시각화 도우미를 사용하여 코드 탐색](syntax-visualizer.md)
- [컴파일러 API 모델 이해](compiler-api-model.md)
- [구문 작업](work-with-syntax.md)
- [의미 체계 작업](work-with-semantics.md)
- [작업 영역 작업](work-with-workspace.md)

시작하려면 **.NET Compiler Platform SDK**를 설치해야 합니다.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

<!--

Turn this on as more of the conceptual content is in place:
- Try the [Quickstarts](quickstart/index.md) to create your first tutorial.
- Experiment with one of the [Tutorials](tutorials/index.md).
- Explore the [Samples](samples/index.md) to see some simple analyzers.
- Read the [Concepts](concepts/index.md) to understand the ideas behind analyzers and code fixes.

-->
