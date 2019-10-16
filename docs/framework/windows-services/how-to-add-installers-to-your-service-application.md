---
title: '방법: 서비스 애플리케이션에 설치 관리자 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, deploying
- installation components, adding to services
- installers, adding to services
- Windows Service applications, adding installers
- services, adding installers
- ServiceInstaller class, adding installers to services
- ServiceProcessInstaller class, adding installers to services
ms.assetid: 8b698e9a-b88e-4f44-ae45-e0c5ea0ae5a8
author: ghogen
ms.openlocfilehash: 99e2376c50f0b47cc21002b2926818707188805e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053646"
---
# <a name="how-to-add-installers-to-your-service-application"></a>방법: 서비스 애플리케이션에 설치 관리자 추가
Visual Studio에서는 서비스 애플리케이션과 관련된 리소스를 설치할 수 있는 설치 구성 요소를 제공합니다. 설치 구성 요소는 서비스를 설치하는 시스템에 개별 서비스를 등록하고 서비스 제어 관리자에 서비스가 있음을 알립니다. 서비스 애플리케이션을 작업할 때 속성 창의 링크를 선택하여 프로젝트에 적절한 설치 관리자를 자동으로 추가할 수 있습니다.  
  
> [!NOTE]
> 서비스의 속성 값이 서비스 클래스에서 설치 관리자 클래스로 복사됩니다. 서비스 클래스에서 속성 값을 업데이트하는 경우 설치 관리자에서 해당 속성이 자동으로 업데이트되지는 않습니다.  
  
 프로젝트에 설치 관리자를 추가하면 새 클래스(기본적으로 이름은 `ProjectInstaller`)가 프로젝트에 생성되고 이 클래스 안에 적절한 설치 구성 요소의 인스턴스가 생성됩니다. 이 클래스는 프로젝트에 필요한 모든 설치 구성 요소의 중심점 역할을 합니다. 예를 들어 애플리케이션에 두 번째 서비스를 추가하고 설치 관리자 추가 링크를 클릭하면 두 번째 설치 관리자 클래스가 생성되지 않습니다. 대신 두 번째 서비스에 필요한 추가 설치 구성 요소가 기존 클래스에 추가됩니다.  
  
 서비스를 올바로 설치하도록 하기 위해 설치 관리자 내에서 코딩을 수행할 필요는 특별히 없습니다. 하지만 가끔은 설치 프로세스에 특수한 기능을 추가해야 하는 경우 설치 관리자의 내용을 수정해야 할 수도 있습니다.  
  
> [!NOTE]
> 표시되는 대화 상자와 메뉴 명령은 활성 설정이나 버전에 따라 도움말에서 설명하는 것과 다를 수 있습니다. 설정을 변경하려면 **도구** 메뉴에서 **설정 가져오기 및 내보내기** 를 선택합니다. 자세한 내용은 [Visual Studio IDE 개인 설정](/visualstudio/ide/personalizing-the-visual-studio-ide)을 참조하세요.  
  
### <a name="to-add-installers-to-your-service-application"></a>서비스 애플리케이션에 설치 관리자를 추가하려면  
  
1. **솔루션 탐색기**에서 설치 구성 요소를 추가할 서비스의 **디자인** 뷰에 액세스합니다.  
  
2. 디자이너의 배경을 클릭하여 서비스 내용이 아닌 서비스 자체를 선택합니다.  
  
3. 디자이너에 포커스가 있는 상태에서 **설치 관리자 추가**를 클릭합니다.  
  
     새 클래스 `ProjectInstaller`와 두 개의 설치 구성 요소 <xref:System.ServiceProcess.ServiceProcessInstaller> 및 <xref:System.ServiceProcess.ServiceInstaller>가 프로젝트에 추가되고 서비스의 속성 값이 이러한 구성 요소에 복사됩니다.  
  
4. <xref:System.ServiceProcess.ServiceInstaller> 구성 요소를 클릭하고 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 속성 값이 서비스 자체의 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 속성과 동일한 값으로 설정되어 있는지 확인합니다.  
  
5. 서비스 시작 방법을 결정하려면 <xref:System.ServiceProcess.ServiceInstaller> 구성 요소를 클릭하고 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 속성을 적절한 값으로 설정합니다.  
  
    |값|결과|  
    |-----------|------------|  
    |<xref:System.ServiceProcess.ServiceStartMode.Manual>|서비스를 설치 후 수동으로 시작해야 합니다. 자세한 내용은 [방법: 서비스 시작](how-to-start-services.md)을 참조하세요.|  
    |<xref:System.ServiceProcess.ServiceStartMode.Automatic>|컴퓨터가 재부팅될 때마다 서비스가 저절로 시작됩니다.|  
    |<xref:System.ServiceProcess.ServiceStartMode.Disabled>|서비스를 시작할 수 없습니다.|  
  
6. 서비스를 실행할 보안 컨텍스트를 결정하려면 <xref:System.ServiceProcess.ServiceProcessInstaller> 구성 요소를 클릭하고 적절한 속성 값을 설정합니다. 자세한 내용은 [방법: 서비스에 대한 보안 컨텍스트 지정](how-to-specify-the-security-context-for-services.md)을 참조하세요.  
  
7. 사용자 지정 처리를 수행해야 하는 모든 메서드를 재정의합니다.  
  
8. 프로젝트의 추가 서비스 각각에 대해 1-7단계를 수행합니다.  
  
    > [!NOTE]
    > 프로젝트의 각 추가 서비스에 대해 프로젝트의 `ProjectInstaller` 클래스에 <xref:System.ServiceProcess.ServiceInstaller> 구성 요소를 추가해야 합니다. 3단계에서 추가된 <xref:System.ServiceProcess.ServiceProcessInstaller> 구성 요소는 프로젝트의 모든 개별 서비스 설치 관리자에서 작동합니다.  
  
## <a name="see-also"></a>참고 항목

- [Windows 서비스 애플리케이션 소개](introduction-to-windows-service-applications.md)
- [방법: 서비스 설치 및 제거](how-to-install-and-uninstall-services.md)
- [방법: 서비스 시작](how-to-start-services.md)
- [방법: 서비스에 대한 보안 컨텍스트 지정](how-to-specify-the-security-context-for-services.md)
