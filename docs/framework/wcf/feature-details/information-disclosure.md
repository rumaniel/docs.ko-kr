---
title: 정보 공개
ms.date: 03/30/2017
ms.assetid: 4064c89f-afa6-444a-aa7e-807ef072131c
ms.openlocfilehash: 0e45a71855ecb172f36aae8139f89d4b8c8ffd0d
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425301"
---
# <a name="information-disclosure"></a>정보 공개

정보 공개를 사용하여 공격자가 시스템에 대해 유용한 정보를 얻을 수 있습니다. 따라서 항상 노출하려는 정보의 내용과 악의가 있는 사용자가 사용해도 되는지 여부를 고려합니다. 다음은 가능한 정보 공개 공격을 나열하고 각 공격에 대한 완화 방안을 제공합니다.

## <a name="message-security-and-http"></a>메시지 보안 및 HTTP

HTTP 전송 계층을 통해 메시지 수준 보안을 사용하는 경우 메시지 수준 보안이 HTTP 헤더를 보호하지 않습니다. HTTP 헤더를 보호하기 위한 유일한 방법은 HTTP 대신 HTTPS 전송을 사용하는 것입니다. HTTPS 전송은 HTTP 헤더를 포함한 전체 메시지를 SSL(Secure Sockets Layer) 프로토콜을 사용하여 암호화합니다.

## <a name="policy-information"></a>정책 정보

민감한 발급된 토큰 요구 사항 또는 토큰 발급자 정보가 정책에 노출되는 페더레이션 시나리오의 경우 특히 정책 보안 유지가 중요합니다. 이러한 경우 페더레이션 서비스 정책 엔드포인트의 보안을 유지하여 발급된 토큰에 삽입할 클레임 형식 또는 악의적인 토큰 발급자에게 클라이언트 리디렉션과 같이 공격자가 서비스에 대한 정보를 가져오지 못하도록 하는 것이 좋습니다. 예를 들어, 공격자가 메시지 가로채기(man-in-the-middle) 공격을 실행한 발급자로 끝나도록 페더레이션 신뢰 체인을 다시 구성하여 사용자 이름/암호 쌍을 검색할 수 있습니다. 또한 정책 검색을 통해 바인딩을 가져오는 페더레이션 클라이언트가 가져온 페더레이션 신뢰 체인의 발급자를 신뢰하는지 확인하는 것이 좋습니다. 페더레이션 시나리오에 대 한 자세한 내용은 참조 하세요. [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md)합니다.

## <a name="memory-dumps-can-reveal-claim-information"></a>메모리 덤프가 클레임 정보를 노출할 수 있음

응용 프로그램이 실패할 경우 예를 들어 Dr. Watson씨가 작성한 파일과 같이 로그 파일에 클레임 정보를 포함할 수 있습니다. 이 정보는 지원 팀과 같은 다른 엔터티에 내보내지 않아야 합니다. 그렇지 않을 경우 개인 데이터가 포함된 클레임 정보도 내보내집니다. 로그 파일을 알 수 없는 엔터티에 보내지 않으면 이러한 문제를 줄일 수 있습니다. 자세한 내용은 [Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=89160)합니다.

## <a name="endpoint-addresses"></a>엔드포인트 주소

엔드포인트 주소에는 엔드포인트와 통신하는 데 필요한 정보가 포함되어 있습니다. SOAP 보안에서는 클라이언트와 서버 간의 대칭 키를 협상하기 위해 교환되는 보안 협상 메시지에 전체 주소가 포함되어 있어야 합니다. 보안 협상은 부트스트랩 프로세스이기 때문에 이 프로세스 동안 주소 헤더를 암호화할 수 없습니다. 따라서 주소에 어떠한 기밀 데이터도 포함하지 않아야 합니다. 포함할 경우 정보 공개 공격을 받을 수 있습니다.

## <a name="certificates-transferred-unencrypted"></a>암호화되지 않은 상태로 전송된 인증서

X.509 인증서를 사용하여 클라이언트를 인증하는 경우 인증서는 SOAP 헤더 내에서 보안되지 않은 상태로 전송됩니다. 이것은 잠재적인 PII(개인적으로 식별할 수 있는 정보) 공개로 고려해야 합니다. 이는 전체 메시지가 전송 수준 보안으로 암호화되는 `TransportWithMessageCredential` 모드에는 적용되지 않습니다.

## <a name="service-references"></a>서비스 참조

서비스 참조는 다른 서비스에 대한 참조입니다. 예를 들어, 서비스가 작업 과정에서 서비스 참조를 클라이언트에 전달할 수 있습니다. 서비스 참조를 사용 하 여도 되는 *트러스트 id 검증 도구*, 응용 프로그램 데이터 또는 대상에 대 한 자격 증명 등의 정보를 공개 하기 전에 대상 주체의 id를 확인 하는 내부 구성 요소. 원격 트러스트 ID를 검증할 수 없거나 잘못된 경우 보낸 사람이 데이터 자체, 애플리케이션 또는 사용자를 손상시킬 수 있는 공개된 데이터가 없는지 확인해야 합니다.

완화 방안에는 다음이 포함됩니다.

- 서비스 참조는 신뢰할 수 있는 것으로 간주합니다. 서비스 참조 인스턴스를 전송할 때마다 손상되지 않았는지 확인해야 합니다.

- 일부 애플리케이션에서 서비스 참조의 데이터 및 원격 호스트에서 제공하는 신뢰 데이터를 기반으로 신뢰를 대화형으로 구축하는 사용자 경험을 제공할 수 있습니다. WCF는 이러한 기능에 대 한 확장성 지점을 제공 하지만 사용자가 구현한 해야 합니다.

## <a name="ntlm"></a>NTLM

기본적으로 Windows 도메인 환경의 경우 Windows 인증은 Kerberos 프로토콜을 사용하여 사용자를 인증하고 권한을 부여합니다. 일부 이유로 인해 Kerberos 프로토콜을 사용할 수 없는 경우 NTLM(NT LAN Manager)을 대신 사용합니다. <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> 속성을 `false`로 설정하면 이 동작을 비활성화할 수 있습니다. NTLM을 사용하는 경우 고려해야 할 문제는 다음과 같습니다.

- NTLM은 클라이언트 사용자 이름을 노출합니다. 사용자 이름을 기밀로 유지해야 하는 경우 바인딩의 `AllowNTLM` 속성을 `false`로 설정합니다.

- NTLM은 서버 인증을 제공하지 않습니다. 따라서 NTLM을 인증 프로토콜로 사용하는 경우 클라이언트가 올바른 서비스와 통신하는지 확인할 수 없습니다.

### <a name="specifying-client-credentials-or-invalid-identity-forces-ntlm-usage"></a>클라이언트 자격 증명 또는 잘못된 ID를 지정하면 강제로 NTLM 사용

클라이언트를 만들 때 도메인 이름 없이 클라이언트 자격 증명을 지정하거나 잘못된 서버 ID를 지정하면 NTLM이 Kerberos 프로토콜 대신 사용됩니다(`AllowNtlm` 속성을 `true`로 설정한 경우). NTLM이 서버 인증을 수행하지 않기 때문에 정보가 잠재적으로 공개될 수 있습니다.

예를 들어 가능성이 도메인 이름 없이 Windows 클라이언트 자격 증명을 지정 하려면 다음 Visual C# 코드에 표시 된 대로 있습니다.

```csharp
MyChannelFactory.Credentials.Windows.ClientCredential = new System.Net.NetworkCredential("username", "password");
```

코드가 도메인 이름을 지정하지 않기 때문에 NTLM이 사용됩니다.

도메인을 지정했지만 엔드포인트 ID 기능을 사용하여 잘못된 서비스 사용자 이름을 지정하는 경우 NTLM이 사용됩니다. 끝점 id를 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [서비스 Id 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)합니다.

## <a name="see-also"></a>참고자료

- [보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)
- [권한 상승](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)
- [서비스 거부](../../../../docs/framework/wcf/feature-details/denial-of-service.md)
- [변조](../../../../docs/framework/wcf/feature-details/tampering.md)
- [지원되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
- [재생 공격](../../../../docs/framework/wcf/feature-details/replay-attacks.md)
