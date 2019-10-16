---
title: '방법: Windows Forms DataGridView 컨트롤에서 열 정렬 모드 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sorting [Windows Forms], data grids
- DataGridView control [Windows Forms], sort mode
- data grids [Windows Forms], sorting data
ms.assetid: 57dfed60-a608-40d5-86f9-d65686ffb325
ms.openlocfilehash: fd627e3aaed7330a05c46b9e2ca0a213404e0bfe
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625742"
---
# <a name="how-to-set-the-sort-modes-for-columns-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 열 정렬 모드 설정
에 <xref:System.Windows.Forms.DataGridView> 컨트롤, 텍스트 상자 열에서는 다른 열 유형에 자동으로 정렬 되어 있지 않으면 하는 동안 기본적으로 자동 정렬 합니다. 이러한 기본값을 재정의할 수도 있습니다. 예를 들어, 텍스트, 숫자 또는 열거형 셀 값 대신 이미지를 표시할 수 있습니다. 이미지를 정렬할 수 없습니다, 하는 동안에 나타내는 내부 값을 정렬할 수 있습니다.  
  
 에 <xref:System.Windows.Forms.DataGridView> 컨트롤을는 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 열 속성 값의 정렬 동작을 결정 합니다.  
  
 에서는 다음 절차는 `Priority` 열에서 [방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 사용자 지정](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)합니다. 이 열은 이미지 열 이므로 기본적으로 정렬 될 수 없습니다. 그러나 자동으로 정렬할 수 있도록 문자열을 되는 실제 셀 값을 포함 합니다.  
  
### <a name="to-set-the-sort-mode-for-a-column"></a>열 정렬 모드를 설정 하려면  
  
- <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType> 속성을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#066](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#066)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#066](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#066)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- 이름이 `Priority`인 열을 포함하는 이름이 `dataGridView1`인 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 데이터 정렬](sorting-data-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 열 정렬 모드](column-sort-modes-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 정렬 사용자 지정](how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)
