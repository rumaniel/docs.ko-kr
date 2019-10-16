---
title: DDD 및 CQRS 패턴을 사용하여 마이크로 서비스에서 비즈니스 복잡성 처리
description: 컨테이너화된 .NET 애플리케이션을 위한 .NET 마이크로 서비스 아키텍처 | DDD 및 CQRS 패턴을 적용하여 복잡한 비즈니스 시나리오를 처리하는 방법 이해
ms.date: 10/08/2018
ms.openlocfilehash: d311641e2ac73205c04c3f1147b54991585ce851
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295104"
---
# <a name="tackle-business-complexity-in-a-microservice-with-ddd-and-cqrs-patterns"></a>DDD 및 CQRS 패턴을 사용하여 마이크로 서비스에서 비즈니스 복잡성 처리

*비즈니스 도메인에 대한 이해를 반영하는 각 마이크로 서비스 또는 제한된 컨텍스트를 위한 도메인 모델을 디자인하세요.*

이 섹션에서는 복잡한 하위 시스템 또는 끊임없이 변화하는 비즈니스 규칙을 사용하는 도메인 전문가의 지식에서 파생된 마이크로 서비스를 처리해야 할 때 구현하는 고급 마이크로 서비스에 중점을 둡니다. 이 섹션에서 사용된 아키텍처 패턴은 그림 7-1에 나와 있는 것처럼 DDD(도메인 기반 디자인) 및 CQRS(명령과 쿼리의 역할 분리) 접근 방식을 기반으로 합니다.

![마이크로 서비스 패턴, API 게이트웨이, 복원력 있는 통신, 게시자/구독자 등의 외부 아키텍처와 데이터 기반/CRUD, DDD 패턴, 종속성 삽입, 여러 라이브러리 등의 내부 아키텍처 간 차이입니다.](./media/image1.png)

**그림 7-1**. 각 마이크로 서비스에 대한 외부 마이크로 서비스 아키텍처 및 내부 아키텍처 패턴

그러나 ASP.NET Core Web API 서비스를 구현하는 방법 또는 Swashbuckle 또는 NSwag를 사용하여 Swagger 메타데이터를 표시하는 방법과 같은 대부분의 데이터 기반 마이크로 서비스 기술은 DDD 패턴을 사용하여 내부적으로 구현된 고급 마이크로 서비스에도 적용할 수 있습니다. 이 섹션은 이전 섹션의 확장입니다. 이전에 설명한 대부분의 방법이 여기 또는 모든 종류의 마이크로 서비스에도 적용되기 때문입니다.

이 섹션에서는 먼저 eShopOnContainers 참조 애플리케이션에 사용되는 간소화된 CQRS 패턴에 대한 세부 정보를 제공합니다. 이후에는 애플리케이션에서 다시 사용할 수 있는 일반적인 패턴을 찾을 수 있도록 지원하는 DDD 기술에 대해 간략히 설명합니다.

DDD는 다양한 학습 리소스 집합이 있는 큰 주제입니다. Eric Evans의 [Domain-Driven Design](https://domainlanguage.com/ddd/)과 같은 서적 및 Vaughn Vernon, Jimmy Nilsson, Greg Young, Udi Dahan, Jimmy Bogard와 그 밖의 여러 DDD/CQRS 전문가의 추가 자료로 시작할 수 있습니다. 그러나 무엇보다도 구체적인 비즈니스 도메인 전문가와 함께 하는 대화, 화이트 보드 및 도메인 모델링 세션에서 DDD 기술을 적용하는 방법을 알아보려고 노력해야 합니다.

#### <a name="additional-resources"></a>추가 자료

##### <a name="ddd-domain-driven-design"></a>DDD(도메인 기반 디자인)

- **Eric Evans. 도메인 언어** \
  <https://domainlanguage.com/>

- **Martin Fowler. 도메인 기반 디자인** \
  <https://martinfowler.com/tags/domain%20driven%20design.html>

- **Jimmy Bogard. 도메인 강화: 입문** \
  <https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/>

##### <a name="ddd-books"></a>DDD 서적

- **Eric Evans. 도메인 기반 디자인: 소프트웨어 핵심에서 복잡성 처리** \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- **Eric Evans. 도메인 기반 디자인 참조: 정의 및 패턴 요약** \
  <https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/>

- **Vaughn Vernon. 도메인 기반 디자인 구현** \
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- **Vaughn Vernon. 도메인 기반 디자인 핵심 정리** \
  <https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/>

- **Jimmy Nilsson. 도메인 기반 디자인 및 패턴 적용** \
  <https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/>

- **Cesar de la Torre. .NET을 사용한 N-레이어 도메인 지향 아키텍처 가이드** \
  <https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/>

- **Abel Avram 및 Floyd Marinescu. 신속한 도메인 기반 디자인** \
  <https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/>

- **Scott Millett, Nick Tune - 도메인 기반 디자인의 패턴, 원칙 및 사례** \
  <http://www.wrox.com/WileyCDA/WroxTitle/Patterns-Principles-and-Practices-of-Domain-Driven-Design.productCd-1118714709.html>

##### <a name="ddd-training"></a>DDD 교육

- **Julie Lerman 및 Steve Smith. 도메인 기반 디자인 기본 사항** \
  <https://bit.ly/PS-DDD>

>[!div class="step-by-step"]
>[이전](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md)
>[다음](apply-simplified-microservice-cqrs-ddd-patterns.md)
