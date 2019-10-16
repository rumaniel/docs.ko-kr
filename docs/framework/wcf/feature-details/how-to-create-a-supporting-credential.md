---
title: '방법: 지원하는 자격 증명 만들기'
ms.date: 03/30/2017
ms.assetid: d0952919-8bb4-4978-926c-9cc108f89806
ms.openlocfilehash: 1f95748235aa5238193b8869f8330f0a7fc650d9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968895"
---
# <a name="how-to-create-a-supporting-credential"></a>방법: 지원하는 자격 증명 만들기
둘 이상의 자격 증명이 필요한 사용자 지정 보안 체계를 사용할 수 있습니다. 예를 들어 서비스는 클라이언트로부터 사용자 이름과 암호뿐 아니라 클라이언트가 18세 이상임을 입증하는 자격 증명을 요구할 수 있습니다. 두 번째 자격 증명은 *지원 자격 증명*입니다. 이 항목에서는 WCF (Windows Communication Foundation) 클라이언트에서 이러한 자격 증명을 구현 하는 방법을 설명 합니다.  
  
> [!NOTE]
> 지원 자격 증명의 사양은 WS-SecurityPolicy 사양의 일부입니다. 자세한 내용은 [Web Services Security 사양](https://go.microsoft.com/fwlink/?LinkId=88537)을 참조 하세요.  
  
## <a name="supporting-tokens"></a>Supporting Tokens  
 간단히 말해서 메시지 보안을 사용 하는 경우 *기본 자격 증명* 을 사용 하 여 메시지를 보호 합니다 (예: x.509 인증서 또는 Kerberos 티켓).  
  
 사양에 정의 된 대로 보안 바인딩은 *토큰* 을 사용 하 여 메시지 교환을 보호 합니다. *토큰* 은 보안 자격 증명을 나타냅니다.  
  
 보안 바인딩은 보안 바인딩 정책에 식별된 기본 토큰을 사용하여 서명을 만듭니다. 이 시그니처를 *메시지 서명*이라고 합니다.  
  
 추가 토큰을 지정하여 메시지 서명과 연결된 토큰이 제공하는 클레임을 증대시킬 수 있습니다.  
  
## <a name="endorsing-signing-and-encrypting"></a>보증, 서명 및 암호화  
 지원 자격 증명은 메시지 내부에 전송 된 *지원 토큰* 을 생성 합니다. WS-SecurityPolicy 사양은 다음 표에 설명된 것처럼 지원 토큰을 메시지에 첨부하는 네 가지 방법을 정의합니다.  
  
|용도|설명|  
|-------------|-----------------|  
|서명|지원 토큰은 보안 헤더에 포함되고 메시지 서명으로 서명됩니다.|  
|보증|*보증 토큰* 은 메시지 서명에 서명 합니다.|  
|서명 및 보증|서명된 보증 토큰은 메시지 서명에서 생성된 `ds:Signature` 요소에 서명하고 그 자체가 해당 메시지 서명으로 서명됩니다. 즉, 두 토큰(메시지 서명에 사용된 토큰과 서명된 보증 토큰)이 서로에 서명합니다.|  
|서명 및 암호화|서명 및 암호화된 지원 토큰은 `wsse:SecurityHeader`에 나타날 때 암호화되는 서명된 지원 토큰입니다.|  
  
## <a name="programming-supporting-credentials"></a>지원 자격 증명 프로그래밍  
 지원 토큰을 사용 하는 서비스를 만들려면 [ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)를 만들어야 합니다. 자세한 내용은 다음을 참조 하세요 [. SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)를 사용 하 여 사용자 지정 바인딩을 만듭니다.  
  
 사용자 지정 바인딩을 만들 때의 첫 단계는 다음 세 가지 형식 중 하나일 수 있는 보안 바인딩 요소를 만드는 작업입니다.  
  
- <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>  
  
- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>  
  
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>  
  
 모든 클래스는 다음 네 가지 관련 속성을 포함하는 <xref:System.ServiceModel.Channels.SecurityBindingElement>에서 상속됩니다.  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.EndpointSupportingTokenParameters%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.OperationSupportingTokenParameters%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.OptionalEndpointSupportingTokenParameters%2A>  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement.OptionalOperationSupportingTokenParameters%2A>  
  
#### <a name="scopes"></a>범위  
 지원 자격 증명에 대한 두 가지 범위가 있습니다.  
  
- *끝점 지원 토큰* 은 끝점의 모든 작업을 지원 합니다. 즉, 엔드포인트 작업을 호출할 때마다 지원 토큰이 나타내는 자격 증명을 사용할 수 있습니다.  
  
- *작업 지원 토큰* 은 특정 끝점 작업만 지원 합니다.  
  
 속성 이름이 나타내는 것처럼 지원 자격 증명은 필수 또는 옵션일 수 있습니다. 즉, 지원 자격 증명이 있으면 필요하지 않아도 사용되지만 없어도 인증이 실패하지 않습니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-create-a-custom-binding-that-includes-supporting-credentials"></a>지원 자격 증명을 포함하는 사용자 지정 바인딩을 만들려면  
  
1. 보안 바인딩 요소를 만듭니다. 아래 예제에서는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 인증 모드로 `UserNameForCertificate`를 만듭니다. <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateUserNameForCertificateBindingElement%2A> 메서드를 사용하세요.  
  
2. 해당 속성(`Endorsing`, `Signed`, `SignedEncrypted` 또는 `SignedEndorsed`)에 의해 반환된 형식 컬렉션에 지원 매개 변수를 추가합니다. <xref:System.ServiceModel.Security.Tokens> 네임스페이스의 형식에는 <xref:System.ServiceModel.Security.Tokens.X509SecurityTokenParameters> 같은 자주 사용되는 형식이 포함됩니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 다음 예제에서는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>의 인스턴스를 만들고 <xref:System.ServiceModel.Security.Tokens.KerberosSecurityTokenParameters> 클래스의 인스턴스를 반환된 Endorsing 속성 컬렉션에 추가합니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[c_SupportingCredential#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_supportingcredential/cs/source.cs#1)]  
  
## <a name="see-also"></a>참고자료

- [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
