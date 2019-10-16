---
title: DataView로 정렬(LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 885b3b7b-51c1-42b3-bb29-b925f4f69a6f
ms.openlocfilehash: 481a56f923c4218cd8689c578ce990785aee0ab3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782717"
---
# <a name="sorting-with-dataview-linq-to-dataset"></a>DataView로 정렬(LINQ to DataSet)
특정 조건을 기준으로 데이터를 정렬한 다음 UI 컨트롤을 통해 클라이언트에 데이터를 제공하는 기능은 데이터 바인딩의 중요한 기능입니다. <xref:System.Data.DataView>에서는 데이터를 정렬하여 특정 정렬 기준에 따라 정렬된 데이터 행을 반환하는 여러 방법을 제공합니다. 문자열 기반 정렬 기능 외에도를 <xref:System.Data.DataView> 사용 하 여 정렬 조건에 식을 사용할 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 수 있습니다. [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]식을 사용 하면 문자열 기반 정렬에 비해 더 복잡 하 고 강력한 정렬 작업을 수행할 수 있습니다. 이 항목에서는 <xref:System.Data.DataView>를 사용하여 정렬하는 두 가지 방법을 모두 설명합니다.  
  
## <a name="creating-dataview-from-a-query-with-sorting-information"></a>정렬 정보가 있는 쿼리에서 DataView 만들기  
 LINQ to DataSet <xref:System.Data.DataView> 쿼리에서 개체를 만들 수 있습니다. 해당 쿼리에 <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.OrderByDescending%2A>, <xref:System.Linq.Enumerable.ThenBy%2A> 또는 <xref:System.Linq.Enumerable.ThenByDescending%2A> 절이 있는 경우 이러한 절의 식은 <xref:System.Data.DataView>의 데이터를 정렬하기 위한 기본 요소로 사용됩니다. 예를 들어 쿼리에 `Order By…` 및 `Then By…` 절이 있는 경우 결과 <xref:System.Data.DataView>는 지정된 두 열을 기준으로 데이터를 정렬합니다.  
  
 식 기반 정렬은 간단한 문자열 기반 정렬에 비해 강력하고 복잡한 정렬 기능을 제공합니다. 문자열 기반 정렬 및 식 기반 정렬은 함께 사용할 수 없습니다. 쿼리에서 <xref:System.Data.DataView.Sort%2A>를 만든 후에 문자열 기반 <xref:System.Data.DataView>를 설정하면 쿼리에서 유추된 식 기반 필터가 지워지며, 이 필터는 재설정할 수 없습니다.  
  
 <xref:System.Data.DataView>의 인덱스는 <xref:System.Data.DataView>가 만들어지거나 정렬 또는 필터링 정보가 수정될 때 작성됩니다. 를 만든 LINQ to DataSet 쿼리에서 <xref:System.Data.DataView> 정렬 기준을 제공 하 고 나중에 정렬 정보를 수정 하지 않는 것이 가장 좋은 성능을 얻을 수 있습니다. 자세한 내용은 [DataView 성능](dataview-performance.md)을 참조 하세요.  
  
> [!NOTE]
> 대부분의 경우 정렬에 사용되는 식은 파생 효과가 없어야 하고 명확해야 합니다. 또한 정렬 작업이 여러 번 실행될 수 있으므로 이러한 식에는 실행 집합 번호에 따라 달라지는 논리가 없어야 합니다.  
  
### <a name="example"></a>예제  
 다음 예제에서는 SalesOrderHeader 테이블을 쿼리하여 반환된 행을 주문 날짜를 기준으로 정렬한 다음 해당 쿼리에서 <xref:System.Data.DataView>를 만들고 <xref:System.Data.DataView>를 <xref:System.Windows.Forms.BindingSource>에 바인딩합니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 SalesOrderHeader 테이블을 쿼리하여 반환된 행을 합계 금액을 기준으로 정렬한 다음 해당 쿼리에서 <xref:System.Data.DataView>를 만들고 <xref:System.Data.DataView>를 <xref:System.Windows.Forms.BindingSource>에 바인딩합니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby2)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby2)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 SalesOrderDetail 테이블을 쿼리하여 반환된 행을 주문 수량과 판매 주문 ID를 기준으로 정렬한 다음 해당 쿼리에서 <xref:System.Data.DataView>를 만들고 <xref:System.Data.DataView>를 <xref:System.Windows.Forms.BindingSource>에 바인딩합니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderbythenby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderbythenby)]  
  
## <a name="using-the-string-based-sort-property"></a>문자열 기반 정렬 속성 사용  
 의 <xref:System.Data.DataView> 문자열 기반 정렬 기능은 여전히 LINQ to DataSet와 함께 작동 합니다. LINQ to DataSet 쿼리에서 <xref:System.Data.DataView> 를 만든 후에는 <xref:System.Data.DataView.Sort%2A> 속성을 사용 하 여에 대 한 정렬을 <xref:System.Data.DataView>설정할 수 있습니다.  
  
 문자열 기반 정렬 및 식 기반 정렬 기능은 함께 사용할 수 없습니다. <xref:System.Data.DataView.Sort%2A> 속성을 설정하면 <xref:System.Data.DataView>가 만들어진 쿼리에서 상속된 식 기반 정렬이 지워집니다.  
  
 문자열 기반 <xref:System.Data.DataView.Sort%2A> 필터링에 대 한 자세한 내용은 [데이터 정렬 및 필터링](./dataset-datatable-dataview/sorting-and-filtering-data.md)을 참조 하세요.  
  
### <a name="example"></a>예제  
 다음 예제에서는 Contact 테이블에서 <xref:System.Data.DataView>를 만든 다음 성을 기준으로 내림차순으로 행을 정렬하고, 이름을 기준으로 오름차순으로 행을 정렬합니다.  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 Contact 테이블에 대해 &quot;S&quot;로 시작하는 성을 쿼리합니다.  해당 쿼리에서 <xref:System.Data.DataView>가 만들어지고 <xref:System.Windows.Forms.BindingSource> 개체에 바인딩됩니다.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## <a name="clearing-the-sort"></a>정렬 지우기  
 <xref:System.Data.DataView>의 정렬 정보는 설정된 후에 <xref:System.Data.DataView.Sort%2A> 속성을 사용하여 지울 수 있습니다. 두 가지 방법으로 <xref:System.Data.DataView>의 정렬 정보를 지울 수 있습니다.  
  
- <xref:System.Data.DataView.Sort%2A> 속성을 `null`으로 설정합니다.  
  
- <xref:System.Data.DataView.Sort%2A> 속성을 빈 문자열로 설정합니다.  
  
### <a name="example"></a>예제  
 다음 예제에서는 쿼리에서 <xref:System.Data.DataView>를 만든 다음 <xref:System.Data.DataView.Sort%2A> 속성을 빈 문자열로 설정하여 정렬을 지웁니다.  
  
 [!code-csharp[DP DataView Samples#LDVClearSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort)]
 [!code-vb[DP DataView Samples#LDVClearSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 Contact 테이블에서 <xref:System.Data.DataView>를 만든 다음 성을 기준으로 내림차순으로 정렬하도록 <xref:System.Data.DataView.Sort%2A> 속성을 설정합니다. 그런 다음 <xref:System.Data.DataView.Sort%2A> 속성을 `null`로 설정하여 정렬 정보를 지웁니다.  
  
 [!code-csharp[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort2)]
 [!code-vb[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort2)]  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 및 LINQ to DataSet](data-binding-and-linq-to-dataset.md)
- [DataView로 필터링](filtering-with-dataview-linq-to-dataset.md)
- [데이터 정렬](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb546145(v=vs.120))
