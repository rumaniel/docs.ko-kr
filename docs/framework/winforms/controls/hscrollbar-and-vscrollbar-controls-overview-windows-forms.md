---
title: HScrollBar 및 VScrollBar 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- HScrollBar
- VScrollBar
helpviewer_keywords:
- ScrollBar control [Windows Forms]
- HScrollBar control [Windows Forms], about HScrollBar
- VScrollBar control [Windows Forms], about VScrollBar control
- ScrollBar control [Windows Forms], about ScrollBar control
- scroll bars [Windows Forms], about scroll bars
ms.assetid: 8b307679-1cae-41d8-99aa-3d1efd207cd6
ms.openlocfilehash: d4a7912a5781fc583357affa728f7d81059b5cf9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61928576"
---
# <a name="hscrollbar-and-vscrollbar-controls-overview-windows-forms"></a>HScrollBar 및 VScrollBar 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ScrollBar> 컨트롤은 가로로 또는 세로로 응용 프로그램 또는 컨트롤 내에서 쉽게 탐색 긴 목록 항목 또는 많은 양의 정보를 제공 하는 데 사용 됩니다. 스크롤 막대는 Windows 인터페이스의 공통 요소 이므로 <xref:System.Windows.Forms.ScrollBar> 컨트롤에서 파생 되지 않은 컨트롤을 사용 하 여 흔히는 <xref:System.Windows.Forms.ScrollableControl> 클래스입니다. 통합 하기 위해 많은 개발자 선택 마찬가지로 <xref:System.Windows.Forms.ScrollBar> 자체 사용자 정의 컨트롤을 작성 하는 경우를 제어 합니다.  
  
 합니다 <xref:System.Windows.Forms.HScrollBar> (수평) 및 <xref:System.Windows.Forms.VScrollBar> (세로) 컨트롤을 다른 컨트롤에서 독립적으로 작동할 수 있고 자체 이벤트, 속성 및 메서드 집합입니다. <xref:System.Windows.Forms.ScrollBar> 컨트롤은 텍스트 상자나 목록 상자, 콤보 상자, MDI 폼에 연결 되어 있는 기본 제공 스크롤 막대와 동일 하지 않습니다 (합니다 <xref:System.Windows.Forms.TextBox> 컨트롤에는 <xref:System.Windows.Forms.TextBox.ScrollBars%2A> 속성을 컨트롤에 연결 되어 있는 스크롤 막대 표시 또는 숨기기).  
  
 합니다 <xref:System.Windows.Forms.ScrollBar> 사용을 제어 합니다 <xref:System.Windows.Forms.ScrollBar.Scroll> 스크롤 막대에 스크롤 상자 (엄지 단추 라고도 함)의 움직임을 모니터링 하는 이벤트입니다. 사용 하는 <xref:System.Windows.Forms.ScrollBar.Scroll> 이벤트를 끄는 대로 스크롤 막대의 값에 대 한 액세스를 제공 합니다.  
  
## <a name="value-property"></a>값 속성  
 합니다 <xref:System.Windows.Forms.ScrollBar.Value%2A> 속성 (즉, 기본적으로 0)는는 `integer` 스크롤 막대의 스크롤 상자 위치에 해당 하는 값입니다. 스크롤 상자 위치를 최소 값인 경우의 가장 왼쪽 위치 (가로 스크롤 막대) 또는 세로 스크롤 막대를 위쪽 위치를 이동 합니다. 스크롤 상자의 경우 최 댓 값, 맨 오른쪽으로 스크롤 상자 이동 이나 아래쪽 위치. 마찬가지로, 중간 및 범위의 상한 값 스크롤 상자 중간 스크롤 막대의 선행 가장자리를 배치합니다.  
  
 스크롤 막대의 값을 변경 하려면 마우스 클릭을 사용 하는 것 외에도 사용자 막대를 따라 모든 지점으로 사용 하는 스크롤 상자를 끌 수도 있습니다. 결과 값의 스크롤 상자 위치에 따라 달라 지지만 범위 내 합니다 <xref:System.Windows.Forms.ScrollBar.Minimum%2A> 에 <xref:System.Windows.Forms.ScrollBar.Maximum%2A> 사용자가 설정 된 속성입니다.  
  
## <a name="largechange-and-smallchange-properties"></a>LargeChange 및 SmallChange 속성  
 사용자가 PAGE UP 또는 PAGE DOWN 키를 누르거나 스크롤 상자 옆에 있는 스크롤 막대 트랙에서 클릭할 때 합니다 <xref:System.Windows.Forms.ScrollBar.Value%2A> 에 설정 된 값에 따라 속성 변경 내용을 <xref:System.Windows.Forms.ScrollBar.LargeChange%2A> 속성.  
  
 키 또는 스크롤 막대 단추 중 하나를 클릭할 때 사용자가 누를 화살표 중 하나는 <xref:System.Windows.Forms.ScrollBar.Value%2A> 에 설정 된 값에 따라 속성 변경 내용을 <xref:System.Windows.Forms.ScrollBar.SmallChange%2A> 속성입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.HScrollBar>
- <xref:System.Windows.Forms.VScrollBar>
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
