---
title: COLLECTION(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 03228bfa-be3a-4ccc-82f8-eee429f85cf1
ms.openlocfilehash: 0e611add4ce3f20e42bb01b0bf0392bbe81ec548
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251194"
---
# <a name="collection-entity-sql"></a>COLLECTION(Entity SQL)
COLLECTION 키워드는 인라인 함수의 정의에만 사용됩니다. 컬렉션 함수는 값 컬렉션에 대해 작업을 수행하고 스칼라 출력을 생성하는 함수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
COLLECTION(type_definition)   
```  
  
## <a name="arguments"></a>인수  
 `type_definition`  
 지원되는 형식, 행 또는 참조 컬렉션을 반환하는 식입니다.  
  
## <a name="remarks"></a>설명  
 COLLECTION 키워드에 대한 자세한 내용은 [Type Definitions](type-definitions-entity-sql.md)항목을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 샘플에서는 COLLECTION 키워드를 사용하여 10진수 컬렉션을 인라인 쿼리 함수의 인수로 선언하는 방법을 보여 줍니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
