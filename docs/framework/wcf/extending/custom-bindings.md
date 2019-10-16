---
title: 사용자 지정 바인딩
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, endpoints
- Windows Communication Foundation, configuration
ms.assetid: 58532b6d-4eea-4a4f-854f-a1c8c842564d
ms.openlocfilehash: a4b3abfe9be25c9080a362eb4a6e4c7b070528f1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797230"
---
# <a name="custom-bindings"></a>사용자 지정 바인딩

시스템에서 제공하는 바인딩 중 하나가 사용자의 서비스 요구 사항을 충족하지 않을 때 <xref:System.ServiceModel.Channels.CustomBinding> 클래스를 사용할 수 있습니다. 모든 바인딩은 정렬된 바인딩 요소 집합으로부터 생성됩니다. 사용자 지정 바인딩은 시스템 제공 바인딩 요소로부터 만들거나 사용자 정의 사용자 지정 바인딩 요소를 포함할 수 있습니다. 예를 들어 사용자 지정 바인딩 요소를 사용하여 서비스 엔드포인트에서 새 전송 또는 새 인코더를 사용하도록 설정할 수 있습니다. 작업 예제는 [사용자 지정 바인딩 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751479(v=vs.90))을 참조 하세요. 자세한 내용은 [ \<customBinding >](../../configure-apps/file-schema/wcf/custombinding.md)를 참조 하세요.

## <a name="construction-of-a-custom-binding"></a>사용자 지정 바인딩 생성

사용자 지정 바인딩은 특정 순서로 "스택"되는 바인딩 요소 컬렉션에서 <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> 생성자를 사용하여 생성됩니다.

- 맨 위에는 트랜잭션 이동을 허용하는 선택적 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> 클래스가 있습니다.

- 다음에는 WS-ReliableMessaging 사양에서 정의된 세션 및 순서 지정 메커니즘을 제공하는 선택적 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> 클래스가 있습니다. 세션은 SOAP 매개자 및 전송 매개자에 적용될 수 있습니다.

- 다음에는 권한 부여, 인증, 보호, 기밀성과 같은 보안 기능을 제공하는 선택적 <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스가 있습니다.

- 다음에는 기본적으로 이중 통신을 지원하지 않는 전송 프로토콜(예: HTTP)을 사용하여 양방향 이중 통신을 수행하는 기능을 제공하는 선택적 <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> 클래스가 있습니다.

- 다음에는 단방향 통신을 제공하는 <xref:System.ServiceModel.Channels.OneWayBindingElement>) 클래스가 있습니다.

- 다음에는 아래와 같은 선택적 스트림 보안 바인딩 요소가 있습니다.

  - <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>

  - <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>

- 다음에는 필수 메시지 인코딩 바인딩 요소가 있습니다. 고유의 메시지 인코더를 사용하거나 다음 세 가지 메시지 인코딩 바인딩 중 하나를 사용할 수 있습니다.

  - <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>

  - <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>

  - <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>

맨 아래에는 필수 전송 요소가 있습니다. 사용자 고유의 전송 또는 WCF (전송 바인딩 요소 Windows Communication Foundation) 중 하나를 사용할 수 있습니다.

- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>

- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>

- <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>

- <xref:System.ServiceModel.Channels.PeerTransportBindingElement>

- <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>

- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>

- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>

다음 표에서는 각 계층의 옵션을 요약합니다.

|계층|옵션|필수|
|-----------|-------------|--------------|
|의|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>|아니요|
|안정성|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>|아니요|
|보안|<xref:System.ServiceModel.Channels.SecurityBindingElement>|아니요|
|인코딩|텍스트, 이진, MTOM(Message Transmission Optimization Mechanism), 사용자 지정|예|
|전송|TCP, HTTP, HTTPS, 명명된 파이프(IPC), P2P(Peer-to-Peer), 메시지 큐(MSMQ), 사용자 지정|예|

또한 고유의 바인딩 요소를 정의하여 이전에 정의된 계층 사이에 삽입할 수 있습니다.

## <a name="see-also"></a>참고자료

- [엔드포인트 만들기 개요](../endpoint-creation-overview.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../using-bindings-to-configure-services-and-clients.md)
- [시스템 제공 바인딩](../system-provided-bindings.md)
- [방법: 시스템 제공 바인딩 사용자 지정](how-to-customize-a-system-provided-binding.md)
- [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md)
- [사용자 지정 바인딩](../samples/custom-binding.md)
