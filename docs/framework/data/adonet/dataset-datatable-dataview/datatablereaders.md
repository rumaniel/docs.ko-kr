---
title: DataTableReader
ms.date: 03/30/2017
ms.assetid: 97546ae2-0e42-4d26-961d-e0b244d81ded
ms.openlocfilehash: 1559cde9cb786ccb2baf920347064b8b28d472c3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785349"
---
# <a name="datatablereaders"></a>DataTableReader
<xref:System.Data.DataTableReader>는 <xref:System.Data.DataTable> 또는 <xref:System.Data.DataSet>의 내용을 하나 이상의 정방향 읽기 전용 결과 집합 형태로 제공합니다.  
  
 **Datatable**에서 **DataTableReader** 를 만들 때 결과 **DataTableReader** 개체에는로 표시 된 행을 제외 하 고 생성 된 **datatable** 과 동일한 데이터가 포함 된 결과 집합이 하나 포함 됩니다. deleted. 열은 원래 **DataTable**과 동일한 순서로 표시 됩니다.  
  
 을 호출 <xref:System.Data.DataSet.CreateDataReader%2A>하 여 생성 된 경우 DataTableReader에는 여러 개의 결과 집합이 포함 될 수 있습니다. 결과는 **DataSet** 개체의 <xref:System.Data.DataSet.Tables%2A> 컬렉션에 있는 **datatable** 의 순서와 동일 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [DataReader 만들기](creating-a-datareader.md)  
 **DataTableReader** 개체를 만드는 방법을 설명 합니다.  
  
 [DataTable 탐색](navigating-datatables.md)  
 **Read** 메서드를 사용 하 여 **DataTableReader**의 콘텐츠를 이동 하는 방법을 설명 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET에서 데이터 검색 및 수정](../retrieving-and-modifying-data.md)
- [ADO.NET 개요](../ado-net-overview.md)
