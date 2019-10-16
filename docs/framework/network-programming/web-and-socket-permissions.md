---
title: 웹 및 소켓 사용 권한
ms.date: 03/30/2017
helpviewer_keywords:
- Networking
- positions [.NET Framework], accepting
- sockets, permissions
- network, permissions
- Internet, permissions
- Network Resources
- SocketPermission class, about SocketPermission class
- positions [.NET Framework], connecting
- WebPermission class, about WebPermission class
- permissions [.NET Framework], sockets
- security [.NET Framework], Internet
- positions [.NET Framework], granting
ms.assetid: d51ad8cb-03ae-4a51-bfcd-cfcf6b98afa9
ms.openlocfilehash: d1b993acbf20eac244e596075c3f826bba3211a1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046860"
---
# <a name="web-and-socket-permissions"></a>웹 및 소켓 사용 권한
<xref:System.Net> 네임스페이스를 사용하는 애플리케이션에 대한 인터넷 보안은 <xref:System.Net.WebPermission> 및 <xref:System.Net.SocketPermission> 클래스에서 제공됩니다. **WebPermission** 클래스는 URI의 데이터를 요청하거나 인터넷에 URI를 제공하는 애플리케이션의 권한을 제어합니다. **SocketPermission** 클래스는 <xref:System.Net.Sockets.Socket>을 사용하여 로컬 포트에서 데이터를 허용하거나 호스트, 포트 번호 및 전송 프로토콜에 따라 다른 주소에서 전송 프로토콜을 사용하여 원격 디바이스에 연결하는 애플리케이션의 권한을 제어합니다.  
  
 사용하는 권한 클래스는 애플리케이션 유형에 따라 달라집니다. <xref:System.Net.WebRequest> 및 해당 하위 항목을 사용하는 애플리케이션은 **WebPermission** 클래스를 사용하여 권한을 관리해야 합니다. 소켓 수준 액세스를 사용하는 애플리케이션은 **SocketPermission** 클래스를 사용하여 권한을 관리해야 합니다.  
  
 **WebPermission** 및 **SocketPermission**은 두 개의 권한인 허용과 연결을 정의합니다. 허용은 다른 파티에서 들어오는 연결에 응답하는 권한을 애플리케이션에 부여합니다. 연결은 다른 파티에 대한 연결을 시작하는 권한을 애플리케이션에 부여합니다.  
  
 **SocketPermission** 인스턴스의 경우 허용은 애플리케이션이 로컬 전송 주소에서 들어오는 연결을 허용할 수 있음을 의미하고, 연결은 애플리케이션이 일부 원격(또는 로컬) 전송 주소에 연결할 수 있음을 의미합니다.  
  
 **WebPermission** 인스턴스의 경우 허용은 애플리케이션이 **WebPermission**에 의해 제어되는 URI을 전 세계에 내보낼 수 있음을 의미합니다. 연결은 애플리케이션이 원격 또는 로컬 여부에 관계없이 해당 URI에 액세스할 수 있음을 의미합니다.  
  
## <a name="see-also"></a>참고 항목

- [보안](../../standard/security/index.md)
- [네트워크 프로그래밍의 보안](security-in-network-programming.md)
