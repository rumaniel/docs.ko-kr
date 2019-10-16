---
title: 연결 집합(association set)
ms.date: 03/30/2017
ms.assetid: a65247b6-ce59-44ea-974c-14ae20a7995f
ms.openlocfilehash: 43ab6cf9f1ee8cb971810add6b9a89467726f3e2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785035"
---
# <a name="association-set"></a>연결 집합(association set)
*연결 집합* 은 같은 형식의 [연결](association-type.md) 인스턴스에 대 한 논리적 컨테이너입니다. 연결 집합은 데이터 모델링 구문이 아니므로 데이터 또는 관계의 구조를 설명하지 않습니다. 대신 연결 집합은 연결 인스턴스를 그룹화하여 데이터 스토리지에 매핑할 수 있도록 호스팅 또는 스토리지 환경(예: 공용 언어 런타임 또는 SQL Server 데이터베이스)에 대한 구문을 제공합니다.  
  
 연결 집합은 엔터티 [집합](entity-set.md) 및 연결 집합의 논리적 그룹인 [엔터티 컨테이너](entity-container.md)내에서 정의 됩니다.  
  
 연결 집합 정의에는 다음 정보가 들어 있습니다.  
  
- 연결 집합 이름 (필수)  
  
- 연결 집합에 인스턴스가 포함될 연결 (필수)  
  
- 두 [연결 집합이 끝납니다](association-set-end.md).  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 두 연결 `PublishedBy` 및 `WrittenBy`의 개념적 모델을 보여 줍니다. 연결 집합에 대한 정보는 다이어그램에 표시되지 않지만 다음 다이어그램에서는 이 모델을 기반으로 하여 연결 집합 및 엔터티 집합의 예제를 보여 줍니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/association-set/example-model-three-entity-types.gif)  
  
 다음 예제에서는 위에 표시된 개념적 모델을 기반으로 하여 연결 집합(`PublishedBy`) 및 엔터티 집합 두 개(`Books` 및 `Publishers`)를 보여 줍니다. `Books` 엔터티 집합의 Bi는 런타임에 `Book` 엔터티 형식의 인스턴스를 나타냅니다. 마찬가지로 Pj는 `Publishers` 엔터티 집합 `Publisher` 의 인스턴스를 나타냅니다. Bipj는 `PublishedBy` `PublishedBy` 연결 집합에서 연결의 인스턴스를 나타냅니다.  
  
 ![집합 예제를 보여 주는 스크린샷](./media/association-set/sets-example-association.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 있는 각 연결에 대한 하나의 연결 집합을 사용하여 엔터티 컨테이너를 정의합니다. 각 연결 집합의 이름과 연결은 XML 특성을 사용하여 정의됩니다.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 연결 [집합 end](association-set-end.md)를 공유 하는 두 개의 연결 집합이 없으면 연결 당 여러 연결 집합을 정의할 수 있습니다. 다음 CSDL에서는 `WrittenBy` 연결에 대한 두 개의 연결 집합이 있는 엔터티 컨테이너를 정의합니다. `Book` 및 `Author` 엔터티 형식에 대해 엔터티 집합이 여러 개 정의되었으며 어떤 연결 집합도 연결 집합 End를 공유하지 않습니다.  
  
 [!code-xml[EDM_Example_Model#MultipleAssociationSets](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#multipleassociationsets)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
- [외래 키 속성](foreign-key-property.md)
