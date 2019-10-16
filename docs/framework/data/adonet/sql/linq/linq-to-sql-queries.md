---
title: LINQ to SQL 쿼리
ms.date: 03/30/2017
ms.assetid: f4897aaa-7f44-4c20-a471-b948c2971aae
ms.openlocfilehash: a170beae3a9f0c923502028f5579de1f3916c07d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793005"
---
# <a name="linq-to-sql-queries"></a>LINQ to SQL 쿼리
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 동일한 구문을 사용하여  [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 쿼리를 정의합니다. 유일한 차이점은 쿼리에서 참조된 개체가 데이터베이스의 요소에 매핑된다는 것입니다. 자세한 내용은 [LINQ 쿼리 소개(C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)를 참조하세요.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 작성한 쿼리를 해당 SQL 쿼리로 변환하고 SQL Server에 전달하여 처리합니다. 다시 말해서 애플리케이션에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] API를 사용하여 쿼리 실행을 요청합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 공급자는 쿼리를 SQL 텍스트로 변환하고 ADO 공급자에게 실행을 위임합니다. ADO 공급자는 `DataReader`의 결과로 쿼리를 반환합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 공급자는 ADO 결과를 사용자 개체의 <xref:System.Linq.IQueryable> 컬렉션으로 변환합니다.  
  
> [!NOTE]
> .NET Framework 기본 제공 형식에 대 한 대부분의 메서드와 연산자는 SQL로 직접 번역 합니다. [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)]에서 변환할 수 없는 일부는 런타임 예외를 발생시킵니다. 자세한 내용은 [SQL-CLR 형식 매핑](sql-clr-type-mapping.md)합니다.  
  
 다음 테이블에서는 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)]와 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 쿼리 항목의 유사점과 차이점에 대해 설명합니다.  
  
|항목|LINQ 쿼리|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Query|  
|----------|----------------|----------------------------------------------------------------------|  
|시퀀스를 반환하는 쿼리에 대한 쿼리를 보관하는 지역 변수의 반환 형식|제네릭 `IEnumerable`|제네릭 `IQueryable`|  
|데이터 소스 지정|(Visual Basic `From` ) 또는 `from` (C#) 절을 사용 합니다.|같은 데이터 집합|  
|필터링|`Where` 절사용/ `where`|같은 데이터 집합|  
|그룹화|`Group…By` 절사용/ `groupby`|같은 데이터 집합|  
|선택(프로젝팅)|`Select` 절사용/ `select`|같은 데이터 집합|  
|지연된 실행과 즉시 실행 비교|[LINQ 쿼리 소개 (C#)를](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md) 참조 하세요.|같은 데이터 집합|  
|조인 구현|`Join` 절사용/ `join`|는 `Join` / <xref:System.Data.Linq.Mapping.AssociationAttribute> 절을 사용할 수 있지만 더 효과적으로 특성을 사용 합니다. `join` 자세한 내용은 [관계 간 쿼리](querying-across-relationships.md)를 참조 하세요.|  
|원격 실행과 로컬 실행 비교||자세한 내용은 [원격 및 로컬 실행](remote-vs-local-execution.md).|  
|스트리밍 쿼리와 캐시된 쿼리 비교|지역 메모리 시나리오에서는 사용할 수 없습니다.||  
  
## <a name="see-also"></a>참고자료

- [LINQ 쿼리 소개(C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)
- [기본 LINQ 쿼리 작업](../../../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)
- [LINQ 쿼리 작업의 형식 관계](../../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)
- [쿼리 개념](query-concepts.md)
