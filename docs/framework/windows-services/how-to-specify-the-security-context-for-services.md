---
title: '방법: 서비스에 대한 보안 컨텍스트 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, security
- security [Visual Studio], contexts
- contexts, Visual Studio security
- security [Visual Studio], service applications
- ServiceProcessInstaller class, security context
- services, security
- ServiceInstaller class, security context
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
author: ghogen
ms.openlocfilehash: a5a437af90f29bc601215176ad5c4fec702ddbc0
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48036080"
---
# <a name="how-to-specify-the-security-context-for-services"></a>방법: 서비스에 대한 보안 컨텍스트 지정
기본적으로 서비스는 로그인한 사용자와 다른 보안 컨텍스트에서 실행됩니다. 서비스는 기본 시스템 계정 `LocalSystem`의 컨텍스트에서 실행되므로, 시스템 리소스에 대해 사용자와는 다른 액세스 권한을 받습니다. 이 동작을 변경하여 서비스를 실행할 다른 사용자 계정을 지정할 수 있습니다.  
  
 보안 컨텍스트는 서비스가 실행되는 프로세스에 대한 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 속성을 조작하여 설정합니다. 이 속성을 사용하면 서비스를 다음 네 가지 계정 유형 중 하나로 설정할 수 있습니다.  
  
-   `User` - 네트워크의 단일 사용자가 지정한 계정의 컨텐스트에서 서비스가 설치 및 실행될 때 시스템에서 유효한 사용자 이름과 암호를 묻는 메시지를 표시합니다.  
  
-   `LocalService` - 로컬 컴퓨터에서 권한 없는 사용자의 역할을 하며 원격 서버에 익명 자격 증명을 제공하는 계정의 컨텍스트에서 실행됩니다.  
  
-   `LocalSystem` - 광범위한 로컬 권한을 제공하며 원격 서버에 컴퓨터의 자격 증명을 제공하는 계정의 컨텍스트에서 실행됩니다.  
  
-   `NetworkService` - 로컬 컴퓨터에서 권한 없는 사용자 역할을 하며 원격 서버에 컴퓨터의 자격 증명을 제공하는 계정의 컨텍스트에서 실행됩니다.  
  
 자세한 내용은 <xref:System.ServiceProcess.ServiceAccount> 열거형을 참조하세요.  
  
### <a name="to-specify-the-security-context-for-a-service"></a>서비스에 대한 보안 컨텍스트를 지정하려면  
  
1.  서비스를 만든 후 서비스에 필요한 설치 관리자를 추가합니다. 자세한 내용은 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)(방법: 서비스 응용 프로그램에 설치 관리자 추가)을 참조하세요.  
  
2.  디자이너에서 `ProjectInstaller` 클래스에 액세스하고 작업 중인 서비스에 대한 서비스 프로세스 설치 관리자를 클릭합니다.  
  
    > [!NOTE]
    >  모든 서비스 응용 프로그램의 `ProjectInstaller` 클래스에는 적어도 두 개의 설치 구성 요소가 있는데, 프로젝트의 모든 서비스에 대한 프로세스를 설치하는 구성 요소와 응용 프로그램에 포함된 각 서비스에 대한 설치 관리자 1개입니다. 이 인스턴스에서 <xref:System.ServiceProcess.ServiceProcessInstaller>을 선택할 수 있습니다.  
  
3.  **속성** 창에서 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A>를 적절한 값으로 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)  
 [방법: 서비스 응용 프로그램에 설치 관리자 추가](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)  
 [방법: Windows 서비스 만들기](../../../docs/framework/windows-services/how-to-create-windows-services.md)
