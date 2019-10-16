---
title: 데이터 서비스 컨텍스트 관리(WCF Data Services)
ms.date: 03/30/2017
ms.assetid: 15b19d09-7de7-4638-9556-6ef396cc45ec
ms.openlocfilehash: 0278e8c31ffa7e9aaab5960c71cee091c9ea586a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779863"
---
# <a name="managing-the-data-service-context-wcf-data-services"></a>데이터 서비스 컨텍스트 관리(WCF Data Services)
<xref:System.Data.Services.Client.DataServiceContext> 클래스는 지정한 데이터 서비스에 대해 지원되는 작업을 캡슐화합니다. [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 서비스는 상태 비저장 특성을 갖지만 컨텍스트는 그렇지 않습니다. 따라서 변경 관리 등의 기능 <xref:System.Data.Services.Client.DataServiceContext> 을 지원 하기 위해 클래스를 사용 하 여 데이터 서비스와의 상호 작용 간에 클라이언트의 상태를 유지할 수 있습니다. 또한 이 클래스는 ID를 관리하고 변경 내용을 추적합니다.  
  
## <a name="merge-options-and-identity-resolution"></a>병합 옵션 및 ID 확인  
 <xref:System.Data.Services.Client.DataServiceQuery%601>가 실행되면 응답 피드의 엔터티가 개체로 구체화됩니다. 자세한 내용은 [개체 구체화](object-materialization-wcf-data-services.md)를 참조 하세요. 응답 메시지의 항목이 개체로 구체화되는 방법은 ID 확인에 따라 수행되며 쿼리가 실행된 병합 옵션에 따라 달라집니다. 여러 쿼리 또는 로드 요청이 단일 <xref:System.Data.Services.Client.DataServiceContext>의 범위에서 실행되는 경우 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트는 특정 키 값이 있는 개체의 단일 인스턴스만 추적합니다. ID 확인을 수행하는 데 사용되는 이 키는 엔터티를 고유하게 식별합니다.  
  
 기본적으로 클라이언트는 응답 피드의 항목을 <xref:System.Data.Services.Client.DataServiceContext>에 의해 추적되지 않는 엔터티의 개체로만 구체화합니다. 즉, 캐시에 이미 있는 개체의 변경 내용이 덮어쓰여지지 않습니다. 쿼리 및 로드 작업에 <xref:System.Data.Services.Client.MergeOption> 값을 지정하여 이 동작을 제어합니다. 이 옵션은 <xref:System.Data.Services.Client.DataServiceContext.MergeOption%2A>에서 <xref:System.Data.Services.Client.DataServiceContext> 속성을 설정하여 지정합니다. 기본 병합 옵션 값은 <xref:System.Data.Services.Client.MergeOption.AppendOnly>입니다. 이 경우 추적되지 않는 엔터티의 개체만 구체화되므로 기존 개체는 덮어쓰여지지 않습니다. 클라이언트의 개체에 대한 변경 내용이 데이터 서비스의 업데이트에 의해 덮어쓰여지지 않도록 하는 다른 방법은 <xref:System.Data.Services.Client.MergeOption.PreserveChanges>를 지정하는 것입니다. <xref:System.Data.Services.Client.MergeOption.OverwriteChanges>를 지정하면 클라이언트의 개체 값은 해당 개체가 이미 변경된 경우에도 응답 피드에 있는 항목의 최신 값으로 대체됩니다. <xref:System.Data.Services.Client.MergeOption.NoTracking> 병합 옵션을 사용하는 경우 <xref:System.Data.Services.Client.DataServiceContext>는 클라이언트 개체의 변경 내용을 데이터 서비스에 보낼 수 없습니다. 이 옵션을 사용하면 변경 내용이 항상 데이터 서비스의 값으로 덮어쓰여집니다.  
  
## <a name="managing-concurrency"></a>동시성 관리  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]는 데이터 서비스에서 업데이트 충돌을 감지할 수 있도록 하는 낙관적 동시성을 지원 합니다. 데이터 서비스에서 동시성 토큰을 사용하여 엔터티의 변경 내용을 확인하는 방식으로 데이터 서비스 공급자를 구성할 수 있습니다. 이 토큰에는 리소스 변경 여부를 확인하기 위해 데이터 서비스에서 유효성이 검사되는 엔터티 형식의 속성이 하나 이상 포함됩니다. 데이터 서비스에 대 한 요청 및 응답의 eTag 헤더에 포함 된 동시성 토큰은 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 클라이언트에서 관리 됩니다. 자세한 내용은 [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)를 참조 하세요.  
  
 <xref:System.Data.Services.Client.DataServiceContext>는 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>, <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> 및 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A>를 사용하거나 <xref:System.Data.Services.Client.DataServiceCollection%601>에 의해 수동으로 보고된 개체의 변경 내용을 추적합니다. <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 메서드가 호출되면 클라이언트가 변경 내용을 데이터 서비스에 보냅니다. <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>는 클라이언트의 데이터 변경 내용이 데이터 서비스의 변경 내용과 충돌하는 경우 실패할 수 있습니다. 이러한 경우에는 엔터티 리소스에 대한 쿼리를 다시 실행하여 업데이트 데이터를 받아야 합니다. 데이터 서비스의 변경 내용을 덮어쓰려면 <xref:System.Data.Services.Client.MergeOption.PreserveChanges> 병합 옵션을 사용하여 쿼리를 실행합니다. <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>를 다시 호출하면 데이터 서비스의 해당 리소스에 다른 변경이 이미 수행되지 않은 경우 클라이언트에 유지된 변경 내용이 데이터 서비스에 유지됩니다.  
  
## <a name="saving-changes"></a>변경 내용 저장  
 변경 내용이 <xref:System.Data.Services.Client.DataServiceContext> 인스턴스에서 추적되기는 하지만 서버로 즉시 전송되지는 않습니다. 지정한 작업에 대해 필요한 변경을 모두 마치면 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>를 호출하여 모든 변경 내용을 데이터 서비스에 전송합니다. <xref:System.Data.Services.Client.DataServiceResponse> 작업이 완료된 후에는 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 개체가 반환됩니다. <xref:System.Data.Services.Client.DataServiceResponse> 개체는 유지되거나 시도된 변경 내용을 나타내는 <xref:System.Data.Services.Client.OperationResponse> 또는 <xref:System.Data.Services.Client.EntityDescriptor> 인스턴스의 시퀀스가 차례로 포함되는 <xref:System.Data.Services.Client.LinkDescriptor> 개체의 시퀀스를 포함합니다. 데이터 서비스에서 엔터티를 만들거나 수정하면 <xref:System.Data.Services.Client.EntityDescriptor>에는 위 예제에서 생성된 `ProductID` 값과 같은 서버에서 생성된 속성 값을 포함하여 업데이트된 엔터티에 대한 참조가 포함됩니다. 클라이언트 라이브러리에서는 .NET Framework 개체를 자동으로 이러한 새 값으로 업데이트합니다.  
  
 성공적인 삽입 및 업데이트 작업을 위해 해당 작업과 연결된 <xref:System.Data.Services.Client.EntityDescriptor> 또는 <xref:System.Data.Services.Client.LinkDescriptor> 개체의 상태 속성은 <xref:System.Data.Services.Client.EntityStates.Unchanged>로 설정되고 새 값은 <xref:System.Data.Services.Client.MergeOption.OverwriteChanges>를 통해 병합됩니다. 데이터 서비스에서 삽입, 업데이트 또는 삭제 작업이 실패하면 엔터티 상태는 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>가 호출되기 전과 동일하게 유지되며, <xref:System.Data.Services.Client.OperationResponse.Error%2A>의 <xref:System.Data.Services.Client.OperationResponse> 속성은 오류 정보가 포함된 <xref:System.Data.Services.Client.DataServiceRequestException>으로 설정됩니다. 자세한 내용은 [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)를 참조 하세요.  
  
### <a name="setting-the-http-method-for-updates"></a>업데이트를 위한 HTTP 메서드 설정  
 기본적으로 .NET Framework 클라이언트 라이브러리는 기존 엔터티에 대한 업데이트를 MERGE 요청으로 보냅니다. 병합 요청은 엔터티의 선택된 속성을 업데이트하지만 클라이언트는 항상 병합 요청에 변경되지 않은 속성을 비롯하여 모든 속성을 포함합니다. 또한 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 프로토콜은 PUT 요청을 보내 엔터티를 업데이트하도록 지원합니다. PUT 요청에서 기존 엔터티는 클라이언트의 속성 값이 있는 엔터티의 새로운 인스턴스로 바뀝니다. PUT 요청을 사용하려면 <xref:System.Data.Services.Client.SaveChangesOptions.ReplaceOnUpdate>를 호출할 때 <xref:System.Data.Services.Client.SaveChangesOptions> 열거에 대한 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 플래그를 설정합니다.  
  
> [!NOTE]
> 클라이언트가 엔터티의 모든 속성에 대해 인식하지 못하는 경우 PUT 요청은 MERGE 요청과 다르게 동작합니다. 엔터티 형식을 클라이언트의 새로운 유형으로 프로젝션할 때 이런 상황이 발생할 수 있습니다. 또한 새로운 속성이 서비스 데이터 모델의 엔터티에 추가되고 <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A>의 <xref:System.Data.Services.Client.DataServiceContext> 속성이 `true`로 설정되어 이러한 클라이언트 매핑 오류를 무시하는 경우에도 이런 상황이 발생할 수 있습니다. 이런 경우 PUT 요청이 클라이언트에 알려지지 않은 모든 속성을 기본값으로 다시 설정합니다.  
  
### <a name="post-tunneling"></a>POST 터널링  
 기본적으로 클라이언트 라이브러리는 POST, GET, PUT/MERGE/PATCH 및 DELETE의 해당 HTTP 메서드를 사용하여 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 서비스에 대한 생성, 읽기, 업데이트 및 삭제 요청을 보냅니다. 이는 REST(Representational State Transfer) 기본 원칙을 준수합니다. 그러나, 모든 웹 서버 구현이 전체 HTTP 메서드 집합을 지원하는 것은 아닙니다. 경우에 따라 지원되는 메서드가 GET 및 POST로만 제한될 수 있습니다. 이는 방화벽 같은 매개자가 특정 메서드를 사용하여 요청을 차단할 경우 발생할 수 있습니다. GET 및 POST 메서드가 가장 많이 지원되는 메서드이기 때문에 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]는 POST 요청을 사용하여 지원되지 않는 모든 HTTP 메서드를 실행하는 방법을 지정합니다. *메서드 터널링* 또는 *사후 터널링*이라고 하는이를 통해 클라이언트는 사용자 지정 `X-HTTP-Method` 헤더에 지정 된 실제 메서드를 사용 하 여 POST 요청을 보낼 수 있습니다. 요청에 대해 POST 터널링을 사용하도록 설정하려면 <xref:System.Data.Services.Client.DataServiceContext.UsePostTunneling%2A> 인스턴스의 <xref:System.Data.Services.Client.DataServiceContext> 속성을 `true`로 설정합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF Data Services 클라이언트 라이브러리](wcf-data-services-client-library.md)
- [데이터 서비스 업데이트](updating-the-data-service-wcf-data-services.md)
- [비동기 작업](asynchronous-operations-wcf-data-services.md)
- [일괄 처리 작업](batching-operations-wcf-data-services.md)
