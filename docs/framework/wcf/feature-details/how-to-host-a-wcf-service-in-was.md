---
title: '방법: WAS에서 WCF 서비스 호스팅'
ms.date: 03/30/2017
ms.assetid: 9e3e213e-2dce-4f98-81a3-f62f44caeb54
ms.openlocfilehash: b6d3ace054260de1ca649fbf4bd54156bbea24ce
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972216"
---
# <a name="how-to-host-a-wcf-service-in-was"></a>방법: WAS에서 WCF 서비스 호스팅
이 항목에서는 WAS (Windows Process Activation service)에서 호스팅된 WCF (Windows Communication Foundation) 서비스를 만드는 데 필요한 기본 단계에 대해 간략하게 설명 합니다. WAS는 HTTP가 아닌 전송 프로토콜에서 사용하는 IIS(Internet Information Services) 기능의 일반화인 새 프로세스 활성화 서비스입니다. WCF는 수신기 어댑터 인터페이스를 사용 하 여 WCF (예: TCP, 명명 된 파이프 및 메시지 큐)에서 지 원하는 HTTP가 아닌 프로토콜을 통해 수신 되는 활성화 요청을 전달 합니다.  
  
 이 호스팅 옵션을 사용하려면 WAS 활성화 구성 요소를 적절히 설치하여 구성해야 하지만 호스팅 코드를 애플리케이션의 일부로 작성하지 않아도 됩니다. WAS를 설치 및 구성 [하는 방법에 대 한 자세한 내용은 방법: WCF 활성화 구성 요소](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)를 설치 하 고 구성 합니다.  
  
> [!WARNING]
> 웹 서버의 요청 처리 파이프라인이 클래식 모드로 설정된 경우 WAS 활성화가 지원되지 않습니다. WAS 활성화를 사용할 경우 웹 서버의 요청 처리 파이프라인이 통합 모드로 설정되어 있어야 합니다.  
  
 WCF 서비스가 WAS에서 호스팅되는 경우 표준 바인딩이 일반적인 방법으로 사용 됩니다. 그러나 WAS에서 호스팅되는 서비스를 구성하기 위해 <xref:System.ServiceModel.NetTcpBinding> 및 <xref:System.ServiceModel.NetNamedPipeBinding>을 사용하는 경우 제약 조건을 충족해야 합니다. 서로 다른 엔드포인트가 동일한 전송을 사용하는 경우 바인딩 설정은 다음 7개의 속성과 일치해야 합니다.  
  
- ConnectionBufferSize  
  
- ChannelInitializationTimeout  
  
- MaxPendingConnections  
  
- MaxOutputDelay  
  
- MaxPendingAccepts  
  
- ConnectionPoolSettings.IdleTimeout  
  
- ConnectionPoolSettings.MaxOutboundConnectionsPerEndpoint  
  
 그렇지 않으면 첫 번째로 초기화된 엔드포인트가 항상 해당 속성 값을 결정하고 나중에 추가된 엔드포인트가 이러한 설정과 일치하지 않을 경우 <xref:System.ServiceModel.ServiceActivationException>을 throw합니다.  
  
 이 예제의 소스 복사에 대해서는 [TCP 활성화](../../../../docs/framework/wcf/samples/tcp-activation.md)를 참조 하십시오.  
  
### <a name="to-create-a-basic-service-hosted-by-was"></a>WAS에서 호스팅되는 기본 서비스를 만들려면  
  
1. 서비스 유형에 대한 서비스 계약을 정의합니다.  
  
     [!code-csharp[C_HowTo_HostInWAS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1121)]  
  
2. 서비스 클래스에 서비스 계약을 구현합니다. 주소 또는 바인딩 정보는 서비스 구현 내에 지정되지 않습니다. 또한 구성 파일에서 해당 정보를 검색하기 위해 코드를 쓰지 않아도 됩니다.  
  
     [!code-csharp[C_HowTo_HostInWAS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1122)]  
  
3. Web.config 파일을 만들어 <xref:System.ServiceModel.NetTcpBinding> 엔드포인트에서 사용할 `CalculatorService` 바인딩을 정의합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <bindings>  
          <netTcpBinding>  
            <binding portSharingEnabled="true">  
              <security mode="None" />  
            </binding>  
          </netTcpBinding>  
        </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4. 다음 코드가 포함된 Service.svc 파일을 만듭니다.  
  
   ```
   <%@ServiceHost language=c# Service="CalculatorService" %>
   ```
  
5. Service.svc 파일을 IIS 가상 디렉터리에 저장합니다.  
  
### <a name="to-create-a-client-to-use-the-service"></a>서비스를 사용할 클라이언트를 만들려면  
  
1. 명령줄에서 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 서비스 메타 데이터에서 코드를 생성 합니다.  
  
    ```console
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
    ```  
  
2. 생성된 클라이언트에는 클라이언트 구현에서 충족해야 하는 서비스 계약을 정의하는 `ICalculator` 인터페이스가 포함되어 있습니다.  
  
     [!code-csharp[C_HowTo_HostInWAS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1221)]  
  
3. 또한 생성된 클라이언트 애플리케이션에는 `ClientCalculator`의 구현이 포함되어 있습니다. 주소 및 바인딩 정보는 서비스 구현 내에 지정되지 않습니다. 또한 구성 파일에서 해당 정보를 검색하기 위해 코드를 쓰지 않아도 됩니다.  
  
     [!code-csharp[C_HowTo_HostInWAS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1222)]  
  
4. 또한 <xref:System.ServiceModel.NetTcpBinding>을 사용하는 클라이언트의 구성도 Svcutil.exe를 통해 생성됩니다. 이 파일은 Visual Studio를 사용하는 경우 이름을 App.config로 지정해야 합니다.  
  
     [!code-xml[C_HowTo_HostInWAS#2211](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/common/app.config#2211)]   
  
5. 애플리케이션에서 `ClientCalculator`의 인스턴스를 만든 다음 서비스 작업을 호출합니다.  
  
     [!code-csharp[C_HowTo_HostInWAS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1223)]  
  
6. 클라이언트를 컴파일하고 실행합니다.  
  
## <a name="see-also"></a>참고자료

- [TCP 활성화](../../../../docs/framework/wcf/samples/tcp-activation.md)
- [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkId=201276)
