---
title: '연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2b5ba5c3-0c6c-48e9-9e46-54acaec443ba
ms.openlocfilehash: d49df909521b3b5e5cf509c1367821856e91e30b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795477"
---
# <a name="walkthrough-creating-custom-client-and-service-credentials"></a>연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기

이 항목에서는 사용자 지정 클라이언트와 서비스 자격 증명을 구현하는 방법 및 애플리케이션 코드로부터 사용자 지정 자격 증명을 사용하는 방법을 보여 줍니다.

## <a name="credentials-extensibility-classes"></a>자격 증명 확장성 클래스

<xref:System.ServiceModel.Description.ClientCredentials> 및<xref:System.ServiceModel.Description.ServiceCredentials> 클래스는 WCF (Windows Communication Foundation) 보안 확장성에 대 한 주 진입점입니다. 이러한 자격 증명 클래스는 API를 제공합니다. 이 API를 통해 애플리케이션 코드에서는 자격 증명 정보를 설정하고, 자격 증명 형식을 보안 토큰으로 변환할 수 있습니다. (*보안 토큰* 은 SOAP 메시지 내부에서 자격 증명 정보를 전송 하는 데 사용 되는 양식입니다.) 이러한 자격 증명 클래스의 책임은 다음과 같은 두 가지 영역으로 나눠 볼 수 있습니다.

- 애플리케이션에서 자격 증명 정보를 설정하도록 API 제공

- <xref:System.IdentityModel.Selectors.SecurityTokenManager> 구현을 위한 팩터리 역할 수행

WCF에서 제공 하는 기본 구현에서는 시스템이 제공 하는 자격 증명 형식을 지원 하 고 이러한 자격 증명 형식을 처리할 수 있는 보안 토큰 관리자를 만듭니다.

## <a name="reasons-to-customize"></a>사용자 지정해야 하는 이유

클라이언트 또는 서비스 자격 증명 클래스를 사용자 지정해야 하는 이유는 여러 가지가 있습니다. 가장 중요 한 것은 시스템 제공 자격 증명 형식의 처리와 관련 하 여 기본 WCF 보안 동작을 변경 해야 하는 요구 사항입니다. 특히 다음과 같은 이유 때문일 수 있습니다.

- 다른 확장성 지점을 사용하여 변경할 수 없는 내용을 변경해야 합니다.

- 새 자격 증명 형식을 추가해야 합니다.

- 새 사용자 지정 보안 토큰 형식을 추가해야 합니다.

이 항목에서는 사용자 지정 클라이언트와 서비스 자격 증명을 구현하는 방법 및 애플리케이션 코드로부터 이들을 사용하는 방법에 대해 설명합니다.

## <a name="first-in-a-series"></a>시리즈의 첫 번째 단계

자격 증명을 사용자 지정 하는 이유는 자격 증명 프로 비전, 보안 토큰 serialization 또는 인증과 관련 된 WCF 동작을 변경 하기 때문에 사용자 지정 자격 증명 클래스를 만드는 것은 첫 번째 단계입니다. 이 단원의 다른 항목에서는 사용자 지정 serializer 및 인증자를 만드는 방법에 대해 설명합니다. 이와 관련하여 사용자 지정 자격 증명 클래스를 만드는 것이 이 시리즈의 첫 번째 항목입니다. 후속 작업(사용자 지정 serializer 및 인증자 만들기)은 사용자 지정 자격 증명을 만든 이후에야 수행할 수 있습니다. 이 항목을 기초로 한 추가 항목은 다음과 같습니다.

- [방법: 사용자 지정 보안 토큰 공급자 만들기](how-to-create-a-custom-security-token-provider.md)

- [방법: 사용자 지정 보안 토큰 인증자 만들기](how-to-create-a-custom-security-token-authenticator.md)

- [방법: 사용자 지정 토큰](how-to-create-a-custom-token.md)을 만듭니다.

## <a name="procedures"></a>절차

#### <a name="to-implement-custom-client-credentials"></a>사용자 지정 클라이언트 자격 증명을 구현하려면

1. <xref:System.ServiceModel.Description.ClientCredentials> 클래스에서 파생된 새 클래스를 정의합니다.

2. 선택 사항입니다. 새 자격 증명 형식에 대해 새 메서드 또는 속성을 추가합니다. 새 자격 증명 형식을 추가하지 않으려면 이 단계를 건너뜁니다. 다음 예제에서는 `CreditCardNumber` 속성을 추가합니다.

3. <xref:System.ServiceModel.Security.SecurityCredentialsManager.CreateSecurityTokenManager%2A> 메서드를 재정의합니다. 이 메서드는 사용자 지정 클라이언트 자격 증명을 사용 하는 경우 WCF 보안 인프라에서 자동으로 호출 됩니다. 이 메서드는 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 클래스 구현의 인스턴스를 만들고 반환합니다.

    > [!IMPORTANT]
    > <xref:System.ServiceModel.Security.SecurityCredentialsManager.CreateSecurityTokenManager%2A> 메서드를 재정의하여 사용자 지정 보안 토큰 관리자를 만든다는 점이 중요합니다. <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>에서 파생된 보안 토큰 관리자는 <xref:System.IdentityModel.Selectors.SecurityTokenProvider>에서 파생된 사용자 지정 보안 토큰 공급자를 반환하여 실제 보안 토큰을 만들어야 합니다. 보안 토큰을 만들 때 이 방식을 따르지 않으면 <xref:System.ServiceModel.ChannelFactory> 개체를 캐시할 때(WCF 클라이언트 프록시의 기본 동작임) 애플리케이션의 기능이 제대로 수행되지 않아 권한 상승 공격이 발생할 수 있습니다. 사용자 지정 자격 증명 개체는 <xref:System.ServiceModel.ChannelFactory>의 일부분으로 캐시됩니다. 그러나 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager>는 호출할 때마다 만들어지므로 토큰 생성 논리가 <xref:System.IdentityModel.Selectors.SecurityTokenManager>에 있는 한 보안 위협은 완화됩니다.

4. <xref:System.ServiceModel.Description.ClientCredentials.CloneCore%2A> 메서드를 재정의합니다.

    [!code-csharp[c_CustomCredentials#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#1)]
    [!code-vb[c_CustomCredentials#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/client/client.vb#1)]

#### <a name="to-implement-a-custom-client-security-token-manager"></a>사용자 지정 클라이언트 보안 토큰 관리자를 구현하려면

1. <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>에서 파생된 새 클래스를 정의합니다.

2. 선택 사항입니다. 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> 구현을 만들어야 하는 경우 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 메서드를 재정의합니다. 사용자 지정 보안 토큰 공급자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 공급자](how-to-create-a-custom-security-token-provider.md)를 만듭니다.

3. 선택 사항입니다. 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%28System.IdentityModel.Selectors.SecurityTokenRequirement%2CSystem.IdentityModel.Selectors.SecurityTokenResolver%40%29> 구현을 만들어야 하는 경우 <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> 메서드를 재정의합니다. 사용자 지정 보안 토큰 인증자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 인증자](how-to-create-a-custom-security-token-authenticator.md)를 만듭니다.

4. 선택 사항입니다. 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenSerializer%2A>를 만들어야 하는 경우 <xref:System.IdentityModel.Selectors.SecurityTokenSerializer> 메서드를 재정의합니다. 사용자 지정 보안 토큰 및 사용자 지정 보안 토큰 serializer [에 대 한 자세한 내용은 방법: 사용자 지정 토큰](how-to-create-a-custom-token.md)을 만듭니다.

    [!code-csharp[c_CustomCredentials#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#2)]
    [!code-vb[c_CustomCredentials#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/client/client.vb#2)]

#### <a name="to-use-a-custom-client-credentials-from-application-code"></a>애플리케이션 코드로부터 사용자 지정 클라이언트 자격 증명을 사용하려면

1. 서비스 인터페이스를 나타내는 생성된 클라이언트의 인스턴스를 만들거나 사용자가 통신하려고 하는 서비스를 가리키는 <xref:System.ServiceModel.ChannelFactory>의 인스턴스를 만듭니다.

2. <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> 속성을 통해 액세스할 수 있는 <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> 컬렉션으로부터 시스템 제공 클라이언트 자격 증명 동작을 제거합니다.

3. 사용자 지정 클라이언트 자격 증명 클래스의 새 인스턴스를 만들고 이 인스턴스를 <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> 속성을 통해 액세스할 수 있는 <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> 컬렉션에 추가합니다.

    [!code-csharp[c_CustomCredentials#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#3)]
    [!code-vb[c_CustomCredentials#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/client/client.vb#3)]

이전 절차는 애플리케이션 코드에서 클라이언트 자격 증명을 사용하는 방법을 보여 줍니다. 응용 프로그램 구성 파일을 사용 하 여 WCF 자격 증명을 구성할 수도 있습니다. 소스를 수정하고, 다시 컴파일하고, 다시 배포하지 않고도 애플리케이션 매개 변수를 수정할 수 있기 때문에 종종 애플리케이션 구성을 사용하는 것이 하드 코딩보다 좋습니다.

다음 절차에서는 사용자 지정 자격 증명을 구성하기 위해 지원을 제공하는 방법에 대해 설명합니다.

#### <a name="creating-a-configuration-handler-for-custom-client-credentials"></a>사용자 지정 클라이언트 자격 증명에 대한 구성 처리기 만들기

1. <xref:System.ServiceModel.Configuration.ClientCredentialsElement>에서 파생된 새 클래스를 정의합니다.

2. 선택 사항입니다. 애플리케이션 구성을 통해 노출하려고 하는 모든 추가 구성 매개 변수에 대한 속성을 추가합니다. 아래 예제에서는 이름이 `CreditCardNumber`인 속성 하나를 추가합니다.

3. 구성 요소를 사용하여 만들어진 사용자 지정 클라이언트 자격 증명 클래스의 형식을 반환하려면 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement.BehaviorType%2A> 속성을 재정의합니다.

4. <xref:System.ServiceModel.Configuration.BehaviorExtensionElement.CreateBehavior%2A> 메서드를 재정의합니다. 이 메서드는 구성 파일로부터 로드된 설정을 기반으로 사용자 지정 자격 증명 클래스의 인스턴스를 만들고 반환합니다. 사용자 지정 클라이언트 자격 증명 인스턴스로 로드된 시스템 제공 자격 증명 설정을 검색하려면 이 메서드로부터 기본 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ApplyConfiguration%28System.ServiceModel.Description.ClientCredentials%29> 메서드를 호출합니다.

5. 선택 사항입니다. 2단계에서 속성을 추가한 경우 구성 프레임워크에 대한 추가 구성 설정을 등록하여 이를 인식할 수 있도록 하려면 <xref:System.Configuration.ConfigurationElement.Properties%2A> 속성을 재정의해야 합니다. 사용자의 속성과 기본 클래스 속성을 조합하면 이 사용자 지정 클라이언트 자격 증명 구성 요소를 통해 시스템 제공 설정을 구성할 수 있습니다.

    [!code-csharp[c_CustomCredentials#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#7)]
    [!code-vb[c_CustomCredentials#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#7)]

구성 처리기 클래스가 있으면 WCF 구성 프레임 워크에 통합 될 수 있습니다. 이를 통해 다음 절차에서처럼 사용자 지정 클라이언트 자격 증명을 클라이언트 엔드포인트 동작 요소에서 사용할 수 있습니다.

#### <a name="to-register-and-use-a-custom-client-credentials-configuration-handler-in-the-application-configuration"></a>애플리케이션 구성에서 사용자 지정 클라이언트 자격 증명 구성 처리기를 등록 및 사용하려면

1. <`extensions`> 요소와 <`behaviorExtensions`> 요소를 구성 파일에 추가 합니다.

2. <`add``behaviorExtensions` >요소에<>요소를추가하고특성을적절한값`name` 으로 설정 합니다.

3. `type` 특성을 정규화된 형식 이름으로 설정합니다. 또한 어셈블리 이름과 기타 어셈블리 특성을 포함시킵니다.

    ```xml
    <system.serviceModel>
      <extensions>
        <behaviorExtensions>
          <add name="myClientCredentials" type="Microsoft.ServiceModel.Samples.MyClientCredentialsConfigHandler, CustomCredentials, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
        </behaviorExtensions>
      </extensions>
    <system.serviceModel>
    ```

4. 구성 처리기를 등록 한 후에는 시스템에서 제공 하는 <`clientCredentials`> 요소가 아닌 동일한 구성 파일 내에서 사용자 지정 자격 증명 요소를 사용할 수 있습니다. 시스템 제공 속성 및 구성 처리기 구현에 추가한 새 속성을 모두 사용할 수 있습니다. 다음 예제에서는 `creditCardNumber` 특성을 사용하여 사용자 지정 속성의 값을 설정합니다.

    ```xml
    <behaviors>
      <endpointBehaviors>
        <behavior name="myClientCredentialsBehavior">
          <myClientCredentials creditCardNumber="123-123-123"/>
        </behavior>
      </endpointBehaviors>
    </behaviors>
    ```

#### <a name="to-implement-custom-service-credentials"></a>사용자 지정 서비스 자격 증명을 구현하려면

1. <xref:System.ServiceModel.Description.ServiceCredentials>에서 파생된 새 클래스를 정의합니다.

2. 선택 사항입니다. 추가 중인 새 자격 증명 값에 대한 API를 제공하려면 새 속성을 추가합니다. 새 자격 증명 값을 추가하지 않으려면 이 단계를 건너뜁니다. 다음 예제에서는 `AdditionalCertificate` 속성을 추가합니다.

3. <xref:System.ServiceModel.Security.SecurityCredentialsManager.CreateSecurityTokenManager%2A> 메서드를 재정의합니다. 사용자 지정 클라이언트 자격 증명을 사용 하는 경우이 메서드는 WCF 인프라에서 자동으로 호출 됩니다. 이 메서드는 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 클래스 구현의 인스턴스를 만들고 반환하며, 이에 대해서는 다음 절차에서 설명합니다.

4. 선택 사항입니다. <xref:System.ServiceModel.Description.ServiceCredentials.CloneCore%2A> 메서드를 재정의합니다. 이는 새 속성 또는 내부 필드를 사용자 지정 클라이언트 자격 증명 구현에 추가하는 경우에만 필요합니다.

    [!code-csharp[c_CustomCredentials#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#4)]
    [!code-vb[c_CustomCredentials#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#4)]

#### <a name="to-implement-a-custom-service-security-token-manager"></a>사용자 지정 서비스 보안 토큰 관리자를 구현하려면

1. <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> 클래스에서 파생된 새 클래스를 정의합니다.

2. 선택 사항입니다. 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%2A> 구현을 만들어야 하는 경우 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 메서드를 재정의합니다. 사용자 지정 보안 토큰 공급자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 공급자](how-to-create-a-custom-security-token-provider.md)를 만듭니다.

3. 선택 사항입니다. 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A> 구현을 만들어야 하는 경우 <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> 메서드를 재정의합니다. 사용자 지정 보안 토큰 인증자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 인증자](how-to-create-a-custom-security-token-authenticator.md) 항목을 만듭니다.

4. 선택 사항입니다. 사용자 지정 <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenSerializer%28System.IdentityModel.Selectors.SecurityTokenVersion%29>를 만들어야 하는 경우 <xref:System.IdentityModel.Selectors.SecurityTokenSerializer> 메서드를 재정의합니다. 사용자 지정 보안 토큰 및 사용자 지정 보안 토큰 serializer [에 대 한 자세한 내용은 방법: 사용자 지정 토큰](how-to-create-a-custom-token.md)을 만듭니다.

    [!code-csharp[c_CustomCredentials#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#5)]
    [!code-vb[c_CustomCredentials#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#5)]

#### <a name="to-use-custom-service-credentials-from-application-code"></a>애플리케이션 코드로부터 사용자 지정 서비스 자격 증명을 사용하려면

1. <xref:System.ServiceModel.ServiceHost>의 인스턴스를 만듭니다.

2. <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 컬렉션으로부터 시스템 제공 서비스 자격 증명 동작을 제거합니다.

3. 사용자 지정 서비스 자격 증명 클래스의 새 인스턴스를 만들고 이 인스턴스를 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 컬렉션에 추가합니다.

    [!code-csharp[c_CustomCredentials#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#6)]
    [!code-vb[c_CustomCredentials#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#6)]

위의 "`To create a configuration handler for custom client credentials`" 및 "`To register and use a custom client credentials configuration handler in the application configuration`" 절차에서 설명된 단계를 사용하여 구성에 대한 지원을 추가합니다. 유일한 차이점은 구성 처리기에 대한 기본 클래스로 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement> 클래스 대신에 <xref:System.ServiceModel.Configuration.ClientCredentialsElement> 클래스를 사용하는 것입니다. 그런 다음 사용자 지정 서비스 자격 증명 요소는 시스템 제공 `<serviceCredentials>` 요소가 사용될 때 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.Security.SecurityCredentialsManager>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement>
- [방법: 사용자 지정 보안 토큰 공급자 만들기](how-to-create-a-custom-security-token-provider.md)
- [방법: 사용자 지정 보안 토큰 인증자 만들기](how-to-create-a-custom-security-token-authenticator.md)
- [방법: 사용자 지정 토큰 만들기](how-to-create-a-custom-token.md)
