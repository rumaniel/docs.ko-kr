---
title: '방법: 설치된 .NET Framework 버전 확인'
ms.date: 04/18/2019
dev_langs:
- csharp
- vb
ms.custom: updateeachrelease
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining version
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: abfa42be4b8c759da3fb34a2204058143e39689c
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956662"
---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a>방법: 설치된 .NET Framework 버전 확인

사용자는 자신의 컴퓨터에 여러 버전의 .NET Framework를 [설치](https://docs.microsoft.com/dotnet/framework/install)하여 실행할 수 있습니다. 따라서 앱을 개발하거나 배포할 때는 사용자의 컴퓨터에 어떤 .NET Framework 버전이 설치되었는지 알아야 합니다.

.NET Framework는 각 버전으로 식별되는 다음과 같은 2개의 주요 구성 요소로 구성됩니다.

- 앱의 기능을 제공하는 형식 및 리소스 컬렉션에 해당하는 어셈블리 집합. .NET Framework와 어셈블리는 동일한 버전 번호를 공유합니다.

- 앱 코드를 관리하고 실행하는 CLR(공용 언어 런타임). CLR은 고유한 버전 번호로 식별됩니다([버전 및 종속성](versions-and-dependencies.md) 참조).

> [!NOTE]
> 새 .NET Framework 버전에서는 각각 이전 버전의 기능을 유지하며 새 기능을 추가합니다. 여러 버전의 .NET Framework를 동시에 단일 컴퓨터에서 로드할 수 있습니다. 즉, 이전 버전을 제거하지 않고도 .NET Framework를 설치할 수 있습니다. 사용 중인 애플리케이션이 특정 버전에 종속적일 수 있고 해당 버전을 제거하면 애플리케이션이 중단될 수 있으므로 컴퓨터에서 .NET Framework의 이전버전은 일반적으로 제거해서는 안 됩니다.
>
> .NET Framework 버전과 CLR 버전은 다릅니다.
>
> - .NET Framework의 버전은 .NET Framework 클래스 라이브러리를 구성하는 어셈블리 세트를 기반으로 정해집니다. 예를 들어, .NET Framework 버전에는 4.5, 4.6.1, 4.7.2가 있습니다.
>- CLR의 버전은 .NET Framework 애플리케이션이 실행되는 런타임을 기반으로 정해집니다. 하나의 CLR 버전이 여러 개의.NET Framework 버전을 지원합니다. 예를들어, CLR 버전 4.0.30319.*xxxxx*는 .NET Framework 버전 4~4.5.2를 지원하고, *xxxxx*는 42000보다 작으며, CLR버전 4.0.30319.42000은 .NET Framework 4.6.에서 시작하는 .NET Framework 버전을 지원합니다.
>
> 자세한 내용은 [.NET Framework 버전 및 종속성](versions-and-dependencies.md)을 참조하십시오.

컴퓨터에 설치된 .NET Framework 버전 목록을 보려면 레지스트리에 액세스 합니다. 또는 레지스트리 편집기를 사용하여 레지스트리를 확인하거나 코드로 레지스트리를 쿼리합니다.

- 최신 .NET Framework 버전 찾기(4.5 이상):
  - [레지스트리 편집기를 사용하여 .NET Framework 버전 찾기](#net_b)
  - [코드를 사용하여 .NET Framework 버전에 대한 레지스트리 쿼리](#net_d)
  - [PowerShell을 사용하여 .NET Framework 버전에 대한 레지스트리 쿼리](#ps_a)
- 이전 .NET Framework 버전 찾기(1&#8211;4):
  - [레지스트리 편집기를 사용하여 .NET Framework 버전 찾기](#net_a)
  - [코드를 사용하여 .NET Framework 버전에 대한 레지스트리 쿼리](#net_c)

컴퓨터에 설치된 CLR 버전의 목록을 보려면 도구 또는 코드를 사용하십시오.

- [Clrver 도구 사용](#clr_a)
- [코드를 사용하여 Environment 클래스 쿼리](#clr_b)

.NET Framework의 버전별로 설치된 업데이트를 검색하는 방법에 대한 자세한 내용은 [방법: 설치된 .NET Framework 업데이트 확인](how-to-determine-which-net-framework-updates-are-installed.md).

## <a name="find-newer-net-framework-versions-45-and-later"></a>최신 .NET Framework 버전 찾기(4.5 이상)

<a name="net_b"></a>

### <a name="find-net-framework-versions-45-and-later-in-the-registry"></a>레지스트리에서 .NET Framework 버전 4.5 이상 찾기

1. **시작** 메뉴에서 **실행**을 선택하고 *regedit*을 입력한 다음, **OK**를 선택합니다.

     regedit을 실행하려면 관리자 자격 증명이 있어야 합니다.

2. 레지스트리 편집기에서 다음 하위 키를 엽니다. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full**. **전체**하위 키가 없으면 .NET Framework 4.5 이상이 설치되어 있지 않은 것입니다.

    > [!NOTE]
    > 레지스트리의 **NET Framework Setup** 폴더는 마침표로 시작하지 ‘않습니다’. 

3. **릴리스**라는 DWORD 항목을 확인합니다. 릴리스 DWORD가 있으면 컴퓨터에 .NET Framework 4.5 이상이 설치된 것입니다. 그 값은 특정 버전의 .NET Framework에 대응되는 릴리스 키입니다. 예를 들어, 다음 그림에서 **릴리스**항목은 *378389*로, 이것은 .NET Framework 4.5.의 릴리스 키입니다.

     ![.NET Framework 4.5에 대한 레지스트리 항목](./media/clr-installdir.png ".NET Framework 4.5에 대한 레지스트리 항목")

다음 표에는 .NET Framework 4.5 이상 버전의 각 운영 체제상의 **릴리스** DWORD가 나와 있습니다.

[!INCLUDE[Release key values note](~/includes/version-keys-note.md)]

<a name="version_table"></a>

|.NET Framework 버전|릴리스 DWORD의 값|
|--------------------------------|-------------|
|.NET Framework 4.5|모든 Windows 운영 체제: 378389|
|.NET Framework 4.5.1|Windows 8.1 및 Windows Server 2012 R2: 378675<br />다른 모든 Windows 운영 체제: 378758|
|.NET Framework 4.5.2|모든 Windows 운영 체제: 379893|
|.NET Framework 4.6|Windows 10: 393295<br />다른 모든 Windows 운영 체제: 393297|
|.NET Framework 4.6.1|Windows 10 11월 업데이트 운영 체제: 394254<br />다른 모든 Windows 운영 체제(Windows 10 포함): 394271|
|.NET Framework 4.6.2|Windows 10 1주년 업데이트 및 Windows Server 2016: 394802<br />다른 모든 Windows 운영 체제(다른 Windows 10 운영 체제 포함): 394806|
|.NET Framework 4.7|Windows 10 Creators Update: 460798<br />다른 모든 Windows 운영 체제(다른 Windows 10 운영 체제 포함): 460805|
|.NET Framework 4.7.1|Windows 10 Fall Creators Update 및 Windows Server, 버전 1709: 461308<br/>다른 모든 Windows 운영 체제(다른 Windows 10 운영 체제 포함): 461310|
|.NET Framework 4.7.2|Windows 10 2018년 4월 업데이트 및 Windows Server, 버전 1803: 461808<br/>Windows 10 2018년 4월 업데이트 및 Windows Server, 버전 1803 이외의 모든 Windows 운영 체제: 461814|
|.NET Framework 4.8|Windows 10 2019년 5월 업데이트: 528040<br/>다른 모든 Windows 운영 체제(다른 Windows 10 운영 체제 포함): 528049|

이 값은 다음과 같이 사용할 수 있습니다.

- 특정 버전의 .NET Framework가 특정 버전의 Windows 운영 체제에 설치되어 있는지 여부를 확인하려면 **릴리스** DWORD 값이 표에 나열된 값과 ‘동일한지’ 테스트하세요.  예를 들어 .NET Framework 4.6이 Windows 10 시스템에 있는지 확인하려면 **릴리스** 값이 393295와 ‘같은지’ 테스트합니다. 

- 최하 버전의 .NET Framework가 있는지 확인하려면 해당 버전에 대해 더 작은 **릴리스** DWORD 값을 사용하세요. 예를 들어 애플리케이션이 .NET Framework 4.6 이상 버전에서 실행되는 경우 393295과 ‘같거나 이보다 큰’ **릴리스** DWORD 값을 테스트합니다.  각 .NET Framework 버전에 대한 최소 **릴리스** DWORD 값만 나열하는 표를 보려면 [.NET Framework 4.5 이상 버전에서 릴리스 DWORD의 최솟값](minimum-release-dword.md)을 참조하세요.

- 여러 버전을 테스트하려면 최신 .NET Framework 버전의 더 작은 DWORD 값과 ‘같거나 이보다 큰’ 값을 테스트한 후 연속적인 각 이전 버전에 대해 더 작은 DWORD 값과 비교하세요.  예를 들어 애플리케이션에 .NET Framework 4.7 이상이 필요하고 특정 버전의 .NET Framework를 확인하려는 경우 461808(또는 .NET Framework 4.7.2의 경우는 더 작은 DWORD 값)과 ‘같거나 이보다 큰’ **릴리스** DWORD 값을 테스트하여 시작합니다.  그런 다음, 이 **릴리스** DWORD 값을 이후의 각 .NET Framework 버전에 대한 더 작은 값과 비교합니다. 각 .NET Framework 버전에 대한 최소 **릴리스** DWORD 값만 나열하는 표를 보려면 [.NET Framework 4.5 이상 버전에서 릴리스 DWORD의 최솟값](minimum-release-dword.md)을 참조하세요.

<a name="net_d"></a>

### <a name="find-net-framework-versions-45-and-later-with-code"></a>코드를 사용하여 .NET Framework 버전 4.5 이상 찾기

1. <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType>와 <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType>메서드를 사용하여 Windows 레지스트리의**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full** 하위 키에 액세스 합니다.

    **릴리스** DWORD 항목이**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full** 하위 키에 있으면 .NET Framework 4.5 이상 버전이 컴퓨터에 설치된 것입니다.

2. **릴리스** 항목값을 확인하여 설치된 버전을 확인합니다. 이후 버전과의 호환성을 유지하려는 경우 버전의 값이 [.NET Framework 버전 표](#version_table)에 나와 있는 값 이상인지를 확인하면 됩니다.

다음 예제에서는 레지스트리에서 **릴리스** 항목값을 확인하여 .NET Framework 4.5 이상 버전이 설치되어 있는지 확인합니다.

[!code-csharp[ListVersions#5](../../../samples/snippets/csharp/framework/migration-guide/versions-installed3.cs)]
[!code-vb[ListVersions#5](../../../samples/snippets/visualbasic/framework/migration-guide/versions-installed3.vb)]

이 예제에서는 버전을 확인하기 위한 권장된 방법을 수행합니다.

- **릴리스**항목의 값이 알려진 릴리스 키의 값보다 *크거나 같은지* 확인합니다.

- 최신 버전에서 가장 오래된 버전 순서대로 확인합니다.

<a name="ps_a"></a>

### <a name="check-for-a-minimum-required-net-framework-version-45-and-later-with-powershell"></a>PowerShell을 사용하여 필요한 최소 .NET Framework 버전(4.5 이상) 확인

- PowerShell 명령을 사용하여 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full** 하위 키의 **릴리스** 항목값을 확인합니다.

다음 예제에서는 **릴리스** 항목 값을 확인하여 .NET Framework 4.6.2 이상이 설치되어 있는지 확인합니다. `True`설치된 경우 코드 반환, 설치되지 않은 경우 `False` 코드 반환.

```PowerShell
(Get-ItemProperty "HKLM:SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
```

다른 최소 필수 .NET Framework 버전을 확인하려면 예제의 *394802*를 [.NET Framework 버전 표](#version_table)의 **릴리스** 값으로 바꿉니다.

## <a name="find-older-net-framework-versions-182114"></a>이전 .NET Framework 버전 찾기(1&#8211;4)

<a name="net_a"></a>

### <a name="find-net-framework-versions-182114-in-the-registry"></a>레지스트리에서 .NET Framework 버전 1&#8211;4 찾기

1. **시작** 메뉴에서 **실행**을 선택하고 *regedit*을 입력한 다음, **OK**를 선택합니다.

    regedit을 실행하려면 관리자 자격 증명이 있어야 합니다.

2. 레지스트리 편집기에서 다음 하위 키를 엽니다. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP**:

    - .NET Framework 버전 1.1~3.5의 경우, 각각 설치된 버전이 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP** 하위 키 아래에 하위 키로 나열됩니다. 예,**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v3.5**. 버전 번호는 버전 하위 키의 **Version** 항목에 값으로 저장됩니다.

    - .NET Framework 4의 경우 **Version** 항목은 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4.0\Client** 하위 키 또는 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4.0\Full** 하위 키 아래에, 또는 두 하위 키 아래에 있습니다.

    > [!NOTE]
    > 레지스트리의**NET Framework Setup**폴더는 마침표로 시작하지 않습니다.

    다음 그림은 .NET Framework 3.5의 하위 키와 **Version** 항목을 보여줍니다.

    ![.NET Framework 3.5의 레지스트리 항목.](./media/net-4-and-earlier.png ".NET Framework 3.5 및 이전 버전")

<a name="net_c"></a>

### <a name="find-net-framework-versions-182114-with-code"></a>코드를 사용하여 .NET Framework 버전 1&#8211;4 찾기

- <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType>클래스를 사용하여 Windows 레지스트리의**HKEY_LOCAL_MACHINE\Software\Microsoft\NET Framework Setup\NDP** 하위 키에 액세스 합니다.

다음 예제에서는 설치된 .NET Framework 1&#8211;4버전을 찾습니다.

[!code-csharp[ListVersions](../../../samples/snippets/csharp/framework/migration-guide/versions-installed1.cs)]
[!code-vb[ListVersions](../../../samples/snippets/visualbasic/framework/migration-guide/versions-installed1.vb)]

## <a name="find-clr-versions"></a>CLR 버전 찾기

<a name="clr_a"></a>

### <a name="find-the-current-clr-version-with-clrverexe"></a>Clrver.exe를 사용하여 현재 CLR 버전 찾기

[CLR 버전 도구(Clrver.exe)](../tools/clrver-exe-clr-version-tool.md)를 사용하여 컴퓨터에 설치된 공용 언어 런타임의 버전을 확인합니다.

- [Visual Studio용 개발자 명령 프롬프트](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)을 입력 `clrver` 합니다.

    샘플 출력:

    ```console
    Versions installed on the machine:
    v2.0.50727
    v4.0.30319
    ```

<a name="clr_b"></a>

### <a name="find-the-current-clr-version-with-the-environment-class"></a>Environment 클래스를 사용하여 현재 CLR 버전 찾기

> [!IMPORTANT]
> .NET Framework 4.5 이상의 경우 <xref:System.Environment.Version%2A?displayProperty=nameWithType>속성을 사용하여 런타임의 버전을 확인하지 않습니다. 대신 코드로 [.NET Framework 버전 4.5 이상 찾기](#net_d)에 설명된 것처럼 레지스트리를 쿼리하십시오.

1. <xref:System.Version>개체를 검색하기 위해 <xref:System.Environment.Version?displayProperty=nameWithType>속성을 쿼리합니다.

    반환된 `System.Version`개체는 현재 코드를 실행하는 런타임 버전을 식별합니다. 컴퓨터에 설치된 어셈블리 버전이나 다른 런타임 버전은 반환하지 않습니다.

    .NET Framework 버전 4, 4.5, 4.5.1 및 4.5.2의 경우 반환된 <xref:System.Version>개체 문자열 표현은 4.0.30319.*xxxxx* 형식이며, *xxxxx*는 42000보다 작습니다. .NET Framework 4.6 및 이후 버전의 경우 형식은 4.0.30319.42000입니다.

2. `Version`개체를 가져온 후, 다음과 같이 개체를 쿼리하십시오.

   - 주 릴리스 식별자(예:버전 4.0의 경우 *4*)는 <xref:System.Version.Major%2A?displayProperty=nameWithType>속성을 사용합니다.

   - 부 릴리스 식별자(예:버전 4.0의 경우 *0*)를 가져오고 <xref:System.Version.Minor%2A?displayProperty=nameWithType>속성을 사용합니다.

   - 전체 버전 문자열(예를 들어*4.0.30319.18010*)에는 <xref:System.Version.ToString%2A?displayProperty=nameWithType>메서드를 사용합니다. 메서드는 코드를 실행 하는 런타임 버전을 반영하는 단일 값을 반환합니다. 이는 컴퓨터에 설치된 어셈블리 버전이나 다른 런타임 버전은 반환하지 않습니다.

다음 예제에서는 <xref:System.Environment.Version%2A?displayProperty=nameWithType>속성을 사용하여 CLR 버전 정보를 검색합니다.

[!code-csharp[ListVersions](../../../samples/snippets/csharp/framework/migration-guide/versions-installed2.cs)]
[!code-vb[ListVersions](../../../samples/snippets/visualbasic/framework/migration-guide/versions-installed2.vb)]

## <a name="see-also"></a>참고 항목

- [방법: 설치된 .NET Framework 업데이트 확인](how-to-determine-which-net-framework-updates-are-installed.md)
- [개발자용 .NET Framework 설치](../install/guide-for-developers.md)
- [.NET Framework 버전 및 종속성](versions-and-dependencies.md)
