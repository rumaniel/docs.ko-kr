---
title: '방법: 디자이너를 사용하여 TreeNode에 바로 가기 메뉴 연결'
ms.date: 03/30/2017
helpviewer_keywords:
- shortcut menus [Windows Forms], attaching to TreeNodes
- TreeNode [Windows Forms], attaching a shortcut menu using Designer
ms.assetid: 8e45e184-1313-4f8f-90ff-2cd5789b2268
ms.openlocfilehash: eb3240d35309e03aa8ce949b9c5000f8581d2c2f
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040455"
---
# <a name="how-to-attach-a-shortcut-menu-to-a-treenode-using-the-designer"></a>방법: 디자이너를 사용하여 TreeNode에 바로 가기 메뉴 연결
Windows Forms <xref:System.Windows.Forms.TreeView> 컨트롤은 windows 운영 체제에서 windows 탐색기 기능의 왼쪽 창에 표시 된 파일 및 폴더와 비슷한 노드 계층 구조를 표시 합니다. <xref:System.Windows.Forms.Control.ContextMenuStrip%2A> 속성을 설정 하 여 사용자가 <xref:System.Windows.Forms.TreeView> 컨트롤을 마우스 오른쪽 단추로 클릭 하면 상황에 맞는 작업을 사용자에 게 제공할 수 있습니다. <xref:System.Windows.Forms.ContextMenuStrip> 구성 요소를 개별 <xref:System.Windows.Forms.TreeNode> 항목과 연결 하면 <xref:System.Windows.Forms.TreeView> 컨트롤에 사용자 지정 수준의 바로 가기 메뉴 기능을 추가할 수 있습니다.

## <a name="to-associate-a-shortcut-menu-with-a-treenode-at-design-time"></a>디자인 타임에 바로 가기 메뉴를 TreeNode와 연결 하려면

1. 폼에 <xref:System.Windows.Forms.TreeView> 컨트롤을 추가한 다음 필요에 따라에 노드를 추가 합니다. <xref:System.Windows.Forms.TreeView> 자세한 내용은 [방법: Windows Forms TreeView 컨트롤](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)을 사용 하 여 노드를 추가 및 제거 합니다.

2. 폼에 <xref:System.Windows.Forms.ContextMenuStrip> 구성 요소를 추가한 다음 런타임에 사용할 수 있도록 설정할 노드 수준 작업을 나타내는 바로 가기 메뉴에 메뉴 항목을 추가 합니다. 자세한 내용은 [방법: ContextMenuStrip](how-to-add-menu-items-to-a-contextmenustrip.md)에 메뉴 항목을 추가 합니다.

3. 컨트롤에 대 한 <xref:System.Windows.Forms.ContextMenuStrip> <xref:System.Windows.Forms.TreeView> TreeNodeEditor 대화 상자를 다시 열고 편집할 노드를 선택 하 고 해당 속성을 추가한 바로 가기 메뉴로 설정 합니다.

4. 이 속성이 설정 되 면 노드를 마우스 오른쪽 단추로 클릭 하면 바로 가기 메뉴가 표시 됩니다.

     또한 이러한 메뉴 항목에 대 한 이벤트를 처리 하 <xref:System.Windows.Forms.ToolStripItem.Click> 는 코드를 작성 하려고 합니다.

## <a name="see-also"></a>참고자료

- [TreeView 컨트롤](treeview-control-windows-forms.md)
- [TreeView 컨트롤 개요](treeview-control-overview-windows-forms.md)
- [ContextMenuStrip 컨트롤](contextmenustrip-control.md)
