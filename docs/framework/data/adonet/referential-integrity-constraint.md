---
title: 참조 무결성 제약 조건
ms.date: 03/30/2017
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
ms.openlocfilehash: 28880c7085f8b4e3dd2e51b5633c1f0e2a984a4b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794447"
---
# <a name="referential-integrity-constraint"></a>참조 무결성 제약 조건
EDM (엔터티 데이터 모델)의 *참조 무결성 제약 조건은* 관계형 데이터베이스의 참조 무결성 제약 조건과 비슷합니다. 데이터베이스 테이블의 열이 다른 테이블의 기본 키를 참조할 수 있는 것과 동일한 방식으로 [엔터티 형식의](entity-type.md) [속성](property.md) 은 다른 엔터티 형식의 [엔터티 키](entity-key.md) 를 참조할 수 있습니다. 참조 되는 엔터티 형식을 제약 조건의 *주 끝* 이라고 합니다. 주 끝을 참조 하는 엔터티 형식을 제약 조건의 *종속 끝* 이라고 합니다.  
  
 참조 무결성 제약 조건은 두 엔터티 형식 간의 [연결](association-type.md) 의 일부로 정의 됩니다. 참조 무결성 제약 조건 정의에서는 다음 정보를 지정합니다.  
  
- 제약 조건의 주 끝 (엔터티 키가 종속 끝에서 참조되는 엔터티 형식)  
  
- 주 끝의 엔터티 키  
  
- 제약 조건의 종속 끝 (주 끝의 엔터티 키를 참조하는 속성이 있는 엔터티 형식)  
  
- 종속 끝의 참조 속성  
  
 EDM의 참조 무결성 제약 조건은 항상 올바른 연결이 존재하도록 보장하는 데 사용됩니다. 자세한 내용은 [외래 키 속성](foreign-key-property.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 두 연결 `WrittenBy` 및 `PublishedBy`의 개념적 모델을 보여 줍니다. `Book` 엔터티 형식에는 `PublisherId` 연결에 참조 무결성 제약 조건을 정의할 때 `Publisher` 엔터티 형식의 엔터티 키를 참조하는 `PublishedBy` 속성이 있습니다.  
  
 ![RefConstraintModel](./media/referential-integrity-constraint/reference-constraint-model.gif "참조 제약 조건 모델 예")  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위의 개념적 모델에 표시된 `PublishedBy` 연결에 참조 무결성 제약 조건을 정의합니다.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
