---
title: 마이크로 서비스에서 간소화된 CQRS 및 DDD 패턴 적용
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | CQRS 및 DDD 간의 전반적인 관계를 이해합니다.
ms.date: 10/08/2018
ms.openlocfilehash: f42b553fd30fdffdc6e325b11740fe9162aab7c8
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834309"
---
# <a name="apply-simplified-cqrs-and-ddd-patterns-in-a-microservice"></a>마이크로 서비스에서 간소화된 CQRS 및 DDD 패턴 적용

CQRS는 데이터를 읽고 쓰기 위해 모델을 구분하는 아키텍처 패턴입니다. 관련 용어 [CQS(명령 쿼리 분리)](https://martinfowler.com/bliki/CommandQuerySeparation.html)는 원래 Bertrand Meyer가 작성한 책 *개체 지향 소프트웨어 생성*에서 정의되었습니다. 기본 개념은 시스템의 작업을 완벽히 분리된 두 가지 범주로 나눌 수 있다는 것입니다.

- 쿼리 결과를 반환하고 시스템의 상태를 변경하지 않으며 부작용이 없습니다.

- 명령 시스템의 상태를 변경합니다.

CQS는 간단한 개념으로 쿼리 또는 명령인 동일한 개체 내의 메서드에 대한 내용입니다. 각 메서드는 상태를 반환하거나 상태를 변경하는 작업 중 하나를 수행합니다. 단일 리포지토리 패턴 개체도 CQS를 따를 수 있습니다. CQS는 CQRS에 대한 기본 원칙으로 간주할 수 있습니다.

[CQRS(명령 및 쿼리 책임 분리)](https://martinfowler.com/bliki/CQRS.html)는 Greg Young이 소개하고 Udi Dahan 및 다른 사용자가 전적으로 지원했습니다. CQS 원칙에 기반하지만 보다 자세히 설명됩니다. 명령 및 이벤트, 필요에 따라 비동기 메시지에 따라 패턴이라고 간주할 수 있습니다. 대부분의 경우 CQRS는 쓰기(업데이트)보다 읽기(쿼리)를 위해 다양한 물리적 데이터베이스를 보유하는 등 고급 시나리오와 관련됩니다. 또한 현재 상태 데이터를 저장하는 대신 도메인 모델에 이벤트만을 저장하도록 더 진화된 CQRS 시스템은 업데이트 데이터베이스에 [ES(이벤트 소싱)](https://martinfowler.com/eaaDev/EventSourcing.html)을 구현할 수 있습니다. 그러나 이것은 이 가이드에서 사용한 접근 방법이 아닙니다. 명령에서 쿼리를 분리하는 작업으로 구성된 단순한 CQRS 접근 방법을 사용하고 있습니다.

CQRS의 분리 양상은 한 계층의 쿼리 작업 및 또 다른 계층의 명령을 그룹화하여 수행됩니다. 각 계층에는 고유한 데이터 모델(모델은 다른 데이터베이스가 아닐 수 있음)이 있고 패턴 및 기술을 고유하게 조합하여 빌드됩니다. 무엇보다도 두 계층은 이 가이드에 사용된 예제(마이크로 서비스 순서)처럼 동일한 계층 또는 마이크로 서비스 내에 있을 수 있습니다. 또는 서로 영향을 주지 않고 개별적으로 확장할 수 있도록 다른 마이크로 서비스 또는 프로세스에서 구현될 수 있습니다.

CQRS에는 읽기/쓰기 작업에 대해 두 개의 개체가 있습니다. 여기서 다른 컨텍스트에는 하나의 개체만 있습니다. 비정규화된 읽기 데이터베이스가 있어야 하는 이유가 있으며 추가 고급 CQRS 문헌에 대해 알아볼 수 있습니다. 하지만 여기서는 접근 방법을 ֲ사용하지 않으며 집계와 같은 DDD 패턴에서 제약 조건을 사용하여 쿼리를 제한하는 대신 쿼리를 유연하게 만드는 것이 목적입니다.

이러한 종류의 서비스 예로 eShopOnContainers 참조 애플리케이션에서 마이크로 서비스 정렬이 있습니다. 이 서비스는 간소화된 CQRS 접근 방식에 따라 마이크로 서비스를 구현합니다. 그림 7-2와 같이 단일 데이터 원본 또는 데이터베이스를 사용하지만 패턴 트랜잭션 도메인에 대한 두 가지 논리 모델과 DDD를 사용하지 않습니다.

![높은 수준의 간소화된 CQRS 및 DDD 마이크로 서비스를 보여 주는 다이어그램입니다.](./media/apply-simplified-microservice-cqrs-ddd-patterns/simplified-cqrs-ddd-microservice.png)

**그림 7-2**. 간소화된 CQRS 및 DDD 기반 마이크로 서비스

논리 ‘주문’ 마이크로 서비스에는 주문 데이터베이스가 포함되어 있으며 동일한 Docker 호스트에 위치할 수 있지만 반드시 그런 것은 아닙니다. 프로덕션이 아닌 개발의 경우에 동일한 Docker 호스트에 데이터베이스를 포함하는 것이 좋습니다.

애플리케이션 계층은 Web API 자체일 수 있습니다. 여기서 중요한 디자인 측면은 마이크로 서비스가 CQRS 패턴을 따라 명령, 도메인 모델 및 트랜잭션에서 쿼리 및 ViewModels(특히 클라이언트 애플리케이션에 생성된 데이터 모델)을 분할한다는 점입니다. 이 방법은 뒤의 섹션에 설명된 대로 트랜잭션 및 업데이트에 대해서만 의미가 있는 DDD 패턴에서 들어오는 제한 사항 및 제약 조건과 독립된 쿼리를 유지합니다.

## <a name="additional-resources"></a>추가 자료

- **Greg Young. 이벤트 소스 시스템에서 버전 관리**(무료로 온라인 eBook 읽기) \
   <https://leanpub.com/esversioning/read>

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](eshoponcontainers-cqrs-ddd-microservice.md)
