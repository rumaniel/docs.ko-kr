---
title: 패싯(facet)
ms.date: 03/30/2017
ms.assetid: 91c4e6aa-3e54-4b6c-a38a-abf27808cc85
ms.openlocfilehash: 1ac46c882b266fbb73d5c709c9fdf297e2b55b1b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783974"
---
# <a name="facet"></a>패싯(facet)
*패싯은* 기본 형식 속성 정의에 세부 정보를 추가 하는 데 사용 됩니다. 속성 [정의에](property.md) 는 속성 형식에 대 한 정보가 포함 되어 있지만 종종 더 자세한 정보가 필요 합니다. 예를 들어, 개념적 모델의 엔터티 형식에는 값을 null로 설정할 수 없는 `String` 형식의 속성이 있을 수 있습니다. 패싯을 사용하면 이 수준의 세부 정보를 지정할 수 있습니다.  
  
 다음 표에서는 EDM에서 지원되는 패싯에 대해 설명합니다.  
  
> [!NOTE]
> 패싯의 정확한 값과 동작은 EDM 구현을 사용하는 런타임 환경에서 결정됩니다.  
  
|패싯|설명|적용 대상|  
|-----------|-----------------|----------------|  
|`Collation`|속성 값에 대한 비교 및 순서 지정 작업을 수행할 때 사용할 데이터 정렬 순서 또는 정렬 순서를 지정합니다.|`String`|  
|`ConcurrencyMode`|속성 값을 낙관적 동시성 검사에 사용하도록 지정합니다.|모든 기본 형식 속성|  
|`Default`|인스턴스화 시 값이 제공되지 않는 경우 속성의 기본값을 지정합니다.|모든 기본 형식 속성|  
|`FixedLength`|속성 값 길이가 다양할 수 있는지 여부를 지정합니다.|`Binary`, `String`|  
|`MaxLength`|속성 값의 최대 길이를 지정합니다.|`Binary`, `String`|  
|`Nullable`|속성 값이 null일 수 있는지 여부를 지정합니다.|모든 기본 형식 속성|  
|`Precision`|형식이 `Decimal`인 속성의 경우 속성 값에 포함할 수 있는 자릿수를 지정합니다. 형식이 `Time`, `DateTime` 및 `DateTimeOffset`인 속성의 경우 속성 값에 대한 초의 소수 부분 자릿수를 지정합니다.|`DateTime`, `DateTimeOffset`, `Decimal`, `Time`,|  
|`Scale`|속성 값에 대한 소수점 오른쪽의 자릿수를 지정합니다.|Decimal|  
|`Unicode`|속성 값을 유니코드로 저장할지 여부를 나타냅니다.|`String`|  
  
## <a name="example"></a>예제  
 [ADO.NET Entity Framework](./ef/index.md) 에서는[CSDL](./ef/language-reference/csdl-specification.md)(개념 스키마 정의 언어) 이라는 DSL (도메인별 언어)을 사용 하 여 개념적 모델을 정의 합니다. 다음 CSDL에서는 `Book` 엔터티 형식을 정의합니다. 패싯은 XML 특성으로 구현됩니다. 패싯 값은 속성을 null로 설정할 수 없으며 `Scale` 속성의 `Precision` 및 `Revision`이 각각 29로 설정됨을 나타냅니다.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 데이터 모델의 주요 개념](entity-data-model-key-concepts.md)
- [엔터티 데이터 모델](entity-data-model.md)
