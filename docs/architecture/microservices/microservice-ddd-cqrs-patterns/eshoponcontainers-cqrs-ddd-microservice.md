---
title: eShopOnContainers의 DDD 마이크로 서비스에서 CQRS 및 CQS 방법 적용
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | eShopOnContainers의 주문 마이크로 서비스에서 CQRS가 구현되는 방식을 이해합니다.
ms.date: 10/08/2018
ms.openlocfilehash: 0380e759595e8a159e89f858a5ced4dacfa4e9b4
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674130"
---
# <a name="apply-cqrs-and-cqs-approaches-in-a-ddd-microservice-in-eshoponcontainers"></a>eShopOnContainers의 DDD 마이크로 서비스에서 CQRS 및 CQS 방법 적용

EShopOnContainers 참조 애플리케이션의 주문 마이크로 서비스 설계는 CQRS 원칙을 기준으로 합니다. 그러나 명령에서 쿼리를 분리하고 두 작업에 동일한 데이터베이스를 사용하는 가장 간단한 방식을 사용합니다.

이러한 패턴의 핵심이자 중요한 점은 쿼리가 idempotent라는 점입니다. 즉, 시스템에 몇 번을 쿼리하던 시스템의 상태가 변하지 않습니다. 다시 말해서 쿼리의 부작용이 없습니다.

따라서 주문 마이크로 서비스에서 동일한 데이터베이스를 사용하더라도 트랜잭션 논리 “쓰기” 도메인 모델과 다른 “읽기” 데이터 모델을 사용할 수 있습니다. 이런 이유로, 간소화된 CQRS 접근 방식입니다.

반면에 트랜잭션과 데이터 업데이트를 트리거하는 명령은 시스템에서 상태를 바꿀 수 있습니다. 명령에서는 복잡성과 끊임없이 변화하는 비즈니스 규칙을 처리하는 데 중의가 필요합니다. DDD 기법을 적용하여 더 나은 모델링 시스템을 갖출 수 있습니다.

이 가이드에서 제시하는 DDD 패턴을 보편적으로 적용해서는 안 됩니다. 여기에는 설계에 제약이 따릅니다. 이러한 제약은 시간에 따른 품질 향상과 같은 장점도 있습니다. 특히 시스템 상태를 수정하는 명령 및 기타 코드에서 그렇습니다. 그러나 이러한 제약은 데이터 읽기 및 쿼리에서 장점보다는 복잡성을 더합니다.

이후의 섹션에서 상세히 다룰 집계가 바로 그러한 패턴입니다. 간략히 말해 집계 패턴에서는 도메인에서의 관계에 따른 결과로 여러 도메인 개체를 단일 단위로 취급합니다. 쿼리에서 이 패턴이 항상 장점만 있는 것은 아닙니다. 쿼리 논리의 복잡성을 높일 수 있습니다. 읽기 전용 쿼리의 경우 여러 개체를 단일 집계로 취급하는 것이 장점이 없습니다. 복잡성만 커집니다.

그림 7-2와 같이 이 가이드는 마이크로 서비스의 트랜잭션/업데이트 영역(즉, 명령에 의해 트리거됨)에서만 DDD 패턴을 사용할 것을 권고합니다. 쿼리는 더 간단한 방식을 따를 수 있고 CQRS 방식에 따라 명령과 구분될 수 있습니다.

"쿼리 측" 구현을 위해 EF Core, AutoMapper 프로젝션 같은 종합 ORM, 저장 프로시저, 뷰, 구체화된 뷰나 마이크로 ORM 등, 여러 방식 중에서 선택할 수 있습니다.

이 가이드와 eShopOnContainers(특히 주문 마이크로 서비스)에서는 [Dapper](https://github.com/StackExchange/dapper-dot-net) 같은 마이크로 ORM을 사용하여 간편한 쿼리를 구현했습니다. 이렇게 하면 부담이 거의 없는 가벼운 프레임워크 덕분에 SQL 문 기반의 모든 쿼리를 구현하여 최고 성능을 낼 수 있습니다.

이 방법을 사용할 때는 엔터티가 SQL 데이터베이스에 지속되는 방식에 영향을 미치는 모든 모델 업데이트에서 Dapper 나 기타 다른 개별(비 EF) 쿼리 방식에서 사용되는 SQL 쿼리에 대한 개별 업데이트도 필요합니다.

## <a name="cqrs-and-ddd-patterns-are-not-top-level-architectures"></a>CQRS 및 DDD 패턴은 최상위 아키텍처가 아닙니다.

CQRS와 대부분의 DDD 패턴(예: DDD 계층 또는 집계가 있는 도메인 모델)은 아키텍처 스타일이 아니라 아키텍처 패턴임을 이해하는 것이 중요합니다. 아키텍처 스타일의 예로는 마이크로 서비스, SOA 및 EDA(이벤트 중심 아키텍처)가 있습니다. 이들은 여러 마이크로 서비스와 같은 여러 구성 요소의 시스템을 설명합니다. CQRS 및 DDD 패턴은 단일 시스템 또는 구성 요소 내 항목을 설명합니다. 이 경우에는 마이크로 서비스 내부의 항목입니다.

서로 다른 DC(경계가 있는 컨텍스트)에는 서로 다른 패턴이 따릅니다. 책임도 다르고 솔루션도 달라지게 됩니다. 동일한 패턴을 모든 곳에 강제할 경우 실패로 이어집니다. CQRS 및 DDD 패턴을 모든 곳에 사용해서는 안 됩니다. 많은 하위 시스템, BC 또는 마이크로 서비스는 더 간단하며 간단한 CRUD 서비스 또는 다른 방식을 통해 더 간편하게 구현될 수 있습니다.

애플리케이션 아키텍처는 하나뿐입니다. 즉 사용자가 설계하는 시스템 아키텍처 또는 엔드투엔드 애플리케이션입니다(예: 마이크로 서비스 아키텍처). 그러나 이 애플리케이션 내에서 경계가 지정된 각각의 컨텍스트나 마이크로 서비스의 설계에서는 아키텍처 패턴 수준에서 자체 절충 및 내부 설계 결정을 반영합니다. CQRS 또는 DDD처럼 동일한 아키텍처 패턴을 모든 곳에 적용해서는 안 됩니다.

### <a name="additional-resources"></a>추가 자료

- **Martin Fowler. CQRS** \
  <https://martinfowler.com/bliki/CQRS.html>

- **Greg Young. CQRS 문서** \
  <https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf>

- **Udi Dahan. 명확한 CQRS** \
  <http://udidahan.com/2009/12/09/clarified-cqrs/>

>[!div class="step-by-step"]
>[이전](apply-simplified-microservice-cqrs-ddd-patterns.md)
>[다음](cqrs-microservice-reads.md)
