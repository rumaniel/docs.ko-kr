---
title: '방법: 사용자 지정 사용자 이름 및 암호에 대한 유효성 검사기 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, username and password
ms.assetid: 8e08b74b-fa44-4018-b63d-0d0805f85e3f
ms.openlocfilehash: 98ffad7e717aac949509fa701c77d8ba2b80a695
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834689"
---
# <a name="how-to-use-a-custom-user-name-and-password-validator"></a>방법: 사용자 지정 사용자 이름 및 암호에 대한 유효성 검사기 사용

기본적으로 인증에 사용자 이름과 암호를 사용 하는 경우 WCF (Windows Communication Foundation)는 Windows를 사용 하 여 사용자 이름과 암호의 유효성을 검사 합니다. 그러나 WCF는 사용자 지정 사용자 이름 및 암호 인증 스키마 ( *유효성 검사기*라고도 함)를 허용 합니다. 사용자 지정 사용자 이름 및 암호 유효성 검사기를 통합하려면 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>에서 파생되는 클래스를 만들어 구성합니다.

응용 프로그램 예제는 [사용자 이름 암호 유효성 검사기](../samples/user-name-password-validator.md)를 참조 하세요.

### <a name="to-create-a-custom-user-name-and-password-validator"></a>사용자 지정 사용자 이름 및 암호 유효성 검사기를 만들려면

1. <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>에서 파생되는 클래스를 만듭니다.

    [!code-csharp[C_CustomUsernameAndPasswordValidator#3](~/samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#3)]
    [!code-vb[C_CustomUsernameAndPasswordValidator#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#3)]

2. <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 메서드를 재정의하여 사용자 지정 인증 스키마를 구현합니다.

    다음 예제에서는 프로덕션 환경에서 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 메서드를 재정의하는 코드를 사용하지 않습니다. 코드를 사용자 지정 사용자 이름 및 암호 유효성 검사 스키마로 바꿉니다. 이 스키마는 데이터베이스에서 사용자 이름과 암호 쌍을 검색합니다.

    인증 오류를 다시 클라이언트에 반환하려면 <xref:System.ServiceModel.FaultException> 메서드에서 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>을 throw합니다.

    [!code-csharp[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#4)]
    [!code-vb[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#4)]

### <a name="to-configure-a-service-to-use-a-custom-user-name-and-password-validator"></a>사용자 지정 사용자 이름 및 암호 유효성 검사기를 사용하도록 서비스를 구성하려면

1. HTTP(S)를 통해 전송 또는 전송 수준 보안에서 메시지 보안을 사용하는 바인딩을 구성합니다.

    메시지 보안을 사용 하는 경우 메시지 보안을 지 원하는 시스템 제공 바인딩 중 하나 (예: [\<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)또는 메시지 보안 및 `UserName` 자격 증명 형식을 지 원하는 [@no__t 3custombinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) )를 추가 합니다.

    HTTP (S)를 통해 전송 수준 보안을 사용 하는 경우 HTTP (S) 및을 사용 하는 @no__t ( [5netTcpBinding](../../configure-apps/file-schema/wcf/nettcpbinding.md) ) [또는 > (](../../configure-apps/file-schema/wcf/custombinding.md) @no__t)를 사용 하는 [\<Wshttpbinding >](../../configure-apps/file-schema/wcf/wshttpbinding.md) 또는 [\<basichttpbinding >](../../configure-apps/file-schema/wcf/basichttpbinding.md)를 추가 합니다. `Basic` 인증 체계입니다.

    > [!NOTE]
    > [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] 이상을 사용하는 경우 메시지 및 전송 보안과 함께 사용자 지정 사용자 이름 및 암호 유효성 검사기를 사용할 수 있습니다. WinFX를 사용 하면 사용자 지정 사용자 이름 및 암호 유효성 검사기를 메시지 보안과 함께 사용할 수 있습니다.

    > [!TIP]
    > 이 컨텍스트에서 \<netTcpBinding >를 사용 하는 방법에 대 한 자세한 내용은 [\<security >](../../configure-apps/file-schema/wcf/security-of-nettcpbinding.md)를 참조 하세요.

    1. 구성 파일의 [\<System >](../../configure-apps/file-schema/wcf/system-servicemodel.md) 요소 아래에서 [\<bindings >](../../configure-apps/file-schema/wcf/bindings.md) 요소를 추가 합니다.

    2. [@No__t-1wsHttpBinding >](../../configure-apps/file-schema/wcf/wshttpbinding.md) 또는 [\<basichttpbinding >](../../configure-apps/file-schema/wcf/basichttpbinding.md) 요소를 바인딩 섹션에 추가 합니다. WCF 바인딩 요소를 만드는 방법에 대 한 자세한 내용은 [How to: 구성](../how-to-specify-a-service-binding-in-configuration.md)에서 서비스 바인딩을 지정 합니다.

    3. [@No__t-2security >](../../configure-apps/file-schema/wcf/security-of-wshttpbinding.md) 의 `mode` 특성 또는 [\<security >](../../configure-apps/file-schema/wcf/security-of-basichttpbinding.md) 을 `Message`, `Transport` 또는 `TransportWithMessageCredential`로 설정 합니다.

    4. [@No__t-2 메시지 >](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) `clientCredentialType` 특성을 설정 하거나 [\<transport >](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md)를 설정 합니다.

        메시지 보안을 사용 하는 경우 [\< 메시지 >](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) `clientCredentialType` 특성을 `UserName`으로 설정 합니다.

        HTTP (S)를 통해 전송 수준 보안을 사용 하는 경우 [\<transport >](../../configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) 의 `clientCredentialType` 특성 또는 [\<transport >](../../configure-apps/file-schema/wcf/transport-of-basichttpbinding.md) 을 `Basic`로 설정 합니다.

        > [!NOTE]
        > WCF 서비스에서 인터넷 정보 서비스 (IIS) 전송 수준 보안을 사용 하 여 호스팅된 경우 및 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.UserNamePasswordValidationMode%2A> 속성이 <xref:System.ServiceModel.Security.UserNamePasswordValidationMode.Custom>, 사용자 지정 인증 체계는 Windows 인증의 하위 집합을 사용 합니다. 이것은 IIS이이 시나리오에서는 WCF 사용자 지정 인증자를 호출 하기 전에 Windows 인증을 수행 합니다.

    WCF 바인딩 요소를 만드는 방법에 대 한 자세한 내용은 [How to: 구성](../how-to-specify-a-service-binding-in-configuration.md)에서 서비스 바인딩을 지정 합니다.

    다음 예제는 바인딩에 대 한 구성 코드를 보여 줍니다.

    ```xml
    <system.serviceModel>
      <bindings>
      <wsHttpBinding>
          <binding name="Binding1">
            <security mode="Message">
              <message clientCredentialType="UserName" />
            </security>
          </binding>
        </wsHttpBinding>
      </bindings>
    </system.serviceModel>
    ```

2. 사용자 지정 사용자 이름 및 암호 유효성 검사기를 사용하여 들어오는 <xref:System.IdentityModel.Tokens.UserNameSecurityToken> 보안 토큰에 대한 사용자 이름과 암호 쌍의 유효성을 검사하도록 지정하는 동작을 구성합니다.

    1. [@No__t-1System >](../../configure-apps/file-schema/wcf/system-servicemodel.md) 요소에 대 한 자식으로 [\<behaviors >](../../configure-apps/file-schema/wcf/behaviors.md) 요소를 추가 합니다.

    2. [@No__t-1serviceBehaviors >](../../configure-apps/file-schema/wcf/servicebehaviors.md) [\<behaviors >](../../configure-apps/file-schema/wcf/behaviors.md) 요소에 추가 합니다.

    3. [@No__t-1behavior >](../../configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 요소를 추가 하 고 `name` 특성을 적절 한 값으로 설정 합니다.

    4. [@No__t-3behavior >](../../configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 요소에 [\<serviceCredentials >](../../configure-apps/file-schema/wcf/servicecredentials.md) 를 추가 합니다.

    5. [@No__t-3serviceCredentials >](../../configure-apps/file-schema/wcf/servicecredentials.md)에 [\<userNameAuthentication >](../../configure-apps/file-schema/wcf/usernameauthentication.md) 를 추가 합니다.

    6. `userNamePasswordValidationMode`를 `Custom`으로 설정합니다.

        > [!IMPORTANT]
        > @No__t-0 값을 설정 하지 않으면 WCF는 사용자 지정 사용자 이름 및 암호 유효성 검사기 대신 Windows 인증을 사용 합니다.

    7. `customUserNamePasswordValidatorType`을 사용자 지정 사용자 이름 및 암호 유효성 검사기를 나타내는 형식으로 설정합니다.

    다음 예제에서는이 시점에 `<serviceCredentials>` 조각을 보여 줍니다.

    ```xml
    <serviceCredentials>
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService.CustomUserNameValidator, service" />
    </serviceCredentials>
    ```

## <a name="example"></a>예제

다음 코드 예제에서는 사용자 지정 사용자 이름 및 암호 유효성 검사기를 만드는 방법을 보여 줍니다. 프로덕션 환경에서는 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 메서드를 재정의하는 코드를 사용하지 않습니다. 코드를 사용자 지정 사용자 이름 및 암호 유효성 검사 스키마로 바꿉니다. 이 스키마는 데이터베이스에서 사용자 이름과 암호 쌍을 검색합니다.

[!code-csharp[C_CustomUsernameAndPasswordValidator#1](~/samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#1)]
[!code-vb[C_CustomUsernameAndPasswordValidator#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#1)]
[!code-csharp[C_CustomUsernameAndPasswordValidator#2](~/samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#2)]
[!code-vb[C_CustomUsernameAndPasswordValidator#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#2)]

## <a name="see-also"></a>참조

- <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>
- [방법: ASP.NET 멤버 자격 공급자 @ no__t-0 사용
- [인증](authentication-in-wcf.md)
