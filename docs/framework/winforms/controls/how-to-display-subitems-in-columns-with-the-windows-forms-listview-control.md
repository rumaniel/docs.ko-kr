---
title: '방법: Windows Forms ListView 컨트롤을 사용하여 열에 하위 항목 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- list items
- Details view
- ListView control [Windows Forms], adding ListSubItems
- subitems
ms.assetid: e465f044-cde7-4fd9-a687-788a73a0f554
ms.openlocfilehash: 318521cc1377be89ef54706d80c8b2990a6ba1b8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61650468"
---
# <a name="how-to-display-subitems-in-columns-with-the-windows-forms-listview-control"></a>방법: Windows Forms ListView 컨트롤을 사용하여 열에 하위 항목 표시
Windows Forms <xref:System.Windows.Forms.ListView> 컨트롤 추가 텍스트 또는 세부 정보 뷰에서 각 항목에 대 한 하위 항목을 표시할 수 있습니다. 첫 번째 열에는 예를 들어 직원 번호 항목 텍스트를 표시합니다. 두 번째, 두 번째, 첫 번째, 세 번째 및 이후의 열에 표시 하 고 후속 관련 된 하위 항목입니다.  
  
### <a name="to-add-subitems-to-a-list-item"></a>목록 항목에 하위 항목을 추가 하려면  
  
1. 필요한 열을 추가 합니다. 첫 번째 열이 항목의 표시 되므로 <xref:System.Windows.Forms.ListView.Text%2A> 속성을 하나 이상의 열 하위 필요 합니다. 열을 추가 하는 방법은 참조 하세요. [방법: 열에는 Windows Forms ListView 컨트롤 추가](how-to-add-columns-to-the-windows-forms-listview-control.md)합니다.  
  
2. 호출을 <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection.Add%2A> 에서 반환 된 컬렉션의 메서드는 <xref:System.Windows.Forms.ListViewItem.SubItems%2A> 항목의 속성입니다. 아래 코드 예제에는 목록 항목에 대 한 부서와 직원 이름을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#61](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#61)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#61](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#61)]  
  
## <a name="see-also"></a>참고자료

- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 열 추가](how-to-add-columns-to-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 대 한 아이콘을 표시 합니다.](how-to-display-icons-for-the-windows-forms-listview-control.md)
- [방법: TreeView 또는 ListView 컨트롤 (Windows Forms)에 사용자 지정 정보 추가](add-custom-information-to-a-treeview-or-listview-control-wf.md)
