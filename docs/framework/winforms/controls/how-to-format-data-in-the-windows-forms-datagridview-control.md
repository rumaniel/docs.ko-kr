---
title: '방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], formatting data
- data [Windows Forms], formatting in DataGridView control
- data grids [Windows Forms], enabling wordwrap
- currency values [Windows Forms], formatting in data grids
- data grids [Windows Forms], currency values
- data grids [Windows Forms], formatting data
- data grids [Windows Forms], text alignment
- data grids [Windows Forms], date values
- cells [Windows Forms], text alignment
ms.assetid: 8c33543c-9c08-4636-a65a-fdf714a529b7
ms.openlocfilehash: 0f295b44bf1dfffc7f4b6c52b54705bba1d82a81
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64609776"
---
# <a name="how-to-format-data-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 지정
다음 절차를 사용 하 여 셀 값의 기본 형식을 보여 줍니다.는 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 의 속성을 <xref:System.Windows.Forms.DataGridView> 컨트롤 및 컨트롤의 특정 열입니다. 고급 데이터 형식에 대 한 내용은 [방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 사용자 지정](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)합니다.  
  
### <a name="to-format-currency-and-date-values"></a>통화 서식 지정 및 날짜 값  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle>의 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 속성을 설정합니다. 다음 코드 예제를 사용 하 여 특정 열에 대 한 형식을 설정 합니다 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 열 속성입니다. 값은 `UnitPrice` 열 괄호로 묶어 음수 값을 사용 하 여 현재 culture 별 통화 형식으로 표시 합니다. 값은 `ShipDate` 열 현재 culture 별 간단한 날짜 형식으로 표시 합니다. 에 대 한 자세한 내용은 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 값을 참조 하세요 [형식](../../../standard/base-types/formatting-types.md)합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#071](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#071)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#071](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#071)]  
  
### <a name="to-customize-the-display-of-null-database-values"></a>Null 데이터베이스 값의 표시 사용자 지정  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle>의 <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 속성을 설정합니다. 다음 코드 예제에서는 합니다 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> "항목이" 같지 값이 포함 된 모든 셀에 표시할 속성 <xref:System.DBNull.Value?displayProperty=nameWithType>합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#073](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#073)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#073](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#073)]  
  
### <a name="to-enable-wordwrap-in-text-based-cells"></a>텍스트를 기반으로 셀에 단어 잘림 방지를 사용 하도록 설정 하려면  
  
- 설정 합니다 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> 의 속성을 <xref:System.Windows.Forms.DataGridViewCellStyle> 중 하나에 <xref:System.Windows.Forms.DataGridViewTriState> 열거형 값. 다음 코드 예제에서는 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> 전체 컨트롤에 대 한 줄 바꿈 모드를 설정 하는 속성입니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#074](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#074)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#074](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#074)]  
  
### <a name="to-specify-the-text-alignment-of-datagridview-cells"></a>DataGridView 셀의 텍스트 맞춤을 지정 하려면  
  
- 설정 합니다 <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A> 의 속성을 <xref:System.Windows.Forms.DataGridViewCellStyle> 중 하나에 <xref:System.Windows.Forms.DataGridViewContentAlignment> 열거형 값. 사용 하 여 특정 열에 대 한 맞춤을 설정 하는 다음 코드 예제는 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 열 속성입니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#072](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#072)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#072](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#072)]  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#070](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#070)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#070](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#070)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이러한 예제에는 다음이 필요합니다.  
  
- A <xref:System.Windows.Forms.DataGridView> 라는 컨트롤 `dataGridView1` 라는 열이 포함 된 `UnitPrice`, 라는 열 `ShipDate`, 및 라는 열 `CustomerName`합니다.  
  
- <xref:System?displayProperty=nameWithType>, <xref:System.Drawing?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 최대 확장성을 공유 해야 <xref:System.Windows.Forms.DataGridViewCellStyle> 여러 행, 열 또는 셀 개별적으로 각 요소에 대 한 스타일 속성을 설정 하는 대신 동일한 스타일을 사용 하는 개체입니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 크기 조정에 대 한 모범 사례](best-practices-for-scaling-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 형식 지정](data-formatting-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 사용자 지정](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)
- [형식 서식 지정](../../../standard/base-types/formatting-types.md)
