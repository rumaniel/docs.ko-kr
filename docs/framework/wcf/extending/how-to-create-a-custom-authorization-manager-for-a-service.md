---
title: '방법: 서비스에 대한 사용자 지정 권한 부여 관리자 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Communication Foundation, extending
- OperationRequirement class
ms.assetid: 6214afde-44c1-4bf5-ba07-5ad6493620ea
ms.openlocfilehash: 9c28cb81b78f80505cfcf5f7e4dfdba083bd0793
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797117"
---
# <a name="how-to-create-a-custom-authorization-manager-for-a-service"></a>방법: 서비스에 대한 사용자 지정 권한 부여 관리자 만들기

WCF (Windows Communication Foundation)의 Id 모델 인프라는 확장 가능한 클레임 기반 권한 부여 모델을 지원 합니다. 클레임은 토큰에서 추출되어 사용자 지정 권한 부여 정책에 의해 선택적으로 처리된 다음,<xref:System.IdentityModel.Policy.AuthorizationContext>에 배치됩니다. 권한 부여 관리자는 <xref:System.IdentityModel.Policy.AuthorizationContext>에서 클레임을 검사하여 권한 부여 결정을 내립니다.

기본적으로 권한 부여는 <xref:System.ServiceModel.ServiceAuthorizationManager> 클래스에서 결정되지만, 사용자 지정 권한 부여 관리자를 만들어 이러한 결정을 재정의할 수 있습니다. 사용자 지정 권한 부여 관리자를 만들려면 <xref:System.ServiceModel.ServiceAuthorizationManager>에서 파생되는 클래스를 만든 다음 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 메서드를 구현합니다. 권한 부여는 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 메서드에서 결정되며, 액세스가 허용되면 `true`를 반환하고 액세스가 거부되면 `false`를 반환합니다.

권한 부여 결정이 메시지 본문 내용에 따라 달라지는 경우 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A> 메서드를 사용합니다.

성능 문제 때문에 가능하다면 권한 부여 결정 시 메시지 본문에 액세스하지 않아도 되도록 애플리케이션을 다시 디자인해야 합니다.

서비스에 대한 사용자 지정 권한 부여 관리자는 코드 또는 구성을 통해 등록할 수 있습니다.

### <a name="to-create-a-custom-authorization-manager"></a>사용자 지정 권한 부여 관리자를 만들려면

1. <xref:System.ServiceModel.ServiceAuthorizationManager> 클래스에서 클래스를 파생시킵니다.

    [!code-csharp[c_CustomAuthMgr#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#5)]
    [!code-vb[c_CustomAuthMgr#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#5)]

2. <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%28System.ServiceModel.OperationContext%29> 메서드를 재정의합니다.

    <xref:System.ServiceModel.OperationContext> 메서드에 전달되는 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%28System.ServiceModel.OperationContext%29>를 사용하여 권한 부여 결정을 내립니다.

    다음 코드 예제에서는 권한 부여 결정을 내리기 위해 <xref:System.IdentityModel.Claims.ClaimSet.FindClaims%28System.String%2CSystem.String%29> 메서드를 사용하여 사용자 지정 클레임 `http://www.contoso.com/claims/allowedoperation`을 찾습니다.

    [!code-csharp[c_CustomAuthMgr#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#6)]
    [!code-vb[c_CustomAuthMgr#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#6)]

### <a name="to-register-a-custom-authorization-manager-using-code"></a>코드를 사용하여 사용자 지정 권한 부여 관리자를 등록하려면

1. 사용자 지정 권한 부여 관리자의 인스턴스를 만들어 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ServiceAuthorizationManager%2A> 속성에 할당합니다.

    <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 속성을 사용하여 <xref:System.ServiceModel.ServiceHostBase.Authorization%2A>에 액세스할 수 있습니다.

    다음 코드 예제에서는 `MyServiceAuthorizationManager` 사용자 지정 권한 부여 관리자를 등록합니다.

    [!code-csharp[c_CustomAuthMgr#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#4)]
    [!code-vb[c_CustomAuthMgr#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#4)]

### <a name="to-register-a-custom-authorization-manager-using-configuration"></a>구성을 사용하여 사용자 지정 권한 부여 관리자를 등록하려면

1. 서비스에 대한 구성 파일을 엽니다.

2. [> 동작\<](../../configure-apps/file-schema/wcf/behaviors.md)에 [ \<serviceauthorization >](../../configure-apps/file-schema/wcf/serviceauthorization-element.md) 를 추가 합니다.

    Serviceauthorization `serviceAuthorizationManagerType` >에 특성을 추가 하 고 해당 값을 사용자 지정 권한 부여 관리자를 나타내는 형식으로 설정 합니다. [ \<](../../configure-apps/file-schema/wcf/serviceauthorization-element.md)

3. 클라이언트와 서비스 간의 통신을 보안하는 바인딩을 추가합니다.

    이 통신에 대해 선택된 바인딩에 따라 <xref:System.IdentityModel.Policy.AuthorizationContext>에 추가되는 클레임이 결정되고, 사용자 지정 권한 부여 관리자는 이 클레임을 사용하여 권한 부여 결정을 내립니다. 시스템에서 제공 하는 바인딩에 대 한 자세한 내용은 [시스템 제공 바인딩](../system-provided-bindings.md)을 참조 하십시오.

4. [ \<서비스 >](../../configure-apps/file-schema/wcf/service.md) 요소를 추가 하 고 `behaviorConfiguration` 특성 값을 [ \<behavior >](../../configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 요소의 name 특성 값으로 설정 하 여 동작을 서비스 끝점에 연결 합니다.

    서비스 끝점 [을 구성 하는 방법에 대 한 자세한 내용은 방법: 구성](../feature-details/how-to-create-a-service-endpoint-in-configuration.md)에서 서비스 끝점을 만듭니다.

    다음 코드 예제에서는 `Samples.MyServiceAuthorizationManager` 사용자 지정 권한 부여 관리자를 등록합니다.

    ```xml
    <configuration>
      <system.serviceModel>
        <services>
          <service
              name="Microsoft.ServiceModel.Samples.CalculatorService"
              behaviorConfiguration="CalculatorServiceBehavior">
            <host>
              <baseAddresses>
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>
              </baseAddresses>
            </host>
            <endpoint address=""
                      binding="wsHttpBinding_Calculator"
                      contract="Microsoft.ServiceModel.Samples.ICalculator" />
          </service>
        </services>
        <bindings>
          <WSHttpBinding>
           <binding name = "wsHttpBinding_Calculator">
             <security mode="Message">
               <message clientCredentialType="Windows"/>
             </security>
            </binding>
          </WSHttpBinding>
        </bindings>
        <behaviors>
          <serviceBehaviors>
            <behavior name="CalculatorServiceBehavior">
              <serviceAuthorization serviceAuthorizationManagerType="Samples.MyServiceAuthorizationManager,MyAssembly" />
             </behavior>
         </serviceBehaviors>
       </behaviors>
      </system.serviceModel>
    </configuration>
    ```

    > [!WARNING]
    > serviceAuthorizationManagerType을 지정할 경우 문자열에 정규화된 형식 이름이 포함되어야 합니다. 콤마 및 형식이 정의된 어셈블리의 이름입니다. 어셈블리 이름을 지정하지 않을 경우 WCF는 System.ServiceModel.dll에서 형식 로드를 시도합니다.

## <a name="example"></a>예제

다음 코드 예제에서는 <xref:System.ServiceModel.ServiceAuthorizationManager> 메서드 재정의를 포함하는 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 클래스의 기본 구현을 보여 줍니다. 예제 코드에서는 <xref:System.IdentityModel.Policy.AuthorizationContext>에서 사용자 지정 클레임을 검사하고 해당 사용자 지정 클레임의 리소스가 `true`의 동작 값과 일치하면 <xref:System.ServiceModel.OperationContext>를 반환합니다. <xref:System.ServiceModel.ServiceAuthorizationManager> 클래스의 전체 구현에 대 한 자세한 내용은 [권한 부여 정책](../samples/authorization-policy.md)을 참조 하세요.

[!code-csharp[c_CustomAuthMgr#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#2)]
[!code-vb[c_CustomAuthMgr#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#2)]

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- [권한 부여 정책](../samples/authorization-policy.md)
