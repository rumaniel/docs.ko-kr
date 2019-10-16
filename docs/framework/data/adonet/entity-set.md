---
title: 엔터티 집합
ms.date: 03/30/2017
ms.assetid: 59ec6ab0-88e5-4d25-b112-7a4eccbe61f0
ms.openlocfilehash: b74d6bf373925ac90a998e2c4425c053e533f82a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783997"
---
# <a name="entity-set"></a>엔터티 집합
엔터티 *집합* 은 엔터티 [형식](entity-type.md) 및 해당 엔터티 형식에서 파생 된 형식의 인스턴스에 대 한 논리적 컨테이너입니다. 파생 형식에 대 한 자세한 내용은 엔터티 데이터 모델 [를 참조 하세요. 상속](entity-data-model-inheritance.md).) 엔터티 형식과 엔터티 집합 간의 관계는 관계형 데이터베이스의 행과 테이블 간의 관계와 유사 합니다. 행과 마찬가지로 엔터티 형식은 데이터 구조를 설명 하 고 테이블 처럼 엔터티 집합에는 지정 된 구조체의 인스턴스가 포함 됩니다. 엔터티 집합은 데이터 모델링 구문이 아니며 데이터 구조를 설명하지 않습니다. 대신 엔터티 집합은 엔터티 형식 인스턴스를 그룹화하여 데이터 스토리지에 매핑할 수 있도록 호스팅 또는 스토리지 환경(예: 공용 언어 런타임 또는 SQL Server 데이터베이스)에 대한 구문을 제공합니다.  
  
 엔터티 집합은 엔터티 집합 및 [연결 집합](association-set.md)의 논리적 그룹인 엔터티 [컨테이너](entity-container.md)내에서 정의 됩니다.  
  
 엔터티 형식 인스턴스가 엔터티 집합에 있으려면 다음 조건을 충족해야 합니다.  
  
- 인스턴스 형식이 엔터티 집합의 기반이 되는 엔터티 형식과 같거나 인스턴스 형식이 엔터티 형식의 하위 형식입니다.  
  
- 인스턴스의 [엔터티 키는](entity-key.md) 엔터티 집합 내에서 고유 합니다.  
  
- 인스턴스가 다른 엔터티 집합에 없습니다.  
  
    > [!NOTE]
    > 같은 엔터티 형식을 사용하여 여러 엔터티 집합을 정의할 수 있지만 지정된 엔터티 형식의 인스턴스는 하나의 엔터티 집합에만 있을 수 있습니다.  
  
 개념적 모델의 각 엔터티 형식에 대해 엔터티 집합을 정의할 필요는 없습니다.  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 세 가지 엔터티 형식 `Book`, `Publisher` 및 `Author`가 포함된 개념적 모델을 보여 줍니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/entity-set/example-model-three-entity-types.gif)  
  
 다음 다이어그램에서는 위에 표시된 개념적 모델을 기반으로 하여 엔터티 집합 두 개(`Books` 및 `Publishers`)와 연결 집합(`PublishedBy`)을 보여 줍니다. `Books` 엔터티 집합의 Bi는 런타임에 `Book` 엔터티 형식의 인스턴스를 나타냅니다. 마찬가지로 Pj는 `Publishers` 엔터티 집합 `Publisher` 의 인스턴스를 나타냅니다. Bipj는 `PublishedBy` `PublishedBy` 연결 집합에서 연결의 인스턴스를 나타냅니다.  
  
 ![집합 예제를 보여 주는 스크린샷](./media/entity-set/sets-example-association.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위에 표시된 개념적 모델의 각 엔터티 형식에 대해 하나의 엔터티 집합이 있는 엔터티 컨테이너를 정의합니다. 각 엔터티 집합의 이름과 엔터티 형식은 XML 특성을 사용하여 정의됩니다.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 형식당 여러 엔터티 집합(MEST)을 정의할 수 있습니다. 다음 CSDL에서는 `Book` 엔터티 형식에 대한 두 개의 엔터티 집합이 있는 엔터티 컨테이너를 정의합니다.  
  
 [!code-xml[EDM_Example_Model#MESTExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#mestexample)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
