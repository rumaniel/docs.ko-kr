---
title: '방법: Windows Forms ContextMenu 구성 요소를 사용하여 메뉴 항목 추가 및 제거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- context menus [Windows Forms], removing items
- ContextMenu component [Windows Forms], adding items
- shortcut menus [Windows Forms], removing items
- shortcut menus [Windows Forms], examples
- context menus [Windows Forms], adding items
- shortcut menus [Windows Forms], adding items
- ContextMenu component [Windows Forms], removing items
- context menus [Windows Forms], examples
- examples [Windows Forms], context menus
ms.assetid: 426d1eaf-7fb8-4b0b-8a33-5e8721786ea4
ms.openlocfilehash: 5d1862b1fc1398f0f8c2217b51c4efb93db639af
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957028"
---
# <a name="how-to-add-and-remove-menu-items-with-the-windows-forms-contextmenu-component"></a>방법: Windows Forms ContextMenu 구성 요소를 사용하여 메뉴 항목 추가 및 제거
Windows Forms에서 바로 가기 메뉴 항목을 추가 하 고 제거 하는 방법을 설명 합니다.  
  
 Windows Forms <xref:System.Windows.Forms.ContextMenu> 구성 요소는 선택한 개체와 관련 된 자주 사용 되는 명령 메뉴를 제공 합니다. 컬렉션에 개체를 추가 <xref:System.Windows.Forms.MenuItem> 하 여 바로 가기 메뉴에 항목을 추가할 수 있습니다. <xref:System.Windows.Forms.Menu.MenuItems%2A>  
  
 바로 가기 메뉴에서 항목을 영구적으로 제거할 수 있습니다. 그러나 런타임에 항목을 숨기 거 나 사용 하지 않도록 설정 하는 것이 더 적합할 수 있습니다.  
  
> [!IMPORTANT]
> 및 <xref:System.Windows.Forms.MenuStrip> 는이전<xref:System.Windows.Forms.MainMenu> 버전 의및<xref:System.Windows.Forms.ContextMenu> 컨트롤에 기능을 추가 하 고 추가 하지만를 선택 하는 경우 이전 버전과의 호환성 및 향후 사용에 대해 모두 유지 됩니다.<xref:System.Windows.Forms.ContextMenu> <xref:System.Windows.Forms.MainMenu> <xref:System.Windows.Forms.ContextMenuStrip>  
  
### <a name="to-remove-items-from-a-shortcut-menu"></a>바로 가기 메뉴에서 항목을 제거 하려면  
  
1. 구성 요소 컬렉션<xref:System.Windows.Forms.Menu.MenuItems%2A> <xref:System.Windows.Forms.Menu.MenuItemCollection.RemoveAt%2A> 의 또는 메서드를 사용 하 여 특정 메뉴 항목을 제거 합니다. <xref:System.Windows.Forms.Menu.MenuItemCollection.Remove%2A> <xref:System.Windows.Forms.ContextMenu>  
  
    ```vb  
    ' Removes the first item in the shortcut menu.  
    ContextMenu1.MenuItems.RemoveAt(0)  
    ' Removes a particular object from the shortcut menu.  
    ContextMenu1.MenuItems.Remove(mnuItemNew)  
    ```  
  
    ```csharp  
    // Removes the first item in the shortcut menu.  
    contextMenu1.MenuItems.RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1.MenuItems.Remove(mnuItemNew);  
    ```  
  
    ```cpp  
    // Removes the first item in the shortcut menu.  
    contextMenu1->MenuItems->RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1->MenuItems->Remove(mnuItemNew);  
    ```  
  
     또는  
  
2. 구성 요소 `Clear` `MenuItems` 컬렉션의 메서드를 사용 하 여 메뉴에서 모든 항목을 제거 합니다. <xref:System.Windows.Forms.ContextMenu>  
  
    ```vb  
    ContextMenu1.MenuItems.Clear()  
    ```  
  
    ```csharp  
    contextMenu1.MenuItems.Clear();  
    ```  
  
    ```cpp  
    contextMenu1->MenuItems->Clear();  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ContextMenu>
- [ContextMenu 구성 요소](contextmenu-component-windows-forms.md)
- [ContextMenu 구성 요소 개요](contextmenu-component-overview-windows-forms.md)
