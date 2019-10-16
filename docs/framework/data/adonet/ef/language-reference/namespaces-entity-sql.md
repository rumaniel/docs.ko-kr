---
title: 네임스페이스(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 83991c21-60db-4af9-aca3-b416f6cae98e
ms.openlocfilehash: 395ffb23859be27b4897dfc352f6e44d52286b26
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249990"
---
# <a name="namespaces-entity-sql"></a>네임스페이스(Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 형식 이름, 엔터티 집합, 함수 등의 전역 식별자에 대한 이름 충돌을 피하기 위해 네임스페이스가 도입되었습니다. 의 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 네임 스페이스 지원은 .NET Framework의 네임 스페이스 지원과 유사 합니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]은 다음 예제와 같이 정규화된 네임스페이스(네임스페이스에 대해 짧은 별칭이 제공됨)와 비정규화된 네임스페이스라는 두 가지 형태의 USING 절을 제공합니다.  
  
 `USING System.Data;`  
  
 `USING tsql = System.Data;`  
  
## <a name="name-resolution-rules"></a>이름 확인 규칙  
 로컬 범위에서 식별자를 확인할 수 없는 경우에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 전역 범위 (네임 스페이스)에서 이름을 찾으려고 시도 합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 먼저 식별자(접두사)와 일치하는 정규화된 네임스페이스가 있는지 확인합니다. 일치하는 것이 있으면 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 해당 네임스페이스에서 나머지 식별자를 확인합니다. 일치하는 것이 없으면 예외가 throw됩니다.  
  
 다음으로 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 모든 비정규화된 네임스페이스(프롤로그에 지정됨)에서 식별자를 검색합니다. 식별자를 정확하게 하나의 네임스페이스에서 찾을 수 있으면 해당 위치가 반환됩니다. 해당 식별자와 일치하는 네임스페이스가 둘 이상이면 예외가 throw됩니다. 식별자의 네임스페이스를 확인할 수 없는 경우 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 다음 예제와 같이 이름을 다음 바깥쪽 범위(<xref:System.Data.Common.DbCommand> 또는 <xref:System.Data.Common.DbConnection> 개체)로 전달합니다.  
  
```  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)  
```  
  
## <a name="differences-from-the-net-framework"></a>.NET Framework와의 차이점  
 .NET Framework에서 부분적으로 정규화 된 네임 스페이스를 사용할 수 있습니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 사용할 수 없습니다.  
  
## <a name="adonet-usage"></a>ADO.NET 사용  
 쿼리는 ADO.NET <xref:System.Data.Common.DbCommand> 개체를 통해 표현됩니다. <xref:System.Data.Common.DbCommand> 개체를 통해 <xref:System.Data.Common.DbConnection> 개체를 작성할 수 있습니다. 네임스페이스는 <xref:System.Data.Common.DbCommand> 및 <xref:System.Data.Common.DbConnection> 개체의 일부로 지정할 수도 있습니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 쿼리 자체 내에서 식별자를 확인할 수 없는 경우 외부 네임스페이스를 검색합니다(비슷한 규칙이 사용됨).  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
- [Entity SQL 개요](entity-sql-overview.md)
