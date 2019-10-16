---
title: .NET Compiler Platform SDK 개념 및 개체 모델
description: 이 개요는 .NET 컴파일러 SDK와 함께 효과적으로 작동해야 하는 배경 정보를 제공합니다. API 계층, 관련된 주요 형식 및 전체 개체 모델을 학습합니다.
ms.date: 10/10/2017
ms.custom: mvc
ms.openlocfilehash: ee8f902bf1df8b63e229fd518e7a0c592fcd47ca
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675708"
---
# <a name="understand-the-net-compiler-platform-sdk-model"></a>.NET Compiler Platform SDK 모델 이해

컴파일러는 종종 사람이 코드를 읽고 이해하는 방식과 다른 구조적 규칙을 따라 작성하는 코드를 처리합니다. 컴파일러에서 사용되는 모델에 대한 기본적인 이해는 Roslyn 기반 도구를 빌드할 때 사용하는 API를 이해하는 데 반드시 필요합니다. 

## <a name="compiler-pipeline-functional-areas"></a>컴파일러 파이프라인 기능 영역

.NET Compiler Platform SDK는 기존의 컴파일러 파이프라인을 미러링하는 API 계층을 제공하여 소비자로서 사용자에게 C# 및 Visual Basic 컴파일러의 코드 분석을 노출합니다.

![개체 코드로 소스 코드를 처리하는 컴파일러 파이프라인의 단계](media/compiler-api-model/compiler-pipeline.png)

이 파이프라인의 각 단계는 별도 구성 요소입니다. 첫째로, 구문 분석 단계는 원본 텍스트를 언어 문법 뒤에 오는 구문으로 토큰화하고 구문 분석합니다. 둘째로, 선언 단계는 원본 및 가져온 메타데이터를 분석하여 명명된 기호를 형성합니다. 다음으로 바인딩 단계는 코드의 식별자를 기호와 일치시킵니다. 마지막으로 내보내기 단계는 컴파일러로 생성된 모든 정보와 함께 어셈블리를 내보냅니다.

![컴파일러 파이프라인 API는 컴파일러 파이프라인의 일부인 각 단계에 대한 액세스를 제공합니다.](media/compiler-api-model/compiler-pipeline-api.png)

이러한 각 단계에 해당하여 .NET Compiler Platform SDK는 해당 단계에서 정보에 액세스할 수 있는 개체 모델을 노출합니다. 구문 분석 단계는 구문 트리를 노출하고, 선언 단계는 계층적 기호 테이블을 노출하고, 바인딩 단계는 컴파일러의 의미 체계 분석 결과를 노출하고, 내보내기 단계는 IL 바이트 코드를 생성하는 API입니다.

![컴파일러 파이프라인의 각 단계에서 컴파일러 API에 사용할 수 있는 언어 서비스](media/compiler-api-model/compiler-pipeline-lang-svc.png)

각 컴파일러는 단일 엔드투엔드 전체로 이러한 구성 요소를 하나로 결합합니다.

이러한 API는 Visual Studio에서 사용하는 API와 동일합니다. 예를 들어 코드 개요 및 서식 지정 기능은 구문 트리를 사용하고, 개체 브라우저 및 탐색 기능은 기호 테이블을 사용하며, 리팩터링 및 정의로 이동은 의미 체계 모델을 사용하고, 편집하며 계속하기는 내보내기 API를 포함하여 이러한 모든 것을 사용합니다. 

## <a name="api-layers"></a>API 계층

.NET 컴파일러 SDK는 두 개의 주요 API 계층인 컴파일러 API 및 작업 영역 API로 이루어져 있습니다.

![컴파일러 파이프라인 API에 의해 표시되는 API 계층](media/compiler-api-model/api-layers.png)

### <a name="compiler-apis"></a>컴파일러 API

컴파일러 계층은 구문 및 의미 체계 모두의 컴파일러 파이프라인의 각 단계에서 노출되는 정보에 해당하는 개체 모델을 포함합니다. 컴파일러 계층은 어셈블리 참조, 컴파일러 옵션 및 소스 코드 파일을 포함하는 컴파일러 단일 호출의 변경할 수 없는 스냅샷도 포함합니다. C# 언어 및 Visual Basic 언어를 나타내는 두 개의 고유한 API가 있습니다. 이러한 두 개의 API는 모양에서 유사하지만 각 개별 언어에 대한 충실도가 높도록 맞춰집니다. 이 계층에는 Visual Studio 구성 요소에 대한 종속성이 없습니다.

### <a name="diagnostic-apis"></a>진단 API

해당 분석의 일환으로 컴파일러는 구문, 의미 체계 및 확실한 할당 오류에서부터 다양한 경고 및 정보 진단까지 모든 것을 다루는 진단 집합을 생성할 수 있습니다. 컴파일러 API 계층은 사용자 정의 분석기를 컴파일 프로세스에 연결할 수 있도록 하는 확장 가능한 API를 통해 진단을 노출합니다. StyleCop 또는 FxCop과 같은 도구에서 만든 것과 같은 사용자 정의 진단을 컴파일러 정의 진단과 함께 생성되도록 합니다. 이러한 방식으로 진단을 생성하면 정책에 기반한 빌드 중지 및 편집기에서 라이브 물결선 표시 및 코드 수정 사항 제안과 같은 환경에 대한 진단에 의존하는 MSBuild 및 Visual Studio와 같은 도구와 자연스럽게 통합하는 이점을 갖습니다.

### <a name="scripting-apis"></a>스크립팅 API

호스팅 및 스크립팅 API는 컴파일러 계층의 일부입니다. 코드 조각을 실행하고 런타임 실행 컨텍스트를 누적하는 데 사용할 수 있습니다.
C# 대화형 REPL(읽기 평가 인쇄 루프)은 이러한 API를 사용합니다. REPL을 통해 작성함에 따라 대화형으로 코드를 실행하여 스크립팅 언어로 C#을 사용할 수 있습니다.

### <a name="workspaces-apis"></a>작업 영역 API

작업 영역 계층은 코드 분석을 수행하고 전체 솔루션을 통해 리팩터링하는 시작 지점인 작업 영역 API를 포함합니다. 파일을 구문 분석하고, 옵션을 구성하거나 프로젝트 간 종속성을 관리하지 않고도 컴파일러 계층 개체 모델에 대한 직접 액세스를 제공하여 솔루션의 프로젝트에 대한 모든 정보를 단일 개체 모델로 구성하는 데 도움을 줍니다.

또한 작업 영역 계층은 코드 분석을 구현하고 Visual Studio IDE와 같은 호스트 환경 내에서 작동하는 도구를 리팩터링할 때 사용되는 API 집합을 나타냅니다. 모든 참조 찾기, 서식 지정 및 코드 생성 API를 예로 들 수 있습니다.

이 계층에는 Visual Studio 구성 요소에 대한 종속성이 없습니다.
