---
title: DataView로 필터링(LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5632d74a-ff53-4ea7-9fe7-4a148eeb1c68
ms.openlocfilehash: 9cbd3d52c0e751097a937fa8781171c8c2a0058f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795051"
---
# <a name="filtering-with-dataview-linq-to-dataset"></a>DataView로 필터링(LINQ to DataSet)
특정 조건을 사용하여 데이터를 필터링한 다음 UI 컨트롤을 통해 클라이언트에 데이터를 제공하는 기능은 데이터 바인딩의 중요한 기능입니다. <xref:System.Data.DataView>에서는 데이터를 필터링하여 특정 필터 조건을 충족하는 데이터 행의 하위 집합을 반환하는 여러 가지 방법을 제공합니다. 문자열 기반 필터링 기능 <xref:System.Data.DataView> 뿐만 아니라 식을 필터링 조건에 사용 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 하는 기능도 제공 합니다. [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]식을 사용 하면 문자열 기반 필터링에 비해 더 복잡 하 고 강력한 필터링 작업을 수행할 수 있습니다.  
  
 <xref:System.Data.DataView>를 사용하여 데이터를 필터링하는 방법에는 두 가지가 있습니다.  
  
- Where 절 <xref:System.Data.DataView> 을 사용 하 여 LINQ to DataSet 쿼리에서를 만듭니다.  
  
- <xref:System.Data.DataView>의 기존 문자열 기반 필터링 기능을 사용합니다.  
  
## <a name="creating-dataview-from-a-query-with-filtering-information"></a>필터링 정보가 있는 쿼리에서 DataView 만들기  
 LINQ to DataSet <xref:System.Data.DataView> 쿼리에서 개체를 만들 수 있습니다. 해당 쿼리에 `Where` 절이 있으면 쿼리의 필터링 정보를 사용하여 <xref:System.Data.DataView>를 만듭니다. `Where` 절의 식은 <xref:System.Data.DataView>에 포함되는 데이터 행을 확인하는 데 사용되며 필터의 기본 요소입니다.  
  
 식 기반 필터는 간단한 문자열 기반 필터에 비해 강력하고 복잡한 필터링 기능을 제공합니다. 문자열 기반 필터와 식 기반 필터는 함께 사용할 수 없습니다. <xref:System.Data.DataView.RowFilter%2A>를 쿼리에서 만든 후에 문자열 기반 <xref:System.Data.DataView>를 설정하면 쿼리에서 유추된 식 기반 필터가 지워집니다.  
  
> [!NOTE]
> 대부분의 경우 필터링에 사용되는 식은 파생 작용이 없어야 하고 명확해야 합니다. 또한 필터링 작업이 여러 번 실행될 수 있으므로 식에는 실행 집합 번호에 따라 달라지는 논리가 없어야 합니다.  
  
### <a name="example"></a>예제  
 다음 예제에서는 SalesOrderDetail 테이블에 대해 수량이 2보다 크고 6보다 작은 주문을 쿼리한 다음 해당 쿼리에서 <xref:System.Data.DataView>를 만들고 <xref:System.Data.DataView>를 <xref:System.Windows.Forms.BindingSource>에 바인딩합니다.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 2001년 6월 6일 이후 주문에 대한 쿼리에서 <xref:System.Data.DataView>를 만듭니다.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere3)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere3)]  
  
### <a name="example"></a>예제  
 필터링을 정렬과 결합할 수도 있습니다. 다음 예제에서는 성이 "S"로 시작하는 연락처를 성과 이름순으로 정렬하는 쿼리에서 <xref:System.Data.DataView>를 만듭니다.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhereorderbythenby)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhereorderbythenby)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 SoundEx 알고리즘을 사용하여 성이 "Zhu"와 비슷한 연락처를 찾습니다. SoundEx 알고리즘은 SoundEx 메서드에서 구현됩니다.  
  
 [!code-csharp[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvsoundexfilter)]
 [!code-vb[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvsoundexfilter)]  
  
 U.S. Census Bureau에서 개발한 SoundEx는 영어 발음의 소리를 기준으로 이름을 인덱싱하는 데 사용되는 음성 있습니다. SoundEx 메서드는 하나의 영어 문자 뒤에 숫자 3개가 있는 형식으로 구성된 이름에 대한 4문자 코드를 반환합니다. 영어 문자는 이름의 첫 번째 문자이고 숫자는 이름의 나머지 자음을 인코딩합니다. 발음이 비슷한 이름은 같은 SoundEx 코드를 공유합니다. 이전 예제의 SoundEx 메서드에 사용된 SoundEx 구현은 다음과 같습니다.  
  
 [!code-csharp[DP DataView Samples#SoundEx](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#soundex)]
 [!code-vb[DP DataView Samples#SoundEx](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#soundex)]  
  
## <a name="using-the-rowfilter-property"></a>RowFilter 속성 사용  
 의 <xref:System.Data.DataView> 기존 문자열 기반 필터링 기능은 여전히 LINQ to DataSet 컨텍스트에서 작동 합니다. 문자열 기반 <xref:System.Data.DataView.RowFilter%2A> 필터링에 대 한 자세한 내용은 [데이터 정렬 및 필터링](./dataset-datatable-dataview/sorting-and-filtering-data.md)을 참조 하세요.  
  
 다음 예제에서는 Contact 테이블에서 <xref:System.Data.DataView>를 만든 다음 연락처의 성이 "Zhu"인 행을 반환하도록 <xref:System.Data.DataView.RowFilter%2A> 속성을 설정합니다.  
  
 [!code-csharp[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvrowfilter)]
 [!code-vb[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvrowfilter)]  
  
 또는 LINQ to DataSet <xref:System.Data.DataView> 쿼리에서를 만든 <xref:System.Data.DataView.RowFilter%2A> 후에는 속성을 사용 하 여 열 값을 기준으로 행의 하위 집합을 지정할 수 있습니다. <xref:System.Data.DataTable> 문자열 기반 필터와 식 기반 필터는 함께 사용할 수 없습니다. 속성을 <xref:System.Data.DataView.RowFilter%2A> 설정 하면 LINQ to DataSet 쿼리에서 유추 된 필터 식이 지워집니다. 필터 식은 다시 설정할 수 없습니다.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywheresetrowfilter)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywheresetrowfilter)]  
  
 데이터의 하위 집합에 대한 동적 뷰를 제공하는 것과는 반대로 데이터에 대한 특정 쿼리 결과를 반환하려는 경우 <xref:System.Data.DataView.Find%2A> 속성을 설정하는 대신 <xref:System.Data.DataView.FindRows%2A>의 <xref:System.Data.DataView> 또는 <xref:System.Data.DataView.RowFilter%2A> 메서드를 사용할 수 있습니다. <xref:System.Data.DataView.RowFilter%2A> 속성은 바인딩된 컨트롤이 필터링된 결과를 표시하는 데이터 바인딩된 애플리케이션에 가장 적합합니다. <xref:System.Data.DataView.RowFilter%2A> 속성을 설정하면 데이터의 인덱스가 다시 작성되므로 애플리케이션에 오버헤드가 발생하여 성능이 저하됩니다. <xref:System.Data.DataView.Find%2A> 및 <xref:System.Data.DataView.FindRows%2A> 메서드는 인덱스를 다시 작성하지 않고 현재 인덱스를 사용합니다. <xref:System.Data.DataView.Find%2A> 또는 <xref:System.Data.DataView.FindRows%2A>를 한 번만 호출할 경우에는 기존 <xref:System.Data.DataView>를 사용해야 합니다. <xref:System.Data.DataView.Find%2A> 또는 <xref:System.Data.DataView.FindRows%2A>를 여러 번 호출할 경우에는 새 <xref:System.Data.DataView>를 만들어서 검색하려는 열의 인덱스를 다시 작성한 다음 <xref:System.Data.DataView.Find%2A> 또는 <xref:System.Data.DataView.FindRows%2A> 메서드를 호출해야 합니다. <xref:System.Data.DataView.Find%2A> 및<xref:System.Data.DataView.FindRows%2A> 메서드에 대 한 자세한 내용은 행 및 [DataView 성능](dataview-performance.md) [찾기](./dataset-datatable-dataview/finding-rows.md) 를 참조 하십시오.  
  
## <a name="clearing-the-filter"></a>필터 지우기  
 필터링이 설정된 후 <xref:System.Data.DataView> 속성을 사용하여 <xref:System.Data.DataView.RowFilter%2A>의 필터를 지울 수 있습니다. <xref:System.Data.DataView>의 필터는 두 가지 방법으로 지울 수 있습니다.  
  
- <xref:System.Data.DataView.RowFilter%2A> 속성을 `null`으로 설정합니다.  
  
- <xref:System.Data.DataView.RowFilter%2A> 속성을 빈 문자열로 설정합니다.  
  
### <a name="example"></a>예제  
 다음 예제에서는 쿼리에서 <xref:System.Data.DataView>를 만든 다음 <xref:System.Data.DataView.RowFilter%2A> 속성을 `null`로 설정하여 필터를 지웁니다.  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter2)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter2)]  
  
### <a name="example"></a>예제  
 다음 예제에서는 테이블에서 <xref:System.Data.DataView>를 만들고, <xref:System.Data.DataView.RowFilter%2A> 속성을 설정한 다음 <xref:System.Data.DataView.RowFilter%2A> 속성을 빈 문자열로 설정하여 필터를 지웁니다.  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter)]  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 및 LINQ to DataSet](data-binding-and-linq-to-dataset.md)
- [DataView로 정렬](sorting-with-dataview-linq-to-dataset.md)
