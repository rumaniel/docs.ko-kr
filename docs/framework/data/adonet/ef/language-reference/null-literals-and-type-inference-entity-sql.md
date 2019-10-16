---
title: Null 리터럴 및 형식 유추(Entity SQL)
ms.date: 03/30/2017
ms.assetid: edd56afb-af1b-4e7d-b210-cb8998143426
ms.openlocfilehash: bb2d9184e17ee2a9916a731eb20eefa105a73753
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249818"
---
# <a name="null-literals-and-type-inference-entity-sql"></a>Null 리터럴 및 형식 유추(Entity SQL)
null 리터럴은 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 형식 시스템의 모든 형식과 호환됩니다. 하지만 null 리터럴의 형식을 올바르게 유추할 수 있도록 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 null 리터럴을 사용할 수 있는 위치에 대한 특정 제약 조건을 설정합니다.  
  
## <a name="typed-nulls"></a>형식화된 null  
 형식화된 null은 어디서나 사용할 수 있습니다. 형식이 알려져 있으므로 형식화된 null에는 형식 유추가 필요 없습니다. 예를 들어, 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 생성자를 사용하여 Int16 형식의 null을 생성할 수 있습니다.  
  
 `(cast(null as Int16))`  
  
## <a name="free-floating-null-literals"></a>자유 부동 null 리터럴  
 다음 컨텍스트에서 자유 부동 null 리터럴을 사용할 수 있습니다.  
  
- CAST 또는 TREAT 식의 인수로 사용합니다. 형식화된 null 식을 생성하기 위한 권장 방법입니다.  
  
- 메서드 또는 함수의 인수로 사용합니다. 표준 오버로드 규칙이 적용됩니다.  
  
- +, -, / 등과 같은 산술 식 인수 중 하나로 사용합니다. 이외의 인수는 null 리터럴일 수 없습니다. 그렇지 않으면 형식을 유추할 수 없습니다.  
  
- AND, OR, NOT 등과 같이 논리 식 인수 중 하나로 사용합니다. 모든 인수는 부울 형식으로 알려져 있습니다.  
  
- IS NULL 또는 IS NOT NULL 식의 인수로 사용합니다.  
  
- LIKE 식의 인수 중 하나 이상으로 사용합니다. 모든 인수는 문자열이어야 합니다.  
  
- 명명된 형식 생성자의 인수 중 하나 이상으로 사용합니다.  
  
- multiset 생성자의 인수 중 하나 이상으로 사용합니다. multiset 생성자의 인수 중 하나 이상은 null 리터럴이 아닌 식이어야 합니다.  
  
- CASE 식에서 THEN 또는 ELSE 식 중 하나 이상으로 사용합니다. CASE 식에서 THEN 또는 ELSE 식 중 하나 이상은 null 리터럴이 아닌 다른 식이어야 합니다.  
  
 다른 시나리오에서는 자유 부동 null 리터럴을 사용할 수 없습니다. 예를 들어, 자유 부동 null 리터럴을 행 생성자의 인수로서 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
