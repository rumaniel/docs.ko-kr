---
title: SqlType 및 DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.openlocfilehash: dea5a2017479443cb747d31e253c1c83585ddd09
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791492"
---
# <a name="sqltypes-and-the-dataset"></a>SqlType 및 DataSet
ADO.NET 2.0에서는 `DataSet` 네임스페이스를 통해 <xref:System.Data.SqlTypes>에 대한 형식 지원이 향상되었습니다. <xref:System.Data.SqlTypes>의 형식은 SQL Server 데이터베이스의 데이터 형식과 의미 체계 및 정밀도가 동일한 데이터 형식을 제공하도록 디자인되었습니다. <xref:System.Data.SqlTypes>의 각 데이터 형식은 SQL Server의 데이터 형식과 동일하며 기본 데이터 표현도 같습니다.  
  
 <xref:System.Data.SqlTypes>에 <xref:System.Data.DataSet>를 직접 사용하면 SQL Server 데이터 형식으로 작업할 때 몇 가지 이점이 있습니다. 우선 <xref:System.Data.SqlTypes>는 SQL Server 기본 데이터 형식과 동일한 의미 체계를 지원합니다. <xref:System.Data.SqlTypes> 정의에 <xref:System.Data.DataColumn> 중 하나를 지정하면 decimal 또는 숫자 데이터 형식을 CLR(공용 언어 런타임) 데이터 형식 중 하나로 변환할 때 발생할 수 있는 전체 자릿수 손실을 방지할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Data.DataTable> 개체를 만들고 CLR 형식 대신 <xref:System.Data.DataColumn>를 사용하여 <xref:System.Data.SqlTypes> 데이터 형식을 명시적으로 정의합니다. 이 코드는 SQL Server의 AdventureWorks 데이터베이스에 있는 Sales.SalesOrderDetail 테이블의 데이터로 <xref:System.Data.DataTable>을 채웁니다. 콘솔 창에 표시된 출력은 각 열의 데이터 형식과 SQL Server에서 검색한 값을 나타냅니다.  
  
 [!code-csharp[DataWorks SqlTypes.GetTypeAW#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.GetTypeAW/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.GetTypeAW#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.GetTypeAW/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [SQL Server 데이터 형식 매핑](../sql-server-data-type-mappings.md)
- [매개 변수 및 매개 변수 데이터 형식 구성](../configuring-parameters-and-parameter-data-types.md)
- [ADO.NET 개요](../ado-net-overview.md)
