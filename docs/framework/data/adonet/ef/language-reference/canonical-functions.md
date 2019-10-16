---
title: 정식 함수
ms.date: 03/30/2017
ms.assetid: bbcc9928-36ea-4dff-9e31-96549ffed958
ms.openlocfilehash: f8ca9e2027e82db89e91287fda02d2014d53f325
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854518"
---
# <a name="canonical-functions"></a>정식 함수
이 단원에서는 모든 데이터 공급자에서 지원되며 모든 쿼리 기술에 사용될 수 있는 정식 함수에 대해 설명합니다. 정식 함수는 공급자에서 확장할 수 없습니다.  
  
 이러한 정식 함수는 공급자에 해당하는 데이터 소스 기능으로 변환됩니다. 그러면 다양한 데이터 소스에서 일반적인 형태로 함수 호출을 표현할 수 있습니다.  
  
 이러한 정식 함수는 데이터 소스에 대해 독립적이므로, 정식 함수의 인수와 반환 형식은 개념적 모델의 형식으로 정의됩니다. 하지만 일부 데이터 소스에서는 개념적 모델의 모든 형식이 지원되지 않을 수도 있습니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에서 정식 함수를 사용하면 데이터 소스에서 적절한 함수가 호출됩니다.  
  
 모든 정규 함수에는 null 입력 동작과 오류 조건이 모두 명시적으로 지정되어 있습니다. 저장소 공급자는 해당 동작을 따라야 하지만 Entity Framework이 동작을 적용 하지는 않습니다.  
  
 LINQ 시나리오의 경우 Entity Framework에 대 한 쿼리에서 CLR 메서드를 기본 데이터 소스의 메서드에 매핑합니다. CLR 메서드는 특정 메서드 집합이 데이터 소스에 관계없이 올바르게 매핑되도록 정식 함수에 매핑됩니다.  
  
## <a name="canonical-functions-namespace"></a>정식 함수 네임스페이스  
 정식 함수의 네임스페이스는 <xref:System.Data.Metadata.Edm>입니다. <xref:System.Data.Metadata.Edm> 네임스페이스는 모든 쿼리에 자동으로 포함됩니다. 하지만, 정식 함수와 이름이 같은 함수가 포함된(<xref:System.Data.Metadata.Edm> 네임스페이스) 다른 네임스페이스를 가져온 경우 네임스페이스를 지정해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [집계 정식 함수](aggregate-canonical-functions.md)  
 집계 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.  
  
 [수학 정식 함수](math-canonical-functions.md)  
 수식 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.  
  
 [문자열 정식 함수](string-canonical-functions.md)  
 문자열 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.  
  
 [날짜 및 시간 정식 함수](date-and-time-canonical-functions.md)  
 날짜 및 시간 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.  
  
 [비트 정식 함수](bitwise-canonical-functions.md)  
 비트 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 정식 함수에 대해 설명합니다.  
  
 [공간 함수](spatial-functions.md)  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]의 공간 정식 함수에 대해 설명합니다.  
  
 [기타 정식 함수](other-canonical-functions.md)  
 비트, 날짜/시간, 문자열, 수식, 집계 등으로 분류되지 않는 함수에 대해 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
- [엔터티 SQL 참조](entity-sql-reference.md)
- [개념적 모델 정식 함수와 SQL Server 함수 매핑](../conceptual-model-canonical-to-sql-server-functions-mapping.md)
- [사용자 정의 함수](user-defined-functions-entity-sql.md)
