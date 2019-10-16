---
title: '방법: Windows Forms DataGridView 컨트롤에 대한 기본 셀 스타일 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], cell styles
- cells [Windows Forms], styles
- data grids [Windows Forms], cell styles
ms.assetid: 1aaaca43-5340-447e-99c0-9177d9776aa1
ms.openlocfilehash: de939051b613a0622f60178a566fd19dbca53694
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638159"
---
# <a name="how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에 대한 기본 셀 스타일 설정
<xref:System.Windows.Forms.DataGridView> 컨트롤을 사용하여 전체 컨트롤과 특정 열 및 행에 대한 기본 셀 스타일을 지정할 수 있습니다. 이러한 기본값은 컨트롤 수준에서 열 수준, 행 수준 및 셀 수준에 이르기까지 필터링합니다. 특정 <xref:System.Windows.Forms.DataGridViewCellStyle> 속성이 셀 수준에서 설정되지 않은 경우 행 수준의 기본 속성 설정이 사용됩니다. 행 수준에서도 속성이 설정되지 않은 경우 기본 열 설정이 사용됩니다. 끝으로, 열 수준에서도 속성이 설정되지 않은 경우 기본 <xref:System.Windows.Forms.DataGridView> 설정이 사용됩니다. 이 설정을 사용하면 여러 수준에서 속성 설정을 복제할 필요가 없습니다. 각 수준에서 상위 수준과 다른 스타일을 지정하면 됩니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.  
  
 Visual Studio에서는 이 작업이 광범위하게 지원됩니다.  또한 참조 [방법: Windows Forms DataGridView 컨트롤 디자이너를 사용 하 여 기본 셀 스타일 및 데이터 형식 설정](default-cell-styles-datagridview.md)합니다.  
  
### <a name="to-set-the-default-cell-styles-programmatically"></a>프로그래밍 방식으로 기본 셀 스타일을 설정하려면  
  
1. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> 속성을 통해 검색된 <xref:System.Windows.Forms.DataGridViewCellStyle>의 속성을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#141](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#141)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#141](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#141)]  
  
2. 여러 행과 열에서 사용할 새로운 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체를 만들고 초기화합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#142](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#142)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#142](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#142)]  
  
3. 특정 행과 열의 `DefaultCellStyle` 속성을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#143](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#143)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#143](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#143)]  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#140](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#140)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#140](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#140)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 큰 데이터 집합으로 작업할 때 최대 확장성을 얻으려면 개별 요소에 대한 스타일 속성을 별도로 설정하는 대신 동일한 스타일을 사용하는 여러 행, 열 또는 셀에서 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체를 공유해야 합니다. 또한 공유 행을 만들고 <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=nameWithType> 속성을 통해 액세스해야 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 크기 조정에 대 한 모범 사례](best-practices-for-scaling-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기를 조정하는 최선의 방법](best-practices-for-scaling-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에 대 한 행 스타일 교대로 반복 되는 설정](how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control.md)
