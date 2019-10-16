---
title: 네트워크 설정 스키마
ms.date: 03/30/2017
helpviewer_keywords:
- elements [.NET Framework], network configuration elements
- sending data, network configuration elements
- receiving data, network configuration elements
- configuration settings [.NET Framework], networks
- Internet, network configuration elements
- network configuration elements
- network settings
- connections [.NET Framework], network configuration elements
- network resources, network configuration elements
ms.assetid: f1de5a0f-76c5-4833-819f-5222b8146340
ms.openlocfilehash: 5e3bd1b1734fc7fba50b72785531a8b001d6d741
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698159"
---
# <a name="network-settings-schema"></a>네트워크 설정 스키마
네트워크 설정으로 .NET Framework의 인터넷 연결 방법을 지정합니다.

@No__t -032> 설정은 .NET Framework 네트워크에 연결 하는 방법을 지정 합니다. 다음 표에서는 [\<system.Net> 요소(네트워크 설정)](system-net-element-network-settings.md)의 각 자식 구성 요소의 기능을 설명합니다.  
  
|요소|설명|  
|-------------|-----------------|  
|[\<authenticationModules> 요소(네트워크 설정)](authenticationmodules-element-network-settings.md)|인터넷 요청을 인증하는 데 사용되는 모듈을 지정합니다.|  
|[\<connectionManagement> 요소(네트워크 설정)](connectionmanagement-element-network-settings.md)|인터넷 호스트에 대한 최대 연결 수를 지정합니다.|  
|[\<defaultProxy> 요소(네트워크 설정)](defaultproxy-element-network-settings.md)|인터넷에 대한 HTTP 요청에 사용할 프록시 서버를 지정합니다.|  
|[\<mailSettings> 요소(네트워크 설정)](mailsettings-element-network-settings.md)|메일 보내기 옵션에 대한 설정을 포함합니다.|  
|[\<requestCaching> 요소(네트워크 설정)](requestcaching-element-network-settings.md)|네트워크 요청에 대 한 캐싱 메커니즘을 제어 합니다.|  
|[\<webRequestModules> 요소 (네트워크 설정)](webrequestmodules-element-network-settings.md)|인터넷 호스트 정보를 요청하는 데 사용되는 모듈을 지정합니다.|  
  
@No__t-0uri > 설정은 .NET Framework Uri (uniform resource identifier)를 사용 하 여 표현 된 웹 주소를 처리 하는 방법을 지정 합니다. 다음 표에서는 [\<uri > 요소 (Uri 설정)](uri-element-uri-settings.md)의 각 자식 구성 요소에 대 한 함수에 대해 설명 합니다.  
  
|요소|설명|  
|-------------|-----------------|  
|[\<IDN> 요소(URI 설정)](idn-element-uri-settings.md)|IDN(Internationalized Domain Name) 구문 분석이 도메인 이름에 적용되는지 지정합니다.|  
|[\<iriParsing> 요소(URI 설정)](iriparsing-element-uri-settings.md)|IRI(International Resource Identifier) 구문 분석이 <xref:System.Uri>에 적용되는지와 IRI 구문 분석 규칙을 적용해야 하는지 지정합니다.|  
|[\<schemeSettings> 요소 (URI 설정)](schemesettings-element-uri-settings.md)|특정 체계에 대해 <xref:System.Uri>가 구문 분석되는 방법을 지정합니다.|  
  
## <a name="see-also"></a>참조

- [인터넷 애플리케이션 구성](../../../network-programming/configuring-internet-applications.md)
- [구성 파일 스키마](../index.md)
