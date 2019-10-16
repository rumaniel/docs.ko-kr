---
title: System.DateTimeOffset 메서드
ms.date: 03/30/2017
ms.assetid: 25b3e5c0-7603-4a70-b3e5-2149e3da69a2
ms.openlocfilehash: 2e29cf02d4f7e8004782264bf940bb1faf393269
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781554"
---
# <a name="systemdatetimeoffset-methods"></a>System.DateTimeOffset 메서드
개체 모델 또는 외부 매핑 파일에 매핑된 경우 LINQ to SQL에서는 LINQ to SQL 쿼리의 <xref:System.DateTimeOffset?displayProperty=nameWithType> 메서드, 연산자 및 속성 대부분을 호출할 수 있습니다.  
  
 지원되지 않는 유일한 메서드는 <xref:System.Object?displayProperty=nameWithType>, `Finalize`, `GetHashCode` 및 `GetType`과 같이 LINQ to SQL 쿼리의 컨텍스트에서 인식되지 않는 `MemberwiseClone`에서 상속된 메서드입니다. SQL Server에서 실행하기 위해 LINQ to SQL에서 변환하지 못하는 이러한 메서드는 지원되지 않습니다.  
  
> [!NOTE]
> CLR(공용 언어 런타임) <xref:System.DateTimeOffset?displayProperty=nameWithType> 구조 및 LINQ to SQL을 사용하여 이 구조를 SQL `DATETIMEOFFSET` 열에 매핑하는 기능을 사용하려면 .NET Framework 3.5 SP1 이상이 필요합니다. SQL `DATETIMEOFFSET` 열은 Microsoft SQL Server 2008 이상에서만 사용할 수 있습니다.  
  
## <a name="sqlmethods-date-and-time-methods"></a>SQLMethod 날짜 및 시간 메서드  
 LINQ to SQL에서는 <xref:System.DateTimeOffset> 구조에서 제공하는 메서드 외에도 날짜 및 시간 작업을 위해 <xref:System.Data.Linq.SqlClient.SqlMethods?displayProperty=nameWithType> 클래스의 메서드를 다음 표와 같이 제공합니다.  
  
||||  
|-|-|-|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffDay%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMillisecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffNanosecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffHour%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMinute%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffSecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMicrosecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMonth%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffYear%2A>|  
  
## <a name="see-also"></a>참고자료

- [쿼리 개념](query-concepts.md)
- [개체 모델 만들기](creating-the-object-model.md)
- [SQL-CLR 형식 매핑](sql-clr-type-mapping.md)
