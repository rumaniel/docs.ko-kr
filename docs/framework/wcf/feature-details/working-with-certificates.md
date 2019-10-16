---
title: 인증서 작업
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- certificates [WCF]
ms.assetid: 6ffb8682-8f07-4a45-afbb-8d2487e9dbc3
ms.openlocfilehash: bbe9341b1fb50985c235bd7f34961f1718f46bc0
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045220"
---
# <a name="working-with-certificates"></a>인증서 작업

WCF(Windows Communication Foundation) 보안을 프로그래밍하려면 일반적으로 X.509 디지털 인증서를 사용하여 클라이언트 및 서버를 인증하고, 암호화하고, 메시지에 디지털 서명합니다. 이 항목에서는 X.509 디지털 인증서 기능과 WCF에서 인증서 기능을 사용하는 방법을 간략하게 설명하며, 이러한 개념을 자세히 설명하거나 WCF 및 인증서를 사용하여 일반 작업을 수행하는 방법을 보여 주는 항목에 대한 링크를 제공합니다.

간단히 말해서 디지털 인증서는 공개 키 암호화 사용을 통해 전자 트랜잭션에 참여하는 각각의 상대방에 대해 유효성을 확인하고 인증하는 디지털 인증서, 인증 기관 및 기타 등록 기관의 시스템인 PKI(*공개 키 인프라*)의 일부입니다. 인증 기관은 인증서를 발급하며 각 인증서에는 *주체*(인증서가 발급되는 엔터티), 유효 날짜(인증서의 유효 기간), 발급자(인증서를 발급한 엔터티), 공개 키 등과 같은 데이터를 포함하는 필드 집합이 있습니다. WCF에서 이러한 각 속성은 <xref:System.IdentityModel.Claims.Claim>으로 처리되며, 각 클레임은 ID와 권한의 두 가지 형식으로 세분화됩니다. X.509 인증서에 대한 자세한 내용은[X.509 공개 키 인증서](/windows/desktop/SecCertEnroll/about-x-509-public-key-certificates)를 참조하세요. WCF에서 클레임 및 권한 부여에 대한 자세한 내용은 [ID 모델을 사용하여 클레임 및 권한 부여 관리](managing-claims-and-authorization-with-the-identity-model.md)를 참조하세요. PKI 구현에 대 한 자세한 내용은 [Windows Server 2012 R2 Active Directory 인증서 서비스를 사용 하는 엔터프라이즈 pki](https://blogs.technet.microsoft.com/yungchou/2013/10/21/enterprise-pki-with-windows-server-2012-r2-active-directory-certificate-services-part-1-of-2/)를 참조 하세요.

인증서의 기본 기능은 인증서 소유자의 ID를 다른 엔터티에 인증하는 것입니다. 인증서는 소유자의 *퍼블릭 키*를 포함하고, 소유자는 프라이빗 키를 보유합니다. 공개 키를 사용하여 인증서 소유자에게 보내는 메시지를 암호화할 수 있습니다. 소유자만 프라이빗 키에 액세스할 수 있으므로 소유자만이 해당 메시지를 해독할 수 있습니다.

인증서는 인증 기관에서 발급해야 합니다. 인증 기관이 인증서의 타사 발급자인 경우도 있습니다. Windows 도메인의 경우 도메인에서 컴퓨터에 인증서를 발급하는 데 사용할 수 있는 인증 기관이 포함되어 있습니다.

## <a name="viewing-certificates"></a>인증서 보기

인증서로 작업하려면 인증서를 표시하여 해당 속성을 검사해야 하는 경우가 종종 있습니다. 이 작업은 MMC(Microsoft Management Console) 스냅인 도구를 사용하여 쉽게 수행할 수 있습니다. 자세한 내용은 [방법: MMC 스냅인](how-to-view-certificates-with-the-mmc-snap-in.md)을 사용 하 여 인증서를 봅니다.

## <a name="certificate-stores"></a>인증서 저장소

인증서는 저장소에 있습니다. 하위 저장소로 세분화되는 두 가지 주 저장소 위치가 있습니다. 컴퓨터의 관리자는 MMC 스냅인 도구를 사용하여 두 주 저장소를 모두 볼 수 있습니다. 관리자가 아닌 사용자는 현재 사용자 저장소만 볼 수 있습니다.

- **로컬 컴퓨터 저장소**. 여기에는 ASP.NET과 같은 컴퓨터 프로세스에서 액세스 하는 인증서가 포함 됩니다. 클라이언트에 서버를 인증하는 인증서를 저장하려면 이 위치를 사용합니다.

- **현재 사용자 저장소**. 대화형 응용 프로그램은 일반적으로 컴퓨터의 현재 사용자에 대한 인증서를 여기에 저장합니다. 클라이언트 응용 프로그램을 만들 경우 일반적으로 서비스에 사용자를 인증하는 인증서를 이 위치에 저장합니다.

이러한 두 저장소는 하위 저장소로 세분화됩니다. WCF로 프로그래밍할 때 가장 중요한 하위 저장소는 다음과 같습니다.

- **신뢰할 수 있는 루트 인증 기관**. 이 저장소에 있는 인증서를 사용하여 인증서 체인을 만들 수 있습니다. 이러한 인증서 체인은 이 저장소에 있는 인증서 인증 기관으로 다시 추적될 수 있습니다.

  > [!IMPORTANT]
  > 로컬 컴퓨터는 인증서를 신뢰할 수 있는 타사 인증 기관에서 가져오지 않았더라도 이 저장소에 있는 모든 인증서를 암시적으로 신뢰합니다. 따라서 발급자를 완전히 신뢰하고 결과를 이해하는 경우가 아니면 이 저장소에 인증서를 저장하지 마십시오.

- **개인**. 이 저장소는 컴퓨터 사용과 연관된 인증서에 사용됩니다. 일반적으로 이 저장소는 신뢰할 수 있는 루트 인증 기관 저장소에 있는 인증 기관 인증서 중 하나에서 발급한 인증서에 사용됩니다. 또한 여기에 있는 인증서는 응용 프로그램에서 자체 발급하고 신뢰할 수 있습니다.

인증서 저장소에 대한 자세한 내용은 [인증서 저장소](/windows/desktop/secauthn/certificate-stores)를 참조하세요.

### <a name="selecting-a-store"></a>저장소 선택

인증서를 저장할 위치는 서비스 또는 클라이언트가 실행되는 방법과 시기에 따라 달라집니다. 다음과 같은 일반 규칙이 적용됩니다.

- WCF 서비스가 Windows 서비스에 호스팅된 경우 **로컬 컴퓨터** 저장소를 사용합니다. 인증서를 로컬 컴퓨터 저장소에 설치하려면 관리자 권한이 필요합니다.

- 서비스 또는 클라이언트가 사용자 계정에서 실행되는 애플리케이션인 경우 **현재 사용자** 저장소를 사용합니다.

### <a name="accessing-stores"></a>저장소 액세스

저장소는 컴퓨터에 있는 폴더처럼 ACL(액세스 제어 목록)에 의해 보호됩니다. 인터넷 정보 서비스 (IIS)에서 호스팅하는 서비스를 만들 때 ASP.NET 계정으로 ASP.NET 프로세스가 실행 됩니다. 이 계정은 서비스에 사용되는 인증서가 들어 있는 저장소에 대한 액세스 권한이 있어야 합니다. 각각의 주 저장소는 기본 액세스 목록으로 보호되지만, 목록을 수정할 수 있습니다. 저장소 액세스를 위한 개별 역할을 만들 경우 해당 역할에 액세스 권한을 부여해야 합니다. Winhttpcertconfig.exe 도구를 사용 하 여 액세스 목록을 수정 하는 방법에 대 한 자세한 [내용은 방법: 개발](how-to-create-temporary-certificates-for-use-during-development.md)하는 동안 사용할 임시 인증서를 만듭니다. IIS에서 클라이언트 인증서 사용에 대한 자세한 내용은 [ASP.NET 웹 애플리케이션에서 인증을 위해 클라이언트 인증서를 사용하여 웹 서비스를 호출하는 방법](https://support.microsoft.com/en-us/help/901183/how-to-call-a-web-service-by-using-a-client-certificate-for-authentica)을 참조하세요.

## <a name="chain-trust-and-certificate-authorities"></a>신뢰 체인 및 인증 기관

인증서는 개별 인증서가 인증서를 발급한 CA에 연결되는 계층 구조에 만들어집니다. 이 링크는 CA의 인증서로 연결됩니다. 그런 다음 CA의 인증서가 원래 CA의 인증서를 발급 한 CA에 연결 됩니다. 이 프로세스는 루트 CA의 인증서에 도달할 때까지 반복됩니다. 루트 CA의 인증서는 본질적으로 신뢰할 수 있는 인증서입니다.

디지털 인증서는 *신뢰 체인*이라고도 하는 이 계층 구조를 사용하여 엔터티를 인증하는 데 사용됩니다. 인증서를 두 번 클릭한 다음 **인증서 경로** 탭을 클릭하여 MMC 스냅인을 통해 인증서의 체인을 볼 수 있습니다. 인증 기관에 대 한 인증서 체인을 [가져오는 방법에 대 한 자세한 내용은 방법: 서명을](specify-the-certificate-authority-chain-verify-signatures-wcf.md)확인 하는 데 사용 되는 인증 기관 인증서 체인을 지정 합니다.

> [!NOTE]
> 신뢰할 수 있는 루트 기관 인증서 저장소에 발급자의 인증서를 넣어 발급자를 신뢰할 수 있는 루트 기관으로 지정할 수 있습니다.

### <a name="disabling-chain-trust"></a>신뢰 체인을 사용하지 않도록 설정

새 서비스를 만들 때 신뢰할 수 있는 루트 인증서를 통해 발급되지 않은 인증서를 사용하거나 발급하는 인증서 자체가 신뢰할 수 있는 루트 인증 기관 저장소에 없을 수도 있습니다. 개발 용도로만 인증서에 대한 신뢰 체인을 검사하는 메커니즘을 일시적으로 사용하지 않도록 설정할 수 있습니다. 이 작업을 수행하려면 `CertificateValidationMode` 속성을 `PeerTrust` 또는 `PeerOrChainTrust`로 설정합니다. 두 모드는 인증서가 자체 발급되거나(신뢰 피어) 신뢰 체인의 일부일 수 있음을 지정합니다. 다음 클래스에 대한 속성을 설정할 수 있습니다.

|클래스|속성|
|-----------|--------------|
|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A?displayProperty=nameWithType>|
|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication.CertificateValidationMode%2A?displayProperty=nameWithType>|
|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A?displayProperty=nameWithType>|
|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential>|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A?displayProperty=nameWithType>|

구성을 사용하여 속성을 설정할 수도 있습니다. 유효성 검사 모드를 지정하는 데 사용되는 요소는 다음과 같습니다.

- [\<authentication>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)

- [\<peerAuthentication>](../../../../docs/framework/configure-apps/file-schema/wcf/peerauthentication-element.md)

- [\<messageSenderAuthentication>](../../../../docs/framework/configure-apps/file-schema/wcf/messagesenderauthentication-element.md)

## <a name="custom-authentication"></a>사용자 지정 인증

`CertificateValidationMode` 속성을 사용하여 인증서가 인증되는 방법을 사용자 지정할 수도 있습니다. 기본적으로 수준은 `ChainTrust`로 설정됩니다. <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom> 값을 사용하려면 `CustomCertificateValidatorType` 특성을 인증서의 유효성을 검사하는 데 사용된 어셈블리 및 형식으로 설정해야 합니다. 사용자 지정 유효성 검사기를 만들려면 추상 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 클래스에서 상속해야 합니다.

사용자 지정 인증자를 만들 때 재정의할 가장 중요한 메서드는 <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A> 메서드입니다. 사용자 지정 인증에 대한 예제는 [X.509 인증서 유효성 검사기](../../../../docs/framework/wcf/samples/x-509-certificate-validator.md) 샘플을 참조하세요. 자세한 내용은 [사용자 지정 자격 증명 및 자격 증명 유효성 검사](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md)를 참조하세요.

## <a name="using-the-powershell-new-selfsignedcertificate-cmdlet-to-build-a-certificate-chain"></a>PowerShell New-selfsignedcertificate Cmdlet을 사용 하 여 인증서 체인 빌드

PowerShell New-selfsignedcertificate cmdlet은 x.509 인증서와 개인 키/공개 키 쌍을 만듭니다. 프라이빗 키를 디스크에 저장한 다음 새 인증서를 발급하고 서명하여 체인 인증서의 계층 구조를 시뮬레이션할 수 있습니다. Cmdlet은 서비스를 개발 하는 데 도움을 주기 위한 것 이며 실제 배포에 대 한 인증서를 만드는 데 사용 하면 안 됩니다. WCF 서비스를 개발 하는 경우 다음 단계를 사용 하 여 New-selfsignedcertificate cmdlet을 사용 하 여 신뢰 체인을 만듭니다.

#### <a name="to-build-a-chain-of-trust-with-the-new-selfsignedcertificate-cmdlet"></a>New-selfsignedcertificate cmdlet을 사용 하 여 신뢰 체인을 빌드하려면

1. New-selfsignedcertificate cmdlet을 사용 하 여 임시 루트 인증 기관 (자체 서명) 인증서를 만듭니다. 프라이빗 키를 디스크에 저장합니다.

2. 새 인증서를 사용하여 공개 키가 들어 있는 다른 인증서를 발급합니다.

3. 루트 기관 인증서를 신뢰할 수 있는 루트 인증 기관 저장소로 가져옵니다.

4. 단계별 지침에 대 한 자세한 내용은 [방법: 개발](how-to-create-temporary-certificates-for-use-during-development.md)하는 동안 사용할 임시 인증서를 만듭니다.

## <a name="which-certificate-to-use"></a>사용할 인증서

인증서에 대한 일반적인 질문은 사용할 인증서와 그 이유에 대한 것입니다. 대답은 클라이언트를 프로그래밍하는지 서비스를 프로그래밍하는지에 따라 달라집니다. 다음 정보에서는 일반적인 지침을 제공하며 이러한 질문에 대한 세부적인 대답은 아닙니다.

### <a name="service-certificates"></a>서비스 인증서

서비스 인증서의 주요 작업은 클라이언트에 서버를 인증하는 것입니다. 클라이언트에서 서버를 인증할 때 초기 검사 중 하나는 **주체** 필드의 값을 서비스를 연결하는 데 사용된 URI(Uniform Resource Identifier)와 비교하는 것입니다. 두 항목의 DNS가 일치해야 합니다. 예를 들어 서비스의 URI가 이면 **제목** 필드 `http://www.contoso.com/endpoint/` 에도 값 `www.contoso.com`이 포함 되어야 합니다.

필드는 값을 나타내는 이니셜 접두사가 붙은 여러 값을 포함할 수 있습니다. 가장 일반적으로 초기화는 일반적인 이름에 대 한 "CN"입니다 (예 `CN = www.contoso.com`:). **주체** 필드를 비워둘 수도 있습니다. 이 경우 **주체 대체 이름** 필드는 **DNS 이름** 값을 포함할 수 있습니다.

또한 인증서의 **용도** 필드 값은 “서버 인증” 또는 “클라이언트 인증”과 같은 적절한 값을 포함해야 합니다.

### <a name="client-certificates"></a>클라이언트 인증서

클라이언트 인증서는 일반적으로 타사 인증 기관에 의해 발급되지 않습니다. 대신 일반적으로 현재 사용자 위치의 개인 저장소에서 용도가 "클라이언트 인증"이고 루트 기관에서 넣은 인증서를 포함합니다. 클라이언트는 상호 인증이 필요할 때 이러한 인증서를 사용할 수 있습니다.

## <a name="online-revocation-and-offline-revocation"></a>온라인 해지 및 오프라인 해지

### <a name="certificate-validity"></a>인증서 유효성

모든 인증서는 *유효 기간*이라고 하는 지정된 기간 동안에만 유효합니다. 유효 기간은 X.509 인증서의 **유효 기간(시작)** 및 **유효 기간(끝)** 필드에 의해 정의됩니다. 인증 중에 인증서를 검사하여 인증서가 유효 기간 내에 있는지 여부를 확인합니다.

### <a name="certificate-revocation-list"></a>인증서 해지 목록

인증 기관은 유효 기간 중에 언제든지 인증서를 해지할 수 있습니다. 인증서의 프라이빗 키 손상 등과 같은 다양한 이유로 인증서를 해지할 수 있습니다.

인증서를 해지하면 해지된 인증서 아래의 모든 체인도 유효하지 않으므로 인증 절차 중에 신뢰되지 않습니다. 해지되는 인증서를 확인하기 위해 각 발급자는 타임스탬프 및 날짜 스탬프가 기록된 CRL(*인증서 해지 목록*)을 게시합니다. 이 목록은 `RevocationMode`, `DefaultRevocationMode`, <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 및 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 클래스의 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication> 또는 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> 속성을 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> 열거형 값 중 하나로 설정하여 온라인 해지 또는 오프라인 해지를 통해 확인할 수 있습니다. 모든 속성의 기본값은 `Online`입니다.

[\<authentication>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)([\<serviceBehaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)의) 및 [\<authentication>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)([\<endpointBehaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)의)의 `revocationMode` 특성을 사용하여 구성에서 모드를 설정할 수도 있습니다.

## <a name="the-setcertificate-method"></a>SetCertificate 메서드

WCF에서는 서비스 또는 클라이언트에서 메시지를 인증, 암호화 또는 디지털 서명하는 데 사용할 인증서 또는 인증서 집합을 지정해야 할 수 있습니다. 이 작업은 X.509 인증서를 나타내는 다양한 클래스의 `SetCertificate` 메서드를 사용하여 프로그래밍 방식으로 수행할 수 있습니다. 다음 클래스에서는 `SetCertificate` 메서드를 사용하여 인증서를 지정합니다.

|클래스|메서드|
|-----------|------------|
|<xref:System.ServiceModel.Security.PeerCredential>|<xref:System.ServiceModel.Security.PeerCredential.SetCertificate%2A>|
|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>|
|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>|
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential>|
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A>|

`SetCertificate` 메서드는 저장소 위치 및 저장소, 인증서의 필드와 필드에서 찾을 값을 지정하는 "찾기" 형식(`x509FindType` 매개 변수)을 지정하여 작동합니다. 예를 들어, 다음 코드에서는 <xref:System.ServiceModel.ServiceHost> 인스턴스를 만들고 `SetCertificate` 메서드를 사용하여 클라이언트에 서비스를 인증하는 데 사용되는 서비스 인증서를 설정합니다.

[!code-csharp[c_WorkingWithCertificates#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_workingwithcertificates/cs/source.cs#1)]
[!code-vb[c_WorkingWithCertificates#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_workingwithcertificates/vb/source.vb#1)]

### <a name="multiple-certificates-with-the-same-value"></a>동일한 값을 가진 여러 인증서

저장소에 동일한 주체 이름을 가진 여러 인증서가 들어 있을 수 있습니다. 즉, `x509FindType`을 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectName> 또는 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectDistinguishedName>으로 지정한 경우 동일한 값을 가진 여러 인증서가 있으면 필요한 인증서를 구별할 수 없으므로 예외가 throw됩니다. `x509FindType`을 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint>로 설정하여 이 문제를 완화할 수 있습니다. 지문 필드에는 저장소에서 특정 인증서를 찾는 데 사용할 수 있는 고유한 값이 포함되어 있습니다. 그러나 인증서를 해지하거나 갱신하면 지문도 제거되므로 `SetCertificate` 메서드가 실패한다는 단점이 있습니다. 또는 인증서가 더 이상 유효하지 않을 경우 인증에 실패합니다. 이 문제를 줄이려면 `x590FindType` 매개 변수를 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByIssuerName>으로 설정하고 발급자의 이름을 지정합니다. 특정 발급자가 필요하지 않은 경우 다른 <xref:System.Security.Cryptography.X509Certificates.X509FindType> 열거형 값 중 하나(예: <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByTimeValid>)를 설정할 수도 있습니다.

## <a name="certificates-in-configuration"></a>구성의 인증서

구성을 사용하여 인증서를 설정할 수도 있습니다. 서비스를 만들 경우 인증서를 포함한 자격 증명이 [\<serviceBehaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)에서 지정됩니다. 클라이언트를 프로그래밍할 경우 인증서가 [\<endpointBehaviors>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)에서 지정됩니다.

## <a name="mapping-a-certificate-to-a-user-account"></a>사용자 계정에 인증서 매핑

IIS 및 Active Directory에는 Windows 사용자 계정에 인증서를 매핑하는 기능이 있습니다. 기능에 대한 자세한 내용은 [사용자 계정에 인증서 매핑](https://go.microsoft.com/fwlink/?LinkId=88917)을 참조하세요.

Active Directory 매핑 사용에 대한 자세한 내용은 [디렉터리 서비스 매핑을 사용하여 클라이언트 인증서 매핑](https://go.microsoft.com/fwlink/?LinkId=88918)을 참조하세요.

이 기능을 사용하여 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.MapClientCertificateToWindowsAccount%2A> 클래스의 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 속성을 `true`로 설정할 수 있습니다. 다음 코드에 표시된 것처럼 구성에서 [\<authentication>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) 요소의 `mapClientCertificateToWindowsAccount` 특성을 `true`로 설정할 수 있습니다.

```xml
<serviceBehaviors>
 <behavior name="MappingBehavior">
  <serviceCredentials>
   <clientCertificate>
    <authentication certificateValidationMode="None" mapClientCertificateToWindowsAccount="true" />
   </clientCertificate>
  </serviceCredentials>
 </behavior>
</serviceBehaviors>
```

Windows 사용자 계정을 나타내는 토큰에 X.509 인증서를 매핑하면 매핑된 Windows 토큰을 사용하여 보호된 리소스에 액세스할 수 있기 때문에 권한 상승으로 간주됩니다. 따라서 도메인 정책에서는 매핑 전에 X.509 인증서가 해당 정책을 준수하도록 요구합니다. *SChannel* 보안 패키지는 이러한 요구 사항을 적용합니다.

[!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] 이상을 사용하는 경우 WCF는 인증서를 Windows 계정에 매핑하기 전에 해당 인증서가 도메인 정책을 준수하는지 확인합니다.

WCF의 첫 번째 릴리스에서는 도메인 정책을 참조하지 않고 매핑을 수행했습니다. 따라서 매핑을 실행할 때 X.509 인증서가 도메인 정책에 맞지 않을 경우 첫 번째 릴리스에서 작동했던 이전 응용 프로그램이 실패할 수 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels>
- <xref:System.ServiceModel.Security>
- <xref:System.ServiceModel>
- <xref:System.Security.Cryptography.X509Certificates.X509FindType>
- [서비스 및 클라이언트에 보안 설정](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
