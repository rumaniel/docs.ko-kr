---
title: '서버리스 앱: 아키텍처, 패턴 및 Azure 구현'
description: 서버를 사용하지 않는 아키텍처에 대한 가이드입니다. 엔터프라이즈 애플리케이션에 대해 서버를 사용하지 않는 아키텍처([IaaS] (Infrastructure as a Service) 또는 [PaaS] (Platform as a Service) 대신)를 구현하는 시기, 이유 및 방법을 알아봅니다.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 148a79e39c047897719e4f97efd84676b1b92636
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70294930"
---
# <a name="serverless-apps-architecture-patterns-and-azure-implementation"></a>서버리스 앱: 아키텍처, 패턴 및 Azure 구현

![서버리스 앱 eBook 표지를 보여주는 스크린샷.](./media/index/serverless-apps-cover.jpg)

> 다운로드 위치: <https://aka.ms/serverless-ebook>

게시자:

Microsoft 개발자 사업부, .NET 및 Visual Studio 제품 팀

Microsoft Corporation의 사업부

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2018 by Microsoft Corporation

All rights reserved. 이 가이드의 내용 중 어떤 부분도 게시자의 서면 허가 없이는 어떠한 형식이나 방법으로도 복제하거나 전송할 수 없습니다.

이 가이드는 작성자의 견해와 의견을 "있는 그대로" 제공하고 전달합니다. URL 및 기타 인터넷 웹 사이트 참조를 비롯하여 이 가이드에 제공된 견해, 의견 및 정보는 예고 없이 변경될 수 있습니다.

여기에 설명된 일부 예제는 예시 용도로만 제공되며 실제 데이터가 아닙니다. 실제로 연관시키거나 관련시키려고 의도하거나 추론해서는 안 됩니다.

"상표" 웹 페이지의 <https://www.microsoft.com>에 나열된 Microsoft 및 상표는 Microsoft 그룹 계열사의 상표입니다.

Mac 및 macOS는 Apple Inc.의 상표입니다.

기타 모든 표시와 로고는 해당 소유자의 자산입니다.

만든 이:

> **[Jeremy Likness](https://twitter.com/jeremylikness)** , Sr. Cloud Developer Advocate, APEX, Microsoft Corp.

기여자:

> **[Cecil Phillip](https://twitter.com/cecilphillip)** , Cloud Developer Advocate II, APEX, Microsoft Corp.

편집자:

> **[Bill Wagner](https://twitter.com/billwagner)** , Senior Content Developer, APEX, Microsoft Corp.

> **[Maira Wenzel](https://twitter.com/mairacw)** , Senior Content Developer, APEX, Microsoft Corp.

참가자 및 검토자:

> **[Steve Smith](https://twitter.com/ardalis)** , Owner, Ardalis Services.

## <a name="introduction"></a>소개

[서버리스](https://azure.microsoft.com/solutions/serverless/) 기능은 순수 클라우드 네이티브 코드의 흐름에서 클라우드 플랫폼이 진화한 결과입니다. 서버를 사용하지 않는 기능은 인프라 문제와 격리하는 동안 개발자에게 비즈니스 논리를 제공합니다. "서버 없음"이 아닌 "적은 서버"를 의미하는 패턴입니다. 서버를 사용하지 않는 코드는 이벤트 기반입니다. 코드는 타이머에 대한 기존 HTTP 웹 요청 또는 파일을 업로드하는 결과로 인해 트리거될 수 있습니다. 서버를 사용하지 않는 인프라를 사용하면 인스턴트 규모가 탄력적 요구 사항을 충족하고 실제로 "사용한 만큼 지불"하는 마이크로 청구를 제공할 수 있습니다. 서버를 사용하지 않는 기능은 애플리케이션을 빌드하는 새로운 사고 및 접근법으로 모든 문제에 적합한 솔루션입니다. 개발자가 다음을 결정해야 합니다.

* 서버를 사용하지 않는 장단점은 무엇인가요?
* 자신의 애플리케이션에 대해 서버를 사용하지 않도록 해야 하는 이유는 무엇인가요?
* 서버를 사용하지 않는 코드를 빌드하고, 테스트하고, 배포하고, 유지 관리하려면 어떻게 하나요?
* 기존 애플리케이션에서 서버를 사용하지 않도록 코드를 마이그레이션하는 것이 좋은 경우 및 이 변환을 수행하기 가장 좋은 방법은 무엇인가요?

## <a name="about-this-guide"></a>이 가이드의 내용

이 가이드는 서버를 사용하지 않는 애플리케이션의 클라우드 네이티브 개발에 중점을 둡니다. 책은 이점을 강조 표시하고 서버를 사용하지 않는 앱을 개발하는 잠재적인 단점을 노출하고, 서버를 사용하지 않는 아키텍처의 설문 조사를 제공합니다. 서버를 사용하지 않는 방법의 많은 예제는 다양한 서버를 사용하지 않는 디자인 패턴와 함께 설명되어 있습니다.

이 가이드는 Azure 서버를 사용하지 않는 플랫폼의 구성 요소를 설명하고 [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)를 사용하여 서버를 사용하지 않는 구현에 특별히 중점을 둡니다. 지속 가능한 함수를 사용하는 상태에 따라 달라지는 서버를 사용하지 않는 앱을 구현하는 방법뿐만 아니라 트리거 및 바인딩에 대해 알아봅니다. 마지막으로 비즈니스 예제 및 사례 연구를 통해 서버를 사용하지 않는 것이 프로젝트에 대해 올바른 접근법인지 결정하기 위한 참조의 컨텍스트 및 프레임을 제공하는 데 도움이 됩니다.

## <a name="evolution-of-cloud-platforms"></a>클라우드 플랫폼의 진화

서버를 사용하지 않는 기능은 반복된 여러 클라우드 플랫폼의 정점입니다. 이러한 진화는 데이터 센터에서 물리적 메탈을 시작하고 IaaS(Infrastructure as a Service) 및 PaaS(Platform as a Service)를 통해 진행되었습니다.

![온-프레미스에서 서버를 사용하지 않도록 진화](./media/serverless-evolution-iaas-paas.png)

클라우드 이전에 개발과 운영 간에 뚜렷한 경계가 존재했습니다. 애플리케이션을 배포하는 작업은 다음과 같은 무수한 질문에 대답하는 것을 의미합니다.

* 어떤 하드웨어를 설치해야 하나요?
* 보호된 머신에 대한 물리적 액세스는 어떻게 되나요?
* 데이터 센터에는 UPS(무정전 전원 공급 장치)가 필요한가요?
* 스토리지 백업을 어디에 보내나요?
* 중복된 전원이 있어야 하나요?

질문이 계속되면 오버헤드가 많았습니다. 대부분의 경우에 IT 부서는 지나친 낭비를 처리하도록 적용되었습니다. 낭비는 스케일 아웃을 사용하기 위해 재해 복구 및 대기 서버에 대한 백업 머신으로 서버를 과도하게 할당하여 발생했습니다. 다행스럽게도 VM(Virtual Machines)에서 가상화 기술(예: [Hyper-V](/virtualization/hyper-v-on-windows/about/))이 도입되면 IaaS(Infrastructure as a Service)가 증가합니다. 가상화된 인프라를 사용하면 작업이 서버의 표준 집합을 백본으로 설정할 수 있으므로 고유한 "주문형" 서버를 프로비전할 수 있는 유연한 환경이 생성되었습니다. 또한 가상화를 통해 가상 머신 "as a service"를 제공하기 위해 클라우드를 사용하는 단계를 설정했습니다. 회사는 비즈니스에서 중복 전원 또는 물리적 머신을 걱정하지 않게 될 수 있었습니다. 대신 가상 환경에 초점을 두었습니다.

작업이 다양한 작업을 처리해야 하기 때문에 IaaS에는 과도한 오버헤드가 필요합니다. 필수 구성 요소 작업을 완료해야 합니다.

* 서버 패치 및 백업
* 패키지 설치
* 운영 체제를 최신 상태로 유지
* 애플리케이션 모니터링

다음 진화는 PaaS(Platform as a Service)를 제공하여 오버헤드를 감소시킵니다. PaaS에서 클라우드 공급자는 운영 체제, 보안 패치 및 특정 플랫폼을 지원하는 데 필요한 패키지도 처리합니다. VM을 빌드한 다음, .NET Framework를 구성하고 IIS(인터넷 정보 서비스) 서버를 준비하는 대신 개발자는 단순히 "웹 애플리케이션" 또는 "API 엔드포인트"와 같은 "플랫폼 대상"을 선택하고 코드를 직접 배포합니다. 인프라 질문은 다음으로 감소됩니다.

* 어떤 크기 서비스가 필요한가요?
* 서비스 규모를 확장하려면 어떻게 하나요(서버 또는 노드 추가)?
* 서비스를 강화하려면 어떻게 하나요(호스팅 서버 또는 노드의 용량 증가)?

추가로 서버를 사용하지 않으면 이벤트 기반 코드에 집중하여 서버를 추상화합니다. 플랫폼 대신 개발자는 하나의 작업을 수행하는 마이크로 서비스에 집중할 수 있습니다. 서버를 사용하지 않는 코드를 빌드하기 위한 두 가지 주요 질문은 다음과 같습니다.

* 코드를 트리거하는 것은 무엇인가요?
* 코드에서 수행하는 작업은 무엇인가요?

서버를 사용하지 않고 인프라가 추상화됩니다. 경우에 따라 개발자는 더 이상 호스트에 대해 우려하지 않습니다. IIS, Kestrel, Apache 또는 일부 기타 웹 서버 인스턴스가 실행되어 웹 요청을 관리하는지 여부에 관계 없이 개발자는 HTTP 트리거에 중점을 둡니다. 트리거는 요청에 대한 표준 플랫폼 간 페이로드를 제공합니다. 페이로드는 개발 프로세스를 간소화할 뿐만 아니라 경우에 따라 테스트를 용이하게 하고 플랫폼에서 코드를 쉽게 이식 가능하게 합니다.

서버를 사용하지 않는 다른 기능은 마이크로 청구입니다. Web API 엔드포인트를 호스트하는 웹 애플리케이션에 대해 일반적입니다. 기존 베어 메탈, IaaS 및 PaaS 구현에서도 API를 호스팅하는 리소스는 지속적으로 요금이 지불됩니다. 즉, 액세스 중이 아닌 경우에도 엔드포인트를 호스트하는 비용을 지불합니다. 다른 항목에 비해 특정 API가 빈번히 호출되기도 합니다. 따라서 널리 사용되는 엔드포인트를 지원하는 방법에 따라 전체 시스템의 크기를 조정합니다. 서버를 사용하지 않으면 각 엔드포인트의 규모를 독립적으로 조정하고 사용량에 대한 요금을 지불할 수 있습니다. 따라서 API가 호출되지 않는 경우 비용이 발생하지 않습니다. 마이그레이션은 엔드포인트를 지원하는 지속적인 비용을 대부분 크게 줄일 수 있습니다.

## <a name="what-this-guide-doesnt-cover"></a>이 가이드에서 다루지 않는 내용

이 가이드에서는 특별히 아키텍처 접근법 및 디자인 패턴을 강조하지만 Azure Functions, [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps) 또는 다른 서버를 사용하지 않는 플랫폼의 구현 세부 정보에 대한 심층 분석이 아닙니다. 예를 들어, 이 가이드에서는 CORS(Cross-Origin Resource Sharing)를 구성하거나, 사용자 지정 도메인을 적용하거나, SSL 인증서를 업로드하는 등 Logic Apps 또는 Azure Functions의 기능을 사용하는 고급 워크플로를 다루지 않습니다. 이러한 세부 정보는 온라인 [Azure Functions 설명서](https://docs.microsoft.com/azure/azure-functions/functions-reference)를 통해 사용할 수 있습니다.

### <a name="additional-resources"></a>추가 자료

* [Azure 아키텍처 센터](https://docs.microsoft.com/azure/architecture/)
* [클라우드 애플리케이션의 모범 사례](https://docs.microsoft.com/azure/architecture/best-practices/api-design)

## <a name="who-should-use-the-guide"></a>가이드의 대상 사용자

이 가이드는 온-프레미스나 클라우드에서 서버를 사용하지 않는 구성 요소를 사용할 수 있는 .NET을 사용하여 엔터프라이즈 애플리케이션을 빌드하려는 개발자와 솔루션 설계자를 위해 작성되었습니다. 다음에 관심이 있는 개발자, 설계자 및 기술 의사 결정권자에게 유용합니다.

* 서버를 사용하지 않는 개발의 장단점 이해
* 서버를 사용하지 않는 아키텍처 접근 방법 알아보기
* 서버를 사용하지 않는 앱의 구현 예제

## <a name="how-to-use-the-guide"></a>가이드를 사용하는 방법

이 가이드의 첫 번째 부분에서는 여러 다른 아키텍처 접근법을 비교하여 서버를 사용하지 않는 기능이 바람직한 옵션인 이유를 검사합니다. 소프트웨어 개발의 모든 측면이 아키텍처 결정에 의해 영향을 받기 때문에 기술 및 개발 수명 주기를 모두 검사합니다. 그런 다음, 이 가이드에서는 사용 사례 및 디자인 패턴을 검사하고 Azure Functions를 사용하는 참조 구현이 포함되어 있습니다. 각 섹션에는 특정 영역에 대해 자세히 알아보는 추가 리소스가 포함됩니다. 이 가이드에는 서버를 사용하지 않는 구현의 연습 및 실습 탐색에 대한 리소스가 포함되어 있습니다.

## <a name="send-your-feedback"></a>피드백 보내기

가이드 및 관련 샘플은 지속적으로 진화합니다. 여러분의 피드백을 기다리고 있습니다! 이 가이드를 향상시킬 수 있는 방법에 대한 주석이 있으면 [GitHub 문제](https://github.com/dotnet/docs/issues)에 빌드된 페이지의 맨 아래에서 피드백 섹션을 사용합니다.

>[!div class="step-by-step"]
>[다음](architecture-approaches.md)
