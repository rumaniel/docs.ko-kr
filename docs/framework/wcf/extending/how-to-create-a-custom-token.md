---
title: '방법: 사용자 지정 토큰 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SecurityTokenParameters class
- security [WCF], creating custom tokens
- WSSecurityTokenSerializer class
- SecurityToken class
ms.assetid: 6d892973-1558-4115-a9e1-696777776125
ms.openlocfilehash: 3bd44d197a655b67253ff363ef15937d4c021e08
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797048"
---
# <a name="how-to-create-a-custom-token"></a>방법: 사용자 지정 토큰 만들기
이 항목에서는 <xref:System.IdentityModel.Tokens.SecurityToken> 클래스를 사용하여 사용자 지정 보안 토큰을 만들고 사용자 지정 보안 토큰 공급자 및 인증자를 사용하여 통합하는 방법에 대해 설명합니다. 전체 코드 예제는 [사용자 지정 토큰](../samples/custom-token.md) 샘플을 참조 하세요.  
  
 *보안 토큰* 은 기본적으로 WCF (Windows Communication Foundation) 보안 프레임 워크에서 SOAP 메시지 내부의 발신자에 대 한 클레임을 나타내는 데 사용 되는 XML 요소입니다. WCF 보안은 시스템 제공 인증 모드에 대 한 다양 한 토큰을 제공 합니다. 예를 들면 <xref:System.IdentityModel.Tokens.X509SecurityToken> 클래스에 의해 표시되는 X.509 인증서 보안 토큰과 <xref:System.IdentityModel.Tokens.UserNameSecurityToken> 클래스에 의해 표시되는 사용자 이름 보안 토큰이 있습니다.  
  
 제공된 형식이 인증 모드나 자격 증명을 지원하지 않는 경우도 있습니다. 그럴 경우 사용자 지정 보안 토큰을 만들어 SOAP 메시지에서 사용자 지정 자격 증명의 XML 표현을 제공해야 합니다.  
  
 다음 절차에서는 사용자 지정 보안 토큰을 만드는 방법과이를 WCF 보안 인프라와 통합 하는 방법을 보여 줍니다. 이 항목에서는 클라이언트의 신용 카드 관련 정보를 서버에 전달하는 데 사용되는 신용 카드 토큰을 만듭니다.  
  
 사용자 지정 자격 증명 및 보안 토큰 관리자 [에 대 한 자세한 내용은 연습: 사용자 지정 클라이언트 및 서비스 자격](walkthrough-creating-custom-client-and-service-credentials.md)증명을 만드는 중입니다.  
  
 보안 토큰을 나타내는 클래스에 대한 자세한 내용은 <xref:System.IdentityModel.Tokens> 네임스페이스를 참조하십시오.  
  
## <a name="procedures"></a>절차  
 클라이언트 애플리케이션에 보안 인프라에 대한 신용 카드 정보를 지정할 수 있는 방법이 제공되어야 합니다. 이 정보는 사용자 지정 클라이언트 자격 증명 클래스를 통해 애플리케이션에서 사용할 수 있습니다. 첫 번째 단계에서는 사용자 지정 클라이언트 자격 증명에 대한 신용 카드 정보를 나타내는 클래스를 만듭니다.  
  
#### <a name="to-create-a-class-that-represents-credit-card-information-inside-client-credentials"></a>클라이언트 자격 증명에서 신용 카드 정보를 나타내는 클래스를 만들려면  
  
1. 애플리케이션에 대한 신용 카드 정보를 나타내는 새 클래스를 정의합니다. 다음 예제에서는 클래스의 이름을 `CreditCardInfo`로 지정합니다.  
  
2. 애플리케이션에서 사용자 지정 토큰에 필요한 정보를 설정할 수 있도록 클래스에 적절한 속성을 추가합니다. 이 예제에서는 클래스에 `CardNumber`, `CardIssuer` 및 `ExpirationDate`의 세 속성이 있습니다.  
  
     [!code-csharp[c_CustomToken#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#4)]
     [!code-vb[c_CustomToken#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#4)]  
  
 이제 사용자 지정 보안 토큰을 나타내는 클래스를 만들어야 합니다. 이 클래스는 보안 토큰 공급자, 인증자 및 serializer 클래스에서 보안 토큰에 대 한 정보를 WCF 보안 인프라에 전달 하는 데 사용 됩니다.  
  
#### <a name="to-create-a-custom-security-token-class"></a>사용자 지정 보안 토큰 클래스를 만들려면  
  
1. <xref:System.IdentityModel.Tokens.SecurityToken> 클래스에서 파생된 새 클래스를 정의합니다. 이 예제에서는 `CreditCardToken` 클래스를 만듭니다.  
  
2. <xref:System.IdentityModel.Tokens.SecurityToken.Id%2A> 속성을 재정의합니다. 이 속성은 SOAP 메시지 내의 다른 요소에서 보안 토큰 XML 표현을 가리키는 데 사용되는 보안 토큰의 로컬 식별자를 가져올 때 사용합니다. 이 예제에서는 토큰 식별자를 생성자 매개 변수로 전달하거나 보안 토큰 인스턴스를 만들 때마다 새 토큰 식별자를 임의로 생성합니다.  
  
3. <xref:System.IdentityModel.Tokens.SecurityToken.SecurityKeys%2A> 속성을 구현합니다. 이 속성은 보안 토큰 인스턴스가 나타내는 보안 키 컬렉션을 반환합니다. 이러한 키는 WCF에서 SOAP 메시지 부분을 서명 하거나 암호화 하는 데 사용할 수 있습니다. 이 예제에서 신용 카드 보안 토큰은 보안 키를 포함할 수 없기 때문에 속성 구현 시 항상 빈 컬렉션을 반환합니다.  
  
4. <xref:System.IdentityModel.Tokens.SecurityToken.ValidFrom%2A> 및 <xref:System.IdentityModel.Tokens.SecurityToken.ValidTo%2A> 속성을 재정의합니다. 이러한 속성은 WCF에서 보안 토큰 인스턴스의 유효성을 확인 하는 데 사용 됩니다. 이 예제에서는 신용 카드 보안 토큰에 만료 날짜만 있으므로, `ValidFrom` 속성은 인스턴스를 만든 날짜와 시간을 나타내는 <xref:System.DateTime>을 반환합니다.  
  
     [!code-csharp[c_CustomToken#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#1)]
     [!code-vb[c_CustomToken#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#1)]  
  
 새 보안 토큰 형식을 만들 때 <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters> 클래스를 구현해야 합니다. 구현은 보안 바인딩 요소 구성에서 새 토큰 형식을 나타내는 데 사용됩니다. 보안 토큰 매개 변수 클래스는 메시지를 처리할 때 실제 보안 토큰 인스턴스를 일치시키는 데 사용되는 템플릿 역할을 합니다. 템플릿은 애플리케이션에서 사용 또는 인증을 위해 보안 토큰을 일치시켜야 하는 기준을 지정하는 데 사용할 수 있는 추가 속성을 제공합니다. 다음 예제에서는 추가 속성을 추가 하지 않으므로 WCF 인프라가 사용할 보안 토큰 인스턴스를 검색 하거나 유효성을 검사할 때 보안 토큰 형식만 일치 합니다.  
  
#### <a name="to-create-a-custom-security-token-parameters-class"></a>사용자 지정 보안 토큰 매개 변수 클래스를 만들려면  
  
1. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters> 클래스에서 파생된 새 클래스를 정의합니다.  
  
2. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.CloneCore%2A> 메서드를 구현합니다. 클래스에 정의된 모든 내부 필드(있는 경우)를 복사합니다. 이 예제에서는 추가 필드를 정의하지 않습니다.  
  
3. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.SupportsClientAuthentication%2A> 읽기 전용 속성을 구현합니다. 이 속성은 이 클래스에 표시된 보안 토큰 형식을 사용하여 서비스에 클라이언트를 인증할 수 있는 경우 `true`를 반환합니다. 이 예제에서는 신용 카드 보안 토큰을 사용하여 서비스에 클라이언트를 인증할 수 있습니다.  
  
4. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.SupportsServerAuthentication%2A> 읽기 전용 속성을 구현합니다. 이 속성은 이 클래스에 표시된 보안 토큰 형식을 사용하여 클라이언트에 서비스를 인증할 수 있는 경우 `true`를 반환합니다. 이 예제에서는 신용 카드 보안 토큰을 사용하여 클라이언트에 서비스를 인증할 수 없습니다.  
  
5. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.SupportsClientWindowsIdentity%2A> 읽기 전용 속성을 구현합니다. 이 속성은 이 클래스에 표시된 보안 토큰 형식을 Windows 계정에 매핑할 수 있는 경우 `true`를 반환합니다. 그럴 경우 인증 결과는 <xref:System.Security.Principal.WindowsIdentity> 클래스 인스턴스에 의해 표시됩니다. 이 예제에서는 토큰을 Windows 계정에 매핑할 수 없습니다.  
  
6. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.CreateKeyIdentifierClause%28System.IdentityModel.Tokens.SecurityToken%2CSystem.ServiceModel.Security.Tokens.SecurityTokenReferenceStyle%29> 메서드를 구현합니다. 이 메서드는이 보안 토큰 매개 변수 클래스가 나타내는 보안 토큰 인스턴스에 대 한 참조가 필요한 경우 WCF 보안 프레임 워크에서 호출 됩니다. 실제 보안 토큰 인스턴스 및 요청 중인 참조 형식을 지정하는 <xref:System.ServiceModel.Security.Tokens.SecurityTokenReferenceStyle>이 모두 이 메서드에 인수로 전달됩니다. 이 예제에서 신용 카드 보안 토큰은 내부 참조만 지원합니다. <xref:System.IdentityModel.Tokens.SecurityToken> 클래스에는 내부 참조를 만드는 기능이 있으므로 구현 시에 추가 코드가 필요하지 않습니다.  
  
7. <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.InitializeSecurityTokenRequirement%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 메서드를 구현합니다. 이 메서드는 보안 토큰 매개 변수 클래스 인스턴스를 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 클래스의 인스턴스로 변환 하기 위해 WCF에서 호출 됩니다. 결과는 보안 토큰 공급자가 해당 보안 토큰 인스턴스를 만드는 데 사용됩니다.  
  
     [!code-csharp[c_CustomToken#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#2)]
     [!code-vb[c_CustomToken#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#2)]  
  
 보안 토큰은 SOAP 메시지 내부에서 전송되며, 메모리 내 보안 토큰 표시와 통신 중 표현 간의 변환 메커니즘이 필요합니다. WCF는 보안 토큰 serializer를 사용 하 여이 작업을 수행 합니다. 모든 사용자 지정 토큰은 SOAP 메시지로부터 사용자 지정 보안 토큰을 serialize 및 deserialize할 수 있는 사용자 지정 보안 토큰 serializer와 함께 표시되어야 합니다.  
  
> [!NOTE]
> 파생 키는 기본적으로 활성화됩니다. 사용자 지정 보안 토큰을 만들고 기본 토큰으로 사용 하는 경우 WCF는 해당 토큰에서 키를 파생 시킵니다. 이때 사용자 지정 보안 토큰 serializer를 호출하여 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause>을 네트워크에 serialize하는 동안 사용자 지정 보안 토큰에 대해 `DerivedKeyToken`을 작성합니다. 받는 측에서는 연결이 끊어진 상태에서 토큰을 deserialize하면 `DerivedKeyToken` serializer에서 `SecurityTokenReference` 요소를 자체의 최상위 자식으로 예상합니다. 사용자 지정 보안 토큰 serializer가 해당 절 형식을 serialize하는 동안 `SecurityTokenReference` 요소를 추가하지 않으면 예외가 throw됩니다.  
  
#### <a name="to-create-a-custom-security-token-serializer"></a>사용자 지정 보안 토큰 serializer를 만들려면  
  
1. <xref:System.ServiceModel.Security.WSSecurityTokenSerializer> 클래스에서 파생된 새 클래스를 정의합니다.  
  
2. <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.CanReadTokenCore%28System.Xml.XmlReader%29>를 사용하여 XML 스트림을 읽도록 <xref:System.Xml.XmlReader> 메서드를 재정의합니다. 이 메서드는 serializer 구현에서 지정된 현재 요소를 기반으로 보안 토큰을 deserialize할 수 있는 경우 `true`를 반환합니다. 이 예제에서 이 메서드는 XML 판독기의 현재 XML 요소의 요소 이름과 네임스페이스가 올바른지 확인합니다. 올바르지 않은 경우 이 메서드의 기본 클래스 구현을 호출하여 XML 요소를 처리합니다.  
  
3. <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.ReadTokenCore%28System.Xml.XmlReader%2CSystem.IdentityModel.Selectors.SecurityTokenResolver%29> 메서드를 재정의합니다. 이 메서드는 보안 토큰의 XML 내용을 읽고 적절한 메모리 내 표현을 생성합니다. 전달된 XML 판독기에 표시된 XML 요소를 인식할 수 없으면 기본 클래스 구현을 호출하여 시스템 제공 토큰 형식을 처리합니다.  
  
4. <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.CanWriteTokenCore%28System.IdentityModel.Tokens.SecurityToken%29> 메서드를 재정의합니다. 이 메서드는 인수로 전달된 메모리 내 토큰 표현을 XML 표현으로 변환할 수 있으면 `true`를 반환합니다. 변환할 수 없으면 기본 클래스 구현을 호출합니다.  
  
5. <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.WriteTokenCore%28System.Xml.XmlWriter%2CSystem.IdentityModel.Tokens.SecurityToken%29> 메서드를 재정의합니다. 이 메서드는 메모리 내 보안 토큰 표현을 XML 표현으로 변환합니다. 변환할 수 없으면 기본 클래스 구현을 호출합니다.  
  
     [!code-csharp[c_CustomToken#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#3)]
     [!code-vb[c_CustomToken#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#3)]  
  
 앞의 네 가지 절차를 완료한 후 보안 토큰 공급자, 인증자, 관리자, 클라이언트 및 서비스 자격 증명에 사용자 지정 보안 토큰을 통합합니다.  
  
#### <a name="to-integrate-the-custom-security-token-with-a-security-token-provider"></a>사용자 지정 보안 토큰을 보안 토큰 공급자와 통합하려면  
  
1. 보안 토큰 공급자는 토큰 인스턴스를 작성, 수정(필요한 경우) 및 반환합니다. 사용자 지정 보안 토큰에 대한 사용자 지정 공급자를 만들려면 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 클래스에서 상속되는 클래스를 만듭니다. 다음 예제에서는 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A> 인스턴스를 반환하도록 `CreditCardToken` 메서드를 재정의합니다. 사용자 지정 보안 토큰 공급자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 공급자](how-to-create-a-custom-security-token-provider.md)를 만듭니다.  
  
     [!code-csharp[c_CustomToken#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#6)]
     [!code-vb[c_CustomToken#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#6)]  
  
#### <a name="to-integrate-the-custom-security-token-with-a-security-token-authenticator"></a>사용자 지정 보안 토큰을 보안 토큰 인증자와 통합하려면  
  
1. 보안 토큰 인증자는 메시지에서 추출된 보안 토큰 내용의 유효성을 검사합니다. 사용자 지정 보안 토큰에 대한 사용자 지정 인증자를 만들려면 <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> 클래스에서 상속되는 클래스를 만듭니다. 다음 예제에서는 <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.ValidateTokenCore%2A> 메서드를 재정의합니다. 사용자 지정 보안 토큰 인증자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 인증자](how-to-create-a-custom-security-token-authenticator.md)를 만듭니다.  
  
     [!code-csharp[c_CustomToken#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#7)]
     [!code-vb[c_CustomToken#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#7)]  
  
     [!code-csharp[c_CustomToken#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#12)]
     [!code-vb[c_CustomToken#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#12)]  
  
#### <a name="to-integrate-the-custom-security-token-with-a-security-token-manager"></a>사용자 지정 보안 토큰을 보안 토큰 관리자와 통합하려면  
  
1. 보안 토큰 관리자는 적절한 토큰 공급자, 보안 인증자 및 토큰 serializer 인스턴스를 만듭니다. 사용자 지정 토큰 관리자를 만들려면 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>에서 상속되는 클래스를 만듭니다. 클래스의 기본 메서드에서는 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>를 사용하여 적절한 공급자와 클라이언트 또는 서비스 자격 증명을 만듭니다. 사용자 지정 보안 토큰 관리자 [에 대 한 자세한 내용은 연습: 사용자 지정 클라이언트 및 서비스 자격](walkthrough-creating-custom-client-and-service-credentials.md)증명을 만드는 중입니다.  
  
     [!code-csharp[c_CustomToken#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#8)]
     [!code-vb[c_CustomToken#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#8)]  
  
     [!code-csharp[c_CustomToken#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#9)]
     [!code-vb[c_CustomToken#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#9)]  
  
#### <a name="to-integrate-the-custom-security-token-with-custom-client-and-service-credentials"></a>사용자 지정 보안 토큰을 사용자 지정 클라이언트 및 서비스 자격 증명과 통합하려면  
  
1. 애플리케이션에서 사용자 지정 보안 토큰 내용을 제공 및 인증하기 위해 앞에서 만든 사용자 지정 보안 토큰 인프라에 사용되는 사용자 지정 토큰 정보를 지정할 수 있도록 API를 제공하려면 사용자 지정 클라이언트 및 서비스 자격 증명을 추가해야 합니다. 다음 샘플은 이 작업을 수행하는 방법을 보여 줍니다. 사용자 지정 클라이언트 및 서비스 자격 증명 [에 대 한 자세한 내용은 연습: 사용자 지정 클라이언트 및 서비스 자격](walkthrough-creating-custom-client-and-service-credentials.md)증명을 만드는 중입니다.  
  
     [!code-csharp[c_CustomToken#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#10)]
     [!code-vb[c_CustomToken#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#10)]  
  
     [!code-csharp[c_customToken#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#11)]
     [!code-vb[c_customToken#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#11)]  
  
 이전에 만든 사용자 지정 보안 토큰 매개 변수 클래스를 사용 하 여 WCF 보안 프레임 워크에 서비스와 통신할 때 사용자 지정 보안 토큰을 사용 해야 함을 알립니다. 다음 절차는 이 작업을 수행하는 방법을 보여 줍니다.  
  
#### <a name="to-integrate-the-custom-security-token-with-the-binding"></a>사용자 지정 보안 토큰을 바인딩과 통합하려면  
  
1. <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스에 노출되는 토큰 매개 변수 컬렉션 중 하나에서 사용자 지정 보안 토큰 매개 변수 클래스를 지정해야 합니다. 다음 예제에서는 `SignedEncrypted`가 반환하는 컬렉션을 사용합니다. 이 코드는 내용을 자동으로 서명한 후 암호화하여 클라이언트에서 서비스로 보낸 모든 메시지에 신용 카드 사용자 지정 토큰을 추가합니다.  
  
     [!code-csharp[c_CustomToken#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#13)]
     [!code-vb[c_CustomToken#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#13)]  
  
 이 항목에서는 사용자 지정 토큰을 구현하고 사용하는 데 필요한 다양한 코드를 보여 줍니다. 이러한 모든 코드 부분이 함께 표시 되는 방법의 전체 예제를 보려면 [사용자 지정 토큰](../samples/custom-token.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Tokens.SecurityToken>
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters>
- <xref:System.ServiceModel.Security.WSSecurityTokenSerializer>
- <xref:System.IdentityModel.Selectors.SecurityTokenProvider>
- <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.Channels.SecurityBindingElement>
- [연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기](walkthrough-creating-custom-client-and-service-credentials.md)
- [방법: 사용자 지정 보안 토큰 인증자 만들기](how-to-create-a-custom-security-token-authenticator.md)
- [방법: 사용자 지정 보안 토큰 공급자 만들기](how-to-create-a-custom-security-token-provider.md)
