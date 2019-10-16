---
title: 인터넷 애플리케이션 구성
ms.date: 03/30/2017
helpviewer_keywords:
- downloading Internet resources, default proxy
- sending data, default proxy
- receiving data, default proxy
- downloading Internet resources, configuring Internet applications
- protocol-specific modules
- custom authentication modules
- receiving data, configuring Internet applications
- configuration settings [.NET Framework], Internet applications
- requesting data from Internet, configuring Internet applications
- requesting data from Internet, default proxy
- response to Internet request, default proxy
- Internet, configuring Internet applications
- response to Internet request, configuring Internet applications
- default proxy
- network resources, default proxy
- sending data, configuring Internet applications
- network resources, configuring Internet applications
- Internet, default proxy
ms.assetid: bb707c72-eed2-4a82-8800-c9e68df2fd4f
ms.openlocfilehash: ee4dc87383153ae4e8df0a3bed7cce5220e65405
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71048628"
---
# <a name="configuring-internet-applications"></a>인터넷 애플리케이션 구성
[\<system.Net&gt; 요소(네트워크 설정)](../configure-apps/file-schema/network/system-net-element-network-settings.md) 구성 요소에는 애플리케이션에 대한 네트워크 구성 정보가 들어 있습니다. [\<system.Net&gt; 요소(네트워크 설정)](../configure-apps/file-schema/network/system-net-element-network-settings.md) 구성 요소를 사용하여 프록시 서버를 설정하고, 연결 관리 매개 변수를 설정하고, 애플리케이션에 사용자 지정 인증 및 요청 모듈을 포함할 수 있습니다.  
  
 [\<defaultProxy> 요소(네트워크 설정)](../configure-apps/file-schema/network/defaultproxy-element-network-settings.md) 구성 요소는 `GlobalProxySelection` 클래스에서 반환된 프록시 서버를 정의합니다. 자체적인 <xref:System.Net.HttpWebRequest.Proxy%2A> 속성이 특정 값으로 설정되지 않은 <xref:System.Net.HttpWebRequest>는 기본 프록시를 사용합니다. 프록시 주소를 설정하는 것 이외에 프록시를 사용하지 않을 서버 주소 목록을 만들고 로컬 주소에 프록시를 사용하지 않도록 지정할 수 있습니다.  
  
 Microsoft Internet Explorer 설정은 구성 설정과 결합되고 구성 설정이 우선 적용된다는 점을 기억해야 합니다.  
  
 다음 예제에서는 기본 프록시 서버 주소를 `http://proxyserver`로 설정하고, 로컬 주소에 프록시를 사용하지 않도록 지정하고, contoso.com 도메인에 있는 서버에 대한 모든 요청이 프록시를 바이패스하도록 지정합니다.  
  
```xml  
<configuration>  
    <system.net>  
        <defaultProxy>  
            <proxy  
                usesystemdefault = "false"  
                proxyaddress = "http://proxyserver:80"  
                bypassonlocal = "true"  
            />  
            <bypasslist>  
                <add address="http://[a-z]+\.contoso\.com/" />  
            </bypasslist>  
        </defaultProxy>  
    </system.net>  
</configuration>  
```  
  
 [\<connectionManagement> 요소(네트워크 설정)](../configure-apps/file-schema/network/connectionmanagement-element-network-settings.md) 구성 요소를 사용하여 특정 서버 또는 모든 기타 서버에 대해 설정할 수 있는 영구 연결 수를 구성합니다. 다음 예제에서는 애플리케이션에서 `www.contoso.com`에 대한 영구 연결 2개, IP 주소 192.168.1.2를 사용한 서버에 대한 영구 연결 4개, 모든 기타 서버에 대한 영구 연결 1개를 사용하도록 구성합니다.  
  
```xml  
<configuration>  
    <system.net>  
        <connectionManagement>  
            <add address="http://www.contoso.com" maxconnection="2" />  
            <add address="192.168.1.2" maxconnection="4" />  
            <add address="*" maxconnection="1" />  
        </connectionManagement>  
    </system.net>  
</configuration>  
```  
  
 사용자 지정 인증 모듈은 [\<authenticationModules> 요소(네트워크 설정)](../configure-apps/file-schema/network/authenticationmodules-element-network-settings.md) 구성 요소를 사용하여 구성됩니다. 사용자 지정 인증 모듈은 <xref:System.Net.IAuthenticationModule> 인터페이스를 구현해야 합니다.  
  
 다음 예제에서는 사용자 지정 인증 모듈을 구성합니다.  
  
```xml  
<configuration>  
    <system.net>  
        <authenticationModules>  
            <add type="MyAuthModule, MyAuthModule.dll" />  
        </authenticationModules>  
    </system.net>  
</configuration>  
```  
  
 [\<webRequestModules&gt; 요소(네트워크 설정)](../configure-apps/file-schema/network/webrequestmodules-element-network-settings.md) 구성 요소를 사용하여 애플리케이션에서 프로토콜별 모듈을 통해 인터넷 리소스의 정보를 요청하도록 구성합니다. 지정된 모듈은 <xref:System.Net.IWebRequestCreate> 인터페이스를 구현해야 합니다. 다음 예제와 같이 구성 파일에서 사용자 지정 모듈을 지정하여 기본 HTTP, HTTPS 및 파일 요청 모듈을 재정의할 수 있습니다.  
  
```xml  
<configuration>  
    <system.net>  
        <webRequestModules>  
            <add  
                prefix="HTTP"  
                type = "MyHttpRequest.dll, MyHttpRequestCreator"  
            />  
        </webRequestModules>  
    </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목

- [.NET Framework의 네트워크 프로그래밍](index.md)
- [네트워크 설정 스키마](../configure-apps/file-schema/network/index.md)
- [\<system.Net> 요소(네트워크 설정)](../configure-apps/file-schema/network/system-net-element-network-settings.md)
