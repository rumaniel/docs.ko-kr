---
title: '방법: 일괄 처리에서 쿼리 실행 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, batch requests
ms.assetid: 3b4db7df-bd33-43a1-8ea4-63a18e131f97
ms.openlocfilehash: a825fe83ff62d935740fb69871ba2d1e2120e9ec
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790497"
---
# <a name="how-to-execute-queries-in-a-batch-wcf-data-services"></a>방법: 일괄 처리에서 쿼리 실행 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리를 사용 하 여 단일 일괄 처리로 데이터 서비스에 대해 둘 이상의 쿼리를 실행할 수 있습니다. 자세한 내용은 [일괄 처리 작업](batching-operations-wcf-data-services.md)을 참조 하세요.  
  
 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스 및 클라이언트 데이터 클래스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Northwind 데이터 서비스에서 <xref:System.Data.Services.Client.DataServiceContext.ExecuteBatch%2A> 개체와 <xref:System.Data.Services.Client.DataServiceRequest%601> 개체를 모두 반환하는 쿼리가 포함된 `Customers` 개체 배열을 실행하는 `Products` 메서드를 호출하는 방법을 보여 줍니다. 반환된 <xref:System.Data.Services.Client.QueryOperationResponse%601>의 <xref:System.Data.Services.Client.DataServiceResponse> 개체 컬렉션이 열거되고 각 <xref:System.Data.Services.Client.QueryOperationResponse%601>에 포함되어 있는 개체 컬렉션도 열거됩니다.  
  
 [!code-csharp[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#batchquery)]
 [!code-vb[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#batchquery)]  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
