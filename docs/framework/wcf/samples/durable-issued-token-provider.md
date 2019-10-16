---
title: 영속 제공된 토큰 공급자
ms.date: 03/30/2017
ms.assetid: 76fb27f5-8787-4b6a-bf4c-99b4be1d2e8b
ms.openlocfilehash: f1bb95ba676b47d29d5b527b5b93eddcf48f4bde
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989949"
---
# <a name="durable-issued-token-provider"></a>영속 제공된 토큰 공급자
이 샘플에서는 사용자 지정 클라이언트가 발급한 토큰 공급자를 구현하는 방법을 보여 줍니다.  
  
## <a name="discussion"></a>토론  
 WCF (Windows Communication Foundation)의 토큰 공급자는 보안 인프라에 자격 증명을 제공 하는 데 사용 됩니다. 일반적으로 토큰 공급자는 대상을 검사하고 적절한 자격 증명을 발급하여 보안 인프라에서 메시지의 보안을 유지할 수 있도록 합니다. WCF는 CardSpace 토큰 공급자와 함께 제공 됩니다. 사용자 지정 토큰 공급자는 다음과 같은 경우에 유용합니다.  
  
- 기본 제공 토큰 공급자가 작동하지 않는 자격 증명 저장소가 있는 경우  
  
- WCF 클라이언트가 자격 증명을 사용 하는 경우 사용자가 세부 정보를 제공 하는 시점에서 자격 증명을 변환 하는 사용자 지정 메커니즘을 제공 하려는 경우  
  
- 사용자 지정 토큰을 빌드하고 있는 경우  
  
 이 샘플에서는 STS(보안 토큰 서비스)에서 발급한 토큰을 캐시하는 사용자 지정 토큰 공급자를 빌드하는 방법을 보여 줍니다.  
  
 즉, 이 샘플에서는 다음 방법을 보여 줍니다.  
  
- 사용자 지정 토큰 공급자로 클라이언트를 구성하는 방법  
  
- 발급 된 토큰을 캐시 하 여 WCF 클라이언트에 제공 하는 방법을 설명 합니다.  
  
- 서버의 X.509 인증서를 사용하여 클라이언트에서 서버를 인증하는 방법  
  
 이 샘플은 클라이언트 콘솔 프로그램(Client.exe), 보안 토큰 서비스 콘솔 프로그램(Securitytokenservice.exe) 및 서비스 콘솔 프로그램(Service.exe)으로 구성되어 있습니다. 이 서비스는 요청-회신 통신 패턴을 정의하는 계약을 구현합니다. 계약은 수학 연산(Add, Subtract, Multiply 및 Divide)을 노출시키는 `ICalculator` 인터페이스에 의해 정의됩니다. 클라이언트가 STS(보안 토큰 서비스)에서 보안 토큰을 가져오고 지정된 수학 연산을 서비스에 동기적으로 요청하면 서비스에서 결과를 회신합니다. 콘솔 창에는 클라이언트 동작이 표시됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플에서는 [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)를 사용 하 여 ICalculator 계약을 노출 합니다. 다음 코드에서는 클라이언트에서의 바인딩 구성을 보여 줍니다.  
  
```xml  
<bindings>
  <wsFederationHttpBinding>
    <binding name="ServiceFed">
      <security mode="Message">
        <message issuedKeyType="SymmetricKey" 
                 issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1">
          <issuer address="http://localhost:8000/sts/windows" 
                  binding="wsHttpBinding" />
        </message>
      </security>
    </binding>
  </wsFederationHttpBinding>
</bindings>  
```  
  
 `security`의 `wsFederationHttpBinding` 요소에서 `mode` 값은 사용해야 하는 보안 모드를 구성합니다. 이 샘플에서는 메시지 보안이 사용되므로 `message`의 `wsFederationHttpBinding` 요소 안에 `security`의 `wsFederationHttpBinding` 요소가 지정됩니다. `issuer`의 `wsFederationHttpBinding` 안에서`message`의 `wsFederationHttpBinding` 요소는 클라이언트가 계산기 서비스에 대해 인증될 수 있도록 보안 토큰을 클라이언트에게 발급하는 보안 토큰 서비스의 주소와 바인딩을 지정합니다.  
  
 서비스에서 이 바인딩의 구성은 다음 코드와 같습니다.  
  
```xml  
<bindings>
  <wsFederationHttpBinding>
    <binding name="ServiceFed">
      <security mode="Message">
        <message issuedKeyType="SymmetricKey" 
                 issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1">
          <issuerMetadata address="http://localhost:8000/sts/mex">
            <identity>
              <certificateReference storeLocation="CurrentUser" 
                                    storeName="TrustedPeople" 
                                    x509FindType="FindBySubjectDistinguishedName" 
                                    findValue="CN=STS" />
            </identity>
          </issuerMetadata>
        </message>
      </security>
    </binding>
  </wsFederationHttpBinding>
</bindings>  
```  
  
 `security`의 `wsFederationHttpBinding` 요소에서 `mode` 값은 사용해야 하는 보안 모드를 구성합니다. 이 샘플에서는 메시지 보안이 사용되므로 `message`의 `wsFederationHttpBinding` 요소 안에 `security`의 `wsFederationHttpBinding` 요소가 지정됩니다. `issuerMetadata`의 `wsFederationHttpBinding` 요소 안에서 `message`의 `wsFederationHttpBinding` 요소는 보안 토큰 서비스에 대한 메타데이터를 검색하는 데 사용할 수 있는 엔드포인트의 주소와 ID를 지정합니다.  
  
 다음 코드에서는 서비스의 동작을 보여 줍니다.  
  
```xml  
<behavior name="ServiceBehavior">
  <serviceDebug includeExceptionDetailInFaults="true" />
  <serviceMetadata httpGetEnabled="true" />
  <serviceCredentials>
    <issuedTokenAuthentication>
      <knownCertificates>
        <add storeLocation="LocalMachine" 
              storeName="TrustedPeople" 
              x509FindType="FindBySubjectDistinguishedName" 
              findValue="CN=STS" />
      </knownCertificates>
    </issuedTokenAuthentication>
    <serviceCertificate storeLocation="LocalMachine" 
                        storeName="My" 
                        x509FindType="FindBySubjectDistinguishedName" 
                        findValue="CN=localhost" />
  </serviceCredentials>
</behavior>  
```  
  
 `issuedTokenAuthentication` 요소 내부의 `serviceCredentials` 요소를 사용하면 서비스에서는 인증 과정 중 클라이언트가 제시할 수 있는 토큰에 대한 제약 조건을 지정할 수 있습니다. 이 구성은 주체 이름이 CN=STS인 인증서에 의해 서명된 토큰을 서비스에서 수락하도록 지정합니다.  
  
 보안 토큰 서비스는 표준 wsHttpBinding을 사용하여 단일 엔드포인트를 노출합니다. 보안 토큰 서비스는 클라이언트의 토큰 요청에 응답하며, 클라이언트가 Windows 계정을 사용하여 인증하는 경우 클라이언트의 사용자 이름을 발급된 토큰의 클레임으로 포함하는 토큰을 발급합니다. 토큰을 만드는 동안 보안 토큰 서비스는 CN=STS 인증서에 연결된 프라이빗 키를 사용하여 토큰에 서명합니다. 또한 대칭 키를 만들고 CN=localhost 인증서와 연관된 공개 키를 사용하여 이를 암호화합니다. 보안 토큰 서비스는 토큰을 클라이언트에 반환하면서 대칭 키도 반환합니다. 클라이언트는 발급된 토큰을 계산기 서비스에 제공하고 대칭 키로 메시지에 서명하여 해당 키를 알고 있음을 증명합니다.  
  
## <a name="custom-client-credentials-and-token-provider"></a>사용자 지정 클라이언트 자격 증명 및 토큰 공급자  
 다음 단계에서는 발급 된 토큰을 캐시 하 고 WCF: security와 통합 하는 사용자 지정 토큰 공급자를 개발 하는 방법을 보여 줍니다.  
  
### <a name="to-develop-a-custom-token-provider"></a>사용자 지정 토큰 공급자를 개발하려면  
  
1. 사용자 지정 토큰 공급자를 작성합니다.  
  
     샘플에서는 캐시에서 검색한 보안 토큰을 반환하는 사용자 지정 토큰 공급자를 구현합니다.  
  
     이 작업을 수행하려면 사용자 지정 토큰 공급자가 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 클래스를 파생하고 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A> 메서드를 재정의해야 합니다. 이 메서드는 캐시로부터 토큰을 가져오려고 시도하거나 캐시에 토큰이 없는 경우에는 기본 공급자에서 토큰을 검색하여 검색한 토큰을 캐시합니다. 두 경우 모두 메서드는 `SecurityToken`을 반환합니다.  
  
    ```csharp  
    protected override SecurityToken GetTokenCore(TimeSpan timeout)  
    {  
      GenericXmlSecurityToken token;  
      if (!this.cache.TryGetToken(target, issuer, out token))  
      {  
        token = (GenericXmlSecurityToken) this.innerTokenProvider.GetToken(timeout);  
        this.cache.AddToken(token, target, issuer);  
      }  
      return token;  
    }  
    ```  
  
2. 사용자 지정 보안 토큰 관리자를 씁니다.  
  
     <xref:System.IdentityModel.Selectors.SecurityTokenManager>는 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 메서드에서 전달되는 특정 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>에 대한 `CreateSecurityTokenProvider`를 만드는 데 사용됩니다. 또한 보안 토큰 관리자는 토큰 인증자와 토큰 serializer를 만드는 데 사용되지만 이 샘플에서는 설명하지 않습니다. 이 샘플에서 사용자 지정 보안 토큰 관리자는 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 클래스를 상속하며, 전달된 토큰 요구 사항에서 발급된 토큰이 필요함을 나타낼 때 사용자 지정 토큰 공급자를 반환하도록 `CreateSecurityTokenProvider` 메서드를 재정의합니다.  
  
    ```csharp  
    class DurableIssuedTokenClientCredentialsTokenManager :  
     ClientCredentialsSecurityTokenManager  
    {  
      IssuedTokenCache cache;  
  
      public DurableIssuedTokenClientCredentialsTokenManager ( DurableIssuedTokenClientCredentials creds ): base(creds)  
      {  
        this.cache = creds.IssuedTokenCache;  
      }  
  
      public override SecurityTokenProvider CreateSecurityTokenProvider ( SecurityTokenRequirement tokenRequirement )  
      {  
        if (IsIssuedSecurityTokenRequirement(tokenRequirement))  
        {  
          return new DurableIssuedSecurityTokenProvider ((IssuedSecurityTokenProvider)base.CreateSecurityTokenProvider( tokenRequirement), this.cache);  
        }  
        else  
        {  
          return base.CreateSecurityTokenProvider(tokenRequirement);  
        }  
      }  
    }  
    ```  
  
3. 사용자 지정 클라이언트 자격 증명을 씁니다.  
  
     클라이언트 자격 증명 클래스는 클라이언트 프록시에 대해 구성된 자격 증명을 나타내는 데 사용되며 토큰 인증자, 토큰 공급자 및 토큰 serializer를 가져오는 데 사용되는 보안 토큰 관리자를 만듭니다.  
  
    ```csharp  
    public class DurableIssuedTokenClientCredentials : ClientCredentials  
    {  
      IssuedTokenCache cache;  
  
      public DurableIssuedTokenClientCredentials() : base()  
      {  
      }  
  
      DurableIssuedTokenClientCredentials ( DurableIssuedTokenClientCredentials other) : base(other)  
      {  
        this.cache = other.cache;  
      }  
  
      public IssuedTokenCache IssuedTokenCache  
      {  
        get  
        {  
          return this.cache;  
        }  
        set  
        {  
          this.cache = value;  
        }  
      }  
  
      protected override ClientCredentials CloneCore()  
      {  
        return new DurableIssuedTokenClientCredentials(this);  
      }  
  
      public override SecurityTokenManager CreateSecurityTokenManager()  
      {  
        return new DurableIssuedTokenClientCredentialsTokenManager ((DurableIssuedTokenClientCredentials)this.Clone());  
      }  
    }  
    ```  
  
4. 토큰 캐시를 구현합니다. 이 샘플 구현에서는 특정 토큰 캐시의 소비자가 캐시와 상호 작용할 때 이용하는 추상 기본 클래스를 사용합니다.  
  
    ```csharp  
    public abstract class IssuedTokenCache  
    {  
      public abstract void AddToken ( GenericXmlSecurityToken token, EndpointAddress target, EndpointAddress issuer);  
      public abstract bool TryGetToken(EndpointAddress target, EndpointAddress issuer, out GenericXmlSecurityToken cachedToken);  
    }  
    // Configure the client to use the custom client credential.  
    ```  
  
     클라이언트가 사용자 지정 클라이언트 자격 증명을 사용할 수 있도록 이 샘플에서는 기본 클라이언트 자격 증명 클래스를 삭제하고 새 클라이언트 자격 증명 클래스를 제공합니다.  
  
    ```csharp  
    clientFactory.Endpoint.Behaviors.Remove<ClientCredentials>();  
    DurableIssuedTokenClientCredentials durableCreds = new DurableIssuedTokenClientCredentials();  
    durableCreds.IssuedTokenCache = cache;  
    durableCreds.ServiceCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.PeerOrChainTrust;  
    clientFactory.Endpoint.Behaviors.Add(durableCreds);  
    ```  
  
## <a name="running-the-sample"></a>샘플 실행  
 샘플 실행을 위한 지침이 아래에 설명되어 있습니다. 샘플을 실행하면 보안 토큰에 대한 요청이 보안 토큰 서비스 콘솔 창에 표시되고, 작업 요청 및 응답이 클라이언트 및 서비스 콘솔 창에 표시됩니다. 애플리케이션을 종료하려면 아무 콘솔 창에서나 Enter 키를 누릅니다.  
  
## <a name="the-setupcmd-batch-file"></a>Setup.cmd 배치 파일  
 이 샘플에 포함된 Setup.cmd 배치 파일을 사용하면 서버와 보안 토큰 서비스를 관련 인증서와 함께 구성하여 자체 호스팅된 애플리케이션을 실행할 수 있습니다. 배치 파일은 CurrentUser/TrustedPeople 인증서 저장소 둘 다에서 두 개의 인증서를 만듭니다. 주체 이름이 CN=STS인 첫 번째 인증서는 보안 토큰 서비스가 클라이언트에 발급되는 보안 토큰에 서명하기 위해 사용합니다. 주체 이름이 CN=localhost인 두 번째 인증서는 보안 토큰 서비스가 서비스에서 해독할 수 있는 암호를 암호화하기 위해 사용합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. Setup.cmd 파일을 실행하여 필요한 인증서를 만듭니다.  
  
2. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요. 솔루션의 모든 프로젝트가 빌드되는지 확인합니다(Shared, RSTRSTR, Service, SecurityTokenService 및 Client).  
  
3. Service.exe 및 SecurityTokenService.exe가 모두 관리자 권한으로 실행되는지 확인합니다.  
  
4. Client.exe를 실행합니다.  
  
### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
1. 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.cmd를 실행합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Security\DurableIssuedTokenProvider`  
