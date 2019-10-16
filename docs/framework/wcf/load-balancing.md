---
title: 부하 분산
ms.date: 03/30/2017
helpviewer_keywords:
- load balancing [WCF]
ms.assetid: 148e0168-c08d-4886-8769-776d0953b80f
ms.openlocfilehash: d3b24ef892e1fe3dd28fee4ce8fa44f7373c7c01
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645487"
---
# <a name="load-balancing"></a>부하 분산
Windows Communication Foundation (WCF) 응용 프로그램의 용량을 늘리려면 하나의 방법은 부하 분산 된 서버 팜에 배포 하 여 확장할 것입니다. WCF 응용 프로그램으로 표준 부하 분산 기술을 Windows 네트워크 부하 분산과 같은 소프트웨어 부하 분산 장치를 포함 하 여 하드웨어 기반 부하 분산을 사용 하 여 부하가 분산 될 수 있습니다.  
  
 다음 섹션에는 다양 한 시스템 제공 바인딩을 사용 하 여 작성 하는 WCF 응용 프로그램 부하 분산에 대 한 고려 사항을 설명 합니다.  
  
## <a name="load-balancing-with-the-basic-http-binding"></a>기본 HTTP 바인딩을 사용한 부하 분산  
 부하 분산을 사용 하 여 통신 하는 WCF 응용 프로그램의 관점에서의 <xref:System.ServiceModel.BasicHttpBinding> 은 다른 일반적인 형식의 HTTP 네트워크 트래픽 (정적 HTML 콘텐츠, ASP.NET 페이지 또는 ASMX 웹 서비스) 다르지 않습니다. 이 바인딩을 사용 하는 WCF 채널은 기본적으로 상태 비저장 및 채널이 닫힐 때 연결을 종료 합니다. 따라서 <xref:System.ServiceModel.BasicHttpBinding>은 기존의 HTTP 부하 분산 기술과 호환됩니다.  
  
 기본적으로 <xref:System.ServiceModel.BasicHttpBinding>은 `Keep-Alive` 값을 사용하여 메시지의 연결 HTTP 헤더를 보내는데, 이를 통해 클라이언트는 영구 연결을 지원하는 서비스에 대해 이러한 연결을 설정할 수 있습니다. 또한 이 구성에서는 이전에 설정된 연결을 다시 사용하여 이후 메시지를 동일한 서버에 보낼 수 있으므로 처리량을 향상시킬 수 있습니다. 하지만 연결을 다시 사용하면 클라이언트가 부하 분산 팜의 특정 서버에만 강력하게 연결되어 라운드 로빈 부하 분산의 효율성이 떨어집니다. 이를 방지하려면, `Keep-Alive` 또는 사용자 정의 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A>에 <xref:System.ServiceModel.Channels.CustomBinding> 속성을 사용하여 서버에서 HTTP <xref:System.ServiceModel.Channels.Binding>를 비활성화할 수 있습니다. 다음 예제에서는 구성을 사용하여 이 작업을 수행하는 방법을 보여 줍니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
 <system.serviceModel>  
  <services>  
   <service   
     name="Microsoft.ServiceModel.Samples.CalculatorService"  
     behaviorConfiguration="CalculatorServiceBehavior">  
     <host>  
      <baseAddresses>  
       <add baseAddress="http://localhost:8000/servicemodelsamples/service"/>  
      </baseAddresses>  
     </host>  
    <!-- configure http endpoint, use base address provided by host  
         And the customBinding -->  
     <endpoint address=""  
           binding="customBinding"  
           bindingConfiguration="HttpBinding"   
           contract="Microsoft.ServiceModel.Samples.ICalculator" />  
   </service>  
  </services>  
  
  <bindings>  
    <customBinding>  
  
    <!-- Configure a CustomBinding that disables keepAliveEnabled-->  
      <binding name="HttpBinding" keepAliveEnabled="False"/>  
  
    </customBinding>  
  </bindings>  
 </system.serviceModel>  
</configuration>  
```  
  
 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]에 도입된 다음과 같은 단순화된 구성을 사용하면 동일한 동작을 수행할 수 있습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
 <system.serviceModel>  
    <protocolMapping>  
      <add scheme="http" binding="customBinding" />  
    </protocolMapping>  
    <bindings>  
      <customBinding>  
  
      <!-- Configure a CustomBinding that disables keepAliveEnabled-->  
        <binding keepAliveEnabled="False"/>  
  
      </customBinding>  
    </bindings>  
 </system.serviceModel>  
</configuration>  
```  
  
 기본 엔드포인트, 바인딩 및 동작에 대한 자세한 내용은 [단순화된 구성](../../../docs/framework/wcf/simplified-configuration.md) 및 [WCF 서비스를 위한 단순화된 구성](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)을 참조하세요.  
  
## <a name="load-balancing-with-the-wshttp-binding-and-the-wsdualhttp-binding"></a>WSHttp 바인딩 및 WSDualHttp 바인딩을 사용한 부하 분산  
 기본 바인딩 구성을 일부 수정한다면, HTTP 부하 분산 기술을 사용하여 <xref:System.ServiceModel.WSHttpBinding>과 <xref:System.ServiceModel.WSDualHttpBinding>을 모두 부하 분산할 수 있습니다.  
  
- 보안 컨텍스트 설정 해제: 이 작업은 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A>의 <xref:System.ServiceModel.WSHttpBinding> 속성을 `false`로 설정하여 수행할 수 있습니다. 또는 보안 세션이 필요한 경우에 설명 된 대로 상태 저장 보안 세션을 사용 하 여 [보안 세션](../../../docs/framework/wcf/feature-details/secure-sessions.md) 항목입니다. 상태 저장 보안 세션을 사용하면 보안 세션을 각 요청과 함께 보호 보안 토큰의 일부로 전송할 때 서비스의 상태를 비저장 상태로 유지할 수 있습니다. 상태 저장 보안 세션을 사용하려면, 필요한 구성 설정이 시스템에서 제공되는 <xref:System.ServiceModel.Channels.CustomBinding> 및 <xref:System.ServiceModel.Channels.Binding>에 노출되지 않으므로 <xref:System.ServiceModel.WSHttpBinding> 또는 사용자 정의 <xref:System.ServiceModel.WSDualHttpBinding>을 사용해야 합니다.  
  
- 신뢰할 수 있는 세션은 사용하지 마십시오. 이 기능은 기본적으로 해제되어 있습니다.  
  
## <a name="load-balancing-the-nettcp-binding"></a>Net.TCP 바인딩을 사용한 부하 분산  
 <xref:System.ServiceModel.NetTcpBinding>은 IP 계층 부하 분산 기술을 사용하여 부하 분산될 수 있습니다. 하지만 <xref:System.ServiceModel.NetTcpBinding>은 연결 대기 시간을 줄이기 위해 기본적으로 TCP 연결을 풀링합니다. 이러한 최적화 작업은 기본 부하 분산 메커니즘과 충돌하게 됩니다. <xref:System.ServiceModel.NetTcpBinding>을 최적화하기 위한 기본 구성 값은 연결 풀 설정의 일부인 대여 시간 제한입니다. 연결을 풀링하면 클라이언트 연결이 팜 내의 특정 서버와 이루어지게 됩니다. 이러한 연결 수명은 대여 시간 제한 설정으로 제어할 수 있지만 수명이 늘어나면 팜 내 여러 서버 간에 부하 분산 균형이 맞지 않게 됩니다. 결과적으로 평균 호출 시간이 늘어납니다. 따라서 <xref:System.ServiceModel.NetTcpBinding>을 부하 분산 시나리오에 사용할 때는 이 바인딩에서 사용하는 기본 대여 시간 제한을 줄이는 것이 좋습니다. 애플리케이션에 따라 최적 값이 다르겠지만 부하 분산 시나리오에 적절한 대여 시간 제한은 30초부터입니다. 채널 임대 시간 제한 및 기타 전송 할당량에 대 한 자세한 내용은 참조 하세요. [전송 할당량](../../../docs/framework/wcf/feature-details/transport-quotas.md)합니다.  
  
 부하 분산 시나리오에서 성능을 최대화하려면 <xref:System.ServiceModel.NetTcpSecurity>(<xref:System.ServiceModel.SecurityMode.Transport> 또는 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고자료

- [인터넷 정보 서비스 호스팅을 위한 최선의 방법](../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)
