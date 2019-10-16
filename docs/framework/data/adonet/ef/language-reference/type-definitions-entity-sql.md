---
title: 형식 정의(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 306b204a-ade5-47ef-95b5-c785d2da4a7e
ms.openlocfilehash: 471964266c290d5eba95804dbe1c2bc5225e3f83
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248945"
---
# <a name="type-definitions-entity-sql"></a>형식 정의(Entity SQL)
형식 정의는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 인라인 함수의 선언문에 사용됩니다.  
  
## <a name="remarks"></a>설명  
 인라인 함수에 대 한 선언문은 [함수 키워드와 함수 이름](function-entity-sql.md) (예: "myavg")을 나타내는 식별자와 괄호 안에 있는 매개 변수 정의 목록 (예: "dues Collection ( Decimal) ").  
  
 매개 변수 정의 목록은 0개 이상의 매개 변수 정의로 구성됩니다. 각 매개 변수 정의는 식별자("dues"와 같은 함수에 대한 매개 변수 이름)와 뒤에 오는 형식 정의(예: "Collection(Decimal)")로 구성됩니다.  
  
 형식 정의는 다음 중 하나가 될 수 있습니다.  
  
- 식별자 형식(예: "Int32" 또는 "AdventureWorks.Order")  
  
- `COLLECTION` 키워드와 뒤에 오는 괄호로 묶은 다른 형식 정의(예: "Collection(AdventureWorks.Order)")  
  
- ROW 키워드와 뒤에 오는 괄호로 묶은 속성 정의 목록(예: "Row(x AdventureWorks.Order)"). 속성 정의의 형식은 "`identifier type_definition`, `identifier type_definition`, ..."과 같습니다.  
  
- REF 키워드와 뒤에 오는 괄호로 묶은 식별자 형식(예: "Ref(AdventureWorks.Order)"). REF 형식 정의 연산자의 경우 엔터티 형식을 인수로 사용해야 합니다. 기본 형식을 인수로 지정할 수 없습니다.  
  
 또한 형식 정의를 중첩할 수 있습니다(예: "Collection(Row(x Ref(AdventureWorks.Order)))").  
  
 형식 정의 옵션은 다음 중 하나입니다.  
  
- `IdentifierName supported_type`, 또는  
  
- `IdentifierName` COLLECTION(`type_definition`)  
  
- `IdentifierName` ROW(`property_definition`)  
  
- `IdentifierName` REF(`supported_entity_type`)  
  
 속성 정의 옵션은 `IdentifierName type_definition`입니다.  
  
 지원되는 형식은 현재 네임스페이스의 모든 형식입니다. 이러한 지원되는 형식에는 기본 형식과 엔터티 형식이 모두 포함됩니다.  
  
 지원되는 엔터티 형식은 현재 네임스페이스의 엔터티 형식만 참조합니다. 이러한 형식에는 기본 형식이 포함되지 않습니다.  
  
## <a name="examples"></a>예  
 다음은 간단한 형식 정의의 예제입니다.  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 EDM.Decimal) AS (  
   Round(p1)  
)  
MyRound(CAST(1.7 as EDM.Decimal))  
```  
  
 다음은 COLLECTION 형식 정의의 예제입니다.  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Collection(EDM.Decimal)) AS (  
   Select Round(p1) from p1  
)  
MyRound({CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)})  
```  
  
 다음은 ROW 형식 정의의 예제입니다.  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Row(x EDM.Decimal)) AS (  
   Round(p1.x)  
)  
select MyRound(row(a as x)) from {CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)} as a  
```  
  
 다음은 REF 형식 정의의 예제입니다.  
  
```  
USING Microsoft.Samples.Entity  
Function UnReference(p1 Ref(AdventureWorks.Order)) AS (  
   Deref(p1)  
)  
select Ref(x) from AdventureWorksEntities.SalesOrderHeaders as x  
```  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
- [엔터티 SQL 참조](entity-sql-reference.md)
