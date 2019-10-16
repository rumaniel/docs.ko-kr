---
title: .NET에 대 한 보안 코딩 지침
ms.date: 06/28/2018
helpviewer_keywords:
- managed wrapper to native code implementation
- secure coding
- reusable components
- library code that exposes protected resources
- code, security
- code security
- secure coding, options
- components [.NET], security
- code security, options
- security-neutral code
- security [.NET], coding guidelines
ms.assetid: 4f882d94-262b-4494-b0a6-ba9ba1f5f177
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b3a8f0dfc1a2b5e09722876b73281ed1d8b6334e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018647"
---
# <a name="secure-coding-guidelines"></a>보안 코딩 지침

정보 기반 보안 및 코드 액세스 보안은 보안 구현을 위한 매우 강력하고 명시적인 메커니즘을 제공합니다. 대부분의 응용 프로그램 코드는.NET에서 구현 하는 인프라를 사용 하기만 하면 됩니다. 경우에 따라, 보안 시스템을 확장하거나 새로운 임시 메서드를 사용하여 빌드되는 추가적인 애플리케이션 관련 보안이 필요합니다.

사용 권한 및 코드의 다른 적용 적용.NET을 사용 하 여, 하지 않도록 되도록 하는 정보에 액세스 하거나 바람직하지 않은 다른 작업을 수행 하는 악성 코드 방지 하기 위해 도용 합니다. 또한 신뢰할 수 있는 코드를 사용하여 예상되는 모든 시나리오에서 보안과 유용성 간의 균형을 맞춰야 합니다.

이 개요에서는 보안 시스템에서 사용하기 위해 코드를 설계하는 여러 가지 방법에 대해 설명합니다.

## <a name="securing-resource-access"></a>리소스 액세스 보안

코드를 설계하고 작성하는 경우, 특히 출처를 알 수 없는 코드를 사용하거나 호출하는 경우 코드에 부여된 리소스 액세스 권한을 보호하고 제한해야 합니다. 따라서 코드의 보안을 유지하도록 다음과 같은 기술을 염두에 둡니다.

- CAS(코드 액세스 보안) 사용 안 함

- 부분적으로 신뢰할 수 있는 코드 사용 안 함

- 사용 하지 않는 합니다 [AllowPartiallyTrustedCaller](xref:System.Security.AllowPartiallyTrustedCallersAttribute) 특성 (APTCA).

- .NET Remoting 사용 안 함

- DCOM(분산 구성 요소 개체 모델) 사용 안 함

- 이진 포맷터 사용 안 함

코드 액세스 보안 및 보안 투명 코드는 부분적으로 신뢰할 수 있는 코드를 사용 하 여 보안 경계로 서 지원 되지 않습니다. 대체 보안 조치를 적용하지 않고 출처를 알 수 없는 코드를 로드 및 실행하지 않는 것이 좋습니다. 대체 보안 조치는 다음과 같습니다.

- 가상화

- AppContainers

- OS(운영 체제) 사용자 및 사용 권한

- Hyper-V 컨테이너

## <a name="security-neutral-code"></a>보안 중립 코드

보안 중립 코드는 보안 시스템에서 명시적인 작업을 수행하는 것이 없습니다. 단순히 코드에 부여되는 권한을 실행합니다. 보호 된 작업 (예: 파일, 네트워킹 및 등을 사용 하 여)와 연결 된 보안 예외를 catch 하지 못하는 응용 프로그램은 처리 되지 않은 예외가 발생할 수 있습니다, 있지만 보안 중립 코드는 여전히 보안 기술의.net .

보안 중립 라이브러리에는 사용자가 파악해야 하는 특징이 있습니다. 파일을 사용 하거나 관리 되지 않는 코드를 호출 하는 API 요소를 제공 하는 라이브러리를 가정 합니다. 코드에 해당 권한이 없으면 설명 된 대로 실행 되지는 않습니다. 하지만 코드에 권한이 있더라도 이 코드를 호출하는 모든 애플리케이션이 작동하려면 동일한 권한이 있어야 합니다. 호출 코드에 올바른 사용 권한이 없는 경우는 <xref:System.Security.SecurityException> 코드 액세스 보안 스택 워크의 결과로 나타납니다.

## <a name="application-code-that-isnt-a-reusable-component"></a>재사용 가능한 구성 되지 않은 응용 프로그램 코드

코드가 다른 코드에서 호출할 수 없습니다 하는 응용 프로그램의 일부 이면 보안은 단순 하며 특수 코딩이 필요 없을 수도 있습니다. 하지만 악성 코드는 해당 코드를 호출할 수 있습니다. 코드 액세스 보안으로 악성 코드가 리소스에 액세스하는 것을 방지할 수 있지만, 이러한 코드는 중요한 정보가 들어 있을 수 있는 필드 또는 속성의 값을 판독할 수 있습니다.

또한 해당 코드가 인터넷 또는 기타 신뢰할 수 없는 소스로부터의 사용자 입력을 허용하는 경우에는 악의적인 입력에 주의해야 합니다.

## <a name="managed-wrapper-to-native-code-implementation"></a>관리 되는 네이티브 코드 구현에 대 한 래퍼

일반적으로 이 시나리오에서는 네이티브 코드에서 관리 코드에 사용 가능하게 하려는 몇 가지 유용한 기능을 구현합니다. 관리되는 래퍼는 플랫폼 호출 또는 COM interop를 사용하여 쉽게 작성할 수 있습니다. 하지만 이 작업을 성공적으로 수행하려면 래퍼 호출자에게 비관리 코드 권한이 있어야 합니다. 기본 정책에 따라 즉, 코드는 인트라넷에서 다운로드 하거나 인터넷은 래퍼와 작동 하지 않습니다.

이러한 래퍼를 사용 하는 모든 응용 프로그램에 대 한 비관리 코드 권한을 부여, 대신 래퍼 코드에만이 권한을 부여 하는 것이 좋습니다. 기본 기능이 리소스를 노출하지 않으며 구현도 안전할 경우에는, 래퍼는 모든 코드가 이를 통해 호출할 수 있도록 해당 권한을 어셜션하기만 하면 됩니다. 리소스가 포함되어 있으면, 보안 코딩은 다음 섹션에 설명된 라이브러리 코드의 경우와 동일해야 합니다. 래퍼는 호출자를 이러한 리소스에 노출할 가능성이 있기 때문에, 네이티브 코드가 안전한지 신중하게 확인해야 하며 이는 래퍼의 책임입니다.

## <a name="library-code-that-exposes-protected-resources"></a>보호 된 리소스를 노출 하는 라이브러리 코드

다음 방법은 가장 강력 하 고 따라서 잠재적으로 위험한 (잘못 수행할 경우) 보안 코딩: 라이브러리의 인터페이스 역할을 적용 하는.NET 클래스 처럼 사용할 수 없는 고, 그렇지는 특정 리소스에 액세스 하기 위해 다른 코드 사용 하는 리소스에 대 한 권한입니다. 리소스를 노출할 경우, 먼저 코드는 리소스에 적절한 권한을 요구해야 합니다(즉, 보안 검사를 수행해야 함). 그런 다음 실제 작업을 수행할 수 있도록 해당 권한을 어설션합니다.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[상태 데이터 보안](securing-state-data.md)|전용 멤버를 보호하는 방법을 설명합니다.|
|[보안 및 사용자 입력](security-and-user-input.md)|사용자 입력을 허용하는 애플리케이션에 대한 보안 문제를 설명합니다.|
|[보안 및 경합 상태](security-and-race-conditions.md)|코드에서 경합 상태를 방지하는 방법을 설명합니다.|
|[보안 및 빠른 코드 생성](security-and-on-the-fly-code-generation.md)|동적 코드를 생성하는 애플리케이션에 대한 보안 문제를 설명합니다.|
|[역할 기반 보안](role-based-security.md)|.NET 역할 기반 보안을 자세히 설명 하 고 코드에서 사용 하는 것에 대 한 지침을 제공 합니다.|
