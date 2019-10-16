---
title: 연결 End
ms.date: 03/30/2017
ms.assetid: 2c345213-0296-4d90-ac6d-cef179798a75
ms.openlocfilehash: 33cc2e10d9b72ef7f5f024905938c41fcc4a9755
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785051"
---
# <a name="association-end"></a>연결 End
연결 *end* 는 연결의 한쪽 end에서 [엔터티 형식을](entity-type.md) 식별 하 [고 연결](association-type.md) 의 해당 end에 있을 수 있는 엔터티 형식 인스턴스 수를 식별 합니다. 연결 End는 연결의 일부로 정의되고 연결에는 정확히 두 개의 연결 End가 있어야 합니다. [탐색 속성](navigation-property.md) 을 통해 한 연결 end에서 다른 연결 끝으로 탐색할 수 있습니다.  
  
 연결 End 정의에는 다음 정보가 들어 있습니다.  
  
- 연결과 관련된 엔터티 형식 중 하나 (필수)  
  
    > [!NOTE]
    > 지정된 연결에서 각 연결 End에 지정한 엔터티 형식은 달라야 합니다. 이렇게 하면 자체 연결이 만들어집니다.  
  
- 연결의 한 end에 있을 수 있는 엔터티 형식 인스턴스 수를 나타내는 [연결 end 복합성](association-end-multiplicity.md) 입니다. 연결 end 복합성은 1 (1), 0 또는 1 (0 ..1) 또는 다 수 (\*)의 값을 가질 수 있습니다.  
  
- 연결 End의 이름. (옵션)  
  
- 삭제 시 계단식 배열과 같이 연결에서 수행되는 작업에 대한 정보 (옵션)  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 두 연결 `PublishedBy` 및 `WrittenBy`의 개념적 모델을 보여 줍니다. `PublishedBy` 연결의 연결 End는 `Book` 및 `Publisher` 엔터티 형식입니다. `Publisher` 끝의 복합성은 1이 고, `Book` 끝의 복합성은 다 수 (\*)입니다. 즉, 게시자가 많은 책을 게시 하 고 한 출판사에서 책을 게시 함을 나타냅니다.  
  
 ![세 개의 엔터티 형식이 있는 예제 모델](./media/association-end/example-model-three-entity-types.gif)  
  
 ADO.NET Entity Framework에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 다이어그램에 표시된 `PublishedBy` 연결을 정의합니다. 각 연결 End의 형식, 이름 및 복합성은 XML 특성(각각 `Type`, `Role` 및 `Multiplicity` 특성)으로 지정됩니다. 한 End에서 수행되는 작업에 대한 선택적 정보는 XML 요소(`OnDelete` 요소)에 지정됩니다. 이 경우 발행자를 삭제하면 연결된 책도 모두 삭제됩니다.  
  
 [!code-xml[EDM_Example_Model#AssociationEnd](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#associationend)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
