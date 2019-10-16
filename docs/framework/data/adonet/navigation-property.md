---
title: 탐색 속성-ADO.NET
ms.date: 03/30/2017
ms.assetid: d0bf1a6a-1d84-484c-b7c3-b410fd8dc0b1
ms.openlocfilehash: b57ecf9329aa9ea8afc07507613c9e3961bfd0a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61772260"
---
# <a name="navigation-property"></a>탐색 속성

*탐색 속성* 은 선택적 속성에는 [엔터티 형식](entity-type.md) 탐색에 허용 되는 [끝](association-end.md) 의 [연결](association-type.md) 를 다른 끝입니다. 달리 [속성](property.md), 탐색 속성 데이터를 전달 하지 않습니다.

탐색 속성 정의에는 다음 정보가 들어 있습니다.

- 이름 (필수)

- 탐색하는 연결 (필수)

- 탐색하는 연결의 End (필수)

탐색 속성은 연결의 양쪽 End에 있는 엔터티 형식 모두에 대해 선택적 요소입니다. 연결의 End에 있는 한 엔터티 형식에 대해 탐색 속성을 정의하는 경우 연결의 다른 End에 있는 엔터티 형식에 대해서는 탐색 속성을 정의할 필요가 없습니다.

탐색 속성의 데이터 형식에서 결정 됩니다 합니다 [복합성](association-end-multiplicity.md) 해당 원격 [연결 end](association-end.md)합니다. 예를 들어, `OrdersNavProp` 탐색 속성이 `Customer` 엔터티 형식에 존재하며 `Customer`와 `Order` 간의 일대다 연결을 탐색한다고 가정합니다. 탐색 속성에 대 한 원격 연결 end의 다중성이 many 있으므로 (\*), 해당 데이터 형식이 컬렉션이 (의 `Order`). 마찬가지로 `CustomerNavProp` 탐색 속성이 `Order` 엔터티 형식에 존재하는 경우 원격 End의 복합성이 한 개(1)이므로 해당 데이터 형식은 `Customer`가 됩니다.

## <a name="example"></a>예제

다음 다이어그램에서는 세 가지 엔터티 형식 `Book`, `Publisher` 및 `Author`가 포함된 개념적 모델을 보여 줍니다. 탐색 속성 `Publisher` 및 `Authors`는 Book 엔터티 형식에 정의됩니다. 탐색 속성 `Books`는 Publisher 엔터티 형식과 `Author` 엔터티 형식에 모두 정의됩니다.

 ![세 가지 엔터티 형식을 사용 하 여 개념적 모델을 보여 주는 다이어그램입니다.](./media/navigation-property/conceptual-model-entity-types-associations.gif)  

합니다 [ADO.NET Entity Framework](./ef/index.md) 개념 스키마 정의 언어를 호출 하는 도메인 특정 언어 (DSL)를 사용 하 여 ([CSDL](./ef/language-reference/csdl-specification.md)) 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `Book` 엔터티 형식을 정의합니다.

[!code-xml[EDM_Example_Model#EntityExample](~/samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]

XML 특성 탐색 속성을 정의 하는 데 필요한 정보를 통신에 사용 되는 note: 특성 `Name` 속성의 이름을 포함 `Relationship` 탐색, 연결의 이름을 포함 하 고 `FromRole` 및 `ToRole` 연결의 end를 포함 합니다.

## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
- [관계, 탐색 속성 및 외래 키](/ef/ef6/fundamentals/relationships)
