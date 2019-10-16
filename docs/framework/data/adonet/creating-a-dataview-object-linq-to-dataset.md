---
title: DataView 개체 만들기(LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 76057508-e12d-4779-a707-06a4c2568acf
ms.openlocfilehash: 054898a3520cbc2b607fc26b94b72b9896ad9c71
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786689"
---
# <a name="creating-a-dataview-object-linq-to-dataset"></a>DataView 개체 만들기(LINQ to DataSet)
LINQ to DataSet 컨텍스트에서를 만드는 방법에는 <xref:System.Data.DataView> 두 가지가 있습니다. 에 <xref:System.Data.DataTable> <xref:System.Data.DataView> 대한LINQtoDataSet쿼리에서를만들거나형식화되거나형식화되지않은에서만들수있습니다.<xref:System.Data.DataTable> 두 경우 모두 <xref:System.Data.DataTableExtensions.AsDataView%2A> 확장 메서드 중 하나 <xref:System.Data.DataView> 를 사용 하 여를 만듭니다. <xref:System.Data.DataView> 는 LINQ to DataSet 컨텍스트에서 직접 생성 가능 되지 않습니다.  
  
 <xref:System.Data.DataView>를 만든 후에 Windows Forms 애플리케이션 또는 ASP.NET 애플리케이션의 UI 컨트롤에 바인딩하거나 필터링 및 정렬 설정을 변경할 수 있습니다.  
  
 <xref:System.Data.DataView>에서 만든 인덱스는 필터링 및 정렬과 같이 인덱스를 사용할 수 있는 작업의 성능을 크게 높여 줍니다. <xref:System.Data.DataView>의 인덱스는 <xref:System.Data.DataView>가 만들어지거나 정렬 또는 필터링 정보가 수정될 때 작성됩니다. <xref:System.Data.DataView>를 만든 다음 정렬 또는 필터링 정보를 설정하면 <xref:System.Data.DataView>가 만들어질 때와 정렬 또는 필터 속성이 수정될 때 각각 한 번씩 인덱스가 작성되므로 적어도 두 개의 인덱스가 작성됩니다.  
  
 을 사용 <xref:System.Data.DataView>하 여 필터링 하 고 정렬 하는 방법에 대 한 자세한 내용은 [dataview를 사용 하 여 필터링](filtering-with-dataview-linq-to-dataset.md) 및 [dataview로 정렬](sorting-with-dataview-linq-to-dataset.md)  
  
## <a name="creating-dataview-from-a-linq-to-dataset-query"></a>LINQ to DataSet 쿼리에서 DataView 만들기  
 LINQ to DataSet 쿼리의 결과에서 <xref:System.Data.DataRow> 개체를만들수있습니다.여기서결과는개체의프로젝션입니다.<xref:System.Data.DataView> 새로 만들어진 <xref:System.Data.DataView>는 자신을 만든 쿼리의 필터링 및 정렬 정보를 상속합니다.  
  
> [!NOTE]
> 대부분의 경우 필터링 및 정렬에 사용되는 식은 파생 효과가 없어야 하고 명확해야 합니다. 또한 정렬 및 필터링 작업이 여러 번 실행될 수 있으므로 이러한 식에는 실행 집합 번호에 따라 달라지는 논리가 없어야 합니다.  
  
 익명 형식을 반환하는 쿼리 또는 조인 연산을 수행하는 쿼리에서는 <xref:System.Data.DataView>를 만들 수 없습니다.  
  
 <xref:System.Data.DataView>를 만드는 데 사용하는 쿼리에서는 다음과 같은 쿼리 연산자만 지원됩니다.  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Cast%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.OrderBy%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.OrderByDescending%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.ThenBy%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.ThenByDescending%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Where%2A>  
  
 LINQ to DataSet 쿼리에서을 <xref:System.Data.DataView> 만드는 경우 메서드는 <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A> 쿼리에서 호출 된 마지막 메서드 여야 합니다. 다음 예제에서는이를 보여 줍니다. 다음 예제에서는 <xref:System.Data.DataView> 온라인 주문 합계를 기준으로 정렬 된를 만듭니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquery1)]
 [!code-vb[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquery1)]  
  
 문자열 기반 <xref:System.Data.DataView.RowFilter%2A> 및 <xref:System.Data.DataView.Sort%2A> 속성을 사용 하 여 쿼리를 만든 후에 <xref:System.Data.DataView> 필터링 하 고 정렬할 수도 있습니다. 이렇게 하면 쿼리에서 상속된 정렬 및 필터링 정보가 지워집니다. 다음 예에서는 ' ' <xref:System.Data.DataView> 로 시작 하는 성을 기준으로 필터링 하는 LINQ to DataSet 쿼리에서를 만듭니다. 성을 기준으로 오름차순으로 정렬한 다음 이름을 기준으로 내림차순으로 정렬하도록 문자열 기반 <xref:System.Data.DataView.Sort%2A> 속성을 설정합니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## <a name="creating-a-dataview-from-a-datatable"></a>DataTable에서 DataView 만들기  
 LINQ to DataSet 쿼리에서 만드는 것 외에도 <xref:System.Data.DataView> <xref:System.Data.DataTableExtensions.AsDataView%2A> 메서드를 사용 하 <xref:System.Data.DataTable> 여에서 개체를 만들 수 있습니다.  
  
 다음 예제에서는 SalesOrderDetail 테이블에서 <xref:System.Data.DataView>를 만든 다음 <xref:System.Windows.Forms.BindingSource> 개체의 데이터 소스로 설정합니다. 이 개체는 <xref:System.Windows.Forms.DataGridView> 컨트롤에 대한 프록시 역할을 합니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromtable)]
 [!code-vb[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromtable)]  
  
 <xref:System.Data.DataView>에서 만들어진 <xref:System.Data.DataTable>에 필터링 및 정렬을 설정할 수 있습니다. 다음 예제에서는 Contact 테이블에서 <xref:System.Data.DataView>를 만든 다음 성을 기준으로 오름차순으로 정렬하고, 이름을 기준으로 내림차순으로 정렬하도록 <xref:System.Data.DataView.Sort%2A> 속성을 설정합니다.  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
 그러나 쿼리에서 <xref:System.Data.DataView.RowFilter%2A>를 만든 후에 <xref:System.Data.DataView.Sort%2A> 또는 <xref:System.Data.DataView> 속성을 설정하면 필터링 및 정렬 작업을 지원하기 위해 <xref:System.Data.DataView>에서 인덱스가 생성되므로 성능이 저하됩니다. <xref:System.Data.DataView.RowFilter%2A> 또는 <xref:System.Data.DataView.Sort%2A> 속성을 설정하면 데이터에 대한 인덱스가 다시 작성되므로 애플리케이션에 오버헤드가 발생하여 성능이 저하됩니다. 가능하면 <xref:System.Data.DataView>를 처음 만들 때 필터링 및 정렬 정보를 지정하고 이후에는 수정하지 않는 것이 좋습니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 및 LINQ to DataSet](data-binding-and-linq-to-dataset.md)
- [DataView로 필터링](filtering-with-dataview-linq-to-dataset.md)
- [DataView로 정렬](sorting-with-dataview-linq-to-dataset.md)
