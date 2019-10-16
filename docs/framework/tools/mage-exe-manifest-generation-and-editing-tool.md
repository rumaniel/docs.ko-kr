---
title: Mage.exe(매니페스트 생성 및 편집 도구)
ms.date: 12/06/2018
helpviewer_keywords:
- Manifest Generation and Editing tool
- Mage.exe
ms.assetid: 77dfe576-2962-407e-af13-82255df725a1
ms.openlocfilehash: 13a22cd15da3d4cf7eb26359c692389d27d377c0
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044514"
---
# <a name="mageexe-manifest-generation-and-editing-tool"></a>Mage.exe(매니페스트 생성 및 편집 도구)

매니페스트 생성 및 편집 도구(*Mage.exe*)는 애플리케이션 매니페스트 및 배포 매니페스트의 생성과 편집을 지원하는 명령줄 도구입니다. *Mage.exe*는 명령줄 도구로서 일괄 처리 스크립트뿐 아니라 ASP.NET 애플리케이션을 비롯한 Windows 기반 애플리케이션에서도 실행할 수 있습니다.

*Mage.exe* 대신 그래픽 애플리케이션인 *MageUI.exe*를 사용할 수도 있습니다. 자세한 내용은 [MageUI.exe (Manifest Generation and Editing Tool, Graphical Client)](mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)을 참조하십시오.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

*Mage.exe* 및 *MageUI.exe*의 두 버전은 Visual Studio에 포함되어 있습니다. 버전 정보를 보려면 *MageUI.exe*를 실행하고, **도움말**을 선택하고, **정보**를 선택합니다. 이 설명서는 *Mage.exe* 및 *MageUI.exe*의 버전 4.0.x.x에 대해 설명합니다.

## <a name="syntax"></a>구문

```console
Mage [commands] [commandOptions]
```

## <a name="parameters"></a>매개 변수

다음 표에서는 *Mage.exe*에서 지원되는 명령을 보여 줍니다. 이러한 명령에서 지원되는 옵션에 대한 자세한 내용은 [New 및 Update 명령 옵션](#new-and-update-command-options) 및 [Sign 명령 옵션](#sign-command-options)을 참조하세요.

|명령|설명|
|-------------|-----------------|
|**-cc, ClearApplicationCache**|모든 온라인 전용 애플리케이션의 다운로드한 애플리케이션 캐시를 지웁니다.|
|**-n, -New** *fileType [newOptions]*|지정한 형식의 새 파일을 만듭니다. 유효한 형식은 다음과 같습니다.<br /><br /> -   `Deployment`: 새 배포 매니페스트를 만듭니다.<br />-   `Application`: 새 애플리케이션 매니페스트를 만듭니다.<br /><br /> 이 명령에 추가 매개 변수를 지정하지 않으면 적절한 기본 태그 및 특성 값을 사용하여 적절한 형식의 파일이 만들어집니다.<br /><br /> 새 파일의 이름과 경로를 지정하려면 **-ToFile** 옵션(아래 표 참조)을 사용합니다.<br /><br /> 매니페스트의 \<dependency&gt; 섹션에 추가한 애플리케이션의 모든 어셈블리를 포함하는 애플리케이션 매니페스트를 만들려면 **-FromDirectory** 옵션(아래 표 참조)을 사용합니다.|
|**-u, -Update** *[filePath] [updateOptions]*|매니페스트 파일에서 하나 이상의 항목을 변경합니다. 편집하는 파일의 형식은 지정할 필요가 없습니다. Mage.exe에서 휴리스틱 집합을 사용하여 파일을 검사하고 배포 매니페스트인지 아니면 애플리케이션 매니페스트인지 확인합니다.<br /><br /> 이미 인증서를 사용하여 파일에 서명한 경우 **-Update** 를 사용하면 키 서명 블록이 제거됩니다. 이유는 키 서명에 파일의 해시가 포함되어 있으며 파일 렌더러를 수정하면 해시가 무효화되기 때문입니다.<br /><br /> 다음 표에 나와 있는 **-ToFile** 옵션을 사용하여 기존 파일을 덮어쓰지 않고 새 파일 이름 및 경로를 지정할 수 있습니다.|
|**-s, -Sign** `[signOptions]`|키 쌍 또는 X509 인증서를 사용하여 파일에 서명합니다. 서명은 파일 내부에 XML 요소로 삽입됩니다.<br /><br /> **-TimestampUri** 값을 지정하는 매니페스트를 서명할 때 인터넷에 연결해야 합니다.|
|**-ver, -Verify** *[manifest-filename]*|매니페스트가 올바르게 서명되었는지 확인합니다. 다른 명령과 함께 사용할 수 없습니다. <br/><br/>**.NET Framework 4.7 이상 버전에서 사용할 수 있습니다.**|
|**-h, -?, -Help** *[verbose]*|사용 가능한 모든 명령과 옵션에 대한 설명을 표시합니다. `verbose` 를 지정하면 자세한 도움말을 볼 수 있습니다.|

## <a name="new-and-update-command-options"></a>New 및 Update 명령 옵션

다음 표에서는 `-New` 및 `-Update` 명령에서 지원하는 옵션을 보여 줍니다.

|옵션|기본값|적용 대상|설명|
|-------------|-------------------|----------------|-----------------|
|**-a, -Algorithm**|sha1RSA|애플리케이션 매니페스트<br /><br /> 배포 매니페스트|종속성 다이제스트를 생성하는 알고리즘을 지정합니다. 값은 "Sha256RSA" 또는 "sha1RSA"이어야 합니다.<br /><br /> "-업데이트" 옵션과 함께 사용합니다. "-기호" 옵션을 사용하는 경우 이 옵션은 무시됩니다.|
|**-appc, -AppCodeBase** `manifestReference`||배포 매니페스트|애플리케이션 매니페스트 파일에 대한 URL 또는 파일 경로 참조를 삽입합니다. 이 값은 애플리케이션 매니페스트에 대한 전체 경로여야 합니다.|
|**-appm, -AppManifest** `manifestPath`||배포 매니페스트|배포의 애플리케이션 매니페스트에 대한 참조를 배포 매니페스트에 추가합니다.<br /><br /> `manifestPath` 에서 가리키는 파일이 실제로 존재해야 하며, 그렇지 않으면 *Mage.exe*에서 오류가 발생합니다. `manifestPath` 에서 참조하는 파일이 애플리케이션 매니페스트가 아니면 *Mage.exe*에서 오류가 발생합니다.|
|**-cf, -CertFile** `filePath`||모든 파일 형식|매니페스트 또는 라이선스 파일에 서명하는 데 사용할 X509 디지털 인증서의 위치를 지정합니다. 인증서에 PFX(Personal Information Exchange) 파일에 대한 암호가 필요한 경우 **-Password** 옵션을 이 옵션과 함께 사용할 수 있습니다. .NET Framework 4.7부터 파일에 프라이빗 키가 없는 경우 **-CryptoProvider** 및 **-KeyContainer** 옵션의 조합이 필요합니다.<br/><br/>.NET Framework 4.6.2부터 *Mage.exe*는 CNG 및 CAPI 인증서로 매니페스트에 서명합니다.|
|**-ch, -CertHash** `hashSignature`||모든 파일 형식|클라이언트 컴퓨터의 개인 인증서 저장소에 저장되는 디지털 인증서의 해시를 지정합니다. 이 해시는 Windows 인증서 콘솔에서 표시되는 디지털 인증서의 지문 문자열에 해당합니다.<br /><br /> `hashSignature` 에는 대문자와 소문자를 모두 사용할 수 있습니다. 이 매개 변수를 단일 문자열로 제공할 수도 있고, 지문의 각 8진수 단위 값을 공백으로 구분하여 전체 지문을 따옴표로 묶어 제공할 수도 있습니다.|
|**-csp, -CryptoProvider** `provider-name`||모든 파일 형식|프라이빗 키 컨테이너를 포함하는 CSP(암호화 서비스 공급자)의 이름을 지정합니다. 이 옵션에는 **-KeyContainer** 옵션이 필요합니다.<br/><br/>이 옵션은 .NET Framework 4.7부터 사용할 수 있습니다.|
|**-fd, -FromDirectory** `directoryPath`||애플리케이션 매니페스트|애플리케이션 매니페스트를 모든 하위 디렉터리를 포함하여 `directoryPath`에 있는 모든 어셈블리 및 파일에 대한 설명으로 채웁니다. 여기에서 `directoryPath` 는 배포할 애플리케이션이 있는 디렉터리입니다. *Mage.exe*는 디렉터리에 있는 각 파일이 어셈블리인지 또는 정적 파일인지 결정합니다. 파일이 어셈블리인 경우에는 `<dependency>` 태그 및 `installFrom` 특성이 어셈블리 이름, 코드베이스 및 버전과 함께 애플리케이션에 추가됩니다. 정적 파일인 경우에는 `<file>` 태그가 추가됩니다. *Mage.exe*는 또한 간단한 휴리스틱 집합을 사용하여 애플리케이션의 주 실행 파일을 검색하고 이를 매니페스트에서 ClickOnce 애플리케이션의 진입점으로 표시합니다.<br /><br /> *Mage.exe*에서는 파일을 "데이터" 파일로 자동으로 표시하지 않습니다. 이는 직접 수행해야 합니다. 자세한 내용은 [방법: ClickOnce 애플리케이션에 데이터 파일 포함](/visualstudio/deployment/how-to-include-a-data-file-in-a-clickonce-application)을 참조하세요.<br /><br /> 또한 *Mage.exe*에서는 각 파일의 크기를 기반으로 파일에 대한 해시를 생성합니다. ClickOnce에서는 이러한 해시를 사용하여 매니페스트가 생성된 후 배포 파일이 무단으로 변경되지 않았는지 확인합니다. 배포 파일 중 변경된 파일이 있는 경우 **-Update** 명령 및 **-FromDirectory** 옵션을 사용하여 *Mage.exe*를 실행하면 모든 참조된 파일의 해시 및 어셈블리 버전이 업데이트됩니다.<br /><br /> **-FromDirectory** 를 사용하면 `directoryPath`에 있는 모든 하위 디렉터리의 모든 파일이 포함됩니다.<br /><br /> **-FromDirectory**를 **-Update** 명령과 함께 사용할 경우 *Mage.exe*는 이 디렉터리에 더 이상 존재하지 않는 파일을 애플리케이션 매니페스트에서 모두 제거합니다.|
|**-if, -IconFile**  `filePath`||애플리케이션 매니페스트|.ICO 아이콘 파일의 전체 경로를 지정합니다. 이 아이콘은 시작 메뉴 및 프로그램 추가 또는 제거 항목에서 애플리케이션 이름 옆에 나타납니다. 아이콘을 지정하지 않으면 기본 아이콘이 사용됩니다.|
|**-ip, -IncludeProviderURL**  `url`|true|배포 매니페스트|배포 매니페스트가 **-ProviderURL**에 의해 설정된 업데이트 위치 값을 포함할지 여부를 나타냅니다.|
|**-i, -Install** `willInstall`|true|배포 매니페스트|ClickOnce 애플리케이션을 로컬 컴퓨터에 설치할지 여부 또는 웹에서 실행할지 여부를 지정합니다. 애플리케이션을 설치하면 Windows의 **시작** 메뉴에 애플리케이션이 표시됩니다. 유효한 값은 "true" 또는 "t"와 "false" 또는 "f"입니다.<br /><br /> **-MinVersion** 옵션을 지정하면 사용자 컴퓨터에 **-MinVersion** 보다 이전 버전이 설치되어 있는 경우 **-Install**에 전달하는 값에 관계없이 애플리케이션이 설치됩니다.<br /><br /> 이 옵션은 **-BrowserHosted** 옵션과 함께 사용할 수 없습니다. 같은 매니페스트에 두 옵션을 모두 지정하려고 하면 오류가 발생합니다.|
|**-kc, -KeyContainer** `name`||모든 파일 형식|프라이빗 키의 이름을 포함하는 키 컨테이너를 지정합니다. 이 옵션에는 **CryptoProvider** 옵션이 필요합니다.<br/><br/>이 옵션은 .NET Framework 4.7부터 사용할 수 있습니다.|
|**-mv, -MinVersion**  `[version]`|ClickOnce 배포 매니페스트에서 **-Version** 플래그에 지정되어 나열된 버전입니다.|배포 매니페스트|사용자가 실행할 수 있는 이 애플리케이션의 최소 버전입니다. 이 플래그를 사용하면 애플리케이션의 명명된 버전이 필수 업데이트가 됩니다. 주요 변경 내용 또는 심각한 보안 결함에 대한 업데이트가 포함된 제품 버전을 출시하는 경우 이 플래그를 사용하여 해당 업데이트를 필수적으로 설치해야 하고 이전 버전을 더 이상 실행할 수 없도록 지정할 수 있습니다.<br /><br /> `version` 의 의미 체계는 **-Version** 플래그에 대한 인수와 동일합니다.|
|**-n, -Name** `nameString`|배포|모든 파일 형식|애플리케이션을 식별하는 데 사용되는 이름입니다. ClickOnce에서는 **시작** 메뉴(애플리케이션 자체를 설치하도록 구성한 경우)와 권한 높이기 대화 상자에 애플리케이션을 표시하는 데 이 이름을 사용합니다. **참고:**  기존 매니페스트를 업데이트하고 게시자 이름을 이 옵션으로 지정하지 않으면 *Mage.exe*에서 컴퓨터에 정의된 조직 이름으로 매니페스트를 업데이트합니다. 다른 이름을 사용하려면 이 옵션을 사용하여 원하는 게시자 이름을 지정합니다.|
|**-pwd, -Password** `passwd`||모든 파일 형식|디지털 인증서로 매니페스트에 서명하는 데 사용되는 암호입니다. **-CertFile** 옵션과 함께 사용해야 합니다.|
|**-p, Processor** `processorValue`|Msil|애플리케이션 매니페스트<br /><br /> 배포 매니페스트|이 배포가 실행될 마이크로프로세서 아키텍처입니다. 이 값은 특정 마이크로프로세서용으로 미리 컴파일된 어셈블리를 가진 하나 이상의 설치를 준비하는 경우에 필요합니다. 유효한 값은 `msil`, `x86`, `ia64`및 `amd64`입니다. `msil` (Microsoft intermediate language)을 지정하면 모든 어셈블리가 플랫폼에 종속되지 않고, 애플리케이션이 처음 실행될 때 CLR(공용 언어 런타임)에서 Just-In-Time 컴파일을 수행합니다.|
|**-pu,** **-ProviderURL** `url`||배포 매니페스트|ClickOnce에서 애플리케이션 업데이트를 확인할 URL을 지정합니다.|
|**-pub, -Publisher** `publisherName`||애플리케이션 매니페스트<br /><br /> 배포 매니페스트|배포 또는 애플리케이션 매니페스트의 설명 요소에 게시자 이름을 추가합니다. 애플리케이션 매니페스트에서 사용하는 경우에는 "true" 또는 "t" 값을 갖는 **-UseManifestForTrust** 를 함께 지정해야 합니다. 이렇게 하지 않으면 이 매개 변수에서 오류가 발생합니다.|
|**-s, -SupportURL**  `url`||애플리케이션 매니페스트<br /><br /> 배포 매니페스트|프로그램 추가/제거에서 ClickOnce 애플리케이션에 대해 표시되는 링크를 지정합니다.|
|**-ti, -TimestampUri** `uri`||애플리케이션 매니페스트<br /><br /> 배포 매니페스트|디지털 타임스탬프 서비스의 URL입니다. 매니페스트에 타임스탬프를 적용하면 애플리케이션의 다음 버전을 배포하기 전에 디지털 인증서가 만료되어도 매니페스트에 다시 서명할 필요가 없습니다. 자세한 내용은 [Windows 루트 인증서 프로그램 구성원](https://go.microsoft.com/fwlink/?LinkId=159000)을 참조하세요.|
|**-t, -ToFile** `filePath`|- 새로 만들기:<br />- 배포: deploy.application<br />- 애플리케이션: application.exe.manifest<br />- 업데이트:<br />- 입력 파일|모든 파일 형식|생성 또는 수정된 파일의 출력 경로를 지정합니다.<br /><br /> **-New** 를 사용할 때 **-ToFile**을 제공하지 않으면 출력이 현재 작업 디렉터리에 기록됩니다. **-Update**를 사용할 때 **-ToFile**을 제공하지 않으면 *Mage.exe*에서 파일을 입력 파일에 다시 기록합니다.|
|**-tr, -TrustLevel** `level`|애플리케이션 URL이 있는 영역을 기반으로 합니다.|애플리케이션 매니페스트|클라이언트 컴퓨터의 애플리케이션에 부여할 신뢰 수준입니다. 유효한 값은 "Internet", "Intranet" 및 "FullTrust" 등입니다.|
|**-um, -UseManifestForTrust** `willUseForTrust`|False|애플리케이션 매니페스트|클라이언트에서 애플리케이션이 실행될 때 애플리케이션 매니페스트의 디지털 서명을 사용하여 신뢰 관련 결정을 내릴지 여부를 지정합니다. "true" 또는 "t"를 지정하면 애플리케이션 매니페스트를 사용하여 신뢰 관련 결정을 내립니다. "false" 또는 "f"를 지정하면 배포 매니페스트의 서명이 사용됩니다.|
|**-v, -Version** `versionNumber`|1.0.0.0|애플리케이션 매니페스트<br /><br /> 배포 매니페스트|배포의 버전입니다. 인수는 "*N.N.N.N*" 형식의 유효한 버전의 문자열이어야 하며, 여기서 "*N*"은 부호 없는 32비트 정수입니다.|
|**-wpf, -WPFBrowserApp**  `isWPFApp`|False|애플리케이션 매니페스트<br /><br /> 배포 매니페스트|애플리케이션이 독립형 실행 파일이 아닌 Internet Explorer 내에 호스팅되는 WPF(Windows Presentation Foundation) 애플리케이션인 경우에만 이 플래그를 사용합니다. 유효한 값은 "true" 또는 "t"와 "false" 또는 "f"입니다.<br /><br /> 애플리케이션 매니페스트의 경우 `hostInBrowser` 요소 아래에 `entryPoint` 특성을 삽입합니다.<br /><br /> 배포 매니페스트의 경우 `install` 요소의 `deployment` 특성을 false로 설정하고 배포 매니페스트를 .xbap 확장명으로 저장합니다. 이 인수를 **-Install** 인수와 함께 지정하면 브라우저에서 호스트되는 애플리케이션을 오프라인 애플리케이션으로 설치할 수 없으므로 오류가 발생합니다.|

## <a name="sign-command-options"></a>Sign 명령 옵션

다음 표에서는 `-Sign` 명령에서 지원하며 모든 파일 형식에 적용할 수 있는 옵션을 보여 줍니다.

|옵션|설명|
|-------------|-----------------|
|**-cf, -CertFile** `filePath`|매니페스트에 서명하는 데 사용할 디지털 인증서의 위치를 지정합니다. 인증서에 PFX(Personal Information Exchange) 파일에 대한 암호가 필요한 경우 **-Password** 옵션을 이 옵션과 함께 사용할 수 있습니다. .NET Framework 4.7부터 파일에 프라이빗 키가 없는 경우 **-CryptoProvider** 및 **-KeyContainer** 옵션의 조합이 필요합니다.<br/><br/>.NET Framework 4.6.2부터 *Mage.exe*는 CNG 및 CAPI 인증서로 매니페스트에 서명합니다.|
|**-ch, -CertHash** `hashSignature`|클라이언트 컴퓨터의 개인 인증서 저장소에 저장되는 디지털 인증서의 해시를 지정합니다. 이 해시는 Windows 인증서 콘솔에서 표시되는 디지털 인증서의 지문 속성에 해당합니다.<br /><br /> `hashSignature` 에는 대문자와 소문자를 모두 사용할 수 있습니다. 이 매개 변수를 단일 문자열로 제공할 수도 있고, 지문의 각 8진수 단위 값을 공백으로 구분하여 전체 지문을 따옴표로 묶어 제공할 수도 있습니다.|
**-csp, -CryptoProvider** `provider-name`|프라이빗 키 컨테이너를 포함하는 CSP(암호화 서비스 공급자)의 이름을 지정합니다. 이 옵션에는 **-KeyContainer** 옵션이 필요합니다.<br/><br/>이 옵션은 .NET Framework 4.7부터 사용할 수 있습니다.|
|**-kc, -KeyContainer** `name`|프라이빗 키의 이름을 포함하는 키 컨테이너를 지정합니다. 이 옵션에는 **CryptoProvider** 옵션이 필요합니다.<br/><br/>이 옵션은 .NET Framework 4.7부터 사용할 수 있습니다.|
|**-pwd, -Password** `passwd`|디지털 인증서로 매니페스트에 서명하는 데 사용되는 암호입니다. **-CertFile** 옵션과 함께 사용해야 합니다.|
|**-t, -ToFile** `filePath`|생성 또는 수정된 파일의 출력 경로를 지정합니다.|

## <a name="remarks"></a>설명

*Mage.exe*에 대한 모든 인수는 대/소문자를 구분하지 않습니다. 명령 및 옵션의 앞에 대시(-) 또는 슬래시(/)를 사용할 수 있습니다.

**-Sign** 명령과 함께 사용되는 모든 인수는 언제든지 **-New** 또는 **-Update** 명령과도 함께 사용될 수 있습니다. 다음 두 명령은 서로 동일합니다.

```console
mage -Sign c:\HelloWorldDeployment\HelloWorld.deploy -CertFile cert.pfx
mage -Update c:\HelloWorldDeployment\HelloWorld.deploy -CertFile cert.pfx
```

> [!NOTE]
> .NET Framework 버전 4.6.2부터는 CNG 인증서도 지원됩니다.

 서명된 문서에서는 파일의 해시를 사용하여 서명이 문서에 대해 올바른지 확인하므로 서명은 마지막에 수행해야 하는 작업입니다. 서명된 파일이 변경되면 다시 서명해야 합니다. 이전에 서명된 문서에 다시 서명하는 경우 *Mage.exe*는 이전 서명을 새로운 서명으로 바꿉니다.

 배포 매니페스트를 채우기 위해 **-AppManifest** 옵션을 사용하는 경우 *Mage.exe*는 현재 배포 버전 기반의 이름을 가진 하위 디렉터리 내의 배포 매니페스트와 동일한 디렉터리에 애플리케이션 매니페스트가 있는 것으로 가정하고 그에 따라 배포 매니페스트를 구성합니다. 애플리케이션 매니페스트가 다른 위치에 있는 경우에는 **-AppCodeBase** 옵션을 사용하여 위치를 설정합니다.

 애플리케이션을 배포하기 전에 배포 및 애플리케이션 매니페스트에 서명해야 합니다. 매니페스트 서명에 대한 지침은 [Trusted Application Deployment Overview](/visualstudio/deployment/trusted-application-deployment-overview)를 참조하세요.

 애플리케이션 매니페스트에 대한 **-TrustLevel** 옵션에서는 클라이언트 컴퓨터에서 애플리케이션을 실행하는 데 필요한 권한 집합을 지정합니다. 기본적으로 애플리케이션의 신뢰 수준은 애플리케이션의 URL이 속하는 *영역* 을 기반으로 할당됩니다. 인터넷을 통해 배포된 애플리케이션은 인터넷 영역에 배치되는 반면 회사 네트워크를 통해 배포된 애플리케이션은 일반적으로 인트라넷 영역에 배치됩니다. 두 가지 보안 영역 모두 애플리케이션에서 로컬 리소스에 액세스하는 데 제한이 있지만 인트라넷 영역이 인터넷 영역보다 약간 덜 제한적입니다. FullTrust 영역에서는 컴퓨터의 로컬 리소스에 대해 애플리케이션에 완전한 액세스가 부여됩니다. **-TrustLevel** 옵션을 통해 애플리케이션을 이 영역에 배치하면 CLR의 트러스트 관리자 구성 요소가 이러한 높은 신뢰 수준을 부여할지 여부를 사용자에게 묻습니다. 애플리케이션을 회사 네트워크를 통해 배포하는 경우에는 신뢰할 수 있는 애플리케이션 배포를 사용하여 사용자에게 묻지 않고 애플리케이션의 신뢰 수준을 높일 수 있습니다.

 애플리케이션 매니페스트에서는 사용자 지정 신뢰 섹션도 지원합니다. 이 섹션을 사용하면 애플리케이션 실행에 필요한 특정 권한만 요청하도록 매니페스트를 구성할 수 있으므로 애플리케이션에서 최소 권한만 요청하도록 하는 보안 원칙을 따르는 데 도움이 됩니다. *Mage.exe*에서는 사용자 지정 신뢰 섹션을 직접 추가할 수 없습니다. 텍스트 편집기, XML 파서 또는 그래픽 도구인 *MageUI.exe*를 사용하여 이를 추가할 수 있습니다. *MageUI.exe*를 사용하여 사용자 지정 신뢰 섹션을 추가하는 방법에 대한 자세한 내용은 [MageUI.exe](mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)(Manifest Generation and Editing Tool, Graphical Client)를 참조하세요.

Visual Studio 2017에는 *Mage.exe*의 4.6.1 버전이 포함되어 있습니다. 이 버전의 *Mage.exe*으로 만들어진 매니페스트는 .NET Framework 4를 대상으로 합니다. 이전 버전의 .NET Framework를 대상으로 지정하려면 *Mage.exe*의 이전 버전을 사용합니다.

기존 매니페스트에 어셈블리를 추가하거나 제거 또는 기존 매니페스트를 다시 서명할 때 *Mage.exe*는 매니페스트를 .NET Framework 4를 대상으로 업데이트하지 않습니다.

다음 표에서는 이러한 기능 및 제한 사항을 보여 줍니다.

|매니페스트 버전|작업|Mage v2.0|Mage v4.0|
|----------------------|---------------|---------------|---------------|
|.NET Framework 버전 2.0 또는 3.x를 대상으로 하는 애플리케이션 매니페스트|열기|확인|확인|
||닫기|확인|확인|
||저장|확인|확인|
||다시 서명|확인|확인|
||새로 만들기|확인|지원 안 함|
||업데이트(아래 참조)|확인|확인|
|.NET Framework 버전 4를 대상으로 하는 애플리케이션 매니페스트|열기|확인|확인|
||닫기|확인|확인|
||저장|확인|확인|
||다시 서명|확인|확인|
||단추를 사용하여 새|지원 안 함|확인|
||업데이트(아래 참조)|지원 안 함|확인|

|매니페스트 버전|작업 세부 정보 업데이트|Mage v2.0|Mage v4.0|
|----------------------|------------------------------|---------------|---------------|
|.NET Framework 버전 2.0 또는 3.x를 대상으로 하는 애플리케이션 매니페스트|어셈블리 수정|확인|확인|
||어셈블리 추가|확인|확인|
||어셈블리 제거|확인|확인|
|.NET Framework 버전 4를 대상으로 하는 애플리케이션 매니페스트|어셈블리 수정|지원 안 함|확인|
||어셈블리 추가|지원 안 함|확인|
||어셈블리 제거|지원 안 함|확인|

 Mage.exe는 [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]대상으로 새 매니페스트를 만듭니다. [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)] 대상의 ClickOnce 애플리케이션은 [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)] 및 전체 버전의 .NET Framework 4에서 실행할 수 있습니다. 애플리케이션이 전체 버전의 .NET Framework 4를 대상으로 하며 [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]에서 실행할 수 없는 경우 텍스트 편집기를 사용하여 클라이언트 `<framework>` 요소를 제거하고 매니페스트에 다시 서명합니다.

다음은 [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)] 대상으로 하는 샘플 `<framework>` 요소입니다.

```xml
<framework targetVersion="4.0" profile="client" supportedRuntime="4.0.20506" />
```

## <a name="examples"></a>예

다음 예제에서는 Mage(*MageUI.exe*)의 사용자 인터페이스를 엽니다.

```console
mage
```

다음 예제에서는 기본 배포 매니페스트 및 애플리케이션 매니페스트를 만듭니다. 이러한 파일은 현재 작업 디렉터리에 각각 deploy.application 및 application.exe.manifest라는 이름으로 만들어집니다.

```console
mage -New Deployment
mage -New Application
```

다음 예제에서는 현재 디렉터리의 모든 어셈블리 및 리소스 파일로 채워진 애플리케이션 매니페스트를 만듭니다.

```console
mage -New Application -FromDirectory . -Version 1.0.0.0
```

다음 예제에서는 배포 이름 및 대상 마이크로프로세서를 지정하여 이전 예제를 계속 진행합니다. 또한 ClickOnce에서 업데이트를 확인할 URL을 지정합니다.

```console
mage -New Application -FromDirectory . -Name "Hello, World! Application" -Version 1.0.0.0 -Processor "x86" -ProviderUrl http://internalserver/HelloWorld/
```

다음 예제에서는 Internet Explorer에 호스팅되는 WPF 애플리케이션을 배포하기 위한 매니페스트 쌍을 만드는 방법을 보여 줍니다.

```console
mage -New Application -FromDirectory . -Version 1.0.0.0 -WPFBrowserApp true
mage -New Deployment -AppManifest 1.0.0.0\application.manifest -WPFBrowserApp true
```

다음 예제에서는 현재 디렉터리의 모든 어셈블리 및 리소스 파일로 채워진 애플리케이션 매니페스트를 만들고 서명합니다.

```console
mage -New Application -FromDirectory . -Version 1.0.0.0 -KeyContainer keypair.snk -CryptoProvider "Microsoft Enhanced Cryptographic Provider v1.0"
```

다음 예제에서는 애플리케이션 매니페스트에서 가져온 정보로 배포 매니페스트를 업데이트하고 애플리케이션 매니페스트의 위치에 대한 코드베이스를 설정합니다.

```console
mage -Update HelloWorld.deploy -AppManifest 1.0.0.0\application.manifest -AppCodeBase http://internalserver/HelloWorld.deploy
```

다음 예제에서는 사용자가 설치한 버전에 업데이트를 적용하도록 배포 매니페스트를 편집합니다.

```console
mage -Update c:\HelloWorldDeployment\HelloWorld.deploy -MinVersion 1.1.0.0
```

다음 예제에서는 다른 디렉터리에서 애플리케이션 매니페스트를 검색하도록 배포 매니페스트를 설정합니다.

```console
mage -Update HelloWorld.deploy -AppCodeBase http://anotherserver/HelloWorld/1.1.0.0/
```

다음 예제에서는 현재 작업 디렉터리에 있는 디지털 인증서를 사용하여 기존 배포 매니페스트에 서명합니다.

```console
mage -Sign deploy.application -CertFile cert.pfx -Password <passwd>
```

다음 예제에서는 현재 작업 디렉터리에 있는 디지털 인증서 및 프라이빗 키를 사용하여 기존 배포 매니페스트에 서명합니다.

```console
mage -Sign deploy.application -CertFile cert.pfx -KeyContainer keyfile.snk -CryptoProvider "Microsoft Enhanced Cryptographic Provider v1.0"
```

## <a name="see-also"></a>참고 항목

- [ClickOnce 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)
- [연습: 수동으로 ClickOnce 애플리케이션 배포](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)
- [신뢰할 수 있는 애플리케이션 배포 개요](/visualstudio/deployment/trusted-application-deployment-overview)
- [MageUI.exe(매니페스트 생성 및 편집 도구, 그래픽 클라이언트)](mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
