---
title: SKIP(Entity SQL)
ms.date: 03/30/2017
ms.assetid: e2139412-8ea4-451b-8f10-91af18dfa3ec
ms.openlocfilehash: 19d3001fb8f226b02f16167dfb51ce1caa80ba3b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249228"
---
# <a name="skip-entity-sql"></a>SKIP(Entity SQL)

ORDER BY 절의 SKIP 하위 절을 사용하여 물리적 페이징을 수행할 수 있습니다. SKIP 절은 ORDER BY 절과 별도로 사용할 수 없습니다.

## <a name="syntax"></a>구문

```
[ SKIP n ]
```

## <a name="arguments"></a>인수

`n` \
건너뛸 항목의 개수입니다.

## <a name="remarks"></a>설명

SKIP 식 하위 절이 ORDER BY 절에 있으면 결과는 정렬 지정에 따라 정렬되고 SKIP 식 바로 뒤에 있는 행에서 시작하는 행이 결과 집합에 포함됩니다. 예를 들어, SKIP 5를 사용하면 처음 다섯 개의 행을 건너뛰고 여섯 번째 행부터 반환됩니다.

> [!NOTE]
> TOP 한정자와 SKIP 하위 절이 모두 같은 쿼리 식에 있는 경우 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리는 유효하지 않습니다. TOP 식을 변경하여 쿼리를 LIMIT 식에 다시 써야 합니다.

> [!NOTE]
> SQL Server 2000에서 키가 아닌 열에 ORDER BY와 함께 SKIP을 사용 하면 잘못 된 결과가 반환 될 수 있습니다. 키가 아닌 열에 중복 데이터가 있는 경우, 지정된 개수 이상의 행을 건너뛸 수 있습니다. 이는 SQL Server 2000에 대해 SKIP이 변환 되기 때문입니다. 예를 들어 다음 코드에서는 `E.NonKeyColumn` 에 중복 값이 있으면 5개가 넘는 행을 건너뛸 수 있습니다.
>
> `SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L`

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 방법 :[ 쿼리 결과](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100)) 를 통한 페이지에서는 SKIP과 함께 ORDER by 연산자를 사용 하 여 SELECT 문에서 반환 되는 개체에 사용 되는 정렬 순서를 지정 합니다.

## <a name="see-also"></a>참고자료

- [ORDER BY](order-by-entity-sql.md)
- [방법: 쿼리 결과를 통한 페이지](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [페이징](paging-entity-sql.md)
- [TOP](top-entity-sql.md)
