---
title: 보안 투명 코드
ms.date: 03/30/2017
helpviewer_keywords:
- transparent code
- security-transparent code
ms.assetid: 4f3dd841-82f7-4659-aab0-6d2db2166c65
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4e4e472185b3b2ba39393c029bca3966fb5ec4b3
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70206059"
---
# <a name="security-transparent-code"></a>보안 투명 코드

<a name="top"></a>

[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]

보안에는 샌드박싱, 권한 및 적용이라는 세 가지 조작 부분이 관련됩니다. 샌드박싱은 일부 코드를 완전히 신뢰할 수 있는 코드로 처리하고 다른 코드를 샌드박스에 대한 권한 부여 집합의 권한으로 제한하는 격리된 도메인을 만드는 방법을 나타냅니다. 샌드박스의 권한 부여 집합 내에서 실행되는 애플리케이션 코드는 투명한 것으로 간주합니다. 즉, 보안에 영향을 줄 수 있는 모든 작업을 수행할 수 없습니다. 샌드박스의 권한 부여 집합은 증거(<xref:System.Security.Policy.Evidence> 클래스)에 따라 결정됩니다. 증거는 샌드박스에 필요한 특정 권한 및 만들 수 있는 샌드박스 종류를 식별합니다. 적용은 투명 코드가 권한 부여 집합 내에서만 실행되도록 허용하는 것입니다.

> [!IMPORTANT]
> 보안 정책은 이전 .NET Framework 버전의 핵심 요소였습니다. .NET Framework 4부터 보안 정책은 사용 되지 않습니다. 보안 정책 제거는 보안 투명도와 관련이 없습니다. 이러한 변경의 영향에 대 한 자세한 내용은 [코드 액세스 보안 정책 호환성 및 마이그레이션](code-access-security-policy-compatibility-and-migration.md)을 참조 하세요.

이 항목에서는 투명도 모델에 대해 자세히 설명합니다. 여기에는 다음 단원이 포함되어 있습니다.

- [투명도 모델의 용도](#purpose)

- [투명도 수준 지정](#level)

- [투명도 적용](#enforcement)

<a name="purpose"></a>

## <a name="purpose-of-the-transparency-model"></a>투명도 모델의 목적

투명도는 애플리케이션 부분으로 실행되는 코드를 인프라 부분으로 실행되는 코드와 구분하는 적용 메커니즘입니다. 투명도는 네이티브 코드 호출과 같은 권한 있는 작업을 수행할 수 있는 코드(중요한 코드)와 수행할 수 없는 코드(투명 코드)를 구분합니다. 투명 코드는 작동하는 권한 집합 경계 내에서 명령을 실행하지만 중요한 코드를 실행 또는 포함하거나 중요한 코드에서 파생될 수 없습니다.

투명도 적용의 기본적인 목표는 권한에 따라 여러 코드 그룹을 격리하는 단순하고 효과적인 메커니즘을 제공하는 것입니다. 샌드박싱 모델의 컨텍스트 내에서 이들 권한 그룹은 완전히 신뢰되거나(제한 없음) 부분적으로 신뢰됩니다(샌드박스에 부여된 권한 집합으로 제한됨).

> [!IMPORTANT]
> 투명도 모델은 코드 액세스 보안을 초월합니다. 투명도는 JIT(Just-In-Time) 컴파일러에서 적용되고 완전 신뢰를 포함한 어셈블리의 권한 부여 집합과 관계없이 계속 적용됩니다.

투명도는 .NET Framework 버전 2.0에서 새로 추가되었고 보안 모델을 단순화하고 이를 통해 보안 라이브러리 및 애플리케이션을 더 쉽게 배포할 수 있습니다. 투명 코드는 Microsoft Silverlight에서 부분적으로 신뢰할 수 있는 애플리케이션의 배포를 단순화하는 데도 사용됩니다.

> [!NOTE]
> 부분적으로 신뢰할 수 있는 애플리케이션을 개발할 때 대상 호스트에 대한 권한 요구 사항을 알고 있어야 합니다. 일부 호스트에서 허용되지 않는 리소스를 사용하는 애플리케이션을 개발할 수 있습니다. 이 애플리케이션은 오류 없이 컴파일되지만 호스트된 환경으로 로드될 경우 실패합니다. Visual Studio를 사용하여 애플리케이션을 개발한 경우 개발 환경에서 부분 신뢰 또는 제한된 권한 집합으로 디버깅을 사용할 수 있습니다. 자세한 내용은 [방법: 제한된 권한으로 ClickOnce 애플리케이션 디버그](/visualstudio/deployment/how-to-debug-a-clickonce-application-with-restricted-permissions)를 참조하세요. ClickOnce 애플리케이션에 제공된 권한 계산 기능은 부분적으로 신뢰할 수 있는 애플리케이션에도 사용할 수 있습니다.

[맨 위로 이동](#top)

<a name="level"></a>

## <a name="specifying-the-transparency-level"></a>투명도 수준 지정

어셈블리 수준 <xref:System.Security.SecurityRulesAttribute> 특성은 어셈블리가 준수하는 <xref:System.Security.SecurityRuleSet> 규칙을 명시적으로 선택합니다. 규칙은 더 높은 수준이 보안 정책의 더 엄격한 적용을 의미하는 숫자 수준 시스템에서 구성됩니다.

수준은 다음과 같습니다.

- 수준 2 (<xref:System.Security.SecurityRuleSet.Level2>) – .NET Framework 4 투명도 규칙입니다.

- 수준 1(<xref:System.Security.SecurityRuleSet.Level1>)-.NET Framework 2.0 투명도 규칙입니다.

두 투명도 수준 간의 주요 차이점은 수준 1은 어셈블리 외부의 호출에 대해 투명도 규칙을 적용하지 않고 호환성 목적으로만 사용된다는 점입니다.

> [!IMPORTANT]
> 수준 1 투명도는 호환성 목적으로만 지정해야 합니다. 즉, <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 특성을 사용하거나 투명도 모델을 사용하지 않는 .NET Framework 3.5 이하로 개발된 코드에만 수준 1을 지정하세요. 예를 들어 부분적으로 신뢰할 수 있는 호출자(APTCA)의 호출을 허용하는 .NET Framework 2.0 어셈블리에는 수준 1 투명도를 사용합니다. .NET Framework 4 용으로 개발 된 코드의 경우 항상 수준 2 투명도를 사용 합니다.

### <a name="level-2-transparency"></a>수준 2 투명도

수준 2 투명도는 .NET Framework 4에서 도입 되었습니다. 이 모델의 세 가지 개념은 투명 코드, 보안 안전에 중요 코드 및 보안에 중요 코드입니다.

- 투명도 코드는 부여된 권한과 관계없이(완전 신뢰 포함) 다른 투명 코드나 보안 안전에 중요 코드만 호출할 수 있습니다. 부분적으로 신뢰할 수 있는 코드는 도메인의 권한 집합에서 허용되는 작업만 수행할 수 있습니다. 투명 코드는 다음을 수행할 수 없습니다.

  - <xref:System.Security.CodeAccessPermission.Assert%2A> 작업 또는 권한 상승을 수행합니다.

  - 안전하지 않거나 확인할 수 없는 코드를 포함합니다.

  - 중요한 코드를 직접 호출합니다.

  - <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 특성이 포함된 코드나 네이티브 코드를 호출합니다.

  - <xref:System.Security.Permissions.SecurityAction.LinkDemand>로 보호된 멤버를 호출합니다.

  - 중요한 형식에서 상속합니다.

    또한 투명 메서드는 중요한 가상 메서드를 재정의하거나 중요한 인터페이스 메서드를 구현할 수 없습니다.

- 보안 안전에 중요 코드는 완전히 신뢰할 수 있지만 투명 코드를 통해 호출할 수 있습니다. 이 코드는 완전 신뢰 코드의 제한된 노출 영역을 노출합니다. 정확성 및 보안 확인은 안전에 중요 코드에서 수행됩니다.

- 보안에 중요 코드는 모든 코드를 호출할 수 있고 완전히 신뢰할 수 있지만 투명 코드를 통해 호출할 수 없습니다.

### <a name="level-1-transparency"></a>수준 1 투명도

수준 1 투명도 모델은 .NET Framework 버전 2.0에서 새로 추가되었고 이를 통해 개발자가 보안 감사의 대상이 되는 코드 양을 줄일 수 있습니다. 수준 1 투명도는 버전 2.0에서 공개적으로 사용할 수 있지만 주로 Microsoft 내에서 보안 감사 목적으로만 사용됩니다. 개발자는 주석을 통해 보안 상승과 기타 신뢰할 수 있는 작업을 수행할 수 있는(보안에 중요) 형식 및 멤버와 수행할 수 없는(보안 투명) 형식 및 멤버를 선언할 수 있습니다. 투명으로 식별되는 코드에는 엄격한 보안 감사가 필요하지 않습니다. 수준 1 투명도는 투명도 적용이 어셈블리 내로 제한됨을 나타냅니다. 즉, 보안에 중요로 식별되는 모든 public 형식 또는 멤버는 어셈블리 내에서만 보안에 중요합니다. 어셈블리 외부에서 호출될 때 해당 형식과 멤버에 대해 보안을 적용하려면 완전 신뢰에 대한 링크 요청을 사용해야 합니다. 이렇게 하지 않으면 공개적으로 표시되는 보안에 중요 형식 및 멤버는 보안 안전에 중요로 처리되고 부분적으로 신뢰할 수 있는 코드가 어셈블리 외부에서 호출할 수 있습니다.

수준 1 투명성 모델에 다음과 같은 제한이 있습니다.

- public인 보안에 중요 형식 및 멤버는 보안 투명 코드에서 액세스할 수 있습니다.

- 투명도 주석은 어셈블리 내에서만 적용됩니다.

- 보안에 중요 형식 및 멤버는 링크 요청을 사용하여 어셈블리 외부에서 호출하는 작업에 보안을 적용해야 합니다.

- 상속 규칙이 적용되지 않습니다.

- 투명 코드가 완전 신뢰에서 실행될 경우 유해한 작업을 수행할 가능성이 있습니다.

[맨 위로 이동](#top)

<a name="enforcement"></a>

## <a name="transparency-enforcement"></a>투명도 적용

투명도 규칙은 투명도가 계산될 때까지 적용되지 않습니다. 적용 시 투명도 규칙에 위반되면 <xref:System.InvalidOperationException>이 throw됩니다. 투명도 계산 시간은 여러 요소에 따라 다르고 예측할 수 없습니다. 가능한 한 늦게 계산됩니다. .NET Framework 4에서 어셈블리 수준 투명도 계산은 .NET Framework 2.0에서 수행 하는 것 보다 더 빨리 발생 합니다. 투명도 계산은 필요한 시간 이내에 수행됩니다. 이는 메서드가 컴파일되고 해당 메서드에서 오류가 감지되는 시점을 JIT(Just-In-Time ) 컴파일러가 변경하는 방법과 비슷합니다. 코드에 투명도 오류가 없으면 투명도 계산이 표시되지 않습니다.

## <a name="see-also"></a>참고자료

- [보안 투명 코드, 수준 1](security-transparent-code-level-1.md)
- [보안 투명 코드, 수준 2](security-transparent-code-level-2.md)
