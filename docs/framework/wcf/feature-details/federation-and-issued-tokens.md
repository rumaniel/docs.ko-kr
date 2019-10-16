---
title: 페더레이션 및 발급된 토큰
ms.date: 03/30/2017
helpviewer_keywords:
- WCF, federation
- issued tokens [WCF]
- federation [WCF], issued tokens
ms.assetid: 4c31ee7d-a820-4067-8b84-a83049021bb6
ms.openlocfilehash: 5ea30c2e9593f289c91a47cc082becf47dedc450
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61856455"
---
# <a name="federation-and-issued-tokens"></a>페더레이션 및 발급된 토큰
사용 하 여 Windows Communication Foundation (WCF), Ws-federation 및 Ws-trust 사양을 구현 하는 서비스를 사용 하 여 안전 하 게 통신 하는 클라이언트를 만들 수 있습니다. 사양은 XML, SOAP 및 WSDL(웹 서비스 기술 언어)을 사용하여 여러 신뢰 영역 간에 인증 및 권한을 사용할 수 있는 메커니즘을 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md)  
 페더레이션을 간략하게 설명합니다.  
  
 [페더레이션 및 트러스트](../../../../docs/framework/wcf/feature-details/federation-and-trust.md)  
 페더레이션 서비스 또는 클라이언트를 만들 때 알아야 할 디자인 문제에 대해 설명합니다.  
  
 [방법: 페더레이션된 클라이언트 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)  
 WCF를 사용 하 여 페더레이션된 클라이언트 만들기의 기본 사항을 설명 합니다.  
  
 [방법: 페더레이션 서비스에서 자격 증명 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)  
 페더레이션 서비스를 만드는 단계를 설명합니다.  
  
 [방법: WSFederationHttpBinding 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)  
 `WSFederationHttpBinding`을 사용하는 클라이언트 및 서비스를 구성하는 방법에 대해 설명합니다.  
  
 [방법: 보안 토큰 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-token-service.md)  
 보안 토큰 서비스를 만드는 단계를 설명합니다.  
  
 [SAML(Security Assertions Markup Language) 토큰 및 클레임](../../../../docs/framework/wcf/feature-details/saml-tokens-and-claims.md)  
 확장 가능하고 다양한 클레임 형식을 만들 수 있는 SAML(Security Assertions Markup Language) 토큰에 대해 설명합니다.  
  
 [방법: 로컬 발급자 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)  
 보안 토큰 로컬 발급자를 만드는 방법에 대해 설명합니다.  
  
 [방법: WSFederationHttpBinding에서 보안 세션을 사용 하지 않도록 설정](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 `WSFederationHttpBinding`에서 보안 세션을 비활성화하는 방법에 대해 설명합니다. 각 클라이언트에 대해 세션이 필요한 웹 팜을 만드는 경우 보안 세션을 비활성화해야 합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>  
  
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>  
  
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenProvider>  
  
 <xref:System.ServiceModel.WSFederationHttpBinding>  
  
## <a name="see-also"></a>참고자료

- [권한 부여](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)
- [사용자 지정 토큰](../../../../docs/framework/wcf/extending/custom-tokens.md)
- [Windows Server appfabric 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
