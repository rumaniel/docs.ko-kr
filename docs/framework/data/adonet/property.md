---
title: 속성
ms.date: 03/30/2017
ms.assetid: a941c53f-fc97-42c2-8832-0fb9f1d55c06
ms.openlocfilehash: 97d934ac581e7b1a923bf77dcf46121782fe8eab
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783182"
---
# <a name="property"></a>속성
*속성* 은 [엔터티 형식](entity-type.md) 및 [복합 형식의](complex-type.md)기본적인 구성 요소입니다. 속성은 엔터티 형식 인스턴스 또는 복합 형식 인스턴스에 포함될 데이터의 모양과 특징을 정의합니다. 개념적 모델의 속성은 클래스에 정의된 속성과 유사합니다. 클래스의 속성이 클래스의 모양을 정의하고 개체에 대한 정보를 전달하는 것과 동일한 방식으로, 개념적 모델의 속성은 엔터티 형식의 모양을 정의하고 엔터티 형식 인스턴스에 대한 정보를 전달합니다.  
  
> [!NOTE]
> 이 항목에서 설명하는 속성은 탐색 속성과는 다릅니다. 자세한 내용은 [탐색 속성](navigation-property.md)을 참조 하세요.  
  
 속성 정의에는 다음 정보가 들어 있습니다.  
  
- 속성 이름 (필수)  
  
- 속성 형식 (필수)  
  
- [패싯](facet.md)집합입니다. (옵션)  
  
 속성에는 기본 데이터(예: 문자열, 정수 또는 부울 값) 또는 구조적 데이터(예: 복합 형식)가 포함될 수 있습니다. 기본 형식인 속성을 스칼라 속성이라고도 합니다. 자세한 내용은 엔터티 데이터 모델를 참조 [하세요. 기본 데이터 형식](entity-data-model-primitive-data-types.md)입니다.  
  
> [!NOTE]
> 복합 형식 자체에 복합 형식인 속성이 있을 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 세 가지 엔터티 형식 `Book`, `Publisher` 및 `Author`가 포함된 개념적 모델을 보여 줍니다. 각 속성의 형식 정보는 다이어그램에 표시되지 않지만 각 엔터티 형식에는 여러 속성이 있습니다. [엔터티 키](entity-key.md) 인 속성은 (키)로 표시 됩니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/property/example-model-three-entity-types.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `Book` 엔터티 형식을 정의하고 XML 특성을 사용하여 각 속성의 형식과 이름을 나타냅니다. 선택적 패싯인 `Nullable`도 XML 특성을 사용하여 정의됩니다.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 다이어그램에 표시된 속성 중 하나는 복합 형식 속성일 수 있습니다. 예를 들어, `Address` 엔터티 형식의 `Publisher` 속성은 `StreetAddress`, `City`, `StateOrProvince`, `Country` 및 `PostalCode`와 같은 여러 스칼라 속성으로 구성된 복합 형식 속성일 수 있습니다. 이러한 복합 형식의 CSDL 표현은 다음과 같습니다.  
  
 [!code-xml[EDM_Example_Model#ComplexTypeExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#complextypeexample)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
