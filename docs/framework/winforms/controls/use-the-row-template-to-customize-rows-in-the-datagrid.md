---
title: '방법: 행 템플릿을 사용하여 Windows Forms DataGridView 컨트롤에서 행 사용자 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data grids [Windows Forms], customizing rows
- DataGridView control [Windows Forms], customizing rows
ms.assetid: 6db61607-7e57-4a84-8d63-9d6a7ed7f9ff
ms.openlocfilehash: 0dba318e6aa35761f4e9471fdb13b65644747b57
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966498"
---
# <a name="how-to-use-the-row-template-to-customize-rows-in-the-windows-forms-datagridview-control"></a>방법: 행 템플릿을 사용하여 Windows Forms DataGridView 컨트롤에서 행 사용자 지정
컨트롤 <xref:System.Windows.Forms.DataGridView> 은 데이터 바인딩을 통해 또는 사용할 기존 행을 지정 하지 않고 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A?displayProperty=nameWithType> 메서드를 호출 하는 경우 컨트롤에 추가 되는 모든 행의 기준으로 행 템플릿을 사용 합니다.  
  
 행 템플릿을 사용 하면 속성이 제공 하 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> 는 것 보다 행의 모양과 동작을 보다 효율적으로 제어할 수 있습니다. 행 템플릿을 사용 하면를 포함 <xref:System.Windows.Forms.DataGridViewRow> <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A>하 여 모든 속성을 설정할 수 있습니다.  
  
 특정 효과를 얻기 위해 행 템플릿을 사용 해야 하는 경우도 있습니다. 예를 들어 행 높이 정보를에 저장할 <xref:System.Windows.Forms.DataGridViewCellStyle>수 없기 때문에 모든 행에 사용 되는 기본 높이를 변경 하려면 행 템플릿을 사용 해야 합니다. 행 템플릿은에서 <xref:System.Windows.Forms.DataGridViewRow> 파생 된 고유한 클래스를 만들고 새 행이 컨트롤에 추가 될 때 사용자 지정 형식을 사용 하려는 경우에도 유용 합니다.  
  
> [!NOTE]
> 행을 추가 하는 경우에만 행 템플릿이 사용 됩니다. 행 템플릿을 변경 하 여 기존 행을 변경할 수 없습니다.  
  
### <a name="to-use-the-row-template"></a>행 템플릿을 사용 하려면  
  
- <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=nameWithType> 속성에서 검색 된 개체에 대 한 속성을 설정 합니다.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.RowTemplate#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/CPP/datagridviewrowtemplate.cpp#1)]
     [!code-csharp[System.Windows.Forms.DataGridView.RowTemplate#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/CS/datagridviewrowtemplate.cs#1)]
     [!code-vb[System.Windows.Forms.DataGridView.RowTemplate#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/VB/datagridviewrowtemplate.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Windows.Forms.DataGridViewRow>
- <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
