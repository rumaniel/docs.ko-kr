---
title: '방법: 서명 및 암호화에 별도의 X.509 인증서 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, extensibility
- ClientCredentials class
- ClientCredentialsSecurityTokenManager class
ms.assetid: 0b06ce4e-7835-4d82-8baf-d525c71a0e49
ms.openlocfilehash: e464aff46f311ede1cd629fb459ade9a6e627d59
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796952"
---
# <a name="how-to-use-separate-x509-certificates-for-signing-and-encryption"></a>방법: 서명 및 암호화에 별도의 X.509 인증서 사용

이 항목에서는 클라이언트와 서비스 모두에서 메시지 서명 및 암호화에 서로 다른 인증서를 사용 하도록 WCF (Windows Communication Foundation)를 구성 하는 방법을 보여 줍니다.

서명 및 암호화에 별도의 인증서를 사용 하려면 WCF에서 여러 클라이언트 또는 서비스 인증서를 설정 하는 API를 제공 하지 않기 때문에 사용자 지정 클라이언트 또는 서비스 자격 증명 (또는 둘 다)을 만들어야 합니다. 또한 여러 개의 인증서 정보를 활용하고 지정된 키 사용과 메시지 방향에 적합한 보안 토큰 공급자를 만들기 위해 보안 토큰 관리자도 제공되어야 합니다.

다음 다이어그램에서는 사용되는 주 클래스, 상속하는 클래스(위쪽 화살표로 표시), 특정 메서드 및 속성의 반환 형식을 보여 줍니다.

- `MyClientCredentials`는 <xref:System.ServiceModel.Description.ClientCredentials>의 사용자 지정 구현입니다.

  - 다이어그램에 표시된 속성은 모두 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>인스턴스를 반환합니다.

  - 메서드 <xref:System.ServiceModel.Description.ClientCredentials.CreateSecurityTokenManager%2A>는 `MyClientCredentialsSecurityTokenManager`인스턴스를 반환합니다.

- `MyClientCredentialsSecurityTokenManager`는 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>의 사용자 지정 구현입니다.

  - 메서드 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A>는 <xref:System.IdentityModel.Selectors.X509SecurityTokenProvider>인스턴스를 반환합니다.

![클라이언트 자격 증명을 사용 하는 방법을 보여 주는 차트](./media/e4971edd-a59f-4571-b36f-7e6b2f0d610f.gif "e4971edd-a59f-4571-b36f-7e6b2f0d610f")

사용자 지정 자격 증명 [에 대 한 자세한 내용은 연습: 사용자 지정 클라이언트 및 서비스 자격](walkthrough-creating-custom-client-and-service-credentials.md)증명을 만드는 중입니다.

또한 사용자 지정 ID 검증 도구를 만들고 사용자 지정 바인딩의 보안 바인딩 요소에 연결해야 합니다. 그리고 기본 자격 증명 대신 사용자 지정 자격 증명을 사용해야 합니다.

다음 다이어그램에서는 사용자 지정 바인딩에 관련된 클래스 및 사용자 지정 ID 검증 도구를 연결하는 방법을 보여 줍니다. 여러 바인딩 요소가 관련되어 있으며 이들 요소는 모두 <xref:System.ServiceModel.Channels.BindingElement>에서 상속합니다. <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>에는 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> 속성이 있습니다. 이 속성은 <xref:System.ServiceModel.Security.IdentityVerifier>가 사용자 지정되는 `MyIdentityVerifier`인스턴스를 반환합니다.

![사용자 지정 바인딩 요소를 보여 주는 차트](./media/dddea4a2-0bb4-4921-9bf4-20d4d82c3da5.gif "dddea4a2-0bb4-4921-9bf4-20d4d82c3da5")

사용자 지정 id 검증 도구를 만드는 방법에 대 한 자세한 내용은 방법: [방법: 사용자 지정 클라이언트 Id 검증 도구](how-to-create-a-custom-client-identity-verifier.md)를 만듭니다.

### <a name="to-use-separate-certificates-for-signing-and-encryption"></a>서명 및 암호화에 별도의 인증서를 사용하려면

1. <xref:System.ServiceModel.Description.ClientCredentials> 클래스에서 상속되는 새로운 클라이언트 자격 증명 클래스를 정의합니다. 여러 인증서 지정을 허용하는 네 가지 새 속성인 `ClientSigningCertificate`, `ClientEncryptingCertificate`, `ServiceSigningCertificate``ServiceEncryptingCertificate`및 를 구현합니다. 또한 <xref:System.ServiceModel.Description.ClientCredentials.CreateSecurityTokenManager%2A> 메서드를 재정의하여 다음 단계에 정의된 사용자 지정된 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 클래스의 인스턴스를 반환합니다.

     [!code-csharp[c_FourCerts#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#1)]
     [!code-vb[c_FourCerts#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#1)]

2. <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 클래스에서 상속되는 새로운 클라이언트 보안 토큰 관리자를 정의합니다. 올바른 보안 토큰 공급자를 만들기 위해 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> 메서드를 재정의합니다. 메시지 방향과 키 사용은 `requirement` 매개 변수(<xref:System.IdentityModel.Selectors.SecurityTokenRequirement>)를 통해 제공됩니다.

     [!code-csharp[c_FourCerts#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#2)]
     [!code-vb[c_FourCerts#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#2)]

3. <xref:System.ServiceModel.Description.ServiceCredentials> 클래스에서 상속되는 새로운 서비스 자격 증명 클래스를 정의합니다. 여러 인증서 지정을 허용하는 네 가지 새 속성인 `ClientSigningCertificate`, `ClientEncryptingCertificate`, `ServiceSigningCertificate``ServiceEncryptingCertificate`및 를 구현합니다. 또한 <xref:System.ServiceModel.Description.ServiceCredentials.CreateSecurityTokenManager%2A> 메서드를 재정의하여 다음 단계에 정의된 사용자 지정된 <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> 클래스의 인스턴스를 반환합니다.

     [!code-csharp[c_FourCerts#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#3)]
     [!code-vb[c_FourCerts#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#3)]

4. <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> 클래스에서 상속되는 새로운 서비스 보안 토큰 관리자를 정의합니다. 전달된 메시지 방향과 키 사용에 적합한 보안 토큰 공급자를 만들기 위해 <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> 메서드를 재정의합니다.

     [!code-csharp[c_FourCerts#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#4)]
     [!code-vb[c_FourCerts#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#4)]

### <a name="to-use-multiple-certificates-on-the-client"></a>클라이언트에 여러 인증서를 사용하려면

1. 사용자 지정 바인딩을 만듭니다. 보안 바인딩 요소는 요청 및 응답에 서로 다른 보안 토큰 공급자를 사용할 수 있도록 이중 모드로 작동되어야 합니다. 이를 위한 한 가지 방법은 다음 코드에서와 같이 <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>를 사용하거나 이중 가능 전송을 사용하는 것입니다. 다음 단계에 정의된 사용자 지정된 <xref:System.ServiceModel.Security.IdentityVerifier>를 보안 바인딩 요소에 연결합니다. 기본 클라이언트 자격 증명을 이전에 만든 사용자 지정된 클라이언트 자격 증명으로 바꿉니다.

     [!code-csharp[c_FourCerts#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#5)]
     [!code-vb[c_FourCerts#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#5)]

2. 사용자 지정 <xref:System.ServiceModel.Security.IdentityVerifier>를 정의합니다. 요청을 암호화하고 응답을 서명하는 데 서로 다른 인증서가 사용되므로 서비스에는 여러 개의 ID가 있습니다.

    > [!NOTE]
    > 다음 샘플에 제공된 사용자 지정 ID 검증 도구는 엔드포인트 ID 확인을 수행하지 않는 데모용이므로, 프로덕션 코드에 사용하지 않는 것이 좋습니다.

     [!code-csharp[c_FourCerts#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#6)]
     [!code-vb[c_FourCerts#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#6)]

### <a name="to-use-multiple-certificates-on-the-service"></a>서비스에 여러 인증서를 사용하려면

1. 사용자 지정 바인딩을 만듭니다. 보안 바인딩 요소는 요청 및 응답에 서로 다른 보안 토큰 공급자를 사용할 수 있도록 이중 모드로 작동되어야 합니다. 클라이언트와 마찬가지로, 다음 코드에서와 같이 <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>를 사용하거나 이중 가능 전송을 사용합니다. 기본 서비스 자격 증명을 이전에 만든 사용자 지정된 서비스 자격 증명으로 바꿉니다.

     [!code-csharp[c_FourCerts#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#7)]
     [!code-vb[c_FourCerts#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#7)]

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>
- <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager>
- <xref:System.ServiceModel.Security.IdentityVerifier>
- [연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기](walkthrough-creating-custom-client-and-service-credentials.md)
