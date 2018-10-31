---
title: '방법: 서비스 설치 및 제거'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, deploying
- services, uninstalling
- services, installing
- installing Windows Services
- uninstalling applications, Windows Services
- installation, Windows Services
- uninstalling Windows Services
- installutil.exe tool
ms.assetid: c89c5169-f567-4305-9d62-db31a1de5481
author: ghogen
ms.openlocfilehash: 265ee152bf106d0f97cca83552fe9a3e75fb4165
ms.sourcegitcommit: fd8d4587cc26e53f0e27e230d6e27d828ef4306b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49349006"
---
# <a name="how-to-install-and-uninstall-services"></a>방법: 서비스 설치 및 제거
.NET Framework를 사용하여 Windows 서비스를 개발하는 경우에는 명령줄 유틸리티 InstallUtil.exe를 사용하여 서비스 응용 프로그램을 빠르게 설치할 수 있습니다. 사용자가 설치 및 제거할 수 있는 Windows 서비스를 릴리스하려는 개발자는 InstallShield를 사용해야 합니다. [Windows Installer Deployment](https://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)(Windows Installer 배포)를 참조하세요.  
  
> [!WARNING]
>  서비스를 컴퓨터에서 제거하려면 이 문서의 단계를 수행하는 대신 서비스를 설치한 프로그램 또는 소프트웨어 패키지를 확인하고 제어판에서 **프로그램 추가/제거**를 선택하여 해당 프로그램을 제거합니다. 대부분의 서비스는 Windows의 필수 요소이므로 제거하는 경우 시스템이 불안정해질 수 있습니다.  
  
 이 문서의 단계를 수행하려면 먼저 Windows 서비스에 서비스 설치 관리자를 추가해야 합니다. [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)(연습: 구성 요소 디자이너에서 Windows 서비스 응용 프로그램 만들기)를 참조하세요.  
  
 Windows 서비스 프로젝트는 F5 키를 눌러 Visual Studio 개발 환경에서 직접 실행할 수 없습니다. 프로젝트를 실행하려면 프로젝트의 서비스를 먼저 설치해야 하기 때문입니다.  
  
> [!TIP]
>  **서버 탐색기**를 시작하여 서비스가 설치 또는 제거되었는지 확인할 수 있습니다. 자세한 내용은 방법: 서버 탐색기-데이터베이스 탐색기 액세스 및 초기화를 참조하세요.  
  
### <a name="to-install-your-service-manually"></a>서비스를 수동으로 설치하려면  
  
1.  Windows **시작** 메뉴 또는 **시작** 화면에서 **Visual Studio**, **Visual Studio Tools**, **개발자 명령 프롬프트**를 차례로 선택합니다.  
  
     Visual Studio 명령 프롬프트가 나타납니다.  
  
2.  프로젝트의 컴파일된 실행 파일이 있는 디렉터리에 액세스합니다.  
  
3.  프로젝트의 실행 파일을 매개 변수로 사용하여 명령 프롬프트에서 InstallUtil.exe를 실행합니다.  
  
    ```  
    installutil <yourproject>.exe  
    ```  
  
     Visual Studio 명령 프롬프트를 사용하는 경우 InstallUtil.exe가 시스템 경로에 있어야 합니다. 그러지 않으면 경로에 InstallUtil.exe를 추가하거나 정규화된 경로를 사용하여 해당 파일을 호출해야 합니다. 이 도구는 .NET Framework와 함께 설치되며 경로는 `%WINDIR%\Microsoft.NET\Framework[64]\<framework_version>`입니다. 예를 들어 32비트 버전 .NET Framework 4 또는 4.5.*의 경우 Windows 설치 디렉터리가 C:\Windows이면 경로는 `C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe`입니다. 64비트 버전 .NET Framework 4 또는 4.5.\*의 경우 기본 경로는 `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe`입니다.  
  
### <a name="to-uninstall-your-service-manually"></a>서비스를 수동으로 제거하려면  
  
1.  Windows **시작** 메뉴 또는 **시작** 화면에서 **Visual Studio**, **Visual Studio Tools**, **개발자 명령 프롬프트**를 차례로 선택합니다.  
  
     Visual Studio 명령 프롬프트가 나타납니다.  
  
2.  프로젝트의 출력을 매개 변수로 사용하여 명령 프롬프트에서 InstallUtil.exe를 실행합니다.  
  
    ```  
    installutil /u <yourproject>.exe  
    ```  
  
3.  서비스의 실행 파일을 삭제해도 서비스가 레지스트리에 남아 있는 경우가 있습니다. 이러한 경우에는 [sc delete](/windows-server/administration/windows-commands/sc-delete) 명령을 사용하여 레지스트리에서 서비스 항목을 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)  
 [방법: Windows 서비스 만들기](../../../docs/framework/windows-services/how-to-create-windows-services.md)  
 [방법: 서비스 응용 프로그램에 설치 관리자 추가](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)  
 [Installutil.exe(설치 관리자 도구)](../../../docs/framework/tools/installutil-exe-installer-tool.md)
