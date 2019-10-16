---
title: '방법: Windows Forms TreeView 컨트롤을 사용하여 노드 추가 및 제거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- TreeView control [Windows Forms], removing nodes
- tree nodes in TreeView control
- TreeView control [Windows Forms], adding nodes
ms.assetid: de1b82db-4905-449a-9f59-af271a6b6673
ms.openlocfilehash: 4cbb5fbdb24790a7ddbce5c38060703c7ba7024a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59326894"
---
# <a name="how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control"></a>방법: Windows Forms TreeView 컨트롤을 사용하여 노드 추가 및 제거
Windows Forms <xref:System.Windows.Forms.TreeView> 컨트롤의 최상위 노드를 저장 합니다. 해당 <xref:System.Windows.Forms.TreeView.Nodes%2A> 컬렉션입니다. 각 <xref:System.Windows.Forms.TreeNode> 역시 자체 <xref:System.Windows.Forms.TreeNode.Nodes%2A> 해당 자식 노드를 저장 하는 컬렉션입니다. 두 컬렉션 속성은 <xref:System.Windows.Forms.TreeNodeCollection>를 추가할 수 있도록 하는 표준 컬렉션 멤버를 제거 및 단일 노드 계층 구조 수준에서 노드를 다시 정렬 제공 합니다.  
  
### <a name="to-add-nodes-programmatically"></a>프로그래밍 방식으로 노드를 추가 하려면  
  
1. 사용 된 <xref:System.Windows.Forms.TreeNodeCollection.Add%2A> 트리 뷰의 메서드의 <xref:System.Windows.Forms.TreeView.Nodes%2A> 속성입니다.  
  
    ```vb  
    ' Adds new node as a child node of the currently selected node.  
    Dim newNode As TreeNode = New TreeNode("Text for new node")  
    TreeView1.SelectedNode.Nodes.Add(newNode)  
    ```  
  
    ```csharp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode newNode = new TreeNode("Text for new node");  
    treeView1.SelectedNode.Nodes.Add(newNode);  
    ```  
  
    ```cpp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode ^ newNode = new TreeNode("Text for new node");  
    treeView1->SelectedNode->Nodes->Add(newNode);  
    ```  
  
### <a name="to-remove-nodes-programmatically"></a>프로그래밍 방식으로 노드를 제거 하려면  
  
1. 사용 된 <xref:System.Windows.Forms.TreeNodeCollection.Remove%2A> 트리 뷰의 메서드의 <xref:System.Windows.Forms.TreeView.Nodes%2A> 단일 노드를 제거 하려면 속성 또는 <xref:System.Windows.Forms.TreeNodeCollection.Clear%2A> 모든 노드를 선택 취소 하는 방법.  
  
    ```vb  
    ' Removes currently selected node, or root if nothing is selected.  
    TreeView1.Nodes.Remove(TreeView1.SelectedNode)  
    ' Clears all nodes.  
    TreeView1.Nodes.Clear()  
    ```  
  
    ```csharp  
    // Removes currently selected node, or root if nothing   
    // is selected.  
    treeView1.Nodes.Remove(treeView1.SelectedNode);  
    // Clears all nodes.  
    TreeView1.Nodes.Clear();  
    ```  
  
    ```cpp  
    // Removes currently selected node, or root if nothing  
    // is selected.  
    treeView1->Nodes->Remove(treeView1->SelectedNode);  
    // Clears all nodes.  
    treeView1->Nodes->Clear();  
    ```  
  
## <a name="see-also"></a>참고자료

- [TreeView 컨트롤](treeview-control-windows-forms.md)
- [TreeView 컨트롤 개요](treeview-control-overview-windows-forms.md)
- [방법: Windows Forms TreeView 컨트롤의 아이콘 설정](how-to-set-icons-for-the-windows-forms-treeview-control.md)
- [방법: Windows Forms TreeView 컨트롤의 노드 전체 반복](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [방법: 클릭 한 TreeView 노드 확인](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [방법: TreeView 또는 ListView 컨트롤 (Windows Forms)에 사용자 지정 정보 추가](add-custom-information-to-a-treeview-or-listview-control-wf.md)
