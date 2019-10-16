---
title: 채널 모델 개요
ms.date: 03/30/2017
helpviewer_keywords:
- channel model [WCF]
ms.assetid: 07a81e11-3911-4632-90d2-cca99825b5bd
ms.openlocfilehash: 362a7392d9dbaedb1942280a6c3b6c8f2139afe5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795895"
---
# <a name="channel-model-overview"></a>채널 모델 개요
WCF (Windows Communication Foundation) 채널 스택은 메시지를 처리 하는 하나 이상의 채널을 포함 하는 계층화 된 통신 스택입니다. 스택의 맨 아래에는 채널 스택을 TCP, HTTP, SMTP 및 기타 다른 유형의 전송과 같은 기본 전송에 적용하는 전송 채널이 있습니다. 채널은 메시지를 보내고 받기 위한 하위 수준의 프로그래밍 모델을 제공합니다. 이 프로그래밍 모델은 WCF 채널 모델 이라고 하는 여러 인터페이스 및 기타 형식을 사용 합니다. 이 항목에서는 채널 셰이프, 서비스에서의 기본 채널 수신기 생성 및 클라이언트에서의 채널 팩터리 생성에 대해 설명합니다.  
  
## <a name="channel-stack"></a>채널 스택  
 WCF 끝점은 채널 스택 이라는 통신 스택을 사용 하 여 세계와 통신 합니다. 다음 다이어그램에서는 채널 스택을 TCP/IP 등의 다른 통신 스택과 비교합니다.  
  
 ![Channel Model](./media/wcfc-channelstackhighlevelc.gif "wcfc_ChannelStackHighLevelc")  
  
 먼저 유사성은 다음과 같습니다. 두 경우 모두 스택의 각 계층은 해당 계층 아래 세계의 일부 추상화를 제공 하 고 해당 추상화를 바로 위에 있는 계층에만 노출 합니다. 각 계층에서는 바로 아래 계층에 대한 추상화만 사용합니다. 또한 두 경우 모두, 두 스택이 통신할 때 각 계층은 상대 스택의 해당 계층과 통신합니다. 예를 들어 IP 계층은 IP 계층끼리, TCP 계층은 TCP 계층끼리 통신합니다.  
  
 이제 다음과 같은 차이점이 있습니다. TCP 스택은 실제 네트워크의 추상화를 제공 하도록 설계 되었지만 채널 스택은 메시지 배달 방법, 즉 전송 뿐만 아니라 메시지의 내용과 같은 기타 기능에 대 한 추상화를 제공 하도록 설계 되었습니다. 프로토콜은 전송을 포함 하 여 통신에 사용 되지만 그 보다 훨씬 더 많습니다. 예를 들어 신뢰할 수 있는 세션 바인딩 요소는 채널 스택의 일부지만 전송 아래에 있거나 전송 자체는 아닙니다. 이러한 추상화는 스택의 맨 아래 채널에게 기본 전송 프로토콜을 채널 스택 아키텍처에 적용하도록 요구한 다음, 안정성 보장 및 보안과 같은 통신 기능을 제공하기 위해 스택의 상위 채널을 사용하는 방식으로 이루어집니다.  
  
 메시지는 <xref:System.ServiceModel.Channels.Message> 개체와 같은 통신 스택을 통해 이동합니다. 위 그림과 같이 맨 아래 채널을 전송 채널이라고 하며, 이 채널을 통해 메시지를 다른 상대방과 주고 받게 됩니다. 또한 <xref:System.ServiceModel.Channels.Message> 개체를 다른 상대방과 통신하기 위한 형식으로 변환하기도 합니다. 이 전송 채널 위에는 안정된 전달 보장과 같은 통신 기능을 제공하는 여러 프로토콜 채널이 있을 수 있습니다. 프로토콜 채널은 <xref:System.ServiceModel.Channels.Message> 개체의 형태로 프로토콜 채널을 통해 이동하는 메시지를 바탕으로 작동합니다. 그리고 일반적으로 헤더 추가 또는 본문 암호화 등을 통해 메시지를 변환하거나 수신 승인과 같은 자체 프로토콜 제어 메시지를 주고 받습니다.  
  
## <a name="channel-shapes"></a>채널 셰이프  
 각 채널에서는 채널 셰이프 인터페이스 또는 채널 셰이프라고 하는 인터페이스를 하나 이상 구현합니다. 이러한 채널 셰이프에서는 채널에서 구현되어 채널 사용자가 호출하는 보내기 및 받기 또는 요청 및 응답과 같은 통신 기반 메서드를 제공합니다. 채널 셰이프 <xref:System.ServiceModel.Channels.IChannel> 는 인터페이스입니다 .이 인터페이스는 스택에서 채널에 의해 노출 되는 임의의 기능 `GetProperty`에 액세스 하기 위한 계층화 된 메커니즘으로 사용 되는 \<T > 메서드를 제공 하는 인터페이스입니다. <xref:System.ServiceModel.Channels.IChannel>을 확장하는 다섯 개의 채널 셰이프는 다음과 같습니다.  
  
- <xref:System.ServiceModel.Channels.IInputChannel>  
  
- <xref:System.ServiceModel.Channels.IOutputChannel>  
  
- <xref:System.ServiceModel.Channels.IRequestChannel>  
  
- <xref:System.ServiceModel.Channels.IReplyChannel>  
  
- <xref:System.ServiceModel.Channels.IDuplexChannel>  
  
 또한 이러한 각 셰이프에는 세션 지원을 위해 <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType>을 확장하는 해당 항목이 있습니다. 이러한 항목은 다음과 같습니다.  
  
- <xref:System.ServiceModel.Channels.IInputSessionChannel>  
  
- <xref:System.ServiceModel.Channels.IOutputSessionChannel>  
  
- <xref:System.ServiceModel.Channels.IRequestSessionChannel>  
  
- <xref:System.ServiceModel.Channels.IReplySessionChannel>  
  
- <xref:System.ServiceModel.Channels.IDuplexSessionChannel>  
  
 채널 셰이프는 기존 전송 프로토콜에서 지원하는 몇 가지 기본 메시지 교환 패턴에 따라 패턴화됩니다. 예를 들어 단방향 메시징은 쌍에 해당 하 <xref:System.ServiceModel.Channels.IInputChannel> 고, 요청-회신 <xref:System.ServiceModel.Channels.IReplyChannel> / / <xref:System.ServiceModel.Channels.IOutputChannel> <xref:System.ServiceModel.Channels.IRequestChannel> 은 쌍에 해당 하 고, 양방향 이중 통신은 <xref:System.ServiceModel.Channels.IDuplexChannel> 다음에 해당 합니다. (및 <xref:System.ServiceModel.Channels.IInputChannel> <xref:System.ServiceModel.Channels.IOutputChannel>)를 모두 확장 합니다.  
  
## <a name="programming-with-the-channel-stack"></a>채널 스택을 사용한 프로그래밍  
 채널 스택은 일반적으로 바인딩을 통해 채널 스택이 만들어지는 팩터리 패턴을 사용하여 만들어집니다. 보내는 쪽에서 바인딩을 사용하여 <xref:System.ServiceModel.ChannelFactory>를 빌드하는데, 이를 통해 채널 스택을 차례로 빌드하고 스택의 맨 위 채널에 참조를 반환합니다. 그러면 애플리케이션에서 이 채널을 사용하여 메시지를 보낼 수 있습니다. 자세한 내용은 [클라이언트 채널 수준 프로그래밍](client-channel-level-programming.md)을 참조 하세요.  
  
 받는 쪽에서는 바인딩을 사용하여 <xref:System.ServiceModel.Channels.IChannelListener>를 빌드하는데, 이를 통해 들어오는 메시지를 수신 대기합니다. <xref:System.ServiceModel.Channels.IChannelListener>에서는 채널 스택을 만들고 맨 위 채널에 응용 프로그램 참조를 전달하여 메시지를 수신 대기 응용 프로그램에 제공합니다. 그러면 애플리케이션에서 이 채널을 사용하여, 들어오는 메시지를 받습니다. 자세한 내용은 [서비스 채널 수준 프로그래밍](service-channel-level-programming.md)을 참조 하세요.  
  
## <a name="the-channel-object-model"></a>채널 개체 모델  
 채널 개체 모델은 채널, 채널 수신기 및 채널 팩터리를 구현하는 데 필요한 핵심 인터페이스 집합입니다. 또한 사용자 지정 구현을 도와 주는 몇 가지 기본 클래스도 있습니다.  
  
 채널 수신기는 들어오는 메시지를 수신 대기한 다음, 이를 채널 수신기에서 만든 채널을 통해 위 계층으로 전달합니다.  
  
 채널 팩터리는 메시지를 전송하고 만들어진 모든 채널을 채널 팩터리 종료 시 닫는 데 사용하는 채널을 만듭니다.  
  
 <xref:System.ServiceModel.ICommunicationObject>는 모든 통신 개체가 구현하는 기본 상태 시스템을 정의하는 핵심 인터페이스입니다. <xref:System.ServiceModel.Channels.CommunicationObject>는 다른 채널 클래스가 인터페이스를 다시 구현하지 않고 파생할 수 있는 이 핵심 인터페이스의 구현을 제공합니다. 하지만 반드시 이렇게 할 필요는 없으며, 사용자 지정 채널을 통해 <xref:System.ServiceModel.ICommunicationObject>를 <xref:System.ServiceModel.Channels.CommunicationObject>에서 상속하지 않고 바로 구현할 수도 있습니다. 그림 3의 클래스는 모두 채널 모델의 일부로 간주되지 않으며, 채널을 빌드하려는 사용자 지정 채널 구현자가 사용할 수 있는 도우미입니다.  
  
 ![채널 모델](./media/wcfc-wcfcchannelsigure3omumtreec.gif "wcfc_WCFCChannelsigure3OMUMTreec")  
  
 다음 항목에서는 채널 개체 모델 및 사용자 지정 채널을 편리하게 빌드할 수 있는 다양한 개발 영역에 대해 설명합니다.  
  
|항목|설명|  
|-----------|-----------------|  
|[출력소 채널 수신기 및 채널](service-channel-listeners-and-channels.md)|서비스 응용 프로그램에서 들어오는 채널을 수신 대기하는 채널 수신기에 대해 설명합니다.|  
|[클라이언트로 채널 팩터리 및 채널](client-channel-factories-and-channels.md)|서비스 응용 프로그램에 연결할 채널을 만드는 채널 팩터리에 대해 설명합니다.|  
|[상태 변경 이해](understanding-state-changes.md)|<xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType> 인터페이스 모델 상태가 채널에서 어떻게 바뀌는지에 대해 설명합니다.|  
|[메시지 교환 패턴 선택](choosing-a-message-exchange-pattern.md)|채널에서 지원할 수 있는 여섯 가지의 기본 메시지 교환 패턴에 대해 설명합니다.|  
|[예외 및 오류 처리](handling-exceptions-and-faults.md)|사용자 지정 채널에서 오류 및 예외를 처리하는 방법에 대해 설명합니다.|  
|[구성 및 메타데이터 지원](configuration-and-metadata-support.md)|응용 프로그램 모델에서 사용자 지정 채널을 사용할 수 있도록 지원하는 방법과 바인딩 및 바인딩 요소를 사용하여 메타데이터를 가져오거나 내보내는 방법에 대해 설명합니다.|
