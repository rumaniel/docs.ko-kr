---
title: System.TimeSpan 메서드
ms.date: 03/30/2017
ms.assetid: 9333fee8-1454-4374-855b-8c14c002f48f
ms.openlocfilehash: 9a7eb3c979219003d497ec752b36ec54ef081b43
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781049"
---
# <a name="systemtimespan-methods"></a>System.TimeSpan 메서드
<xref:System.TimeSpan?displayProperty=nameWithType>에 대한 멤버 지원은 사용 중인 .NET Framework 및 Microsoft SQL Server의 버전에 따라 크게 다릅니다.  
  
 메서드, 연산자 또는 속성이 지원되지 않는 경우 LINQ to SQL에서는 멤버를 SQL Server에서 실행하기 위해 변환할 수 없습니다. 이러한 멤버를 코드에 사용할 수 있지만 쿼리를 Transact-SQL로 변환하기 전이나 데이터베이스에서 결과가 검색된 후에 반드시 평가해야 합니다.  
  
## <a name="previous-limitations"></a>기존의 제한  
 .NET Framework 3.5 SP1보다 낮은 버전의 .NET Framework과 함께 LINQ to SQL을 사용하는 경우 SQL Server 데이터베이스 필드를 <xref:System.TimeSpan?displayProperty=nameWithType>에 매핑할 수 없습니다. 그러나 <xref:System.TimeSpan> 값은 <xref:System.TimeSpan> 빼기에서 반환되거나 리터럴 또는 바인딩된 변수로 식에 삽입될 수 있기 때문에 <xref:System.DateTime>에 대한 연산은 지원됩니다.  
  
## <a name="supported-systemtimespan-member-support"></a>지원 되는 시스템. TimeSpan 멤버 지원

 다음 LINQ to SQL에서 지원하는 메서드, 연산자 및 속성을 LINQ to SQL 쿼리에 사용할 수 있습니다. 개체 모델 또는 외부 매핑 파일에 매핑되면 LINQ to SQL을 사용하여 LINQ to SQL 쿼리 내부의 <xref:System.TimeSpan?displayProperty=nameWithType> 멤버 대부분을 호출할 수 있습니다.  
  
|지원되는 <xref:System.TimeSpan> 메서드|지원되는 <xref:System.TimeSpan> 연산자|지원되는 <xref:System.TimeSpan> 속성|  
|------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.TimeSpan.Compare%2A>|<xref:System.TimeSpan.op_Equality%2A>|<xref:System.TimeSpan.Days%2A>|  
|<xref:System.TimeSpan.CompareTo%28System.TimeSpan%29>|<xref:System.TimeSpan.op_GreaterThan%2A>|<xref:System.TimeSpan.Hours%2A>|  
|<xref:System.TimeSpan.Duration%2A>|<xref:System.TimeSpan.op_GreaterThanOrEqual%2A>|<xref:System.TimeSpan.MaxValue>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%2CSystem.TimeSpan%29>|<xref:System.TimeSpan.op_Inequality%2A>|<xref:System.TimeSpan.Milliseconds%2A>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%29>|<xref:System.TimeSpan.op_LessThan%2A>|<xref:System.TimeSpan.Minutes%2A>|  
||<xref:System.TimeSpan.op_LessThanOrEqual%2A>|<xref:System.TimeSpan.MinValue>|  
  
> [!NOTE]
> LINQ to SQL을 사용하여 <xref:System.TimeSpan?displayProperty=nameWithType>을 SQL `TIME` 열에 매핑하려면 .NET Framework 3.5 SP1 이상이 필요합니다. SQL `TIME` 데이터 형식은 Microsoft SQL Server 2008 이상에서만 사용할 수 있습니다.  
  
### <a name="addition-and-subtraction"></a>더하기 및 빼기  
 CLR <xref:System.TimeSpan?displayProperty=nameWithType> 형식은 더하기와 빼기를 지원하지만 SQL `TIME` 형식은 그렇지 않습니다. 이 때문에 LINQ to SQL 쿼리에서 SQL `TIME` 형식에 매핑할 때 더하기와 빼기를 시도할 경우 오류가 발생합니다. Sql의 날짜 및 시간 형식에 대 한 작업에 대 한 기타 고려 사항은 [SQL CLR 형식 매핑에서](sql-clr-type-mapping.md)확인할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [쿼리 개념](query-concepts.md)
- [개체 모델 만들기](creating-the-object-model.md)
- [SQL-CLR 형식 매핑](sql-clr-type-mapping.md)
- [데이터 형식 및 함수](data-types-and-functions.md)
