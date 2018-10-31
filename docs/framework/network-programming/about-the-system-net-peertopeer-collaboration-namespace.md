---
title: System.Net.PeerToPeer.Collaboration 네임스페이스 정보
ms.date: 03/30/2017
ms.assetid: b5d8c1c1-6844-4947-9759-c7f1b564bded
ms.openlocfilehash: 9e95dc571bc520c0abd0cf676ce37f383fed84ba
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197082"
---
# <a name="about-the-systemnetpeertopeercollaboration-namespace"></a>System.Net.PeerToPeer.Collaboration 네임스페이스 정보
<xref:System.Net.PeerToPeer.Collaboration> 네임스페이스는 피어 투 피어 공동 작업 인프라를 사용하여 피어 공동 작업 활동을 구현하는 데 사용되는 클래스 및 API를 제공합니다.  
  
## <a name="classes"></a>클래스  
 피어 투 피어 공동 작업 구현에 사용되는 기본 클래스는 다음과 같습니다.  
  
-   <xref:System.Net.PeerToPeer.Collaboration.ContactManager> - 피어 연락처를 저장하는 데 사용할 수 있습니다.  
  
-   <xref:System.Net.PeerToPeer.Collaboration.PeerApplication> - 게임, 채팅 클라이언트, 회의 솔루션 등 공동 작업하는 응용 프로그램입니다.  
  
-   활동에서 공동 작업할 피어.  이러한 피어는 <xref:System.Net.PeerToPeer.Collaboration.PeerContact>, <xref:System.Net.PeerToPeer.Collaboration.PeerNearMe> 또는 <xref:System.Net.PeerToPeer.Collaboration.PeerEndPoint> 개체로 나타낼 수 있습니다.  
  
-   정적 <xref:System.Net.PeerToPeer.Collaboration.PeerCollaboration> 클래스 자체 - 사용할 수 있는 응용 프로그램 및 참여하는 피어를 지정합니다.  
  
 <xref:System.Net.PeerToPeer.Collaboration.PeerContact.Invite%2A> 메서드는 공동 작업 세션에 피어를 초대하는 데 사용됩니다.  호출하는 피어는 공동 작업 세션과 연결된 응용 프로그램, 개체 또는 현재 상태 정보에 대한 업데이트를 알리는 이벤트를 위해 다른 피어를 구독할 수 있습니다. 현재 상태 클래스는 <xref:System.Net.PeerToPeer.Collaboration.Peer>를 공동 작업에 사용할 수 있는지 여부를 지정하고, <xref:System.Net.PeerToPeer.Collaboration.PeerScope> 클래스는 피어에 허용되는 참여 정도를 <xref:System.Net.PeerToPeer.Collaboration.PeerScope.Internet>(전역), <xref:System.Net.PeerToPeer.Collaboration.PeerScope.NearMe>(서브넷) 또는 <xref:System.Net.PeerToPeer.Collaboration.PeerScope.None> 등으로 지정하는 데 사용됩니다.  
  
 공동 작업 세션은 다음 네 단계로 구성됩니다.  
  
-   검색. 응용 프로그램, 피어 및 현재 상태 정보를 검색하거나 게시합니다.  예를 들어 동일한 게임이 설치되어 있는 로컬 서브넷에서 다른 사용자를 찾습니다.  
  
-   초대. 원격 피어에게 <xref:System.Net.PeerToPeer.Collaboration.PeerCollaboration> 세션을 시작하거나 참여하라는 보안 초대를 보내고 수락합니다.  
  
-   연락처 관리. 검색된 피어를 <xref:System.Net.PeerToPeer.Collaboration.ContactManager>에 연락처로 추가합니다.  
  
-   통신. 통신이 설정되면 <xref:System.Net> API, <xref:System.Net.PeerToPeer> API 또는 Windows Communication Foundation 피어 채널 클래스를 다자간 통신에 사용합니다.  
  
 예를 들어 호스트 피어는 공동 작업 세션을 시작하고 <xref:System.Net.PeerToPeer.Collaboration.ContactManager.CreateContact%2A> 메서드를 활용하여 원격 피어 및 로컬 피어 중 하나를 호스트 피어의 연락처 관리자에 추가합니다.  그런 다음 세 명의 사용자가 개인 공동 작업 세션에 참여합니다.  
  
 일반적인 P2P 응용 프로그램은 공동 작업 기록 또는 화이트보드 작성을 위한 전화 회의, 서버가 없는 채팅 응용 프로그램, 대화형 보급 알림, 온라인 게임 세션 등입니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.PeerToPeer.Collaboration>
