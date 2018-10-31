---
title: WCF 및 ASP.NET Web API
ms.date: 03/30/2017
ms.assetid: 08ceded3-fd9a-4467-9715-c4cbd9c7228e
ms.openlocfilehash: 9ff974ca59b5a6448a140cbb1e7d6e8114840bdf
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198421"
---
# <a name="wcf-and-aspnet-web-api"></a>WCF 및 ASP.NET Web API
WCF는 서비스 기반 응용 프로그램을 빌드하기 위한 Microsoft의 통합 프로그래밍 모델이며, 이를 통해 개발자는 플랫폼 간에 통합되고 기존 투자와 상호 운용할 수 있는 안정적인 보안 트랜잭션된 솔루션을 빌드할 수 있습니다. [ASP.NET Web API](https://www.asp.net/web-api) 쉽고 광범위 한 브라우저 및 모바일 장치를 비롯 하 여 클라이언트를 연결 하는 HTTP 서비스를 구축할 수 있는 프레임 워크입니다. ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다. 이 항목에서는 요구 사항에 가장 적합한 기술을 결정하는 데 도움이 되는 몇 가지 지침을 제공합니다.  
  
## <a name="choosing-which-technology-to-use"></a>사용할 기술 선택  
 다음 표에서는 각 기술의 주요 기능에 대해 설명합니다.  
  
|WCF|ASP.NET Web API|  
|---------|---------------------|  
|여러 전송 프로토콜(HTTP, TCP, UDP 및 사용자 지정 전송)을 지원하며 이러한 전송 프로토콜 간의 전환을 허용하는 서비스를 빌드할 수 있습니다.|HTTP 전용. HTTP에 대 한 최고 수준의 프로그래밍 모델입니다. 다양 한 브라우저의 폭넓은 지원 등 사용 하도록 설정 하는 모바일 장치에서 액세스를 위해 더 적합 합니다.|  
|동일한 메시지 유형의 여러 인코딩(텍스트, MTOM 및 이진)을 지원하며 이러한 인코딩 간의 전환을 허용하는 서비스를 빌드할 수 있습니다.|XML, JSON 등을 비롯한 광범위한 미디어 형식을 지원하는 웹 API를 빌드할 수 있습니다.|  
|Reliable Messaging, Transactions, Message Security 같은 WS-* 표준을 사용하는 서비스 빌드를 지원합니다.|기본 프로토콜을 사용 하 고 HTTP, WebSockets, SSL, JSON 및 XML과 같은 형식입니다. Reliable Messaging 또는 Transactions와 같은 상위 수준 프로토콜은 지원하지 않습니다.|  
|요청-회신, 단방향 및 이중 메시지 교환 패턴을 지원합니다.|추가 패턴을 통해 지원 될 수 있지만 HTTP는 요청/응답 [SignalR](https://github.com/SignalR/SignalR) 및 Websocket 통합 합니다.|  
|WCF SOAP 서비스는 자동화된 도구로 클라이언트 프록시를 생성할 수 있는 WSDL로 기술될 수 있습니다. 이는 복잡한 스키마를 사용하는 서비스의 경우에도 해당됩니다.|자동 생성된 HTML 도움말 페이지에서부터 OData 통합 API에 대한 구조적 메타데이터에 이르기까지 다양한 방법으로 웹 API를 기술할 수 있습니다.|  
|.NET Framework와 함께 제공됩니다.|.NET Framework와 함께 제공되지만, 오픈 소스로서 out-of-band 방식으로도 제공되므로 독립적으로 다운로드할 수도 있습니다.|  
  
 WCF를 사용 하 여 다양 한 전송 방식을 통해 액세스할 수 있는 안정적이 고 안전한 웹 서비스를 만듭니다. 광범위한 클라이언트에서 액세스할 수 있는 HTTP 기반 서비스를 만들려면 ASP.NET Web API를 사용하십시오. 새로운 REST 스타일의 서비스를 만들고 디자인하려는 경우에는 ASP.NET Web API를 사용하십시오. WCF도 REST 스타일의 서비스를 작성하기 위한 몇 가지 기능을 지원하지만, ASP.NET Web API에서는 REST를 보다 완전하게 지원하며 향후의 모든 REST 기능 개선 사항도 ASP.NET Web API에서 구현될 것입니다. 기존 WCF 서비스가 있고 추가 REST 엔드포인트를 노출하려는 경우에는 WCF와 <xref:System.ServiceModel.WebHttpBinding>을 사용하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Windows Communication Foundation 정의](../../../docs/framework/wcf/whats-wcf.md)  
 [기본적인 Windows Communication Foundation 개념](../../../docs/framework/wcf/fundamental-concepts.md)  
