---
ms.openlocfilehash: 0036fc2b03dde64d24d883e55b9f00c931f0c218
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70997667"
---
### <a name="net-interop-will-now-queryinterface-for-iagileobject-a-winrt-interface"></a>.NET Interop는 이제 IAgileObject(WinRT 인터페이스)에 대한 QueryInterface가 됩니다.

|   |   |
|---|---|
|세부 정보|.NET 대리자와 함께 WinRT 이벤트를 사용하는 경우 Windows는 .NET Framework 4.8부터 IAgileObject에 대한 QI를 제공합니다.  이전 버전의 .NET Framework에서는 런타임이 해당 QI를 실패하여 이벤트를 구독할 수 없었습니다.<ul><li>[ x ] Quirked</li></ul>|
|제안 해결 방법|IAgileObject에 대한 QI를 활성화하여 실행이 중단되면 다음 구성을 설정하여 이 코드를 비활성화할 수 있습니다. <h4>방법 1: 환경 변수</h4> 다음 환경 변수 COMPLUS_DisableCCWSupportIAgileObject=1을 설정합니다. 이 메서드는 이 환경 변수를 상속하는 모든 환경에 영향을 줍니다. 이는 단일 콘솔 세션일 수도 있고 환경 변수를 전역적으로 설정하는 경우 전체 머신에 영향을 줄 수도 있습니다. 환경 변수 이름은 대/소문자를 구분하지 않습니다. <h4>방법 2: 레지스트리</h4> 레지스트리 편집기(regedit.exe)를 사용하여 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft.NETFramework, HKEY_CURRENT_USER\SOFTWARE\Microsoft.NETFramework 하위 키 중 하나를 찾습니다. 그런 후, 다음 값 이름을 추가합니다. DisableCCWSupportIAgileObject 유형: DWORD(32비트) 값(REG_WORD라고도 함) 값: 1. Windows REG.EXE 도구를 사용하여 명령줄 또는 스크립팅 환경에서 이 값을 추가할 수 있습니다. 예:<pre><code class="lang-console">reg add HKLM\SOFTWARE\Microsoft\.NETFramework /v DisableCCWSupportIAgileObject /t REG_DWORD /d 1&#13;&#10;</code></pre>이 경우 <code>HKEY_LOCAL_MACHINE</code> 대신 <code>HKLM</code>가 사용됩니다. 이 구문에 대한 도움말을 보려면 <code>reg add /?</code>를 사용합니다. 레지스트리 값 이름은 대/소문자를 구분하지 않습니다.|
|범위|Microsoft Edge|
|버전|4.8|
|형식|런타임|
