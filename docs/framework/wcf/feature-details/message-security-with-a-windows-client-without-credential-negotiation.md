---
title: 자격 증명 협상 없이 Windows 클라이언트를 사용하는 메시지 보안
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fc07a26c-cbee-41c5-8fb0-329085fef749
ms.openlocfilehash: 09ca073a39322e54433c25321e3a9ef44c9efe90
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199372"
---
# <a name="message-security-with-a-windows-client-without-credential-negotiation"></a>자격 증명 협상 없이 Windows 클라이언트를 사용하는 메시지 보안
다음 시나리오에는 Windows Communication Foundation (WCF) 클라이언트 및 Kerberos 프로토콜에 의해 보호 되는 서비스를 보여 줍니다.  
  
 서비스와 클라이언트 모두 동일한 도메인 또는 신뢰할 수 있는 도메인에 있습니다.  
  
> [!NOTE]
>  이 시나리오의 차이점 및 [Windows 클라이언트를 사용 하 여 메시지 보안](../../../../docs/framework/wcf/feature-details/message-security-with-a-windows-client.md) 은이 시나리오는 응용 프로그램 메시지를 보내기 전에 서비스를 사용 하 여 서비스 자격 증명을 협상 하지 않습니다. 또한 이 시나리오에는 Kerberos 프로토콜이 필요하기 때문에 Windows 도메인 환경이 필요합니다.  
  
 ![메시지 보안 자격 증명 협상이](../../../../docs/framework/wcf/feature-details/media/0c9f9baa-2439-4ef9-92f4-43c242d85d0d.gif "0c9f9baa-2439-4ef9-92f4-43c242d85d0d")  
  
|특성|설명|  
|--------------------|-----------------|  
|보안 모드|메시지|  
|상호 운용성|예, 클라이언트와 호환되는 WS-Security 및 Kerberos 토큰 프로필과 상호 운용할 수 있습니다.|  
|인증(서버)|서버와 클라이언트의 상호 인증|  
|인증(클라이언트)|서버와 클라이언트의 상호 인증|  
|무결성|예|  
|기밀성|예|  
|전송|HTTP|  
|바인딩|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a>서비스  
 다음 코드와 구성은 독립적으로 실행되어야 합니다. 다음 작업 중 하나를 수행합니다.  
  
-   구성 없이 코드를 사용하여 독립 실행형 서비스를 만듭니다.  
  
-   제공된 구성을 사용하여 서비스를 만들지만 엔드포인트를 정의하지 않습니다.  
  
### <a name="code"></a>코드  
 다음 코드에서는 메시지 보안을 사용하는 서비스 엔드포인트를 만듭니다. 코드는 서비스 자격 증명 협상과 SCT(보안 컨텍스트 토큰) 설정을 비활성화합니다.  
  
> [!NOTE]
>  Windows 자격 증명 형식을 협상 없이 사용하려면 서비스의 사용자 계정이 Active Directory 도메인에 등록된 SPN(서비스 사용자 이름)에 대한 액세스 권한이 있어야 합니다. 이 작업은  
  
1.  `NetworkService` 또는 `LocalSystem` 계정을 사용하여 서비스를 실행합니다. WCF는 서비스의 메타 데이터 (웹 서비스 설명에서에서 끝점 서비스의 적절 한 SPN 요소를 자동으로 생성 이러한 계정이 컴퓨터 시스템을 Active Directory 도메인에 연결할 때 설정 된 SPN에 대 한 액세스를 수, 있으므로 언어 또는 WSDL)입니다.  
  
2.  임의의 Active Directory 도메인 계정을 사용하여 서비스를 실행합니다. 이 경우 해당 도메인 계정에 대한 SPN을 설정해야 합니다. 그렇게 하는 한 가지 방법으로 Setspn.exe 유틸리티 도구를 사용합니다. SPN이 만들어지면 서비스의 계정에 대 한 메타 데이터 (WSDL)를 통해 서비스 클라이언트에 SPN을 게시 하는 WCF를 구성 합니다. 이 작업은 응용 프로그램 구성 파일이나 코드를 통해 노출된 엔드포인트에 대한 엔드포인트 ID를 설정하여 수행합니다. 다음 예제에서는 ID를 프로그래밍 방식으로 게시합니다.  
  
 Spn에 대 한 자세한 정보, Kerberos 프로토콜 및 Active Directory에 대 한 참조 [Kerberos 기술 보완에 대 한 Windows](https://go.microsoft.com/fwlink/?LinkId=88330)합니다. 끝점 id에 대 한 자세한 내용은 참조 하세요. [SecurityBindingElement 인증 모드](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)합니다.  
  
 [!code-csharp[C_SecurityScenarios#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#12)]
 [!code-vb[C_SecurityScenarios#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#12)]  
  
### <a name="configuration"></a>구성  
 코드 대신 다음 구성을 사용할 수 있습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration="" name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"   
                  binding="wsHttpBinding"  
                  bindingConfiguration="KerberosBinding"  
                  name="WSHttpBinding_ICalculator"  
                  contract="ServiceModel.ICalculator"   
                  listenUri="net.tcp://localhost/metadata" >  
         <identity>  
            <servicePrincipalName value="service_spn_name" />  
         </identity>  
        </endpoint>  
      </service>  
    </services>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="KerberosBinding">  
          <security>  
            <message negotiateServiceCredential="false"   
                     establishSecurityContext="false" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>클라이언트  
 다음 코드와 구성은 독립적으로 실행되어야 합니다. 다음 작업 중 하나를 수행합니다.  
  
-   이 코드와 클라이언트 코드를 사용하여 독립 실행형 클라이언트를 만듭니다.  
  
-   엔드포인트 주소를 정의하지 않는 클라이언트를 만듭니다. 대신 구성 이름을 인수로 사용하는 클라이언트 생성자를 사용합니다. 예를 들면 다음과 같습니다.  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>코드  
 다음 코드에서는 클라이언트를 구성합니다. 보안 모드는 Message로 설정되고, 클라이언트 자격 증명 형식은 Windows로 설정됩니다. <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> 및 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 속성은 `false`로 설정됩니다.  
  
> [!NOTE]
>  Windows 자격 증명 형식을 협상 없이 사용하려면 서비스와 통신을 시작하기 전에 서비스의 계정 SPN을 사용하여 클라이언트를 구성해야 합니다. 클라이언트는 SPN을 사용하여 Kerberos 토큰을 가져온 다음 서비스와의 통신을 인증하고 보안합니다. 다음 예제에서는 서비스의 SPN을 사용하여 클라이언트를 구성하는 방법을 보여 줍니다. 사용 중인 경우는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 클라이언트를 생성 하려면 서비스의 SPN을 자동으로 전파 됩니다 클라이언트에 서비스의 메타 데이터 (WSDL)에서 서비스의 메타 데이터를 포함 하는 경우 해당 정보입니다. 서비스의 메타 데이터에 SPN을 포함 하도록 서비스를 구성 하는 방법에 대 한 자세한 내용은이 항목 뒷부분에서의 "서비스" 섹션을 참조 하세요.  
>   
>  Spn, Kerberos 및 Active Directory에 대 한 자세한 내용은 참조 하세요. [Kerberos 기술 보완에 대 한 Windows](https://go.microsoft.com/fwlink/?LinkId=88330)합니다. 끝점 id에 대 한 자세한 내용은 참조 하세요. [SecurityBindingElement 인증 모드](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md) 항목입니다.  
  
 [!code-csharp[C_SecurityScenarios#19](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#19)]
 [!code-vb[C_SecurityScenarios#19](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#19)]  
  
### <a name="configuration"></a>구성  
 다음 코드에서는 클라이언트를 구성합니다. 유의 합니다 [ \<servicePrincipalName >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceprincipalname.md) 요소 Active Directory 도메인 서비스의 계정에 대해 등록 된 서비스의 SPN에 맞게 설정 해야 합니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Message">  
            <message clientCredentialType="Windows"   
                     negotiateServiceCredential="false"  
                     establishSecurityContext="false" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="http://localhost/Calculator"   
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"  
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator">  
        <identity>  
          <servicePrincipalName value="service_spn_name" />  
        </identity>  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
 [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [서비스 ID 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)  
 [Windows Server appfabric 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
