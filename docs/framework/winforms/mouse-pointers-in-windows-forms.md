---
title: Windows Forms의 마우스 포인터
ms.date: 03/30/2017
helpviewer_keywords:
- pointers [Windows Forms], setting
- mouse pointers
- mouse cursors
- mouse pointers [Windows Forms], setting
- cursors [Windows Forms], setting
- mouse [Windows Forms], cursors
ms.assetid: c3400d85-de5b-42e8-abc3-d6088d69ee53
ms.openlocfilehash: e9b572ba40618a72b8db58917008ebd61a23de79
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61800786"
---
# <a name="mouse-pointers-in-windows-forms"></a>Windows Forms의 마우스 포인터
마우스 *포인터*, 커서도 참조 되는 경우에 따라 있는 마우스를 사용 하 여 사용자 입력에 대 한 화면에서 포커스 지점을 지정 하는 비트맵입니다. 이 항목에서는 Windows Forms에서 마우스 포인터의 개요를 제공 하 고 수정 하 고 마우스 포인터를 제어 하는 방법 중 일부를 설명 합니다.  
  
## <a name="accessing-the-mouse-pointer"></a>마우스 포인터에 액세스  
 마우스 포인터를 표현 합니다 <xref:System.Windows.Forms.Cursor> 클래스 및 각 <xref:System.Windows.Forms.Control> 에 <xref:System.Windows.Forms.Control.Cursor%2A?displayProperty=nameWithType> 해당 컨트롤에 대 한 포인터를 지정 하는 속성. <xref:System.Windows.Forms.Cursor> 클래스와 같은 포인터를 설명 하는 속성을 포함 합니다 <xref:System.Windows.Forms.Cursor.Position%2A> 및 <xref:System.Windows.Forms.Cursor.HotSpot%2A> 속성과 같은 포인터의 모양을 수정할 수 있는 메서드를 <xref:System.Windows.Forms.Cursor.Show%2A>, <xref:System.Windows.Forms.Cursor.Hide%2A>, 및 <xref:System.Windows.Forms.Cursor.DrawStretched%2A> 메서드입니다.  
  
## <a name="controlling-the-mouse-pointer"></a>마우스 포인터를 제어합니다.  
 경우에 따라 다음 마우스 포인터를 사용할 수 있습니다 또는 마우스 위치를 변경할 영역을 제한 하는 것이 좋습니다. 가져오거나 사용 하 여 마우스의 현재 위치를 설정할 수는 <xref:System.Windows.Forms.Cursor.Position%2A> 의 속성을 <xref:System.Windows.Forms.Cursor>입니다. 또한 마우스 포인터를 사용할 수 있습니다 영역을 제한할 수 있습니다 설정 수는 <xref:System.Windows.Forms.Cursor.Clip%2A> 속성입니다. 기본적으로 클립 영역에서 전체 화면입니다.  
  
## <a name="changing-the-mouse-pointer"></a>마우스 포인터를 변경합니다.  
 사용자에 게 피드백을 제공 하는 가장 좋은 방법은 마우스 포인터를 변경 합니다. 예를 들어 처리기에서 마우스 포인터를 수정할 수 있습니다 합니다 <xref:System.Windows.Forms.Control.MouseEnter> 고 <xref:System.Windows.Forms.Control.MouseLeave> 계산이 수행 되는 사용자에 게 알림 컨트롤에서 사용자 상호 작용을 제한 하는 이벤트입니다. 경우에 따라 마우스 포인터를 끌어서 놓기 작업에서 응용 프로그램이 포함 된 경우 등, 시스템 이벤트로 인해 변경 됩니다.  
  
 설정 된 경우 마우스 포인터를 변경 하는 기본 방법은 합니다 <xref:System.Windows.Forms.Control.Cursor%2A?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.Control.DefaultCursor%2A> 새 컨트롤의 속성 <xref:System.Windows.Forms.Cursor>합니다. 마우스 포인터를 변경 하는 예제 코드 예제를 보려면를 <xref:System.Windows.Forms.Cursor> 클래스입니다. 또한 합니다 <xref:System.Windows.Forms.Cursors> 클래스의 집합을 노출 <xref:System.Windows.Forms.Cursor> 다양 한 유형의 손 모양의 하는 포인터와 같은 포인터에 대 한 개체입니다. 마우스 포인터가 컨트롤에 있는 때마다 모래 시계와 유사한, 대기 포인터를 표시 하려면 사용 합니다 <xref:System.Windows.Forms.Control.UseWaitCursor%2A> 속성의는 <xref:System.Windows.Forms.Control> 클래스.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Cursor>
- [Windows Forms 애플리케이션의 마우스 입력](mouse-input-in-a-windows-forms-application.md)
- [Windows Forms에서의 끌어서 놓기 기능](drag-and-drop-functionality-in-windows-forms.md)
