---
title: 서비스 채널 수준 프로그래밍
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8d8dcd85-0a05-4c44-8861-4a0b3b90cca9
ms.openlocfilehash: be5c73e2ac9fcc45d136280c869148326cd91315
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857761"
---
# <a name="service-channel-level-programming"></a>서비스 채널 수준 프로그래밍
이 항목에서는 사용 하지 않고 Windows Communication Foundation (WCF) 서비스 응용 프로그램을 작성 하는 방법을 설명 합니다 <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> 및 관련된 개체 모델입니다.  
  
## <a name="receiving-messages"></a>메시지 받기  
 메시지를 받은 다음 처리할 준비를 하려면 다음 단계가 필요합니다.  
  
1. 바인딩을 만듭니다.  
  
2. 채널 수신기를 빌드합니다.  
  
3. 채널 수신기를 엽니다.  
  
4. 요청을 읽고 회신을 보냅니다.  
  
5. 모든 채널 개체를 닫습니다.  
  
#### <a name="creating-a-binding"></a>바인딩 만들기  
 메시지를 수신 대기하고 받는 첫 번째 단계는 바인딩을 만드는 것입니다. WCF 인스턴스화 중 하나에서 직접 사용할 수 있는 여러 기본 제공 또는 시스템 제공 바인딩이 포함 되어 있습니다. 또한 목록 1의 코드가 수행하는 작업인 CustomBinding 클래스를 인스턴스화하여 사용자 지정 바인딩을 만들 수도 있습니다.  
  
 아래의 코드 예제에서는 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>의 인스턴스를 만들고 <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType>를 채널 스택을 빌드하는 데 사용되는 바인딩 요소의 컬렉션인 해당 요소 컬렉션에 추가합니다. 이 예제에서는 요소 컬렉션에 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>만 있으므로 결과 채널 스택에는 HTTP 전송 채널만 있게 됩니다.  
  
#### <a name="building-a-channellistener"></a>ChannelListener 빌드  
 바인딩을 만든 후에 <xref:System.ServiceModel.Channels.Binding.BuildChannelListener%2A?displayProperty=nameWithType>을 호출하여 형식 매개 변수가 만들 채널 셰이프인 채널 수신기를 빌드합니다. 이 예제에서는 요청/회신 메시지 교환 패턴으로 들어오는 메시지를 수신 대기하려고 하므로 <xref:System.ServiceModel.Channels.IReplyChannel?displayProperty=nameWithType>을 사용합니다.  
  
 <xref:System.ServiceModel.Channels.IReplyChannel>은 요청 메시지를 받고 회신 메시지를 다시 보내는 데 사용됩니다. <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A?displayProperty=nameWithType>를 호출하면 요청 메시지를 받고 회신 메시지를 다시 보내는 데 사용할 수 있는 <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType>을 반환합니다.  
  
 수신기를 만들 때 수신하는 네트워크 주소를 전달합니다. 이 경우는 `http://localhost:8080/channelapp`입니다. 일반적으로 각 전송 채널은 하나 또는 여러 개의 주소 스키마를 지원합니다. 예를 들면 HTTP 전송은 http와 https 스키마를 모두 지원합니다.  
  
 또한 수신기를 만들 때 빈 <xref:System.ServiceModel.Channels.BindingParameterCollection?displayProperty=nameWithType>을 전달합니다. 바인딩 매개 변수는 수신기가 빌드되는 방식을 제어하는 매개 변수를 전달하는 메커니즘입니다. 예제에서는 그러한 매개 변수를 사용하지 않으므로 빈 컬렉션을 전달합니다.  
  
#### <a name="listening-for-incoming-messages"></a>들어오는 메시지 수신 대기  
 수신기에서 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType>을 호출하고 채널을 수락합니다. <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A?displayProperty=nameWithType>의 동작은 전송이 연결 지향인지, 연결 지양인지에 따라 다릅니다. 연결 지향 전송에서 <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A>은 새 연결 요청이 들어올 때까지 차단됩니다. 이 시점에서 새 연결을 나타내는 새 채널을 반환합니다. HTTP와 같은 연결 지양 전송에서 <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A>은 전송 수신기가 만드는 유일한 채널과 함께 즉시 반환됩니다.  
  
 이 예제에서 수신기는 <xref:System.ServiceModel.Channels.IReplyChannel>을 구현하는 채널을 반환합니다. 이 채널에서 메시지를 받기 위해 먼저 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType>을 호출하여 통신 준비 상태로 전환합니다. 그런 다음 메시지가 도착할 때까지 차단되는 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A>를 호출합니다.  
  
#### <a name="reading-the-request-and-sending-a-reply"></a>요청 읽기 및 회신 보내기  
 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A>가 <xref:System.ServiceModel.Channels.RequestContext>를 반환하면 <xref:System.ServiceModel.Channels.RequestContext.RequestMessage%2A> 속성을 사용하여 받은 메시지를 가져옵니다. 메시지 동작 및 본문 내용(문자열)을 작성합니다.  
  
 회신을 보내려면 이 경우 요청에서 받은 문자열 데이터를 다시 전달하는 새 회신 메시지를 만듭니다. 그런 다음 <xref:System.ServiceModel.Channels.RequestContext.Reply%2A>를 호출하여 회신 메시지를 보냅니다.  
  
#### <a name="closing-objects"></a>개체 닫기  
 리소스 누수를 방지하려면 통신에 사용된 개체가 더 이상 필요하지 않은 경우 그 개체를 닫아야 합니다. 이 예제에서는 요청 메시지, 요청 컨텍스트, 채널 및 수신기를 닫습니다.  
  
 다음 코드 예제에서는 채널 수신기가 한 메시지만 받는 기본 서비스를 보여 줍니다. 실제 서비스는 서비스가 종료될 때까지 채널을 계속 수락하고 메시지를 받습니다.  
  
 [!code-csharp[ChannelProgrammingBasic#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/serviceprogram.cs#1)]
 [!code-vb[ChannelProgrammingBasic#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/serviceprogram.vb#1)]
