---
title: OFTYPE(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 6d259ca7-bbf0-40f8-a154-181d25c0d67e
ms.openlocfilehash: 36701a5e75e804ea541d242aaff243de0b24cec3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249791"
---
# <a name="oftype-entity-sql"></a>OFTYPE(Entity SQL)
쿼리 식에서 특정 형식을 가진 개체 컬렉션을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
OFTYPE ( expression, [ONLY] test_type )  
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 개체 컬렉션을 반환하는 모든 유효한 쿼리 식입니다.  
  
 `test_type`  
 `expression` 에서 반환된 각 개체를 테스트할 형식입니다. 형식은 네임스페이스로 한정되어야 합니다.  
  
## <a name="return-value"></a>반환 값  
 `test_type`형식이거나 `test_type`의 기본 형식 또는 파생 형식인 개체 컬렉션입니다. ONLY를 지정하면 `test_type` 인스턴스나 빈 컬렉션만 반환됩니다.  
  
## <a name="remarks"></a>설명  
 `OFTYPE` 식은 컬렉션의 각 요소에 대해 형식 테스트를 수행하기 위해 실행되는 형식 식을 지정합니다.  `OFTYPE` 식은 해당 형식이나 하위 형식에 해당하는 요소만 포함하는 지정된 형식의 새 컬렉션을 생성합니다.  
  
 `OFTYPE` 식은 다음 쿼리 식의 단축된 형태입니다.  
  
```  
select value treat(t as T) from ts as t where t is of (T)  
```  
  
 Manager가 Employee의 하위 형식인 경우 다음 식은 직원 컬렉션에 있는 관리자만으로 구성된 컬렉션을 생성합니다.  
  
```  
OfType(employees, NamespaceName.Manager)  
```  
  
 형식 필터를 사용하여 컬렉션을 캐스팅할 수도 있습니다.  
  
```  
OfType(executives, NamespaceName.Manager)  
```  
  
 모든 임원은 관리자이므로 현재 컬렉션이 관리자 컬렉션으로 형식화된 경우에도 결과 컬렉션에 원래 임원이 모두 포함됩니다.  
  
 다음 표에서는 일부 패턴에 대한 `OFTYPE` 연산자의 동작을 보여 줍니다. 공급자가 호출되기 전에 클라이언트 쪽에서 모든 예외가 throw됩니다.  
  
|무늬|동작|  
|-------------|--------------|  
|OFTYPE(Collection(EntityType), EntityType)|Collection(EntityType)|  
|OFTYPE(Collection(ComplexType), ComplexType)|되거나|  
|OFTYPE(Collection(RowType), RowType)|되거나|  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에서는 OFTYPE 연산자를 사용하여 Course 개체 컬렉션에서 OnsiteCourse 개체 컬렉션을 반환합니다. 쿼리는 [School 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))을 기반으로 합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#OFTYPE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#oftype)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
