---
title: '방법: Windows Forms TreeView 컨트롤에 대한 아이콘 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- TreeView control [Windows Forms], node icons
- ImageList component [Windows Forms], adding images
- icons [Windows Forms], setting for TreeView control
- tree nodes in TreeView control [Windows Forms], icons
ms.assetid: c14ddcc0-e5a6-4c21-a2d5-6799fd491781
ms.openlocfilehash: 451f9ab2b35ad1fbbe9401dacbc8aab44e302701
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69909804"
---
# <a name="how-to-set-icons-for-the-windows-forms-treeview-control"></a>방법: Windows Forms TreeView 컨트롤에 대한 아이콘 설정
Windows Forms <xref:System.Windows.Forms.TreeView> 컨트롤은 각 노드 옆에 아이콘을 표시할 수 있습니다. 아이콘은 노드 텍스트의 바로 왼쪽에 배치 됩니다. 이러한 아이콘을 표시 하려면 <xref:System.Windows.Forms.ImageList> 컨트롤에 트리 뷰를 연결 해야 합니다. 이미지 목록에 대 한 자세한 내용은 [ImageList 구성 요소](imagelist-component-windows-forms.md) 및 [방법: Windows Forms ImageList 구성 요소](how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)를 사용 하 여 이미지를 추가 하거나 제거 합니다.  
  
> [!NOTE]
> Microsoft .NET Framework 버전 1.1의 버그는 응용 프로그램에서를 호출할 <xref:System.Windows.Forms.TreeView> <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType>때 이미지가 노드에 나타나지 않도록 합니다. 이 버그를 해결 하려면를 호출한 <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=nameWithType> <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>직후에 `Main` 메서드를 호출 합니다. 이 버그는 .NET Framework 2.0에서 수정 되었습니다.  
  
### <a name="to-display-images-in-a-tree-view"></a>트리 뷰에서 이미지를 표시 하려면  
  
1. 컨트롤의 <xref:System.Windows.Forms.TreeView.ImageList%2A> 속성을 사용 하려는 기존 <xref:System.Windows.Forms.ImageList> 컨트롤로 설정 합니다. <xref:System.Windows.Forms.TreeView>  
  
     이러한 속성은 디자이너에서 속성 창 또는 코드를 사용 하 여 설정할 수 있습니다.  
  
    ```vb  
    TreeView1.ImageList = ImageList1  
    ```  
  
    ```csharp  
    treeView1.ImageList = imageList1;  
    ```  
  
    ```cpp  
    treeView1->ImageList = imageList1;  
    ```  
  
2. 노드의 <xref:System.Windows.Forms.TreeNode.ImageIndex%2A> 및<xref:System.Windows.Forms.TreeNode.SelectedImageIndex%2A> 속성을 설정 합니다. 속성 <xref:System.Windows.Forms.TreeNode.ImageIndex%2A> 은 노드의 표준 및 확장 된 상태에 대해 표시 되는 이미지를 결정 하 <xref:System.Windows.Forms.TreeNode.SelectedImageIndex%2A> 고, 속성은 노드의 선택 된 상태에 대해 표시 되는 이미지를 결정 합니다.  
  
     이러한 속성은 코드 또는 TreeNode 편집기 내에서 설정할 수 있습니다. TreeNode 편집기를 열려면 속성 창의 ![ <xref:System.Windows.Forms.TreeView.Nodes%2A> 속성 옆에 있는 줄임표 단추 (Visual](./media/visual-studio-ellipsis-button.png)Studio 속성 창의 줄임표 단추 (...)를 클릭 합니다.  
  
    ```vb  
    ' (Assumes that ImageList1 contains at least two images and  
    ' the TreeView control contains a selected image.)  
    TreeView1.SelectedNode.ImageIndex = 0  
    TreeView1.SelectedNode.SelectedImageIndex = 1  
    ```  
  
    ```csharp  
    // (Assumes that imageList1 contains at least two images and  
    // the TreeView control contains a selected image.)  
    treeView1.SelectedNode.ImageIndex = 0;  
    treeView1.SelectedNode.SelectedImageIndex = 1;  
    ```  
  
    ```cpp  
    // (Assumes that imageList1 contains at least two images and  
    // the TreeView control contains a selected image.)  
    treeView1->SelectedNode->ImageIndex = 0;  
    treeView1->SelectedNode->SelectedImageIndex = 1;  
    ```  
  
## <a name="see-also"></a>참고자료

- [TreeView 컨트롤 개요](treeview-control-overview-windows-forms.md)
- [방법: Windows Forms TreeView 컨트롤을 사용 하 여 노드 추가 및 제거](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [방법: Windows Forms TreeView 컨트롤의 모든 노드를 반복 합니다.](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [방법: 클릭 한 TreeView 노드 확인](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [방법: TreeView 또는 ListView 컨트롤에 사용자 지정 정보 추가 (Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
