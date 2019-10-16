---
title: 차단된 .NET Framework 설치 및 제거 문제 해결
ms.date: 04/18/2019
ms.custom: updateeachrelease
helpviewer_keywords:
- .NET Framework, troubleshooting blocked installations
- blocked .NET Framework installations, troubleshooting
ms.assetid: c3fdfbc1-ed99-4202-a2b0-8c4f1646385d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2e932399b1d199fc69d4a541e7ee2298bc5526e2
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051914"
---
# <a name="troubleshoot-blocked-net-framework-installations-and-uninstallations"></a>차단된 .NET Framework 설치 및 제거 문제 해결

.NET Framework 4.5 이상 버전용 [웹 또는 오프라인 설치 관리자](guide-for-developers.md)를 실행할 때 .NET Framework 설치를 방해하거나 차단하는 문제가 발생할 수 있습니다. 다음 표에서는 가능한 차단 문제를 보여 주고 문제 해결 정보에 대한 링크를 제공합니다.

Windows 8 이상에서 .NET Framework는 운영 체제 구성 요소이며 독립적으로 제거할 수 없습니다. .NET Framework에 대한 업데이트는 제어판 **프로그램 및 기능** 응용 프로그램의 **설치된 업데이트** 탭에 나타납니다. .NET Framework가 사전 설치되지 않은 운영 체제의 경우, .NET Framework는 제어판의 **프로그램 및 기능** 응용 프로그램의 **제거 또는 변경 프로그램** 탭 (또는 **프로그램 추가/제거** 탭)에 나타납니다. .NET Framework가 사전 설치된 Windows 버전에 대한 자세한 내용은 [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.

> [!IMPORTANT]
> 4\.x 버전의 .NET Framework는 In-place 업데이트이기 때문에 최신 버전이 이미 설치된 시스템에 이전 버전의 .NET Framework 4.x를 설치할 수 없습니다. 예를 들어, Windows 10 Fall Creators Update 시스템에 .NET Framework 4.7.1이 운영 체제와 함께 미리 설치되어 있기 때문에, .NET Framework 4.6.2를 설치할 수 없습니다.

시스템에 설치된 .NET Framework의 버전을 확인할 수 있습니다. [방법: 설치된 .NET Framework 버전 확인](../migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요.

이 표에서 4.5.x는 .NET Framework 4.5 및 해당 포인트 릴리스 4.5.1 및 4.5.2를 참조하고, 4.6.x는 .NET Framework 4.6 및 해당 포인트 릴리스 4.6.1 및 4.6.2을 참조합니다. 4.7.x는 .NET Framework 4.7 및 해당 포인트 릴리스, 4.7.1 및 4.7.2를 참조하며 4.8은 .NET Framework 4.8을 참조합니다.

|차단 메시지|자세한 내용 또는 문제 해결 방법|  
|----------------------|--------------------------------------------------|  
|Microsoft .NET Framework를 제거하면 일부 애플리케이션의 작동이 중지될 수 있습니다.|사용하는 애플리케이션이 특정 버전의 .NET Framework에 종속될 수 있으므로 일반적으로 컴퓨터에 설치된 .NET Framework 버전을 제거해서는 안 됩니다. 자세한 내용은 *시작* 가이드의 [사용자용 .NET Framework](../get-started/index.md#ForUsers)를 참조하십시오.|  
|이 컴퓨터에 .NET Framework 4.5.x/4.6.x/4.7.x(ENU) 또는 이후 버전이 이미 설치되어 있습니다.|아무런 작업도 수행할 필요가 없습니다.<br /><br /> 시스템에 설치된 .NET Framework의 버전을 확인하려면 [방법: 설치된 .NET Framework 버전 확인](../migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요.|  
|.NET Framework 4.5.x/4.6.x/4.7.x/4.8(*언어*)에는 .NET Framework 4.5.x/4.6.x/4.7.x/4.8이 필요합니다. 다운로드 센터에서 .NET Framework 4.5.x/4.6.x/4.7.x/4.8을 설치한 후 설치 프로그램을 다시 실행하세요.|언어 팩을 설치하기 전에, 지정된 .NET Framework 릴리스의 영어 버전을 설치해야 합니다. 자세한 내용은 설치 가이드의 [언어 팩 설치](guide-for-developers.md#to-install-language-packs) 섹션을 참조하십시오.|  
|.NET Framework 4.5.x/4.6.x/4.7.x/4.8을 설치할 수 없습니다. 컴퓨터에 있는 다른 애플리케이션이 이 프로그램과 호환되지 않습니다.<br /><br /> 또는<br /><br /> 컴퓨터에 있는 다른 애플리케이션이 이 프로그램과 호환되지 않습니다.|이 메시지가 표시되는 원인은 .NET Framework의 Preview 또는 RC 버전이 설치되었기 때문일 가능성이 높습니다. Preview 또는 RC 버전을 제거하고 설치 프로그램을 다시 실행합니다.|  
|이 패키지를 사용하여 .NET Framework 4.5.x/4.6.x/4.7.x/4.8을 제거할 수 없습니다. 컴퓨터에서 .NET Framework 4.5.x/4.6.x/4.7.x/4.8을 제거하려면 **제어판**으로 이동하여 **프로그램 및 기능**, **설치된 업데이트 보기**, Microsoft Windows(KB2828152)에 대한 업데이트를 차례로 선택한 다음, **제거**를 선택합니다.|설치 패키지로는 .NET Framework의 Preview 또는 RC 릴리스를 제거할 수 없습니다.<br /><br /> 제어판에서 Preview 또는 RC 릴리스를 제거합니다.|  
|.NET Framework 4.5.x/4.6.x/4.7.x/4.8을 제거할 수 없습니다. 컴퓨터의 다른 애플리케이션이 이 프로그램에 종속되어 있습니다.|사용하는 애플리케이션이 특정 버전의 .NET Framework에 종속될 수 있으므로 일반적으로 컴퓨터에서 .NET Framework 버전을 제거해서는 안 됩니다. 자세한 내용은 *시작* 가이드의 [사용자용 .NET Framework](../get-started/index.md#ForUsers)를 참조하십시오.|  
|.NET Framework 4.5.x/4.6.x/4.7.x/4.8 재배포 가능 패키지는 이 운영 체제에 적용되지 않습니다. Microsoft 다운로드 센터에서 해당 운영 체제용 .NET Framework 4.5.x/4.6.x/4.7.x/4.8을 다운로드하세요.|지원되지 않는 플랫폼에 .NET Framework 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2 또는 4.8을 설치하려고 했거나 지원되는 모든 운영 체제에 대한 구성 요소가 포함되지 않은 설치 패키지를 선택했을 수 있습니다. 오프라인 설치 관리자([4.5.1용](https://go.microsoft.com/fwlink/p/?LinkId=309493), [4.5.2용](https://go.microsoft.com/fwlink/p/?LinkId=397706), [4.6용](https://go.microsoft.com/fwlink/p/?LinkId=528233), [4.6.1용](https://go.microsoft.com/fwlink/p/?LinkId=671744), [4.6.2용](https://go.microsoft.com/fwlink/p/?LinkId=780604), [4.7용](https://go.microsoft.com/fwlink/p/?LinkId=825306)), [4.7.1](https://go.microsoft.com/fwlink/p/?LinkId=852090)용, [4.7.2](https://go.microsoft.com/fwlink/p/?LinkId=863265)용 또는 [4.8](https://go.microsoft.com/fwlink/?linkid=2088631)용을 사용하여 설치를 다시 실행합니다. 자세한 내용은 지원되는 운영 체제의 [설치 가이드](guide-for-developers.md) 및 [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.|  
|이 제품을 설치하기 전에 Kb\<*번호*>에 해당하는 업데이트를 설치해야 합니다.|.NET Framework를 설치하기 전에 KB 업데이트가 설치되어 있어야 .NET Framework를 설치할 수 있습니다. 업데이트를 설치하고 .NET Framework 설치를 다시 시작합니다.<br /><br /> 예를 들어 .NET Framework에 Windows 8.1, Windows RT 8.1 및 Windows Server 2012 R2의 업데이트된 버전 설치는 [KB 2919355](https://support.microsoft.com/kb/2919355)에 해당하는 업데이트가 설치되어 있어야 합니다.|  
|컴퓨터에서 현재 Windows Server 2008 운영 체제의 Server Core 설치를 실행하고 있습니다. .NET Framework 4.5.x를 실행하려면 이후 버전의 운영 체제가 필요합니다. Windows Server 2008 R2 SP1 이상을 설치한 후 .NET Framework 4.5.x 설치 프로그램을 다시 실행하세요.|.NET Framework 4.5.1 및 4.5.2는 Windows Server 2008 R2 SP1 이상의 Server Core 역할에서 지원됩니다. [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.|  
|이 컴퓨터의 모든 사용자가 사용하도록 이 작업을 완료할 수 있는 권한이 없습니다. 관리자로 로그온한 다음 **설치 프로그램**을 다시 실행하십시오.|.NET Framework를 설치하려면 컴퓨터의 관리자여야 합니다.|  
|이전에 실행한 설치 작업을 사용하려면 컴퓨터를 다시 시작해야 하므로 설치 프로그램을 계속할 수 없습니다. 컴퓨터를 다시 시작하고 설치 프로그램을 다시 실행하십시오.|설치를 완료하려면 컴퓨터를 다시 시작해야 할 수도 있습니다. 지침에 따라 컴퓨터를 다시 시작하고 설치 프로그램을 다시 실행하세요.<br /><br /> 드문 경우지만 Windows가 누락된 업데이트 횟수를 감지하고 다음 순서의 업데이트를 설치하기 위해 다시 시작하는 경우 두 번 이상 시스템을 다시 시작하라는 메시지가 나타날 수 있습니다.|  
|.NET Framework 설치 프로그램은 프로그램 호환성 모드로 실행할 수 없습니다.|이 문서 뒷부분에 있는 [프로그램 호환성 문제](#compat) 섹션을 참조하십시오.|  
|구성 요소 저장소가 손상되었으므로 .NET Framework 4.5.x/4.6.x/4.7.x/4.8이 설치되지 않았습니다.|자세한 내용은 [DISM 또는 시스템 업데이트 준비 도구를 사용하여 Windows 업데이트 오류 해결](https://support.microsoft.com/kb/947821)을 참조하십시오.|  
|이 컴퓨터에서 Windows Installer 서비스를 사용할 수 없으므로 설치 프로그램을 실행할 수 없습니다.|Microsoft 지원 웹 사이트의 [프로그램을 설치하거나 업데이트할 때의 Windows Installer 서비스 오류](https://go.microsoft.com/fwlink/p/?LinkId=248684)를 참조하십시오.|  
|이 컴퓨터에서 Windows 업데이트 서비스를 사용할 수 없으므로 설치 프로그램이 올바르게 실행되지 않을 수 있습니다.|컴퓨터가 Microsoft Windows 업데이트 대신 WSUS(Windows Server Update Services)를 사용하도록 구성되었을 수 있습니다. 자세한 내용은 [Windows 8 또는 Windows Server 2012에서 .NET Framework 3.5를 설치하려고 할 때의 오류 코드](https://support.microsoft.com/kb/2734782)에서 오류 코드 0x800F0906 섹션을 참조하십시오.<br /><br /> Microsoft 지원 웹 사이트의 [컴퓨터 업데이트 관리에 도움이 되는 최신 버전의 Windows 업데이트 에이전트를 구하는 방법](https://go.microsoft.com/fwlink/p/?LinkId=248437)을 참조할 수도 있습니다.|  
|이 컴퓨터에서 BITS(Background Intelligent Transfer Service)를 사용할 수 없으므로 설치 프로그램이 올바르게 실행되지 않을 수 있습니다.|Microsoft 지원 웹 사이트에서 [Windows Vista 기반 컴퓨터에서 BITS(Background Intelligent Transfer Service) 충돌을 방지하기 위한 업데이트](https://go.microsoft.com/fwlink/p/?LinkId=248680)를 참조하십시오.|  
|Windows 업데이트에 오류가 발생하고 오류 코드 “0x80070643” 또는 “0x643”이 표시되었기 때문에 설치 프로그램이 올바르게 실행되지 않을 수 있습니다.|Microsoft 지원 웹 사이트에서 [.NET Framework 업데이트 설치 오류: "0x80070643" 또는 "0x643"](https://support.microsoft.com/kb/976982)을 참조하세요.|  
|.NET Framework 4.5.x/4.6.x/4.7.x/4.8은 이 운영 체제에 이미 포함되어 있습니다. .NET Framework 4.5.x/4.6.x/4.7.x/4.8 재배포 가능 패키지를 설치할 필요가 없습니다.|작업이 필요 없습니다.<br /><br /> 시스템에 설치된 .NET Framework의 버전을 확인하려면 [방법: 설치된 .NET Framework 버전 확인](../migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요. 지원되는 운영 체제는 [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.|  
|.NET Framework 4.5.x/4.6.x/4.7.x/4.8은 이 운영 체제에서 지원되지 않습니다.|지원되는 운영 체제는 [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.<br /><br /> Windows 7에서 .NET Framework의 설치가 실패하는 경우 이 메시지는 일반적으로 Windows 7 SP1이 설치되어 있지 않는 것을 나타냅니다. Windows 7 시스템에서 .NET Framework를 사용하려면 Windows 7 SP1이 필요합니다. Windows 7을 사용하며 서비스 팩 1을 아직 설치하지 않은 경우 .NET Framework를 설치하기 전에 먼저 설치해야 합니다. Windows 7 SP1의 설치에 대한 정보는 [Windows 7 서비스 팩 1(SP1) 설치 방법 알아보기](https://windows.microsoft.com/windows7/install-windows-7-service-pack-1)를 참조하십시오.|  
|컴퓨터에서 현재 Windows Server 2008 운영 체제의 Server Core 설치를 실행하고 있습니다. .NET Framework 4.5.x를 실행하려면 정식 버전의 운영 체제 또는 Server Core 2008 R2 SP1이 필요합니다. Windows Server 2008 SP2 또는 Windows Server 2008 R2 SP1 또는 Server Core 2008 R2 SP1의 정식 버전을 설치하고 .NET Framework 4.5.x 설치 프로그램을 다시 실행하세요.|.NET Framework는 Windows Server 2008 R2 SP1 이상의 Server Core 역할에서 지원됩니다. [시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.|  
|.NET Framework 4.5.x는 이 운영 체제에 이미 포함되어 있지만 현재 해제되어 있습니다([!INCLUDE[winserver8](../../../includes/winserver8-md.md)] 전용).|Windows 웹 사이트의 [Windows 기능 사용/사용 안 함](https://go.microsoft.com/fwlink/p/?LinkId=248438)을 참조하십시오.|  
|이 설치 프로그램을 사용하려면 x86 컴퓨터가 필요합니다. x64 또는 IA64 컴퓨터에는 설치할 수 없습니다.|[시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.|  
|이 설치 프로그램을 사용하려면 x64 또는 x86 컴퓨터가 필요합니다. IA64 컴퓨터에는 설치할 수 없습니다.|[시스템 요구 사항](../get-started/system-requirements.md)을 참조하십시오.|  

<a name="compat"></a>
### <a name="program-compatibility-issues"></a>프로그램 호환성 문제

Windows 프로그램 호환성 모드로 실행될 때 .NET Framework 4.5 또는 해당 포인트 릴리스 설치가 1603 오류 코드와 함께 실패하거나 차단됩니다. **프로그램 호환성 관리자**는 .NET Framework가 올바르게 설치되지 않았을 수 있다고 표시하고 권장되는 설정(프로그램 호환성 모드)을 사용하여 다시 설치하라는 메시지를 표시합니다. 이전에 .NET Framework 설치 프로그램 실행이 실패했거나 취소되었을 때 프로그램 호환성 관리자에서 프로그램 호환성 모드를 설정했을 수도 있습니다.

프로그램 호환성 모드에서는 .NET Framework 설치 관리자를 실행할 수 없습니다. 이 차단 문제를 해결하려면 레지스트리 편집기에서 호환성 모드 설정이 시스템 전체적으로 사용하지 않도록 설정되었는지 확인해야 합니다.

1. **시작** 버튼을 선택한 다음 **실행**을 선택합니다.

1. **실행** 대화 상자에서 “regedit”을 입력한 다음 **확인**을 선택합니다.

1. 레지스트리 편집기에서 다음 하위 키를 찾습니다.

   - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Compatibility Assistant\Persisted

   - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers

1. 이름 열에서 설치하는 버전에 따라 .NET Framework 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1 또는 4.7.2 다운로드 이름을 찾아 이러한 항목을 삭제합니다. 다운로드 이름에 대해서는 [개발자용 .NET Framework 설치](guide-for-developers.md) 문서를 참조하세요.

1. 4\.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1 또는 4.7.2 버전용 .NET Framework 설치 관리자를 다시 실행합니다.

## <a name="see-also"></a>참고 항목

- [개발자용 .NET Framework 설치](guide-for-developers.md)
- [방법: 설치된 .NET Framework 버전 확인](../migration-guide/how-to-determine-which-versions-are-installed.md)
- [버전 및 종속성](../migration-guide/versions-and-dependencies.md)
