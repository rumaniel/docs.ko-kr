---
title: 데이터를 데이터 세트에 로드
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a53e5dc1-9669-49d4-828d-efa633237066
ms.openlocfilehash: 53f0f5a589a0033c9612f0465dff090ab04e3fc4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794949"
---
# <a name="loading-data-into-a-dataset"></a>데이터를 데이터 세트에 로드
LINQ to DataSet <xref:System.Data.DataSet> 를 사용 하 여 쿼리 하려면 먼저 개체를 채워야 합니다. <xref:System.Data.DataSet>은 여러 방법으로 채울 수 있습니다. 예를 들어, [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)]를 사용하여 데이터베이스를 쿼리한 다음 그 결과를 <xref:System.Data.DataSet>에 로드할 수 있습니다. 자세한 내용은 [LINQ to SQL](./sql/linq/index.md)을 참조하세요.  
  
 <xref:System.Data.DataSet>에 데이터를 로드하는 일반적인 방법 중에는 <xref:System.Data.Common.DataAdapter> 클래스를 사용하여 데이터베이스에서 데이터를 검색하는 방법도 있습니다. 다음 예에서 확인할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 <xref:System.Data.Common.DataAdapter>를 사용하여 AdventureWorks 데이터베이스에서 2002년 판매 정보를 쿼리한 다음 그 결과를 <xref:System.Data.DataSet>에 로드합니다. <xref:System.Data.DataSet> 을 채운 후 LINQ to DataSet를 사용 하 여 쿼리를 작성할 수 있습니다. 이 예제의 `FillDataSet`메서드는 [LINQ to DataSet 예제](linq-to-dataset-examples.md)에서 예제 쿼리에 사용됩니다. 자세한 내용은 [데이터 집합 쿼리](querying-datasets-linq-to-dataset.md)를 참조 하세요.  
  
 [!code-csharp[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#filldataset)]
 [!code-vb[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#filldataset)]  
  
## <a name="see-also"></a>참고자료

- [LINQ to DataSet 개요](linq-to-dataset-overview.md)
- [데이터 집합 쿼리](querying-datasets-linq-to-dataset.md)
- [LINQ to DataSet 예제](linq-to-dataset-examples.md)
