---
title: '방법: Windows Forms DataGridView 컨트롤에 대한 대체 행 스타일 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], row styles
- data grids [Windows Forms], row styles
- rows [Windows Forms], data grids
ms.assetid: 699ef759-458c-426d-ac87-7c7e71b018ae
ms.openlocfilehash: d113c45469f6a78c94b9489bd82f9e55b5b96bba
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962271"
---
# <a name="how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에 대한 대체 행 스타일 설정
대체로 테이블 형식 데이터는 교대로 반복되는 행의 배경색이 서로 다른 장부와 비슷한 형식으로 사용자에게 표시됩니다. 이 형식을 사용하면 특히 많은 열을 포함하는 넓은 테이블에서 사용자가 각 행에 있는 셀을 쉽게 구분할 수 있습니다.  
  
 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용하여 교대로 반복되는 행에 대한 전체 스타일 정보를 지정할 수 있습니다. 이 경우 배경색 외에도 전경색 및 글꼴과 같은 스타일 특성을 사용하여 교대로 반복되는 행을 구분할 수 있습니다.  
  
 Visual Studio에서는 이 작업이 지원됩니다.  자세한 내용은 [다음을 참조 하세요. 디자이너](set-alternating-row-styles-for-the-datagrid-using-the-designer.md)를 사용 하 여 Windows Forms DataGridView 컨트롤에 대해 교대로 반복 되는 행 스타일을 설정 합니다.  
  
### <a name="to-set-alternating-row-styles-programmatically"></a>프로그래밍 방식으로 교대로 반복되는 행 스타일을 설정하려면  
  
- <xref:System.Windows.Forms.DataGridView>의 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> 및 <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A> 속성에서 반환된 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체의 속성을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#068](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#068)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#068](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#068)]  
  
    > [!NOTE]
    > <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> 및 <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A> 속성을 사용하여 지정된 스타일은 열과 <xref:System.Windows.Forms.DataGridView> 수준에 지정된 스타일을 재정의하지만 개별 행 및 셀 수준에서 설정된 스타일에 의해 재정의됩니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 최대 확장성을 얻으려면 각 요소에 대한 스타일 속성을 별도로 설정하는 대신 동일한 스타일을 사용하는 여러 행, 열 또는 셀에서 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체를 공유해야 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 크기 조정에 대 한 모범 사례](best-practices-for-scaling-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기를 조정하는 최선의 방법](best-practices-for-scaling-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 글꼴 및 색 스타일 설정](how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)
