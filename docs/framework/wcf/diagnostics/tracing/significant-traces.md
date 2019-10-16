---
title: 중요한 추적
ms.date: 03/30/2017
ms.assetid: 40a1770e-3b09-4142-b0dd-f9ef73642074
ms.openlocfilehash: c230c65b4d3fd45c4905d4ae5f4cbbf90e10faad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61784962"
---
# <a name="significant-traces"></a>중요한 추적
이 항목에서는 Windows Communication Foundation (WCF)에서 내보낸 주요 추적을 보여 줍니다.  
  
## <a name="significant-traces"></a>중요한 추적  
  
|추적|설명|  
|-----------|-----------------|  
|메시지 로그 추적|WCF 메시지를 메시지 로깅을 통해 기록 되 면 추적을 내보냅니다 할 때 기능을 `System.ServiceModel.MessageLogging` 추적 소스를 사용 합니다. 이 추적을 클릭하면 메시지가 표시됩니다. 메시지에 대해 네 가지 구성 가능한 로깅 지점은 `ServiceLevelSendRequest`, `TransportSend`, `TransportReceive` 및 `ServiceLevelReceiveRequest`이며 이러한 로깅 지점도 메시지 로그 추적의 메시지 소스 특성에 표시됩니다.|  
|수신된 메시지 추적|경우에 WCF 메시지를 받을 때이 추적을 내보낸다는 `System.ServiceModel` 추적 소스를 information 또는 verbose 수준에서 사용 합니다. 이 추적은 동작 그래프 보기에서 메시지 상관 관계 화살표를 확인해야 합니다.|  
|전송된 메시지 추적|경우에 WCF 메시지를 보낼 때이 추적을 내보냅니다 여 `System.ServiceModel` 추적 소스를 information 또는 verbose 수준에서 사용 합니다. 이 추적은 동작 그래프 보기에서 메시지 상관 관계 화살표를 확인해야 합니다.|  
|Get ChannelEndpointElement|Information 수준에서 생성 채널 팩터리에 이 추적을 내보냅니다. 클라이언트가 통신하는 엔드포인트에 대한 설명(원격 주소, 바인딩, 계약 이름)을 제공합니다.|  
|Get ServiceElement|Information 수준에서 생성 서비스 호스트에 이 추적을 내보냅니다. 서비스 계약 및 바인딩의 설명을 제공합니다.|  
|SocketConnection create|클라이언트가 수행한 첫 번째 프로세스 동작 및 서비스의 Receive bytes 동작에 이 추적을 내보냅니다. 로컬 및 원격 IP 주소를 제공합니다. Information 수준에서 내보내집니다.|
