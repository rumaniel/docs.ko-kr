---
title: HTTP 및 HTTPS-WCF 구성
ms.date: 04/08/2019
helpviewer_keywords:
- configuring HTTP [WCF]
ms.assetid: b0c29a86-bc0c-41b3-bc1e-4eb5bb5714d4
ms.openlocfilehash: 4bfdbbc19bb9ed72bc50ebeeac114241ccd47c25
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053406"
---
# <a name="configuring-http-and-https"></a>HTTP 및 HTTPS 구성

WCF 서비스 및 클라이언트는 HTTP 및 HTTPS를 통해 통신할 수 있습니다. HTTP/HTTPS 설정은 IIS(인터넷 정보 서비스)나 명령줄 도구를 사용하여 구성합니다. WCF 서비스가 IIS 아래에서 호스팅되거나 IIS에서 inetmgr.exe 도구를 사용하여 HTTP 또는 HTTPS 설정을 구성할 수 있는 경우입니다. WCF 서비스가 자체 호스팅되는 경우 HTTP 또는 HTTPS 설정은 명령줄 도구를 사용하여 구성됩니다.

최소한 URL 등록을 구성 하 고 서비스를 사용 하는 URL에 대 한 방화벽 예외를 추가 해야 합니다. Netsh.exe 도구를 사용 하 여 이러한 설정을 구성할 수 있습니다.

## <a name="configuring-namespace-reservations"></a>네임 스페이스 예약 구성

네임스페이스 예약은 HTTP URL 네임스페이스 일부에 대한 권한을 특정 사용자 그룹에 할당합니다. 예약을 통해 이러한 사용자에게 네임스페이스의 해당 부분에서 수신 대기하는 서비스를 만들 수 있는 권한을 제공합니다. 예약은 URL 접두사 이며 예약이 예약 경로의 모든 하위 경로 포함 함을 의미 합니다. 네임스페이스 예약은 와일드카드를 사용하는 두 가지 방법을 허용합니다. HTTP Server API 설명서에 설명 합니다 [와일드 카드를 포함 하는 네임 스페이스 클레임 확인 순서](/windows/desktop/Http/routing-incoming-requests)합니다.

실행 중인 애플리케이션에서 비슷한 요청을 만들어 네임스페이스 등록을 추가할 수 있습니다. 등록과 예약은 네임스페이스의 특정 부분에 대해 충돌합니다. 에 제공 된 확인 순서에 따라 등록을 통해 예약 우선 순위 있을 합니다 [와일드 카드를 포함 하는 네임 스페이스 클레임 확인 순서](/windows/desktop/Http/routing-incoming-requests)합니다. 이 경우 예약은 실행 중인 애플리케이션이 요청을 수신하지 못하도록 차단합니다.

다음 예제에서는 Netsh.exe 도구를 사용합니다.

```console
netsh http add urlacl url=http://+:80/MyUri user=DOMAIN\user
```

이 명령은 도메인 \ 사용자 계정에 대 한 지정된 된 URL 네임 스페이스에 대 한 URL 예약을 추가합니다. 자세한 내용은 netsh 명령을 사용 하 여 입력 `netsh http add urlacl /?` 명령 프롬프트에서 Enter 키를 누릅니다.

## <a name="configuring-a-firewall-exception"></a>방화벽 예외 구성

HTTP에서 통신하는 WCF 서비스를 자체 호스팅하는 경우 특정 URL을 사용하여 인바운드 연결을 허용하려면 예외를 방화벽 구성에 추가해야 합니다.

## <a name="configuring-ssl-certificates"></a>SSL 인증서 구성

SSL(Secure Sockets Layer) 프로토콜은 클라이언트 및 서버에서 인증서를 사용하여 암호화 키를 저장합니다. 서버는 클라이언트가 서버 ID를 확인할 수 있도록 연결된 경우 SSL 인증서를 제공합니다. 또한 서버는 양쪽 연결에 상호 인증을 제공하기 위해 클라이언트로부터 인증서를 요청할 수 있습니다.

인증서는 연결 IP 주소 및 연결 포트 번호에 따라 중앙 저장소에 저장됩니다. 특수 IP 주소 0.0.0.0은 로컬 시스템의 IP 주소와 일치합니다. 인증서 저장소 경로 기반으로 하는 Url을 구분 하지 않습니다는 참고 합니다. IP 주소와 포트 조합이 같은 서비스는 서비스의 URL 경로가 다른 경우에도 인증서를 공유해야 합니다.

단계별 지침을 참조 하세요. [방법: SSL 인증서로 포트 구성](how-to-configure-a-port-with-an-ssl-certificate.md)합니다.

## <a name="configuring-the-ip-listen-list"></a>IP 수신 대기 목록 구성

사용자가 URL을 등록하면 HTTP Server API는 IP 주소 및 포트에만 바인딩됩니다. 기본적으로 HTTP Server API는 모든 시스템 IP 주소에 대한 URL의 포트에 바인딩됩니다. HTTP Server API를 사용 하지 않는 응용 프로그램의 IP 주소 및 포트 조합에 이전에 바인딩된 경우 충돌이 발생 합니다. IP 수신 목록에는 컴퓨터의 IP 주소 중 일부에 대 한 포트를 사용 하는 응용 프로그램과 함께 WCF 서비스 수 있습니다. IP 수신 대기 목록에 항목이 포함된 경우 HTTP Server API는 목록에서 지정한 IP 주소에만 바인딩됩니다. IP 수신 대기 목록을 수정하려면 관리자 권한이 필요합니다.

다음 예제에서와 같이 netsh 도구를 사용 하 여 IP 수신 대기 목록을 수정 하려면:

```console
netsh http add iplisten ipaddress=0.0.0.0:8000
```

## <a name="other-configuration-settings"></a>기타 구성 설정

<xref:System.ServiceModel.WSDualHttpBinding>을 사용하는 경우 클라이언트 연결은 네임스페이스 예약 및 Windows 방화벽과 호환되는 기본값을 사용합니다. 이중 연결에 대한 클라이언트 기본 주소를 사용자 지정하는 경우에도 새 주소와 일치하도록 클라이언트에 이러한 HTTP 설정을 구성해야 합니다.

HTTP Server API에 HttpCfg를 통해 사용할 수 없는 일부 고급 구성 설정이 있습니다. 이러한 설정은 레지스트리에 유지되며 HTTP Server API를 사용하는 시스템에서 실행되는 모든 애플리케이션에 적용됩니다. 이러한 설정에 대 한 자세한 내용은 [IIS에 대 한 Http.sys 레지스트리 설정](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows)합니다. 대부분의 사용자는 이러한 설정을 변경할 필요가 없습니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.WSDualHttpBinding>
- [방법: SSL 인증서로 포트 구성](how-to-configure-a-port-with-an-ssl-certificate.md)
