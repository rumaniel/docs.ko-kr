---
title: 개발자를 위한 .NET Framework 배포 가이드
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- developer's guide, deploying .NET Framework
- deployment [.NET Framework], developer's guide
ms.assetid: 094d043e-33c4-40ba-a503-e0b20b55f4cf
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dbb196b5beb2fc04ff85f2924356699fd83f3ea6
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833667"
---
# <a name="net-framework-deployment-guide-for-developers"></a>개발자를 위한 .NET Framework 배포 가이드
이 항목에서는 앱과 함께 .NET Framework 4.5에서 [!INCLUDE[net_current](../../../includes/net-current-version.md)] 사이의 .NET Framework 버전을 설치하려는 개발자를 위한 정보를 제공합니다.

다운로드 링크를 확인하려면 [재배포 가능 패키지](#redistributable-packages) 섹션을 참조하세요. 재배포 가능 패키지 및 언어 팩은 다음 Microsoft 다운로드 센터 페이지에서 다운로드할 수도 있습니다.

- 모든 운영 체제용 .NET Framework 4.8([웹 설치 관리자](http://go.microsoft.com/fwlink/?LinkId=2085155) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2088631))

- 모든 운영 체제용 .NET Framework 4.7.2([웹 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=863262) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=863265))

- 모든 운영 체제용 .NET Framework 4.7.1([웹 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=852095) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=852107))

- 모든 운영 체제용 .NET Framework 4.7([웹 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=825299) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=825303))

- 모든 운영 체제용 .NET Framework 4.6.2([웹 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=780597) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=780601))

- 모든 운영 체제용 .NET Framework 4.6.1([웹 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=671729) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=671744))

- 모든 운영 체제용 .NET Framework 4.6([웹 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=528222) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=528232))

- 모든 운영 체제용 .NET Framework 4.5.2([웹 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=397703) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=397706))

- 모든 운영 체제용 .NET Framework 4.5.1([웹 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=310158) 또는 [오프라인 설치 관리자](https://go.microsoft.com/fwlink/p/?LinkId=310159))

- [.NET Framework 4.5](https://go.microsoft.com/fwlink/p/?LinkId=245484)

 유의 사항:

> [!NOTE]
> “.NET Framework 4.5 및 해당 포인트 릴리스”라는 구는 .NET Framework 4.5 및 모든 이후 버전을 의미합니다.

- .NET Framework 4.5.1에서 [!INCLUDE[net_current](../../../includes/net-current-version.md)] 사이의 .NET Framework 버전은 .NET Framework 4.5의 내부 업데이트입니다. 즉, 같은 런타임 버전을 사용하지만 어셈블리 버전이 업데이트되어 새 형식과 멤버를 포함합니다.

- .NET Framework 4.5 및 해당 포인트 릴리스는 .NET Framework 4에서 증분 방식으로 빌드됩니다. .NET Framework 4가 설치되어 있는 시스템에 .NET Framework 4.5 또는 해당 포인트 릴리스를 설치하면 버전 4 어셈블리가 최신 버전으로 바뀝니다.

- 앱에서 Microsoft [번외 패키지](../get-started/the-net-framework-and-out-of-band-releases.md) 를 참조하는 경우 어셈블리가 앱 패키지에 포함됩니다.

- .NET Framework 4.5 및 해당 포인트 릴리스를 설치하려면 관리자 권한이 있어야 합니다.

- [!INCLUDE[win8](../../../includes/win8-md.md)] 및 [!INCLUDE[winserver8](../../../includes/winserver8-md.md)]에는 .NET Framework 4.5가 포함되어 있으므로, 해당 운영 체제에서는 앱과 함께 배포할 필요가 없습니다. 마찬가지로, [!INCLUDE[win81](../../../includes/win81-md.md)] 및 Windows Server 2012 R2에는 .NET Framework 4.5.1이 포함되어 있습니다. .NET Framework 4.5.2는 어떤 운영 체제에도 포함되어 있지 않습니다. .NET Framework 4.6은 Windows 10, .NET Framework 4.6.1은 Windows 10의 11월 업데이트, .NET Framework 4.6.2는 Windows 10의 1주년 업데이트에 각각 포함되어 있습니다.  .NET Framework 4.7은 Windows 10 크리에이터스 업데이트, .NET Framework 4.7.1은 Windows 10 Fall Creators Update, .NET Framework 4.7.2는 Windows 10 2018년 10월 업데이트와 Windows 10 2018년 4월 업데이트에 각각 포함되어 있습니다. .NET Framework 4.8은 Windows 10 2019년 5월 업데이트에 포함되어 있습니다. 하드웨어 및 소프트웨어 요구 사항의 전체 목록은 [시스템 요구 사항](../get-started/system-requirements.md)을 참조하세요.

- .NET Framework 4.5부터, 사용자는 설치하는 동안 실행 중인 .NET Framework 앱 목록을 보고 쉽게 닫을 수 있습니다. 이렇게 하면 .NET Framework 설치로 인해 시스템이 다시 시작되는 것을 방지할 수 있습니다. [시스템 다시 시작 사례 감소](reducing-system-restarts.md)를 참조하세요.

- .NET Framework 4.5 또는 해당 포인트 릴리스 중 하나를 제거하면 기존의 .NET Framework 4 파일도 제거됩니다. .NET Framework 4로 돌아가려면 해당 프로그램과 모든 업데이트를 다시 설치해야 합니다. [.NET Framework 4 설치](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5a4x27ek(v=vs.100))를 참조하세요.

- .NET Framework 4.5 재배포 가능 패키지는 Microsoft에서 생성 및 서명된 파일의 디지털 서명이 중간에 만료되도록 한 디지털 서명의 부적절한 타임스탬프 관련 문제를 해결하기 위해 2012년 10월 9일 업데이트되었습니다. 이전에 2012년 8월 16일자 .NET Framework 4.5 재배포 가능 패키지를 설치한 경우 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkId=245484)에서 최신 재배포 가능 패키지로 업데이트하는 것이 좋습니다. 이 문제에 대한 자세한 내용은 [Microsoft 보안 공지 2749655](https://docs.microsoft.com/security-updates/SecurityAdvisories/2012/2749655)를 참조하세요.

시스템 관리자가 .NET Framework 및 시스템 종속성을 네트워크에 배포하는 방법에 대한 자세한 내용은 [관리자용 배포 가이드](guide-for-administrators.md)를 참조하세요.

## <a name="deployment-options-for-your-app"></a>앱용 배포 옵션

응용 프로그램을 사용자가 설치할 수 있도록 웹 서버나 다른 중앙 위치에 게시할 준비가 되면 몇 가지 배포 방법 중에서 선택할 수 있습니다. 이러한 방법 중 몇 가지는 Visual Studio에서 제공됩니다. 다음 표에는 앱의 배포 옵션이 나열되어 있고 각 옵션을 지원하는 .NET Framework 재배포 가능 패키지가 지정되어 있습니다. 또한 응용 프로그램을 위한 사용자 지정 설치 프로그램을 작성할 수 있습니다. 자세한 내용은 [응용 프로그램 설치를 위해 .NET Framework 설치 연결](#chaining)섹션을 참조하세요.

|응용 프로그램용 배포 전략|사용 가능한 배포 방법|사용할 .NET Framework 재배포 가능 패키지|
|--------------------------------------|----------------------------------|-------------------------------------------|
|웹에서 설치|- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [WiX 도구 집합](#wix)<br />- [수동 설치](#installing_manually)|[Web installer](#redistributable-packages)|
|디스크에서 설치|- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [WiX 도구 집합](#wix)<br />- [수동 설치](#installing_manually)|[Offline installer](#redistributable-packages)|
|LAN(Local Area Network)(엔터프라이즈 앱용)에서 설치|- [ClickOnce](#clickonce-deployment)|[웹 설치 관리자](#redistributable-packages) (제한의 경우 [ClickOnce](#clickonce-deployment) 참조) 또는 [오프라인 설치 관리자](#redistributable-packages)|

## <a name="redistributable-packages"></a>재배포 가능 패키지

.NET Framework에서는 두 개의 재배포 가능 패키지인 웹 설치 관리자(부트스트래퍼) 및 오프라인 설치 관리자(독립 실행형 재배포 가능 패키지)를 사용할 수 있습니다. 다음 표에서는 두 개의 패키지를 비교합니다.

||웹 설치 관리자|오프라인 설치 관리자|
|-|-------------------|-----------------------|
|파일 다운로드|.NET Framework 4.8: <br/>[ndp48-web.exe](https://go.microsoft.com/fwlink/?LinkId=2085155)<br/><br/>.NET Framework 4.7.2: <br/>[NDP472-KB4054531-Web.exe](https://go.microsoft.com/fwlink/?LinkId=863262)<br/><br/>.NET Framework 4.7.1: <br/>[NDP471-KB4033344-Web.exe](https://go.microsoft.com/fwlink/?LinkId=852092)<br/><br/>.NET Framework 4.7: <br />[NDP47-KB3186500-Web.exe](https://go.microsoft.com/fwlink/?LinkId=825298) <br /><br />.NET Framework 4.6.2: <br />[NDP462-KB3151802-Web.exe](https://go.microsoft.com/fwlink/?LinkId=780596)<br /><br /> .NET Framework 4.6.1:<br />[NDP461-KB3102438-Web.exe](https://go.microsoft.com/fwlink/?LinkId=671728)<br /><br /> .NET Framework 4.6:<br />[NDP46-KB3045560-Web.exe](https://go.microsoft.com/fwlink/?LinkId=528222)<br /><br /> .NET Framework 4.5.2: <br />[NDP452-KB2901954-Web.exe](https://go.microsoft.com/fwlink/?LinkId=397707)<br /><br /> .NET Framework 4.5.1: <br />[NDP451-KB2859818-Web.exe](https://go.microsoft.com/fwlink/?LinkId=322115)<br /><br /> .NET Framework 4.5: <br />[dotNetFx45_Full_setup.exe](https://go.microsoft.com/fwlink/?LinkId=225704)|.NET Framework 4.8: <br/>[NDP48-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?linkid=2088631)<br/><br/>.NET Framework 4.7.2: <br/>[NDP472-KB4054530-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=863265)<br/><br/>.NET Framework 4.7.1: <br />[NDP471-KB4033342-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=852104) <br /><br />.NET Framework 4.7: <br />[NDP47-KB3186497-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=825302) <br /><br />.NET Framework 4.6.2: <br />[NDP462-KB3151800-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=780600)<br /><br /> .NET Framework 4.6.1: <br />[NDP461-KB3102436-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=671743)<br /><br /> .NET Framework 4.6: <br />[NDP46-KB3045557-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=528232)<br /><br /> .NET Framework 4.5.2: <br />[NDP452-KB2901907-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=397708)<br /><br /> .NET Framework 4.5.1: <br />[NDP451-KB2858728-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=322116)<br /><br /> .NET Framework 4.5: <br />[dotNetFx45_Full_x86_x64.exe](https://go.microsoft.com/fwlink/?LinkId=225702)|
|인터넷 연결 여부|예|아니요|
|다운로드 크기|작게(대상 플랫폼의 설치 관리자만 포함) *|크게*|
|언어 팩|포함됨**|반드시 [별도로 설치](#chain_langpack)합니다. 그러지 않으면, 모든 운영 체제를 대상으로 하는 패키지를 사용합니다.|
|배포 방법|모든 메서드 지원:<br /><br />- [ClickOnce](#clickonce-deployment)<br />- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [WiX(Windows Installer XML)](#wix)<br />- [수동 설치](#installing_manually)<br />- [사용자 지정 설치(연결)](#chaining)|모든 메서드 지원:<br /><br /> - [ClickOnce](#clickonce-deployment)<br />- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [WiX(Windows Installer XML)](#wix)<br />- [수동 설치](#installing_manually)<br />- [사용자 지정 설치(연결)](#chaining)|
|ClickOnce 배포를 위한 다운로드 위치|Microsoft 다운로드 센터:<br /><br /> - [.NET Framework 4.8](https://go.microsoft.com/fwlink/?LinkId=2085155) <br/> - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/?LinkId=863262) <br/> - [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/?LinkId=852092) <br/> - [.NET Framework 4.7](https://go.microsoft.com/fwlink/?LinkId=825298) <br/> - [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/?LinkId=780596)<br />- [.NET Framework 4.6.1](https://go.microsoft.com/fwlink/?LinkId=671728)<br />- [.NET Framework 4.6](https://go.microsoft.com/fwlink/?LinkId=528222)<br />- [.NET Framework 4.5.2](https://go.microsoft.com/fwlink/?LinkId=397703)<br />- [.NET Framework 4.5.1](https://go.microsoft.com/fwlink/p/?LinkId=310158)<br />- [.NET Framework 4.5](https://go.microsoft.com/fwlink/p/?LinkId=245484)|사용자의 서버 또는 Microsoft 다운로드 센터:<br /><br /> - [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088631)<br /> - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/?LinkId=863265)<br /> - [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/?LinkId=852104)<br /> - [.NET Framework 4.7](https://go.microsoft.com/fwlink/?LinkId=825302)<br /> - [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/?LinkId=780600)<br />- [.NET Framework 4.6.1](https://go.microsoft.com/fwlink/?LinkId=671743)<br />- [.NET Framework 4.6](https://go.microsoft.com/fwlink/?LinkId=528232)<br />- [.NET Framework 4.5.2](https://go.microsoft.com/fwlink/p/?LinkId=397706)<br />- [.NET Framework 4.5.1](https://go.microsoft.com/fwlink/p/?LinkId=310159)<br />- [.NET Framework 4.5](https://go.microsoft.com/fwlink/p/?LinkId=245484)|

\* 오프라인 설치 관리자는 모든 대상 플랫폼의 구성 요소를 포함하기 때문에 더 큽니다. 설치 프로그램의 실행을 마치면 Windows 운영 체제에서는 사용한 설치 관리자만 캐시합니다. 설치 후에 오프라인 설치 관리자를 삭제하는 경우 사용된 디스크 공간은 웹 설치 관리자에서 사용하는 것과 동일합니다. 앱의 설치 프로그램을 만드는 데 사용하는 도구(예: [InstallAware](#installaware-deployment) 또는 [InstallShield](#installshield-deployment))가 설치 후에 제거되는 설치 파일 폴더를 제공하는 경우 오프라인 설치 관리자를 설치 폴더에 저장하여 자동으로 삭제할 수 있습니다.

\*\* 사용자 지정 설치로 웹 설치 관리자를 사용하는 경우 사용자의 MUI(다국어 사용자 인터페이스) 설정을 기준으로 기본 언어 설정을 사용하거나, 명령줄에서 `/LCID` 옵션을 사용하여 다른 언어 팩을 지정할 수 있습니다. 자세한 내용은 [기본 .NET Framework UI를 사용하여 연결](#chaining_default) 섹션을 참조하세요.

## <a name="deployment-methods"></a>배포 방법

 사용 가능한 네 가지 배포 방법은 다음과 같습니다.

- .NET Framework에 대한 종속성을 설정할 수 있습니다. 다음 방법 중 하나를 사용하여 응용 프로그램 설치 시 필수 구성 요소로 .NET Framework를 지정할 수 있습니다.

  - [ClickOnce 배포](#clickonce-deployment) 사용(Visual Studio에서 사용 가능)

  - [InstallAware 프로젝트](#installaware-deployment) 만들기(Visual Studio 사용자가 사용할 수 있는 무료 버전)

  - [InstallShield 프로젝트](#installshield-deployment) 만들기(Visual Studio에서 사용 가능)

  - [WiX(Windows Installer XML) 도구 집합](#wix)사용

- 사용자에게 [.NET Framework를 수동으로 설치](#installing_manually)하도록 요청할 수 있습니다.

- 응용 프로그램의 설치 프로그램에서 .NET Framework 설치 프로세스를 연결(포함)하고 .NET Framework 설치 환경을 다루는 방법을 결정할 수 있습니다.

  - [기본 UI를 사용](#chaining_default)합니다. .NET Framework 설치 관리자에서 설치 환경을 제공하게 합니다.

  - [UI를 사용자 지정](#chaining_custom) 하여 통합된 설치 경험을 제공하고 .NET Framework 설치 진행 상황을 모니터링합니다.

이러한 배포 방법은 다음 섹션에서 자세하게 설명됩니다.

## <a name="setting-a-dependency-on-the-net-framework"></a>.NET Framework에 대한 종속성 설정

ClickOnce, InstallAware, InstallShield 또는 WiX를 사용하여 앱을 배포하는 경우 앱의 일부로 설치될 수 있도록 .NET Framework에 대한 종속성을 추가할 수 있습니다.

### <a name="clickonce-deployment"></a>ClickOnce 배포

ClickOnce 배포는 Visual Basic, Visual C# 및 Visual J#을 사용하여 만들어진 프로젝트에 사용할 수 있지만 Visual C++로 만든 프로젝트에는 사용할 수 없습니다.

Visual Studio에서 ClickOnce 배포를 선택하고 .NET Framework에 대한 종속성을 추가합니다.

1. 게시하려는 응용 프로그램 프로젝트를 엽니다.

2. 솔루션 탐색기에서 프로젝트의 바로 가기 메뉴를 열고 **속성**을 선택합니다.

3. **게시** 창을 선택합니다.

4. **필수 구성 요소** 단추를 선택합니다.

5. **필수 구성 요소** 대화 상자에서 **필수 구성 요소를 설치하기 위한 설치 프로그램 만들기** 확인란이 선택되어 있는지 확인합니다.

6. 필수 구성 요소 목록에서 프로젝트를 빌드하는 데 사용한 .NET Framework 버전을 찾아서 선택합니다.

7. 필수 구성 요소의 소스 위치를 지정하는 옵션을 선택한 다음 **확인**을 선택합니다.

     .NET Framework 다운로드 위치의 URL을 제공하는 경우 Microsoft 다운로드 센터 사이트 또는 자체 사이트를 지정할 수 있습니다. 재배포 가능 패키지를 자체 서버에 배치하려면 패키지가 웹 설치 관리자가 아닌 오프라인 설치 관리자여야 합니다. Microsoft 다운로드 센터에 있는 웹 설치 관리자에만 연결할 수 있습니다. URL은 사용자 응용 프로그램을 배포할 CD를 지정할 수도 있습니다.

8. **속성 페이지** 대화 상자에서 **확인**을 선택합니다.

<a name="installaware"></a>

### <a name="installaware-deployment"></a>InstallAware 배포

InstallAware는 단일 소스에서 Windows 앱(APPX), Windows Installer(MSI), 네이티브 코드(EXE) 및 App-V(Application Virtualization) 패키지를 빌드합니다. 설치 프로그램에 쉽게 [원하는 버전의 .NET Framework를 포함](https://www.installaware.com/one-click-pre-requisite-installer.htm)하여, 필요에 따라 [기본 스크립트를 편집](https://www.installaware.com/msicode.htm)함으로써 설치를 사용자 지정할 수 있습니다. 예를 들어 InstallAware는 Windows 7에 인증서를 미리 설치하여 .NET Framework 4.7 설치가 실패하지 않도록 방지합니다. InstallAware에 대한 자세한 내용은 [Windows Installer용 InstallAware](https://www.installaware.com/) 웹 사이트를 참조하세요.

### <a name="installshield-deployment"></a>InstallShield 배포

Visual Studio에서 InstallShield 배포를 선택하고 .NET Framework에 대한 종속성을 추가합니다.

1. Visual Studio 메뉴 모음에서 **파일**, **새로 만들기**, **프로젝트**를 선택합니다.

2. **새 프로젝트** 대화 상자의 왼쪽 창에서 **기타 프로젝트 형식**, **설치 및 배포**, **InstallShield LE**를 선택합니다.

3. **이름** 상자에 프로젝트 이름을 입력한 다음 **확인**을 선택합니다.

4. 설치 및 배포 프로젝트를 처음으로 만들 경우 **InstallShield로 이동** 또는 **InstallShield Limited Edition 사용**을 선택하여 사용 중인 Microsoft Visual Studio 버전의 InstallShield Limited Edition을 다운로드합니다. Visual Studio를 다시 시작합니다.

5. **프로젝트 도우미** 마법사로 이동한 다음 **애플리케이션 파일** 을 선택하여 프로젝트 출력을 추가합니다. 이 마법사를 사용하여 다른 프로젝트 특성을 구성할 수 있습니다.

6. **설치 요구 사항** 으로 이동한 다음 운영 체제 및 설치할 .NET Framework의 버전을 선택합니다.

7. 설치 프로젝트에 대한 바로 가기 메뉴를 열고 **빌드**를 선택합니다.

<a name="wix"></a>

### <a name="windows-installer-xml-wix-deployment"></a>WiX(Windows Installer XML) 배포

WiX(Windows Installer XML) 도구 집합은 XML 소스 코드에서 Windows 설치 패키지를 빌드합니다. WiX는 MSI 및 MSM 설치 패키지를 빌드하기 위해 빌드 프로세스로 통합할 수 있는 명령줄 환경을 지원합니다. WiX를 사용하여 .NET Framework 배포 환경을 완벽하게 제어하기 위해 [.NET Framework를 필수 조건으로 지정](http://wixtoolset.org/documentation/manual/v3/howtos/redistributables_and_install_checks/install_dotnet.html)하거나 [chainer를 만들](http://wixtoolset.org/documentation/manual/v3/xsd/wix/exepackage.html) 수 있습니다. WiX에 대한 자세한 내용은 [WiX(Windows Installer XML) 도구 집합](http://wixtoolset.org/) 웹 사이트를 참조하세요.

<a name="installing_manually"></a>

## <a name="installing-the-net-framework-manually"></a>.NET Framework 수동 설치

.NET Framework를 응용 프로그램과 함께 자동으로 설치하는 것이 적절하지 않은 경우도 있습니다. 이 경우 사용자가 .NET Framework를 직접 설치하도록 할 수 있습니다. 재배포 가능 패키지는 [두 패키지](#redistributable-packages)에서 사용할 수 있습니다. .NET Framework를 찾아서 설치하는 방법에 대한 지침을 설치 프로세스에서 제공하는 것이 좋습니다.

<a name="chaining"></a>

## <a name="chaining-the-net-framework-installation-to-your-apps-setup"></a>응용 프로그램 설치를 위해 .NET Framework 설치 연결

응용 프로그램의 사용자 지정 설치 프로그램을 만드는 경우 응용 프로그램의 설치 프로세스에 .NET Framework 설치 프로세스를 연결(포함)할 수 있습니다. 연결 시 .NET Framework 설치를 위해 두 개의 UI 옵션 제공:

- .NET Framework 설치 관리자에 의해 제공된 기본 UI를 사용합니다.

- 응용 프로그램의 설치 프로그램과 일관되도록 .NET Framework 설치용 사용자 지정 UI를 만듭니다.

두 방법 모두 웹 설치 관리자 또는 오프라인 설치 관리자를 사용할 수 있습니다. 각 패키지의 장점은 다음과 같습니다.

- 웹 설치 관리자를 사용하는 경우 .NET Framework 설치 프로세스에서 필요한 설치 패키지를 판단하고 웹에서 해당 패키지만 다운로드하고 설치합니다.

- 오프라인 설치 관리자를 사용하는 경우 사용자가 설치 도중 웹에서 파일을 추가로 다운로드할 필요가 없도록 재배포 미디어에 전체 .NET Framework 설치 패키지 집합을 포함할 수 있습니다.

<a name="chaining_default"></a>

### <a name="chaining-by-using-the-default-net-framework-ui"></a>기본 .NET Framework UI를 사용하여 연결

.NET Framework 설치 프로세스를 자동으로 연결하고 .NET Framework 설치 관리자에서 UI를 제공하도록 하려면 다음 명령을 설치 프로그램에 추가합니다.

`<.NET Framework redistributable> /q /norestart /ChainingPackage <PackageName>`

예를 들어 실행 프로그램이 Contoso.exe이고 .NET Framework 4.5 오프라인 재배포 가능 패키지를 자동으로 설치하려는 경우 다음 명령을 사용합니다.

`dotNetFx45_Full_x86_x64.exe /q /norestart /ChainingPackage Contoso`

추가 명령줄 옵션을 사용하여 설치를 사용자 지정할 수 있습니다. 예:

- 사용자가 실행 중인 .NET Framework 응용 프로그램을 닫아 시스템이 다시 시작되는 경우를 최소화하려면 다음과 같이 Passive 모드를 설정하고 `/showrmui` 옵션을 사용합니다.

    `dotNetFx45_Full_x86_x64.exe /norestart /passive /showrmui /ChainingPackage Contoso`

     이 명령을 사용하면 다시 시작 관리자가 .NET Framework를 설치하기 전에 .NET Framework 앱을 닫을 기회를 사용자에게 제공하는 메시지 상자를 표시할 수 있습니다.

- 웹 설치 관리자를 사용하는 경우 `/LCID` 옵션을 사용하여 언어 팩을 지정할 수 있습니다. 예를 들어 .NET Framework 4.5 웹 설치 관리자를 Contoso 설치 프로그램에 연결하고 일본어 언어 팩을 설치하려면 앱의 설치 프로세스에 다음 명령을 추가합니다.

    `dotNetFx45_Full_setup.exe /q /norestart /ChainingPackage Contoso /LCID 1041`

     `/LCID` 옵션을 생략하는 경우 설치 프로그램은 사용자의 MUI 설정과 일치하는 언어 팩을 설치합니다.

    > [!NOTE]
    > 언어 팩에 따라 릴리스 날짜가 서로 다를 수 있습니다. 지정한 언어 팩을 다운로드 센터에서 사용할 수 없는 경우 설치 프로세스는 언어 팩 없이 .NET Framework를 설치합니다. .NET Framework가 사용자의 컴퓨터에 이미 설치되어 있는 경우에는 언어 팩만 설치됩니다.

전체 옵션 목록은 [명령줄 옵션](#command-line-options) 섹션을 참조하세요.

일반적인 반환 코드에 대한 자세한 내용은 [반환 코드](#return-codes) 섹션을 참조하세요.

<a name="chaining_custom"></a>

### <a name="chaining-by-using-a-custom-ui"></a>사용자 지정 UI를 사용하여 연결

사용자 지정 설치 패키지가 있는 경우 설치 진행 상황을 자체적으로 표시하면서 .NET Framework 설치를 자동으로 시작하고 추적할 수 있습니다. 이 경우 코드가 다음을 충족하도록 해야 합니다.

- [.NET Framework 하드웨어 및 소프트웨어 요구 사항](../get-started/system-requirements.md)을 확인합니다.

- .NET Framework의 올바른 버전이 사용자 컴퓨터에 이미 설치되어 있는지 여부를[감지](#detect_net) 합니다.

    > [!IMPORTANT]
    > 올바른 버전의 .NET Framework가 설치되어 있는지 확인할 때, 대상 버전의 설치 여부가 아니라 대상 버전 *또는* 이후 버전이 설치되어 있는지를 확인해야 합니다. 즉, 레지스트리에서 검색한 릴리스 키가 대상 버전의 릴리스 키와 같은지가 *아니라* 대상 버전의 릴리스 키보다 크거나 같은지를 확인해야 합니다.

- 언어 팩이 사용자 컴퓨터에 이미 설치되어 있는지 여부를[감지](#detecting-the-language-packs) 합니다.

- 배포를 제어하려면 .NET Framework 설치 프로세스를 자동으로 시작하고 추적합니다([방법: .NET Framework 4.5 설치 관리자에서 진행률 가져오기](how-to-get-progress-from-the-dotnet-installer.md) 참조).

- 오프라인 설치 관리자를 배포 중인 경우 [언어 팩을 별도로 연결](#chain_langpack)합니다.

- [명령줄 옵션](#command-line-options)을 사용하여 배포를 사용자 지정합니다. 예를 들어 .NET Framework 웹 설치 관리자를 연결하고 있지만 기본 언어 팩을 재정의하려는 경우 앞 섹션에서 설명하는 대로 `/LCID` 옵션을 사용하세요.

- [문제 해결](#troubleshooting)

<a name="detect_net"></a>

### <a name="detecting-the-net-framework"></a>.NET Framework 검색

.NET Framework 설치 관리자는 설치가 성공적으로 이루어지면 레지스트리 키를 씁니다. 이름이 `Release`인 `DWORD` 값에 대해 레지스트리의 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full` 폴더를 확인하여 .NET Framework 4.5 이상이 설치되어 있는지 테스트할 수 있습니다. ("NET Framework Setup"은 마침표로 시작되지 않습니다.) 이 키가 있으면 해당 컴퓨터에 .NET Framework 4.5 이상 버전이 설치되어 있는 것입니다. `Release` 의 값은 어떤 .NET Framework 버전이 설치되었는지를 나타냅니다.

> [!IMPORTANT]
> 특정 버전이 있는지 여부를 검색할 때는 값이 릴리스 키워드 값  **보다 크거나 같은지** 를 확인해야 합니다.

[!INCLUDE[Release key values note](~/includes/version-keys-note.md)]

|버전|릴리스 DWORD의 값|
|-------------|--------------------------------|
|Windows 10 2019년 5월 업데이트에 설치된 .NET Framework 4.8|528040|
|Windows 10 2019년 5월 업데이트 이외의 모든 OS 버전에 설치된 .NET Framework 4.8|528049|
|Windows 10 2018년 4월 업데이트 및 Windows Server, 버전 1803에 설치된 .NET Framework 4.7.2|461808|
|Windows 10 2018년 4월 업데이트 및 Windows Server, 버전 1803 이외의 모든 OS 버전에 설치된 .NET Framework 4.7.2. 여기에는 Windows 10 2018년 10월 업데이트가 포함됩니다. |461814|
|Windows 10 Fall Creators Update 및 Windows Server, 버전 1709에 설치된 .NET Framework 4.7.1|461308|
|Windows 10 Fall Creators Update 및 Windows Server, 버전 1709 이외의 모든 OS 버전에 설치된 .NET Framework 4.7.1|461310|
|.NET Framework 4.7이 Windows 10 크리에이터 업데이트에 설치됨|460798|
|Windows 10 크리에이터스 업데이트 이외의 모든 OS 버전에 설치된 .NET Framework 4.7|460805|
|Windows 10 Anniversary Edition 및 Windows Server 2016에 설치된 .NET Framework 4.6.2|394802|
|Windows 10 Anniversary Edition 및 Windows Server 2016 이외의 모든 OS 버전에 설치된 .NET Framework 4.6.2|394806|
|Windows 10 11월 업데이트에 설치된 .NET Framework 4.6.1|394254|
|Windows 10 11월 업데이트 이외의 모든 OS 버전에 설치된 .NET Framework 4.6.1|394271|
|Windows 10에 설치된 .NET Framework 4.6|393295|
|Windows 10 이외의 모든 OS 버전에 설치된 .NET Framework 4.6|393297|
|.NET Framework 4.5.2|379893|
|[!INCLUDE[win81](../../../includes/win81-md.md)] 또는 Windows Server 2012 R2와 함께 설치된 .NET Framework 4.5.1|378675|
|[!INCLUDE[win8](../../../includes/win8-md.md)], Windows 7에 설치된 .NET Framework 4.5.1|378758|
|.NET Framework 4.5|378389|

### <a name="detecting-the-language-packs"></a>언어 팩 검색

이름이 `Release`인 DWORD 값의 레지스트리에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full\\*LCID* 폴더를 확인하여 특정 언어 팩이 설치되어 있는지 여부를 테스트할 수 있습니다. ("NET Framework Setup"은 마침표로 시작되지 않습니다.) *LCID*는 로캘 식별자를 지정합니다. 로캘 식별자 목록은 [지원되는 언어](#supported-languages)를 참조하세요.

예를 들어 전체 일본어 언어 팩(LCID=1041)이 설치되어 있는지 검색하려면 레지스트리에서 다음 명명된 값을 검색합니다.

| | |
|-|-|
| 키 | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full\1041 |
| name | Release |
| 형식 | DWORD |

4\.5~4.7.2의 특정 버전의 .NET Framework에 대해 최종 릴리스 버전의 언어 팩이 설치되었는지를 확인하려면 이전 섹션인 [.NET Framework 검색](#detect_net)에 설명된 릴리스 키 DWORD의 값을 확인하세요.

<a name="chain_langpack"></a>

### <a name="chaining-the-language-packs-to-your-app-setup"></a>응용 프로그램 설치 프로그램에 언어 팩 연결

.NET Framework에서는 특정 문화권에 맞게 지역화된 리소스를 포함하는 독립 실행형 언어 팩 실행 파일의 집합을 제공합니다. 언어 팩은 Microsoft 다운로드 센터에 있습니다.

- [.NET Framework 4.8 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=2086170)

- [.NET Framework 4.7.2 언어 팩](https://go.microsoft.com/fwlink/?LinkId=863275)

- [.NET Framework 4.7.1 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=852090)

- [.NET Framework 4.7 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=825306)

- [.NET Framework 4.6.2 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=780604)

- [.NET Framework 4.6.1 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=671747)

- [.NET Framework 4.6 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=528314)

- [.NET Framework 4.5.2 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=397701)

- [.NET Framework 4.5.1 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=322101)

- [.NET Framework 4.5 언어 팩](https://go.microsoft.com/fwlink/p/?LinkId=245451)

> [!IMPORTANT]
> 언어 팩에는 응용 프로그램을 실행하는 데 필요한 .NET Framework 구성 요소가 포함되지 않으므로 언어 팩을 설치하기 전에 웹 또는 오프라인 설치 관리자를 사용하여 .NET Framework를 설치해야 합니다.

.NET Framework 4.5.1부터 패키지 이름은 NDP<`version`>-KB<`number`>-x86-x64-AllOS-<`culture`>.exe 양식을 사용합니다. 여기서 `version`은 .NET Framework의 버전 번호이고, `number`는 Microsoft 기술 자료 문서 번호이며, `culture`는 [국가/지역](#supported-languages)을 지정합니다. 이러한 패키지 중 하나의 예는 `NDP452-KB2901907-x86-x64-AllOS-JPN.exe`입니다. 패키지 이름은 이 문서 앞부분의 [Redistributable Packages](#redistributable-packages) 섹션에 나열되어 있습니다.

.NET Framework 오프라인 설치 관리자를 사용하여 언어 팩을 설치하려면 해당 설치 관리자를 응용 프로그램의 설치 프로그램에 연결해야 합니다. 예를 들어 .NET Framework 4.5.1 오프라인 설치 관리자를 일본어 언어 팩과 함께 배포하려면 다음 명령을 사용합니다.

`NDP451-KB2858728-x86-x64-AllOS-JPN.exe /q /norestart /ChainingPackage <ProductName>`

웹 설치 관리자를 사용하는 경우 언어 팩을 연결하지 않아도 됩니다. 즉, 사용자의 MUI 설정에 맞는 언어 팩이 설치됩니다. 다른 언어를 설치하려면 `/LCID` 옵션을 사용하여 언어 팩을 지정합니다.

명령줄 옵션의 전체 목록은 [명령줄 옵션](#command-line-options) 섹션을 참조하세요.

### <a name="troubleshooting"></a>문제 해결

#### <a name="return-codes"></a>반환 코드

다음 표에서는 .NET Framework 재배포 가능 설치 관리자의 가장 일반적인 반환 코드를 보여 줍니다. 반환 코드는 설치 관리자 버전에 관계없이 모두 동일합니다. 자세한 정보에 대한 링크는 다음 섹션을 참조하세요.

|반환 코드|설명|
|-----------------|-----------------|
|0|설치되었습니다.|
|1602|사용자가 설치를 취소했습니다.|
|1603|설치하는 동안 심각한 오류가 발생했습니다.|
|1641|설치를 완료하려면 컴퓨터를 다시 시작해야 합니다. 이 메시지는 설치가 성공적으로 수행되었음을 의미합니다.|
|3010|설치를 완료하려면 컴퓨터를 다시 시작해야 합니다. 이 메시지는 설치가 성공적으로 수행되었음을 의미합니다.|
|5100|사용자 컴퓨터가 시스템 요구 사항을 충족하지 못합니다.|

#### <a name="download-error-codes"></a>다운로드 오류 코드

다음 콘텐츠를 참조하세요.

- [BITS(Background Intelligent Transfer Service) 오류 코드](https://go.microsoft.com/fwlink/?LinkId=180946)

- [URL 모니커 오류 코드](https://go.microsoft.com/fwlink/?LinkId=180947)

- [WinHttp 오류 코드](https://go.microsoft.com/fwlink/?LinkId=180948)

#### <a name="other-error-codes"></a>기타 오류 코드

다음 콘텐츠를 참조하세요.

- [Windows Installer 오류 코드](https://go.microsoft.com/fwlink/?LinkId=180949)

- [Windows 업데이트 에이전트 결과 코드](https://go.microsoft.com/fwlink/?LinkId=180951)

## <a name="uninstalling-the-net-framework"></a>.NET Framework 제거

[!INCLUDE[win8](../../../includes/win8-md.md)]부터, 제어판의 **Windows 기능 사용/사용 안 함**을 통해 .NET Framework 4.5 또는 해당 포인트 릴리스 중 하나를 제거할 수 있습니다. 이전 버전의 Windows에서는 제어판의 **프로그램 추가/제거**를 통해 .NET Framework 4.5 또는 해당 포인트 릴리스 중 하나를 제거할 수 있습니다.

> [!IMPORTANT]
> Windows 7 및 이전 버전의 운영 체제에서 .NET Framework 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 또는 4.8을 제거하면 .NET Framework 4.5 파일이 복원되지 않고, .NET Framework 4.5를 제거하면 .NET Framework 4 파일이 복원되지 않습니다. 이전 버전으로 돌아가려면 해당 프로그램과 업데이트를 다시 설치해야 합니다.

## <a name="appendix"></a>부록

### <a name="command-line-options"></a>명령줄 옵션

다음 표에서는 .NET Framework 4.5 재배포 가능 패키지를 앱 설치에 연결할 때 포함할 수 있는 옵션을 보여 줍니다.

|옵션|설명|
|------------|-----------------|
|**/CEIPConsent**|기본 동작을 덮어쓰고 향후 배포 환경을 개선하기 위해 Microsoft에 익명으로 피드백을 보냅니다. 이 옵션은 설치 프로그램에서 사용자에게 동의를 요청하고 Microsoft로 익명 피드백을 보낼 수 있는 권한을 사용자가 부여한 경우에만 사용될 수 있습니다.|
|**/chainingpackage** `packageName`|연결을 수행하는 실행 파일의 이름을 지정합니다. 이 정보는 향후 배포 환경 개선을 지원하기 위해 익명 피드백으로 Microsoft에 보내집니다.<br /><br /> 패키지 이름에 공백이 포함되어 있으면 **/chainingpackage "Lucerne Publishing"** 과 같이 큰따옴표를 구분자로 사용합니다. 연결 패키지의 예는 MSDN 라이브러리의 [설치 패키지에서 진행 정보 가져오기](https://go.microsoft.com/fwlink/?LinkId=181926) 를 참조하세요.|
|**/LCID**  `LCID`<br /><br /> 여기서 `LCID` 는 로캘 식별자를 지정합니다( [지원되는 언어](#supported-languages)참조).|`LCID` 로 지정된 언어 팩을 설치하고 표시된 UI가 해당 언어로 표시되도록 합니다(자동 모드가 설정되어 있지 않은 경우).<br /><br /> 웹 설치 관리자에 대해 이 옵션을 사용하면 웹을 통해 언어 팩도 함께 설치됩니다. **참고:**  웹 설치 관리자에서만 이 옵션을 사용합니다.|
|**/log** `file` &#124; `folder`|로그 파일의 위치를 지정합니다. 기본값은 프로세스에 대한 임시 폴더이며 기본 파일 이름은 패키지를 기반으로 합니다. 파일 확장명이 .txt인 경우 텍스트 로그가 생성됩니다. 다른 확장명을 지정하거나 확장명을 지정하지 않는 경우 HTML 로그가 만들어집니다.|
|**/msioptions**|.msi 및 .msp 항목에 대해 전달될 옵션을 지정합니다(예: `/msioptions "PROPERTY1='Value'"`).|
|**/norestart**|설치 프로그램이 자동으로 재부팅하지 않도록 합니다. 이 옵션을 사용하는 경우 연결 응용 프로그램은 반환 코드를 캡처하고 재부팅을 처리해야 합니다. MSDN 라이브러리의 [설치 패키지에서 프로세스 진행 정보 가져오기](https://go.microsoft.com/fwlink/?LinkId=179606) 를 참조하세요.|
|**/passive**|Passive 모드를 설정합니다. 설치가 진행 중임을 나타내는 진행률 표시줄을 표시하지만 사용자에게 프롬프트 또는 오류 메시지를 표시하지는 않습니다. 이 모드에서 설치 프로그램에 의해 연결되면 연결 패키지에서 [반환 코드](#return-codes)를 처리해야 합니다.|
|**/pipe**|연결 패키지를 사용하여 진행하기 위해 통신 채널을 만듭니다.|
|**/promptrestart**|설치 프로그램을 다시 시작해야 하는 경우 수동 모드에서만 사용자에게 메시지가 표시됩니다. 이 옵션에서는 다시 시작해야 하는 경우 사용자 상호 작용이 필요합니다.|
|**/q**|자동 모드를 설정합니다.|
|**/repair**|복구 기능을 작동시킵니다.|
|**/serialdownload**|패키지가 다운로드된 후에만 강제 설치됩니다.|
|**/showfinalerror**|Passive 모드를 설정합니다. 설치가 성공적으로 완료되지 않은 경우에만 오류를 표시합니다. 설치가 성공적이 아니면 이 옵션에서는 사용자 조작이 필요합니다.|
|**/showrmui**|**/passive** 옵션에만 사용합니다. 현재 실행 중인 .NET Framework 응용 프로그램을 닫으라는 메시지 상자가 표시됩니다. 이 메시지 상자는 수동 모드와 비수동 모드에서 동일하게 작동합니다.|
|**/uninstall**|.NET Framework 재배포 가능 패키지를 제거합니다.|

### <a name="supported-languages"></a>지원되는 언어

다음 표에는 .NET Framework 4.5 및 해당 포인트 릴리스에 사용할 수 있는 .NET Framework 언어 팩이 나와 있습니다.

|인 DWORD 값의 레지스트리에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full\|언어 - 국가/지역|culture|
|----------|--------------------------------|-------------|
|1025|아랍어 - 사우디아라비아|ar|
|1028|중국어 - 번체|zh-Hant|
|1029|체코어|cs|
|1030|덴마크어|da|
|1031|독일어 - 독일|de|
|1032|그리스어|el|
|1035|핀란드어|fi|
|1036|프랑스어 - 프랑스|fr|
|1037|히브리어|he|
|1038|헝가리어|hu|
|1040|이탈리아어 - 이탈리아|it|
|1041|일본어|ja|
|1042|한국어|ko|
|1043|네덜란드어 - 네덜란드|nl|
|1044|노르웨이어(복말)|no|
|1045|폴란드어|pl|
|1046|포르투갈어 – 브라질|pt-BR|
|1049|러시아어|ru|
|1053|스웨덴어|sv|
|1055|터키어|tr|
|2052|중국어 - 간체|zh-Hans|
|2070|포르투갈어 - 포르투갈|pt-PT|
|3082|스페인어 - 스페인(현대 정렬)|es|

## <a name="see-also"></a>참고 항목

- [관리자를 위한 배포 가이드](guide-for-administrators.md)
- [시스템 요구 사항](../get-started/system-requirements.md)
- [개발자용 .NET Framework 설치](../install/guide-for-developers.md)
- [차단된 .NET Framework 설치 및 제거 문제 해결](../install/troubleshoot-blocked-installations-and-uninstallations.md)
- [.NET Framework 4.5를 설치하는 동안 시스템 다시 시작 줄이기](reducing-system-restarts.md)
- [방법: .NET Framework 4.5 설치 관리자에서 진행률 가져오기](how-to-get-progress-from-the-dotnet-installer.md)
