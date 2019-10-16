---
title: 엔터티 키
ms.date: 03/30/2017
ms.assetid: 0d447a6d-fa7a-4db0-8e7a-fd45e385fca0
ms.openlocfilehash: db867b3a853bd29f1faf1be2faf77776e48be2d2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795134"
---
# <a name="entity-key"></a>엔터티 키
*엔터티 키* 는 id를 확인 하는 데 사용 되는 [엔터티 형식의](entity-type.md) [속성 또는 속성](property.md) 집합입니다. 엔터티 키를 구성하는 속성은 디자인 타임에 선택됩니다. 엔터티 키 속성의 값은 런타임에 [엔터티 집합](entity-set.md) 내에서 엔터티 형식 인스턴스를 고유 하 게 식별 해야 합니다. 엔터티 키를 구성하는 속성을 선택하여 엔터티 집합에서 인스턴스의 고유성을 보장해야 합니다.  
  
 다음은 속성 집합이 엔터티 키가 되기 위한 요구 사항입니다.  
  
- 엔터티 집합 내의 두 엔터티 키는 같지 않아야 합니다. 즉, 엔터티 집합 내의 두 엔터티에서 키를 구성하는 모든 속성 값은 달라야 합니다. 그러나 엔터티 키를 구성하는 일부 값은 같을 수 있습니다.  
  
- 엔터티 키는 null을 허용 하지 않는, 변경할 수 없는 [기본 형식 속성](entity-data-model-primitive-data-types.md)집합으로 구성 되어야 합니다.  
  
- 지정된 엔터티 형식의 엔터티 키를 구성하는 속성은 변경할 수 없습니다. 지정된 엔터티 형식에 사용 가능한 엔터티 키를 여러 개 허용할 수는 없습니다. 서로게이트 키는 지원되지 않습니다.  
  
- 엔터티가 상속 계층 구조에 포함되어 있는 경우 루트 엔터티는 엔터티 키를 구성하는 모든 속성을 포함해야 하며, 루트 엔터티 형식에 엔터티 키를 정의해야 합니다. 자세한 내용은 엔터티 데이터 모델를 참조 [하세요. 상속](entity-data-model-inheritance.md).  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 세 가지 엔터티 형식 `Book`, `Publisher` 및 `Author`가 포함된 개념적 모델을 보여 줍니다. 엔터티 키를 구성하는 각 엔터티 형식의 속성은 "(키)"로 표시됩니다. `Author` 엔터티 형식에는 두 가지 속성 `Name` 및 `Address`로 구성된 엔터티 키가 있습니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/entity-key/example-model-three-entity-types.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `Book` 엔터티 형식을 정의합니다. 엔터티 키는 엔터티 형식의 `ISBN` 속성을 참조하여 정의됩니다.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 ISBN(International Standard Book Number)은 책을 고유하게 식별하므로 엔터티 키에 대해 `ISBN` 속성을 사용하는 것이 좋습니다.  
  
 다음 CSDL에서는 위의 다이어그램에 표시된 `Author` 엔터티 형식을 정의합니다. 엔터티 키는 두 가지 속성 `Name` 및 `Address`로 구성됩니다.  
  
 [!code-xml[EDM_Example_Model#CompositeKeyExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#compositekeyexample)]  
  
 이름이 같은 두 저자가 같은 주소지에서 거주할 가능성은 없으므로 엔터티 키에 대해 `Name` 및 `Address`를 사용하는 것이 좋습니다. 그러나 이러한 엔터티 키 선택이 엔터티 집합에서의 고유한 엔터티 키를 절대적으로 보장하지는 않습니다. 이 경우에는 저자를 고유하게 식별하는 데 사용할 수 있는 `AuthorId`와 같은 속성을 추가하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
