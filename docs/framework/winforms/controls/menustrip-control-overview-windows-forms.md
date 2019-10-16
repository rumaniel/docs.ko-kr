---
title: MenuStrip 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- MenuStrip
helpviewer_keywords:
- MenuStrip control [Windows Forms], about MenuStrip control
- menus [Windows Forms], creating
ms.assetid: f45516e5-bf01-4468-b851-d45f4c33c055
ms.openlocfilehash: 46a3a25415db77ee261f5fb1c3bf114b2275a2d4
ms.sourcegitcommit: 8c6426a3d2adff5fbcbe1fed0f28eda718c15351
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2019
ms.locfileid: "68733454"
---
# <a name="menustrip-control-overview-windows-forms"></a>MenuStrip 컨트롤 개요(Windows Forms)
메뉴는 공통 테마에 따라 그룹화 된 명령을 포함 하 여 사용자에 게 기능을 노출 합니다.  
  
 이 <xref:System.Windows.Forms.MenuStrip> 컨트롤은 .NET Framework 버전 2.0에서 도입 되었습니다. <xref:System.Windows.Forms.MenuStrip> 컨트롤을 사용 하면 Microsoft Office에 있는 것과 같은 메뉴를 쉽게 만들 수 있습니다.  
  
 컨트롤 <xref:System.Windows.Forms.MenuStrip> 은 MDI (다중 문서 인터페이스) 및 메뉴 병합, 도구 설명 및 오버플로를 지원 합니다. 액세스 키, 바로 가기 키, 확인 표시, 이미지 및 구분 기호를 추가 하 여 메뉴의 유용성 및 가독성을 향상 시킬 수 있습니다.  
  
 컨트롤은 기능을 대체 하 고 <xref:System.Windows.Forms.MainMenu> 컨트롤에 기능을 추가 합니다 <xref:System.Windows.Forms.MainMenu> . 그러나 선택 하는 경우 컨트롤은 이전 버전과의 호환성 및 향후 사용을 위해 유지 됩니다. <xref:System.Windows.Forms.MenuStrip>  
  
## <a name="ways-to-use-the-menustrip-control"></a>MenuStrip 컨트롤을 사용 하는 방법  
 컨트롤을 <xref:System.Windows.Forms.MenuStrip> 사용 하 여 다음을 수행 합니다.  
  
- 텍스트 및 이미지 정렬 및 맞춤, 끌어서 놓기 작업, MDI, 오버플로 및 메뉴 명령 액세스의 대체 모드와 같은 고급 사용자 인터페이스 및 레이아웃 기능을 지 원하는, 일반적으로 사용 되는 사용자 지정 된 메뉴를 쉽게 만들 수 있습니다.  
  
- 운영 체제의 일반적인 모양과 동작을 지원 합니다.  
  
- 다른 컨트롤에 대 한 이벤트를 처리 하는 것과 동일한 방식으로 모든 컨테이너 및 포함 된 항목에 대해 이벤트를 일관 되 게 처리 합니다.  
  
 다음 표에서는 및 관련 클래스의 <xref:System.Windows.Forms.MenuStrip> 일부 특히 중요 한 속성을 보여 줍니다.  
  
|속성|Description|  
|--------------|-----------------|  
|<xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A>|MDI 자식 폼의 <xref:System.Windows.Forms.ToolStripMenuItem> 목록을 표시 하는 데 사용 되는를 가져오거나 설정 합니다.|  
|<xref:System.Windows.Forms.ToolStripItem.MergeAction%2A?displayProperty=nameWithType>|자식 메뉴를 MDI 응용 프로그램의 부모 메뉴와 병합 하는 방법을 가져오거나 설정 합니다.|  
|<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A?displayProperty=nameWithType>|MDI 응용 프로그램의 메뉴 내에서 병합 된 항목의 위치를 가져오거나 설정 합니다.|  
|<xref:System.Windows.Forms.Form.IsMdiContainer%2A?displayProperty=nameWithType>|폼이 MDI 자식 폼의 컨테이너 인지 여부를 나타내는 값을 가져오거나 설정 합니다.|  
|<xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A>|에 대 한 <xref:System.Windows.Forms.MenuStrip>도구 설명이 표시 되는지 여부를 나타내는 값을 가져오거나 설정 합니다.|  
|<xref:System.Windows.Forms.MenuStrip.CanOverflow%2A>|<xref:System.Windows.Forms.MenuStrip>에서 오버플로 기능을 지원하는지를 나타내는 값을 가져오거나 설정합니다.|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A>|연결 된 바로 가기 키를 가져오거나 설정 합니다.는 <xref:System.Windows.Forms.ToolStripMenuItem>합니다.|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>|연결 된 바로 가기 키 여부를 나타내는 값을 가져오거나 설정 합니다 <xref:System.Windows.Forms.ToolStripMenuItem> 옆에 표시 됩니다는 <xref:System.Windows.Forms.ToolStripMenuItem>합니다.|  
  
 다음 표에서는 중요 한 <xref:System.Windows.Forms.MenuStrip> 도우미 클래스를 보여 줍니다.  
  
|클래스|Description|  
|-----------|-----------------|  
|<xref:System.Windows.Forms.ToolStripMenuItem>|에 표시 된 선택 가능한 옵션을 나타내는 <xref:System.Windows.Forms.MenuStrip> 또는 <xref:System.Windows.Forms.ContextMenuStrip>합니다.|  
|<xref:System.Windows.Forms.ContextMenuStrip>|바로 가기 메뉴를 나타냅니다.|  
|<xref:System.Windows.Forms.ToolStripDropDown>|사용자가 <xref:System.Windows.Forms.ToolStripDropDownButton> 또는 더 높은 수준의 메뉴 항목을 클릭할 때 표시 되는 목록에서 단일 항목을 선택할 수 있도록 하는 컨트롤을 나타냅니다.|  
|<xref:System.Windows.Forms.ToolStripDropDownItem>|클릭 하면 드롭다운 항목을 표시 하 <xref:System.Windows.Forms.ToolStripItem> 는에서 파생 된 컨트롤에 대 한 기본 기능을 제공 합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ContextMenuStrip>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripDropDown>
