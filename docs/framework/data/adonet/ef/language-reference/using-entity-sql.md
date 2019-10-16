---
title: USING(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 20f58b8f-6070-4456-b7e8-5ff3d6269273
ms.openlocfilehash: 9495e5daf88326c5a682172d835c3349fe79e571
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248756"
---
# <a name="using-entity-sql"></a>USING(Entity SQL)
쿼리 식에 사용되는 네임스페이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
USING [ alias = ] namespace  
```  
  
## <a name="arguments"></a>인수  
 `alias`  
 네임스페이스를 정규화하는 데 사용할 짧은 별칭을 지정합니다.  
  
 `namespace`  
 유효한 네임스페이스입니다.  
  
## <a name="example"></a>예제  
 다음 Entity SQL 쿼리에서는 USING 연산자를 사용하여 쿼리 식에 사용되는 네임스페이스를 지정합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1. [방법: PrimitiveType 결과](../how-to-execute-a-query-that-returns-primitivetype-results.md)를 반환 하는 쿼리를 실행 합니다.  
  
2. 다음 쿼리를 `ExecutePrimitiveTypeQuery` 메서드에 인수로 전달합니다.  
  
```  
using SqlServer; RAND()  
```  
  
## <a name="see-also"></a>참고자료

- [네임스페이스](namespaces-entity-sql.md)
- [엔터티 SQL 참조](entity-sql-reference.md)
