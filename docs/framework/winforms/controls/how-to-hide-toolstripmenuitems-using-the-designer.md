---
title: '방법: 디자이너를 사용하여 ToolStripMenuItems 숨기기'
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], hiding menu items in designer
- MenuStrip control [Windows Forms], hiding menu items in designer
- menu items [Windows Forms], hiding
ms.assetid: 8f1b057e-3d8a-4f11-88df-935f7b29a836
ms.openlocfilehash: 0e1cd7d1868adabd4d3eec9510f6ee567ba3867d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966612"
---
# <a name="how-to-hide-toolstripmenuitems-using-the-designer"></a>방법: 디자이너를 사용하여 ToolStripMenuItems 숨기기
메뉴 항목을 숨기면 응용 프로그램의 UI (사용자 인터페이스)를 제어 하 고 사용자 명령을 제한 하는 방법입니다. 대부분의 메뉴 항목을 사용할 수 없는 경우 전체 메뉴를 숨기는 것이 좋습니다. 이 경우 사용자에 게 혼란을 덜 수 있습니다. 또한 숨기 더라도 메뉴 또는 메뉴 항목을 숨기 거 나 사용 하지 않도록 설정 하는 것이 좋습니다 .이 경우에는 사용자가 바로 가기 키를 사용 하 여 메뉴 명령에 액세스할 수 있습니다. 메뉴 항목을 [사용 하지 않도록 설정 하는 방법에 대 한 자세한 내용은 방법: 디자이너](how-to-disable-toolstripmenuitems-using-the-designer.md)를 사용 하 여 ToolStripMenuItems를 사용 하지 않도록 설정 합니다.

## <a name="to-hide-a-top-level-menu-and-its-submenu-items"></a>최상위 메뉴와 해당 하위 메뉴 항목을 숨기려면

1. 최상위 메뉴 항목을 선택 하 고 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 또는 <xref:System.Windows.Forms.ToolStripItem.Available%2A> 속성을로 `false`설정 합니다.

     최상위 메뉴 항목을 숨기면 해당 메뉴의 모든 메뉴 항목도 숨겨집니다. 이후에를로 설정 <xref:System.Windows.Forms.MenuStrip> <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 하 `false`는 경우 이외의 다른 위치를 클릭 하면 전체 최상위 메뉴 항목과 해당 하위 메뉴 항목이 폼에서 사라지고 작업의 런타임 효과를 볼 수 있습니다. 디자인 타임에 숨겨진 최상위 메뉴 항목을 표시 하려면 <xref:System.Windows.Forms.MenuStrip> **구성 요소 트레이**, **문서 개요**또는 속성 그리드 위쪽에서를 클릭 합니다.

> [!NOTE]
> 병합 시나리오에서는 MDI (다중 문서 인터페이스) 자식 메뉴를 제외 하 고 전체 메뉴를 숨기는 것이 거의 없습니다.

## <a name="to-hide-a-submenu-item"></a>하위 메뉴 항목을 숨기려면

1. 하위 메뉴 항목을 선택 하 고 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 속성을 `false`로 설정 합니다.

     하위 메뉴 항목을 숨기면 디자인 타임에 폼에 계속 표시 되므로 추가 작업을 위해 쉽게 선택할 수 있습니다. 실제로는 런타임에 숨겨집니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripItem.Visible%2A>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>
- <xref:System.Windows.Forms.ToolStripItem.Available%2A>
- <xref:System.Windows.Forms.ToolStripMenuItem.Overflow%2A>
- [MenuStrip 컨트롤 개요](menustrip-control-overview-windows-forms.md)
- [방법: 디자이너를 사용 하 여 ToolStripMenuItems 비활성화](how-to-disable-toolstripmenuitems-using-the-designer.md)
