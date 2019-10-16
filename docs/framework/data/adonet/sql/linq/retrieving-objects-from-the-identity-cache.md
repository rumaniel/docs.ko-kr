---
title: ID 캐시에서 개체 검색
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 96c13903-ccb6-4a0e-ab6a-8ca955ca314d
ms.openlocfilehash: d14b15f72bd196d8b3a61f22c614516e17d2e95b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781234"
---
# <a name="retrieving-objects-from-the-identity-cache"></a>ID 캐시에서 개체 검색
이 항목은 <xref:System.Data.Linq.DataContext>에서 관리하는 ID 캐시에서 개체를 반환하는 LINQ to SQL 쿼리의 형식에 대해 설명합니다.  
  
 LINQ to SQL에서 <xref:System.Data.Linq.DataContext>가 개체를 관리하는 방법 중 하나는 쿼리가 실행될 때 ID 캐시에 개체 ID를 로깅하는 것입니다. 일부 경우 LINQ to SQL은 데이터베이스에서 쿼리를 실행하기 전에 ID 캐시에서 개체를 검색하려고 합니다.  
  
 일반적으로 LINQ to SQL 쿼리의 경우 ID 캐시에서 개체를 반환하려면 쿼리가 개체의 기본 키를 기반으로 해야 하며 단일 개체를 반환해야 합니다. 특히 쿼리는 아래에 나와 있는 일반적인 형태 중 하나여야 합니다.  
  
> [!NOTE]
> 미리 컴파일된 쿼리는 ID 캐시에서 개체를 반환하지 않습니다. 미리 컴파일된 쿼리에 <xref:System.Data.Linq.CompiledQuery> 대 한 자세한 내용은 및 [방법: 쿼리](how-to-store-and-reuse-queries.md)를 저장 하 고 다시 사용 합니다.  
  
 ID 캐시에서 개체를 검색하려면 쿼리는 다음과 같은 일반적인 형태 중 하나로 되어 있어야 합니다.  
  
- <xref:System.Data.Linq.Table%601> `.Function1(` `predicate` `)`  
  
- <xref:System.Data.Linq.Table%601> `.Function1(` `predicate` `).Function2()`  
  
 이러한 일반적인 형태에서 `Function1`, `Function2` 및 `predicate`는 다음과 같이 정의됩니다.  
  
 `Function1`는 다음과 같을 수 있습니다.  
  
- <xref:System.Linq.Queryable.Where%2A>  
  
- <xref:System.Linq.Queryable.First%2A>  
  
- <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
- <xref:System.Linq.Queryable.Single%2A>  
  
- <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `Function2`는 다음과 같을 수 있습니다.  
  
- <xref:System.Linq.Queryable.First%2A>  
  
- <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
- <xref:System.Linq.Queryable.Single%2A>  
  
- <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `predicate`는 개체의 기본 키 속성이 상수 값으로 설정되어 있는 식이어야 합니다. 개체에 둘 이상의 속성에서 정의한 기본 키가 있는 경우 각 기본 키 속성은 상수 값으로 설정되어야 합니다. 다음은 `predicate`가 사용해야 하는 형태의 예제입니다.  
  
- `c => c.PK == constant_value`  
  
- `c => c.PK1 == constant_value1 && c=> c.PK2 == constant_value2`  
  
## <a name="example"></a>예제  
 다음 코드는 ID 캐시에서 개체를 검색하는 LINQ to SQL 쿼리의 형식에 대한 예제를 제공합니다.  
  
 [!code-csharp[L2S_QueryCache#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/l2s_querycache/cs/program.cs#1)]
 [!code-vb[L2S_QueryCache#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/l2s_querycache/vb/module1.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [쿼리 개념](query-concepts.md)
- [개체 ID](object-identity.md)
- [배경 정보](background-information.md)
- [개체 ID](object-identity.md)
