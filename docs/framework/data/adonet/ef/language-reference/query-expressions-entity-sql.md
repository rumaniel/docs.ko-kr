---
title: 쿼리 식(Entity SQL)
ms.date: 03/30/2017
ms.assetid: c36f327b-e230-48d4-bbd5-78dc6478c447
ms.openlocfilehash: 4428286890f41573a02daf31a4593d0c8f9ad34b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249271"
---
# <a name="query-expressions-entity-sql"></a>쿼리 식(Entity SQL)
쿼리 식은 다양한 쿼리 연산자를 단일 구문에 결합합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]는 [리터럴](literals-entity-sql.md), [매개 변수](parameters-entity-sql.md), [변수](variables-entity-sql.md), 연산자, [함수](functions-entity-sql.md), 집합 연산자 등을 비롯 한 다양 한 종류의 식을 제공 합니다. 자세한 내용은 [Entity SQL 참조](entity-sql-reference.md)를 참조 하세요.  
  
## <a name="clauses"></a>절  
 쿼리 식은 개체 컬렉션에 연속적인 연산을 적용하는 일련의 절로 구성되어 있으며, 표준 SQL select 문에서와 동일한 절인 [SELECT](select-entity-sql.md), [FROM](from-entity-sql.md), [WHERE](where-entity-sql.md), [GROUP By](group-by-entity-sql.md), [HAVING](having-entity-sql.md)및 [ORDER by](order-by-entity-sql.md)를 선택 합니다.  
  
## <a name="scope"></a>범위  
 FROM 절에 정의된 이름이 나타나는 순서대로 왼쪽에서 오른쪽 순으로 FROM 범위에 제공됩니다. JOIN 목록에서 식은 목록에서 앞쪽에 정의된 이름을 참조할 수 있습니다. FROM 절에서 식별된 요소의 공용 속성은 FROM 범위에 추가되지 않으며 항상 정규화된 별칭 이름을 통해 참조해야 합니다. 일반적으로 select 식의 모든 부분은 FROM 범위 내에 있는 것으로 간주됩니다.  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
