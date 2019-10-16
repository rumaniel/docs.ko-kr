---
title: '방법: 등록하지 않고 Windows Communication Foundation 서비스 모니커 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], service monikers without registration
ms.assetid: ee3cf5c0-24f0-4ae7-81da-73a60de4a1a8
ms.openlocfilehash: 16f428b614fe331faffabab477c6584fb682801d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955239"
---
# <a name="how-to-use-the-windows-communication-foundation-service-moniker-without-registration"></a>방법: 등록하지 않고 Windows Communication Foundation 서비스 모니커 사용
Wcf (Windows Communication Foundation) 서비스에 연결 하 고 통신 하려면 WCF 클라이언트 응용 프로그램에 서비스 주소, 바인딩 구성 및 서비스 계약에 대 한 세부 정보가 있어야 합니다.  
  
 WCF 서비스 모니커는 일반적으로 필수 특성 형식의 이전 등록을 통해 필요한 계약을 가져오지만이 방법이 적합 하지 않은 경우도 있습니다. 등록 대신 모니커는 `wsdl` 매개 변수 사용, 메타데이터 교환 또는 `mexAddress` 매개 변수 사용을 통해 계약 정의를 WSDL(웹 서비스 기술 언어) 문서의 형태로 가져올 수 있습니다.  
  
 이 경우 웹 서비스 상호 작용을 통해 일부 셀 값을 계산하는 Excel 스프레드시트를 배포할 수 있습니다. 이 시나리오에서는 문서를 열 수 있는 모든 클라이언트에서 서비스 계약 어셈블리를 등록하지 못할 수도 있습니다. `wsdl` 매개 변수 또는 `mexAddress` 매개 변수가 자체 포함된 솔루션을 활성화합니다.  
  
> [!NOTE]
> 요청 및 응답 훼손 또는 스푸핑을 방지하려면 상호 인증을 사용해야 합니다. 특히 클라이언트는 응답하는 메타 데이터 교환 엔드포인트가 신뢰할 수 있는 당사자가 맞는지 확인해야 합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 MEX 계약에서 서비스 모니커를 사용하는 방법을 보여 줍니다. 다음 계약에서 서비스는 wsHttpBinding을 통해 노출됩니다.  
  
```  
using System.ServiceModel;  
  
...  
  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Demo")]  
public interface IAffiliate  
{  
    [OperationContract]  
    bool NewAffiliate(string ID, string company, string fullname, string accountsCode);  
    [OperationContract]  
    bool RemoveAffiliate(string ID);  
    [OperationContract]  
    double RevenueCheckMonthly(ref string ID);  
    [OperationContract]  
    double RevenueCheckTotal(ref string ID);  
}  
```  
  
 원격 서비스에 대 한 WCF 클라이언트를 구성 하려면 다음 예제 모니커 문자열을 사용할 수 있습니다.  
  
```  
service4:mexAddress="http://servername/Affiliates/service.svc/mex",  
address="http://servername/Affiliates/service.svc",  
contract=IAffiliate, contractNamespace=http://Microsoft.ServiceModel.Demo,  
binding=WSHttpBinding_IAffiliate, bindingNamespace=http://tempuri.org/  
```  
  
 클라이언트 애플리케이션을 실행하는 동안 클라이언트는 제공된 `WS-MetadataExchange`를 사용하여 `mexAddress`를 수행합니다. 그러면 다양한 서비스에 대한 주소, 바인딩 및 계약 정보가 반환될 수 있습니다. `address`, `contract`, `contractNamespace`, `binding` 및 `bindingNamespace` 매개 변수는 필요한 서비스를 식별하는 데 사용됩니다. 이러한 매개 변수를 일치 시킨 후에는 모니커에서 적절 한 계약 정의를 사용 하 여 WCF 클라이언트를 생성 하 고, 형식화 된 계약과 마찬가지로 WCF 클라이언트를 사용 하 여 호출을 수행할 수 있습니다.  
  
> [!NOTE]
> 모니커 형식이 잘못되었거나 서비스를 사용할 수 없는 경우 `GetObject`를 호출하면 "구문이 잘못되었습니다."라는 오류가 반환됩니다. 이 오류가 발생하면 사용하고 있는 모니커가 올바르고 서비스를 사용할 수 있는지 확인하세요.  
  
## <a name="see-also"></a>참고자료

- [방법: 서비스 모니커 등록 및 구성](../../../../docs/framework/wcf/feature-details/how-to-register-and-configure-a-service-moniker.md)
