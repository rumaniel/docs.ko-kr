---
title: ToolStrip 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- Toolstrip
helpviewer_keywords:
- ToolStrip control [Windows Forms], about ToolStrip control
- toolbars [Windows Forms], what's new in Windows Forms
- toolbars [Windows Forms]
- what's new [Windows Forms], toolbars
ms.assetid: 81d067ed-297c-4dad-90de-1bcac15336ec
ms.openlocfilehash: 75df256f852b45af4bc6cf519c13ccd62ae1d689
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64654766"
---
# <a name="toolstrip-control-overview-windows-forms"></a>ToolStrip 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ToolStrip> 컨트롤 및 해당 관련된 클래스 도구 모음, 상태 표시줄 및 메뉴를 사용자 인터페이스 요소를 결합 하는 것에 대 한 일반적인 프레임 워크를 제공 합니다. <xref:System.Windows.Forms.ToolStrip> 컨트롤 도구 모음의 가로 또는 세로 공간을 공유할 수 있는 내부 활성화와 편집, 사용자 지정 레이아웃 및 래프팅 (rafting)를 비롯 한 다양 한 디자인 타임 환경을 제공 합니다.  
  
 하지만 <xref:System.Windows.Forms.ToolStrip> 대체 하 고 이전 버전에서는 컨트롤에 기능 추가 <xref:System.Windows.Forms.ToolBar> 원하는 경우 이전 버전과 호환성 및 향후 사용을 위해 유지 됩니다.  
  
## <a name="features-of-the-toolstrip-controls"></a>ToolStrip 컨트롤의 기능  
 사용 된 <xref:System.Windows.Forms.ToolStrip> 컨트롤:  
  
- 컨테이너 간에 공통 사용자 인터페이스를 제공 합니다.  
  
- 쉽게 사용자 지정 만들기를 지 원하는 일반적인된 도구 모음 사용자 인터페이스 및 레이아웃 기능, 고급 텍스트 및 이미지, 드롭다운 단추 및 컨트롤을 래프팅, 도킹 단추와 같은 오버플로 단추 및 다시 정렬 런타임 <xref:System.Windows.Forms.ToolStrip> 항목입니다.  
  
- 오버플로 및 런타임 항목 다시 정렬을 지원 합니다. 오버플로 기능 이동 항목 드롭다운 메뉴에 표시할 만큼 충분 한 공간이 없을 때를 <xref:System.Windows.Forms.ToolStrip>입니다.  
  
- 일반적인 모양 및 동작의 일반적인 렌더링 모델을 통해 운영 체제를 지원 합니다.  
  
- 다른 컨트롤에 대 한 이벤트를 처리 하는 동일한 방식으로 모든 컨테이너 및 포함 된 항목에 대해 일관 되 게 이벤트를 처리 합니다.  
  
- 항목을 끌어올 <xref:System.Windows.Forms.ToolStrip> 간 또는 한 <xref:System.Windows.Forms.ToolStrip>합니다.  
  
- 고급 레이아웃을 사용 하 여 드롭다운 목록 컨트롤 및 사용자 인터페이스 형식 편집기 만들기를 <xref:System.Windows.Forms.ToolStripDropDown>입니다.  
  
 사용 합니다 <xref:System.Windows.Forms.ToolStripControlHost> 에서 다른 컨트롤을 사용 하는 클래스를 <xref:System.Windows.Forms.ToolStrip> 얻고이 <xref:System.Windows.Forms.ToolStrip> 에 기능.  
  
 기능을 확장 하 고 사용 하 여 모양과 동작을 수정할 수는 <xref:System.Windows.Forms.ToolStripRenderer>, <xref:System.Windows.Forms.ToolStripProfessionalRenderer>, 및 <xref:System.Windows.Forms.ToolStripManager> 와 함께 합니다 <xref:System.Windows.Forms.ToolStripRenderMode> 및 <xref:System.Windows.Forms.ToolStripManagerRenderMode> 열거형입니다.  
  
 <xref:System.Windows.Forms.ToolStrip> 컨트롤은 항상 구성이 가능 하며 확장 가능 하며 여러 속성, 메서드 및 이벤트 모양 및 동작을 사용자 지정할 수 있습니다. 몇 가지 중요 한 멤버는 다음과 같습니다.  
  
### <a name="important-toolstrip-members"></a>중요 한 ToolStrip 멤버  
  
|이름|설명|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStrip.Dock%2A>|부모 컨테이너의 가장자리를 가져오거나 설정 합니다.는 <xref:System.Windows.Forms.ToolStrip> 에 도킹 됩니다.|  
|<xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A>|<xref:System.Windows.Forms.ToolStrip> 클래스를 통해 끌어서 놓기와 항목 다시 정렬을 전용으로 처리할지를 나타내는 값을 가져오거나 설정합니다.|  
|<xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>|나타내는 값을 가져오거나 하는 방법을 <xref:System.Windows.Forms.ToolStrip> 해당 항목을 배치 합니다.|  
|<xref:System.Windows.Forms.ToolStripItem.Overflow%2A>|가져오거나 설정 여부를 <xref:System.Windows.Forms.ToolStripItem> 에 연결할 때 합니다 <xref:System.Windows.Forms.ToolStrip> 또는 <xref:System.Windows.Forms.ToolStripOverflowButton> 또는 둘 사이의 부동 상태로 있을 수 있습니다.|  
|<xref:System.Windows.Forms.ToolStrip.IsDropDown%2A>|나타내는 값을 가져옵니다 여부를 <xref:System.Windows.Forms.ToolStripItem> 드롭다운 목록에서 다른 항목을 표시 때 목록을 <xref:System.Windows.Forms.ToolStripItem> 를 클릭 합니다.|  
|<xref:System.Windows.Forms.ToolStrip.OverflowButton%2A>|오버플로가 활성화된 <xref:System.Windows.Forms.ToolStrip>에 대한 오버플로 단추인 <xref:System.Windows.Forms.ToolStripItem>을 가져옵니다.|  
|<xref:System.Windows.Forms.ToolStrip.Renderer%2A>|가져오거나를 <xref:System.Windows.Forms.ToolStripRenderer> 모양 및 동작 (모양 및 느낌)의 사용자 지정 하는 데는 <xref:System.Windows.Forms.ToolStrip>합니다.|  
|<xref:System.Windows.Forms.ToolStrip.RenderMode%2A>|적용할 것 그리기 스타일을 가져오거나 설정 합니다.는 <xref:System.Windows.Forms.ToolStrip>합니다.|  
|<xref:System.Windows.Forms.ToolStrip.RendererChanged>|<xref:System.Windows.Forms.ToolStrip.Renderer%2A> 속성이 변경되면 발생합니다.|  
  
 <xref:System.Windows.Forms.ToolStrip> 컨트롤의 유연성은 다양 한 도우미 클래스를 사용 하 여 수행 됩니다. 다음은 가장 중요 한 일부입니다.  
  
### <a name="important-toolstrip-companion-classes"></a>ToolStrip에 중요 한 역할 클래스  
  
|이름|설명|  
|----------|-----------------|  
|<xref:System.Windows.Forms.MenuStrip>|대체 하 고 기능을 추가 합니다 <xref:System.Windows.Forms.MainMenu> 클래스입니다.|  
|<xref:System.Windows.Forms.StatusStrip>|대체 하 고 기능을 추가 합니다 <xref:System.Windows.Forms.StatusBar> 클래스입니다.|  
|<xref:System.Windows.Forms.ContextMenuStrip>|대체 하 고 기능을 추가 합니다 <xref:System.Windows.Forms.ContextMenu> 클래스입니다.|  
|<xref:System.Windows.Forms.ToolStripItem>|이벤트 및 모든 요소에 대 한 레이아웃을 관리 하는 추상 기본 클래스는를 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.ToolStripControlHost>, 또는 <xref:System.Windows.Forms.ToolStripDropDown> 포함 될 수 있습니다.|  
|<xref:System.Windows.Forms.ToolStripContainer>|다양 한 방법으로 제어를 정렬할 수 있는 폼의 양쪽 패널을 사용 하 여 컨테이너를 제공 합니다.|  
|<xref:System.Windows.Forms.ToolStripRenderer>|에 대 한 그리기 기능을 처리 <xref:System.Windows.Forms.ToolStrip> 개체입니다.|  
|<xref:System.Windows.Forms.ToolStripProfessionalRenderer>|Microsoft Office 스타일 모양을 제공합니다.|  
|<xref:System.Windows.Forms.ToolStripManager>|컨트롤 <xref:System.Windows.Forms.ToolStrip> 렌더링 및 래프팅 및 병합 <xref:System.Windows.Forms.MenuStrip>를 <xref:System.Windows.Forms.ToolStripDropDownMenu>, 및 <xref:System.Windows.Forms.ToolStripMenuItem> 개체입니다.|  
|<xref:System.Windows.Forms.ToolStripManagerRenderMode>|여러 적용할 그리기 스타일 (사용자 지정 Windows XP 또는 Microsoft Office Professional)을 지정 <xref:System.Windows.Forms.ToolStrip> 폼에 포함 된 개체입니다.|  
|<xref:System.Windows.Forms.ToolStripRenderMode>|하나에 적용 되는 그리기 스타일 (사용자 지정 Windows XP 또는 Microsoft Office Professional) 지정 <xref:System.Windows.Forms.ToolStrip> 폼에 포함 된 개체입니다.|  
|<xref:System.Windows.Forms.ToolStripControlHost>|특히 되지 않는 다른 컨트롤을 호스트 <xref:System.Windows.Forms.ToolStrip> 컨트롤 이지만 하려는 <xref:System.Windows.Forms.ToolStrip> 기능입니다.|  
|<xref:System.Windows.Forms.ToolStripItemPlacement>|지정 여부를 <xref:System.Windows.Forms.ToolStripItem> 주에 배치 하는 것 <xref:System.Windows.Forms.ToolStrip>, 오버플로에 <xref:System.Windows.Forms.ToolStrip>, 하거나 사용 하지 않도록 합니다.|  
  
 자세한 내용은 [ToolStrip 기술 요약](toolstrip-technology-summary.md) 하 고 [ToolStrip 컨트롤 아키텍처](toolstrip-control-architecture.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ContextMenuStrip>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripDropDown>
