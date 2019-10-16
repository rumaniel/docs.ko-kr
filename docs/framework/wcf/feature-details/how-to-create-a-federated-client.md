---
title: '방법: 페더레이션 클라이언트 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
ms.assetid: 56ece47e-98bf-4346-b92b-fda1fc3b4d9c
ms.openlocfilehash: 988fc79f71b670f5eaed1a305f54cc90374e4b17
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950624"
---
# <a name="how-to-create-a-federated-client"></a>방법: 페더레이션 클라이언트 만들기
WCF (Windows Communication Foundation)에서 *페더레이션된 서비스* 에 대 한 클라이언트 만들기는 세 가지 주요 단계로 구성 됩니다.  
  
1. [\<WsFederationHttpBinding](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) > 또는 유사한 사용자 지정 바인딩을 구성 합니다. 적절 한 바인딩을 [만드는 방법에 대 한 자세한 내용은 방법: WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)를 만듭니다. 또는 페더레이션된 서비스의 메타 데이터 끝점에 대해 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 실행 하 여 페더레이션된 서비스 및 하나 이상의 보안 토큰 서비스와 통신 하기 위한 구성 파일을 생성 합니다.  
  
2. 보안 토큰 서비스와 클라이언트의 상호 작용에 대한 다양한 측면을 제어하는 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>의 속성을 설정합니다.  
  
3. <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>의 속성을 설정합니다. 이 설정은 보안 토큰 서비스의 경우처럼 제공된 엔드포인트와 안전하게 통신하는 데 필요한 인증서를 허용합니다.  
  
> [!NOTE]
> 클라이언트가 가장된 자격 증명, <xref:System.Security.Cryptography.CryptographicException> 바인딩 또는 사용자 지정 발급 토큰 및 비대칭 키를 사용할 때 <xref:System.ServiceModel.WSFederationHttpBinding>이 throw될 수 있습니다. 비대칭 키는 <xref:System.ServiceModel.WSFederationHttpBinding> 및 <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.IssuedKeyType%2A> 속성이 각각 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.KeyType%2A>로 설정된 경우 <xref:System.IdentityModel.Tokens.SecurityKeyType.AsymmetricKey> 바인딩 및 사용자 지정 발급 토큰과 함께 사용됩니다. 클라이언트가 메시지를 보내려고 할 때 및 클라이언트가 가장하고 있는 ID에 대해 사용자 프로필이 없을 때 <xref:System.Security.Cryptography.CryptographicException>이 throw됩니다. 이 문제를 완화하려면 메시지를 보내기 전에 클라이언트 컴퓨터에 로그온하거나 `LoadUserProfile`을 호출합니다.  
  
 이 항목에서는 이러한 절차에 대해 자세히 설명합니다. 적절 한 바인딩을 [만드는 방법에 대 한 자세한 내용은 방법: WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)를 만듭니다. 페더레이션된 서비스의 작동 방식에 대 한 자세한 내용은 [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md)을 참조 하세요.  
  
### <a name="to-generate-and-examine-the-configuration-for-a-federated-service"></a>페더레이션 서비스에 대한 구성을 생성하고 검사하려면  
  
1. 서비스의 메타 데이터 URL 주소를 명령줄 매개 변수로 사용 하 여 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 실행 합니다.  
  
2. 생성된 구성 파일을 적절한 편집기에서 엽니다.  
  
3. [ 생성\<된 발급자 >](../../../../docs/framework/configure-apps/file-schema/wcf/issuer.md) 및 [ \<issuerMetadata >](../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata.md) 요소에 대 한 특성 및 내용을 검토 합니다. 이러한 요소 [는 \<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) 또는 사용자 지정 바인딩 요소에 대 한 [ \<보안 >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsfederationhttpbinding.md) 요소 내에 있습니다. 주소에 예상 도메인 이름 또는 다른 주소 정보가 포함되어 있는지 확인합니다. 클라이언트가 이러한 주소를 인증하고 사용자 이름/암호 쌍과 같은 정보를 노출할 수 있으므로 이 정보를 확인해야 합니다. 해당 주소가 예상 주소가 아닐 경우 의도하지 않은 받는 사람에게 정보가 노출될 수 있습니다.  
  
4. 주석 처리 된 <`alternativeIssuedTokenParameters`> 요소 내의 추가 [ \<issuedTokenParameters >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md) 요소를 검사 합니다. Svcutil.exe 도구를 사용하여 페더레이션 서비스에 대한 구성을 생성할 때, 페더레이션 서비스 또는 중간 보안 토큰 서비스에서 발급자 주소를 지정하지 않고 여러 엔드포인트를 노출하는 보안 토큰 서비스에 대한 메타데이터 주소를 지정하는 경우 결과 구성 파일이 첫 번째 엔드포인트를 참조합니다. 추가 끝점은 구성 파일에서 주석 처리 된 <`alternativeIssuedTokenParameters`> 요소로 추가 됩니다.  
  
     이러한 <`issuedTokenParameters`중 하나가 이미 구성에 있는 것 보다 > 하는지 여부를 확인 합니다. 예를 들어 클라이언트는 사용자 이름/암호 쌍이 아닌 Windows CardSpace 토큰을 사용 하 여 보안 토큰 서비스를 인증 하는 것을 선호 합니다.  
  
    > [!NOTE]
    > 서비스와 통신하기 전에 여러 보안 토큰 서비스를 이동해야 하는 경우 중간 보안 토큰 서비스가 클라이언트에 잘못된 보안 토큰 서비스를 지시할 수 있습니다. 따라서 [ \<issuedTokenParameters >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md) 의 보안 토큰 서비스에 대 한 끝점이 예상 보안 토큰 서비스이 고 알 수 없는 보안 토큰 서비스가 아닌지 확인 합니다.  
  
### <a name="to-configure-an-issuedtokenclientcredential-in-code"></a>코드에서 IssuedTokenClientCredential을 구성하려면  
  
1. 다음 예제 코드에서처럼 <xref:System.ServiceModel.Security.IssuedTokenClientCredential> 클래스(<xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A> 클래스의 <xref:System.ServiceModel.Description.ClientCredentials> 속성 또는 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 클래스를 통해 반환된 클래스)의 <xref:System.ServiceModel.ClientBase%601> 속성을 통해 <xref:System.ServiceModel.ChannelFactory>에 액세스합니다.  
  
     [!code-csharp[c_CreateSTS#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#9)]
     [!code-vb[c_CreateSTS#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#9)]  
  
2. 토큰 캐싱이 필요하지 않은 경우 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.CacheIssuedTokens%2A> 속성을 `false`로 설정합니다. <xref:System.ServiceModel.Security.IssuedTokenClientCredential.CacheIssuedTokens%2A> 속성은 보안 토큰 서비스의 이러한 토큰이 캐싱되었는지 여부를 제어합니다. 이 속성이 `false`로 설정된 경우 클라이언트는 이전 토큰이 유효한지 여부에 관계없이 페더레이션 서비스에 자신을 다시 인증해야 할 때마다 보안 토큰 서비스로부터 새 토큰을 요청합니다. 이 속성이 `true`로 설정된 경우 클라이언트는 토큰이 만료되지 않는 한 페더레이션 서비스에 자신을 다시 인증해야 할 때마다 기존 토큰을 다시 사용합니다. 기본값은 `true`입니다.  
  
3. 캐싱된 토큰에서 시간 제한이 필요한 경우 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.MaxIssuedTokenCachingTime%2A> 속성을 <xref:System.TimeSpan> 값으로 설정합니다. 이 속성은 토큰을 캐싱할 수 있는 기간을 지정합니다. 지정한 시간 범위가 경과되면 토큰이 클라이언트 캐시로부터 제거됩니다. 기본적으로 토큰은 무기한 캐싱됩니다. 다음 예제에서는 이 시간 범위를 10분으로 설정합니다.  
  
     [!code-csharp[c_CreateSTS#15](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#15)]
     [!code-vb[c_CreateSTS#15](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#15)]  
  
4. 선택 사항입니다. <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuedTokenRenewalThresholdPercentage%2A>를 백분율로 설정합니다. 기본값은 60(%)입니다. 이 속성은 토큰 유효 기간의 백분율을 지정합니다. 예를 들어 발급한 토큰이 10시간 동안 유효하고 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuedTokenRenewalThresholdPercentage%2A>가 80으로 설정된 경우 8시간 후에 토큰이 갱신됩니다. 다음 예제에서는 이 값을 80%로 설정합니다.  
  
     [!code-csharp[c_CreateSTS#16](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#16)]
     [!code-vb[c_CreateSTS#16](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#16)]  
  
     토큰 유효 기간 및 `IssuedTokenRenewalThresholdPercentage` 값에 따라 결정되는 갱신 간격은 캐싱 시간이 갱신 임계값 시간보다 짧은 경우에 `MaxIssuedTokenCachingTime` 값으로 재정의됩니다. 예를 들어 `IssuedTokenRenewalThresholdPercentage`와 토큰의 기간을 곱한 값이 8시간이고, `MaxIssuedTokenCachingTime` 값이 10분이면 클라이언트가 업데이트된 토큰에 대한 보안 토큰 서비스에 10분마다 연결합니다.  
  
5. 메시지 자격 증명에 메시지 보안 또는 전송 보안을 사용하지 않는 바인딩에서 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode.CombinedEntropy> 이외의 키 엔트로피 모드가 필요한 경우 (예: 바인딩에 <xref:System.ServiceModel.Channels.SecurityBindingElement>가 없는 경우) <xref:System.ServiceModel.Security.IssuedTokenClientCredential.DefaultKeyEntropyMode%2A> 속성을 적절한 값으로 설정합니다. *엔트로피* 모드는 속성을 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.DefaultKeyEntropyMode%2A> 사용 하 여 대칭 키를 제어할 수 있는지 여부를 결정 합니다. 이 기본값은 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode.CombinedEntropy>입니다. 이 경우, 클라이언트와 토큰 발급자 모두 결합된 데이터를 제공하여 실제 키를 생성합니다. 다른 값은 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode.ClientEntropy>와 <xref:System.ServiceModel.Security.SecurityKeyEntropyMode.ServerEntropy>입니다. 즉, 전체 키가 클라이언트나 서버에 의해 각각 지정됩니다. 다음 예제에서는 키에 대해 서버 데이터만 사용하도록 속성을 설정합니다.  
  
     [!code-csharp[c_CreateSTS#17](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#17)]
     [!code-vb[c_CreateSTS#17](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#17)]  
  
    > [!NOTE]
    > <xref:System.ServiceModel.Channels.SecurityBindingElement>가 보안 토큰 서비스 또는 서비스 바인딩에 있는 경우 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.DefaultKeyEntropyMode%2A>에 설정된 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>가 <xref:System.ServiceModel.Channels.SecurityBindingElement.KeyEntropyMode%2A>의 `SecurityBindingElement` 속성으로 재정의됩니다.  
  
6. 발급자 특정 엔드포인트 동작을 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuerChannelBehaviors%2A> 속성에서 반환된 컬렉션에 추가하여 해당 동작을 구성합니다.  
  
     [!code-csharp[c_CreateSTS#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#14)]
     [!code-vb[c_CreateSTS#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#14)]  
  
### <a name="to-configure-the-issuedtokenclientcredential-in-configuration"></a>구성에서 IssuedTokenClientCredential을 구성하려면  
  
1. 요소를 끝점 동작에서 [\<issuedToken >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md) 요소의 자식으로 만듭니다. [\<IssuedToken](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)  
  
2. 토큰 캐싱이 필요 하지 않은 경우 < `cacheIssuedTokens` `issuedToken`> 요소의 특성을로 `false`설정 합니다.  
  
3. 캐시 된 토큰에 시간 제한이 필요한 경우 < `maxIssuedTokenCachingTime` `issuedToken`> 요소의 특성을 적절 한 값으로 설정 합니다. 예:  
    `<issuedToken maxIssuedTokenCachingTime='00:10:00' />`  
  
4. 기본값 이외의 값을 선호 하는 경우 < `issuedTokenRenewalThresholdPercentage` `issuedToken`> 요소의 특성을 적절 한 값으로 설정 합니다. 예를 들면 다음과 같습니다.  
  
    ```xml  
    <issuedToken issuedTokenRenewalThresholdPercentage = "80" />  
    ```  
  
5. 메시지 자격 증명에 메시지 보안 또는 전송 보안을 사용하지 않는 바인딩에 `CombinedEntropy` 이외의 키 엔트로피 모드가 있는 경우(예: 바인딩에 `SecurityBindingElement`가 없는 경우) `defaultKeyEntropyMode` 요소의 `<issuedToken>` 특성을 필요에 따라 `ServerEntropy` 또는 `ClientEntropy`로 설정합니다.  
  
    ```xml  
    <issuedToken defaultKeyEntropyMode = "ServerEntropy" />  
    ```  
  
6. 선택 사항입니다. `issuerChannelBehaviors`<`issuedToken`> 요소의 자식으로 < > 요소를 만들어 발급자 별 사용자 지정 끝점 동작을 구성 합니다. 각 동작에 대해 <`add``issuerChannelBehaviors`> 요소의 자식으로 < > 요소를 만듭니다. `issuerAddress` <`add`> 요소에 특성을 설정 하 여 동작의 발급자 주소를 지정 합니다. `behaviorConfiguration` <`add`> 요소에 특성을 설정 하 여 동작 자체를 지정 합니다.  
  
    ```xml  
    <issuerChannelBehaviors>  
    <add issuerAddress="http://fabrikam.org/sts" behaviorConfiguration="FabrikamSTS" />  
    </issuerChannelBehaviors>  
    ```  
  
### <a name="to-configure-an-x509certificaterecipientclientcredential-in-code"></a>코드에 X509CertificateRecipientClientCredential을 구성하려면  
  
1. <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential> 속성 또는 <xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A> 클래스 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> 속성의 <xref:System.ServiceModel.ClientBase%601> 속성을 통해 <xref:System.ServiceModel.ChannelFactory>에 액세스합니다.  
  
     [!code-csharp[c_CreateSTS#18](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#18)]
     [!code-vb[c_CreateSTS#18](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#18)]  
  
2. <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 인스턴스를 제공된 엔드포인트의 인증서에 사용할 수 있는 경우 <xref:System.Collections.Generic.ICollection%601.Add%2A> 속성에서 반환된 컬렉션의 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A> 메서드를 사용합니다.  
  
     [!code-csharp[c_CreateSTS#19](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#19)]
     [!code-vb[c_CreateSTS#19](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#19)]  
  
3. <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 인스턴스를 사용할 수 없는 경우 다음 예제에서처럼 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.SetScopedCertificate%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential> 메서드를 사용합니다.  
  
     [!code-csharp[c_CreateSTS#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#20)]
     [!code-vb[c_CreateSTS#20](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#20)]  
  
### <a name="to-configure-an-x509certificaterecipientclientcredential-in-configuration"></a>구성에서 X509CertificateRecipientClientCredential을 구성하려면  
  
1. [ \<ScopedCertificates >](../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md) 요소를 끝점 동작에서 [ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) 요소의 자식인 [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) 요소의 자식으로 만듭니다.  
  
2. `<add>` 요소를 `<scopedCertificates>` 요소의 자식으로 만듭니다. 적합한 인증서를 참조하도록 `storeLocation`, `storeName`, `x509FindType` 및 `findValue` 특성에 대한 값을 지정합니다. 다음 예제에서처럼 인증서를 사용할 엔드포인트의 주소를 제공하는 값으로 `targetUri` 특성을 설정합니다.  
  
    ```xml  
    <scopedCertificates>  
     <add targetUri="http://fabrikam.com/sts"   
          storeLocation="CurrentUser"  
          storeName="TrustedPeople"  
          x509FindType="FindBySubjectName"  
          findValue="FabrikamSTS" />  
    </scopedCertificates>  
    ```  
  
## <a name="example"></a>예제  
 다음 코드 샘플에서는 코드에 <xref:System.ServiceModel.Security.IssuedTokenClientCredential> 클래스의 인스턴스를 구성합니다.  
  
 [!code-csharp[c_FederatedClient#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_federatedclient/cs/source.cs#2)]
 [!code-vb[c_FederatedClient#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_federatedclient/vb/source.vb#2)]  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 가능한 정보 노출을 방지하려면 Svcutil.exe 도구를 실행하여 페더레이션 엔드포인트에서 메타데이터를 처리하는 클라이언트는 결과 보안 토큰 서비스 주소가 예상한 주소인지 확인해야 합니다. 이러한 확인은 보안 토큰 서비스가 여러 엔드포인트를 노출할 때 특히 중요합니다. 왜냐하면 Svcutil.exe 도구에서는 결과 구성 파일을 생성하여 이와 같은 첫 번째 엔드포인트를 사용하지만 이 엔드포인트가 클라이언트가 사용해야 하는 것이 아닐 수도 있기 때문입니다.  
  
## <a name="localissuer-required"></a>필수 LocalIssuer  
 클라이언트가 항상 로컬 발급자를 사용해야 하는 경우, 체인의 두 번째에서 마지막까지의 보안 토큰 서비스가 발급자 주소나 발급자 메타데이터 주소를 지정하면 Svcutil.exe의 기본 출력으로 인해 로컬 발급자가 사용되지 않는다는 사실을 알아야 합니다.  
  
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerAddress%2A> <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerBinding%2A>클래스의, 및<xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerChannelBehaviors%2A> 속성을 설정 하는 방법에 대 한 자세한 내용은 방법:[ <xref:System.ServiceModel.Security.IssuedTokenClientCredential> 로컬 발급자](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)를 구성 합니다.  
  
## <a name="scoped-certificates"></a>범위가 지정된 인증서  
 보안 토큰 서비스와 통신할 서비스 인증서를 지정해야 하는 경우 일반적으로 인증서 협상이 사용되지 않으므로 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential> 속성을 사용하여 지정할 수 있습니다. <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.SetDefaultCertificate%2A> 메서드는 <xref:System.Uri> 및 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>를 매개 변수로 사용합니다. 지정한 인증서는 지정한 URI에서 엔드포인트와 통신할 때 사용됩니다. 또는 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.SetScopedCertificate%2A> 메서드를 사용하여 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A> 속성에서 반환된 컬렉션에 인증서를 추가할 수 있습니다.  
  
> [!NOTE]
> 제공된 URI로 범위가 지정된 인증서에 대한 클라이언트 개념은 이러한 URI에서 엔드포인트를 노출하는 서비스로 아웃바운드 호출하는 애플리케이션에만 적용됩니다. 발급 된 토큰에 서명 하는 데 사용 되는 인증서 (예: <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A> <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> 클래스의에서 반환 된 컬렉션의 서버에 구성 된 인증서)에는 적용 되지 않습니다. 자세한 내용은 [방법: 페더레이션 서비스](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)에 대 한 자격 증명을 구성 합니다.  
  
## <a name="see-also"></a>참고자료

- [페더레이션 샘플](../../../../docs/framework/wcf/samples/federation-sample.md)
- [방법: WSFederationHttpBinding에서 보안 세션을 사용 하지 않도록 설정](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)
- [방법: WSFederationHttpBinding 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)
- [방법: 페더레이션 서비스에 대 한 자격 증명 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [방법: 로컬 발급자 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)
- [메타데이터 관련 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)
- [방법: 보안 메타 데이터 끝점](../../../../docs/framework/wcf/feature-details/how-to-secure-metadata-endpoints.md)
