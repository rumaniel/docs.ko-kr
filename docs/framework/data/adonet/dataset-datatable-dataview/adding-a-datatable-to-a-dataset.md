---
title: 데이터 세트에 DataTable 추가
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 556d29a3-8fc9-4e38-b3ee-c188f7e7b155
ms.openlocfilehash: a1249718d1e1e1e64fd6fa6ee9ee8157545b5e0b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786637"
---
# <a name="adding-a-datatable-to-a-dataset"></a>데이터 세트에 DataTable 추가
ADO.NET에서는 <xref:System.Data.DataTable> 개체를 만들어 기존 <xref:System.Data.DataSet>에 추가할 수 있습니다. 또한 <xref:System.Data.DataTable> 및 <xref:System.Data.DataTable.PrimaryKey%2A> 속성을 사용하여 <xref:System.Data.DataColumn.Unique%2A>에 대한 제약 조건 정보를 설정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Data.DataSet>을 구성하고 새 <xref:System.Data.DataTable> 개체를 <xref:System.Data.DataSet>에 추가한 다음 세 개의 <xref:System.Data.DataColumn> 개체를 해당 테이블에 추가합니다. 마지막으로 이 코드에서는 열 하나를 기본 키 열로 설정합니다.  
  
 [!code-csharp[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/VB/source.vb#1)]  
  
## <a name="case-sensitivity"></a>대/소문자 구분  
 이름은 같으나 대/소문자가 다른 두 개 이상의 테이블이나 관계가 하나의 <xref:System.Data.DataSet>에 존재할 수 있습니다. 이런 경우 테이블과 관계를 이름에 따라 참조할 때는 대/소문자가 구분됩니다. 예를 들어 <xref:System.Data.DataSet> **데이터 집합** 에 **table1** 과 **table1**테이블이 포함 되어 있는 경우 table1은 이름으로 **table1** **["table1"]** 및 **table1** 은 **dataset ["table1"]** 로 참조 합니다. 테이블 중 하나를 데이터 집합으로 참조 하려고 **합니다. tables ["TABLE1"]** 은 예외를 생성 합니다.  
  
 특별한 이름의 테이블이나 관계가 하나만 있으면 대/소문자 구분 동작이 적용되지 않습니다. 예를 들어에 <xref:System.Data.DataSet> **Table1**만 있는 경우에는 **dataSet ["Table1"]** 을 사용 하 여 참조할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Data.DataSet.CaseSensitive%2A>의 <xref:System.Data.DataSet> 속성은 이 동작에 영향을 미치지 않습니다. <xref:System.Data.DataSet.CaseSensitive%2A> 속성은 <xref:System.Data.DataSet> 내의 데이터에 적용되며 정렬, 찾기, 필터링, 제약 조건 적용 등에 영향을 줍니다.  
  
## <a name="namespace-support"></a>네임스페이스 지원  
 ADO.NET 2.0보다 이전 버전에서는 네임스페이스가 서로 다르더라도 두 테이블의 이름이 같을 수 없었습니다. 하지만 ADO.NET 2.0에서는 이러한 제한이 사라졌습니다. <xref:System.Data.DataSet>에 <xref:System.Data.DataTable.TableName%2A> 속성 값은 같지만 <xref:System.Data.DataTable.Namespace%2A> 속성 값이 다른 두 테이블이 포함될 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
