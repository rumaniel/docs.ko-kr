---
title: 데이터 서비스 업데이트(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, changing data
- WCF Data Services, client library
ms.assetid: 00d993be-ffed-4dea-baf7-6eea982cdb54
ms.openlocfilehash: 5cf7a6e563069e35a4ac0fe729a616dc1c56bdb5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779750"
---
# <a name="updating-the-data-service-wcf-data-services"></a>데이터 서비스 업데이트(WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트 라이브러리를 사용 하 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 여 피드를 사용 하는 경우 라이브러리는 피드의 항목을 클라이언트 데이터 서비스 클래스의 인스턴스로 변환 합니다. 이러한 데이터 서비스 클래스는 <xref:System.Data.Services.Client.DataServiceContext>가 속해 있는 <xref:System.Data.Services.Client.DataServiceQuery%601>를 사용하여 추적됩니다. 클라이언트는 <xref:System.Data.Services.Client.DataServiceContext>의 메서드를 사용하여 보고하는 엔터티의 변경 내용을 추적합니다. 클라이언트는 이러한 메서드를 사용하여 추가된 엔터티와 삭제된 엔터티를 추적하고 속성 값 또는 엔터티 인스턴스 간의 관계에 대한 변경 내용도 추적할 수 있습니다. 이렇게 추적된 변경 내용은 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 메서드를 호출할 때 REST 기반 작업으로 데이터 서비스에 전송됩니다.  
  
> [!NOTE]
> <xref:System.Data.Services.Client.DataServiceCollection%601>의 인스턴스를 사용하여 데이터를 컨트롤에 바인딩하는 경우 바인딩된 컨트롤의 데이터에 대한 변경 내용이 <xref:System.Data.Services.Client.DataServiceContext>에 자동으로 보고됩니다. 자세한 내용은 [컨트롤에 데이터 바인딩](binding-data-to-controls-wcf-data-services.md)합니다.  
  
## <a name="adding-modifying-and-changing-entities"></a>엔터티 추가, 수정 및 변경  
 Visual Studio의 **서비스 참조 추가** 대화 상자를 사용 하 여 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드에 대 한 참조를 추가 하는 경우 생성 되는 클라이언트 데이터 서비스 클래스에는 각각의 nullable이 아닌 엔터티 속성에 대해 하나의 매개 변수를 사용 하는 정적 *Create* 메서드가 있습니다. . 다음 예제와 같이 이 메서드를 사용하여 엔터티 형식 클래스 인스턴스를 만들 수 있습니다.  
  
 [!code-csharp[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#createnewproduct)]
 [!code-vb[Astoria Northwind Client#CreateNewProduct](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#createnewproduct)]  
  
 엔터티 인스턴스를 추가 하려면 다음 예제와 같이 **서비스 참조 추가** 대화 상자에 <xref:System.Data.Services.Client.DataServiceContext> 의해 생성 된 클래스에 대해 적절 한 *AddTo* 메서드를 호출 합니다.  
  
 [!code-csharp[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addproductspecific)]
 [!code-vb[Astoria Northwind Client#AddProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addproductspecific)]  
  
 이렇게 하면 컨텍스트와 올바른 엔터티 집합에 개체가 추가됩니다. <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>를 호출할 수도 있지만 대신 엔터티 집합 이름을 제공해야 합니다. 추가한 엔터티에 다른 엔터티와의 관계가 하나 이상 있는 경우 <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> 메서드를 사용하거나 이전 메서드 중 하나를 사용하고 해당 링크를 명시적으로 정의할 수 있습니다. 이러한 작업에 대해서는 이 항목의 뒷부분에서 설명합니다.  
  
 기존 엔터티 인스턴스를 수정하려면 다음 예제와 같이 먼저 해당 엔터티에 대해 쿼리하고 해당 속성을 원하는 대로 변경한 다음 <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A>의 <xref:System.Data.Services.Client.DataServiceContext> 메서드를 호출하여 해당 개체의 업데이트를 보내야 한다고 클라이언트 라이브러리에 알립니다.  
  
 [!code-csharp[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#modifycustomerspecific)]
 [!code-vb[Astoria Northwind Client#ModifyCustomerSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#modifycustomerspecific)]  
  
 엔터티 인스턴스를 삭제하려면 다음 예제와 같이 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A>의 <xref:System.Data.Services.Client.DataServiceContext> 메서드를 호출합니다.  
  
 [!code-csharp[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#deleteproductspecific)]
 [!code-vb[Astoria Northwind Client#DeleteProductSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#deleteproductspecific)]  
  
 자세한 내용은 [방법: 엔터티](how-to-add-modify-and-delete-entities-wcf-data-services.md)추가, 수정 및 삭제  
  
## <a name="attaching-entities"></a>엔터티 연결  
 클라이언트 라이브러리를 사용하면 먼저 쿼리를 실행하여 엔터티를 <xref:System.Data.Services.Client.DataServiceContext>로 로드하지 않고 엔터티 업데이트를 저장할 수 있습니다. <xref:System.Data.Services.Client.DataServiceContext.AttachTo%2A> 메서드를 사용하여 <xref:System.Data.Services.Client.DataServiceContext>의 특정 엔터티 집합에 기존 개체를 연결합니다. 그런 다음 개체를 수정하고 변경 내용을 데이터 서비스에 저장할 수 있습니다. 다음 예제에서는 변경된 고객 개체가 컨텍스트에 연결된 다음 <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A>가 호출되기 전에 <xref:System.Data.Services.Client.EntityStates.Modified>가 호출되어 연결된 개체를 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>로 표시합니다.  
  
 [!code-csharp[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#attachobjectspecific)]
 [!code-vb[Astoria Northwind Client#AttachObjectSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#attachobjectspecific)]  
  
 개체를 연결할 때는 다음 사항을 고려해야 합니다.  
  
- 개체는 <xref:System.Data.Services.Client.EntityStates.Unchanged> 상태로 연결됩니다.  
  
- 개체를 연결할 때 연결되는 개체와 관련된 개체는 연결되지 않습니다.  
  
- 엔터티가 컨텍스트에서 이미 추적되고 있는 경우에는 개체를 연결할 수 없습니다.  
  
- <xref:System.Data.Services.Client.DataServiceContext.AttachTo%28System.String%2CSystem.Object%2CSystem.String%29> 매개 변수를 사용하는 `etag` 메서드 오버로드는 eTag 값과 함께 받은 엔터티 개체를 연결할 때 사용됩니다. 이 eTag 값은 연결된 개체의 변경 내용을 저장할 때 동시성을 확인하는 데 사용됩니다.  
  
 자세한 내용은 [방법: 기존 엔터티를 DataServiceContext](attach-an-existing-entity-to-dc-wcf-data.md)에 연결 합니다.  
  
## <a name="creating-and-modifying-relationship-links"></a>관계 링크 만들기 및 수정  
 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 메서드 또는 **서비스 참조 추가** 대화 상자에서 생성 하는 <xref:System.Data.Services.Client.DataServiceContext> 클래스의 적절 한 *AddTo* 메서드를 사용 하 여 새 엔터티를 추가 하는 경우 새 엔터티와 관련 엔터티 간의 관계는 자동으로 정의 되지 않습니다.  
  
 엔터티 인스턴스 간의 관계를 만들고 변경할 수 있으며 클라이언트 라이브러리에서 이러한 변경 사항을 데이터 서비스에 반영하도록 지정할 수 있습니다. 엔터티 간의 관계는 모델에서 연결로 정의되며 <xref:System.Data.Services.Client.DataServiceContext>는 각 관계를 컨텍스트의 링크 개체로 추적합니다. [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 <xref:System.Data.Services.Client.DataServiceContext> 클래스에서 다음 메서드를 제공 하 여 이러한 링크를 만들고 수정 하 고 삭제 합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|<xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A>|관련된 두 엔터티 개체 간에 새 링크를 만듭니다. 이 메서드를 호출하는 것은 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>및 <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>를 호출하여 새로운 개체를 만들고 기존 개체에 대한 관계를 정의하는 것과 같습니다.|  
|<xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>|관련된 두 엔터티 개체 간에 새 링크를 만듭니다.|  
|<xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>|관련된 두 엔터티 개체 간의 기존 링크를 업데이트합니다. <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>는 또한 카디널리티가 0 또는 일대일(`0..1:1`)과 일대일 (`1:1`)인 링크를 삭제하는 데 사용합니다. 관련 개체를 `null`로 설정하여 링크를 업데이트할 수 있습니다.|  
|<xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A>|<xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 메서드가 호출될 때 컨텍스트에서 추적 중인 링크를 삭제하도록 표시합니다. 관련 개체를 삭제하거나 먼저 기존 개체에 대한 링크를 삭제한 후 새 관련 개체에 대한 링크를 추가하여 관계를 변경할 때 이 메서드를 사용합니다.|  
|<xref:System.Data.Services.Client.DataServiceContext.AttachLink%2A>|두 엔터티 개체 간의 기존 링크를 컨텍스트에 알립니다. 컨텍스트에서는 이 관계가 데이터 서비스에 이미 있다고 간주하고 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 메서드가 호출될 때 링크를 만들지 않습니다. 개체를 컨텍스트에 연결하고 둘 사이의 링크도 연결해야 하는 경우 이 메서드를 사용합니다. 새 관계를 정의하는 경우 <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A>를 대신 사용해야 합니다.|  
|<xref:System.Data.Services.Client.DataServiceContext.DetachLink%2A>|컨텍스트에서 지정된 링크 추적을 중지합니다. 이 메서드는 일대다( `*:*`) 관계를 삭제하는 데 사용됩니다. 1의 카디널리티를 가진 관계 링크의 경우 <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A>를 대신 사용해야 합니다.|  
  
 다음 예제에서는 <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> 메서드를 사용하여 기존 `Order_Detail` 엔터티와 관련된 새 `Orders`을 추가하는 방법을 보여 줍니다. 이제 새 `Order_Details` 개체가 <xref:System.Data.Services.Client.DataServiceContext>에서 추적되므로 추가한 `Order_Details` 개체와 기존 `Products` 엔터티 간의 관계는 <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> 메서드를 호출하여 정의됩니다.  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addorderdetailtoorderspecific)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addorderdetailtoorderspecific)]  
  
 <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> 메서드가 데이터 서비스에 만들어야 하는 링크를 정의하여 이러한 링크가 컨텍스트에 있는 개체에 반영되도록 하지만, 개체 자체의 탐색 속성은 사용자가 직접 설정해야 합니다. 위 예제에서는 다음과 같이 탐색 속성을 설정해야 합니다.  
  
 [!code-csharp[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#setnavprops)]
 [!code-vb[Astoria Northwind Client#SetNavProps](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#setnavprops)]  
  
 자세한 내용은 [방법: 엔터티 관계](how-to-define-entity-relationships-wcf-data-services.md)를 정의 합니다.  
  
## <a name="saving-changes"></a>변경 내용 저장  
 변경 내용이 <xref:System.Data.Services.Client.DataServiceContext> 인스턴스에서 추적되기는 하지만 서버로 즉시 전송되지는 않습니다. 지정한 작업에 대해 필요한 변경을 모두 마치면 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>를 호출하여 모든 변경 내용을 데이터 서비스에 전송합니다. 자세한 내용은 [데이터 서비스 컨텍스트 관리](managing-the-data-service-context-wcf-data-services.md)를 참조 하세요. <xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A> 및 <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A> 메서드를 사용하여 변경 내용을 비동기적으로 저장할 수도 있습니다. 자세한 내용은 [비동기 작업](asynchronous-operations-wcf-data-services.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
- [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)
- [비동기 작업](asynchronous-operations-wcf-data-services.md)
- [일괄 처리 작업](batching-operations-wcf-data-services.md)
- [개체 구체화](object-materialization-wcf-data-services.md)
- [데이터 서비스 컨텍스트 관리](managing-the-data-service-context-wcf-data-services.md)
