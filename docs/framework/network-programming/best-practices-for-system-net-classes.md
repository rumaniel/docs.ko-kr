---
title: System.Net 클래스에 대한 모범 사례
ms.date: 03/30/2017
helpviewer_keywords:
- sending data, best practices
- requesting data from Internet, best practices
- WebRequest class, best practices
- data requests, best practices
- WebResponse class, best practices
- best practices, data requests
- receiving data, best practices
ms.assetid: 716decc6-5952-47b7-9c5a-ba6fc5698684
ms.openlocfilehash: ce365d088c01ae4a89c77713b6970ae3389b3f0e
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50190952"
---
# <a name="best-practices-for-systemnet-classes"></a>System.Net 클래스에 대한 모범 사례
다음 권장 사항은 <xref:System.Net>에 포함된 클래스를 최대한 활용하는 데 도움이 됩니다.  
  
-   TLS(전송 계층 보안) 모범 사례는 [.NET Framework를 사용한 TLS(전송 계층 보안) 모범 사례](tls.md)를 참조하세요.

-   가능한 경우 하위 클래스에 대한 형식 캐스팅 대신 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse>를 사용합니다. **WebRequest** 및 **WebResponse**를 사용하는 응용 프로그램은 광범위한 코드 변경 없이 새 인터넷 프로토콜을 활용할 수 있습니다.  
  
-   **System.Net** 클래스를 사용하여 서버에서 실행되는 ASP.NET 응용 프로그램을 작성할 때는 성능 관점에서 대체로 <xref:System.Net.WebRequest.GetResponse%2A> 및 <xref:System.Net.WebResponse.GetResponseStream%2A>에 대해 비동기 메서드를 사용하는 것이 좋습니다.  
  
-   인터넷 리소스에 대해 열린 연결 수는 네트워크 성능 및 처리량에 상당한 영향을 줄 수 있습니다. **System.Net**은 기본적으로 호스트당 응용 프로그램마다 두 개의 연결을 사용합니다. 응용 프로그램에 대한 <xref:System.Net.ServicePoint>의 <xref:System.Net.ServicePoint.ConnectionLimit%2A> 속성을 설정하면 특정 호스트에 대해 이 개수를 늘릴 수 있습니다. <xref:System.Net.ServicePointManager.DefaultPersistentConnectionLimit?displayProperty=nameWithType> 속성을 설정하면 모든 호스트에 대해 이 기본값을 늘릴 수 있습니다.  
  
-   소켓 수준 프로토콜을 작성할 때는 가능한 경우 <xref:System.Net.Sockets.Socket>에 직접 작성하는 대신 <xref:System.Net.Sockets.TcpClient> 또는 <xref:System.Net.Sockets.UdpClient>를 사용합니다. 이러한 두 클라이언트 클래스는 연결의 세부 정보를 처리할 필요 없이 TCP 및 UDP 소켓 생성을 캡슐화합니다.  
  
-   자격 증명을 요구하는 사이트에 액세스하는 경우 요청할 때마다 자격 증명을 제공하는 대신 <xref:System.Net.CredentialCache> 클래스를 사용하여 자격 증명 캐시를 만듭니다. **CredentialCache** 클래스는 캐시를 검색하여 요청과 함께 제공할 적절한 자격 증명을 찾아 URL을 기준으로 자격 증명을 만들고 제공해야 하는 부담을 덜어줍니다.  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 네트워크 프로그래밍](../../../docs/framework/network-programming/index.md)
