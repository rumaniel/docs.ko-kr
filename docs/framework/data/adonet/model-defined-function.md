---
title: 모델 정의 함수
ms.date: 03/30/2017
ms.assetid: 8bb2edc8-e8e7-44c2-adc7-f44e11bda4f0
ms.openlocfilehash: 1418eccecea647204620455969696c6390bd4a18
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783622"
---
# <a name="model-defined-function"></a>모델 정의 함수
*모델 정의 함수* 는 개념적 모델에 정의 된 함수입니다. 모델 정의 함수의 본문은 함수를 데이터 소스에서 지원 되는 규칙이 나 언어와는 독립적으로 표현할 수 있도록 하는 [Entity SQL](./ef/language-reference/entity-sql-language.md)으로 표현 됩니다.  
  
 모델 정의 함수 정의에는 다음 정보가 들어 있습니다.  
  
- 함수 이름 (필수)  
  
- 반환 값의 형식 (옵션)  
  
    > [!NOTE]
    > 반환 형식을 지정하지 않으면 반환 값은 void입니다.  
  
- 매개 변수 정보 (옵션)  
  
- 함수의 본문을 정의 하는 [Entity SQL](./ef/language-reference/entity-sql-language.md) 식입니다.  
  
 모델 정의 함수는 출력 매개 변수를 지원하지 않습니다. 모델 정의 함수를 작성할 수 있도록 이러한 제한이 적용됩니다.  
  
## <a name="example"></a>예제  
 다음 다이어그램에서는 세 가지 엔터티 형식 `Book`, `Publisher` 및 `Author`가 포함된 개념적 모델을 보여 줍니다.  
  
 ![게시 된 날짜가 있는 모델을 보여 주는 스크린샷](./media/model-defined-function/model-published-date-three-entity-types.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 위 다이어그램의 `Book` 인스턴스가 출판된 이후의 년 수를 반환하는 함수를 개념적 모델에 정의합니다.  
  
 [!code-xml[EDM_Example_Model#ModelDefinedFunction](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#modeldefinedfunction)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
- [엔터티 데이터 모델: 기본 데이터 형식](entity-data-model-primitive-data-types.md)
