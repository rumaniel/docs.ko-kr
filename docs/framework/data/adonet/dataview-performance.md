---
title: DataView 성능
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 90820e49-9d46-41f6-9a3d-6c0741bbd8eb
ms.openlocfilehash: 51ea09965c423f04c220260248c3501e061820cb
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784145"
---
# <a name="dataview-performance"></a>DataView 성능
이 항목에서는 <xref:System.Data.DataView.Find%2A> 클래스의 <xref:System.Data.DataView.FindRows%2A> 및 <xref:System.Data.DataView> 메서드를 사용하여 웹 애플리케이션에서 <xref:System.Data.DataView>를 캐시할 때 얻을 수 있는 성능상의 이점에 대해 설명합니다.  
  
## <a name="find-and-findrows"></a>Find 및 FindRows  
 <xref:System.Data.DataView>는 인덱스를 구성합니다. 인덱스에는 테이블이나 뷰에 있는 하나 이상의 열로 작성되는 키가 포함됩니다. 이러한 키는 <xref:System.Data.DataView>를 사용하여 키 값과 연결된 행을 빠르고 효과적으로 찾을 수 있는 구조체에 저장됩니다. 필터링 및 정렬과 같이 인덱스를 사용 하는 연산은 상당한 성능 향상을 참조 하세요. <xref:System.Data.DataView>의 인덱스는 <xref:System.Data.DataView>가 만들어지거나 정렬 또는 필터링 정보가 수정될 때 작성됩니다. <xref:System.Data.DataView>를 만든 다음 정렬 또는 필터링 정보를 설정하면 <xref:System.Data.DataView>가 만들어질 때와 정렬 또는 필터 속성이 수정될 때 각각 한 번씩 인덱스가 작성되므로 적어도 두 개의 인덱스가 작성됩니다. 을 사용 <xref:System.Data.DataView>하 여 필터링 하 고 정렬 하는 방법에 대 한 자세한 내용은 [dataview를 사용 하 여 필터링](filtering-with-dataview-linq-to-dataset.md) 및 [dataview로 정렬](sorting-with-dataview-linq-to-dataset.md)  
  
 데이터의 하위 집합에 대한 동적 뷰를 제공하는 것과는 반대로 데이터에 대한 특정 쿼리 결과를 반환하려는 경우 <xref:System.Data.DataView.Find%2A> 속성을 설정하는 대신 <xref:System.Data.DataView.FindRows%2A>의 <xref:System.Data.DataView> 또는 <xref:System.Data.DataView.RowFilter%2A> 메서드를 사용할 수 있습니다. <xref:System.Data.DataView.RowFilter%2A> 속성은 바인딩된 컨트롤이 필터링된 결과를 표시하는 데이터 바인딩된 애플리케이션에 가장 적합합니다. <xref:System.Data.DataView.RowFilter%2A> 속성을 설정하면 데이터의 인덱스가 다시 작성되므로 애플리케이션에 오버헤드가 발생하여 성능이 저하됩니다. <xref:System.Data.DataView.Find%2A> 및 <xref:System.Data.DataView.FindRows%2A> 메서드는 인덱스를 다시 작성하지 않고 현재 인덱스를 사용합니다. <xref:System.Data.DataView.Find%2A> 또는 <xref:System.Data.DataView.FindRows%2A>를 한 번만 호출할 경우에는 기존 <xref:System.Data.DataView>를 사용해야 합니다. <xref:System.Data.DataView.Find%2A> 또는 <xref:System.Data.DataView.FindRows%2A>를 여러 번 호출할 경우에는 새 <xref:System.Data.DataView>를 만들어서 검색하려는 열의 인덱스를 다시 작성한 다음 <xref:System.Data.DataView.Find%2A> 또는 <xref:System.Data.DataView.FindRows%2A> 메서드를 호출해야 합니다. <xref:System.Data.DataView.Find%2A> 및<xref:System.Data.DataView.FindRows%2A> 메서드에 대 한 자세한 내용은 [행 찾기](./dataset-datatable-dataview/finding-rows.md)를 참조 하십시오.  
  
 다음 예제에서는 <xref:System.Data.DataView.Find%2A> 메서드를 사용하여 성이 "Zhu"인 연락처를 검색합니다.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryorderbyfind)]
 [!code-vb[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryorderbyfind)]  
  
 다음 예제에서는 <xref:System.Data.DataView.FindRows%2A> 메서드를 사용하여 모든 빨간색 제품을 검색합니다.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryfindrows)]
 [!code-vb[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryfindrows)]  
  
## <a name="aspnet"></a>ASP.NET  
 ASP.NET에는 만드는 데 많은 서버 자원이 필요한 개체를 메모리에 저장할 수 있는 캐시 메커니즘이 있습니다. 이러한 유형의 자원을 캐시하면 애플리케이션의 성능을 상당히 향상시킬 수 있습니다. 캐시는 <xref:System.Web.Caching.Cache> 클래스에 의해 각 애플리케이션에 개별적인 캐시 인스턴스로 구현됩니다. 새 <xref:System.Data.DataView> 개체를 만들면 많은 자원이 소요될 수 있으므로 웹 애플리케이션에서 이 캐시 기능을 사용하면 웹 페이지를 새로 고칠 때마다 <xref:System.Data.DataView>를 다시 작성하지 않도록 할 수 있습니다.  
  
 다음 예제에서는 <xref:System.Data.DataView>가 캐시되기 때문에 페이지가 새로 고쳐질 때 데이터를 다시 정렬하지 않아도 됩니다.  
  
```vb  
If (Cache("ordersView") = Nothing) Then  
  
Dim dataSet As New DataSet()  
  
   FillDataSet(dataSet)  
  
   Dim orders As DataTable = dataSet.Tables("SalesOrderHeader")  
  
   Dim query = _  
                    From order In orders.AsEnumerable() _  
                    Where order.Field(Of Boolean)("OnlineOrderFlag") = True _  
                    Order By order.Field(Of Decimal)("TotalDue") _  
                    Select order  
  
   Dim view As DataView = query.AsDataView()  
  
   Cache.Insert("ordersView", view)  
  
End If  
  
Dim ordersView = CType(Cache("ordersView"), DataView)  
  
GridView1.DataSource = ordersView  
GridView1.DataBind()  
```  
  
```csharp  
if (Cache["ordersView"] == null)  
{  
   // Fill the DataSet.                  
   DataSet dataSet = FillDataSet();  
  
   DataTable orders = dataSet.Tables["SalesOrderHeader"];  
  
   EnumerableRowCollection<DataRow> query =  
                        from order in orders.AsEnumerable()  
                        where order.Field<bool>("OnlineOrderFlag") == true  
                        orderby order.Field<decimal>("TotalDue")  
                        select order;  
  
   DataView view = query.AsDataView();  
   Cache.Insert("ordersView", view);  
}  
  
DataView ordersView = (DataView)Cache["ordersView"];  
  
GridView1.DataSource = ordersView;  
GridView1.DataBind();  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 및 LINQ to DataSet](data-binding-and-linq-to-dataset.md)
