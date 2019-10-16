---
title: 클라이언트 채널 수준 프로그래밍
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3b787719-4e77-4e77-96a6-5b15a11b995a
ms.openlocfilehash: 4f24c558b1d5303b2417416beb14555539f498ea
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797264"
---
# <a name="client-channel-level-programming"></a>클라이언트 채널 수준 프로그래밍
이 항목에서는 <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType> 클래스 및 관련 개체 모델을 사용 하지 않고 WCF (Windows Communication Foundation) 클라이언트 응용 프로그램을 작성 하는 방법에 대해 설명 합니다.  
  
## <a name="sending-messages"></a>메시지 보내기  
 메시지를 보낸 다음 회신을 받고 처리할 준비를 하려면 다음 단계가 필요합니다.  
  
1. 바인딩을 만듭니다.  
  
2. 채널 팩터리를 빌드합니다.  
  
3. 채널을 만듭니다.  
  
4. 요청을 보내고 회신을 읽습니다.  
  
5. 모든 채널 개체를 닫습니다.  
  
#### <a name="creating-a-binding"></a>바인딩 만들기  
 수신 사례와 유사 하 게 ( [서비스 채널 수준 프로그래밍](service-channel-level-programming.md)참조) 바인딩을 만들어 메시지를 보냅니다. 이 예제에서는 새 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>을 만들고 <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType>를 요소 컬렉션에 추가합니다.  
  
#### <a name="building-a-channelfactory"></a>ChannelFactory 빌드  
 이번에는 <xref:System.ServiceModel.Channels.IChannelListener?displayProperty=nameWithType>를 만드는 대신 형식 매개 변수가 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>인 바인딩에서 <xref:System.ServiceModel.ChannelFactory.CreateFactory%2A?displayProperty=nameWithType>를 호출하여 <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType>를 만듭니다. 채널 수신기는 들어오는 메시지를 기다리는 측에서 사용하는 반면에 채널 팩터리는 채널을 만들기 위해 통신을 시작하는 측에서 사용합니다. 채널 수신기에서처럼 채널 팩터리를 사용하기 전에 먼저 열어야 합니다.  
  
#### <a name="creating-a-channel"></a>채널 만들기  
 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType>을 호출하여 <xref:System.ServiceModel.Channels.IRequestChannel>을 만듭니다. 이 호출을 통해 만들려는 새 채널을 사용하여 통신할 엔드포인트의 주소를 가져옵니다. 채널이 있는 경우 채널에서 열기를 호출하여 통신 준비 상태로 설정합니다. 전송 특성에 따라 이 열기 호출을 통해 대상 엔드포인트와 연결을 시작하거나 네트워크 상에서 아무것도 수행하지 않을 수 있습니다.  
  
#### <a name="sending-a-request-and-reading-the-reply"></a>요청 보내기 및 회신 읽기  
 채널이 열린 상태이면 메시지를 만들고 채널 요청 메서드를 사용하여 해당 요청을 보낸 다음 수신할 회신을 기다릴 수 있습니다. 이 메서드가 반환되면 엔드포인트의 회신이 무엇인지 찾기 위해 읽을 수 있는 회신 메시지를 제공 받습니다.  
  
#### <a name="closing-objects"></a>개체 닫기  
 리소스 누수를 방지하기 위해 통신에서 사용되는 개체가 더 이상 필요 없는 경우 닫습니다.  
  
 다음 코드 예제에서는 메시지를 보내고 회신을 읽기 위해 채널 팩터리를 사용하는 기본 클라이언트를 보여 줍니다.  
  
 [!code-csharp[ChannelProgrammingBasic#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/clientprogram.cs#2)]
 [!code-vb[ChannelProgrammingBasic#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/clientprogram.vb#2)]
