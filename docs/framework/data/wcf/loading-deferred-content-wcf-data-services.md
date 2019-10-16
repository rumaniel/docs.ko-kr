---
title: 지연 콘텐츠 로드(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, deferred content
- WCF Data Services, loading data
ms.assetid: 32f9b588-c832-44c4-a7e0-fcce635df59a
ms.openlocfilehash: 7c53ad18e029dbe1f882035c1bffc8f4bfbaa2f9
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790416"
---
# <a name="loading-deferred-content-wcf-data-services"></a>지연 콘텐츠 로드(WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 기본적으로 쿼리에서 반환되는 데이터 양을 제한합니다. 그러나 필요한 경우 데이터 서비스에서 관련 엔터티, 페이징 응답 데이터 및 이진 데이터 스트림을 포함한 추가 데이터를 명시적으로 로드할 수 있습니다. 이 항목에서는 이러한 지연된 콘텐츠를 애플리케이션에 로드하는 방법을 설명합니다.  
  
## <a name="related-entities"></a>관련 엔터티  
 쿼리를 실행하면 주소가 지정된 엔터티 집합의 엔터티만 반환됩니다. 예를 들어, Northwind 데이터 서비스에 대한 쿼리가 `Customers` 엔터티를 반환하는 경우 `Orders` 및 `Customers` 간에 관계가 있어도 기본적으로 관련 `Orders` 엔터티가 반환되지 않습니다. 또한 데이터 서비스에서 페이징을 사용하도록 설정한 경우 서비스에서 이후 데이터 페이지를 명시적으로 로드해야 합니다. 관련 엔터티를 로드하는 방법에는 다음 두 가지가 있습니다.  
  
- **즉시 로드**: 쿼리 옵션을 사용 `$expand` 하 여 쿼리가 요청한 엔터티 집합에 대 한 연결과 관련 된 엔터티를 반환 하도록 요청할 수 있습니다. 데이터 서비스에 전송되는 쿼리에 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> 옵션을 추가하려면 <xref:System.Data.Services.Client.DataServiceQuery%601>의 `$expand` 메서드를 사용합니다. 다음 예제와 같이 관련 엔터티 집합을 쉼표로 구분하여 여러 개 요청할 수 있습니다. 쿼리에서 요청한 모든 엔터티가 하나의 응답으로 반환됩니다. 다음 예제에서는 `Order_Details` 엔터티 집합과 함께 `Customers` 및 `Orders`를 반환합니다.  
  
     [!code-csharp[Astoria Northwind Client#ExpandOrderDetailsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#expandorderdetailsspecific)]
     [!code-vb[Astoria Northwind Client#ExpandOrderDetailsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#expandorderdetailsspecific)]  
  
     [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에서는 `$expand` 쿼리 옵션을 사용하여 단일 쿼리에 포함할 수 있는 엔터티 집합의 수를 12개로 제한합니다.  
  
- **명시적 로드**: 인스턴스에 대해 메서드를 <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 호출 하 여 관련 엔터티를 명시적으로 로드할 수 있습니다. <xref:System.Data.Services.Client.DataServiceContext> <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 메서드를 호출할 때마다 데이터 서비스에 대해 별도의 요청이 만들어집니다. 다음 예제에서는 `Order_Details` 엔터티에 대한 `Orders`를 명시적으로 로드합니다.  
  
     [!code-csharp[Astoria Northwind Client#LoadRelatedOrderDetailsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadrelatedorderdetailsspecific)]
     [!code-vb[Astoria Northwind Client#LoadRelatedOrderDetailsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadrelatedorderdetailsspecific)]  
  
 사용할 옵션을 고려할 때는 데이터 서비스에 대한 요청 수와 하나의 응답으로 반환되는 데이터 양이 서로 상쇄되는 관계임을 염두에 두어야 합니다. 애플리케이션에 연결된 개체가 필요하지만 이러한 개체의 명시적 검색 요청에서 추가적인 지연이 발생하는 것을 피하려는 경우 즉시 로드를 사용합니다. 그러나 애플리케이션에 특정 관련 엔터티 인스턴스에 대한 데이터만 필요한 경우 <xref:System.Data.Services.Client.DataServiceContext.LoadProperty%2A> 메서드를 호출하여 이러한 엔터티를 명시적으로 로드하는 것을 고려해야 합니다. 자세한 내용은 [방법: 관련 엔터티](how-to-load-related-entities-wcf-data-services.md)를 로드 합니다.  
  
## <a name="paged-content"></a>페이징 콘텐츠  
 데이터 서비스에서 페이징을 사용하도록 설정한 경우 데이터 서비스가 반환하는 피드의 항목 수는 데이터 서비스의 구성에 의해 제한됩니다. 페이지 제한은 각 엔터티 집합에 대해 별도로 설정할 수 있습니다. 자세한 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)합니다. 페이징을 사용하도록 설정하면 피드의 최종 항목에 다음 데이터 페이지에 대한 링크가 포함됩니다. 이 링크는 <xref:System.Data.Services.Client.DataServiceQueryContinuation%601> 개체에 포함됩니다. <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A>를 실행할 때 반환되는 <xref:System.Data.Services.Client.QueryOperationResponse%601>의 <xref:System.Data.Services.Client.DataServiceQuery%601> 메서드를 호출하여 다음 데이터 페이지의 URI를 가져옵니다. 반환된 <xref:System.Data.Services.Client.DataServiceQueryContinuation%601> 개체는 다음 결과 페이지를 로드하는 데 사용됩니다. <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 메서드를 호출하기 전에 쿼리 결과를 열거해야 합니다. `do…while` 루프를 사용하여 쿼리 결과를 먼저 열거한 후 다음 `non-null` 링크 값을 확인하는 것이 좋습니다. <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 메서드에서 `null`(Visual Basic에서는 `Nothing`)을 반환하면 원래 쿼리에 대한 추가 결과 페이지가 없습니다. 다음 예제에서는 Northwind 샘플 데이터 서비스에서 페이징 고객 데이터를 로드하는 `do…while` 루프를 보여 줍니다.  
  
 [!code-csharp[Astoria Northwind Client#LoadNextLink](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadnextlink)]
 [!code-vb[Astoria Northwind Client#LoadNextLink](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadnextlink)]  
  
 쿼리에서 관련 엔터티가 요청된 엔터티 집합과 함께 단일 응답으로 반환되도록 요청하는 경우 페이징 제한이 응답에 인라인으로 포함된 중첩된 피드에 영향을 줄 수 있습니다. 예를 들어, Northwind 샘플 데이터 서비스에 `Customers` 엔터티 집합에 대한 페이징 제한이 설정되어 있는 경우 Northwind 샘플 데이터 서비스를 정의하는 Northwind.svc.cs 파일에서 다음 예제와 같이 관련 `Orders` 엔터티 집합에 대해 독립적인 페이징 제한을 설정할 수도 있습니다.  
  
 [!code-csharp[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind.svc.cs#dataserviceconfigpaging)]
 [!code-vb[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind.svc.vb#dataserviceconfigpaging)]  
  
 이 경우 최상위 `Customers`와 중첩된 `Orders` 엔터티 피드에 대해 모두 페이징을 구현해야 합니다. 다음 예제에서는 선택한 `while` 엔터티와 관련된 `Orders` 엔터티의 페이지를 로드하는 데 사용되는 `Customers` 루프를 보여 줍니다.  
  
 [!code-csharp[Astoria Northwind Client#LoadNextOrdersLink](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#loadnextorderslink)]
 [!code-vb[Astoria Northwind Client#LoadNextOrdersLink](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#loadnextorderslink)]  
  
 자세한 내용은 [방법: 페이지 단위 결과](how-to-load-paged-results-wcf-data-services.md)를 로드 합니다.  
  
## <a name="binary-data-streams"></a>이진 데이터 스트림  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 BLOB(Binary Large Object) 데이터를 데이터 스트림으로 액세스할 수 있습니다. 스트리밍을 사용하면 필요할 때까지 이진 데이터 로드가 지연되며, 클라이언트가 보다 효율적으로 이 데이터를 처리할 수 있습니다. 이 기능을 사용하려면 데이터 서비스에서 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 공급자를 구현해야 합니다. 자세한 내용은 [스트리밍 공급자](streaming-provider-wcf-data-services.md)합니다. 스트리밍을 사용하도록 설정하면 엔터티 형식이 관련 이진 데이터 없이 반환됩니다. 이 경우 <xref:System.Data.Services.Client.DataServiceContext.GetReadStream%2A> <xref:System.Data.Services.Client.DataServiceContext> 클래스의 메서드를 사용 하 여 서비스에서 이진 데이터에 대 한 데이터 스트림에 액세스 해야 합니다. 이와 유사하게, <xref:System.Data.Services.Client.DataServiceContext.SetSaveStream%2A> 메서드를 사용하여 엔터티의 이진 데이터를 스트림으로 추가하거나 변경할 수 있습니다. 자세한 내용은 [이진 데이터 작업](working-with-binary-data-wcf-data-services.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
- [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)
