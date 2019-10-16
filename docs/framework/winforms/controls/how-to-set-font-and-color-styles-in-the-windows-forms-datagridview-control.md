---
title: '방법: Windows Forms DataGridView 컨트롤에서 글꼴 및 색 스타일 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], cell customization
- data grids [Windows Forms], customizing cells
- data grids [Windows Forms], font styles
- data grids [Windows Forms], color styles
ms.assetid: 588f2c57-d963-41b1-9c1d-d02d71818113
ms.openlocfilehash: ad2426ed9643fd46927c4f8b6373fedbec372d38
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638100"
---
# <a name="how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 글꼴 및 색 스타일 설정
<xref:System.Windows.Forms.DataGridViewCellStyle> 클래스의 속성을 설정하여 <xref:System.Windows.Forms.DataGridView> 컨트롤 내에 있는 셀의 모양을 지정할 수 있습니다. <xref:System.Windows.Forms.DataGridView> 클래스 및 해당 도우미 클래스의 다양한 속성에서 이 클래스의 인스턴스를 검색하거나 이러한 속성에 할당하기 위해 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체를 인스턴스화할 수 있습니다.  
  
 다음 절차에서는 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 속성을 사용한 셀 모양의 기본 사용자 지정을 보여 줍니다. 컨트롤의 모든 셀은 행, 열 또는 셀 수준에서 재정의되지 않는 한 이 속성을 통해 지정된 스타일을 상속합니다. 스타일 상속의 예제를 참조 하세요. [방법: Windows Forms DataGridView 컨트롤에 기본 셀 스타일 설정](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)합니다. <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스의 추가 사용에 대한 자세한 내용은 참고 항목 섹션에 나열된 항목을 참조하세요.  
  
 Visual Studio에서는 이 작업이 광범위하게 지원됩니다.  또한 참조 [방법: Windows Forms DataGridView 컨트롤 디자이너를 사용 하 여 기본 셀 스타일 및 데이터 형식 설정](default-cell-styles-datagridview.md)합니다.  
  
### <a name="to-specify-the-font-used-by-datagridview-cells"></a>DataGridView 셀에서 사용되는 글꼴을 지정하려면  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle>의 <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A> 속성을 설정합니다. 다음 코드 예제에서는 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> 속성을 사용하여 전체 컨트롤의 글꼴을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#101](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#101)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#101](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#101)]  
  
### <a name="to-specify-the-foreground-and-background-colors-of-datagridview-cells"></a>DataGridView 셀의 전경색과 배경색을 지정하려면  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle>의 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 및 <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> 속성을 설정합니다. 다음 코드 예제에서는 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> 속성을 사용하여 전체 컨트롤에 대해 이러한 스타일을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#102](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#102)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#102](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#102)]  
  
### <a name="to-specify-the-foreground-and-background-colors-of-selected-datagridview-cells"></a>선택한 DataGridView 셀의 전경색과 배경색을 지정하려면  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle>의 <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A> 및 <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> 속성을 설정합니다. 다음 코드 예제에서는 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> 속성을 사용하여 전체 컨트롤에 대해 이러한 스타일을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#103](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#103)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#103](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#103)]  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#100](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#100)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#100](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#100)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 최대 확장성을 얻으려면 각 요소에 대한 스타일 속성을 별도로 설정하는 대신 동일한 스타일을 사용하는 여러 행, 열 또는 셀에서 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체를 공유해야 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 크기 조정에 대 한 모범 사례](best-practices-for-scaling-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
