---
title: 메시지 교환 패턴 선택
ms.date: 03/30/2017
ms.assetid: 0f502ca1-6a8e-4607-ba15-59198c0e6146
ms.openlocfilehash: 7dcbea30b53142ed68db9ac138f8c7a665ca1729
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797296"
---
# <a name="choosing-a-message-exchange-pattern"></a>메시지 교환 패턴 선택
사용자 지정 전송을 작성 하는 첫 번째 단계는 개발 중인 채널에 필요한 *메시지 교환 패턴* (또는 meps)을 결정 하는 것입니다. 이 항목에서는 사용 가능한 옵션과 여러 가지 요구 사항에 대해 설명합니다. 채널 개발 작업 목록의 첫 번째 작업 [입니다.](developing-channels.md)  
  
## <a name="six-message-exchange-patterns"></a>여섯 개의 메시지 교환 패턴  
 다음과 같은 세 개의 MEP가 있습니다.  
  
- 데이터그램(<xref:System.ServiceModel.Channels.IInputChannel> 및 <xref:System.ServiceModel.Channels.IOutputChannel>)  
  
     데이터 그램 MEP를 사용 하는 경우 클라이언트는 *화재 및 잊은* 교환을 사용 하 여 메시지를 보냅니다. 실행 후 제거 교환은 성공적인 전달에 대한 out-of-band 확인이 필요한 교환입니다. 메시지는 전송 중에 손실되어 서비스에 전달되지 않을 수 있습니다. 보내기 작업이 클라이언트 쪽에서 완료되더라도 원격 엔드포인트에서 메시지를 수신했다고 보장할 수는 없습니다. 데이터그램은 메시징을 위한 기본적인 빌딩 블록으로, 이 위에 신뢰할 수 있는 프로토콜 및 보안 프로토콜을 포함한 고유 프로토콜을 빌드할 수 있습니다. 클라이언트 데이터그램 채널은 <xref:System.ServiceModel.Channels.IOutputChannel> 인터페이스를 구현하고, 서비스 데이터그램 채널은 <xref:System.ServiceModel.Channels.IInputChannel> 인터페이스를 구현합니다.  
  
- 요청-응답(<xref:System.ServiceModel.Channels.IRequestChannel> 및 <xref:System.ServiceModel.Channels.IReplyChannel>)  
  
     이 MEP에서는 메시지가 전송되고 회신이 수신됩니다. 이 패턴은 요청-응답 쌍으로 구성됩니다. RPC(원격 프로시저 호출) 및 브라우저 GET 요청 등이 요청-응답 호출에 해당합니다. 이 패턴을 반이중이라고도 합니다. 이 MEP에서 클라이언트 채널은 <xref:System.ServiceModel.Channels.IRequestChannel>을 구현하고 서비스 채널은 <xref:System.ServiceModel.Channels.IReplyChannel>을 구현합니다.  
  
- 이중(<xref:System.ServiceModel.Channels.IDuplexChannel>)  
  
     이중 MEP를 사용하면 임의 개수의 메시지를 클라이언트에서 보내고 임의의 순서로 받을 수 있습니다. 이중 MEP는 말로 전달되는 각 단어가 메시지에 해당하는 전화 통화와 같습니다. 이 MEP에서는 양측의 송/수신이 가능하기 때문에 클라이언트와 서비스 채널에서 <xref:System.ServiceModel.Channels.IDuplexChannel> 인터페이스를 구현합니다.  
  
 ![메시지 교환 패턴 선택](./media/wcfc-basicthreemepsc.gif "wcfc_BasicThreeMEPsc")  
다음은 세 가지 기본 메시지 교환 패턴으로 위에서부터 차례로 데이터그램, 요청-응답 및 이중 교환 패턴입니다.  
  
 이러한 MEPs는 각각 *세션*을 지원할 수도 있습니다. 세션(및 <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType> 형식의 <xref:System.ServiceModel.Channels.ISession?displayProperty=nameWithType> 구현)은 채널에서 주고 받는 모든 메시지와 상호 관련됩니다. 요청-응답 패턴은 요청과 회신이 상호 관련되어 있지만 독립 실행형 두 메시지 세션입니다. 반면, 세션을 지원하는 요청-응답 패턴은 해당 채널의 모든 요청/응답 쌍이 상호 관련되어 있음을 의미합니다. 이런 식으로 다음과 같이 총 여섯 개의 MEP가 제공됩니다.  
  
- 데이터그램  
  
- 요청-응답  
  
- 이중  
  
- 세션 지원 데이터그램 MEP  
  
- 세션 지원 요청-응답 MEP  
  
- 세션 지원 이중 MEP  
  
> [!NOTE]
> UDP 전송의 경우 UDP는 본래 실행 후 제거 프로토콜이므로 데이터그램 MEP만 지원됩니다.  
  
## <a name="sessions-and-sessionful-channels"></a>세션 및 세션 채널  
 네트워킹 환경에는 TCP와 같은 연결 지향 프로토콜과 UDP와 같은 연결 지양 프로토콜이 있습니다. WCF는 세션 이라는 용어를 사용 하 여 연결과 비슷한 논리적 추상화를 의미 합니다. 세션 WCF 프로토콜은 연결 지향 네트워크 프로토콜과 비슷하며 세션 없는 WCF 프로토콜은 연결 지양 네트워크 프로토콜과 비슷합니다.  
  
 채널 개체 모델에서 각각의 논리적 세션은 세션 채널의 인스턴스로 매니페스트됩니다. 따라서 클라이언트에서 만들어져 서비스에서 허용되는 모든 새 세션은 클라이언트와 서비스 측의 새 세션 채널에 해당합니다. 다음은 위와 아래에 세션 없는 채널 구조와 세션 채널 구조가 각각 표시된 다이어그램입니다.  
  
 ![메시지 교환 패턴 선택](./media/wcfc-sessionandsessionlesschannelsc.gif "wcfc_SessionAndSessionlessChannelsc")  
  
 클라이언트는 새로운 세션 채널을 만들어 메시지를 보냅니다. 그러면 서비스 측에서 채널 수신기가 이 메시지를 받고 해당 메시지가 새 세션에 속하는 것으로 감지하여, 새 세션 채널을 만들고 채널 수신기의 AcceptChannel을 호출하는 애플리케이션에 대한 응답으로 이를 애플리케이션에 전달합니다. 그럼 다음 애플리케이션에서는 이 메시지를 비롯한, 동일한 세션 채널을 통해 같은 세션에서 보내진 모든 후속 메시지를 받습니다.  
  
 다른 클라이언트 또는 같은 클라이언트에서도 새로운 세션 채널을 만들어 메시지를 보냅니다. 채널 수신기는 이 메시지가 새 세션에 있는 것으로 감지하고 새 세션 채널을 만드는데, 이 프로세스가 반복됩니다.  
  
 세션이 없는 경우에는 채널과 세션 간에 상호 관련성이 없습니다. 따라서 채널 수신기는 모든 수신 메시지가 애플리케이션에 전달되는 하나의 채널만 만듭니다. 메시지 순서를 관리할 세션이 없으므로 메시지에 대한 순서 지정도 없습니다. 이러한 세션 없는 메시지 교환에 대해서는 이전 그림의 상단에 설명되어 있습니다.  
  
## <a name="starting-and-terminating-sessions"></a>세션 시작 및 종료  
 세션 채널이 새로 만들어지면 클라이언트에서 세션이 시작됩니다. 또한 새 세션에서 전송된 메시지를 서비스에서 받으면 서비스에서 세션이 시작됩니다. 이와 마찬가지로, 세션 채널을 닫거나 중단하면 세션이 종료됩니다.  
  
 하지만 이중 세션 통신 패턴으로 메시지를 보내고 받는 데 모두 사용되는 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>은 이 경우에 예외입니다. 한 쪽에서 메시지 전송은 중단하고 메시지 수신을 계속하길 원할 수 있는데, 이 경우 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>을 사용하면 출력 세션을 닫을 수 있는 메커니즘이 제공됩니다. 즉, 더 이상 메시지를 보내지 않지만 계속해서 메시지를 받을 수 있도록 입력 세션이 열린 상태로 유지됩니다.  
  
 일반적으로 세션은 들어오는 쪽이 아닌 나가는 쪽에서 닫힙니다. 즉, 세션 출력 채널을 닫아 세션을 완전히 종료할 수 있습니다. 세션 출력 채널을 닫으면 해당 세션 입력 채널에서는 <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>를 호출하는 애플리케이션에 null을 반환합니다.  
  
 하지만 세션 입력 채널은 <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>가세션이 이미 닫혀 있음을 나타내는 null을 반환하지 않는 이상 닫히지 않습니다. <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>가null을 반환하지 않은 상태에서 세션 입력 채널을 닫으면 채널을 닫는 동안 예기치 않은 메시지를 받을 수 있으므로 예외가 throw됩니다. 발신자가 세션을 종료하기 전에 수신자가 세션을 종료하려면 갑자기 세션이 종료되는 <xref:System.ServiceModel.ICommunicationObject.Abort%2A>를 입력 채널에서 호출해야 합니다.  
  
## <a name="writing-sessionful-channels"></a>세션 채널 작성  
 세션 채널 작성자로서 채널에서 세션 제공을 위해 수행해야 할 몇 가지 사항이 있습니다. 보내는 쪽의 채널에서는 다음이 이루어져야 합니다.  
  
- 각각의 새로운 채널에 대해 새 세션을 만들고 이를 고유 문자열인 새 세션 ID와 연결합니다. 또는 스택 내 하위 세션 채널에서 새 세션을 얻습니다.  
  
- 세션을 하위 계층에서 얻지 않고 채널에서 세션을 만든 경우에는, 이 채널을 통해 보낸 각 메시지에 대해 해당 메시지를 세션과 연결해야 합니다. 이러한 작업은 프로토콜 채널의 경우 일반적으로 SOAP 헤더를 추가하여 이루어지고, 전송 채널의 경우에는 새 전송 연결을 만들거나 세션 정보를 프레이밍 프로토콜에 추가하여 이루어집니다.  
  
- 이 채널을 통해 보낸 각 메시지에 대해, 앞서 설명한 전달 보장이 이루어져야 합니다. 세션을 제공하는 데 하위 채널을 사용하면 해당 채널을 통해서도 전달 보장이 이루어집니다. 사용자가 세션을 직접 제공할 경우에는 이러한 보장을 프로토콜의 일부로 구현해야 합니다. 일반적으로 양쪽 모두에서 WCF를 사용하는 것으로 가정하는 프로토콜 채널을 작성하는 경우에는 TCP 전송이나 신뢰할 수 있는 메시징 채널이 필요할 수 있고, 세션을 제공하는 데에는 어느 쪽이든 사용할 수 있습니다.  
  
- 채널에서 <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType>가 호출되면 지정된 시간 제한이나 기본 시간 제한을 사용하여 세션을 닫는 데 필요한 작업을 수행합니다. 이 작업은 세션을 하위 채널에서 얻은 경우 해당 채널에서 <xref:System.ServiceModel.ICommunicationObject.Close%2A>를 호출하거나 특별한 SOAP 메시지를 보내거나 전송 연결을 닫는 작업만큼이나 간단합니다.  
  
- 채널에서 <xref:System.ServiceModel.ICommunicationObject.Abort%2A>를 호출하면 I/O가 수행되지 않고 세션이 갑자기 종료됩니다. 즉, 수행된 작업이 없거나 네트워크 연결 또는 일부 다른 리소스가 중단될 수 있습니다.  
  
 받는 쪽의 채널에서는 다음이 이루어져야 합니다.  
  
- 들어오는 각 메시지에 대해, 채널 수신기에서 해당 메시지가 속한 세션을 감지해야 합니다. 세션의 첫 번째 메시지에 대해서는 채널 수신기가 새 채널을 만들고 <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A?displayProperty=nameWithType>에 대한 호출에서 이를 반환해야 합니다. 그렇지 않으면 채널 수신기가 세션에 해당하는 기존 채널을 찾아 해당 채널을 통해 메시지를 전달해야 합니다.  
  
- 요구되는 전달 보장과 함께 채널에서 세션을 제공하는 경우에는 받는 쪽에서 메시지 순서 변경이나 승인 전송 등의 일부 작업을 수행해야 합니다.  
  
- 채널에서 <xref:System.ServiceModel.ICommunicationObject.Close%2A>가 호출되면 지정된 시간 제한이나 기본 시간 제한을 사용하여 세션을 닫는 데 필요한 작업을 수행합니다. 이로 인해 종료 시간 제한 만료를 기다리는 동안 채널에서 메시지를 받을 경우 예외가 발생할 수 있는데, 이는 채널이 메시지를 받을 때 Closing 상태에 있기 때문입니다.  
  
- 채널에서 <xref:System.ServiceModel.ICommunicationObject.Abort%2A>를 호출하면 I/O가 수행되지 않고 세션이 갑자기 종료됩니다. 위에서 언급한 바와 같이, 이는 수행된 작업이 없거나 네트워크 연결 또는 일부 다른 리소스가 중단될 수 있음을 의미합니다.  
  
## <a name="see-also"></a>참고자료

- [채널 모델 개요](channel-model-overview.md)
