---
title: '방법: 사용자 지정 클라이언트 ID 검증 도구 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f2d34e43-fa8b-46d2-91cf-d2960e13e16b
ms.openlocfilehash: 86e7869efdba50d72cc61a1aebb767cf43927546
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795640"
---
# <a name="how-to-create-a-custom-client-identity-verifier"></a>방법: 사용자 지정 클라이언트 ID 검증 도구 만들기
WCF (Windows Communication Foundation)의 *id* 기능을 사용 하면 클라이언트에서 필요한 서비스 id를 미리 지정할 수 있습니다. 서버가 클라이언트에 자신을 인증할 때마다 이 ID와 비교하여 ID가 검사됩니다. (Id 및 작동 방식에 대 한 설명은 [서비스 id 및 인증](../feature-details/service-identity-and-authentication.md)을 참조 하세요.)  
  
 필요한 경우 사용자 지정 ID 검증 도구를 사용하여 확인을 사용자 지정할 수 있습니다. 예를 들어, 서비스 ID 확인 검사를 추가로 수행할 수 있습니다. 이 예에서 사용자 지정 ID 검증 도구는 서버에서 반환되는 X.509 인증서에서 추가 클레임을 검사합니다. 샘플 응용 프로그램은 [서비스 Id 샘플](../samples/service-identity-sample.md)을 참조 하세요.  
  
### <a name="to-extend-the-endpointidentity-class"></a>EndpointIdentity 클래스를 확장하려면  
  
1. <xref:System.ServiceModel.EndpointIdentity> 클래스에서 파생되는 새 클래스를 정의합니다. 이 예에서는 확장 이름을 `OrgEndpointIdentity`로 지정합니다.  
  
2. 서비스에서 반환된 보안 토큰의 클레임에 대해 ID 검사를 수행하기 위해 확장 <xref:System.ServiceModel.Security.IdentityVerifier> 클래스에서 사용할 속성과 함께 private 멤버를 추가합니다. 이 예에서는 `OrganizationClaim` 속성 하나를 정의합니다.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
     [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
### <a name="to-extend-the-identityverifier-class"></a>IdentityVerifier 클래스를 확장하려면  
  
1. <xref:System.ServiceModel.Security.IdentityVerifier>에서 파생되는 새 클래스를 정의합니다. 이 예에서는 확장 이름을 `CustomIdentityVerifier`로 지정합니다.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#7)]
     [!code-vb[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#7)]  
  
2. <xref:System.ServiceModel.Security.IdentityVerifier.CheckAccess%2A> 메서드를 재정의합니다. 이 메서드는 ID 검사의 성공 또는 실패 여부를 확인합니다.  
  
3. `CheckAccess` 메서드는 두 개의 매개 변수를 사용합니다. 하나는 <xref:System.ServiceModel.EndpointIdentity> 클래스의 인스턴스이고 다른 하나는 <xref:System.IdentityModel.Policy.AuthorizationContext> 클래스의 인스턴스입니다.  
  
     메서드 구현에서는 <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> 클래스의 <xref:System.IdentityModel.Policy.AuthorizationContext> 속성에서 반환된 클레임의 컬렉션을 검사한 다음 필요한 경우 인증 검사를 수행합니다. 이 예에서는 먼저 형식이 "고유 이름"인 클레임을 찾은 다음 <xref:System.ServiceModel.EndpointIdentity>의 확장명(`OrgEndpointIdentity`)과 이름을 비교합니다.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#1)]
     [!code-vb[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#1)]  
  
### <a name="to-implement-the-trygetidentity-method"></a>TryGetIdentity 메서드를 구현하려면  
  
1. 클라이언트가 <xref:System.ServiceModel.Security.IdentityVerifier.TryGetIdentity%2A> 클래스의 인스턴스를 반환할 수 있는지 여부를 확인하는 <xref:System.ServiceModel.EndpointIdentity> 메서드를 구현합니다. WCF 인프라는 먼저 `TryGetIdentity` 메서드의 구현을 호출 하 여 메시지에서 서비스의 id를 검색 합니다. 그런 다음 반환된 `CheckAccess` 및 `EndpointIdentity`와 함께 <xref:System.IdentityModel.Policy.AuthorizationContext> 구현을 호출합니다.  
  
2. `TryGetIdentity` 메서드에서 다음 코드를 입력합니다.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#2)]
     [!code-vb[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#2)]  
  
### <a name="to-implement-a-custom-binding-and-set-the-custom-identityverifier"></a>사용자 지정 바인딩을 구현하고 사용자 지정 IdentityVerifier를 설정하려면  
  
1. <xref:System.ServiceModel.Channels.Binding> 개체를 반환하는 메서드를 만듭니다. 이 예에서는 먼저 <xref:System.ServiceModel.WSHttpBinding> 클래스의 인스턴스를 만든 다음 보안 모드를 <xref:System.ServiceModel.SecurityMode.Message>로 설정하고 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A>을 <xref:System.ServiceModel.MessageCredentialType.None>으로 설정합니다.  
  
2. <xref:System.ServiceModel.Channels.BindingElementCollection> 메서드를 사용하여 <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A>을 만듭니다.  
  
3. 컬렉션에서 <xref:System.ServiceModel.Channels.SecurityBindingElement>를 반환한 다음 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 변수로 캐스팅합니다.  
  
4. <xref:System.ServiceModel.Channels.LocalClientSecuritySettings.IdentityVerifier%2A> 클래스의 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> 속성을 이전에 만든 `CustomIdentityVerifier` 클래스의 새 인스턴스로 설정합니다.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#3)]
     [!code-vb[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#3)]  
  
5. 반환된 사용자 지정 바인딩을 사용하여 클라이언트 및 클래스의 인스턴스를 만듭니다. 그런 다음 클라이언트는 다음 코드에서와 같이 서비스에 대해 사용자 지정 ID 확인 검사를 수행할 수 있습니다.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#4)]
     [!code-vb[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#4)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.ServiceModel.Security.IdentityVerifier> 클래스의 전체 구현을 보여 줍니다.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#5)]
 [!code-vb[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#5)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.ServiceModel.EndpointIdentity> 클래스의 전체 구현을 보여 줍니다.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
 [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- <xref:System.ServiceModel.EndpointIdentity>
- <xref:System.ServiceModel.Security.IdentityVerifier>
- [서비스 ID 샘플](../samples/service-identity-sample.md)
- [권한 부여 정책](../samples/authorization-policy.md)
