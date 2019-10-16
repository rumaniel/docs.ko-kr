---
title: 컨텍스트 교환 프로토콜
ms.date: 03/30/2017
ms.assetid: 3dfd38e0-ae52-491c-94f4-7a862b9843d4
ms.openlocfilehash: 19780cccc74f8c3615dc844e47be7613ca5f8bc1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69911200"
---
# <a name="context-exchange-protocol"></a>컨텍스트 교환 프로토콜
이 섹션에서는 Windows Communication Foundation (WCF) 릴리스 .NET Framework 버전 3.5에 도입 된 컨텍스트 교환 프로토콜에 대해 설명 합니다. 클라이언트 채널에서는 이 프로토콜을 사용하여 서비스에서 제공되는 컨텍스트를 수락하고, 동일한 클라이언트 채널 인스턴스를 통해 보내는 해당 서비스에 대한 모든 후속 요청에 이 컨텍스트를 적용합니다. 컨텍스트 교환 프로토콜의 구현에서는 다음 두 가지 메커니즘 중 하나를 사용 하 여 서버와 클라이언트 간에 컨텍스트를 전파할 수 있습니다. HTTP 쿠키 또는 SOAP 헤더.  
  
 컨텍스트 교환 프로토콜은 사용자 지정 채널 계층에서 구현됩니다. 채널은 <xref:System.ServiceModel.Channels.ContextMessageProperty> 속성을 사용하여 애플리케이션 계층 간에 컨텍스트를 전달합니다. 엔드포인트 간 전송을 위해 컨텍스트 값은 채널 계층에서 SOAP 헤더로 serialize되거나 HTTP 요청 및 응답을 나타내는 메시지 속성 간에 변환됩니다. 후자의 경우, 기존 채널 계층 중 하나가 HTTP 요청 및 응답 메시지 속성을 HTTP 쿠키로 변환하거나 HTTP 쿠키를 HTTP 요청 및 응답 메시지 속성으로 변환합니다. 컨텍스트 교환에 사용하는 메커니즘은 <xref:System.ServiceModel.Channels.ContextExchangeMechanism>에서 <xref:System.ServiceModel.Channels.ContextBindingElement> 속성을 사용하여 선택합니다. 유효한 값은 `HttpCookie` 또는 `SoapHeader`입니다.  
  
 클라이언트에서 채널의 인스턴스는 채널 속성 <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A>의 설정에 따라 두 가지 모드에서 작동할 수 있습니다.  
  
## <a name="mode-1-channel-context-management"></a>모드 1: 채널 컨텍스트 관리  
 <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A>가 `true`로 설정된 경우 이 모드가 기본 모드입니다. 이 모드에서 컨텍스트 채널은 컨텍스트를 관리하고 수명 중에 컨텍스트를 캐시합니다. `IContextManager` 메서드를 호출하여 채널 속성 `GetContext`를 통해 채널에서 컨텍스트를 검색할 수 있습니다. 채널 속성에서 `SetContext` 메서드를 호출하여 채널을 열기 전에 특정 컨텍스트로 채널을 미리 초기화할 수도 있습니다. 컨텍스트를 사용하여 초기화된 채널은 다시 설정할 수 없습니다.  
  
 다음은 이 모드의 고정 조건 목록입니다.  
  
- 채널이 열린 후에 `SetContext`를 사용하여 컨텍스트를 다시 설정하려고 하면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
- 보내는 메시지에 <xref:System.ServiceModel.Channels.ContextMessageProperty>를 사용하여 컨텍스트를 보내려고 하면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
- 특정 컨텍스트를 사용하여 서버에서 메시지를 받은 경우 채널이 이미 특정 컨텍스트로 초기화되었으면 <xref:System.ServiceModel.ProtocolException>이 생성됩니다.  
  
    > [!NOTE]
    > 채널이 컨텍스트 집합 없이 명시적으로 열린 경우에만 서버에서 초기 컨텍스트를 받을 수 있습니다.  
  
- 들어오는 메시지의 <xref:System.ServiceModel.Channels.ContextMessageProperty>는 항상 null입니다.  
  
## <a name="mode-2-application-context-management"></a>모드 2: 응용 프로그램 컨텍스트 관리  
 <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A>가 `false`로 설정된 경우의 모드입니다. 이 모드에서 컨텍스트 채널은 컨텍스트를 관리하지 않습니다. <xref:System.ServiceModel.Channels.ContextMessageProperty>를 사용하여 컨텍스트를 검색, 관리 및 적용하는 것은 애플리케이션의 역할입니다. `GetContext` 또는 `SetContext`를 호출하려고 하면 <xref:System.InvalidOperationException>이 발생합니다.  
  
 선택한 모드에 관계없이 클라이언트 채널 팩토리는 <xref:System.ServiceModel.Channels.IRequestChannel>, <xref:System.ServiceModel.Channels.IRequestSessionChannel> 및 <xref:System.ServiceModel.Channels.IDuplexSessionChannel> 메시지 교환 패턴을 지원합니다.  
  
 서비스에서 채널의 인스턴스는 들어오는 메시지에서 클라이언트가 제공한 컨텍스트를 <xref:System.ServiceModel.Channels.ContextMessageProperty>로 변환합니다. 애플리케이션 계층 또는 호출 스택의 위쪽에 있는 다른 채널에서 메시지 속성에 액세스할 수 있습니다. 서비스 채널을 사용하면 애플리케이션 계층에서도 응답 메시지에 <xref:System.ServiceModel.Channels.ContextMessageProperty>를 첨부하여 클라이언트에 다시 전파할 새 컨텍스트 값을 지정할 수 있습니다. 이 속성은 바인딩 구성에 따라 달라지는 컨텍스트가 포함된 SOAP 헤더 또는 HTTP 쿠키로 변환됩니다. 서비스 채널 수신기는 <xref:System.ServiceModel.Channels.IReplyChannel>, <xref:System.ServiceModel.Channels.IReplySessionChannel> 및 <xref:System.ServiceModel.Channels.IReplySessionChannel> 메시지 교환 패턴을 지원합니다.  
  
 컨텍스트 교환 프로토콜은 컨텍스트를 전파할 때 HTTP 쿠키를 사용하지 않는 경우에 컨텍스트 정보를 나타낼 새 `wsc:Context` SOAP 헤더를 도입했습니다. 컨텍스트 헤더 스키마는 각각 문자열 키와 문자열 내용이 포함된 임의의 수의 자식 요소를 허용합니다. 다음은 컨텍스트 헤더의 예제입니다.  
  
 `<Context xmlns="http://schemas.microsoft.com/ws/2006/05/context">`  
  
 `<property name="myContext">context-2</property>`  
  
 `</Context>`  
  
 `HttpCookie` 모드에서는 `SetCookie` 헤더를 사용하여 쿠키가 설정됩니다. 쿠키 이름은 `WscContext`입니다. 쿠키 값은 `wsc:Context` 헤더의 Base64 인코딩입니다. 이 값은 따옴표로 묶여집니다.  
  
 WS-Addressing 헤더는 서비스에서 요청을 디스패치할 위치를 결정하는 데 사용되기 때문에 보호되어야 하며, 이와 동일한 이유로 컨텍스트 값도 전송 중에 수정되지 않도록 보호되어야 합니다. 따라서 `wsc:Context` 헤더는 바인딩이 메시지 보호 기능을 제공하는 경우 SOAP 또는 전송 수준에서 디지털 서명되거나 서명 후에 암호화되어야 합니다. 컨텍스트를 전파하는 데 사용되는 HTTP 쿠키는 전송 보안을 사용하여 보호해야 합니다.  
  
 컨텍스트 교환 프로토콜을 지원해야 하는 서비스 엔드포인트에서는 이를 게시된 정책에 명시할 수 있습니다. 클라이언트가 SOAP 수준에서 컨텍스트 교환 프로토콜을 지원하기 위한 요구 사항 또는 클라이언트가 HTTP 쿠키 지원을 사용하기 위한 요구 사항을 나타내기 위해 두 개의 새로운 정책 어설션이 도입되었습니다. 서비스 측의 정책에 대한 이러한 어설션의 생성은 다음과 같이 <xref:System.ServiceModel.Channels.ContextBindingElement.ContextExchangeMechanism%2A> 속성의 값으로 제어됩니다.  
  
- <xref:System.ServiceModel.Channels.ContextExchangeMechanism.ContextSoapHeader>의 경우 다음 어설션이 생성됩니다.  
  
    ```xml  
    <IncludeContext   
    xmlns="http://schemas.microsoft.com/ws/2006/05/context"  
    protectionLevel="Sign" />  
    ```  
  
- <xref:System.ServiceModel.Channels.ContextExchangeMechanism.HttpCookie>의 경우 다음 어설션이 생성됩니다.  
  
    ```xml  
    <HttpUseCookie xmlns="http://schemas.xmlsoap.org/soap/http"/>  
    ```  
  
## <a name="see-also"></a>참고자료

- [웹 서비스 프로토콜 상호 운용성 가이드](../../../../docs/framework/wcf/feature-details/web-services-protocols-interoperability-guide.md)
