---
title: Windows 서비스 응용 프로그램 소개
ms.date: 03/30/2017
f1_keywords:
- ServiceController
helpviewer_keywords:
- Windows Service applications, deploying
- OnStop method
- OnPause method
- services, about services
- Service class, Windows Service applications
- framework services, creating services
- ServiceController components, about Windows services
- Win32OwnProcess service type
- services, lifetime
- OnContinue method
- Windows Service applications, about Windows Service applications
- services, states
- service states
- WaitForStatus method
- Win32ShareProcess service type
- Windows Service applications, lifetime
ms.assetid: 1b1b5e67-3ff3-40c0-8154-322cfd6ef0ae
author: ghogen
ms.openlocfilehash: d0a16ee6f627ecc062fcad5f5216dda9855e430e
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48036067"
---
# <a name="introduction-to-windows-service-applications"></a>Windows 서비스 응용 프로그램 소개
과거에 NT 서비스라고 불리던 Microsoft Windows 서비스를 사용하면 고유한 Windows 세션에서 장시간 실행되는 응용 프로그램을 만들 수 있습니다. 이러한 서비스는 컴퓨터가 부팅될 때 자동으로 시작될 수 있고, 일시 중지 및 다시 시작할 수 있으며, 사용자 인터페이스를 표시하지 않습니다. 이러한 특징 때문에 서버에서 사용하거나 같은 컴퓨터에서 작업하는 다른 사용자를 방해하지 않는 장기 실행 기능이 필요한 경우 유용합니다. 로그온한 사용자나 기본 컴퓨터 계정과 다른 특정 사용자 계정의 보안 컨텍스트에서 서비스를 실행할 수도 있습니다. 서비스 및 Windows 세션에 대한 자세한 내용은 Windows SDK 설명서를 참조하세요.  
  
 서비스로 설치되는 응용 프로그램을 만들어 서비스를 쉽게 만들 수 있습니다. 예를 들어 성능 카운터 데이터를 모니터링하고 임계값에 대응하려 한다고 가정합니다. 이 경우 성능 카운터 데이터를 수신하고, 응용 프로그램을 배포하고, 데이터 수집 및 분석을 시작하는 Windows 서비스 응용 프로그램을 만들 수 있습니다.  
  
 서비스를 Microsoft Visual Studio 프로젝트로 만들고, 서비스로 전송할 수 있는 명령과 해당 명령이 수신될 때 수행할 작업을 제어하는 코드를 서비스 내에 정의합니다. 서비스에 전송할 수 있는 명령은 서비스를 시작, 일시 중지, 다시 시작 및 중지하는 등의 명령이며, 사용자 지정 명령을 실행할 수도 있습니다.  
  
 응용 프로그램을 만들고 빌드한 후 명령줄 유틸리티 InstallUtil.exe를 실행하고 서비스의 실행 파일 경로를 전달하여 응용 프로그램을 설치할 수 있습니다. 그런 다음, **서비스 제어 관리자**를 사용하여 서비스를 시작, 중지, 일시 중지, 다시 시작 및 구성할 수 있습니다. **서버 탐색기**의 **서비스** 노드를 통해서나 <xref:System.ServiceProcess.ServiceController> 클래스를 사용하여 같은 작업을 대부분 수행할 수도 있습니다.  
  
## <a name="service-applications-vs-other-visual-studio-applications"></a>서비스 응용 프로그램 및 기타 Visual Studio 응용 프로그램  
 서비스 응용 프로그램은 다른 여러 프로젝트 유형과는 다음의 여러 가지 면에서 다르게 작동합니다.  
  
-   서비스 응용 프로그램 프로젝트에서 생성하는 컴파일된 실행 파일을 서버에 설치해야만 프로젝트가 의미 있는 방식으로 작동할 수 있습니다. F5 키 또는 F11 키를 눌러 서비스 응용 프로그램을 디버그하거나 실행할 수 없습니다. 즉, 서비스를 즉시 실행하거나 코드를 한 단계씩 실행할 수 없습니다. 대신 서비스를 설치하고 시작한 다음, 서비스의 프로세스에 디버거를 연결해야 합니다. 자세한 내용은 [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)(방법: Windows 서비스 응용 프로그램 디버그)를 참조하세요.  
  
-   일부 프로젝트 유형과 달리 서비스 응용 프로그램의 경우 설치 구성 요소를 만들어야 합니다. 설치 구성 요소는 서버에 서비스를 설치 및 등록하고 Windows **서비스 제어 관리자**를 사용하여 서비스에 대한 항목을 만듭니다. 자세한 내용은 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)(방법: 서비스 응용 프로그램에 설치 관리자 추가)을 참조하세요.  
  
-   서비스 응용 프로그램의 `Main` 메서드는 프로젝트에 포함된 서비스에 대해 Run 명령을 실행해야 합니다. `Run` 메서드는 해당 서버의 **서비스 제어 관리자**로 서비스를 로드합니다. **Windows 서비스** 프로젝트 템플릿을 사용하는 경우에는 이 메서드가 자동으로 작성됩니다. 서비스 로드는 서비스 시작과 같은 작업이 아닙니다. 자세한 내용은 아래에서 “서비스 수명”을 참조하세요.  
  
-   Windows 서비스 응용 프로그램은 로그온한 사용자의 대화형 스테이션과 다른 윈도우 스테이션에서 실행됩니다. 윈도우 스테이션은 클립보드, 전역 아톰 집합 및 데스크톱 개체 집합을 포함하는 보안 개체입니다. Windows 서비스의 스테이션은 대화형 스테이션이 아니므로 Windows 서비스 응용 프로그램 내에서 대화 상자가 발생할 경우 대화 상자가 표시되지 않으며 프로그램이 응답하지 않게 될 수 있습니다. 마찬가지로 오류 메시지는 사용자 인터페이스에서 발생하지 않고 Windows 이벤트 로그에 기록됩니다.  
  
     .NET Framework에서 지원하는 Windows 서비스 클래스는 대화형 스테이션 즉, 로그인한 사용자와의 상호 작용을 지원하지 않습니다. 또한 .NET Framework에는 스테이션 및 데스크톱을 나타내는 클래스가 포함되어 있지 않습니다. Windows 서비스가 다른 스테이션과 상호 작용해야 하는 경우 관리되지 않는 Windows API에 액세스해야 합니다. 자세한 내용은 Windows SDK 설명서를 참조하세요.  
  
     사용자 또는 다른 스테이션과 Windows 서비스의 상호 작용은 로그온한 사용자나 예기치 않은 데스크톱 개체 집합이 있는 사용자가 없는 등과 같은 시나리오를 포함하도록 주의해서 설계해야 합니다. 때로는 사용자의 제어하에서 실행되는 Windows 응용 프로그램을 작성하는 것이 더 적절할 수 있습니다.  
  
-   Windows 서비스 응용 프로그램은 자체 보안 컨텍스트에서 실행되며 설치된 Windows 컴퓨터에 사용자가 로그인하기 전에 시작됩니다. 서비스를 실행할 사용자 계정을 계획할 때는 신중해야 합니다. 시스템 계정에서 실행되는 서비스가 사용자 계정에서 실행되는 서비스보다 권한이 많습니다.  
  
## <a name="service-lifetime"></a>서비스 수명  
 서비스는 수명 동안 여러 내부 상태를 거칩니다. 먼저 서비스가 실행될 시스템에 설치됩니다. 이 프로세스에서는 서비스 프로젝트의 설치 관리자를 실행하고 서비스를 해당 컴퓨터의 **서비스 제어 관리자**로 로드합니다. **서비스 제어 관리자**는 Windows에서 제공하는 중앙 유틸리티로, 서비스를 관리합니다.  
  
 서비스가 로드되면 서비스를 시작해야 합니다. 서비스를 시작하면 서비스가 작동하기 시작합니다. **서비스 제어 관리자**나 **서버 탐색기**에서 또는 코드에서 <xref:System.ServiceProcess.ServiceController.Start%2A> 메서드를 호출하여 서비스를 시작할 수 있습니다. <xref:System.ServiceProcess.ServiceController.Start%2A> 메서드는 처리를 응용 프로그램의 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드에 전달하고 해당 메서드에서 정의한 코드를 처리합니다.  
  
 실행 중인 서비스는 중지 또는 일시 중지되거나 컴퓨터가 종료될 때까지 이 상태로 무기한 유지될 수 있습니다. 서비스 상태는 <xref:System.ServiceProcess.ServiceControllerStatus.Running> , <xref:System.ServiceProcess.ServiceControllerStatus.Paused> 또는 <xref:System.ServiceProcess.ServiceControllerStatus.Stopped>의 세 가지 기본 상태 중 하나일 수 있습니다. 또한 서비스에서 보류 중인 명령의 상태를 <xref:System.ServiceProcess.ServiceControllerStatus.ContinuePending> , <xref:System.ServiceProcess.ServiceControllerStatus.PausePending> , <xref:System.ServiceProcess.ServiceControllerStatus.StartPending>, <xref:System.ServiceProcess.ServiceControllerStatus.StopPending> 등으로 보고할 수도 있습니다. 이러한 상태는 실행 중인 서비스를 일시 중지하는 명령 등과 같은 명령이 실행되었지만 아직 수행되지 않았음을 나타냅니다. <xref:System.ServiceProcess.ServiceController.Status%2A>을 쿼리하여 서비스의 상태를 확인하거나 <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A>를 사용하여 이러한 상태가 발생할 경우 작업을 수행할 수 있습니다.  
  
 **서비스 제어 관리자**나 **서버 탐색기**에서 또는 코드에서 메서드를 호출하여 서비스를 일시 중지, 중지 또는 다시 시작할 수 있습니다. 이러한 각 작업은 서비스의 관련 프로시저(<xref:System.ServiceProcess.ServiceBase.OnStop%2A> , <xref:System.ServiceProcess.ServiceBase.OnPause%2A> 또는 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>)를 호출할 수 있으며, 이러한 프로시저 내에 서비스 상태가 변경될 때 수행할 추가 처리를 정의할 수 있습니다.  
  
## <a name="types-of-services"></a>서비스 유형  
 .NET Framework을 사용하여 Visual Studio에서 만들 수 있는 서비스 유형은 두 가지입니다. 프로세스의 유일한 서비스인 경우 <xref:System.ServiceProcess.ServiceType.Win32OwnProcess> 유형이 할당됩니다. 다른 서비스와 프로세스를 공유하는 서비스에는 <xref:System.ServiceProcess.ServiceType.Win32ShareProcess> 유형이 할당됩니다. <xref:System.ServiceProcess.ServiceController.ServiceType%2A> 속성을 쿼리하여 서비스 유형을 검색할 수 있습니다.  
  
 Visual Studio에서 만들지 않은 기존 서비스를 쿼리하면 다른 서비스 유형도 가끔 볼 수 있습니다. 이에 대한 자세한 내용은 <xref:System.ServiceProcess.ServiceType>을 참조하세요.  
  
## <a name="services-and-the-servicecontroller-component"></a>서비스 및 ServiceController 구성 요소  
 <xref:System.ServiceProcess.ServiceController> 구성 요소는 설치된 서비스에 연결하고 서비스 상태를 조작하는 데 사용됩니다. <xref:System.ServiceProcess.ServiceController> 구성 요소를 사용하면 서비스를 시작 및 중지하고, 서비스 작동을 일시 중지하거나 계속하고, 서비스에 사용자 지정 명령을 전송할 수 있습니다. 하지만 서비스 응용 프로그램을 만들 때는 <xref:System.ServiceProcess.ServiceController> 구성 요소를 사용할 필요가 없습니다. 실제로 대부분의 경우 <xref:System.ServiceProcess.ServiceController> 구성 요소는 서비스를 정의하는 Windows 서비스 응용 프로그램과 별도의 응용 프로그램에 있어야 합니다.  
  
 자세한 내용은 <xref:System.ServiceProcess.ServiceController>을 참조하세요.  
  
## <a name="requirements"></a>요구 사항  
  
-   서비스는 **Windows 서비스** 응용 프로그램 프로젝트나 다른 .NET Framework 지원 프로젝트에서 만들어야 합니다. 이러한 프로젝트는 빌드될 때 .exe 파일을 생성하고 <xref:System.ServiceProcess.ServiceBase> 클래스에서 상속됩니다.  
  
-   Windows 서비스를 포함하는 프로젝트에는 프로젝트 및 해당 서비스에 대한 설치 구성 요소가 있어야 합니다. 이 작업은 **속성** 창에서 간단히 수행할 수 있습니다. 자세한 내용은 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)(방법: 서비스 응용 프로그램에 설치 관리자 추가)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램](../../../docs/framework/windows-services/index.md)  
 [서비스 응용 프로그램 프로그래밍 아키텍처](../../../docs/framework/windows-services/service-application-programming-architecture.md)  
 [방법: Windows 서비스 만들기](../../../docs/framework/windows-services/how-to-create-windows-services.md)  
 [방법: 서비스 설치 및 제거](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)  
 [방법: 서비스 시작](../../../docs/framework/windows-services/how-to-start-services.md)  
 [방법: Windows 서비스 응용 프로그램 디버깅](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)  
 [연습: 구성 요소 디자이너에서 Windows 서비스 응용 프로그램 만들기](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)  
 [방법: 서비스 응용 프로그램에 설치 관리자 추가](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)
