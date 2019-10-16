---
title: Windows Forms의 전원 관리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- battery states
- power states
ms.assetid: ad04a801-5682-4d88-92c5-26eb9cdb209a
ms.openlocfilehash: 36c152a9e388fe61b1c82a8783bf74bbe6c8f123
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592511"
---
# <a name="power-management-in-windows-forms"></a>Windows Forms의 전원 관리
Windows Forms 응용 프로그램 Windows 운영 체제에서 전원 관리 기능 활용을 걸릴 수 있습니다. 응용 프로그램 컴퓨터의 전원 상태를 모니터링 하 고 상태 변경이 발생할 때 작업을 수행할 수 있습니다. 예를 들어, 응용 프로그램 휴대용 컴퓨터를 실행 하는 경우 컴퓨터의 배터리 충전량 특정 수준에 속하는 경우 응용 프로그램의 특정 기능을 사용 하지 않도록 설정 하는 것이 좋습니다.  
  
 .NET Framework에서 제공 된 <xref:Microsoft.Win32.SystemEvents.PowerModeChanged> AC 전원 상태 또는 배터리 상태를 변경 하는 경우 또는 사용자 일시 중단 하거나 운영 체제를 다시 시작 하는 등 전원 상태가 변경 될 때마다 발생 하는 이벤트입니다. <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> 속성의는 <xref:System.Windows.Forms.SystemInformation> 클래스 수 있습니다 다음 코드 예제에 표시 된 대로 현재 상태에 대 한 쿼리를 사용 합니다.  
  
 [!code-csharp[PowerMode#1](~/samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#1)]
 [!code-vb[PowerMode#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#1)]  
  
 외에 합니다 <xref:System.Windows.Forms.BatteryChargeStatus> 열거형을 <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> 속성 열거형 배터리 용량을 결정 하는 데에 포함 되어 있습니다 (<xref:System.Windows.Forms.PowerStatus.BatteryFullLifetime%2A>) 및 배터리 백분율 요금이 부과 됩니다 (<xref:System.Windows.Forms.PowerStatus.BatteryLifePercent%2A>, <xref:System.Windows.Forms.PowerStatus.BatteryLifeRemaining%2A>).  
  
 사용할 수는 <xref:System.Windows.Forms.Application.SetSuspendState%2A> 메서드는 <xref:System.Windows.Forms.Application> 컴퓨터 최대 절전 모드로 전환 하거나 일시 중단 모드입니다. 경우는 `force` 인수가로 설정 된 `false`, 운영 체제 이벤트 일시 중단 하는 권한을 요청 하는 모든 응용 프로그램에 브로드캐스트 됩니다. 경우는 `disableWakeEvent` 인수가로 설정 된 `true`, 운영 체제 절전 모드 해제 이벤트를 모두 사용 하지 않도록 설정 합니다.  
  
 다음 코드 예제에서는 컴퓨터 최대 절전 모드로 전환 하는 방법에 설명 합니다.  
  
 [!code-csharp[PowerMode#2](~/samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#2)]
 [!code-vb[PowerMode#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.Win32.SystemEvents.PowerModeChanged>
- <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>
- <xref:System.Windows.Forms.Application.SetSuspendState%2A>
- <xref:Microsoft.Win32.SystemEvents.SessionSwitch>
