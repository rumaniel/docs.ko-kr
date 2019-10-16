---
title: '방법: 런타임에 Windows Forms DataGrid 컨트롤에 표시되는 데이터 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- DataGrid control [Windows Forms], dynamically changing at run time
- DataGrid control [Windows Forms], data binding
- cells [Windows Forms], changing DataGrid cell values
ms.assetid: 0c7a6d00-30de-416e-8223-0a81ddb4c1f8
ms.openlocfilehash: c7bf70a67729744f4cf96318f6b270a5ea81b812
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917720"
---
# <a name="how-to-change-displayed-data-at-run-time-in-the-windows-forms-datagrid-control"></a>방법: 런타임에 Windows Forms DataGrid 컨트롤에 표시되는 데이터 변경
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 디자인 타임 기능을 사용 하 <xref:System.Windows.Forms.DataGrid> 여 Windows Forms를 만든 후에는 런타임에 그리드 <xref:System.Data.DataSet> 개체의 요소를 동적으로 변경할 수도 있습니다. 여기에는 테이블의 개별 값에 대 한 변경 또는 <xref:System.Windows.Forms.DataGrid> 컨트롤에 바인딩되는 데이터 원본이 변경 될 수 있습니다. 개별 값에 대 한 변경 내용은 <xref:System.Data.DataSet> <xref:System.Windows.Forms.DataGrid> 컨트롤이 아니라 개체를 통해 수행 됩니다.  
  
### <a name="to-change-data-programmatically"></a>프로그래밍 방식으로 데이터를 변경 하려면  
  
1. <xref:System.Data.DataSet> 개체에서 원하는 테이블을 지정 하 고 테이블에서 원하는 행과 필드를 지정한 다음 셀을 새 값으로 설정 합니다.  
  
    > [!NOTE]
    > 첫 번째 테이블이 <xref:System.Data.DataSet> 나 테이블의 첫 번째 행을 지정 하려면 0을 사용 합니다.  
  
     다음 예에서는를 클릭 `Button1`하 여 데이터 집합의 첫 번째 테이블에 있는 첫 번째 행의 두 번째 항목을 변경 하는 방법을 보여 줍니다. () 및`0` 테이블 (및 `1`)이 이전에 작성 되었습니다.`ds` <xref:System.Data.DataSet>  
  
    ```vb  
    Protected Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       ds.tables(0).rows(0)(1) = "NewEntry"  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       ds.Tables[0].Rows[0][1]="NewEntry";  
    }  
    ```  
  
    ```cpp  
    private:   
       void button1_Click(System::Object^ sender, System::EventArgs^ e)  
       {  
          dataSet1->Tables[0]->Rows[0][1] = "NewEntry";  
       }  
    ```  
  
     (시각적 C#개체, C++시각적 개체) 폼의 생성자에 다음 코드를 추가 하 여 이벤트 처리기를 등록 합니다.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click +=  
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
     런타임에 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 메서드를 사용 하 여 다른 데이터 소스에 <xref:System.Windows.Forms.DataGrid> 컨트롤을 바인딩할 수 있습니다. 예를 들어 서로 다른 데이터베이스에 연결 된 여러 개의 ADO.NET 데이터 컨트롤이 있을 수 있습니다.  
  
### <a name="to-change-the-datasource-programmatically"></a>데이터 원본을 프로그래밍 방식으로 변경 하려면  
  
1. 메서드를 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 바인딩할 데이터 원본 및 테이블의 이름으로 설정 합니다.  
  
     다음 예에서는 메서드를 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 사용 하 여 Pubs 데이터베이스의 Authors 테이블에 연결 된 adoPubsAuthors (ADO.NET data control)로 날짜 원본을 변경 하는 방법을 보여 줍니다.  
  
    ```vb  
    Private Sub ResetSource()  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors")  
    End Sub  
    ```  
  
    ```csharp  
    private void ResetSource()  
    {  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors");  
    }  
    ```  
  
    ```cpp  
    private:  
       void ResetSource()  
       {  
          dataGrid1->SetDataBinding(adoPubsAuthors, "Authors");  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 데이터 세트](../../data/adonet/ado-net-datasets.md)
- [방법: Windows Forms DataGrid 컨트롤에서 열 삭제 또는 숨기기](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
- [방법: Windows Forms DataGrid 컨트롤에 테이블 및 열 추가](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [방법: Windows Forms DataGrid 컨트롤을 데이터 소스에 바인딩](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
