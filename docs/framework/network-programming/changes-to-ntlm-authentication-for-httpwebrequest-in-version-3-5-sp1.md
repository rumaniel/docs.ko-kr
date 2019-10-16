---
title: 버전 3.5 SP1에서 HttpWebRequest에 대한 NTLM 인증 변경 내용
ms.date: 03/30/2017
ms.assetid: 8bf0b428-5a21-4299-8d6e-bf8251fd978a
ms.openlocfilehash: 388e6dc648e1fd68e24a852cb08de107f09f9c9f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754884"
---
# <a name="changes-to-ntlm-authentication-for-httpwebrequest-in-version-35-sp1"></a>버전 3.5 SP1에서 HttpWebRequest에 대한 NTLM 인증 변경 내용

.NET Framework 버전 3.5 SP1 이상에서는 <xref:System.Net.HttpWebRequest>, <xref:System.Net.HttpListener>, <xref:System.Net.Security.NegotiateStream> 및 System.Net 네임스페이스의 관련 클래스에 의해 Windows 통합 인증이 처리되는 방식에 영향을 미치는 보안 변경 사항이 적용되었습니다. 이러한 변경 내용은 NTLM 기반의 Windows 통합 인증이 사용되는 경우 이러한 클래스를 통해 웹 요청을 만들고 응답을 수신하는 애플리케이션에 영향을 줄 수 있습니다. 이 변경 내용은 Windows 통합 인증을 사용하도록 구성된 웹 서버 및 클라이언트 애플리케이션에 영향을 미칠 수 있습니다.

## <a name="overview"></a>개요

Windows 통합 인증의 디자인을 사용하면 일부 자격 증명 응답이 유니버설이 될 수 있으므로 다시 사용되거나 전달될 수 있습니다. 이 특정 디자인 기능이 필요하지 않은 경우 인증 프로토콜이 채널 관련 정보뿐만 아니라 대상 관련 정보도 전달해야 합니다. 그런 다음 서비스가 확장된 보호를 제공하여 자격 증명 응답에 SPN(서비스 사용자 이름) 같은 서비스 관련 정보가 포함되어 있는지 확인할 수 있습니다. 자격 증명 교환에 이 정보가 포함되면 서비스는 부적절하게 확보되었을 수 있는 자격 증명 응답의 악의적인 사용을 더 효과적으로 방지할 수 있습니다.

<xref:System.Net> 및 <xref:System.Net.Security> 네임스페이스의 여러 구성 요소는 호출하는 애플리케이션 대신 Windows 통합 인증을 수행합니다. 이 섹션에서는 Windows 통합 인증 사용에 확장된 보호를 추가하기 위한 System.Net 구성 요소의 변경 내용을 설명합니다.

## <a name="changes"></a>변경 내용

Windows 통합 인증과 함께 사용되는 NTLM 인증 프로세스는 대상 컴퓨터에서 실행되고 다시 클라이언트 컴퓨터로 전송되는 시도를 포함합니다. 컴퓨터 자체가 생성한 시도를 수신하는 경우 연결이 루프백 연결(예: IPv4 주소 127.0.0.1)이 아니면 인증이 실패합니다.

내부 웹 서버에서 실행되는 서비스에 액세스하는 경우 `http://contoso/service` 또는 `https://contoso/service`와 비슷한 URL을 사용하여 서비스에 액세스하는 것이 일반적입니다. 이름 “contoso”는 서비스가 배포된 컴퓨터의 컴퓨터 이름이 아닌 경우가 많습니다. <xref:System.Net> 및 관련 네임스페이스는 Active Directory, DNS, NetBIOS, 로컬 컴퓨터의 호스트 파일(예: 일반적으로 WINDOWS\system32\drivers\etc\hosts) 또는 로컬 컴퓨터의 lmhosts 파일(예: 일반적으로 WINDOWS\system32\drivers\etc\lmhosts)을 사용하여 이름을 주소로 확인하는 기능을 지원합니다. “contoso”로 전송된 요청이 적절한 서버 컴퓨터로 전송되도록 이름 “contoso”가 확인됩니다.

대규모 배포용으로 구성된 경우 클라이언트 애플리케이션 및 최종 사용자가 사용한 적이 없는 기본 컴퓨터 이름과 함께 하나의 가상 서버 이름을 배포에 지정하는 것이 일반적이기도 합니다. 예를 들어 `www.contoso.com` 서버를 호출하지만 내부 네트워크에서는 단순히 “contoso”를 사용할 수 있습니다. 이 이름을 클라이언트 웹 요청에서는 호스트 헤더라고 합니다. HTTP 프로토콜에 지정된 대로 호스트 요청-헤더 필드는 요청되는 리소스의 인터넷 호스트 및 포트 번호를 지정합니다. 이 정보는 사용자 또는 참조 리소스(일반적으로 HTTP URL)에 의해 지정된 원래 URI에서 가져옵니다. .NET Framework 버전 4에서는 클라이언트가 새 <xref:System.Net.HttpWebRequest.Host%2A> 속성을 사용하여 이 정보를 설정할 수도 있습니다.

<xref:System.Net.AuthenticationManager> 클래스는 <xref:System.Net.WebRequest> 파생 클래스와 <xref:System.Net.WebClient> 클래스에서 사용하는 관리되는 인증 구성 요소(“모듈”)를 제어합니다. <xref:System.Net.AuthenticationManager> 클래스는 애플리케이션이 인증 중에 사용할 사용자 지정 SPN 문자열을 제공할 수 있도록 URI 문자열로 인덱싱된 <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A?displayProperty=nameWithType> 개체를 노출하는 속성을 제공합니다.

이제 버전 3.5 SP1에서는 <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A> 속성이 설정되지 않은 경우 NTLM(NT LAN Manager) 인증 교환에서 SPN의 요청 URL에 사용된 호스트 이름을 지정하도록 기본적으로 설정됩니다. 요청 URL에 사용된 호스트 이름은 클라이언트 요청의 <xref:System.Net.HttpRequestHeader?displayProperty=nameWithType>에 지정된 호스트 헤더와 다를 수 있습니다. 요청 URL에 사용된 호스트 이름은 서버의 실제 호스트 이름, 서버의 컴퓨터 이름, 컴퓨터의 IP 주소 또는 루프백 주소와 다를 수 있습니다. 이 경우 Windows가 인증 요청에 실패합니다. 이 문제를 해결하려면 클라이언트 요청의 요청 URL에 사용된 호스트 이름(예: “contoso”)이 실제로 로컬 컴퓨터의 대체 이름이라고 Windows에 알려야 합니다.

서버 애플리케이션이 이 변경 내용을 해결하기 위한 몇 가지 가능한 방법이 있습니다. 권장 방법은 요청 URL에 사용된 호스트 이름을 서버의 레지스트리에 있는 `BackConnectionHostNames` 키에 매핑하는 것입니다. `BackConnectionHostNames` 레지스트리 키는 일반적으로 호스트 이름을 루프백 주소에 매핑하는 데 사용됩니다. 단계는 다음과 같습니다.

루프백 주소에 매핑되고 로컬 컴퓨터에서 웹 사이트에 연결할 수 있는 호스트 이름을 지정하려면 다음 단계를 따르세요.

1. [시작], [실행]을 차례로 클릭하고 regedit를 입력한 다음 [확인]을 클릭합니다.

2. 레지스트리 편집기에서 다음 레지스트리 키를 찾아 클릭합니다.

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\MSV1_0`

3. MSV1_0을 마우스 오른쪽 단추로 클릭하고 새로 만들기를 가리킨 다음 다중 문자열 값을 클릭합니다.

4. `BackConnectionHostNames`를 입력한 후 Enter 키를 누릅니다.

5. `BackConnectionHostNames`를 마우스 오른쪽 단추로 클릭하고 수정을 클릭합니다.

6. 값 데이터 상자에 로컬 컴퓨터에 있는 사이트의 호스트 이름(요청 URL에 사용된 호스트 이름)을 입력하고 확인을 클릭합니다.

7. 레지스트리 편집기를 종료한 다음 IISAdmin 서비스를 다시 시작하고 IISReset을 실행합니다.

보안 수준이 낮은 해결 방법은 <https://support.microsoft.com/kb/896861>에 설명된 대로 루프백 검사를 사용하지 않도록 설정하는 것입니다. 이렇게 하면 리플렉션 공격에 대한 보호가 해제됩니다. 따라서 대체 이름 집합을 컴퓨터에서 실제로 사용할 것으로 예상되는 이름으로만 제한하는 것이 좋습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A?displayProperty=nameWithType>
- <xref:System.Net.HttpRequestHeader?displayProperty=nameWithType>
- <xref:System.Net.HttpWebRequest.Host%2A?displayProperty=nameWithType>
