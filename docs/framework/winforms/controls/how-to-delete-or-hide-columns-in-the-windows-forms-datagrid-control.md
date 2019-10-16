---
title: '방법: Windows Forms DataGrid 컨트롤에서 열 삭제 또는 숨기기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data grids [Windows Forms], deleting columns
- DataGrid control [Windows Forms], deleting columns
- data grids [Windows Forms], hiding columns
- columns [Windows Forms], hiding
- columns [Windows Forms], deleting in data grids
- DataGrid control [Windows Forms], hiding columns
ms.assetid: bcd0dd96-6687-4c48-b0e1-d5287b93ac91
ms.openlocfilehash: 70229abddb831788f521f85747db1093c941ba8a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967384"
---
# <a name="how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control"></a>방법: Windows Forms DataGrid 컨트롤에서 열 삭제 또는 숨기기
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 <xref:System.Windows.Forms.GridColumnStylesCollection> 및 <xref:System.Windows.Forms.DataGrid> 개체<xref:System.Windows.Forms.DataGridColumnStyle> ( 클래스<xref:System.Windows.Forms.DataGridTableStyle> 의 멤버)의 속성과 메서드를 사용 하 여 Windows Forms 컨트롤의 열을 프로그래밍 방식으로 삭제 하거나 숨길 수 있습니다.  
  
 삭제 된 열 이나 숨겨진 열이 표가 바인딩된 데이터 소스에 여전히 존재 하 고 프로그래밍 방식으로 액세스할 수 있습니다. 이러한 기능은 datagrid에 더 이상 표시 되지 않습니다.  
  
> [!NOTE]
> 응용 프로그램이 데이터의 특정 열에 액세스 하지 않고 datagrid에 표시 하지 않으려는 경우 처음에 데이터 소스에 포함 하지 않아도 됩니다.  
  
### <a name="to-delete-a-column-from-the-datagrid-programmatically"></a>프로그래밍 방식으로 DataGrid에서 열을 삭제 하려면  
  
1. 폼의 선언 영역에서 <xref:System.Windows.Forms.DataGridTableStyle> 클래스의 새 인스턴스를 선언 합니다.  
  
2. <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A?displayProperty=nameWithType> 속성을 스타일을 적용 하려는 데이터 원본의 테이블로 설정 합니다. 다음 예에서는가 이미 <xref:System.Windows.Forms.DataGrid.DataMember%2A?displayProperty=nameWithType> 설정 된 것으로 가정 하는 속성을 사용 합니다.  
  
3. 새 <xref:System.Windows.Forms.DataGridTableStyle> 개체를 datagrid의 테이블 스타일 컬렉션에 추가 합니다.  
  
4. 컬렉션의 <xref:System.Windows.Forms.DataGrid>메서드를 호출 하 여 삭제할 열의 열 인덱스를 지정 합니다. <xref:System.Windows.Forms.GridColumnStylesCollection.RemoveAt%2A> <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>  
  
    ```vb  
    ' Declare a new DataGridTableStyle in the  
    ' declarations area of your form.  
    Dim ts As DataGridTableStyle = New DataGridTableStyle()  
  
    Sub DeleteColumn()  
       ' Set the DataGridTableStyle.MappingName property  
       ' to the table in the data source to map to.  
       ts.MappingName = DataGrid1.DataMember  
  
       ' Add it to the datagrid's TableStyles collection  
       DataGrid1.TableStyles.Add(ts)  
  
       ' Delete the first column (index 0)  
       DataGrid1.TableStyles(0).GridColumnStyles.RemoveAt(0)  
    End Sub  
    ```  
  
    ```csharp  
    // Declare a new DataGridTableStyle in the  
    // declarations area of your form.  
    DataGridTableStyle ts = new DataGridTableStyle();  
  
    private void deleteColumn()  
    {  
       // Set the DataGridTableStyle.MappingName property  
       // to the table in the data source to map to.  
       ts.MappingName = dataGrid1.DataMember;  
  
       // Add it to the datagrid's TableStyles collection  
       dataGrid1.TableStyles.Add(ts);  
  
       // Delete the first column (index 0)  
       dataGrid1.TableStyles[0].GridColumnStyles.RemoveAt(0);  
    }  
    ```  
  
### <a name="to-hide-a-column-in-the-datagrid-programmatically"></a>프로그래밍 방식으로 DataGrid에서 열을 숨기려면  
  
1. 폼의 선언 영역에서 <xref:System.Windows.Forms.DataGridTableStyle> 클래스의 새 인스턴스를 선언 합니다.  
  
2. <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 의속성을데이터소스에서스타일을적용<xref:System.Windows.Forms.DataGridTableStyle> 하려는 테이블로 설정 합니다. 다음 코드 예제에서는가 이미 <xref:System.Windows.Forms.DataGrid.DataMember%2A?displayProperty=nameWithType> 설정 된 것으로 가정 하는 속성을 사용 합니다.  
  
3. 새 <xref:System.Windows.Forms.DataGridTableStyle> 개체를 datagrid의 테이블 스타일 컬렉션에 추가 합니다.  
  
4. 숨길 열의 열 인덱스를 지정 `Width` 하 여 해당 속성을 0으로 설정 하 여 열을 숨깁니다.  
  
    ```vb  
    ' Declare a new DataGridTableStyle in the  
    ' declarations area of your form.  
    Dim ts As DataGridTableStyle = New DataGridTableStyle()  
  
    Sub HideColumn()  
       ' Set the DataGridTableStyle.MappingName property  
       ' to the table in the data source to map to.  
       ts.MappingName = DataGrid1.DataMember  
  
       ' Add it to the datagrid's TableStyles collection  
       DataGrid1.TableStyles.Add(ts)  
  
       ' Hide the first column (index 0)  
       DataGrid1.TableStyles(0).GridColumnStyles(0).Width = 0  
    End Sub  
    ```  
  
    ```csharp  
    // Declare a new DataGridTableStyle in the  
    // declarations area of your form.  
    DataGridTableStyle ts = new DataGridTableStyle();  
  
    private void hideColumn()  
    {  
       // Set the DataGridTableStyle.MappingName property  
       // to the table in the data source to map to.  
       ts.MappingName = dataGrid1.DataMember;  
  
       // Add it to the datagrid's TableStyles collection  
       dataGrid1.TableStyles.Add(ts);  
  
       // Hide the first column (index 0)  
       dataGrid1.TableStyles[0].GridColumnStyles[0].Width = 0;  
    }  
    ```  
  
## <a name="see-also"></a>참고자료

- [방법: 런타임에 Windows Forms DataGrid 컨트롤에 표시 된 데이터 변경](change-displayed-data-at-run-time-wf-datagrid-control.md)
- [방법: Windows Forms DataGrid 컨트롤에 테이블 및 열 추가](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
