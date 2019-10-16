---
title: '방법: 관련 엔터티 로드 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, deferred content
- WCF Data Services, loading data
ms.assetid: 6f143d30-d997-4e6b-bcf0-d5c394ecb108
ms.openlocfilehash: 14b0ba988c96c270610208a4f944083bb333eac5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780020"
---
# <a name="how-to-load-related-entities-wcf-data-services"></a>방법: 관련 엔터티 로드 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에서 관련 엔터티를 로드해야 하는 경우 <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 클래스의 <xref:System.Data.Services.Client.DataServiceContext> 메서드를 사용할 수 있습니다. <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 또한<xref:System.Data.Services.Client.DataServiceQuery%601> 에서 메서드를 사용 하 여 관련 엔터티를 동일한 쿼리 응답에서 적극적으로 로드할 수 있습니다.  
  
 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스 및 클라이언트 데이터 클래스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 반환되는 각 `Customer` 인스턴스와 관련된 `Orders`를 명시적으로 로드하는 방법을 보여 줍니다.  
  
 [!code-csharp[Astoria Northwind Client#LoadRelatedOrderCustomer](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadrelatedordercustomer)]
 [!code-vb[Astoria Northwind Client#LoadRelatedOrderCustomer](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadrelatedordercustomer)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 메서드를 사용하여 쿼리에서 반환된 `Order Details`에 속하는 `Orders`를 반환하는 방법을 보여 줍니다.  
  
 [!code-csharp[Astoria Northwind Client#ExpandOrderDetails](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#expandorderdetails)]
 [!code-vb[Astoria Northwind Client#ExpandOrderDetails](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#expandorderdetails)]  
  
## <a name="see-also"></a>참고자료

- [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)
