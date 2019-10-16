---
title: DataTable 탐색
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 202026a1-ec79-435e-b507-12a77f5011b2
ms.openlocfilehash: 5008f8397b7d396b14fdfe8e24f1e59785c4319d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785259"
---
# <a name="navigating-datatables"></a>DataTable 탐색
<xref:System.Data.DataTableReader>는 하나 이상의 <xref:System.Data.DataTable> 개체 내용을 하나 이상의 앞으로만 이동 가능한 읽기 전용 결과 집합 형태로 가져옵니다.  
  
 <xref:System.Data.DataTableReader> 메서드를 사용하여 <xref:System.Data.DataSet.CreateDataReader%2A>를 만들 경우에는 여러 개의 결과 집합이 포함될 수 있습니다. 결과 집합이 둘 이상이면 <xref:System.Data.DataTableReader.NextResult%2A> 메서드는 커서를 다음 결과 집합으로 이동합니다. 이것은 앞으로만 이동 가능한 프로세스이며, 이전 결과 집합으로 돌아갈 수는 없습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서 메서드는 `TestConstructor` 두 개의 <xref:System.Data.DataTable> 인스턴스를 만듭니다. 이 샘플은 <xref:System.Data.DataTableReader> 클래스에 대 한이 생성자를 보여 주기 위해 두 **datatable**포함 된 배열을 기반으로 하는 새 **DataTableReader** 을 만들고 간단한 작업을 수행 하 여 처음 몇 개에서 콘텐츠를 인쇄 합니다. 콘솔 창에 열을 추가할 수 있습니다.  
  
 [!code-csharp[DataWorks DataTableReader.NextResult#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTableReader.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks DataTableReader.NextResult#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTableReader.NextResult/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [DataTableReader](datatablereaders.md)
- [ADO.NET 개요](../ado-net-overview.md)
