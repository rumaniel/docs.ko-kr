---
title: LIKE(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 8300e6d2-875b-481e-9ef4-e1e7c12d46fa
ms.openlocfilehash: fbe27f6e25c9d69f092a060fa2c3fbf0abc93318
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250507"
---
# <a name="like-entity-sql"></a>LIKE(Entity SQL)
특정 문자 `String`이 지정된 패턴과 일치하는지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
match [NOT] LIKE pattern [ESCAPE escape]  
```  
  
## <a name="arguments"></a>인수  
 `match`  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 값을 반환하는 `String` 식입니다.  
  
 `pattern`  
 지정된 `String`과 일치하는 패턴입니다.  
  
 `escape`  
 이스케이프 문자입니다.  
  
 NOT  
 LIKE의 결과를 부정하도록 지정합니다.  
  
## <a name="return-value"></a>반환 값  
 `true`이 패턴과 일치하면 `string`이고, 그렇지 않으면 `false`입니다.  
  
## <a name="remarks"></a>설명  
 LIKE 연산자를 사용하는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 식의 계산은 같음을 필터 조건으로 사용하는 식과 동일한 방법으로 이루어집니다. 하지만, LIKE 연산자를 사용하는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 식에는 리터럴과 와일드카드 문자 모두가 포함될 수 있습니다.  
  
 다음 표에서는 패턴 `string`의 구문을 설명합니다.  
  
|와일드카드 문자|Description|예제|  
|------------------------|-----------------|-------------|  
|%|문자 0개 이상으로 이루어진 임의의 `string`입니다.|`title like '%computer%'`제목의 임의의 위치에 단어가 `"computer"` 있는 모든 제목을 찾습니다.|  
|_(밑줄)|임의의 단일 문자입니다.|`firstname like '_ean'`은 Dean이나 Sean처럼 `"ean`"으로 끝나면서 4문자로 이루어진 이름을 찾습니다.|  
|[ ]|지정된 범위([a-f]) 또는 집합([abcdef]) 내의 임의의 단일 문자입니다.|`lastname like '[C-P]arsen'`은 Carsen이나 Larsen처럼 C와 P 사이의 단일 문자로 시작되고 "arsen"으로 끝나는 성을 찾습니다.|  
|[^]|지정된 범위([^a-f]) 또는 집합([^abcdef])에 속하지 않는 임의의 단일 문자입니다.|`lastname like 'de[^l]%'`는 "de"로 시작되고 그 다음 문자에 "l"이 포함되지 않는 성을 모두 찾습니다.|  
  
> [!NOTE]
> [!INCLUDE[esql](../../../../../../includes/esql-md.md)] LIKE 연산자와 ESCAPE 절은 `System.DateTime` 또는 `System.Guid` 값에 적용할 수 없습니다.  
  
 LIKE는 ASCII 패턴 일치 및 유니코드 패턴 일치를 지원합니다. 모든 매개 변수가 ASCII 문자인 경우 ASCII 패턴 일치가 수행됩니다. 인수 하나 이상이 유니코드인 경우 모든 인수가 유니코드로 변환되고 유니코드 패턴 일치가 수행됩니다. LIKE로 유니코드를 사용할 경우에는 후행 공백이 중요하지만 비유니코드의 경우에는 후행 공백이 중요하지 않습니다. 의 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 패턴 문자열 구문은 transact-sql의 구문과 같습니다.  
  
 패턴에는 정규 문자와 와일드카드 문자가 포함될 수 있습니다. 패턴 일치 과정에서 정규 문자는 문자 `string`에 지정된 문자와 정확히 일치해야 합니다. 와일드카드 문자는 문자열의 임의의 부분과 일치하면 됩니다. 와일드카드 문자와 함께 사용할 때 LIKE 연산자는 = 및 != 문자열 비교 연산자보다 융통성이 뛰어납니다.  
  
> [!NOTE]
> 특정 공급자를 대상으로 하는 경우 공급자 특정 확장을 사용할 수 있습니다. 하지만 그렇게 하면 다른 공급자에서 다르게 취급할 수 있습니다. SqlServer에서는 [first-last] 및 [^first-last] 패턴이 지원되며, 여기서 첫 번째는 first와 last 사이의 한 문자와 정확히 일치하고 두 번째는 first와 last 사이에 존재하지 않는 한 문자와 정확히 일치합니다.  
  
### <a name="escape"></a>이스케이프  
 ESCAPE 절을 사용하면 이전 단원의 표에서 설명한 특수 와일드카드 문자가 한 개 이상 포함된 문자열을 검색할 수 있습니다. 예를 들어, 여러 문서의 제목에 "100%"라는 리터럴이 포함되어 있고 해당 문서 전체에서 검색하려는 경우를 가정해 봅니다. 백분율(%) 문자는 와일드카드 문자이므로, 검색을 성공적으로 실행하려면 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ESCAPE 절을 사용하여 이 문자를 이스케이프 처리해야 합니다. 다음은 이러한 필터의 예제입니다.  
  
```  
"title like '%100!%%' escape '!'"  
```  
  
 이 검색 식에서 느낌표(!) 문자 바로 다음에 나오는 백분율(%) 와일드카드 문자는 와일드카드 문자가 아니라 리터럴로 취급됩니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 와일드카드 문자 및 대괄호(`[ ]`) 문자를 제외한 모든 문자를 이스케이프 문자로 사용할 수 있습니다. 이전의 예제에서 느낌표(!) 문자가 이스케이프 문자입니다.  
  
## <a name="example"></a>예제  
 다음 두 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에서는 LIKE 및 ESCAPE 연산자를 사용하여 특정 문자열이 지정된 패턴과 일치하는지 여부를 결정합니다. 첫 번째 쿼리는 `Name`이라는 문자로 시작되는 `Down_`을 검색합니다. 이 쿼리에서는 밑줄(`_`)이 와일드카드 문자이므로 ESCAPE 옵션이 사용되었습니다. 이스케이프 옵션을 지정 하지 않으면 쿼리는 단어 `Name` `Down` 다음에 밑줄 문자 이외의 단일 문자로 시작 하는 값을 검색 합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1. [방법: PrimitiveType 결과](../how-to-execute-a-query-that-returns-primitivetype-results.md)를 반환 하는 쿼리를 실행 합니다.  
  
2. 다음 쿼리를 `ExecutePrimitiveTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#LIKE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#like)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
