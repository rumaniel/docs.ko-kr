---
title: 매개 변수(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 8d618edd-0988-4ff2-8263-ce59448af7a5
ms.openlocfilehash: 723e40f523f8bb573e0ffcb1863ed0c082ea9d8d
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249583"
---
# <a name="parameters-entity-sql"></a>매개 변수(Entity SQL)
매개 변수는 일반적으로 호스트 언어에서 사용되는 바인딩 API를 통해 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 외부에서 정의되는 변수입니다. 각 매개 변수에는 이름과 형식이 있습니다. 매개 변수 이름은 쿼리 식에서 정의 되며 at (@) 기호가 접두사로 사용 됩니다. 쿼리에서 정의되는 속성 이름이나 다른 이름과 쉽게 구분할 수 있습니다.  
  
 호스트 언어 바인딩 API는 매개 변수 바인딩을 위한 API를 제공합니다.  
  
## <a name="example"></a>예제  
  
```  
select c   
      from LOB.Customers as c   
      where c.Name = @name  
```  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
- [Entity SQL 개요](entity-sql-overview.md)
