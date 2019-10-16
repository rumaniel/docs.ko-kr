---
title: '방법: Windows Forms DataGrid 컨트롤 서식 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- columns [Windows Forms], DataGrid control
- colors [Windows Forms], applying to DataGrid controls
- DataGrid control [Windows Forms], formatting
- columns [Windows Forms], formatting in DataGrid control
- DataGrid control [Windows Forms], default styles
- tables [Windows Forms], formatting in DataGrid control
- formatting [Windows Forms]
ms.assetid: a50fcc3b-8abf-47ec-9029-7f268af4ddb1
ms.openlocfilehash: 99acef0a7b29228ddf0406352ff5a88b77294b00
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966666"
---
# <a name="how-to-format-the-windows-forms-datagrid-control"></a>방법: Windows Forms DataGrid 컨트롤 서식 지정
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 <xref:System.Windows.Forms.DataGrid> 컨트롤의 다양 한 부분에 다양 한 색을 적용 하면 정보를 쉽게 읽고 해석 하는 데 도움이 됩니다. 행과 열에 색을 적용할 수 있습니다. 행과 열은 사용자의 판단에 따라 숨겨지거나 표시 될 수도 있습니다.  
  
 컨트롤의 서식을 지정 하 <xref:System.Windows.Forms.DataGrid> 는 세 가지 기본 측면이 있습니다. 속성을 설정 하 여 데이터가 표시 되는 기본 스타일을 설정할 수 있습니다. 그런 다음이 기본에서 특정 테이블이 런타임에 표시 되는 방식을 사용자 지정할 수 있습니다. 마지막으로 데이터 표에 표시 되는 열 뿐만 아니라 표시 되는 색 및 기타 서식을 수정할 수 있습니다.  
  
 데이터 그리드 서식 지정의 초기 단계로 서 <xref:System.Windows.Forms.DataGrid> 자체의 속성을 설정할 수 있습니다. 이러한 색 및 서식 선택 항목은 표시 된 데이터 테이블 및 열에 따라 변경할 수 있는 기본을 형성 합니다.  
  
### <a name="to-establish-a-default-style-for-the-datagrid-control"></a>DataGrid 컨트롤의 기본 스타일을 설정 하려면  
  
1. 다음 속성을 적절 하 게 설정 합니다.  
  
    |속성|Description|  
    |--------------|-----------------|  
    |<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>|속성 <xref:System.Windows.Forms.DataGrid.BackColor%2A> 은 표에 있는 짝수 번호 행의 색을 정의 합니다. <xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A> 속성을 다른 색으로 설정 하면 다른 모든 행이 새 색 (행 1, 3, 5 등)으로 설정 됩니다.|  
    |<xref:System.Windows.Forms.DataGrid.BackColor%2A>|표 형태에서 짝수 행의 배경색입니다 (행 0, 2, 4, 6 등).|  
    |<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>|및 <xref:System.Windows.Forms.DataGrid.BackColor%2A> <xref:System.Windows.Forms.DataGrid.BackgroundColor%2A> 속성은 표에서 행의 색을 결정 하는 반면 속성은 표가 아래쪽으로 스크롤 되거나 몇 개의 행만 포함 된 경우에만 표시 되는 비 행 영역의 색을 결정 합니다. <xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A> 표입니다.|  
    |<xref:System.Windows.Forms.DataGrid.BorderStyle%2A>|표의 테두리 스타일로, <xref:System.Windows.Forms.BorderStyle> 열거형 값 중 하나입니다.|  
    |<xref:System.Windows.Forms.DataGrid.CaptionBackColor%2A>|그리드 바로 위에 표시 되는 표 창 캡션의 배경색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.CaptionFont%2A>|그리드 위쪽에 있는 캡션의 글꼴입니다.|  
    |<xref:System.Windows.Forms.DataGrid.CaptionForeColor%2A>|표 창 캡션의 배경색입니다.|  
    |<xref:System.Windows.Forms.Control.Font%2A>|표에 텍스트를 표시 하는 데 사용 되는 글꼴입니다.|  
    |<xref:System.Windows.Forms.DataGrid.ForeColor%2A>|데이터 표 행의 데이터로 표시 되는 글꼴의 색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.GridLineColor%2A>|데이터 표의 눈금선 색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.GridLineStyle%2A>|표의 셀을 구분 하는 <xref:System.Windows.Forms.DataGridLineStyle> 열거형 값 중 하나인 줄의 스타일입니다.|  
    |<xref:System.Windows.Forms.DataGrid.HeaderBackColor%2A>|행 및 열 머리글의 배경색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.HeaderFont%2A>|열 머리글에 사용 되는 글꼴입니다.|  
    |<xref:System.Windows.Forms.DataGrid.HeaderForeColor%2A>|열 머리글 텍스트 및 더하기/빼기 문자 모양을 포함 하 여 표 열 머리글의 전경색입니다 (여러 관련 테이블이 표시 되는 경우 행 확장).|  
    |<xref:System.Windows.Forms.DataGrid.LinkColor%2A>|자식 테이블에 대 한 링크, 관계 이름 등을 포함 하 여 데이터 표에 있는 모든 링크의 텍스트 색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsBackColor%2A>|자식 테이블에서 부모 행의 배경색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsForeColor%2A>|자식 테이블에서이는 부모 행의 전경색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsLabelStyle%2A>|<xref:System.Windows.Forms.DataGridParentRowsLabelStyle> 열거를 통해 테이블 및 열 이름을 부모 행에 표시할지 여부를 결정 합니다.|  
    |<xref:System.Windows.Forms.DataGrid.PreferredColumnWidth%2A>|데이터 표에서 열의 기본 너비(픽셀)입니다. 다시 설정 하기 전에이 속성을 설정 합니다 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 및 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성 (중 하나 개별적으로 또는 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 메서드), 또는 속성이 영향을 주지 것입니다.<br /><br /> 속성이 0 보다 작은 값으로 설정할 수 없습니다.|  
    |<xref:System.Windows.Forms.DataGrid.PreferredRowHeight%2A>|모눈에 있는 행의 행 높이 (픽셀)입니다. 다시 설정 하기 전에이 속성을 설정 합니다 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 및 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성 (중 하나 개별적으로 또는 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 메서드), 또는 속성이 영향을 주지 것입니다.<br /><br /> 속성이 0 보다 작은 값으로 설정할 수 없습니다.|  
    |<xref:System.Windows.Forms.DataGrid.RowHeaderWidth%2A>|표의 행 머리글 너비입니다.|  
    |<xref:System.Windows.Forms.DataGrid.SelectionBackColor%2A>|행 또는 셀을 선택 하는 경우이 색은 배경색입니다.|  
    |<xref:System.Windows.Forms.DataGrid.SelectionForeColor%2A>|행 또는 셀을 선택 하는 경우이 색은 전경색입니다.|  
  
    > [!NOTE]
    > 컨트롤의 색을 사용자 지정 하는 경우 색 선택이 잘못 되어 컨트롤에 액세스할 수 없도록 하는 것이 좋습니다 (예: 빨강 및 녹색). 이 문제를 방지 하려면 **시스템 색** 색상표에 있는 색을 사용 합니다.  
  
     다음 절차에서는 폼 <xref:System.Windows.Forms.DataGrid> 에 데이터 테이블에 바인딩된 컨트롤이 있다고 가정 합니다. 자세한 내용은 [Windows Forms DataGrid 컨트롤을 데이터 소스에 바인딩](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)을 참조 하세요.  
  
### <a name="to-set-the-table-and-column-style-of-a-data-table-programmatically"></a>프로그래밍 방식으로 데이터 테이블의 테이블 및 열 스타일을 설정 하려면  
  
1. 새 테이블 스타일을 만들고 해당 속성을 설정 합니다.  
  
2. 열 스타일을 만들고 해당 속성을 설정 합니다.  
  
3. 테이블 스타일의 열 스타일 컬렉션에 열 스타일을 추가 합니다.  
  
4. 데이터 표의 테이블 스타일 컬렉션에 테이블 스타일을 추가 합니다.  
  
5. 아래 예제에서는 새 <xref:System.Windows.Forms.DataGridTableStyle> 의 인스턴스를 만들고 해당 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 속성을 설정 합니다.  
  
6. **Gridcolumnstyle** 의 새 인스턴스를 만들고 해당 **MappingName** (및 다른 레이아웃 및 표시 속성)를 설정 합니다.  
  
7. 만들려는 각 열 스타일에 대해 2 ~ 6 단계를 반복 합니다.  
  
     다음 예에서는 열에 이름이 <xref:System.Windows.Forms.DataGridTextBoxColumn> 표시 되기 때문에가 생성 되는 방법을 보여 줍니다. 또한 테이블 스타일 <xref:System.Windows.Forms.GridColumnStylesCollection> 의에 열 스타일을 추가 하 고 데이터 표의에 <xref:System.Windows.Forms.GridTableStylesCollection> 테이블 스타일을 추가 합니다.  
  
    ```vb  
    Private Sub CreateAuthorFirstNameColumn()  
       ' Add a GridTableStyle and set the MappingName   
       ' to the name of the DataTable.  
       Dim TSAuthors As New DataGridTableStyle()  
       TSAuthors.MappingName = "Authors"  
  
       ' Add a GridColumnStyle and set the MappingName   
       ' to the name of a DataColumn in the DataTable.   
       ' Set the HeaderText and Width properties.   
       Dim TCFirstName As New DataGridTextBoxColumn()  
       TCFirstName.MappingName = "AV_FName"  
       TCFirstName.HeaderText = "First Name"  
       TCFirstName.Width = 75  
       TSAuthors.GridColumnStyles.Add(TCFirstName)  
  
       ' Add the DataGridTableStyle instance to   
       ' the GridTableStylesCollection.   
       myDataGrid.TableStyles.Add(TSAuthors)  
    End Sub  
    ```  
  
    ```csharp  
    private void addCustomDataTableStyle()  
    {  
       // Add a GridTableStyle and set the MappingName   
       // to the name of the DataTable.  
       DataGridTableStyle TSAuthors = new DataGridTableStyle();  
       TSAuthors.MappingName = "Authors";  
  
       // Add a GridColumnStyle and set the MappingName   
       // to the name of a DataColumn in the DataTable.   
       // Set the HeaderText and Width properties.   
       DataGridColumnStyle TCFirstName = new DataGridTextBoxColumn();  
       TCFirstName.MappingName = " AV_FName";  
       TCFirstName.HeaderText = "First Name";  
       TCFirstName.Width = 75;  
       TSAuthors.GridColumnStyles.Add(TCFirstName);  
  
       // Add the DataGridTableStyle instance to   
       // the GridTableStylesCollection.   
       dataGrid1.TableStyles.Add(TSAuthors);  
    }  
    ```  
  
    ```cpp  
    private:  
       void addCustomDataTableStyle()  
       {  
          // Add a GridTableStyle and set the MappingName   
          // to the name of the DataTable.  
          DataGridTableStyle^ TSAuthors = new DataGridTableStyle();  
          TSAuthors->MappingName = "Authors";  
  
          // Add a GridColumnStyle and set the MappingName   
          // to the name of a DataColumn in the DataTable.   
          // Set the HeaderText and Width properties.   
          DataGridColumnStyle^ TCFirstName = gcnew DataGridTextBoxColumn();  
          TCFirstName->MappingName = "AV_FName";  
          TCFirstName->HeaderText = "First Name";  
          TCFirstName->Width = 75;  
          TSAuthors->GridColumnStyles->Add(TCFirstName);  
  
          // Add the DataGridTableStyle instance to   
          // the GridTableStylesCollection.   
          dataGrid1->TableStyles->Add(TSAuthors);  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.GridTableStylesCollection>
- <xref:System.Windows.Forms.GridColumnStylesCollection>
- <xref:System.Windows.Forms.DataGrid>
- [방법: Windows Forms DataGrid 컨트롤에서 열 삭제 또는 숨기기](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
