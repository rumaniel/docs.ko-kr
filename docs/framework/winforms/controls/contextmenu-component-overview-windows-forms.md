---
title: ContextMenu 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ContextMenu
helpviewer_keywords:
- ContextMenu component [Windows Forms], about ContextMenu component
- context menus [Windows Forms], ContextMenu component
- shortcut menus [Windows Forms], ContextMenu component
ms.assetid: 49d6398f-d3c4-4679-84fa-1de07b68b05e
ms.openlocfilehash: 6ae7817bc158f30fbf55b5f6228ecdf134d6657d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962183"
---
# <a name="contextmenu-component-overview-windows-forms"></a>ContextMenu 구성 요소 개요(Windows Forms)
> [!IMPORTANT]
> 및 <xref:System.Windows.Forms.MenuStrip> 는이전<xref:System.Windows.Forms.MainMenu> 버전 의및<xref:System.Windows.Forms.ContextMenu> 컨트롤에 기능을 추가 하 고 추가 하지만를 선택 하는 경우 이전 버전과의 호환성 및 향후 사용에 대해 모두 유지 됩니다.<xref:System.Windows.Forms.ContextMenu> <xref:System.Windows.Forms.MainMenu> <xref:System.Windows.Forms.ContextMenuStrip>  
  
 Windows Forms <xref:System.Windows.Forms.ContextMenu> 구성 요소를 사용 하 여 선택한 개체와 연결 된 자주 사용 되는 명령의 바로 가기 메뉴를 사용자에 게 제공할 수 있습니다. 바로 가기 메뉴의 항목은 종종 응용 프로그램의 다른 위치에 표시 되는 주 메뉴의 항목 하위 집합입니다. 일반적으로 사용자는 마우스 오른쪽 단추를 클릭 하 여 바로 가기 메뉴에 액세스할 수 있습니다. Windows Forms에서 바로 가기 메뉴는 컨트롤과 연결 됩니다.  
  
## <a name="key-properties"></a>키 속성  
 컨트롤의 <xref:System.Windows.Forms.Control.ContextMenu%2A> 속성 <xref:System.Windows.Forms.ContextMenu> 을 구성 요소로 설정 하 여 바로 가기 메뉴를 컨트롤과 연결할 수 있습니다. 단일 바로 가기 메뉴를 여러 컨트롤에 연결할 수 있지만 각 컨트롤에는 바로 가기 메뉴 하나만 있을 수 있습니다.  
  
 <xref:System.Windows.Forms.ContextMenu> 구성 요소의<xref:System.Windows.Forms.Menu.MenuItems%2A> 키 속성은 속성입니다. 프로그래밍 방식으로 개체를 만들어 <xref:System.Windows.Forms.MenuItem> 바로 가기 메뉴의에 <xref:System.Windows.Forms.Menu.MenuItemCollection> 추가 하 여 메뉴 항목을 추가할 수 있습니다. 바로 가기 메뉴의 항목은 일반적으로 다른 메뉴에서 그려지며 항목을 복사 하 여 바로 가기 메뉴에 항목을 추가 하는 경우가 가장 많습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ContextMenu>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ContextMenuStrip>
