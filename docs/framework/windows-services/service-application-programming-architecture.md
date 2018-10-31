---
title: 서비스 응용 프로그램 프로그래밍 아키텍처
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ServiceController components, programming architecture
- ServiceBase class, service states
- Windows Service applications, code model
- services, programming architecture
- ServiceController class
- services, states
- ServiceProcessInstaller class, service application code model
- Windows Service applications, states
ms.assetid: 83230026-d068-4174-97ff-e264c896eb2f
author: ghogen
ms.openlocfilehash: fbe75d8ec4a677c47a98a5868c4e7e44c95f1d93
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48028201"
---
# <a name="service-application-programming-architecture"></a>서비스 응용 프로그램 프로그래밍 아키텍처
Windows 서비스 응용 프로그램은 <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> 클래스에서 상속되는 클래스를 기반으로 합니다. 이 클래스의 메서드를 재정의하고 이 메서드에서 서비스 동작 방식을 결정하는 기능을 정의합니다.  
  
 서비스 만들기와 관련된 기본 클래스는 다음과 같습니다.  
  
-   <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> - 서비스를 만들 때 <xref:System.ServiceProcess.ServiceBase> 클래스의 메서드를 재정의하고 이 상속된 클래스에서 서비스가 작동하는 방식을 결정하는 코드를 정의합니다.  
  
-   <xref:System.ServiceProcess.ServiceProcessInstaller?displayProperty=nameWithType> 및 <xref:System.ServiceProcess.ServiceInstaller?displayProperty=nameWithType> - 이러한 클래스를 사용하여 서비스를 설치 및 제거합니다.  
  
 또한 <xref:System.ServiceProcess.ServiceController>라는 클래스를 사용하여 서비스 자체를 조작할 수 있습니다. 이 클래스는 서비스 만들기와는 관련이 없지만 서비스를 시작 및 중지하고 서비스에 명령을 전달하고 일련의 열거형을 반환하는 데 사용할 수 있습니다.  
  
## <a name="defining-your-services-behavior"></a>서비스 동작 정의  
 서비스 클래스에서 기본 클래스 함수를 재정의하여 서비스 제어 관리자에서 서비스 상태를 변경하는 경우 어떤 작업을 수행할지 결정합니다. <xref:System.ServiceProcess.ServiceBase> 클래스는 다음과 같은 메서드를 노출하며, 이들 메서드를 재정의하여 사용자 지정 동작을 추가할 수 있습니다.  
  
|메서드|재정의 목적|  
|------------|-----------------|  
|<xref:System.ServiceProcess.ServiceBase.OnStart%2A>|서비스 실행이 시작될 때 수행할 작업을 지정합니다. 서비스가 유용한 작업을 수행하려면 이 프로시저에 코드를 작성해야 합니다.|  
|<xref:System.ServiceProcess.ServiceBase.OnPause%2A>|서비스가 일시 중지될 경우 수행할 작업을 지정합니다.|  
|<xref:System.ServiceProcess.ServiceBase.OnStop%2A>|서비스 실행이 중지될 경우 수행할 작업을 지정합니다.|  
|<xref:System.ServiceProcess.ServiceBase.OnContinue%2A>|서비스가 일시 중지되었다가 정상 작동을 재개할 경우 수행할 작업을 지정합니다.|  
|<xref:System.ServiceProcess.ServiceBase.OnShutdown%2A>|서비스가 실행 중일 때 시스템이 종료될 경우 종료 직전에 수행할 작업을 지정합니다.|  
|<xref:System.ServiceProcess.ServiceBase.OnCustomCommand%2A>|서비스가 사용자 지정 명령을 받을 경우 수행할 작업을 지정합니다. 사용자 지정 명령에 대한 자세한 내용은 MSDN Online을 참조하세요.|  
|<xref:System.ServiceProcess.ServiceBase.OnPowerEvent%2A>|배터리 부족 또는 일시 중단된 작업과 같은 전원 관리 이벤트가 수신될 경우 서비스가 응답할 방법을 지정합니다.|  
  
> [!NOTE]
>  이러한 메서드는 서비스가 수명 동안 진행되는 상태를 나타냅니다. 즉, 서비스는 한 상태에서 다음 상태로 전환됩니다. 예를 들어 <xref:System.ServiceProcess.ServiceBase.OnStart%2A>가 호출되기 전에는 서비스가 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 명령에 응답하도록 하지 못합니다.  
  
 중요한 여러 다른 속성 및 메서드가 있습니다. 여기에는 다음이 포함됩니다.  
  
-   <xref:System.ServiceProcess.ServiceBase> 클래스의 <xref:System.ServiceProcess.ServiceBase.Run%2A> 메서드. 서비스의 주 진입점입니다. Windows 서비스 템플릿을 사용하여 서비스를 만드는 경우 응용 프로그램의 `Main` 메서드에 코드를 삽입하여 서비스를 실행합니다. 이 코드는 다음과 같습니다.  
  
     [!code-csharp[VbRadconService#6](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#6)]
     [!code-vb[VbRadconService#6](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#6)]  
  
    > [!NOTE]
    >  이러한 예제에서는 <xref:System.ServiceProcess.ServiceBase> 형식의 배열을 사용합니다. 이 배열에 응용 프로그램에 포함되는 각 서비스를 추가한 다음, 모든 서비스를 함께 실행할 수 있습니다. 하지만 단일 서비스만 만드는 경우에는 배열을 사용하지 않고 <xref:System.ServiceProcess.ServiceBase>에서 상속되는 새 개체를 선언하고 실행하기만 하면 됩니다. 예제는 [How to: Write Services Programmatically](../../../docs/framework/windows-services/how-to-write-services-programmatically.md)(방법: 프로그래밍 방식으로 서비스 작성)를 참조하세요.  
  
-   <xref:System.ServiceProcess.ServiceBase> 클래스에 대한 일련의 속성. 이러한 속성은 서비스에서 호출할 수 있는 메서드를 결정합니다. 예를 들어 <xref:System.ServiceProcess.ServiceBase.CanStop%2A> 속성을 `true`로 설정하면 서비스의 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드를 호출할 수 있습니다. <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> 속성을 `true`로 설정하면 <xref:System.ServiceProcess.ServiceBase.OnPause%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 메서드를 호출할 수 있습니다. 이러한 속성 중 하나를 `true`로 설정하는 경우 관련 메서드에 대한 처리를 재정의 및 정의해야 합니다.  
  
    > [!NOTE]
    >  서비스가 유용하려면 적어도 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnStop%2A>을 재정의해야 합니다.  
  
 <xref:System.ServiceProcess.ServiceController>라는 구성 요소를 사용하여 기존 서비스와 통신하고 서비스의 동작을 제어할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)  
 [방법: Windows 서비스 만들기](../../../docs/framework/windows-services/how-to-create-windows-services.md)
