---
title: TreeView 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- TreeView
helpviewer_keywords:
- TreeView control [Windows Forms], about TreeView control
ms.assetid: 0ece823a-9508-478a-bbdb-7d7c3bae51d5
ms.openlocfilehash: b2722d21521fd9e59d911fb3b9cd177ec60c9903
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640856"
---
# <a name="treeview-control-overview-windows-forms"></a>TreeView 컨트롤 개요(Windows Forms)

Windows Forms <xref:System.Windows.Forms.TreeView> 컨트롤을 통해 Windows 운영 체제에서 Windows 탐색기 기능의 왼쪽 창에 파일 및 폴더가 표시되는 방식과 같은 노드 계층 구조를 사용자에게 표시할 수 있습니다. 트리 보기에서 각 노드 라는 다른 노드가 포함 될 수 있습니다 *자식 노드*합니다. 부모 노드, 즉 자식 노드를 포함하는 노드를 확장 또는 축소된 상태로 표시할 수 있습니다. 트리 뷰의 <xref:System.Windows.Forms.TreeView.CheckBoxes%2A> 속성을 `true`로 설정하여 노드 옆에 확인란이 있는 트리 뷰를 표시할 수도 있습니다. 그런 다음 노드의 <xref:System.Windows.Forms.TreeNode.Checked%2A> 속성을 `true` 또는 `false`로 설정하여 프로그래밍 방식으로 노드를 선택하거나 선택 취소할 수 있습니다.

## <a name="key-properties"></a>키 속성

<xref:System.Windows.Forms.TreeView> 컨트롤의 키 속성은 <xref:System.Windows.Forms.TreeView.Nodes%2A> 및 <xref:System.Windows.Forms.TreeView.SelectedNode%2A>입니다. <xref:System.Windows.Forms.TreeView.Nodes%2A> 속성에는 트리 뷰의 최상위 노드 목록이 포함됩니다. <xref:System.Windows.Forms.TreeView.SelectedNode%2A> 속성은 현재 선택된 노드를 설정합니다. 노드 옆에 아이콘을 표시할 수 있습니다. 컨트롤은 트리 뷰의 <xref:System.Windows.Forms.TreeView.ImageList%2A> 속성에 명명된 <xref:System.Windows.Forms.ImageList>의 이미지를 사용합니다. <xref:System.Windows.Forms.TreeView.ImageIndex%2A> 속성은 트리 뷰의 노드에 대한 기본 이미지를 설정합니다. 이미지를 표시 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: Windows Forms TreeView 컨트롤에 대 한 아이콘 설정](how-to-set-icons-for-the-windows-forms-treeview-control.md)합니다. Visual Studio 2005를 사용 하는 경우 액세스에 사용할 수 있는 표준 이미지의 대규모 라이브러리에는 <xref:System.Windows.Forms.TreeView> 제어 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TreeView>
- [TreeView 컨트롤](treeview-control-windows-forms.md)
- [방법: Windows Forms TreeView 컨트롤의 아이콘 설정](how-to-set-icons-for-the-windows-forms-treeview-control.md)
- [방법: 추가 하 고 Windows Forms TreeView 컨트롤을 사용 하 여 노드를 제거 합니다.](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [방법: Windows Forms TreeView 컨트롤의 노드 전체 반복](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [방법: 클릭 한 TreeView 노드 확인](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [방법: TreeView 또는 ListView 컨트롤 (Windows Forms)에 사용자 지정 정보 추가](add-custom-information-to-a-treeview-or-listview-control-wf.md)
