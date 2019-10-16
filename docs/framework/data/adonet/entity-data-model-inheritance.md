---
title: '엔터티 데이터 모델: 상속'
ms.date: 03/30/2017
ms.assetid: 42c7ef24-710a-4af9-8493-cd41c399ecb0
ms.openlocfilehash: 21dbdff63c07dbcdac8de7bf4b3a8e5d0ece7901
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784075"
---
# <a name="entity-data-model-inheritance"></a>엔터티 데이터 모델: 상속
EDM (엔터티 데이터 모델)은 [엔터티 형식](entity-type.md)에 대 한 상속을 지원 합니다. EDM의 상속은 개체 지향 프로그래밍 언어의 클래스에 대한 상속과 유사합니다. 개체 지향 언어의 클래스와 마찬가지로 개념적 모델에서는 다른 엔터티 형식 ( *기본 형식*)에서 상속 되는 엔터티 형식 ( *파생 된 형식*)을 정의할 수 있습니다. 그러나 개체 지향 프로그래밍의 클래스와는 달리, 파생 형식은 항상 기본 형식의 모든 [속성](property.md) 및 [탐색 속성](navigation-property.md) 을 상속 합니다. 파생 형식에서 상속된 속성을 재정의할 수는 없습니다.  
  
 개념적 모델에서는 파생 형식이 다른 파생 형식으로부터 상속받는 상속 계층 구조를 작성할 수 있습니다. 계층 구조의 맨 위에 있는 형식 (파생 형식이 아닌 계층 구조에서 한 형식)을 *루트 형식*이라고 합니다. 상속 계층 구조에서 루트 형식에 [엔터티 키](entity-key.md) 를 정의 해야 합니다.  
  
 파생 형식이 둘 이상의 형식으로부터 상속받는 상속 계층 구조는 작성할 수 없습니다. 예를 들어, `Book` 엔터티 형식이 포함된 개념적 모델에서는 각각 `FictionBook`으로부터 상속되는 파생 형식 `NonFictionBook`과 `Book`을 정의할 수 있습니다. 그러나 `FictionBook` 및 `NonFictionBook` 형식에서 모두 상속되는 형식을 정의할 수는 없습니다.  
  
## <a name="example"></a>예제  

다음 다이어그램에서는 네 가지 `Book`엔터티 형식인 `Publisher`, `FictionBook`, 및 `Author`가 포함 된 개념적 모델을 보여 줍니다. `FictionBook` 엔터티 형식은 `Book` 엔터티 형식에서 상속되는 파생 형식입니다. `FictionBook` 형식은 `ISBN (Key)`, `Title` 및 `Revision` 속성을 상속하고 `Genre`라는 추가 속성을 정의합니다.  
  
 ![네 개의 엔터티 형식이 포함 된 개념적 모델을 보여 주는 다이어그램입니다.](./media/entity-data-model-inheritance/entity-type-inheritance.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `FictionBook` 형식에서 상속되는 엔터티 형식 `Book`을 정의합니다.  
  
 [!code-xml[EDM_Example_Model#DerivedType](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books5.edmx#derivedtype)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
