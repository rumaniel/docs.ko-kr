---
title: .NET Framework의 애플리케이션 호환성
ms.date: 05/19/2017
helpviewer_keywords:
- application compatibility
- .NET Framework application compatibility
- .NET Framework changes
ms.assetid: c4ba3ff2-fe59-4c5d-9e0b-86bba3cd865c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f547180995ec155f9121eeace109e7dfb07c7827
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790119"
---
# <a name="application-compatibility-in-the-net-framework"></a>.NET Framework의 애플리케이션 호환성

## <a name="introduction"></a>소개
호환성은 각 .NET 릴리스의 매우 중요한 목표입니다. 호환성이 있으면 각 버전이 누적되므로 이전 버전이 계속 작동합니다. 반면, 성능 향상, 보안 문제 해결 또는 버그 수정을 위해 이전 기능이 변경되면 이후 버전에서 실행되는 기존 코드 또는 기존 애플리케이션에서 호환성 문제가 발생할 수 있습니다. .NET Framework는 대상 다시 지정 변경 내용 및 런타임 변경 내용을 인식합니다. 대상 다시 지정 변경 내용은 .NET Framework의 특정 버전을 대상으로 지정하지만 이후 버전에서 실행되는 애플리케이션에 영향을 미칩니다. 런타임 변경 내용은 특정 버전에서 실행되는 모든 애플리케이션에 영향을 미칩니다.

각 앱은 .NET Framework의 특정 버전을 대상으로 하며, 다음을 통해 지정됩니다.

- Visual Studio에서 대상 프레임워크 정의
- 프로젝트 파일에서 대상 프레임워크 지정
- 소스 코드에 <xref:System.Runtime.Versioning.TargetFrameworkAttribute> 적용

대상으로 지정된 버전보다 더 새로운 버전에서 실행될 경우 .NET Framework는 특수 동작을 사용하여 대상으로 지정된 이전 버전을 모방합니다. 즉, 앱은 Framework의 더 새로운 버전에서 실행되지만 이전 버전에서 실행되는 것처럼 동작합니다. .NET Framework 버전 간의 대부분의 호환성 문제는 이 특수 모델을 통해 완화됩니다. 애플리케이션의 대상이 되는 .NET Framework 버전은 코드가 실행되는 애플리케이션 도메인의 항목 어셈블리의 대상 버전에 따라 결정됩니다. 해당 애플리케이션 도메인에 로드된 모든 추가 어셈블리는 이 .NET Framework 버전을 대상으로 합니다. 예를 들어, 실행 파일의 경우, 실행 파일의 대상 프레임워크는 해당 AppDomain의 모든 어셈블리가 실행되는 호환 모드입니다.

## <a name="runtime-changes"></a>런타임 변경 내용

런타임 문제는 새 런타임이 컴퓨터에서 발생하고 같은 이진 파일이 실행되지만 다른 동작이 확인될 경우 발생하는 문제입니다. .NET Framework 4.0용으로 컴파일된 이진 파일은 4.5 이상 버전의 .NET Framework 4.0 호환성 모드에서 실행됩니다. 4\.5에 영향을 미치는 대부분의 변경 내용은 4.0용으로 컴파일된 이진 파일에 영향을 미치지 않습니다. 이 내용은 AppDomain에만 적용되고 항목 어셈블리의 설정에 따라 달라집니다.

## <a name="retargeting-changes"></a>대상 다시 지정 변경 내용

대상 다시 지정 문제는 4.0을 대상으로 하는 어셈블리가 4.5를 대상으로 지정하도록 설정된 경우 발생하는 문제입니다. 이제 어셈블리는 이전 기능에 대한 잠재적인 호환성 문제뿐 아니라 새로운 기능을 선택합니다. 또한 이것은 어셈블리를 사용하는 콘솔 앱 또는 어셈블리를 참조하는 웹 사이트와 같은 항목 어셈블리에 의해 지정됩니다.

## <a name="net-compatibility-diagnostics"></a>.NET 호환성 진단

.NET 호환성 진단은 .NET Framework 버전 간에 애플리케이션 호환성 문제를 식별할 수 있도록 하는 Roslyn 기반 분석기입니다. 이 목록은 사용할 수 있는 모든 분석기를 포함하지만, 한 하위 집합은 특정 마이그레이션에만 적용됩니다. 분석기는 예정된 마이그레이션에 적용되는 문제를 확인하고 해당 문제만 표시합니다.

각 문제는 다음과 같은 정보를 포함합니다.

- 이전 버전에서 변경된 내용에 대한 설명입니다.

- 변경 내용이 고객에 미치는 영향 및 버전 간 호환성을 유지하기 위한 사용할 수 있는 해결 방법의 여부를 나타냅니다.

- 변경 내용의 중요성에 대한 평가입니다. 애플리케이션 호환성 문제는 다음과 같이 분류됩니다.

    |   |   |
    |---|---|
    |주요함|다수의 앱에 영향을 주거나 코드를 대폭 수정해야 하는 중요한 변경 내용입니다.|
    |부|소수의 앱에 영향을 주거나 코드를 약간만 수정해야 하는 변경 내용입니다.|
    |특별한 경우|매우 특별하고 일반적이지 않은 시나리오의 앱에 영향을 주는 변경 내용입니다.|
    |투명|애플리케이션 개발자나 사용자에게 뚜렷한 영향을 주지 않는 변경 내용입니다.|

- 버전은 변경 내용이 프레임워크에 처음 표시될 때를 나타냅니다. 일부 변경 내용이 특정 버전에 소개되고 이후 버전에서 되돌려지면 되돌려진 내용도 표시됩니다.

- 변경 형식:

    |   |   |
    |---|---|
    |대상 변경|새 버전의 .NET Framework를 대상으로 다시 컴파일되는 앱에 변경 내용이 적용됩니다.|
    |런타임|이전 버전의 .NET Framework를 대상으로 하지만 이후 버전에서 실행되는 기존 앱에 변경 내용이 적용됩니다.|

- 영향을 받는 API입니다(있는 경우).

- 사용 가능한 진단의 ID

## <a name="usage"></a>사용
시작하려면 아래에서 호환성 변경 형식을 선택합니다.

- [대상 다시 지정 변경 내용](./retargeting/index.md)
- [런타임 변경 내용](./runtime/index.md)

## <a name="see-also"></a>참고 항목

- [버전 및 종속성](versions-and-dependencies.md)
- [새로운 기능](../whats-new/index.md)
- [클래스 라이브러리의 사용되지 않는 기능](../whats-new/whats-obsolete.md)
