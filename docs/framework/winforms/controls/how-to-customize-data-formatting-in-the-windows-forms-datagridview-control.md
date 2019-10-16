---
title: '방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 사용자 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], formatting data
- DataGridView control [Windows Forms], cell styles
- cells [Windows Forms], changing colors in DataGridView control [Windows Forms]
- colors [Windows Forms], changing in DataGridView control [Windows Forms]
- data [Windows Forms], formatting in DataGridView control
- DataGridView control [Windows Forms], cell customization
- DataGridView control [Windows Forms], changing cell colors
- Windows Forms, changing colors of DataGridView cells
- DataGridView control [Windows Forms], substituting cell values for display
- data grids [Windows Forms], formatting data
ms.assetid: a6e72c70-ce18-425f-828d-d57be6f96ab6
ms.openlocfilehash: 948e9bf485b42b445491a4da9f8de7ae7974075c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592832"
---
# <a name="how-to-customize-data-formatting-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 사용자 지정
다음 코드 예제에서는 열과 값에 따라 셀이 표시되는 방식을 변경하는 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType> 이벤트에 대한 처리기를 구현하는 방법을 보여 줍니다.  
  
 음수를 포함하는 `Balance` 열의 셀에는 빨간색 배경이 제공됩니다. 또한 이러한 셀에 통화 형식을 지정하여 음수 값을 괄호 안에 표시할 수도 있습니다. 자세한 내용은 [방법: 형식 데이터에는 Windows Forms DataGridView 컨트롤](how-to-format-data-in-the-windows-forms-datagridview-control.md)합니다.  
  
 `Priority` 열의 셀에는 해당하는 텍스트 셀 값 대신 이미지가 표시됩니다. <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs>의 <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> 속성은 텍스트 셀 값을 가져오고 해당하는 이미지 표시 값을 설정하는 데 사용됩니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewCustomizeDataFormatting#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCustomizeDataFormatting/cs/customFormatting.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewCustomizeDataFormatting#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCustomizeDataFormatting/vb/customFormatting.vb#00)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
- 실행 파일과 동일한 디렉터리에 있는 <xref:System.Drawing.Bitmap>, `highPri.bmp` 및 `mediumPri.bmp`로 명명된 `lowPri.bmp` 이미지  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Drawing.Bitmap>
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
- [방법: 형식 데이터에는 Windows Forms DataGridView 컨트롤](how-to-format-data-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 형식 지정](data-formatting-in-the-windows-forms-datagridview-control.md)
