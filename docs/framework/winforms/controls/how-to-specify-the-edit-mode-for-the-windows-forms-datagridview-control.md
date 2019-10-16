---
title: '방법: Windows Forms DataGridView 컨트롤에 대한 편집 모드 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], edit mode
- data grids [Windows Forms], edit mode
ms.assetid: 93e117e8-94c4-411b-ba31-645e475ed85c
ms.openlocfilehash: a999582aeb629646fa1843f973b10a039c29e1a3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64630530"
---
# <a name="how-to-specify-the-edit-mode-for-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에 대한 편집 모드 지정
기본적으로 사용자의 현재 내용을 편집할 수 있습니다 <xref:System.Windows.Forms.DataGridView> 에 입력 하거나 F2 키를 눌러 텍스트 상자 셀입니다. 그러면 셀 편집 모드에서 다음 조건이 모두 충족 될 경우:  
  
- 데이터 원본 편집을 지원 합니다.  
  
- <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용할 수 있습니다.  
  
- 합니다 <xref:System.Windows.Forms.DataGridView.EditMode%2A> 속성 값이 <xref:System.Windows.Forms.DataGridViewEditMode.EditProgrammatically>합니다.  
  
- 합니다 `ReadOnly` 셀, 행, 열 및 컨트롤의 속성은 모두 설정 됩니다. `false`합니다.  
  
 편집 모드에 사용자는 셀 값을 변경 하 고 enter 키를 눌러 변경 내용을 커밋하거나 ESC 원래 값에 있는 셀을 되돌릴 수 있습니다.  
  
 구성할 수는 <xref:System.Windows.Forms.DataGridView> 이 현재 셀으로 셀이 편집 모드로 전환 되도록 합니다. 이 경우 ENTER 및 ESC 키의 동작이 변경 되지 않습니다 하지만 값 커밋하거나 되돌려야 하면 셀이 편집 모드로 유지 됩니다. 셀 사용자 셀 또는 사용자 F2 키를 입력 하는 경우에 편집 모드로 전환 되도록 컨트롤을 구성할 수도 있습니다. 마지막으로 호출 하는 경우를 제외 하 고 편집 모드가에서 셀을 방지할 수 있습니다는 <xref:System.Windows.Forms.DataGridView.BeginEdit%2A> 메서드.  
  
### <a name="to-change-the-edit-mode-of-a-datagridview-control"></a>DataGridView 컨트롤의 편집 모드를 변경 하려면  
  
- 설정 된 <xref:System.Windows.Forms.DataGridView.EditMode%2A?displayProperty=nameWithType> 속성을 적절 한 <xref:System.Windows.Forms.DataGridViewEditMode> 열거형입니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#067](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#067)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#067](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#067)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System> 및 <xref:System.Windows.Forms> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.EditMode%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 데이터 입력](data-entry-in-the-windows-forms-datagridview-control.md)
