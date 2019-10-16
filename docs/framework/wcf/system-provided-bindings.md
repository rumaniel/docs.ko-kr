---
title: 시스템 제공 바인딩
description: 시스템 제공 WCF(Windows Communication Foundation) 바인딩의 모든 것을 알아봅니다.
ms.date: 06/05/2018
helpviewer_keywords:
- bindings [WCF], system-provided
ms.assetid: 2c243746-45ce-4588-995e-c17126a579a6
ms.openlocfilehash: 3c6c6b628d208aede8c547dcfa66fc189a26ae01
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61791510"
---
# <a name="system-provided-bindings"></a>시스템 제공 바인딩

바인딩은 엔드포인트와 통신할 때 사용할 통신 메커니즘을 지정하고 엔드포인트에 연결하는 방법을 나타냅니다. 바인딩에 다음과 같은 요소가 포함됩니다.

- 프로토콜 스택은 엔드포인트에 보내는 메시지에 사용할 보안, 안정성 및 컨텍스트 흐름 설정을 결정합니다.

- 전송은 엔드포인트에 메시지를 보낼 때 사용할 TCP 또는 HTTP와 같은 기본 전송 프로토콜을 결정합니다.

- 인코딩은 연결 엔드포인트로 전송된 메시지에 사용할 통신 인코딩을 결정합니다. 예를 들어 text/XML, 이진 또는 MTOM(Message Transmission Optimization Mechanism)입니다.

 이 문서에서는 시스템 제공 WCF(Windows Communication Foundation) 바인딩의 모든 것을 보여줍니다. 이러한 바인딩 중 하나라도 애플리케이션의 정확한 조건을 충족하지 않을 경우 사용자 지정 바인딩을 만들 수 있습니다. 사용자 지정 바인딩을 만드는 방법에 대한 자세한 내용은 [사용자 지정 바인딩](./extending/custom-bindings.md)을 참조하십시오.

 WS-Federation 프로토콜을 지원하는 안전하며 상호 운용 가능한 바인딩을 사용하면 페더레이션에 있는 조직이 사용자를 효율적으로 인증하고 권한을 부여할 수 있습니다.

> [!IMPORTANT]
> 항상 보안을 포함하는 바인딩을 선택합니다. 기본적으로 [\<basicHttpBinding>](../configure-apps/file-schema/wcf/basichttpbinding.md) 요소를 제외한 모든 바인딩에는 보안이 설정되어 있습니다. 보안 바인딩을 선택하지 않거나 보안을 비활성화하는 경우 보안 데이터 센터 또는 격리된 네트워크에 저장하는 것과 같은 방식으로 데이터를 보호해야 합니다.

> [!IMPORTANT]
> 다른 방법으로 데이터의 보안을 유지하지 않는 한 보안을 지원하지 않거나 보안이 설정되지 않은 바인딩과 함께 이중 계약을 사용하지 마십시오.

다음 바인딩은 WCF와 함께 제공됩니다.

|바인딩|구성 요소|설명|
|-------------|---------------------------|-----------------|
|<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding>](../configure-apps/file-schema/wcf/basichttpbinding.md)|WS-Basic Profile 사양의 웹 서비스와 통신하는 데 적합한 바인딩에는 ASP.NET 웹 서비스(ASMX) 기반 서비스 등이 있습니다. 이 바인딩은 HTTP를 전송으로 사용하고 텍스트/XML을 기본 메시지 인코딩으로 사용합니다.|
|<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md)|비이중 서비스 계약에 적합한 안전하고 상호 운용할 수 있는 바인딩입니다.|
|<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding>](../configure-apps/file-schema/wcf/wsdualhttpbinding.md)|이중 서비스 계약 또는 SOAP 매개자를 통한 통신에 적합한 안전하고 상호 운용할 수 있는 바인딩입니다.|
|<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding>](../configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|WS-Federation 프로토콜을 지원하는 안전하며 상호 운용 가능한 바인딩을 사용하면 페더레이션에 있는 조직이 사용자를 효율적으로 인증하고 권한을 부여할 수 있습니다.|
|<xref:System.ServiceModel.NetHttpBinding>|[\<netHttpBinding>](../configure-apps/file-schema/wcf/nethttpbinding.md)|기본적으로 이진 인코딩을 사용하는 HTTP 또는 WebSocket 서비스를 사용하도록 디자인된 바인딩입니다.|
|<xref:System.ServiceModel.NetHttpsBinding>|[\<netHttpsBinding>](../configure-apps/file-schema/wcf/nethttpsbinding.md)|HTTP 또는 WebSocket 서비스를 사용하기 디자인된 보안 바인딩이며 기본적으로 이진 인코딩을 사용합니다.|
|<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding>](../configure-apps/file-schema/wcf/nettcpbinding.md)|WCF 애플리케이션 간 시스템 통신에 적합한 안전하고 최적화된 바인딩입니다.|
|<xref:System.ServiceModel.NetNamedPipeBinding>|[\<netNamedPipeBinding>](../configure-apps/file-schema/wcf/netnamedpipebinding.md)|WCF 애플리케이션 간 시스템 통신에 적합한, 안전하고 신뢰할 수 있으며 최적화된 바인딩입니다.|
|<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding>](../configure-apps/file-schema/wcf/netmsmqbinding.md)|WCF 애플리케이션 간 시스템 통신에 적합한 대기 중인 바인딩입니다.|
|<xref:System.ServiceModel.NetPeerTcpBinding>|[\<netPeerTcpBinding>](../configure-apps/file-schema/wcf/netpeertcpbinding.md)|안전하게 여러 시스템 간에 통신할 수 있는 바인딩입니다.|
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|[\<msmqIntegrationBinding>](../configure-apps/file-schema/wcf/msmqintegrationbinding.md)|WCF 애플리케이션과 기존 메시지 큐 애플리케이션 간 시스템 통신에 적합한 바인딩입니다.|
|<xref:System.ServiceModel.BasicHttpContextBinding>|[\<basicHttpContextBinding>](../configure-apps/file-schema/wcf/basichttpcontextbinding.md)|HTTP 쿠키를 사용하여 컨텍스트를 교환할 수 있는 WS-Basic Profile 사양의 웹 서비스와 통신하는 데 적합한 바인딩입니다.|
|<xref:System.ServiceModel.NetTcpContextBinding>|[\<netTcpContextBinding>](../configure-apps/file-schema/wcf/nettcpcontextbinding.md)|SOAP 헤더를 사용하여 컨텍스트를 교환할 수 있는 WCF 애플리케이션 간 시스템 통신에 적합한 안전하고 최적화된 바인딩입니다.|
|<xref:System.ServiceModel.WebHttpBinding>|[\<webHttpBinding>](../configure-apps/file-schema/wcf/webhttpbinding.md)|SOAP 메시지 대신 HTTP 요청을 통해 노출되는 WCF 웹 서비스에 대한 엔드포인트를 구성하는 데 사용되는 바인딩입니다.|
|<xref:System.ServiceModel.WSHttpContextBinding>|[\<wsHttpContextBinding>](../configure-apps/file-schema/wcf/wshttpcontextbinding.md)|SOAP 헤더를 사용하여 컨텍스트를 교환할 수 있는 비이중 서비스 계약에 적합한 안전하고 상호 운용 가능한 바인딩입니다.|
|<xref:System.ServiceModel.UdpBinding>|[\<udpBinding>](../configure-apps/file-schema/wcf/udpbinding.md)|다수의 클라이언트에 다수의 간단한 메시지를 보낼 때 사용하는 바인딩입니다.|

 다음 표에서는 각 시스템 제공 바인딩의 기능을 보여 줍니다. 바인딩은 표 열에 있고, 기능은 행에 나열되며 두 번째 표에 설명되어 있습니다. 다음 표에는 사용된 바인딩 약어에 대한 키가 나와 있습니다. 바인딩을 선택하려면 필요한 행 기능을 모두 만족하는 열을 결정합니다.

|바인딩|상호 운용성|보안(기본값)|세션<br />(기본값)|트랜잭션|이중|인코딩(기본값)|스트리밍<br />(기본값)|
|-------------|----------------------|--------------------------|-----------------------------|------------------|------------|--------------------------|-------------------------------|
|<xref:System.ServiceModel.BasicHttpBinding>|Basic Profile 1.1|(None), Transport, Message, Mixed|(None)|(None)|N/A|Text, (MTOM)|예<br />(buffered)|
|<xref:System.ServiceModel.WSHttpBinding>|WS|Transport, (Message), Mixed|(None), Reliable Session, Security Session|(None), 예|N/A|(Text), MTOM|아니요|
|<xref:System.ServiceModel.WSDualHttpBinding>|WS|(Message), None|(Reliable Session), Security Session|(None), 예|예|(Text), MTOM|아니요|
|<xref:System.ServiceModel.WSFederationHttpBinding>|WS-Federation|(Message), Mixed, None|(None), Reliable Session, Security Session|(None), 예|아니요|(Text), MTOM|아니요|
|<xref:System.ServiceModel.NetHttpBinding>|.NET|(None), Transport, Message, TransportWithMessageCredential, TransportCredentialOnly|다음의 참고를 참조하십시오.|없음|다음의 참고를 참조하십시오.|(이진), 텍스트, MTOM|예(버퍼링됨)|
|<xref:System.ServiceModel.NetHttpsBinding>|.NET|(전송), TransportWithMessageCredential|다음의 참고를 참조하십시오.|없음|다음의 참고를 참조하십시오.|(이진), 텍스트, MTOM|예<br />(buffered)|
|<xref:System.ServiceModel.NetTcpBinding>|.NET|(Transport), Message, None, Mixed|(Transport), Reliable Session, Security Session|(None), 예|예|이항|예<br />(buffered)|
|<xref:System.ServiceModel.NetNamedPipeBinding>|.NET|(Transport), None|None, (Transport)|(None), 예|예|이항|예<br />(buffered)|
|<xref:System.ServiceModel.NetMsmqBinding>|.NET|Message, (Transport), None|(None), Transport|None, (예)|아니요|이항|아니요|
|<xref:System.ServiceModel.NetPeerTcpBinding>|Peer|(Transport)|(None)|(None)|예||아니요|
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|MSMQ|(Transport)|(None)|None, (예)|N/A|N/A|아니요|
|<xref:System.ServiceModel.BasicHttpContextBinding>|Basic Profile 1.1|(None), Transport, Message, Mixed|(None)|(None)|N/A|Text, (MTOM)|예<br />(buffered)|
|<xref:System.ServiceModel.NetTcpContextBinding>|.NET|(Transport), Message, None, Mixed|(Transport), Reliable Session, Security Session|(None), 예|예|이항|예<br />(buffered)|
|<xref:System.ServiceModel.WSHttpContextBinding>|WS|Transport, (Message), Mixed|(None), Reliable Session, Security Session|(None), 예|N/A|Text, (MTOM)|아니요|
|<xref:System.ServiceModel.UdpBinding> <br /><br /> **참고:**  이 바인딩 구현 안에 표준 SOAP-over-UDP 사양을 구현하여 상호 운용성을 구현할 수 있습니다.|.NET|(None)|(None)|(None)|N/A|(Text)|아니요|

> [!IMPORTANT]
> <xref:System.ServiceModel.NetHttpBinding>은 HTTP 또는 WebSocket 서비스를 사용하도록 디자인된 바인딩이며 기본적으로 이진 인코딩을 사용합니다. <xref:System.ServiceModel.NetHttpBinding>은 해당 바인딩이 HTTP 요청-회신 계약 또는 이중 계약에 사용되는지를 검색하고 그에 맞게 동작을 변경합니다. 요청-회신에는 HTTP를 사용하고 이중 계약에는 WebSocket을 사용합니다. 사용 하 여이 동작을 재정의할 수 있습니다는 <xref:System.ServiceModel.Channels.WebSocketTransportUsage> 바인딩 설정: WhenDuplex - 이 설정은 기본값이며 위에 설명된 대로 동작합니다. Never - 이 설정은 WebSocket이 사용되지 않도록 합니다. 이 설정으로 이중 계약을 사용하려고 시도하면 예외가 발생합니다. Always - 이 설정은 요청-회신 계약의 경우에도 WebSocket이 사용되도록 합니다. NetHttpBinding은 HTTP 모드 및 WebSocket 모드에서 신뢰할 수 있는 세션을 지원합니다. WebSocket 모드에서는 세션이 전송에 의해 제공됩니다.

 다음 표에서는 앞의 표에 나열되어 있는 기능에 대해 설명합니다.

|기능|설명|
|-------------|-----------------|
|상호 운용성 형식|바인딩이 상호 운용하는 프로토콜 또는 기술에 이름을 지정합니다.|
|보안|채널 보안 방식을 지정합니다.<br />-None. SOAP 메시지 보안이 설정 되지 않습니다 및 클라이언트가 인증 되지 않습니다.<br />-전송 합니다. 전송 계층에서 보안 요구 사항은 충족 합니다.<br />-메시지: 메시지 계층에서 보안 요구 사항은 충족 합니다.<br />-혼합 합니다. 클레임 메시지가 전달 됩니다. 전송 계층에서 무결성 및 기밀성 요구 사항이 충족 됩니다.|
|세션|이 바인딩이 세션 계약을 지원할지 여부를 지정합니다.|
|트랜잭션|트랜잭션이 활성화되었는지 여부를 지정합니다.|
|이중|이중 계약이 지원되는지 여부를 지정합니다. 이 기능을 사용하려면 바인딩의 세션을 지원해야 합니다.|
|인코딩|메시지의 통신 형식을 지정합니다. 허용 가능한 값은 다음과 같습니다.<br />- Text: 예를 들어 UTF-8이 있습니다.<br />- 이진<br />-Message Transmission Optimization Mechanism (MTOM): SOAP 봉투의 컨텍스트 내에서 이진 XML 요소를 효율적으로 인코딩하는 방법입니다.|
|스트리밍|스트리밍이 들어오는 메시지와 보내는 메시지를 지원하는지 여부를 지정합니다. 바인딩의 `TransferMode` 속성을 사용하여 값을 설정합니다. 허용 가능한 값은 다음과 같습니다.<br />- <xref:System.ServiceModel.TransferMode.Buffered>: 요청 및 응답 메시지가 모두 버퍼링됩니다.<br />- <xref:System.ServiceModel.TransferMode.Streamed>: 요청 및 응답 메시지가 모두 스트리밍됩니다.<br />- <xref:System.ServiceModel.TransferMode.StreamedRequest>: 요청 메시지는 스트리밍되고 응답 메시지는 버퍼링됩니다.<br />- <xref:System.ServiceModel.TransferMode.StreamedResponse>: 요청 메시지는 버퍼링되고 응답 메시지는 스트리밍됩니다.|

## <a name="see-also"></a>참고자료

- [엔드포인트 만들기 개요](endpoint-creation-overview.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](using-bindings-to-configure-services-and-clients.md)
- [기본 WCF 프로그래밍](basic-wcf-programming.md)
