---
title: '방법: ToolStripMenuItems에 향상된 기능 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- commands [Windows Forms], grouping on menus
- check marks [Windows Forms], adding to menus
- ToolStripMenuItems [Windows Forms], displaying access keys
- menus [Windows Forms], grouping commands
- menu items [Windows Forms], displaying shortcut keys
- ToolStripMenuItems
- separators [Windows Forms], displaying on menus
- menu items [Windows Forms], showing separators
- menu items [Windows Forms], adding check marks
- ToolStripMenuItems [Windows Forms], adding check marks
- menu items [Windows Forms], adding images
- ToolStripSeparators [Windows Forms], displaying on MenuStrips
- menu items [Windows Forms], displaying access keys
- ToolStripMenuItems [Windows Forms], displaying shortcut keys
- ToolStripMenuItems [Windows Forms], adding images
- keyboard shortcuts [Windows Forms], displaying on menus
- images [Windows Forms], adding to menus
- ToolStripMenuItems [Windows Forms], showing separator bars
ms.assetid: aa5f19bb-b545-4378-bfa6-36ba592f0d7c
ms.openlocfilehash: 9e95c3623bf9bad8395f586392a0557ad1cde880
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912578"
---
# <a name="how-to-add-enhancements-to-toolstripmenuitems"></a>방법: ToolStripMenuItems에 향상된 기능 추가
다음과 같은 방법으로 및 <xref:System.Windows.Forms.MenuStrip> <xref:System.Windows.Forms.ContextMenuStrip> 컨트롤의 유용성을 향상 시킬 수 있습니다.  
  
- 선택 표시를 추가 하 여 기능이 설정 되었는지 여부를 지정 합니다. 예를 들어, 워드 프로세싱 응용 프로그램의 여백에 눈금자가 표시 되는지 여부와 같은 **창** 메뉴에 표시 되는 파일 목록에서 파일을 표시할지 여부를 지정 합니다.  
  
- 시각적으로 표시 되는 메뉴 명령을 표시 하는 이미지를 추가 합니다.  
  
- 바로 가기 키를 표시 하 여 명령을 수행할 때 마우스에 대 한 키보드 대체를 제공 합니다. 예를 들어 CTRL + C를 누르면 **Copy** 명령이 수행 됩니다.  
  
- 메뉴 탐색에 마우스에 대 한 키보드 대체를 제공 하는 액세스 키를 표시 합니다. 예를 들어 ALT + F를 누르면 **파일** 메뉴가 선택 됩니다.  
  
- 구분 기호를 표시 하 여 관련 명령을 그룹화 하 고 메뉴를 더 읽기 쉽게 만듭니다.  
  
### <a name="to-display-a-check-mark-on-a-menu-command"></a>메뉴 명령에 확인 표시를 표시 하려면  
  
- 해당 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 속성을로 `true`설정 합니다.  
  
     또한 <xref:System.Windows.Forms.ToolStripMenuItem.CheckState%2A> 속성을로 `true`설정 합니다. 이 절차는 선택 여부에 관계 없이 메뉴 명령을 기본적으로 선택 된 것으로 표시 하려는 경우에만 사용 합니다.  
  
### <a name="to-display-a-check-mark-that-changes-state-with-each-click"></a>각 클릭의 상태를 변경 하는 확인 표시를 표시 하려면  
  
- 메뉴 명령의 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> 속성을로 `true`설정 합니다.  
  
### <a name="to-add-an-image-to-a-menu-command"></a>메뉴 명령에 이미지를 추가 하려면  
  
- 메뉴 명령의 <xref:System.Windows.Forms.ToolStripItem.Image%2A> 속성을 이미지 이름으로 설정 합니다. 이 메뉴 명령의 <xref:System.Windows.Forms.ToolStripItemDisplayStyle.None> <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text> <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 속성을 또는로 설정 하면 이미지를 표시할 수 없습니다.  
  
> [!NOTE]
> 이미지 여백은 선택 하는 경우 확인 표시를 표시할 수도 있습니다. 또한 이미지의 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 속성을로 `true`설정할 수 있으며, 이미지는 런타임에 빗금 테두리와 함께 표시 됩니다.  
  
### <a name="to-display-a-shortcut-key-for-a-menu-command"></a>메뉴 명령에 대 한 바로 가기 키를 표시 하려면  
  
- 메뉴 명령의 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A> 속성을 **열기** 메뉴 명령에 대 한 CTRL + O와 같이 원하는 키보드 조합으로 설정 하 고 <xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A> 속성을로 `true`설정 합니다.  
  
### <a name="to-display-custom-shortcut-keys-for-a-menu-command"></a>메뉴 명령에 대 한 사용자 지정 바로 가기 키를 표시 하려면  
  
- 메뉴 명령의 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A> 속성을 shift + ctrl + o 대신 CTRL + shift + o와 같이 원하는 키보드 조합으로 설정 하 고 <xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A> 속성을로 `true`설정 합니다.  
  
### <a name="to-display-an-access-key-for-a-menu-command"></a>메뉴 명령에 대 한 선택 키를 표시 하려면  
  
- 메뉴 명령에 대 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 한 속성을 설정할 때 선택 키로 밑줄이 표시 될 문자 앞에 앰퍼샌드 (&)를 입력 합니다. 예를 들어를 `&Open` 메뉴 항목 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 의 속성으로 입력 하면 메뉴 명령이 <u>O</u>펜으로 표시 됩니다.
  
     이 메뉴 명령으로 이동 하려면 ALT 키를 눌러에 포커스 <xref:System.Windows.Forms.MenuStrip>를 이동 하 고 메뉴 이름의 선택 키를 누릅니다. 메뉴가 열리고 액세스 키가 포함 된 항목이 표시 되 면 액세스 키를 눌러 메뉴 명령을 선택 하기만 하면 됩니다.  
  
> [!NOTE]
> 동일한 메뉴 시스템에서 ALT + F를 두 번 정의 하는 것과 같이 중복 된 액세스 키를 정의 하지 마십시오. 중복 된 액세스 키의 선택 순서는 보장할 수 없습니다.  
  
### <a name="to-display-a-separator-bar-between-menu-commands"></a>메뉴 명령 사이에 구분 기호를 표시 하려면  
  
- <xref:System.Windows.Forms.MenuStrip> 및 여기에 포함 될 항목을 정의한 후에는 <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> 또는 <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> 메서드를 사용 하 여 메뉴 명령과 <xref:System.Windows.Forms.ToolStripSeparator> 컨트롤 <xref:System.Windows.Forms.MenuStrip> 을 원하는 순서 대로에 추가 합니다.  
  
    ```vb  
    ' This code adds a top-level File menu to the MenuStrip.  
    Me.menuStrip1.Items.Add(New ToolStripMenuItem() _  
    {Me.fileToolStripMenuItem})  
  
    ' This code adds the New and Open menu commands, a separator bar,   
    ' and the Save and Exit menu commands to the top-level File menu,   
    ' in that order.  
    Me.fileToolStripMenuItem.DropDownItems.AddRange(New _  
    ToolStripMenuItem() {Me.newToolStripMenuItem, _  
    Me.openToolStripMenuItem, Me.toolStripSeparator1, _  
    Me.saveToolStripMenuItem, Me.exitToolStripMenuItem})  
    ```  
  
    ```csharp  
    // This code adds a top-level File menu to the MenuStrip.  
    this.menuStrip1.Items.Add(new ToolStripItem[]_  
    {this.fileToolStripMenuItem});  
  
    // This code adds the New and Open menu commands, a separator bar,   
    // and the Save and Exit menu commands to the top-level File menu,   
    // in that order.  
    this.fileToolStripMenuItem.DropDownItems.AddRange(new _  
    ToolStripItem[] {  
    this.newToolStripMenuItem,  
    this.openToolStripMenuItem,  
    this.toolStripSeparator1,  
    this.saveToolStripMenuItem,  
    this.exitToolStripMenuItem});  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip 컨트롤 개요](menustrip-control-overview-windows-forms.md)
