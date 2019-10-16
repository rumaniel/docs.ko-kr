---
title: '방법: 사용자 지정 권한 부여 정책 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 05b0549b-882d-4660-b6f0-5678543e5475
ms.openlocfilehash: 5d5268cd2171bdccc3885cd599fdc8c277e61aa4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795709"
---
# <a name="how-to-create-a-custom-authorization-policy"></a>방법: 사용자 지정 권한 부여 정책 만들기
WCF (Windows Communication Foundation)의 Id 모델 인프라는 클레임 기반 권한 부여 모델을 지원 합니다. 클레임은 토큰에서 추출되어 사용자 지정 권한 부여 정책에 의해 선택적으로 처리된 다음,이후에 권한 부여를 결정하기 위해 검사할 수 있는 <xref:System.IdentityModel.Policy.AuthorizationContext>에 배치됩니다. 사용자 지정 정책은 들어오는 토큰을 애플리케이션에서 필요로 하는 클레임으로 변형하는 데 사용할 수 있습니다. 이러한 방식으로 WCF가 지 원하는 다양 한 토큰 형식에 의해 제공 되는 다양 한 클레임에 대 한 세부 정보에서 응용 프로그램 계층이 절연 될 수 있습니다. 이 항목에서는 사용자 지정 권한 부여 정책을 구현하는 방법과 이 정책을 서비스에 사용된 정책 컬렉션에 추가하는 방법에 대해 설명합니다.  
  
### <a name="to-implement-a-custom-authorization-policy"></a>사용자 지정 권한 부여 정책을 구현하려면  
  
1. <xref:System.IdentityModel.Policy.IAuthorizationPolicy>에서 파생되는 새 클래스를 정의합니다.  
  
2. 클래스에 대해 생성자에서 고유 문자열을 생성하고 속성에 액세스할 때마다 해당 문자열을 반환하여 읽기 전용 <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> 속성을 구현합니다.  
  
3. 정책 발급자를 나타내는<xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A>를 반환하여 읽기 전용 <xref:System.IdentityModel.Claims.ClaimSet> 속성을 구현합니다. 이는 애플리케이션을 나타내는 `ClaimSet`이거나 기본 제공된`ClaimSet`(예를 들면 정적 `ClaimSet` 속성에 의해 반환된 <xref:System.IdentityModel.Claims.ClaimSet.System%2A>)일 수 있습니다.  
  
4. 다음 절차에 따라 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 메서드를 구현합니다.  
  
### <a name="to-implement-the-evaluate-method"></a>Evaluate 메서드를 구현하려면  
  
1. 두 매개 변수인 개체 참조와 <xref:System.IdentityModel.Policy.EvaluationContext> 클래스의 인스턴스를 이 메서드에 전달합니다.  
  
2. 사용자 지정 권한 부여 정책이의 <xref:System.IdentityModel.Claims.ClaimSet> 현재 콘텐츠 <xref:System.IdentityModel.Policy.EvaluationContext>를 고려 하지 않고 인스턴스를 추가 하는 경우 메서드 `ClaimSet` 를 <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> 호출 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> 하 여 각를 `true` 추가 하 고 메서드에서를 반환 합니다. `true`가 반환되면 권한 부여 정책의 작업이 수행되어 이를 다시 호출할 필요가 없음을 권한 부여 인프라에 알립니다.  
  
3. 특정 클레임이 `EvaluationContext`에 이미 있는 경우에만 사용자 지정 권한 부여 정책을 통해 클레임 집합을 추가하려면 `ClaimSet` 속성에 의해 반환된 <xref:System.IdentityModel.Policy.EvaluationContext.ClaimSets%2A> 인스턴스를 검사하여 이러한 클레임을 찾습니다. 클레임이 있으면 <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> 메서드를 호출하여 새로운 클레임 집합을 추가하고, 추가할 클레임 집합이 없으면 권한 부여 정책의 작업이 완료되었음을 권한 부여 인프라에 알리는 `true`를 반환합니다. 클레임이 없으면 `false`를 반환하는 데, 이는 다른 권한 부여 정책을 통해 클레임 집합을 `EvaluationContext`에 추가하려면 권한 부여 정책을 다시 호출해야 함을 알립니다.  
  
4. 더 복잡한 처리 시나리오에서는 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 메서드의 두 번째 매개 변수를 사용하여 상태 변수를 저장합니다. 이 상태 변수는 이후 각 호출 동안 특정 평가를 목적으로 권한 부여 인프라가 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 메서드에 다시 전달하는 변수입니다.  
  
### <a name="to-specify-a-custom-authorization-policy-through-configuration"></a>구성을 통해 사용자 지정 권한 부여 정책을 지정하려면  
  
1. `policyType` 요소에서 `add` 요소에 있는 `authorizationPolicies` 요소의 `serviceAuthorization` 특성에 사용자 지정 권한 부여 정책 유형을 지정합니다.  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
        <serviceAuthorization serviceAuthorizationManagerType=  
                  "Samples.MyServiceAuthorizationManager" >  
          <authorizationPolicies>  
            <add policyType="Samples.MyAuthorizationPolicy" />  
          </authorizationPolicies>  
        </serviceAuthorization>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
### <a name="to-specify-a-custom-authorization-policy-through-code"></a>코드를 통해 사용자 지정 권한 부여 정책을 지정하려면  
  
1. <xref:System.Collections.Generic.List%601>의 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>을 만듭니다.  
  
2. 사용자 지정 권한 부여 정책의 인스턴스를 만듭니다.  
  
3. 권한 부여 정책 인스턴스를 목록에 추가합니다.  
  
4. 각 사용자 지정 권한 부여 정책에 대해 2단계와 3단계를 반복합니다.  
  
5. 읽기 전용 버전의 목록을 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A> 속성에 할당합니다.  
  
     [!code-csharp[c_CustomAuthPol#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#8)]
     [!code-vb[c_CustomAuthPol#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#8)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 전체 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 구현을 보여 줍니다.  
  
 [!code-csharp[c_CustomAuthPol#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#5)]
 [!code-vb[c_CustomAuthPol#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#5)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- [방법: 클레임 비교](how-to-compare-claims.md)
- [방법: 서비스에 대 한 사용자 지정 권한 부여 관리자 만들기](how-to-create-a-custom-authorization-manager-for-a-service.md)
- [권한 부여 정책](../samples/authorization-policy.md)
