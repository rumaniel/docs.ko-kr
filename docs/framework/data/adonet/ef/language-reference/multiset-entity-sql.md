---
title: MULTISET (Entity SQL)
ms.date: 03/30/2017
ms.assetid: eb90a377-e47a-43a5-b308-e993b6d611e6
ms.openlocfilehash: 8e02d2d3171c9f08333ecef7ee22e65100bdf822
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250089"
---
# <a name="multiset-entity-sql"></a>MULTISET (Entity SQL)
값 목록에서 multiset 인스턴스를 만듭니다. MULTISET 생성자의 모든 값은 호환되는 `T`형식이어야 합니다. 빈 multiset 생성자는 사용할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
MULTISET ( expression [{, expression }] )  
or  
{ expression [{, expression }] }  
```  
  
## <a name="arguments"></a>인수  
 `expression`  
 유효한 모든 값 목록입니다.  
  
## <a name="return-value"></a>반환 값  
 MULTISET\<T > 유형의 컬렉션입니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 에서는 행 생성자, 개체 생성자, multiset 또는 컬렉션 생성자라는 세 가지 종류의 생성자를 제공합니다. 자세한 내용은 [형식 구성](constructing-types-entity-sql.md)을 참조 하세요.  
  
 multiset 생성자는 값 목록에서 multiset 인스턴스를 만듭니다. 생성자의 모든 값은 호환되는 형식이어야 합니다.  
  
 예를 들어, 다음 식은 정수의 multiset를 만듭니다.  
  
 `MULTISET(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
> [!NOTE]
> 중첩 multiset 리터럴은 래핑 multiset에 단일 multiset 요소가 있는 경우에만 지원 됩니다. 예를 `{{1, 2, 3}}`들면입니다. 래핑 multiset에 여러 개의 multiset 요소가 있는 경우(예: `{{1, 2}, {3, 4}}`) 중첩된 multiset 리터럴이 지원되지 않습니다.  
  
## <a name="example"></a>예제  
 다음 Entity SQL 쿼리에서는 MULTISET 연산자를 사용하여 값 목록에서 multiset 인스턴스를 만듭니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1. [방법: StructuralType 결과](../how-to-execute-a-query-that-returns-structuraltype-results.md)를 반환 하는 쿼리를 실행 합니다.  
  
2. 다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#MULTISET](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#multiset)]  
  
## <a name="see-also"></a>참고자료

- [형식 생성](constructing-types-entity-sql.md)
- [엔터티 SQL 참조](entity-sql-reference.md)
