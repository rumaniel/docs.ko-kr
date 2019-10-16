---
title: '방법: Windows Forms DataGrid 컨트롤을 사용 하 여 마스터-세부 목록 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- master-details lists
- DataGrid control [Windows Forms], master-details lists
- related tables [Windows Forms], displaying in DataGrid control
ms.assetid: 20388c6a-94f9-4d96-be18-8c200491247f
ms.openlocfilehash: f0fd95cf0cd66e9a5105c0b8ff77d8c536a5822d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914760"
---
# <a name="how-to-create-masterdetail-lists-with-the-windows-forms-datagrid-control"></a>방법: Windows Forms DataGrid 컨트롤을 사용하여 마스터/세부 목록 만들기
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 에 <xref:System.Data.DataSet> 일련의 관련 테이블이 포함 되어 있는 경우 두 개의 <xref:System.Windows.Forms.DataGrid> 컨트롤을 사용 하 여 데이터를 마스터/세부 형식으로 표시할 수 있습니다. 하나 <xref:System.Windows.Forms.DataGrid> 는 마스터 그리드로 지정 되 고 두 번째는 세부 정보 표로 지정 됩니다. 마스터 목록에서 항목을 선택 하면 관련 된 모든 자식 항목이 세부 정보 목록에 표시 됩니다. 예를 들어에 <xref:System.Data.DataSet> customers 테이블과 관련 Orders 테이블이 포함 되어 있는 경우에는 customers 테이블을 마스터 그리드로 지정 하 고 orders 테이블을 세부 정보 표로 지정 합니다. 마스터 표에서 고객이 선택 된 경우 Orders 테이블에서 해당 고객과 연결 된 모든 주문이 세부 정보 표에 표시 됩니다.  
  
### <a name="to-set-a-masterdetail-relationship-programmatically"></a>마스터/세부 관계를 프로그래밍 방식으로 설정 하려면  
  
1. 두 개의 새 <xref:System.Windows.Forms.DataGrid> 컨트롤을 만들고 해당 속성을 설정 합니다.  
  
2. 데이터 집합에 테이블을 추가 합니다.  
  
3. 만들 관계를 나타내는 형식의 <xref:System.Data.DataRelation> 변수를 선언 합니다.  
  
4. 관계의 이름을 지정 하 고 두 테이블을 연결 하는 테이블, 열 및 항목을 지정 하 여 관계를 인스턴스화합니다.  
  
5. <xref:System.Data.DataSet> 개체 의<xref:System.Data.DataSet.Relations%2A> 컬렉션에 관계를 추가 합니다.  
  
6. 의 메서드를 사용 하 여 각 표 <xref:System.Data.DataSet>를에 바인딩합니다. <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> <xref:System.Windows.Forms.DataGrid>  
  
     다음 예에서는 이전에 생성 <xref:System.Data.DataSet> 된 (`ds`)에서 Customers 테이블과 Orders 테이블 간에 마스터/세부 관계를 설정 하는 방법을 보여 줍니다.  
  
    ```vb  
    Dim myDataRelation As DataRelation  
    myDataRelation = New DataRelation _  
       ("CustOrd", ds.Tables("Customers").Columns("CustomerID"), _  
       ds.Tables("Orders").Columns("CustomerID"))  
    ' Add the relation to the DataSet.  
    ds.Relations.Add(myDataRelation)  
    GridOrders.SetDataBinding(ds, "Customers")  
    GridDetails.SetDataBinding(ds, "Customers.CustOrd")  
    ```  
  
    ```csharp  
    DataRelation myDataRelation;  
    myDataRelation = new DataRelation("CustOrd", ds.Tables["Customers"].Columns["CustomerID"], ds.Tables["Orders"].Columns["CustomerID"]);  
    // Add the relation to the DataSet.  
    ds.Relations.Add(myDataRelation);  
    GridOrders.SetDataBinding(ds,"Customers");  
    GridDetails.SetDataBinding(ds,"Customers.CustOrd");  
    ```  
  
    ```cpp  
    DataRelation^ myDataRelation;  
    myDataRelation = gcnew DataRelation("CustOrd",  
       ds->Tables["Customers"]->Columns["CustomerID"],  
       ds->Tables["Orders"]->Columns["CustomerID"]);  
    // Add the relation to the DataSet.  
    ds->Relations->Add(myDataRelation);  
    GridOrders->SetDataBinding(ds, "Customers");  
    GridDetails->SetDataBinding(ds, "Customers.CustOrd");  
    ```  
  
## <a name="see-also"></a>참고자료

- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
- [DataGrid 컨트롤 개요](datagrid-control-overview-windows-forms.md)
- [방법: Windows Forms DataGrid 컨트롤을 데이터 소스에 바인딩](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
