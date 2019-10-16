---
ms.openlocfilehash: a02887327390afb6859c0d5f78a8875bff9539e6
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70997671"
---
### <a name="product-versioning-changes-in-the-net-framework-46-and-later-versions"></a>.NET Framework 4.6 및 이후 버전의 제품 버전 관리 변경 내용

|   |   |
|---|---|
|세부 정보|제품 버전 관리가 .NET Framework의 이전 릴리스와 특히, .NET Framework 4, 4.5, 4.5.1 및 4.5.2에서 변경되었습니다. 자세한 변경 내용은 다음과 같습니다.<ul><li><code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full</code> 키에서 <code>Version</code> 항목의 값이 .NET Framework 4.6 및 해당 지점 릴리스의 경우 <code>4.6.xxxxx</code>로, .NET Framework 4.7 및 4.7.1의 경우 <code>4.7.xxxxx</code>로 변경되었습니다. .NET Framework 4.5, 4.5.1 및 4.5.2에서는 <code>4.5.xxxxx</code> 형식이었습니다.</li><li>.NET Framework 파일에 대한 파일 및 제품 버전 관리는 .NET Framework 4.6 및 해당 지점 릴리스의 경우 이전 버전 관리 체계 4.0.30319.x에서 4.6.X.0으로 변경되었으며, .NET Framework 4.7 및 4.7.1의 경우 4.7.X.0으로 변경되었습니다. 파일을 마우스 오른쪽 단추로 클릭한 후 파일의 속성을 보면 이러한 새 값을 확인할 수 있습니다.</li><li>관리되는 어셈블리의 <xref:System.Reflection.AssemblyFileVersionAttribute> 및 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 특성은 .NET Framework 4.6 및 해당 지점 릴리스의 경우 4.6.X.0 형식, 그리고 .NET Framework 4.7 및 4.7.1의 경우 4.7.X.0 형식의 버전 값을 포함합니다.</li><li>.NET Framework 4.6, 4.6.1, 4.6.2, 4.7 및 4.7.1에서 <xref:System.Environment.Version?displayProperty=nameWithType> 속성은 최종 버전 문자열 <code>4.0.30319.42000</code>을 반환합니다. .NET Framework 4, 4.5, 4.5.1 및 4.5.2에서는 버전 문자열을 <code>4.0.30319.xxxxx</code> 형식(예: &quot;4.0.30319.18010&quot;)으로 반환합니다. Environment.Version 속성에서 새 종속성을 취하는 애플리케이션 코드는 권장하지 않습니다.</li></ul>자세한 내용은 [방법: 설치된 .NET Framework 버전 확인](~/docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요.|
|제안 해결 방법|일반적으로 애플리케이션은 .NET Framework 및 설치 디렉터리 검색의 런타임 버전과 같은 항목 검색을 위한 권장 기술에 의존해야 합니다.<ul><li>.NET Framework의 런타임 버전을 검색하려면 [방법: 설치된 .NET Framework 버전 확인](~/docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요.</li><li>.NET Framework의 설치 경로를 확인하려면<code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full</code> 키의 <code>InstallPath</code> 항목 값을 사용합니다.</li></ul> <blockquote> [!IMPORTANT] 하위 키 이름은 <code>.NET Framework Setup</code>이 아니라 <code>NET Framework Setup</code>입니다.</blockquote> <ul><li>.NET Framework 공용 언어 런타임에 대한 디렉터리 경로를 확인하려면 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeDirectory?displayProperty=nameWithType> 메서드를 호출합니다.</li><li>CLR 버전을 알아보려면 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion?displayProperty=nameWithType> 메서드를 호출합니다. .NET Framework 4 및 해당 지점 릴리스(.NET Framework 4.5, 4.5.1, 4.5.2 및 .NET Framework 4.6, 4.6.1, 4.6.2, 4.7 및 4.7.1)의 경우 문자열 v4.0.30319를 반환합니다.</li></ul>|
|범위|부|
|버전|4.6|
|형식|런타임|
