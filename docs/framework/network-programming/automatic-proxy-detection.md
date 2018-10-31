---
title: 자동 프록시 검색
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- automatic proxy detections
- Web Proxy Auto-Discovery
- Web proxy
- detecting proxies automatically
- WebProxy class, automatic proxy detections
- proxies, automatically detecting
- network
- WPAD (Web Proxy Auto-Discovery)
ms.assetid: fcd9c3bd-93de-4c92-8ff3-837327ad18de
ms.openlocfilehash: 3a59347c3fcd72f68ee2ae07ccc638ec43021a3b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188510"
---
# <a name="automatic-proxy-detection"></a>자동 프록시 검색
자동 프록시 검색은 웹 프록시 서버가 시스템에 의해 식별되고 클라이언트 대신 요청을 보내는 데 사용되는 프로세스입니다. 이 기능을 WPAD(웹 프록시 자동 검색)라고도 합니다. 자동 프록시 검색을 사용하면 시스템이 요청에 사용할 수 있는 프록시 집합을 반환하는 프록시 구성 스크립트를 찾으려고 시도합니다. 프록시 구성 스크립트가 발견되면 <xref:System.Net.WebProxy> 인스턴스를 사용하는 요청에 대한 프록시 정보, 요청 스트림 또는 응답이 확보될 때 로컬 컴퓨터에서 스크립트가 다운로드, 컴파일 및 실행됩니다.  
  
 자동 프록시 검색은 <xref:System.Net.WebProxy> 클래스에 의해 수행되며 요청 수준 설정, 구성 파일의 설정 및 Internet Explorer **LAN(Local Area Network)** 대화 상자를 사용하여 지정된 설정을 이용할 수 있습니다.  
  
> [!NOTE]
>  Internet Explorer 주 메뉴에서 **도구**를 선택한 다음 **인터넷 옵션**을 선택하면 Internet Explorer **LAN(Local Area Network) 설정** 대화 상자를 표시할 수 있습니다. 다음으로, **연결** 탭을 선택하고 **LAN 설정**을 클릭합니다.  
  
 자동 프록시 검색을 사용하면 <xref:System.Net.WebProxy> 클래스가 다음과 같이 프록시 구성 스크립트를 찾으려고 시도합니다.  
  
1.  WinINet `InternetQueryOption` 함수는 Internet Explorer에서 가장 최근에 검색된 프록시 구성 스크립트를 찾는 데 사용됩니다.  
  
2.  스크립트를 찾을 수 없는 경우 <xref:System.Net.WebProxy> 클래스는 DHCP(Dynamic Host Configuration Protocol)를 사용하여 스크립트를 찾습니다. DHCP 서버는 스크립트의 위치(호스트 이름) 또는 스크립트에 대한 전체 URL로 응답할 수 있습니다.  
  
3.  DHCP가 WPAD 호스트를 식별하지 않는 경우 WPAD를 해당 이름 또는 별칭으로 사용하여 DNS에서 호스트를 쿼리합니다.  
  
4.  호스트가 확인되지 않고 프록시 구성 스크립트의 위치가 Internet Explorer LAN 설정 또는 구성 파일에서 지정된 경우 이 위치가 사용됩니다.  
  
> [!NOTE]
>  NT 서비스 또는 ASP.NET의 일부로 실행 중인 응용 프로그램은 호출하는 사용자의 Internet Explorer 프록시 서버 설정(사용 가능한 경우)을 사용합니다. 일부 서비스 응용 프로그램에는 이러한 설정을 사용할 수 없습니다.  
  
 프록시는 전화 접속 아이콘별로 구성됩니다. 전화 접속 아이콘은 네트워크 연결 대화 상자에 있는 항목이며, 실제 네트워크 장치(모뎀 또는 이더넷 카드) 또는 가상 인터페이스(예: 네트워크 장치를 통해 실행되는 VPN 연결)일 수 있습니다. 전화 접속 아이콘이 변경되면(예: 무선 연결이 액세스 지점을 변경하거나 VPN이 사용되는 경우) 프록시 검색 알고리즘이 다시 실행됩니다.  
  
 기본적으로 Internet Explorer 프록시 설정이 프록시를 검색하는 데 사용됩니다. 응용 프로그램이 비대화형 계정으로 실행되는 경우(IE 프록시 설정을 구성하는 편리한 방법 없이) 또는 IE 설정과 다른 프록시 설정을 사용하려는 경우 [\<defaultProxy> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md) 및 [\<proxy> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/proxy-element-network-settings.md) 요소가 정의된 구성 파일을 만들어 프록시를 구성할 수 있습니다.  
  
 직접 만든 요청의 경우 다음 코드 예제와 같이 요청과 함께 null <xref:System.Net.WebRequest.Proxy%2A>를 사용하여 요청 수준에서 프록시 자동 검색을 사용하지 않도록 설정할 수 있습니다.  
  
```csharp  
public static void DisableForMyRequest (Uri resource)  
{  
    WebRequest request = WebRequest.Create (resource);  
    request.Proxy = null;  
    WebResponse response = request.GetResponse ();  
}  
```  
  
```vb  
Public Shared Sub DisableForMyRequest(ByVal resource As Uri)  
    Dim request As WebRequest = WebRequest.Create(resource)  
    request.Proxy = Nothing  
    Dim response As WebResponse = request.GetResponse()  
    End Sub   
```  
  
 프록시가 없는 요청은 <xref:System.Net.WebRequest.DefaultWebProxy%2A> 속성에서 사용할 수 있는 응용 프로그램 도메인의 기본 프록시를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.WebProxy>  
 <xref:System.Net.WebRequest>  
 [\<system.Net> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)
