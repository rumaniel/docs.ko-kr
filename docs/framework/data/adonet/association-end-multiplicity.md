---
title: 연결 End 복합성
ms.date: 03/30/2017
ms.assetid: 340926ee-aefb-4bef-92cc-453e5251fd03
ms.openlocfilehash: cdcf69e7118620b2f8febd02d7695d429bf8cc2c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786949"
---
# <a name="association-end-multiplicity"></a>연결 End 복합성
*연결 end 복합성* 은 [연결](association-type.md)의 한 end에 있을 수 있는 [엔터티 형식](entity-type.md) 인스턴스 수를 정의 합니다.  
  
 연결 End 복합성은 다음 값 중 하나일 수 있습니다.  
  
- 1 (1): 연결 end에 엔터티 형식 인스턴스가 정확히 한 개 있음을 나타냅니다.  
  
- 0 또는 1 (0 ..1): 연결 end에 엔터티 형식 인스턴스가 0 개 또는 한 개 존재 함을 나타냅니다.  
  
- many (\*): 연결 end에 엔터티 형식 인스턴스가 0 개 이상 있음을 나타냅니다.  
  
 연결은 대체로 연결 End 복합성 특성을 사용합니다. 예를 들어 연결의 끝에 복합성 one (1) 및 many (\*)가 있는 경우 연결을 일대다 연결 이라고 합니다. 다음 예에서 `PublishedBy` 연결은 일대다 연결입니다. 즉, 한 명의 발행자가 많은 책을 출판하고 책 하나는 한 명의 발행자에 의해 출판됩니다. `WrittenBy` 연결은 다대다 연결입니다. 한 권의 책에 저자가 여러 명일 수 있고 한 명의 저자가 여러 책을 쓸 수도 있습니다.  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 두 연결 `PublishedBy` 및 `WrittenBy`의 개념적 모델을 보여 줍니다. `PublishedBy` 연결의 연결 End는 `Book` 및 `Publisher` 엔터티 형식입니다. `Publisher` 끝의 복합성은 1이 고, `Book` 끝의 복합성은 다 수 (\*)입니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/association-end-multiplicity/example-model-three-entity-types.gif)  
  
 ADO.NET Entity Framework에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `PublishedBy` 연결을 정의합니다.  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
