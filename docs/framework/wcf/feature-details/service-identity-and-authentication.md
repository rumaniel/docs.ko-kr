---
title: 서비스 ID 및 인증
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- authentication [WCF], specifying the identity of a service
ms.assetid: a4c8f52c-5b30-45c4-a545-63244aba82be
ms.openlocfilehash: f9ed2a7c284588a0fb481d41dca61e663fd090b1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969241"
---
# <a name="service-identity-and-authentication"></a>서비스 ID 및 인증
서비스의 *끝점 id* 는 서비스 WSDL (웹 서비스 기술 언어)에서 생성 된 값입니다. 모든 클라이언트에 전파되는 이 값은 서비스를 인증하는 데 사용합니다. 클라이언트가 엔드포인트에 대한 통신을 시작하고 서비스가 클라이언트에 대해 인증되면 클라이언트는 엔드포인트 ID 값과 엔드포인트 인증 프로세스에서 반환된 실제 값을 비교합니다. 두 값이 일치하는 경우 클라이언트는 예상 서비스 엔드포인트에 연결됩니다. 이는 클라이언트가 악의적인 서비스에서 호스트 되는 끝점으로 리디렉션되는 것을 방지 하 여 *피싱* 으로부터 보호 하는 역할을 합니다.  
  
 Id 설정을 보여 주는 샘플 응용 프로그램은 [서비스 Id 샘플](../../../../docs/framework/wcf/samples/service-identity-sample.md)을 참조 하세요. 끝점 및 끝점 주소에 대 한 자세한 내용은 [주소](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md)를 참조 하십시오.  
  
> [!NOTE]
> 인증을 위해 NTLM(NT LanMan)을 사용하는 경우 NTLM에서 클라이언트는 서버를 인증할 수 없기 때문에 서비스 ID가 확인되지 않습니다. NTLM은 컴퓨터가 Windows 작업 그룹의 일부이거나 Kerberos 인증을 지원하지 않는 이전 버전의 Windows를 실해하는 경우 사용됩니다.  
  
 클라이언트가 보안 채널을 시작 하 여 서비스에 메시지를 보내는 경우 WCF (Windows Communication Foundation) 인프라는 서비스를 인증 하 고 서비스 id가 끝점에 지정 된 id와 일치 하는 경우에만 메시지를 보냅니다. 클라이언트에서 사용 하는 주소입니다.  
  
 다음 단계를 통해 ID 처리를 수행합니다.  
  
- 디자인 타임에 클라이언트 개발자는 WSDL을 통해 노출된 엔드포인트의 메타데이터에서 서비스의 ID를 확인합니다.  
  
- 런타임에 클라이언트 애플리케이션은 메시지를 서비스에 보내기 전에 서비스의 보안 자격 증명 클레임을 확인합니다.  
  
 클라이언트에서의 ID 처리 작업은 서비스에 대한 클라이언트 인증과 유사합니다. 보안 서비스는 클라이언트의 자격 증명이 인증될 때까지 코드를 실행하지 않습니다. 마찬가지로 서비스 메타데이터에서 미리 알려진 정보에 따라 서비스의 자격 증명이 인증될 때까지 클라이언트에서 메시지를 서비스로 보내지 않습니다.  
  
 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 클래스의 <xref:System.ServiceModel.EndpointAddress> 속성은 클라이언트에서 호출한 서비스의 ID를 나타냅니다. 서비스는 메타데이터에 <xref:System.ServiceModel.EndpointAddress.Identity%2A>를 게시합니다. 클라이언트 개발자가 서비스 끝점에 대해 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 실행 하는 경우 생성 된 구성에는 서비스의 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 속성 값이 포함 됩니다. WCF 인프라 (보안을 사용 하 여 구성 된 경우)는 서비스가 지정 된 id를 소유 하 고 있는지 확인 합니다.  
  
> [!IMPORTANT]
> 메타데이터에는 서비스의 예상 ID가 포함되어 있기 때문에 서비스에 대한 HTTPS 엔드포인트를 만드는 것과 같이 보안을 설정하여 서비스 메타데이터를 노출하는 것이 좋습니다. 자세한 내용은 [방법: 메타 데이터 끝점](../../../../docs/framework/wcf/feature-details/how-to-secure-metadata-endpoints.md)을 보호 합니다.  
  
## <a name="identity-types"></a>ID 형식  
 서비스는 6 가지 유형의 id를 제공할 수 있습니다. 각 ID 형식은 구성의 `<identity>` 요소 내에 포함될 수 있는 요소에 해당합니다. 사용되는 형식은 시나리오 및 서비스 보안 요구 사항에 따라 다릅니다. 다음 표에서는 각 ID 형식에 대해 설명합니다.  
  
|ID 형식|설명|일반적인 시나리오|  
|-------------------|-----------------|----------------------|  
|DNS(Domain Name System)|이 요소를 X.509 인증서 또는 Windows 계정과 함께 사용합니다. 자격 증명에 지정된 DNS 이름과 이 요소에 지정된 값을 비교합니다.|DNS 검사를 사용하면 DNS 또는 주체 이름을 가진 인증서를 사용할 수 있습니다. DNS 또는 주체 이름이 같은 인증서를 다시 발급하는 경우 ID 검사가 계속 유효합니다. 인증서를 다시 발급하면 새 RSA 키를 얻게 되지만 같은 DNS 또는 주체 이름을 유지합니다. 따라서 클라이언트는 서비스에 대한 ID 정보를 업데이트할 필요가 없습니다.|  
|인증서. `ClientCredentialType`을 Certificate로 설정한 경우 기본값입니다.|이 요소는 클라이언트와 비교할 Base64 인코딩된 X.509 인증서 값을 지정합니다.<br /><br /> 또한 서비스를 인증 하는 데 CardSpace를 자격 증명으로 사용 하는 경우이 요소를 사용 합니다.|이 요소는 지문 값에 따라 하나의 인증서만 사용하도록 인증을 제한합니다. 이렇게 하면 고유한 지문 값을 가지므로 인증을 강화할 수 있습니다. 여기에는 한 가지 주의 사항이 있습니다. 인증서가 동일한 주체 이름으로 다시 발급 되는 경우 새 지문이 있습니다. 따라서 새 지문을 모르는 경우 클라이언트가 서비스의 유효성을 검사할 수 없습니다. 인증서의 지문을 [찾는 방법에 대 한 자세한 내용은 방법: 인증서](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)의 지문을 검색 합니다.|  
|Certificate Reference|앞에서 설명한 Certificate 옵션과 동일합니다. 그러나 이 요소를 사용하면 인증서 이름 및 인증서를 검색할 저장소 위치를 지정할 수 있습니다.|앞에서 설명한 Certificate 시나리오와 동일합니다.<br /><br /> 인증서 저장소 위치를 변경할 수 있는 이점이 있습니다.|  
|RSA|이 요소는 클라이언트와 비교할 RSA 키 값을 지정합니다. Certificate 옵션과 비슷하지만 인증서 지문을 사용하는 대신 인증서의 RSA 키를 사용합니다.|RSA 검사를 사용하면 RSA 키에 따라 하나의 인증서만 사용하도록 인증을 제한할 수 있습니다. 이렇게 하면 RSA 키 값이 변경된 경우 기존 클라이언트와 작동하지 않는 서비스 대신 특정 RSA 키에 대한 인증을 강화할 수 있습니다.|  
|UPN(User Principal Name). `ClientCredentialType`이 Windows로 설정되고 시스템 계정 중 하나로 서비스 프로세스가 실행되지 않는 경우 기본값입니다.|이 요소는 서비스를 실행하는 UPN을 지정합니다. [인증을 위해 서비스 id를 재정의](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)하는 Kerberos 프로토콜 및 id 섹션을 참조 하세요.|이렇게 하면 서비스가 특정 Windows 사용자 계정으로 실행됩니다. 사용자 계정은 현재 로그온한 사용자이거나 특정 사용자 계정으로 실행 중인 서비스일 수 있습니다.<br /><br /> 서비스가 Active Directory 환경 내의 도메인 계정으로 실행 중인 경우 이 설정에서는 Windows Kerberos 보안을 활용합니다.|  
|SPN(서비스 사용자 이름). `ClientCredentialType`을 Windows로 설정하고 서비스 프로세스가 LocalService, LocalSystem 또는 NetworkService의 시스템 계정 중 하나로 실행 중인 경우 기본값입니다.|이 요소는 서비스 계정과 연결된 SPN을 지정합니다. [인증을 위해 서비스 id를 재정의](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)하는 Kerberos 프로토콜 및 id 섹션을 참조 하세요.|이렇게 하면 SPN 및 SPN과 연결된 특정 Windows 계정이 서비스를 식별합니다.<br /><br /> Setspn.exe 도구를 사용하여 서비스 사용자 계정의 컴퓨터 계정을 연결할 수 있습니다.<br /><br /> 서비스가 시스템 계정 중 하나 또는 연결된 SPN 이름을 가진 도메인 계정으로 실행 중이고 컴퓨터가 Active Directory 환경 내의 도메인 멤버인 경우 이 설정에서는 Windows Kerberos 보안을 활용합니다.|  
  
## <a name="specifying-identity-at-the-service"></a>서비스에서 ID 지정  
 일반적으로 선택한 클라이언트 자격 증명 형식에 따라 서비스 메타데이터에 노출되는 ID 형식이 결정되므로 서비스에 ID를 설정할 필요가 없습니다. 서비스 id를 재정의 하거나 지정 하는 방법에 대 한 자세한 내용은 [인증을 위해 서비스 Id 재정의](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)를 참조 하세요.  
  
## <a name="using-the-identity-element-in-configuration"></a>구성에서 \<identity > 요소 사용  
 이전에 `Certificate,`에 표시된 바인딩에서 클라이언트 자격 증명 형식을 변경하면 생성된 WSDL에 다음 코드에 표시된 ID 값에 대한 Base64로 serialize된 X.509 인증서가 포함됩니다. 이는 Windows 이외의 모든 클라이언트 자격 증명 형식에 대한 기본값입니다.  

 구성의 요소를 `<identity>` 사용 하거나 코드에서 id를 설정 하 여 기본 서비스 id의 값을 변경 하거나 id 형식을 변경할 수 있습니다. 다음 구성 코드에서는 값 `contoso.com`으로 DNS(Domain Name System) ID를 설정합니다.  

## <a name="setting-identity-programmatically"></a>프로그래밍 방식으로 ID 설정  
 WCF가 자동으로 결정 하므로 서비스에서 명시적으로 id를 지정할 필요가 없습니다. 그러나 WCF를 사용 하면 필요한 경우 끝점에 id를 지정할 수 있습니다. 다음 코드에서는 특정 DNS ID를 사용하여 새 서비스 엔드포인트를 추가합니다.  
  
 [!code-csharp[C_Identity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_identity/cs/source.cs#5)]
 [!code-vb[C_Identity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_identity/vb/source.vb#5)]  
  
## <a name="specifying-identity-at-the-client"></a>클라이언트에서 ID 지정  
 디자인 타임에 클라이언트 개발자는 일반적으로 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 클라이언트 구성을 생성 합니다. 생성된 구성 파일(클라이언트에서 사용)에는 서버 ID가 포함되어 있습니다. 예를 들어, 다음 코드는 앞의 예제에서처럼 DNS ID를 지정하는 서비스에서 생성됩니다. 클라이언트 엔드포인트 ID 값은 서비스 값과 일치합니다. 이 경우 클라이언트가 서비스에 대한 Windows(Kerberos) 자격 증명을 받을 때 값은 `contoso.com`이 됩니다.  

 Windows 대신 서비스가 Certificate를 클라이언트 자격 증명 형식으로 지정하는 경우 인증서의 DNS 속성 값은 `contoso.com`이 됩니다. 또는 DNS 속성이 `null`인 경우 인증서의 주체 이름은 `contoso.com`이어야 합니다.  
  
#### <a name="using-a-specific-value-for-identity"></a>ID에 대해 특정 값 사용  
 다음 클라이언트 구성 파일에서는 서비스 ID가 특정 값이 되는 방법을 보여 줍니다. 다음 예제에서 클라이언트는 두 개의 엔드포인트와 통신할 수 있습니다. 첫 번째 끝점은 인증서 지문으로 식별되고 두 번째는 인증서 RSA 키로 식별됩니다. 즉, 퍼블릭 키/프라이빗 키 쌍만 포함하는 신뢰할 수 있는 기관에서 발급하지 않은 인증서입니다.  

## <a name="identity-checking-at-run-time"></a>런타임에 ID 검사  
 디자인 타임에 클라이언트 개발자는 메타데이터를 통해 서버 ID를 확인합니다. 런타임에 서비스에서 엔드포인트를 호출하기 전에 ID 검사가 수행됩니다.  
  
 ID 값은 메타데이터에 의해 지정되는 인증 형식, 즉 서비스에 사용되는 자격 증명 형식과 연결됩니다.  
  
 채널이 인증을 위해 X.509 인증서를 사용하여 메시지 수준 또는 전송 수준의 SSL(Secure Sockets Layer)을 인증하도록 구성된 경우 다음 ID 값이 유효합니다.  
  
- DNS. WCF는 SSL 핸드셰이크 중에 제공 된 인증서에 dns 또는 `CommonName` (CN) 특성이 클라이언트의 dns id에 지정 된 값과 동일한 지 확인 합니다. 이러한 검사는 서버 인증서 유효성 검사 확인 작업 이외에 추가로 수행됩니다. 기본적으로 WCF는 신뢰할 수 있는 루트 인증 기관에서 서버 인증서를 발급 했는지 확인 합니다.  
  
- 인증서. SSL 핸드셰이크 중에 WCF는 원격 끝점이 id에 지정 된 정확한 인증서 값을 제공 하는지 확인 합니다.  
  
- 인증서 참조. 인증서와 동일합니다.  
  
- RSA. WCF는 SSL 핸드셰이크 중에 원격 끝점이 id에 지정 된 정확한 RSA 키를 제공 하는지 확인 합니다.  
  
 서비스가 인증을 목적으로 Windows 자격 증명을 통해 메시지 또는 전송 수준 SSL을 사용하여 인증하고 자격 증명을 협상하는 경우 다음 ID 값이 유효합니다.  
  
- DNS. 협상은 DNS 이름을 검사할 수 있도록 서비스의 SPN을 전달합니다. SPN은 `host/<dns name>` 형식입니다.  
  
- SPN. `host/myservice`와 같은 명시적 서비스 SPN이 반환됩니다.  
  
- UPN. 서비스 계정의 UPN입니다. UPN은 형식 `username` @ 입니다`domain`. 예를 들어, 서비스가 사용자 계정으로 실행 중인 경우 `username@contoso.com`일 수 있습니다.  
  
 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 속성을 사용하여 ID를 프로그램 방식으로 지정하는 작업은 선택 사항입니다. ID를 지정하지 않고 클라이언트 자격 증명 형식이 Windows인 경우 기본값은 "host/" 리터럴이 접두사로 붙은 서비스 엔드포인트 주소의 호스트 이름 부분으로 값이 설정된 SPN입니다. ID를 지정하지 않고 클라이언트 자격 증명 형식이 Certificate인 경우 기본값은 `Certificate`입니다. 이 값은 메시지 수준 및 전송 수준 보안 모두에 적용됩니다.  
  
## <a name="identity-and-custom-bindings"></a>ID 및 사용자 지정 바인딩  
 서비스 ID는 사용하는 바인딩 형식에 따라 달라지기 때문에 사용자 지정 바인딩을 만들 때 적절한 ID가 노출되는지 확인합니다. 예를 들어, 다음 코드 예제에서 보안 대화 부트스트랩 바인딩의 ID가 엔드포인트의 바인딩 ID와 일치하지 않기 때문에 노출된 ID는 보안 형식과 호환되지 않습니다. 보안 대화 바인딩은 DNS ID를 설정하는 반면 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>는 UPN 또는 SPN ID를 설정합니다.  
  
 [!code-csharp[C_Identity#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_identity/cs/source.cs#8)]
 [!code-vb[C_Identity#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_identity/vb/source.vb#8)]  
  
 사용자 지정 바인딩에 대해 바인딩 요소를 올바르게 스택 하는 방법에 대 한 자세한 내용은 [사용자 정의 바인딩 만들기](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)를 참조 하세요. 를 사용 <xref:System.ServiceModel.Channels.SecurityBindingElement> [하 여 사용자 지정 바인딩을 만드는 방법에 대 한 자세한 내용은 방법: 지정 된 인증 모드](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)에 대 한 SecurityBindingElement를 만듭니다.  
  
## <a name="see-also"></a>참고자료

- [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [방법: 지정 된 인증 모드에 대 한 SecurityBindingElement 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
- [방법: 사용자 지정 클라이언트 Id 검증 도구 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)
- [자격 증명 형식 선택](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)
- [인증서 작업](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
- [사용자 정의 바인딩 만들기](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)
- [방법: 인증서의 지문을 검색 합니다.](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)
