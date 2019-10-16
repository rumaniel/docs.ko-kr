---
title: DataTable 이벤트 처리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 62f404a5-13ea-4b93-a29f-55b74a16c9d3
ms.openlocfilehash: 3edafa6c6a1bc3da2abc0598f329caf0e2f21e8b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786256"
---
# <a name="handling-datatable-events"></a>DataTable 이벤트 처리
<xref:System.Data.DataTable> 개체는 애플리케이션에서 처리할 수 있는 일련의 이벤트를 제공합니다. 다음 표에서는 `DataTable` 이벤트에 대해 설명합니다.  
  
|이벤트|설명|  
|-----------|-----------------|  
|<xref:System.Data.DataTable.Initialized>|<xref:System.Data.DataTable.EndInit%2A>의 `DataTable` 메서드가 호출된 후에 발생합니다. 이 이벤트는 기본적으로 디자인 타임 시나리오를 지원하는 데 사용됩니다.|  
|<xref:System.Data.DataTable.ColumnChanged>|<xref:System.Data.DataColumn>에서 값이 성공적으로 변경된 후에 발생합니다.|  
|<xref:System.Data.DataTable.ColumnChanging>|`DataColumn`의 값이 제출될 때 발생합니다.|  
|<xref:System.Data.DataTable.RowChanged>|`DataColumn` 값 또는 <xref:System.Data.DataRow.RowState%2A>에 있는 <xref:System.Data.DataRow>의 `DataTable`가 성공적으로 변경된 후에 발생합니다.|  
|<xref:System.Data.DataTable.RowChanging>|`DataColumn` 값 또는 `RowState`에 있는 `DataRow`의 `DataTable`에 대한 변경된 값이 제출될 때 발생합니다.|  
|<xref:System.Data.DataTable.RowDeleted>|`DataRow`의 `DataTable`가 `Deleted`로 표시된 후에 발생합니다.|  
|<xref:System.Data.DataTable.RowDeleting>|`DataRow`의 `DataTable`가 `Deleted`로 표시되기 전에 발생합니다.|  
|<xref:System.Data.DataTable.TableCleared>|<xref:System.Data.DataTable.Clear%2A>의 `DataTable` 메서드 호출을 통해 모든 `DataRow`가 성공적으로 삭제된 후에 발생합니다.|  
|<xref:System.Data.DataTable.TableClearing>|`Clear` 메서드가 호출된 후 `Clear` 작업이 시작되기 전에 발생합니다.|  
|<xref:System.Data.DataTable.TableNewRow>|`DataRow`의 `NewRow` 메서드 호출을 통해 새 `DataTable`가 만들어진 후에 발생합니다.|  
|<xref:System.ComponentModel.MarshalByValueComponent.Disposed>|`DataTable`이 `Disposed`가 될 때 발생합니다. <xref:System.ComponentModel.MarshalByValueComponent>에서 상속됩니다.|  
  
> [!NOTE]
> 행을 추가하거나 삭제하는 대부분의 작업은 `ColumnChanged` 및 `ColumnChanging` 이벤트를 발생시키지 않습니다. 그러나 `ReadXml` 메서드는 `ColumnChanged` 및 `ColumnChanging` 이벤트를 발생시킵니다. 단, 읽고 있는 XML 문서가 `XmlReadMode`이고 `DiffGram`가 `Auto` 또는 `DiffGram`로 설정되어 있는 경우는 예외입니다.  
  
> [!WARNING]
> `DataSet` 이벤트가 발생한 `RowChanged`에서 데이터를 수정하면 데이터가 손상될 수 있습니다. 이와 같은 데이터 손상이 발생하면 예외가 발생하지 않습니다.  
  
## <a name="additional-related-events"></a>추가 관련 이벤트  
 <xref:System.Data.DataTable.Constraints%2A> 속성은 <xref:System.Data.ConstraintCollection> 인스턴스를 포함합니다. <xref:System.Data.ConstraintCollection> 클래스는 <xref:System.Data.ConstraintCollection.CollectionChanged> 이벤트를 노출합니다. 이 이벤트는 `ConstraintCollection`에서 제약 조건이 추가되거나 수정되거나 제거될 때 발생합니다.  
  
 <xref:System.Data.DataTable.Columns%2A> 속성은 <xref:System.Data.DataColumnCollection> 인스턴스를 포함합니다. `DataColumnCollection` 클래스는 <xref:System.Data.DataColumnCollection.CollectionChanged> 이벤트를 노출합니다. 이 이벤트는 `DataColumn`에서 `DataColumnCollection`이 추가되거나 수정되거나 제거될 때 발생합니다. 열의 이름, 형식, 식 또는 위치 등이 변경되어 열이 수정되면 이 이벤트가 발생합니다.  
  
 <xref:System.Data.DataSet.Tables%2A>의 <xref:System.Data.DataSet> 속성은 <xref:System.Data.DataTableCollection> 인스턴스를 포함합니다. `DataTableCollection` 클래스는 `CollectionChanged`와 `CollectionChanging` 이벤트를 모두 노출합니다. 이 두 이벤트는 `DataTable`에서 `DataSet`이 추가되거나 제거될 때 발생합니다.  
  
 `DataRows`가 변경되는 경우에도 관련 <xref:System.Data.DataView>의 이벤트가 발생합니다. `DataView` 클래스는 <xref:System.Data.DataView.ListChanged> 값이 변경되거나 뷰의 구성 또는 정렬 순서가 변경될 때 발생하는 `DataColumn` 이벤트를 노출합니다. <xref:System.Data.DataRowView> 클래스는 관련 <xref:System.Data.DataRowView.PropertyChanged> 값이 변경될 때 발생하는 `DataColumn` 이벤트를 노출합니다.  
  
## <a name="sequence-of-operations"></a>작업 순서  
 다음은 `DataRow`가 추가, 수정 또는 삭제되는 경우의 작업 순서입니다.  
  
1. 제안된 레코드를 만들고 변경 내용을 적용합니다.  
  
2. 식이 아닌 열의 제약 조건을 검사합니다.  
  
3. 가능한 경우 `RowChanging` 또는 `RowDeleting` 이벤트를 발생시킵니다.  
  
4. 제안된 레코드를 현재 레코드로 설정합니다.  
  
5. 관련된 인덱스를 업데이트합니다.  
  
6. 관련 `ListChanged` 개체에 대해 `DataView` 이벤트를 발생시키고, 관련 `PropertyChanged` 개체에 대해 `DataRowView` 이벤트를 발생시킵니다.  
  
7. 모든 식 열을 계산합니다. 단, 열의 제약 조건 검사는 지금 수행하지 않습니다.  
  
8. 식 열 계산 결과에 영향을 받은 관련 `ListChanged` 개체에 대해 `DataView` 이벤트를 발생시키고, 관련 `PropertyChanged` 개체에 대해 `DataRowView` 이벤트를 발생시킵니다.  
  
9. 가능한 경우 `RowChanged` 또는 `RowDeleted` 이벤트를 발생시킵니다.  
  
10. 식 열의 제약 조건을 검사합니다.  
  
> [!NOTE]
> 식 열이 변경되는 경우에는 `DataTable` 이벤트가 발생하지 않습니다. 식 열이 변경되면 `DataView` 및 `DataRowView` 이벤트만 발생합니다. 식 열은 다른 여러 열에 종속될 수 있으므로 단일 `DataRow` 작업 중 여러 번 계산될 수 있습니다. 식을 계산할 때마다 이벤트가 발생합니다. 또한 식 열이 변경되는 경우 동일한 식 열에 대한 여러 이벤트를 포함하여 단일 `DataRow` 작업에서 여러 `ListChanged` 및 `PropertyChanged` 이벤트가 발생할 수 있습니다.  
  
> [!WARNING]
> <xref:System.NullReferenceException> 이벤트 처리기 내에서 `RowChanged`을 throw하지 마세요. <xref:System.NullReferenceException>이 `RowChanged`의 `DataTable` 이벤트 내에서 throw되면 `DataTable`이 손상됩니다.  
  
### <a name="example"></a>예제  
 다음 예제에서는 `RowChanged`, `RowChanging`, `RowDeleted`, `RowDeleting`, `ColumnChanged`, `ColumnChanging`, `TableNewRow`, `TableCleared` 및 `TableClearing` 이벤트에 대한 이벤트 처리기를 만드는 방법을 보여 줍니다. 각 이벤트 처리기는 이벤트가 발생하면 콘솔 창에 해당 출력을 표시합니다.  
  
 [!code-csharp[DataWorks DataTable.Events#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.Events/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.Events#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.Events/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [DataTable에서 데이터 조작](manipulating-data-in-a-datatable.md)
- [DataAdapter 이벤트 처리](../handling-dataadapter-events.md)
- [데이터 집합 이벤트 처리](handling-dataset-events.md)
- [ADO.NET 개요](../ado-net-overview.md)
