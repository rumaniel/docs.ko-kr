---
title: Windows Forms에서의 끌어서 놓기 기능
ms.date: 03/30/2017
helpviewer_keywords:
- drag and drop [Windows Forms], Windows Forms
- Windows Forms, drag and drop
ms.assetid: 65cd2c03-8782-474e-b958-cbe43eeb902c
ms.openlocfilehash: 437b632706b27cd487d60c2ad23db3f9a3c96c09
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61966873"
---
# <a name="drag-and-drop-functionality-in-windows-forms"></a>Windows Forms에서의 끌어서 놓기 기능
Windows Forms에는 끌어서 놓기 동작을 구현하는 메서드, 이벤트 및 클래스 집합이 포함되어 있습니다. 이 항목에서는 Windows Forms의 끌어서 놓기 지원에 대해 개괄적으로 설명합니다.  도 참조 하세요 [끌어서 놓기 작업 및 클립보드 지원](./advanced/drag-and-drop-operations-and-clipboard-support.md)합니다.  
  
## <a name="performing-drag-and-drop-operations"></a>끌어서 놓기 작업 수행  
 끌어서 놓기 작업을 수행하려면 <xref:System.Windows.Forms.Control> 클래스의 <xref:System.Windows.Forms.Control.DoDragDrop%2A> 메서드를 사용합니다. 끌어서 놓기 작업을 수행하는 방법에 대한 자세한 내용은 <xref:System.Windows.Forms.Control.DoDragDrop%2A>을 참조하세요. 끌어서 놓기 작업이 시작되기 전에 마우스 포인터를 위로 끌어와야 하는 사각형을 가져오려면 <xref:System.Windows.Forms.SystemInformation> 클래스의 <xref:System.Windows.Forms.SystemInformation.DragSize%2A> 속성을 사용합니다.  
  
## <a name="events-related-to-drag-and-drop-operations"></a>끌어서 놓기 작업과 관련된 이벤트  
 끌어서 놓기 작업에는 두 가지 범주의 이벤트가 있습니다. 하나는 끌어서 놓기 작업의 현재 대상에서 발생하는 이벤트이고, 다른 하나는 끌어서 놓기 작업의 소스에서 발생하는 이벤트입니다.  
  
### <a name="events-on-the-current-target"></a>현재 대상의 이벤트  
 다음 표에서는 끌어서 놓기 작업의 현재 대상에서 발생하는 이벤트를 보여 줍니다.  
  
|마우스 이벤트|설명|  
|-----------------|-----------------|  
|<xref:System.Windows.Forms.Control.DragEnter>|이 이벤트는 개체를 컨트롤의 범위로 끌어올 때 발생합니다. 이 이벤트의 처리기는 <xref:System.Windows.Forms.DragEventArgs> 형식의 인수를 받습니다.|  
|<xref:System.Windows.Forms.Control.DragOver>|이 이벤트는 마우스 포인터가 컨트롤의 범위 내에 있는 동안 개체를 끌 때 발생합니다. 이 이벤트의 처리기는 <xref:System.Windows.Forms.DragEventArgs> 형식의 인수를 받습니다.|  
|<xref:System.Windows.Forms.Control.DragDrop>|이 이벤트는 끌어서 놓기 작업이 완료될 때 발생합니다. 이 이벤트의 처리기는 <xref:System.Windows.Forms.DragEventArgs> 형식의 인수를 받습니다.|  
|<xref:System.Windows.Forms.Control.DragLeave>|이 이벤트는 컨트롤의 범위 밖으로 개체를 끌 때 발생합니다. 이 이벤트의 처리기는 <xref:System.EventArgs> 형식의 인수를 받습니다.|  
  
 <xref:System.Windows.Forms.DragEventArgs> 클래스는 마우스 포인터의 위치, 마우스 단추의 현재 상태 및 키보드의 한정자 키, 끄는 데이터, 끌기 이벤트의 소스에서 허용되는 작업과 작업의 대상 놓기 효과를 지정하는 <xref:System.Windows.Forms.DragDropEffects> 값을 제공합니다.  
  
### <a name="events-on-the-source"></a>소스의 이벤트  
 다음 표에서는 끌어서 놓기 작업의 소스에서 발생하는 이벤트를 보여 줍니다.  
  
|마우스 이벤트|설명|  
|-----------------|-----------------|  
|<xref:System.Windows.Forms.Control.GiveFeedback>|이 이벤트는 끌기 작업 중에 발생합니다. 마우스 포인터 변경 등 끌어서 드롭 작업이 발생하고 있음을 알리는 시각 신호를 사용자에게 제공할 수 있습니다. 이 이벤트의 처리기는 <xref:System.Windows.Forms.GiveFeedbackEventArgs> 형식의 인수를 받습니다.|  
|<xref:System.Windows.Forms.Control.QueryContinueDrag>|이 이벤트는 끌어서 놓기 작업 중에 발생하며 끌기 소스가 끌어서 놓기 작업을 취소해야 할지를 결정하도록 합니다. 이 이벤트의 처리기는 <xref:System.Windows.Forms.QueryContinueDragEventArgs> 형식의 인수를 받습니다.|  
  
 <xref:System.Windows.Forms.QueryContinueDragEventArgs> 클래스는 마우스 단추의 현재 상태 및 키보드의 한정자 키, Esc 키를 눌렀는지 여부를 지정하는 값, 끌어서 놓기 작업을 계속할지 여부를 지정하기 위해 설정할 수 있는 <xref:System.Windows.Forms.DragAction> 값을 제공합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms 애플리케이션의 마우스 입력](mouse-input-in-a-windows-forms-application.md)
