---
title: '방법: ToolStripMenuItems를 사용하지 않도록 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], enabling
- ToolStripMenuItems [Windows Forms], disabling
- menu items [Windows Forms], disabling
- disabling menu items
- menu items [Windows Forms], enabling
- menus [Windows Forms], disabling menu items
ms.assetid: bcc1da84-50fd-41d2-8475-103b581d5654
ms.openlocfilehash: f86a2934e799e4604693491dacbecc517d44d810
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046221"
---
# <a name="how-to-disable-toolstripmenuitems"></a>방법: ToolStripMenuItems를 사용하지 않도록 설정
사용자 활동에 대 한 응답으로 메뉴 항목을 사용 하거나 사용 하지 않도록 설정 하 여 사용자가 수행할 수 있는 명령을 제한 하거나 넓힐 수 있습니다. 메뉴 항목은 만들어질 때 기본적으로 사용 하도록 설정 되지만 속성을 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> 통해 조정할 수 있습니다. 디자인 타임에 **속성** 창에서이 속성을 조작 하거나 코드에서이 속성을 설정 하 여 프로그래밍 방식으로 조작할 수 있습니다.  
  
### <a name="to-disable-a-menu-item-programmatically"></a>프로그래밍 방식으로 메뉴 항목을 사용 하지 않도록 설정 하려면  
  
- 메뉴 항목의 속성을 설정 하는 메서드 내에서 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> `false`속성을 설정 하는 코드를 추가 합니다.  
  
    ```vb  
    MenuItem1.Enabled = False  
    ```  
  
    ```csharp  
    menuItem1.Enabled = false;  
    ```  
  
    ```cpp  
    menuItem1->Enabled = false;  
    ```  
  
    > [!TIP]
    > 메뉴의 첫 번째 또는 최상위 메뉴 항목을 사용 하지 않도록 설정 하면 메뉴에 포함 된 모든 메뉴 항목이 숨겨지고 비활성화 되지는 않습니다. 마찬가지로 하위 메뉴 항목이 있는 메뉴 항목을 사용 하지 않도록 설정 하면 하위 메뉴 항목이 숨겨지고 비활성화 되지 않습니다. 지정 된 메뉴의 모든 명령을 사용자가 사용할 수 없는 경우에는 완전 한 사용자 인터페이스를 제공 하므로 전체 메뉴를 숨기 거 나 사용 하지 않도록 설정 하는 것이 좋은 프로그래밍 습관 이라고 간주 됩니다. 메뉴를 숨기 거 나 사용 하지 않도록 설정 하 고 메뉴의 모든 항목 및 하위 메뉴 항목을 사용 하지 않도록 설정 해야 합니다. 숨기기만 하면 바로 가기 키를 통해 메뉴 명령에 액세스할 수 있습니다. 최상위 메뉴 항목의 `false` 속성을로설정하여전체메뉴를숨깁니다.<xref:System.Windows.Forms.ToolStripItem.Visible%2A>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [방법: ToolStripMenuItems 숨기기](how-to-hide-toolstripmenuitems.md)
- [MenuStrip 컨트롤 개요](menustrip-control-overview-windows-forms.md)
