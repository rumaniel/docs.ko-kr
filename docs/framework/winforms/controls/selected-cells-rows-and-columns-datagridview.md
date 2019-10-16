---
title: '방법: Windows Forms DataGridView 컨트롤에서 선택한 셀, 행 및 열 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- selection [Windows Forms], DataGridView control [Windows Forms]
- DataGridView control [Windows Forms], getting selection
- getting selection [Windows Forms], DataGridView control [Windows Forms]
ms.assetid: d93c4b5b-498e-49bc-982a-2229d61778e4
ms.openlocfilehash: 25b3ed50081add77b9f522ca8e597f2b3306cb2e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960522"
---
# <a name="how-to-get-the-selected-cells-rows-and-columns-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 선택한 셀, 행 및 열 가져오기
해당 <xref:System.Windows.Forms.DataGridView> 하는 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>속성인, <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>및 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>를 사용 하 여 컨트롤에서 선택한 셀, 행 또는 열을 가져올 수 있습니다. 다음 절차에서는 선택한 셀을 가져오고 행 및 열 인덱스를 <xref:System.Windows.Forms.MessageBox>에 표시 합니다.  
  
### <a name="to-get-the-selected-cells-in-a-datagridview-control"></a>DataGridView 컨트롤에서 선택한 셀을 가져오려면  
  
- <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 속성을 사용합니다.  
  
    > [!NOTE]
    > 잠재적으로 많은 수의 셀이 표시 되지 않도록 하려면 메서드를사용합니다.<xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#10)]  
  
### <a name="to-get-the-selected-rows-in-a-datagridview-control"></a>DataGridView 컨트롤에서 선택 된 행을 가져오려면  
  
- <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 속성을 사용합니다. 사용자가 행을 선택할 수 있도록 하려면 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 속성을 또는 <xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>로 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> 설정 해야 합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#20)]  
  
### <a name="to-get-the-selected-columns-in-a-datagridview-control"></a>DataGridView 컨트롤에서 선택한 열을 가져오려면  
  
- <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 속성을 사용합니다. 사용자가 열을 선택할 수 있도록 하려면 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 속성을 또는 <xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>로 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect> 설정 해야 합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#30)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- <xref:System.Windows.Forms.Button>각각 연결 `selectedCellsButton`된 `selectedRowsButton` <xref:System.Windows.Forms.Control.Click> 이벤트에 `selectedColumnsButton`대 한 처리기가 있는, 및 라는 컨트롤  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType>, <xref:System.Windows.Forms?displayProperty=nameWithType> 및 <xref:System.Text?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 이 항목에 설명 된 컬렉션은 많은 셀, 행 또는 열이 선택 된 경우 효율적으로 수행 되지 않습니다. 많은 양의 데이터에 이러한 컬렉션을 사용 하는 방법에 대 한 자세한 내용은 [Windows Forms DataGridView 컨트롤 크기 조정에 대 한 모범 사례](best-practices-for-scaling-the-windows-forms-datagridview-control.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>
- <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>
- <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>
- <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>
- <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>
- [Windows Forms DataGridView 컨트롤에서 선택 및 클립보드 사용](selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)
