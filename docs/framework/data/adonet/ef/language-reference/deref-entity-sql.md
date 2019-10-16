---
title: DEREF(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 4c78e833-b260-453d-9bf4-eb39857dd0fa
ms.openlocfilehash: 27fc23a2be47ea00eff20aa8d2f559af5ae90387
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833900"
---
# <a name="deref-entity-sql"></a>DEREF(Entity SQL)
참조 값을 역참조하고 이 역참조의 결과를 생성합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
SELECT DEREF ( o.expression ) FROM Table AS o;
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 컬렉션을 반환하는 모든 유효한 쿼리 식입니다.  
  
## <a name="return-value"></a>반환 값  
 참조되는 엔터티의 값입니다.  
  
## <a name="remarks"></a>설명  
 DEREF 연산자는 참조 값을 역참조하고 이 역참조의 결과를 생성합니다. 예를 들어 `r`이 ref @ no__t-1T > 형식의 참조 인 경우 `Deref(r)`는 `r`에서 참조 하는 엔터티를 생성 하는 `T` 형식의 식입니다. 참조 값이 null이거나 현수 참조(참조 대상이 존재하지 않음)인 경우 DEREF 연산자의 결과는 null입니다.  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리는 DEREF 연산자를 사용하여 참조 값을 역참조하고 이 역참조의 결과를 생성합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1. @No__t-0How to: PrimitiveType 결과 @ no__t-0을 반환 하는 쿼리를 실행 합니다.  
  
2. 다음 쿼리를 ExecutePrimitiveTypeQuery 메서드에 인수로 전달합니다.  
  
 [!code-sql[DP EntityServices Concepts#DEREF](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#deref)]  
  
## <a name="see-also"></a>참조

- [엔터티 SQL 참조](entity-sql-reference.md)
- [REF](ref-entity-sql.md)
- [CREATEREF](createref-entity-sql.md)
- [KEY](key-entity-sql.md)
- [null 허용 구조적 형식](nullable-structured-types-entity-sql.md)
