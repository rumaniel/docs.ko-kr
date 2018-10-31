---
title: 플러그형 프로토콜 프로그래밍
ms.date: 03/30/2017
helpviewer_keywords:
- downloading Internet resources, pluggable protocols
- WebRequest class, pluggable protocols
- response to Internet request, pluggable protocols
- WebResponse class, pluggable protocols
- sending data, pluggable protocols
- network resources, pluggable protocols
- Internet, pluggable protocols
- programming pluggable protocols
- pluggable protocols, programming
- requesting data from Internet, pluggable protocols
- receiving data, pluggable protocols
- protocols, pluggable
ms.assetid: 66ef8456-7576-4e97-8956-959b216373db
ms.openlocfilehash: 74dd44e704836b209366a7975d08a43375318e90
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50190790"
---
# <a name="programming-pluggable-protocols"></a>플러그형 프로토콜 프로그래밍
추상 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse> 클래스에서 플러그형 프로토콜의 기초를 제공합니다. <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse>에서 프로토콜별 클래스를 파생시키면, 응용 프로그램에서 사용할 프로토콜을 지정하지 않아도 인터넷 리소스에서 데이터를 요청하고 응답을 읽을 수 있습니다.  
  
 Create 메서드를 등록해야 프로토콜별 <xref:System.Net.WebRequest>를 만들 수 있습니다. 특정 인터넷 구성표, 구성표와 서버 또는 구성표, 서버 및 경로에 대한 요청 집합을 처리하려면 <xref:System.Net.WebRequest>의 정적 <xref:System.Net.WebRequest.RegisterPrefix%28System.String%2CSystem.Net.IWebRequestCreate%29> 메서드를 사용하여 <xref:System.Net.WebRequest> 하위 항목을 등록합니다.  
  
 대부분의 경우 <xref:System.Net.WebRequest> 클래스의 속성과 메서드를 사용하여 데이터를 보내고 받을 수 있습니다. 그러나 프로토콜별 속성에 액세스해야 하는 경우 <xref:System.Net.WebRequest>를 특정 파생 클래스 인스턴스로 형식 캐스팅할 수 있습니다.  
  
 플러그형 프로토콜을 이용하려면 <xref:System.Net.WebRequest> 하위 항목에서 프로토콜별 속성을 설정하지 않아도 되는 기본 요청 및 응답 트랜잭션을 제공해야 합니다. 예를 들어 HTTP의 <xref:System.Net.WebRequest> 클래스를 구현하는 <xref:System.Net.HttpWebRequest> 클래스에서 기본적으로 `GET` 요청을 제공하고 웹 서버에서 반환된 스트림을 포함하는 <xref:System.Net.HttpWebResponse>를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [WebRequest에서 파생](../../../docs/framework/network-programming/deriving-from-webrequest.md)  
 [WebResponse에서 파생](../../../docs/framework/network-programming/deriving-from-webresponse.md)  
 [.NET Framework의 네트워크 프로그래밍](../../../docs/framework/network-programming/index.md)  
 [방법: 프로토콜 관련 속성에 액세스하기 위해 WebRequest 형식 캐스팅](../../../docs/framework/network-programming/how-to-typecast-a-webrequest-to-access-protocol-specific-properties.md)
