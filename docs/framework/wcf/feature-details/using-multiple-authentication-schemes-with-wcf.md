---
title: WCF와 함께 여러 인증 스키마 사용
ms.date: 03/30/2017
ms.assetid: f32a56a0-e2b2-46bf-a302-29e1275917f9
ms.openlocfilehash: b0f5da9a4c6fdfede9a86434f49f9e9821778176
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61932683"
---
# <a name="using-multiple-authentication-schemes-with-wcf"></a>WCF와 함께 여러 인증 스키마 사용
이제 WCF를 사용하여 단일 엔드포인트에 여러 인증 체계를 지정할 수 있습니다. 또한 웹 호스팅 서비스가 IIS에서 직접 인증 설정을 상속할 수 있습니다. 자체 호스팅 서비스는 사용할 수 있는 인증 체계를 지정할 수 있습니다. IIS에서 인증 설정을 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [IIS 인증](https://go.microsoft.com/fwlink/?LinkId=232458)  
  
## <a name="iis-hosted-services"></a>IIS에서 호스트되는 서비스  
 IIS에서 호스트되는 서비스의 경우 IIS에서 사용할 인증 체계를 설정합니다. 다음 서비스의 web.config 파일에서 바인딩 구성에서 clientCredential 형식을 "inheritedfromhost" 표시 된 대로 지정 다음 XML 조각에서:  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 ServiceAuthenticationBehavior를 사용 하 여 서비스를 사용 하 여 사용할 인증 체계의 하위 집합만 지정할 수 있습니다 또는 \<serviceAuthenticationManager > 요소입니다. 이를 코드로 구성할 때는 다음 코드 조각에서와 같이 ServiceAuthenticationBehavior를 사용합니다.  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
```  
  
 이 구성 파일에서 구성할 때 사용 된 \<serviceAuthenticationManager > 다음 XML 코드 조각에 나와 있는 것 처럼 요소.  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 그러면 IIS에서 선택된 항목에 따라 여기에 나열된 인증 체계의 하위 집합만 서비스 엔드포인트에 적용되는 것으로 간주됩니다. 즉, 개발자는 serviceAuthenticationManager 목록에서 기본 인증을 생략하여 목록에서 기본 인증을 제외할 수 있으며, IIS에서 사용할 수 있는 인증의 경우에도 서비스 엔드포인트에 적용되지 않습니다.  
  
## <a name="self-hosted-services"></a>자체 호스팅 서비스  
 자체 호스팅 서비스는 설정을 상속할 IIS가 없으므로 약간 다르게 구성됩니다. 여기서 사용은 \<serviceAuthenticationManager > 요소 또는 ServiceAuthenticationBehavior를 상속 되는 인증 설정을 지정할 수 있습니다. 코드는 다음과 비슷합니다.  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
```  
  
 구성은 다음과 비슷합니다.  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 그런 다음, 아래 XML 조각에 나와 있는 것처럼 바인딩 설정에 InheritFromHost를 지정할 수 있습니다.  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 또는 다음 구성 조각에서와 같이 HTTP 전송 바인딩 요소에 인증 체계를 설정하여 사용자 지정 바인딩에 인증 체계를 지정할 수 있습니다.  
  
```xml  
<binding name="multipleBinding">  
      <textMessageEncoding/>  
      <httpTransport authenticationScheme="Negotiate, Ntlm, Digest, Basic" />  
    </binding>  
```  
  
## <a name="see-also"></a>참고자료

- [바인딩 및 보안](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)
- [끝점: 주소, 바인딩 및 계약](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
- [시스템 제공 바인딩 구성](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)
- [사용자 지정 바인딩을 사용하는 보안 기능](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [바인딩](../../../../docs/framework/wcf/feature-details/bindings.md)
- [사용자 지정 바인딩](../../../../docs/framework/wcf/extending/custom-bindings.md)
