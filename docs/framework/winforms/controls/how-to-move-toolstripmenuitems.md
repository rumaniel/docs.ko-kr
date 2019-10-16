---
title: '방법: ToolStripMenuItems 이동'
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], moving
- menus [Windows Forms], arranging items
- ToolStripMenuItems [Windows Forms], dragging and dropping
- menu items [Windows Forms], moving
- menu items [Windows Forms], cutting and pasting
- menu items [Windows Forms], dragging and dropping
- MenuStrip control [Windows Forms], arranging items
- ToolStripMenuItems [Windows Forms], cutting and pasting
ms.assetid: cab9e03e-4edd-4c25-b3e3-bd1edc602bd9
ms.openlocfilehash: adf25973fde790937461007bd0106cca02dd83be
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039805"
---
# <a name="how-to-move-toolstripmenuitems"></a>방법: ToolStripMenuItems 이동
디자인 타임에 전체 최상위 메뉴와 해당 메뉴 항목을의 다른 위치로 <xref:System.Windows.Forms.MenuStrip>이동할 수 있습니다. 최상위 메뉴 간에 개별 메뉴 항목을 이동 하거나 메뉴 내에서 메뉴 항목의 위치를 변경할 수도 있습니다.

## <a name="to-move-a-top-level-menu-and-its-menu-items-to-another-top-level-location"></a>최상위 메뉴와 해당 메뉴 항목을 다른 최상위 위치로 이동 하려면

1. 이동 하려는 메뉴에서 마우스 왼쪽 단추를 클릭 하 여 누르고 있습니다.

2. 원하는 새 위치 앞에 있는 최상위 메뉴로 삽입 지점을 끌고 왼쪽 마우스 단추를 놓습니다.

     선택한 메뉴가 삽입 지점의 오른쪽으로 이동 합니다.

## <a name="to-move-a-top-level-menu-and-its-menu-items-to-a-drop-down-location"></a>최상위 메뉴와 해당 메뉴 항목을 드롭다운 위치로 이동 하려면

1. 이동 하려는 메뉴를 마우스 왼쪽 단추로 클릭 하 고 CTRL + X를 누르거나, 메뉴를 마우스 오른쪽 단추로 클릭 하 고 바로 가기 메뉴에서 **잘라내기** 를 선택 합니다.

2. 대상 최상위 메뉴에서 원하는 새 위치 위의 메뉴 항목을 마우스 왼쪽 단추로 클릭 하 고 CTRL + V를 누르거나, 원하는 새 위치 위에 있는 메뉴 항목을 마우스 오른쪽 단추로 클릭 하 고 바로 가기 메뉴에서 **붙여넣기** 를 선택 합니다.

     선택한 메뉴 항목 뒤에 잘린 메뉴가 삽입 됩니다.

## <a name="to-move-a-menu-item-within-a-menu-using-the-items-collection-editor"></a>항목 컬렉션 편집기를 사용 하 여 메뉴에서 메뉴 항목을 이동 하려면

1. 이동 하려는 메뉴 항목이 포함 된 메뉴를 마우스 오른쪽 단추로 클릭 합니다.

2. 바로 가기 메뉴에서 **DropDownItems 편집**을 선택 합니다.

3. **항목 컬렉션 편집기**에서 이동할 메뉴 항목을 마우스 왼쪽 단추를 클릭 합니다.

4. 위쪽 및 아래쪽 화살표 키를 클릭 하 여 메뉴에서 메뉴 항목을 이동 합니다.

5. **확인**을 클릭합니다.

## <a name="to-move-a-menu-item-within-a-menu-using-the-keyboard"></a>키보드를 사용 하 여 메뉴에서 메뉴 항목을 이동 하려면

1. ALT 키를 누르고 있습니다.

2. 이동 하려는 메뉴 항목의 왼쪽 마우스 단추를 클릭 하 여 유지 합니다.

3. 메뉴 항목을 새 위치로 끌고 왼쪽 마우스 단추를 놓습니다.

## <a name="to-move-a-menu-item-to-another-menu"></a>메뉴 항목을 다른 메뉴로 이동 하려면

1. 이동 하려는 메뉴 항목을 마우스 왼쪽 단추로 클릭 하 고 CTRL + X를 누르거나, 메뉴 항목을 마우스 오른쪽 단추로 클릭 하 고 바로 가기 메뉴에서 **잘라내기** 를 선택 합니다.

2. 잘린 메뉴 항목이 포함 될 메뉴를 마우스 왼쪽 단추를 클릭 합니다.

3. 원하는 새 위치 앞에 있는 메뉴 항목을 마우스 왼쪽 단추로 클릭 하 고 CTRL + V를 누르거나, 원하는 새 위치 앞에 있는 메뉴 항목을 마우스 오른쪽 단추로 클릭 하 고 바로 가기 메뉴에서 **붙여넣기** 를 선택 합니다.

     잘린 메뉴 항목이 선택한 메뉴 항목 뒤에 삽입 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip 컨트롤 개요](menustrip-control-overview-windows-forms.md)
