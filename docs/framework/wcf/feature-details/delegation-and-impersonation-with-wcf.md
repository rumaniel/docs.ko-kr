---
title: WCF를 통한 위임 및 가장
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- impersonation [WCF]
- delegation [WCF]
ms.assetid: 110e60f7-5b03-4b69-b667-31721b8e3152
ms.openlocfilehash: 39b71d3b5cbcfdc8bde3449560587f033c437d50
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856159"
---
# <a name="delegation-and-impersonation-with-wcf"></a>WCF를 통한 위임 및 가장
*가장* 은 서비스에서 서비스 도메인 리소스에 대한 클라이언트 액세스를 제한하는 데 사용하는 일반적인 기술 서비스입니다. 서비스 도메인 리소스는 로컬 파일(가장)과 같은 시스템 리소스이거나 파일 공유(위임)와 같은 다른 시스템의 리소스일 수 있습니다. 샘플 응용 프로그램을 보려면 [클라이언트 가장](../../../../docs/framework/wcf/samples/impersonating-the-client.md)을 참조하세요. 가장을 사용 하는 방법에 대 한 예제 [를 보려면 방법: 서비스](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)에서 클라이언트를 가장 합니다.  
  
> [!IMPORTANT]
> 서비스를 통해 클라이언트를 가장하는 경우 서버 프로세스보다 높은 권한의 클라이언트 자격 증명을 사용하여 서비스가 실행됩니다.  
  
## <a name="overview"></a>개요  
 일반적으로 클라이언트는 서비스에서 클라이언트 대신 일부 작업을 수행하도록 서비스를 호출합니다. 가장을 사용하면 서비스는 작업을 수행하는 동안 클라이언트 역할을 할 수 있습니다. 위임을 사용하면 백 엔드 서비스가 클라이언트를 가장할 수 있는 방식으로 프론트 엔드 서비스가 클라이언트의 요청을 백 엔드 서비스에 전달할 수 있습니다. 가장은 클라이언트에 특정 작업을 수행할 수 있는 권한을 부여할지 여부를 확인하는 데 사용되는 가장 일반적인 방법인 반면 위임은 클라이언트 ID와 함께 가장 기능을 백 엔드 서비스에 전달하는 방법입니다. 위임은 Kerberos 기반 인증을 수행할 때 사용할 수 있는 Windows 도메인 기능입니다. 위임은 ID 전달과 구분되며, 클라이언트의 암호 없이 클라이언트를 가장하는 기능을 전송하기 때문에 ID 전달보다 훨씬 권한이 높습니다.  
  
 가장과 위임 모두 클라이언트에 Windows ID가 있어야 합니다. 클라이언트에 Windows ID가 없는 경우 사용할 수 있는 유일한 옵션은 클라이언트 ID를 두 번째 서비스에 전달하는 것입니다.  
  
## <a name="impersonation-basics"></a>가장 기본 사항  
 WCF (Windows Communication Foundation)는 다양 한 클라이언트 자격 증명에 대 한 가장을 지원 합니다. 이 항목에서는 서비스 메서드를 구현하는 동안 호출자를 가장하기 위한 서비스 모델 지원에 대해 설명합니다. 이러한 시나리오에서 가장 및 SOAP 보안과 WCF 옵션을 포함 하는 일반적인 배포 시나리오에 대해서도 설명 합니다.  
  
 이 항목에서는 SOAP 보안을 사용 하는 경우 WCF의 가장 및 위임에 대해 중점적으로 설명 합니다. 전송 보안을 사용 하 여 가장을 사용 [하는 방법](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md)에 설명 된 대로 전송 보안을 사용 하는 경우 WCF에서 가장 및 위임을 사용할 수도 있습니다.  
  
## <a name="two-methods"></a>두 가지 방법  
 WCF SOAP 보안에는 가장을 수행 하는 두 가지 방법이 있습니다. 사용되는 방법은 바인딩에 따라 결정됩니다. 첫 번째 방법은 SSPI(보안 지원 공급자 인터페이스) 또는 Kerberos 인증에서 가져온 후 서비스에 캐시되는 Windows 토큰을 통한 가장이며, 두 번째 방법은 통칭 *S4U* (Service-for-User)라고 알려진 Kerberos 확장에서 가져온 Windows 토큰을 통한 가장입니다.  
  
### <a name="cached-token-impersonation"></a>캐시된 토큰 가장  
 다음과 같은 바인딩을 통해 캐시된 토큰 가장을 수행할 수 있습니다.  
  
- Windows 클라이언트 자격 증명이 있는<xref:System.ServiceModel.WSHttpBinding>, <xref:System.ServiceModel.WSDualHttpBinding>및 <xref:System.ServiceModel.NetTcpBinding>  
  
- <xref:System.ServiceModel.BasicHttpBinding> 가 <xref:System.ServiceModel.BasicHttpSecurityMode> 자격 증명으로 설정된 <xref:System.ServiceModel.BasicHttpSecurityMode.TransportWithMessageCredential> 또는 서비스를 통해 올바른 Windows 계정으로 매핑할 수 있는 사용자 이름 자격 증명을 클라이언트에서 제공하는 기타 표준 바인딩  
  
- <xref:System.ServiceModel.Channels.CustomBinding> 속성이 `requireCancellation`로 설정된 Windows 클라이언트 자격 증명을 사용하는 모든 `true`. 이 속성은 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters>, <xref:System.ServiceModel.Security.Tokens.SslSecurityTokenParameters> 및 <xref:System.ServiceModel.Security.Tokens.SspiSecurityTokenParameters> 클래스에서 사용할 수 있습니다. 바인딩에 보안 대화가 사용되는 경우에도 `requireCancellation` 속성이 `true`로 설정되어야 합니다.  
  
- 클라이언트에서 사용자 이름 자격 증명을 제공하는 <xref:System.ServiceModel.Channels.CustomBinding>. 바인딩에 보안 대화가 사용되는 경우에도 `requireCancellation` 속성이 `true`로 설정되어야 합니다.  
  
### <a name="s4u-based-impersonation"></a>S4U 기반 가장  
 다음과 같은 바인딩을 통해 S4U 기반 가장을 수행할 수 있습니다.  
  
- 서비스를 통해 올바른Windows 계정으로 매핑될 수 있는 인증서 클라이언트 자격 증명을 가진<xref:System.ServiceModel.WSHttpBinding>, <xref:System.ServiceModel.WSDualHttpBinding>및 <xref:System.ServiceModel.NetTcpBinding>  
  
- <xref:System.ServiceModel.Channels.CustomBinding> 속성이 `requireCancellation` 로 설정된 Windows 클라이언트 자격 증명을 사용하는 `false`  
  
- <xref:System.ServiceModel.Channels.CustomBinding> 속성이 `requireCancellation` 로 설정된 보안 대화 및 Windows 클라이언트 자격 증명 또는 사용자 이름을 사용하는 `false`  
  
 서비스를 통해 클라이언트를 가장할 수 있는 범위는 서비스를 통해 가장을 시도할 때의 서비스 계정 권한, 사용되는 가장 형식 및 클라이언트에서 허용하는 가장 범위에 따라 다릅니다.  
  
> [!NOTE]
> 클라이언트 및 서비스가 동일한 컴퓨터에서 실행 중이고 클라이언트가 시스템 계정(예: `Local System` 또는 `Network Service`)으로 실행 중인 경우, 상태 저장 보안 컨텍스트 토큰을 사용하여 보안 세션을 설정할 때 클라이언트를 가장할 수 없습니다. 일반적으로 Windows Form 또는 콘솔 애플리케이션은 현재 계정에 로그인된 상태에서 실행되기 때문에 기본적으로 계정을 가장할 수 있습니다. 그러나 클라이언트가 ASP.NET 페이지이 고 해당 페이지가 iis 6.0 또는 iis 7.0에서 호스트 되는 경우 클라이언트는 기본적으로 `Network Service` 계정으로 실행 됩니다. 보안 세션을 지원하는 모든 시스템 제공 바인딩은 기본적으로 상태 비저장 SCT(보안 컨텍스트 토큰)를 사용합니다. 그러나 클라이언트가 ASP.NET 페이지이 고 상태 저장 Sct을 사용 하는 보안 세션을 사용 하는 경우 클라이언트를 가장할 수 없습니다. 보안 세션에서 상태 저장 sct를 [사용 하는 방법에 대 한 자세한 내용은 방법: 보안 세션](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)에 대 한 보안 컨텍스트 토큰을 만듭니다.  
  
## <a name="impersonation-in-a-service-method-declarative-model"></a>서비스 메서드의 가장: 선언적 모델  
 대부분의 가장 시나리오의 경우 호출자 컨텍스트에서 서비스 메서드를 실행하게 됩니다. WCF는 사용자가 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성에 가장 요구 사항을 지정할 수 있도록 하 여이 작업을 쉽게 수행할 수 있게 해 주는 가장 기능을 제공 합니다. 예를 들어 다음 코드에서 WCF 인프라는 메서드를 `Hello` 실행 하기 전에 호출자를 가장 합니다. `Hello` 메서드 내의 네이티브 리소스에 대한 액세스 시도는 이 리소스의 ACL(액세스 제어 목록)에서 호출자 액세스 권한을 허용하는 경우에만 가능합니다. 가장을 가능하게 하려면, 다음 예제에서와 같이 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> 속성을 <xref:System.ServiceModel.ImpersonationOption> 열거형 값인 <xref:System.ServiceModel.ImpersonationOption.Required?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.ImpersonationOption.Allowed?displayProperty=nameWithType> 중 하나로 설정합니다.  
  
> [!NOTE]
> 서비스의 자격 증명 권한이 원격 클라이언트의 자격 증명보다 더 높을 때 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> 속성이 <xref:System.ServiceModel.ImpersonationOption.Allowed>로 설정되어 있으면 서비스의 자격 증명이 사용됩니다. 즉, 권한이 낮은 사용자가 자격 증명을 제공하면 권한이 더 높은 서비스에서 서비스의 자격 증명으로 메서드를 실행하여, 권한이 낮은 사용자가 일반적으로 사용할 수 없는 리소스를 사용할 수 있습니다.  
  
 [!code-csharp[c_ImpersonationAndDelegation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#1)]
 [!code-vb[c_ImpersonationAndDelegation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#1)]  
  
 WCF 인프라는 호출자가 Windows 사용자 계정에 매핑될 수 있는 자격 증명으로 인증 된 경우에만 호출자를 가장할 수 있습니다. Windows 계정에 매핑될 수 없는 자격 증명을 통해 인증하도록 서비스를 구성한 경우에는 서비스 메서드가 실행되지 않습니다.  
  
> [!NOTE]
> [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서는 상태 저장 SCT가 만들어지면 가장이 실패하여 <xref:System.InvalidOperationException>이 발생합니다. 자세한 내용은 [지원 되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)합니다.  
  
## <a name="impersonation-in-a-service-method-imperative-model"></a>서비스 메서드의 가장: 명령적 모델  
 작동하는 전체 서비스 메서드가 아닌 그 중 일부만 호출자가 가장해야 하는 경우가 있습니다. 이 경우에는 서비스 메서드 내의 호출자 Windows ID를 가져와 명령적 방식으로 가장을 수행합니다. 이 작업은 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 클래스의 인스턴스를 반환하도록 <xref:System.ServiceModel.ServiceSecurityContext> 의 <xref:System.Security.Principal.WindowsIdentity> 속성을 사용하고 해당 인스턴스를 사용하기 전에 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> 메서드를 호출하여 수행합니다.  
  
> [!NOTE]
> 가장 동작을 자동으로 되돌리려면`Using` Visual Basic 문 C# `using` 또는 문을 사용 해야 합니다. 문을 사용 하지 않거나 Visual Basic 또는 C#이외의 프로그래밍 언어를 사용 하는 경우 가장 수준을 되돌려야 합니다. 이 작업에 실패하면 서비스 거부 및 권한 상승 공격이 발생할 수 있습니다.  
  
 [!code-csharp[c_ImpersonationAndDelegation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#2)]
 [!code-vb[c_ImpersonationAndDelegation#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#2)]  
  
## <a name="impersonation-for-all-service-methods"></a>모든 서비스 메서드에 대한 가장  
 서비스의 모든 메서드를 호출자의 컨텍스트에서 수행해야 하는 경우가 있습니다. 이 경우 메서드별로 이 기능을 명시적으로 활성화하는 대신 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>를 사용합니다. 다음 코드에서처럼 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ImpersonateCallerForAllOperations%2A> 속성을 `true`로 설정합니다. <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 는 <xref:System.ServiceModel.ServiceHost> 클래스의 동작 컬렉션에서 검색됩니다. 또한 각 메서드에 적용되는 `Impersonation` 의 <xref:System.ServiceModel.OperationBehaviorAttribute> 속성도 <xref:System.ServiceModel.ImpersonationOption.Allowed> 또는 <xref:System.ServiceModel.ImpersonationOption.Required>중 하나로 설정되어야 합니다.  
  
 [!code-csharp[c_ImpersonationAndDelegation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#3)]
 [!code-vb[c_ImpersonationAndDelegation#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#3)]  
  
 다음 표에서는 및 `ImpersonationOption` `ImpersonateCallerForAllServiceOperations`의 모든 가능한 조합에 대 한 WCF 동작을 설명 합니다.  
  
|`ImpersonationOption`|`ImpersonateCallerForAllServiceOperations`|동작|  
|---------------------------|------------------------------------------------|--------------|  
|필수|N/A|WCF는 호출자를 가장 합니다.|  
|Allowed|False|WCF는 호출자를 가장 하지 않습니다.|  
|Allowed|true|WCF는 호출자를 가장 합니다.|  
|NotAllowed|False|WCF는 호출자를 가장 하지 않습니다.|  
|NotAllowed|true|허용되지 않습니다. <xref:System.InvalidOperationException> 이 throw됩니다.|  
  
## <a name="impersonation-level-obtained-from-windows-credentials-and-cached-token-impersonation"></a>Windows 자격 증명 및 캐시된 토큰 가장에서 가져온 가장 수준  
 일부 시나리오에서는 Windows 클라이언트 자격 증명이 사용될 때 서비스에서 수행하는 가장 수준을 클라이언트에서 부분적으로 제어합니다. 클라이언트가 익명 가장 수준을 지정하는 경우 또는 캐시된 토큰으로 가장을 수행하는 경우가 해당됩니다. 이 작업은 제네릭 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> 클래스의 속성으로 액세스되는 <xref:System.ServiceModel.Security.WindowsClientCredential> 클래스의 <xref:System.ServiceModel.ChannelFactory%601> 속성을 설정하여 수행합니다.  
  
> [!NOTE]
> 가장 수준을 익명으로 지정하면 클라이언트가 익명으로 서비스에 로그온됩니다. 따라서 서비스에서는 가장 수행 여부와 상관없이 익명 로그온을 허용해야 합니다.  
  
 클라이언트에서는 가장 수준을 <xref:System.Security.Principal.TokenImpersonationLevel.Anonymous>, <xref:System.Security.Principal.TokenImpersonationLevel.Identification>, <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation>또는 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>으로 지정할 수 있습니다. 다음 코드에서처럼 지정된 수준의 토큰만이 만들어집니다.  
  
 [!code-csharp[c_ImpersonationAndDelegation#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#4)]
 [!code-vb[c_ImpersonationAndDelegation#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#4)]  
  
 다음 표에는 캐시된 토큰을 통해 가장할 때 서비스를 통해 가져오는 가장 수준이 지정되어 있습니다.  
  
|`AllowedImpersonationLevel` 값|서비스의 `SeImpersonatePrivilege` 포함 여부|서비스와 클라이언트의 위임 가능 여부|캐시된 토큰 `ImpersonationLevel`|  
|---------------------------------------|------------------------------------------|--------------------------------------------------|---------------------------------------|  
|Anonymous|예|N/A|가장|  
|Anonymous|아니요|해당 없음|ID|  
|ID|N/A|N/A|ID|  
|가장|예|N/A|가장|  
|가장|아니요|해당 없음|ID|  
|위임|예|예|위임|  
|위임|예|아니요|가장|  
|위임|아니요|해당 없음|ID|  
  
## <a name="impersonation-level-obtained-from-user-name-credentials-and-cached-token-impersonation"></a>사용자 이름 자격 증명 및 캐시된 토큰 가장에서 가져온 가장 수준  
 클라이언트는 서비스의 사용자 이름 및 암호를 전달 하 여 WCF에서 해당 사용자로 로그온 할 수 있게 합니다. 즉, `AllowedImpersonationLevel` 속성을로 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>설정 하는 것과 같습니다. `AllowedImpersonationLevel`은 <xref:System.ServiceModel.Security.WindowsClientCredential> 및 <xref:System.ServiceModel.Security.HttpDigestClientCredential> 클래스에서 사용할 수 있습니다. 다음 표에는 서비스에서 사용자 이름 자격 증명을 받을 때 가져오는 가장 수준이 지정되어 있습니다.  
  
|`AllowedImpersonationLevel`|서비스의 `SeImpersonatePrivilege`포함 여부|서비스와 클라이언트의 위임 가능 여부|캐시된 토큰 `ImpersonationLevel`|  
|---------------------------------|------------------------------------------|--------------------------------------------------|---------------------------------------|  
|N/A|예|예|위임|  
|N/A|예|아니요|가장|  
|해당 없음|아니요|해당 없음|ID|  
  
## <a name="impersonation-level-obtained-from-s4u-based-impersonation"></a>S4U 기반 가장에서 가져온 가장 수준  
  
|서비스의 `SeTcbPrivilege`포함 여부|서비스의 `SeImpersonatePrivilege`포함 여부|서비스와 클라이언트의 위임 가능 여부|캐시된 토큰 `ImpersonationLevel`|  
|----------------------------------|------------------------------------------|--------------------------------------------------|---------------------------------------|  
|예|예|N/A|가장|  
|예|아니요|해당 없음|ID|  
|아니요|N/A|N/A|ID|  
  
## <a name="mapping-a-client-certificate-to-a-windows-account"></a>Windows 계정에 클라이언트 인증서 매핑  
 클라이언트가 인증서를 사용하여 자신을 서비스에 인증하고 서비스에서 Active Directory를 통해 클라이언트를 기존 계정에 매핑하도록 할 수 있습니다. 다음 XML에서는 인증서를 매핑하도록 서비스를 구성하는 방법을 보여 줍니다.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="MapToWindowsAccount">  
      <serviceCredentials>  
        <clientCertificate>  
          <authentication mapClientCertificateToWindowsAccount="true" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 다음 코드에서는 서비스를 구성하는 방법을 보여 줍니다.  
  
```csharp
// Create a binding that sets a certificate as the client credential type.  
WSHttpBinding b = new WSHttpBinding();  
b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a service host that maps the certificate to a Windows account.  
Uri httpUri = new Uri("http://localhost/Calculator");  
ServiceHost sh = new ServiceHost(typeof(HelloService), httpUri);  
sh.Credentials.ClientCertificate.Authentication.MapClientCertificateToWindowsAccount = true;  
```  
  
## <a name="delegation"></a>위임  
 백 엔드 서비스에 위임하려면 서비스에서는 클라이언트 Windows ID를 사용하여 백 엔드 서비스에 대해 Kerberos multi-leg(NTLM 대체(fallback) 없는 SSPI) 인증 또는 Kerberos 직접 인증을 수행해야 합니다. 백 엔드 서비스에 위임하기 위해 <xref:System.ServiceModel.ChannelFactory%601> 및 채널을 만든 다음 클라이언트를 가장하는 동안 채널을 통해 통신합니다. 이 형식의 위임을 사용하는 경우 프런트 엔드 서비스에서 백 엔드 서비스가 위치할 수 있는 범위는 프런트 엔드 서비스에서 수행한 가장 수준에 따라 달라집니다. 가장 수준이 <xref:System.Security.Principal.TokenImpersonationLevel.Impersonation>인 경우 프런트 엔드 및 백 엔드 서비스는 동일한 시스템에서 실행되어야 합니다. 가장 수준이 <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>인 경우 프런트 엔드 및 백 엔드 서비스는 개별 시스템 또는 동일한 시스템에 있을 수 있습니다. 위임 수준 가장을 사용하려면 위임을 허용하도록 Windows 도메인 정책을 구성해야 합니다. 위임 지원을 위한 Active Directory 구성에 대한 자세한 내용은 [Enabling Delegated Authentication](https://go.microsoft.com/fwlink/?LinkId=99690)을 참조하십시오.  
  
> [!NOTE]
> 클라이언트가 백 엔드 서비스의 Windows 계정에 해당하는 사용자 이름 및 암호를 사용하여 프런트 엔드 서비스를 인증하는 경우 프런트 엔드 서비스는 해당 클라이언트의 사용자 이름과 암호를 다시 사용하여 백 엔드 서비스를 인증할 수 있습니다. 사용자 이름과 암호를 백 엔드 서비스에 전달하면 백 엔드 서비스가 가장을 수행할 수 있으므로 이 방식은 매우 유용한 ID 전달 방식이지만 Kerberos를 사용하지 않기 때문에 위임을 구성하지 않습니다. 위임에 대한 Active Directory 제어는 사용자 이름 및 암호 인증에 적용되지 않습니다.  
  
### <a name="delegation-ability-as-a-function-of-impersonation-level"></a>가장 수준에 따른 위임 기능  
  
|가장 수준|서비스에서 프로세스 간 위임을 수행할 수 있음|서비스에서 시스템 간 위임을 수행할 수 있음|  
|-------------------------|---------------------------------------------------|---------------------------------------------------|  
|<xref:System.Security.Principal.TokenImpersonationLevel.Identification>|아니요|아니요|  
|<xref:System.Security.Principal.TokenImpersonationLevel.Impersonation>|예|아니요|  
|<xref:System.Security.Principal.TokenImpersonationLevel.Delegation>|예|예|  
  
 다음 코드 예제에서는 위임을 사용하는 방법을 보여 줍니다.  
  
 [!code-csharp[c_delegation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_delegation/cs/source.cs#1)]
 [!code-vb[c_delegation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_delegation/vb/source.vb#1)]  
  
### <a name="how-to-configure-an-application-to-use-constrained-delegation"></a>한정된 위임을 사용하도록 애플리케이션을 구성하는 방법  
 한정된 위임을 사용하기 전에 발신자, 수신자 및 도메인 컨트롤러는 한정된 위임을 사용하도록 구성되어야 합니다. 다음 절차에서는 한정된 위임을 사용하는 단계를 보여 줍니다. 위임과 한정된 위임의 차이에 대한 자세한 내용은 간략하게 설명된 [Windows Server 2003 Kerberos Extensions](https://go.microsoft.com/fwlink/?LinkId=100194) 부분을 참조하십시오.  
  
1. 도메인 컨트롤러에서 클라이언트 애플리케이션이 실행 중인 계정에 대해 **계정이 민감하여 위임할 수 없음** 확인란의 선택을 취소합니다.  
  
2. 도메인 컨트롤러에서 클라이언트 애플리케이션이 실행 중인 계정에 대해 **위임에 대해 계정을 신뢰할 수 있음** 확인란을 선택합니다.  
  
3. 도메인 컨트롤러에서 **위임용으로 이 컴퓨터 트러스트** 옵션을 클릭하여 위임을 위해 신뢰할 수 있도록 중간 계층의 컴퓨터를 구성합니다.  
  
4. 도메인 컨트롤러에서 **지정한 서비스에 대한 위임용으로만 이 컴퓨터 트러스트** 옵션을 클릭하여 한정된 위임을 사용하도록 중간 계층의 컴퓨터를 구성합니다.  
  
 한정된 위임 구성에 대한 자세한 내용은 MSDN의 다음 항목을 참조하십시오.  
  
- [Troubleshooting Kerberos Delegation](https://go.microsoft.com/fwlink/?LinkId=36724)  
  
- [Kerberos Protocol Transition and Constrained Delegation](https://go.microsoft.com/fwlink/?LinkId=36725)  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.OperationBehaviorAttribute>
- <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>
- <xref:System.ServiceModel.ImpersonationOption>
- <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A>
- <xref:System.ServiceModel.ServiceSecurityContext>
- <xref:System.Security.Principal.WindowsIdentity>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ImpersonateCallerForAllOperations%2A>
- <xref:System.ServiceModel.ServiceHost>
- <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A>
- <xref:System.ServiceModel.Security.WindowsClientCredential>
- <xref:System.ServiceModel.ChannelFactory%601>
- <xref:System.Security.Principal.TokenImpersonationLevel.Identification>
- [전송 보안을 통해 가장 사용](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md)
- [클라이언트 가장](../../../../docs/framework/wcf/samples/impersonating-the-client.md)
- [방법: 서비스에서 클라이언트 가장](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)
- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
