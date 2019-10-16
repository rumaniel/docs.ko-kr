---
title: 연산자 우선 순위(Entity SQL)
ms.date: 03/30/2017
ms.assetid: e92e4ca5-2889-4266-9625-47f0eb01a948
ms.openlocfilehash: 2d8c78f410708fd1aa843ee8f14f7243a9f686c0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249778"
---
# <a name="operator-precedence-entity-sql"></a>연산자 우선 순위(Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에 여러 개의 연산자가 있는 경우 연산자 우선 순위에 따라 연산이 수행 되는 순서가 결정 됩니다. 실행 순서는 쿼리 결과에 상당한 영향을 미칠 수 있습니다.  
  
 다음 표에서는 연산자 우선 순위를 보여 줍니다. 높은 수준의 연산자는 낮은 수준의 연산자보다 먼저 계산됩니다.  
  
|Level|연산 유형|연산자|  
|-----------|--------------------|--------------|  
|1|기본 연산자|`. , [] ()`|  
|2|단항|`! not`|  
|3|곱하기|`* / %`|  
|4|더하기|`+ -`|  
|5|순서 지정|`< > <= >=`|  
|6|같음|`= != <>`|  
|7|조건부 AND|`and &&`|  
|8|조건부 OR|`or &#124;&#124;`|  
  
 식에 연산자 우선 순위 수준이 동일한 두 연산자가 있으면 쿼리 내의 위치를 기준으로 왼쪽에서 오른쪽으로 계산됩니다. 예를 들어, `x+y-z`는 `(x+y)-z`로 계산됩니다.  
  
 괄호를 사용하여 쿼리에서 연산자에 정의된 우선 순위를 재정의할 수 있습니다. 괄호 안의 모든 연산자를 먼저 계산하여 단일 결과를 생성한 후, 이 결과를 괄호 밖의 연산자에 사용할 수 있습니다. 예를 들어 `x+y*z` , `y` 은 `z` 를 곱한 다음 `x`를 추가 `(x+y)*z` 하지만 `x` 는 `y` 를에 추가한 다음 결과 `z`를에 곱합니다.  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
