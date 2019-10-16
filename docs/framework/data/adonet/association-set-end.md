---
title: 연결 집합 End
ms.date: 03/30/2017
ms.assetid: fe4bf1d3-047a-4a37-98c5-a66e70811346
ms.openlocfilehash: 48ba84d46e380462405551cc2d826d84368b351a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786937"
---
# <a name="association-set-end"></a>연결 집합 End
*연결 집합 end* 는 [연결 집합](association-set.md)의 끝에 있는 [엔터티 형식](entity-type.md) 및 [엔터티 집합](entity-set.md) 을 식별 합니다. 연결 집합 End는 연결 집합의 일부로 정의되고 연결 집합에는 정확히 두 개의 연결 집합 End가 있어야 합니다.  
  
 연결 집합 End 정의에는 다음 정보가 들어 있습니다.  
  
- 연결 집합과 관련된 엔터티 형식 중 하나 (필수)  
  
- 연결 집합과 관련된 엔터티 형식에 대한 엔터티 집합 (필수)  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 두 연결 `WrittenBy` 및 `PublishedBy`의 개념적 모델을 보여 줍니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/association-set-end/example-model-three-entity-types.gif)  
  
 다음 다이어그램에서는 위에 나온 개념적 모델을 기반으로 하여 하나의 연결 집합(`PublishedBy`) 및 두 개의 엔터티 집합(`Books` 및 `Publishers`)을 보여 줍니다. 연결 집합 End는 `Books` 및 `Publishers` 엔터티 집합입니다. `Books` 엔터티 집합의 Bi는 런타임에 `Book` 엔터티 형식의 인스턴스를 나타냅니다. 마찬가지로 Pj는 `Publishers` 엔터티 집합 `Publisher` 의 인스턴스를 나타냅니다. Bipj는 `PublishedBy` `PublishedBy` 연결 집합에서 연결의 인스턴스를 나타냅니다.  
  
 ![집합 예제를 보여 주는 스크린샷](./media/association-set-end/sets-example-association.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 있는 각 연결에 대한 하나의 연결 집합을 사용하여 엔터티 컨테이너를 정의합니다. 연결 집합 End는 각 연결 집합 정의의 일부로 정의되어 있습니다.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
