---
title: Windows Forms 애플리케이션의 사용자 입력
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, user input
ms.assetid: 9d61fa96-70f7-4754-885a-49a4a6316bdb
ms.openlocfilehash: 0eb39f0ecd8fcd12918b38bd77fed2ff32cac1d8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61800141"
---
# <a name="user-input-in-a-windows-forms-application"></a>Windows Forms 애플리케이션의 사용자 입력
Windows Forms에서 사용자 입력은 Windows 메시지 형식으로의 응용 프로그램에 전송 됩니다. 일련의 재정의 가능한 메서드를 폼을 응용 프로그램에서 이러한 메시지를 처리 하 고 수준을 제어 합니다. 이러한 메서드는 마우스 및 키보드 메시지를 수신 하는 경우 입력 키보드 또는 마우스에 대 한 정보를 처리할 수 있는 이벤트를 발생 시킵니다. 대부분의 경우에서 Windows Forms 응용 프로그램은 이러한 이벤트를 처리 하면 모든 사용자 입력을 처리할 수 됩니다. 다른 경우에 응용 프로그램에 응용 프로그램, 폼 또는 컨트롤에 의해 수신 되기 전에 특정 메시지를 차단 하기 위해 메시지를 처리 하는 방법 중 하나를 재정의 해야 합니다.  
  
## <a name="mouse-and-keyboard-events"></a>마우스 및 키보드 이벤트  
 모든 Windows Forms 컨트롤에 관련 된 마우스 및 키보드 입력 이벤트 집합을 상속 합니다. 예를 들어, 컨트롤을 처리할 수는 <xref:System.Windows.Forms.Control.KeyPress> 누른 키의 문자 코드를 확인 하려면 이벤트 또는 컨트롤을 처리할 수는 <xref:System.Windows.Forms.Control.MouseClick> 클릭 마우스의 위치를 결정 하는 이벤트입니다. 마우스 및 키보드 이벤트에 대 한 자세한 내용은 참조 하세요. [키보드 이벤트를 사용 하 여](using-keyboard-events.md) 하 고 [Windows Forms의 마우스 이벤트](mouse-events-in-windows-forms.md)합니다.  
  
## <a name="methods-that-process-user-input-messages"></a>사용자 입력된 메시지를 처리 하는 방법  
 폼 및 컨트롤에 액세스할 수는 <xref:System.Windows.Forms.IMessageFilter> 인터페이스 및 메시지 큐의 다른 지점에서 Windows 메시지를 처리 하는 재정의 가능한 메서드 집합이 있습니다. 모든 이러한 메서드는 <xref:System.Windows.Forms.Message> Windows 메시지의 하위 수준 세부 정보를 캡슐화 하는 매개 변수입니다. 구현 하거나 메시지를 검토 하 고 메시지를 사용 하거나 다음 소비자는 메시지 큐에 전달 이러한 메서드를 재정의할 수 있습니다. 다음 표에서 Windows Forms에 있는 모든 Windows 메시지를 처리 하는 메서드를 제공 합니다.  
  
|메서드|노트|  
|------------|-----------|  
|<xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A>|이 메서드는 응용 프로그램 수준 (라고도 게시) Windows 메시지를 큐에 대기를 차단합니다.|  
|<xref:System.Windows.Forms.Control.PreProcessMessage%2A>|이 메서드는 처리 전에 폼과 컨트롤 수준에서 Windows 메시지를 차단 합니다.|  
|<xref:System.Windows.Forms.Control.WndProc%2A>|이 메서드는 폼과 컨트롤 수준에서 Windows 메시지를 처리합니다.|  
|<xref:System.Windows.Forms.Control.DefWndProc%2A>|이 메서드는 폼과 컨트롤 수준에서 Windows 메시지의 기본 처리를 수행합니다. 이 창에 최소한의 기능을 제공 합니다.|  
|<xref:System.Windows.Forms.Control.OnNotifyMessage%2A>|이 메서드는 처리 된 후 폼과 컨트롤 수준에서 메시지를 차단 합니다. <xref:System.Windows.Forms.ControlStyles.EnableNotifyMessage> 이 메서드를 호출할 수에 대 한 스타일 비트를 설정 해야 합니다.|  
  
 키보드 및 마우스 메시지가 해당 유형의 메시지에만 적용 되는 재정의 가능한 메서드 집합을 추가 하 여 처리 됩니다. 자세한 내용은 [키보드 입력 작동 방식](how-keyboard-input-works.md) 하 고 [Windows Forms의 마우스 입력 방법](how-mouse-input-works-in-windows-forms.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms에 사용자 입력](user-input-in-windows-forms.md)
- [Windows Forms 응용 프로그램의 키보드 입력](keyboard-input-in-a-windows-forms-application.md)
- [Windows Forms 애플리케이션의 마우스 입력](mouse-input-in-a-windows-forms-application.md)
