---
title: SAML 토큰 및 클레임
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
- issued tokens
- SAML token
ms.assetid: 930b6e34-9eab-4e95-826c-4e06659bb977
ms.openlocfilehash: 7037daf299d7c750ab398c21c1d7ccb541620701
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69943067"
---
# <a name="saml-tokens-and-claims"></a>SAML 토큰 및 클레임
SAML (Security 어설션이 Markup Language) *토큰* 은 클레임의 XML 표현입니다. 기본적으로 페더레이션 보안 시나리오에서 WCF (Windows Communication Foundation)가 사용 하는 SAML 토큰은 *발급 된 토큰*입니다.  
  
 SAML 토큰은 하나의 엔터티에서 다른 엔터티에 대해 만든 클레임 집합인 문을 수행합니다. 예를 들어, 페더레이션 보안 시나리오의 경우 시스템의 사용자에 대한 보안 토큰 서비스에서 문을 작성합니다. 보안 토큰 서비스에서는 토큰에 포함된 문의 정확성을 나타내기 위해 SAML 토큰을 서명합니다. 또한 SAML 토큰은 암호화 키 자료와 연결되어 있으며, 이 때 SAML 토큰의 사용자는 해당 키 자료를 알고 있음을 증명합니다. 이 증명은 신뢰하는 상대에게 SAML 토큰이 실제로 해당 사용자에게 발행되었음을 나타냅니다. 예를 들어, 일반적인 시나리오는 다음과 같습니다.  
  
1. 클라이언트는 보안 토큰 서비스에서 SAML 토큰을 요청하고 Windows 자격 증명을 사용하여 해당 보안 토큰 서비스를 인증합니다.  
  
2. 보안 토큰 서비스는 SAML 토큰을 클라이언트에 발행합니다. SAML 토큰은 보안 토큰 서비스와 연결된 인증서를 통해 서명되며, 대상 서비스에 대해 암호화된 증명 키를 포함합니다.  
  
3. 클라이언트는 *증명 키*의 복사본도 받습니다. 클라이언트는 응용 프로그램 서비스 ( *신뢰*당사자)에 SAML 토큰을 제공 하 고 해당 증명 키로 메시지에 서명 합니다.  
  
4. SAML 토큰을 통한 서명은 신뢰하는 상대에게 보안 토큰 서비스에서 토큰을 발행했음을 나타냅니다. 증명 키를 사용하여 만든 메시지 서명은 신뢰하는 상대에게 토큰이 클라이언트에게 발행되었음을 나타냅니다.  
  
## <a name="from-claims-to-samlattributes"></a>클레임에서 SamlAttribute로  
 WCF에서 SAML 토큰의 문은 개체로 모델링 <xref:System.IdentityModel.Tokens.SamlAttribute> 됩니다. 개체의 <xref:System.IdentityModel.Claims.Claim.Right%2A> 속성이 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 이 고 <xref:System.IdentityModel.Claims.Claim.Resource%2A> 속성이 인 경우 <xref:System.IdentityModel.Claims.Claim> 개체에서 <xref:System.IdentityModel.Claims.Claim> 직접 채워질 수 있습니다. 을 <xref:System.String>입력 합니다. 예를 들어:  
  
 [!code-csharp[c_CreateSTS#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#8)]
 [!code-vb[c_CreateSTS#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#8)]  
  
> [!NOTE]
> SAML 토큰이 메시지에 serialize될 때 보안 토큰 서비스에서 해당 토큰을 발행하거나 클라이언트에서 인증의 일부로 해당 토큰을 서비스에 제공하는 경우, 최대 메시지 크기 할당량은 SAML 토큰 및 다른 메시지 부분을 수용할 수 있도록 충분히 커야 합니다. 일반적으로 기본 메시지 크기 할당량이면 충분합니다. 그러나 SAML 토큰에 수백 개의 클레임이 포함되어 있어 SAML 토큰이 큰 경우에는 serialize된 토큰을 수용할 수 있도록 할당량을 늘려야 할 수 있습니다. 자세한 내용은 [데이터에 대 한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)합니다.  
  
## <a name="from-samlattributes-to-claims"></a>SamlAttribute에서 클레임으로  
 메시지에서 SAML 토큰을 받으면 SAML 토큰의 여러 문이 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>에 배치되는 <xref:System.IdentityModel.Policy.AuthorizationContext> 개체로 변경됩니다. 각 SAML 문의 클레임은 <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A>의 <xref:System.IdentityModel.Policy.AuthorizationContext> 속성에서 반환하며, 사용자 인증 및 권한 부여 여부를 결정하기 위해 검사할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Policy.AuthorizationContext>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- <xref:System.IdentityModel.Claims.ClaimSet>
- [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md)
- [방법: 페더레이션된 클라이언트 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [방법: 페더레이션 서비스에 대 한 자격 증명 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [ID 모델을 사용하여 클레임 및 권한 부여 관리](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
- [클레임 및 토큰](../../../../docs/framework/wcf/feature-details/claims-and-tokens.md)
- [클레임 만들기 및 리소스 값](../../../../docs/framework/wcf/feature-details/claim-creation-and-resource-values.md)
- [방법: 사용자 지정 클레임 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-claim.md)
