---
title: Visual Basic 애플리케이션 모델 개요
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application object [Visual Basic], Visual Basic application model
- Visual Basic application model
ms.assetid: 17538984-84fe-43c9-82c8-724c9529fe8b
ms.openlocfilehash: 0144c92e01e617081ae05003e6a7175c63166891
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622801"
---
# <a name="overview-of-the-visual-basic-application-model"></a>Visual Basic 애플리케이션 모델 개요
Visual Basic Windows Forms 응용 프로그램의 동작을 제어 하기 위한 잘 정의 된 모델을 제공 합니다: Visual Basic 응용 프로그램 모델입니다. 이 모델에는 catch 하면 처리 되지 않은 예외에 대 한 이벤트 뿐만 아니라 응용 프로그램의 시작 및 종료를 처리 하는 것에 대 한 이벤트가 포함 됩니다. 단일 인스턴스 응용 프로그램 개발에 대 한 지원 기능을 제공 합니다. 응용 프로그램 모델 확장 가능 하며 이므로 더 많은 제어가 필요한 개발자는 재정의 가능한 메서드를 사용자 지정할 수 있습니다.  
  
## <a name="uses-for-the-application-model"></a>응용 프로그램 모델 사용  
 일반적인 응용 프로그램을 시작 하 고 종료 하는 경우 작업을 수행 해야 합니다. 예를 들어 시작 될 때 응용 프로그램 수 시작 화면을 표시, 데이터베이스 연결을 확인, 저장된 된 상태를 로드 등에입니다. 응용 프로그램을 종료 하는 경우이 수 데이터베이스 연결 닫기, 현재 상태를 저장 등에입니다. 또한를 통해 응용 프로그램 종료 될 때 특정 코드를 실행할 수 아래로 예기치 않게 등 처리 되지 않은 예외가 발생 한 경우 처럼 합니다.  
  
 Visual Basic 응용 프로그램 모델을 사용 하면 쉽게 만들 수는 *단일 인스턴스* 응용 프로그램입니다. 단일 인스턴스 애플리케이션을 하는 일반적인 애플리케이션에서 애플리케이션의 인스턴스 하나만 실행할 수 있습니다 번 다릅니다. 단일 인스턴스 응용 프로그램의 다른 인스턴스를 시작 하려고 알리지 원래 인스턴스에서 결과-이용 하 여는 `StartupNextInstance` 이벤트-다른 실행이 시도 되었습니다. 알림을 후속 인스턴스가 명령줄 인수를 포함합니다. 초기화가 실행 되기 전에 응용 프로그램의 후속 인스턴스가 닫힙니다.  
  
 단일 인스턴스 응용 프로그램을 시작 및 첫 번째 인스턴스 또는 응용 프로그램의 후속 인스턴스가 인지 확인 합니다.  
  
- 첫 번째 인스턴스의 경우 일반적으로 시작 합니다.  
  
- 첫 번째 인스턴스가 실행 되는 동안 응용 프로그램을 시작 하려고 할 때마다 결과가 다릅니다. 후속 시도 명령줄 인수에 대 한 첫 번째 인스턴스를 알리고 즉시 종료 됩니다. 첫 번째 인스턴스 핸들을 `StartupNextInstance` 이벤트에는 후속 인스턴스의 명령줄 인수를 및 계속 실행 됩니다.  
  
     이 다이어그램에서는 후속 인스턴스가 첫 번째 인스턴스를 신호 하는 방법을 보여 줍니다.  
  
     ![단일 인스턴스 응용 프로그램 이미지를 보여 주는 다이어그램입니다.](./media/overview-of-the-visual-basic-application-model/single-instance-application.gif)  
  
 처리는 `StartupNextInstance` 이벤트를 단일 인스턴스 응용 프로그램의 동작을 제어할 수 있습니다. 예를 들어, Microsoft Outlook 일반적으로 실행 되는 단일 인스턴스 응용 프로그램으로 Outlook이 실행 되 고 Outlook을 시작 하려고 하면 다시 원래 인스턴스에 포커스가 이동 되지만 다른 인스턴스가 열리지 않습니다.  
  
## <a name="events-in-the-application-model"></a>응용 프로그램 모델에서 이벤트  
 다음 이벤트를 응용 프로그램 모델에 포함 됩니다.  
  
- **응용 프로그램 시작**합니다. 발생 된 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> 시작 시 이벤트입니다. 이 이벤트를 처리 하 여 기본 폼이 로드 되기 전에 응용 프로그램을 초기화 하는 코드를 추가할 수 있습니다. `Startup` 이벤트 시작 프로세스의 단계는 응용 프로그램의 실행을 취소 하는 것에 대 한 원하는 경우도 제공 합니다.  
  
     응용 프로그램 시작 코드를 실행 하는 동안 시작 화면에 표시할 응용 프로그램을 구성할 수 있습니다. 기본적으로 응용 프로그램 모델을 시작 하지 않습니다 때 화면 중 하나는 `/nosplash` 또는 `-nosplash` 명령줄 인수를 사용 합니다.  
  
- **단일 인스턴스 응용 프로그램**합니다. <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> 단일 인스턴스 응용 프로그램의 후속 인스턴스가 시작 될 때 이벤트가 발생 합니다. 이벤트의 후속 인스턴스가 명령줄 인수를 전달합니다.  
  
- **처리 되지 않은 예외**합니다. 응용 프로그램 처리 되지 않은 예외가 발생 하는 경우 발생 합니다 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 이벤트입니다. 해당 이벤트에 대 한 처리기는 예외를 검사 하 고 실행을 계속할지 여부를 확인할 수 있습니다.  
  
     `UnhandledException` 일부 상황에서 이벤트가 발생 하지 않습니다. 자세한 내용은 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>을 참조하세요.  
  
- **네트워크 연결 변경**합니다. 응용 프로그램 발생 하는 컴퓨터의 네트워크 가용성이 변경 되 면는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged> 이벤트입니다.  
  
     `NetworkAvailabilityChanged` 일부 상황에서 이벤트가 발생 하지 않습니다. 자세한 내용은 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>을 참조하세요.  
  
- **응용 프로그램을 종료할**합니다. 응용 프로그램을 제공 합니다 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> 에 종료 되었을 때 신호를 보내는 이벤트입니다. 이벤트의 처리기를 할 수 있습니다는 작업 응용 프로그램을 수행 해야-닫기 및 예를 들어 저장-완료 됩니다. 기본 폼이 닫히면 종료 되거나 모든 폼이 닫힐 때만 종료 하려면 응용 프로그램을 구성할 수 있습니다.  
  
## <a name="availability"></a>가용성  
 기본적으로 Visual Basic 응용 프로그램 모델은 Windows Forms 프로젝트에 사용할 수 있습니다. 다른 시작 개체를 사용 하도록 응용 프로그램을 구성 하거나 사용자 지정을 사용 하 여 응용 프로그램 코드를 시작 하기 `Sub Main`, 하는 개체 또는 클래스의 구현을 제공 해야 할 수는 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 응용 프로그램 모델을 사용 하는 클래스입니다. 시작 개체를 변경 하는 방법에 대 한 내용은 [응용 프로그램 페이지, 프로젝트 디자이너 (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- [Visual Basic 응용 프로그램 모델 확장](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)
