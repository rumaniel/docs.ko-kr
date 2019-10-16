---
title: 엔터티 형식(entity type)
ms.date: 03/30/2017
ms.assetid: a6dee9ab-9e4a-48f2-a169-3f79cc15821c
ms.openlocfilehash: efd3ea0972148e885d4b22b49040640539bb28cd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795125"
---
# <a name="entity-type"></a>엔터티 형식(entity type)
*엔터티 형식은* EDM (엔터티 데이터 모델)을 사용 하 여 데이터 구조를 설명 하는 기본 구성 요소입니다. 개념적 모델에서 엔터티 형식은 고객이나 주문과 같은 최상위 개념의 구조를 나타냅니다. 엔터티 형식은 엔터티 형식 인스턴스의 템플릿입니다. 각 템플릿에는 다음 정보가 들어 있습니다.  
  
- 고유한 이름 (필수)  
  
- 하나 이상의 속성으로 정의 된 [엔터티 키](entity-key.md) 입니다. (필수)  
  
- [속성](property.md)형식의 데이터입니다. 필요에 따라  
  
- [연결](association-type.md) 의 한 [end](association-end.md) 에서 다른 end로의 탐색을 허용 하는 [탐색 속성](navigation-property.md) 입니다. (옵션)  
  
 애플리케이션에서 엔터티 형식의 인스턴스는 특정 고객 또는 주문과 같은 특정 개체를 나타냅니다. 엔터티 형식의 각 인스턴스에는 [엔터티 집합](entity-set.md)내에 고유한 [엔터티 키](entity-key.md) 가 있어야 합니다.  
  
 두 엔터티 형식 인스턴스는 형식이 동일하고 해당 엔터티 키 값이 동일한 경우에만 동일한 것으로 간주됩니다.  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 세 가지 엔터티 형식 `Book`, `Publisher` 및 `Author`가 포함된 개념적 모델을 보여 줍니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/entity-type/example-model-three-entity-types.gif)  
  
 엔터티 키를 구성하는 각 엔터티 형식의 속성은 "(키)"로 표시됩니다.  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `Book` 엔터티 형식을 정의합니다.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
- [facet](facet.md)
