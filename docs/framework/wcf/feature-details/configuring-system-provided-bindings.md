---
title: 시스템 제공 바인딩 구성
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], system-provided bindings
- WCF [WCF], system-provided bindings
- bindings [WCF], system-provided
ms.assetid: 443f8d65-f1f2-4311-83b3-4d8fdf7ccf16
ms.openlocfilehash: c2c1f468fba404768fe01e84260125843964fea0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949620"
---
# <a name="configuring-system-provided-bindings"></a>시스템 제공 바인딩 구성
바인딩은 엔드포인트와 통신할 때 사용할 통신 메커니즘을 지정하고 엔드포인트에 연결하는 방법을 나타냅니다. 바인딩은 필요한 통신 기능을 제공 하기 위해 WCF (Windows Communication Foundation) 채널이 계층화 되는 방식을 정의 하는 요소로 구성 됩니다. 바인딩에는 다음 세 가지 형식의 요소가 있습니다.  
  
- 프로토콜 채널 바인딩 요소. 엔드포인트에 보내는 메시지에 사용할 보안, 안정성, 컨텍스트 흐름 설정 또는 사용자 정의 프로토콜을 결정합니다.  
  
- 전송 채널 바인딩 요소. TCP 또는 HTTP 등의 엔드포인트에 메시지를 보낼 때 사용할 기존 전송 프로토콜을 결정합니다.  
  
- 메시지 인코딩 바인딩 요소. 엔드포인트에 보내는 메시지에 사용할 텍스트/XML, 이진 또는 MTOM(Message Transmission Optimization Mechanism) 등의 연결 인코딩을 결정합니다.  
  
 이 항목에서는 시스템에서 제공 하는 모든 WCF (Windows Communication Foundation) 바인딩을 제공 합니다. 이러한 바인딩이 모두 응용 프로그램에 대한 정확한 요구 사항을 충족하지 않을 경우 <xref:System.ServiceModel.Channels.CustomBinding> 클래스를 사용하여 바인딩을 만들 수 있습니다. 사용자 지정 바인딩을 만드는 방법에 대한 자세한 내용은 [사용자 지정 바인딩](../../../../docs/framework/wcf/extending/custom-bindings.md)을 참조하십시오.  
  
> [!IMPORTANT]
> 보안이 설정된 바인딩을 선택합니다. 기본적으로 <xref:System.ServiceModel.BasicHttpBinding> 바인딩을 제외한 모든 바인딩에는 보안이 설정되어 있습니다. 보안 바인딩을 선택하지 않거나 보안을 비활성화하는 경우 보안 데이터 센터 또는 격리된 네트워크에 보호하는 것과 같은 방식으로 네트워크 교환을 보호해야 합니다.  
  
> [!IMPORTANT]
> 다른 방법으로 네트워크 교환의 보안을 유지하지 않는 한 보안을 지원하지 않거나 보안이 설정되지 않은 바인딩과 함께 이중 계약을 사용하지 마십시오.  
  
## <a name="system-provided-bindings"></a>시스템 제공 바인딩  
 다음 바인딩은 WCF와 함께 제공 됩니다.  
  
|바인딩|구성 요소|설명|  
|-------------|---------------------------|-----------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)|WS-Basic Profile 사양의 웹 서비스와 통신하는 데 적합한 바인딩에는 ASP.NET 웹 서비스(ASMX) 기반 서비스 등이 있습니다. 이 바인딩은 HTTP를 전송으로 사용하고 텍스트/XML을 기본 메시지 인코딩으로 사용합니다.|  
|<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)|비이중 서비스 계약에 적합한 안전하고 상호 운용할 수 있는 바인딩입니다.|  
|<xref:System.ServiceModel.WS2007HttpBinding>|[\<ws2007HttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)|올바른 버전의 <xref:System.ServiceModel.WSHttpBinding.Security%2A>, <xref:System.ServiceModel.ReliableSession> 및 <xref:System.ServiceModel.WSHttpBindingBase.TransactionFlow%2A> 바인딩 요소를 지원하는 안전하며 상호 운용 가능한 바인딩입니다.|  
|<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)|이중 서비스 계약 또는 SOAP 매개자를 통한 통신에 적합한 안전하고 상호 운용할 수 있는 바인딩입니다.|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|WS-Federation 프로토콜을 지원하는 안전하며 상호 운용 가능한 바인딩을 사용하면 페더레이션에 있는 조직이 사용자를 효율적으로 인증하고 권한을 부여할 수 있습니다.|  
|<xref:System.ServiceModel.WS2007FederationHttpBinding>|[\<ws2007FederationHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007federationhttpbinding.md)|<xref:System.ServiceModel.WS2007HttpBinding>에서 파생되며 페더레이션 보안을 지원하는 안전하고 상호 운용 가능한 바인딩입니다.|  
|<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)|WCF 애플리케이션 간 시스템 통신에 적합한 안전하고 최적화된 바인딩입니다.|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|[\<netNamedPipeBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md)|WCF 애플리케이션 간 시스템 통신에 적합한, 안전하고 신뢰할 수 있으며 최적화된 바인딩입니다.|  
|<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)|WCF 애플리케이션 간 시스템 통신에 적합한 대기 중인 바인딩입니다.|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|[\<netPeerTcpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md)|안전하게 여러 시스템 간에 통신할 수 있는 바인딩입니다.|  
|<xref:System.ServiceModel.WebHttpBinding>|[\<webHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md)|SOAP 메시지 대신 HTTP 요청을 통해 노출되는 WCF 웹 서비스에 대한 엔드포인트를 구성하는 데 사용되는 바인딩입니다.|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|[\<msmqIntegrationBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)|WCF 응용 프로그램과 기존 메시지 큐 (MSMQ) 응용 프로그램 간의 시스템 간 통신에 적합 한 바인딩입니다.|  
  
## <a name="binding-features"></a>바인딩 기능  
 다음 표에서는 각 시스템 제공 바인딩의 몇 가지 주요 기능을 보여 줍니다. 바인딩은 첫 번째 열에 나열되어 있고, 기능에 대한 정보는 표에 설명되어 있습니다. 다음 표에는 사용된 바인딩 약어에 대한 키가 나와 있습니다. 바인딩을 선택하려면 필요한 행 기능을 모두 만족하는 열을 결정합니다.  
  
|바인딩|상호 운용성|보안 모드(기본값)|세션<br /><br /> (기본값)|트랜잭션|이중|  
|-------------|----------------------|----------------------------------|-----------------------------|------------------|------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|Basic Profile 1.1|(None), Transport, Message, Mixed|None, (None)|(None)|N/A|  
|<xref:System.ServiceModel.WSHttpBinding>|WS|None, Transport, (Message), Mixed|(None), Transport, Reliable Session|(None), 예|N/A|  
|<xref:System.ServiceModel.WS2007HttpBinding>|WS-Security, WS-Trust, WS-SecureConversation, WS-SecurityPolicy|None, Transport, (Message), Mixed|(None), Transport, Reliable Session|(None), 예|N/A|  
|<xref:System.ServiceModel.WSDualHttpBinding>|WS|None, (Message)|(Reliable Session)|(None), 예|예|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|WS-Federation|None, (Message), Mixed|(None), Reliable Session|(None), 예|아니요|  
|<xref:System.ServiceModel.WS2007FederationHttpBinding>|WS-Federation|None, (Message), Mixed|(None), Reliable Session|(None), 예|아니요|  
|<xref:System.ServiceModel.NetTcpBinding>|.NET|None, (Transport), Message,<br /><br /> 혼합|Reliable Session, (Transport)|(None), 예|예|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|.NET|None,<br /><br /> (Transport)|None, (Transport)|(None), 예|예|  
|<xref:System.ServiceModel.NetMsmqBinding>|.NET|None, Message, (Transport), Both|(None)|(None), 예|아니요|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|Peer|None, Message, (Transport), Mixed|(None)|(None)|예|  
|<xref:System.ServiceModel.WebHttpBinding>|.Net|없음, 전송, 전송|(None)|(None)|N/A|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|MSMQ|None, (Transport)|(None)|(None), 예|N/A|  
  
 다음 표에서는 앞의 표에서 볼 수 있는 기능에 대해 설명합니다.  
  
|기능|설명|  
|-------------|-----------------|  
|상호 운용성 형식|바인딩이 상호 운용하는 프로토콜 또는 기술에 이름을 지정합니다.|  
|보안|채널 보안 방식을 지정합니다.<br /><br /> 없음을 SOAP 메시지가 보호 되지 않고 클라이언트가 인증 되지 않습니다.<br />트랜스포트가 전송 계층에서 보안 요구 사항이 충족 됩니다.<br />메시지나 메시지 계층에서 보안 요구 사항이 충족 됩니다.<br />모음집 이 보안 모드를 `TransportWithMessageCredentials`라고 합니다. 이 보안 모드는 메시지 수준에서 자격 증명을 처리하고 전송 계층에서 무결성 및 기밀성 요구 사항을 충족합니다.<br />양방향 메시지 수준과 전송 수준 보안이 모두 사용 됩니다. 이 기능은 <xref:System.ServiceModel.NetMsmqBinding>에 고유합니다.|  
|세션|이 바인딩이 세션 계약을 지원할지 여부를 지정합니다.|  
|트랜잭션|트랜잭션이 활성화되었는지 여부를 지정합니다.|  
|이중|이중 계약이 지원되는지 여부를 지정합니다. 이 기능을 사용하려면 바인딩의 세션을 지원해야 합니다.|  
|스트리밍|메시지 스트리밍이 지원되는지 여부를 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- [엔드포인트 만들기 개요](../../../../docs/framework/wcf/endpoint-creation-overview.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [기본 WCF 프로그래밍](../../../../docs/framework/wcf/basic-wcf-programming.md)
