---
title: '방법: Windows 서비스 설치 및 제거'
ms.date: 02/05/2019
helpviewer_keywords:
- Windows Service applications, deploying
- services, uninstalling
- services, installing
- installing Windows Services
- uninstalling applications, apps, Windows services
- installation, Windows services
- uninstalling Windows services
- installutil.exe tool
ms.assetid: c89c5169-f567-4305-9d62-db31a1de5481
author: ghogen
ms.openlocfilehash: 38fc0172b5f97561d69fe495237e95597d7b9727
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003128"
---
# <a name="how-to-install-and-uninstall-windows-services"></a>방법: Windows 서비스 설치 및 제거

.NET Framework를 사용 하 여 Windows 서비스를 개발 하는 경우 [*installutil.exe*](../tools/installutil-exe-installer-tool.md) 명령줄 유틸리티 또는 [PowerShell](/powershell/scripting/overview)을 사용 하 여 서비스 앱을 신속 하 게 설치할 수 있습니다. 사용자가 설치하고 제거할 수 있는 Windows 서비스를 릴리스하려는 개발자는 InstallShield를 사용해야 합니다. 자세한 내용은 [설치 관리자 패키지 만들기(Windows 클라이언트)](https://docs.microsoft.com/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-client)를 참조하세요.

> [!WARNING]
> 서비스를 컴퓨터에서 제거하려면 이 문서의 단계를 수행하는 대신 서비스를 설치한 프로그램 또는 소프트웨어 패키지를 확인한 다음, 설정에서 **앱**을 선택하여 해당 프로그램을 제거합니다. 대부분의 서비스는 Windows의 필수 요소이므로 제거하는 경우 시스템이 불안정해질 수 있습니다.

이 문서의 단계를 수행하려면 먼저 Windows 서비스에 서비스 설치 관리자를 추가해야 합니다. 자세한 내용은 [연습: Windows 서비스 앱 만들기](../windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)를 참조하세요.

F5 키를 눌러 Visual Studio 개발 환경에서 직접 Windows 서비스 프로젝트를 실행할 수 없습니다. 프로젝트를 실행하려면 먼저 프로젝트에 서비스를 설치해야 합니다.

> [!TIP]
> **서버 탐색기**를 사용하여 서비스가 설치되거나 제거되었는지 확인할 수 있습니다. 자세한 내용은 [Visual Studio에서 서버 탐색기를 사용하는 방법](https://support.microsoft.com/help/316649/how-to-use-the-server-explorer-in-visual-studio-net-and-visual-studio)을 참조하세요.

### <a name="install-your-service-manually-using-installutilexe-utility"></a>Installutil.exe 유틸리티를 사용 하 여 수동으로 서비스 설치

1. **시작** 메뉴에서 **Visual Studio \<*version*>** 디렉터리를 선택한 다음, **Developer Command Prompt for VS \<*version*>** 을 선택합니다.

     Visual Studio용 개발자 명령 프롬프트가 나타납니다.

2. 프로젝트의 컴파일된 실행 파일이 있는 디렉터리에 액세스합니다.

3. 프로젝트의 실행 파일을 매개 변수로 사용하여 명령 프롬프트에서 *InstallUtil.exe*를 실행합니다.

    ```console
    installutil <yourproject>.exe
    ```

     Visual Studio용 개발자 명령 프롬프트를 사용하는 경우 *InstallUtil.exe*가 시스템 경로에 있어야 합니다. 그렇지 않으면 해당 파일을 경로에 추가하거나 정규화된 경로를 사용하여 호출하면 됩니다. 이 도구는 *%WINDIR%\Microsoft.NET\Framework[64]\\<framework_version\>* 에 .NET Framework와 함께 설치됩니다.

     예를 들어 다음과 같은 가치를 제공해야 합니다.
     - 32비트 버전의 .NET Framework 4 또는 4.5 이상인 경우 Windows 설치 디렉터리가 *C:\Windows*이면 기본 경로는 *C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe*입니다.
     - 64비트 버전의 .NET Framework 4 또는 4.5 이상인 경우 기본 경로는 *C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*입니다.

### <a name="uninstall-your-service-manually-using-installutilexe-utility"></a>Installutil.exe 유틸리티를 사용 하 여 수동으로 서비스 제거

1. **시작** 메뉴에서 **Visual Studio \<*version*>** 디렉터리를 선택한 다음, **Developer Command Prompt for VS \<*version*>** 을 선택합니다.

     Visual Studio용 개발자 명령 프롬프트가 나타납니다.

2. 프로젝트의 출력을 매개 변수로 사용하여 명령 프롬프트에서 *InstallUtil.exe*를 실행합니다.

    ```console
    installutil /u <yourproject>.exe
    ```

3. 서비스의 실행 파일을 삭제해도 서비스가 레지스트리에 남아 있을 수 있습니다. 이러한 경우에는 [sc delete](/windows-server/administration/windows-commands/sc-delete) 명령을 사용하여 레지스트리에서 서비스의 항목을 제거합니다.

### <a name="install-your-service-manually-using-powershell"></a>PowerShell을 사용 하 여 수동으로 서비스 설치

1. **시작** 메뉴에서 **windows powershell** 디렉터리를 선택 하 고 **windows powershell**을 선택 합니다.

2. 프로젝트의 컴파일된 실행 파일이 있는 디렉터리에 액세스합니다.

3. 프로젝트의 출력과 서비스 이름을 매개 변수로 사용 하 여 [**새 서비스**](/powershell/module/microsoft.powershell.management/new-service) cmdlet을 실행 합니다.

    ```powershell
    New-Service -Name "YourServiceName" -BinaryPathName <yourproject>.exe
    ```

### <a name="uninstall-your-service-manually-using-powershell"></a>PowerShell을 사용 하 여 수동으로 서비스 제거

1. **시작** 메뉴에서 **windows powershell** 디렉터리를 선택 하 고 **windows powershell**을 선택 합니다.

2. 서비스 이름을 매개 변수로 사용 하 여 [**서비스**](/powershell/module/microsoft.powershell.management/remove-service) 이름 cmdlet을 실행 합니다.

    ```powershell
    Remove-Service -Name "YourServiceName"
    ```

3. 서비스의 실행 파일을 삭제해도 서비스가 레지스트리에 남아 있을 수 있습니다. 이러한 경우에는 [sc delete](/windows-server/administration/windows-commands/sc-delete) 명령을 사용하여 레지스트리에서 서비스의 항목을 제거합니다.

    ```powershell
    sc.exe delete "YourServiceName"
    ```

## <a name="see-also"></a>참조

- [Windows 서비스 애플리케이션 소개](../windows-services/introduction-to-windows-service-applications.md)
- [방법: Windows 서비스 만들기](../windows-services/how-to-create-windows-services.md)
- [방법: 서비스 애플리케이션에 설치 관리자 추가](../windows-services/how-to-add-installers-to-your-service-application.md)
- [Installutil.exe(설치 관리자 도구)](../tools/installutil-exe-installer-tool.md)
