---
title: '방법: Windows Forms DataGridView 컨트롤에서 열 고정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- columns [Windows Forms], freezing
- DataGridView control [Windows Forms], freezing columns
- DataGridView control [Windows Forms], columns always in view
ms.assetid: 2ef8b1de-782e-4867-af8d-58171ab5c106
ms.openlocfilehash: a83c5078d67be40fda2ae3382b8124594ee78103
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966655"
---
# <a name="how-to-freeze-columns-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 열 고정
사용자가 Windows Forms <xref:System.Windows.Forms.DataGridView> 컨트롤에 표시된 데이터를 볼 때 단일 열이나 열 집합을 자주 참조해야 하는 경우가 있습니다. 예를 들어 많은 열이 포함된 고객 정보 테이블을 표시하는 경우 다른 열을 표시되는 영역 바깥으로 스크롤할 수 있게 하면서 고객 이름은 항상 표시하는 것이 유용합니다.  
  
 이 동작을 얻기 위해 컨트롤에서 열을 고정할 수 있습니다. 열을 고정하는 경우 왼쪽(또는 오른쪽에서 왼쪽 언어 스크립트의 경우 오른쪽)에 있는 모든 열도 고정됩니다. 다른 모든 열을 스크롤할 수 있는 동안 고정된 열은 그대로 유지됩니다.  
  
> [!NOTE]
> 열 다시 정렬을 사용하는 경우 고정된 열은 고정되지 않은 열과 별개인 그룹으로 처리됩니다. 사용자는 각 그룹에서 열의 위치를 변경할 수 있지만 그룹 간에 열을 이동할 수는 없습니다.  
  
 열의 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A> 속성은 표에서 열이 항상 표시되는지 여부를 결정합니다.  
  
 Visual Studio에서는 이 작업이 지원됩니다.  자세한 내용은 [다음을 참조 하세요. 디자이너](freeze-columns-in-the-datagrid-using-the-designer.md)를 사용 하 여 Windows Forms DataGridView 컨트롤의 열을 고정 합니다.  
  
### <a name="to-freeze-a-column-programmatically"></a>프로그래밍 방식으로 열을 고정하려면  
  
- <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=nameWithType> 속성을 `true`으로 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#061](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#061)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#061](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#061)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- 이름이 `AddToCartButton`인 열을 포함하는 이름이 `dataGridView1`인 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView>
- [Windows Forms DataGridView 컨트롤의 기본 열, 행 및 셀 기능](basic-column-row-and-cell-features-wf-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 열 다시 정렬 사용](how-to-enable-column-reordering-in-the-windows-forms-datagridview-control.md)
