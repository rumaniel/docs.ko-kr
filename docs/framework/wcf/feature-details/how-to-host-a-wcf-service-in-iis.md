---
title: '방법: IIS에서 WCF 서비스 호스팅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b044b1c9-c1e5-4c9f-84d8-0f02f4537f8b
ms.openlocfilehash: ad1fb7d289dea3396b4edb4d3b3e9fb7fb1891e3
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972417"
---
# <a name="how-to-host-a-wcf-service-in-iis"></a>방법: IIS에서 WCF 서비스 호스팅
이 항목에서는 인터넷 정보 서비스 (IIS)에서 호스트 되는 WCF (Windows Communication Foundation) 서비스를 만드는 데 필요한 기본 단계에 대해 간략하게 설명 합니다. 이 항목에서는 사용자가 IIS에 대해 잘 알고 있으며 IIS 관리 도구를 사용해 IIS 응용 프로그램을 만들고 관리하는 방법을 이해하고 있다고 가정합니다. IIS에 대 한 자세한 내용은 [인터넷 정보 서비스](https://go.microsoft.com/fwlink/?LinkId=132449)를 참조 하세요. IIS 환경에서 실행 되는 WCF 서비스는 프로세스 재활용, 유휴 상태 종료, 프로세스 상태 모니터링 및 메시지 기반 활성화와 같은 IIS 기능을 최대한 활용 합니다. 이 호스팅 옵션을 사용하려면 IIS를 적절히 구성해야 하지만 호스팅 코드를 애플리케이션의 일부로 작성하지 않아도 됩니다. HTTP 전송을 사용하는 경우에만 IIS 호스팅을 사용할 수 있습니다.  
  
 WCF 및 ASP.NET가 상호 작용 하는 방법에 대 한 자세한 내용은 [Wcf 서비스 및 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)를 참조 하세요. 보안 구성에 대 한 자세한 내용은 [보안](../../../../docs/framework/wcf/feature-details/security.md)을 참조 하세요.  
  
 이 예제의 소스 복사에 대해서는 [인라인 코드를 사용 하는 IIS 호스팅](../../../../docs/framework/wcf/samples/iis-hosting-using-inline-code.md)을 참조 하세요.  
  
### <a name="to-create-a-service-hosted-by-iis"></a>IIS에 의해 호스팅되는 서비스를 만들려면  
  
1. IIS가 컴퓨터에 설치되어 실행되고 있는지 확인합니다. IIS를 설치 하 고 구성 하는 방법에 대 한 자세한 내용은 [iis 7.0 설치 및 구성을](https://go.microsoft.com/fwlink/?LinkID=132128) 참조 하세요.  
  
2. "IISHostedCalcService" 라는 응용 프로그램 파일에 대 한 새 폴더를 만들고, ASP.NET에 폴더의 콘텐츠에 대 한 액세스 권한이 있는지 확인 하 고, IIS 관리 도구를 사용 하 여이 응용 프로그램 디렉터리에 실제로 있는 새 IIS 응용 프로그램을 만듭니다. 응용 프로그램 디렉터리의 별칭을 만들 때는 “IISHostedCalc”를 사용합니다.  
  
3. 응용 프로그램 디렉터리에 “service.svc”라는 새 파일을 만든 다음 다음 @ServiceHost 요소를 추가 하 여이 파일을 편집 합니다.  
  
   ```
   <%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService"%>
   ```  
  
4. 응용 프로그램 디렉터리 내에 App_Code 하위 디렉터리를 만듭니다.  
  
5. App_Code subdirectory에 Service.cs라는 코드 파일을 만듭니다.  
  
6. Service.cs 파일의 맨 위에 다음의 using 문을 추가합니다.  
  
    ```csharp  
    using System;  
    using System.ServiceModel;  
    ```  
  
7. using 문 뒤에 다음 네임스페이스 선언을 추가합니다.  
  
    ```csharp  
    namespace Microsoft.ServiceModel.Samples  
    {  
    }  
    ```  
  
8. 다음 코드와 같이 네임스페이스 선언 내에 서비스 계약을 정의합니다.  
  
     [!code-csharp[c_HowTo_HostInIIS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#11)]
     [!code-vb[c_HowTo_HostInIIS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#11)]  
  
9. 다음 코드와 같이 서비스 계약 정의 뒤에서 서비스 계약을 구현합니다.  
  
     [!code-csharp[c_HowTo_HostInIIS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#12)]
     [!code-vb[c_HowTo_HostInIIS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#12)]  
  
10. 응용 프로그램 디렉터리에 “Web.config”라는 파일을 만들고 다음 구성 코드를 파일에 추가합니다. 런타임에 WCF 인프라는이 정보를 사용 하 여 클라이언트 응용 프로그램이 통신할 수 있는 끝점을 생성 합니다.  
  
     [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]      
  
     다음 예제에서는 구성 파일의 엔드포인트를 명시적으로 지정합니다. 서비스에 엔드포인트를 추가하지 않으면 런타임에서 기본 엔드포인트를 자동으로 추가합니다. 기본 끝점, 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../../docs/framework/wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.  
  
11. 서비스가 올바르게 호스팅되는지 확인하려면 Internet Explorer 인스턴스를 열고 서비스 URL인 `http://localhost/IISHostedCalc/Service.svc`로 이동합니다.  
  
## <a name="example"></a>예제  
 다음은 IIS에서 호스팅되는 계산기 서비스에 해당되는 전체 코드 목록입니다.  
  
 [!code-csharp[C_HowTo_HostInIIS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#1)] 
 [!code-vb[C_HowTo_HostInIIS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#1)] 
 [!code-xml[c_HowTo_HostInIIS#100](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]  
  
## <a name="see-also"></a>참고자료

- [인터넷 정보 서비스에서 호스팅](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)
- [서비스 호스팅](../../../../docs/framework/wcf/hosting-services.md)
- [WCF 서비스 및 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)
- [보안](../../../../docs/framework/wcf/feature-details/security.md)
- [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkId=201276)
