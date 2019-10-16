---
ms.openlocfilehash: da79a19b3276f6fd2d679eb98406dd85e2a19948
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70997673"
---
### <a name="apps-published-with-clickonce-that-use-a-sha-256-code-signing-certificate-may-fail-on-windows-2003"></a>SHA-256 코드 서명 인증서를 사용하는 ClickOnce로 게시된 앱이 Windows 2003에서 실패할 수 있음

|   |   |
|---|---|
|세부 정보|실행 파일이 SHA256으로 서명됩니다. 이전에는 코드 서명 인증서가 SHA-1 또는 SHA-256인지에 관계없이 SHA1로 서명되었습니다. 적용 대상:<ul><li>Visual Studio 2012 이상으로 빌드된 모든 애플리케이션</li><li>.NET Framework 4.5가 있는 시스템에서 Visual Studio 2010 또는 이전 버전으로 빌드된 애플리케이션</li></ul>또한 .NET Framework 4.5 이상이 있는 경우 컴파일 시의 대상 .NET Framework 버전에 관계없이 ClickOnce 매니페스트도 SHA-256 인증서에 대해 SHA-256으로 서명됩니다.|
|제안 해결 방법|ClickOnce 실행 파일의 서명 변경 내용은 Windows Server 2003 시스템에만 영향을 줍니다. KB 938397을 설치해야 합니다. 앱이 .NET Framework 4.0 또는 이전 버전을 대상으로 하는 경우에도 SHA-256으로 매니페스트에 서명하는 변경 내용으로 인해 .NET Framework 4.5 이상 버전에서 런타임 종속성이 발생합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|대상 변경|
