---
title: HttpTransportBindingElement
ms.date: 03/30/2017
ms.assetid: 088a7bce-6bb2-4839-ad74-f68d4b1aa0f9
ms.openlocfilehash: 5e23342d57621554aaec67c5c568bb75202a9454
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61963490"
---
# <a name="httptransportbindingelement"></a>HttpTransportBindingElement
HttpTransportBindingElement  
  
## <a name="syntax"></a>구문  
  
```csharp
class HttpTransportBindingElement : TransportBindingElement  
{  
  boolean AllowCookies;  
  string AuthenticationScheme;  
  boolean BypassProxyOnLocal;  
  string HostNameComparisonMode;  
  boolean KeepAliveEnabled;  
  sint32 MaxBufferSize;  
  string ProxyAddress;  
  string ProxyAuthenticationScheme;  
  string Realm;  
  string TransferMode;  
  boolean UnsafeConnectionNtlmAuthentication;  
  boolean UseDefaultWebProxy;  
};  
```  
  
## <a name="methods"></a>메서드  
 HttpTransportBindingElement 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 HttpTransportBindingElement 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="allowcookies"></a>AllowCookies  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 클라이언트가 쿠키를 수락하고 그러한 쿠키를 이후 요청에 전파할지 여부를 나타내는 값입니다.  
  
### <a name="authenticationscheme"></a>AuthenticationScheme  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 HTTP 수신기가 처리하는 클라이언트 요청을 인증하는 데 사용되는 인증 스키마입니다.  
  
### <a name="bypassproxyonlocal"></a>BypassProxyOnLocal  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 로컬 주소의 프록시를 무시할지 여부를 나타내는 값입니다.  
  
### <a name="hostnamecomparisonmode"></a>HostNameComparisonMode  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 URI를 일치시킬 때 서비스에 연결하기 위해 호스트 이름이 사용되는지 여부를 나타내는 값입니다.  
  
### <a name="keepaliveenabled"></a>KeepAliveEnabled  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 선택하면 동작 수준에 상관없이 HTTP 연결이 유지됩니다.  
  
### <a name="maxbuffersize"></a>MaxBufferSize  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 버퍼 풀의 최대 크기입니다.  
  
### <a name="proxyaddress"></a>ProxyAddress  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 HTTP 요청에 사용할 프록시의 주소를 포함하는 URI입니다.  
  
### <a name="proxyauthenticationscheme"></a>ProxyAuthenticationScheme  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 HTTP 프록시가 처리하는 클라이언트 체계를 인증하는 데 사용되는 인증 스키마입니다.  
  
### <a name="realm"></a>Realm  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 인증 영역입니다.  
  
### <a name="transfermode"></a>TransferMode  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 메시지가 버퍼링되거나 스트리밍되는지 또는 요청이나 응답인지 지정하는 값입니다.  
  
### <a name="unsafeconnectionntlmauthentication"></a>UnsafeConnectionNtlmAuthentication  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 서버에서 안전하지 않은 연결 공유를 사용할 수 있는지 여부를 나타내는 값입니다.  
  
### <a name="usedefaultwebproxy"></a>UseDefaultWebProxy  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 사용자별 설정이 아닌 시스템 수준의 프록시 설정을 사용할지 여부를 나타내는 값입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
