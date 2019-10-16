---
title: '방법: 사용자가 Windows Forms DataGridView 컨트롤에서 여러 셀을 클립보드에 복사할 수 있도록 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cells [Windows Forms], copying to Clipboard
- DataGridView control [Windows Forms], copying multiple cells
- data grids [Windows Forms], copying multiple cells
- Clipboard [Windows Forms], copying multiple cells
ms.assetid: fd0403b2-d0e3-4ae0-839c-0f737e1eb4a9
ms.openlocfilehash: b220603adcaeae6f3380a2e3c10ea524c9a61f24
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591912"
---
# <a name="how-to-enable-users-to-copy-multiple-cells-to-the-clipboard-from-the-windows-forms-datagridview-control"></a>방법: 사용자가 Windows Forms DataGridView 컨트롤에서 여러 셀을 클립보드에 복사할 수 있도록 설정
셀 복사를 사용하면 <xref:System.Windows.Forms.DataGridView> 컨트롤의 데이터가 <xref:System.Windows.Forms.Clipboard>를 통해 다른 애플리케이션에 쉽게 액세스할 수 있습니다. 선택된 셀의 값은 문자열로 변환되고 메모장 및 Excel 같은 애플리케이션에 붙여넣도록 탭으로 구분된 텍스트 값으로 클립보드에 추가되거나 Word 같은 애플리케이션에 붙여넣도록 HTML 형식 테이블로 클립보드에 추가됩니다.  
  
 셀 값만 복사하거나 클립보드 데이터에 행 및 열 머리글 텍스트를 포함하거나 사용자가 전체 행이나 열을 선택할 때만 머리글을 포함하도록 셀 복사를 구성할 수 있습니다.  
  
 선택 모드에 따라 사용자는 연결이 끊어진 셀 그룹 여러 개를 선택할 수 있습니다. 사용자가 셀을 클립보드에 복사할 때 셀이 선택되지 않은 행과 열은 복사되지 않습니다. 모든 다른 행 또는 열은 클립보드에 복사된 데이터 테이블의 행과 열이 됩니다. 이들 행이나 열에서 선택되지 않은 셀은 빈 자리 표시자로 클립보드에 복사됩니다.  
  
### <a name="to-enable-cell-copying"></a>셀 복사를 사용하도록 설정하려면 다음을 수행합니다.  
  
- <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A?displayProperty=nameWithType> 속성을 설정합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewClipboardDemo#15](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/CS/datagridviewclipboarddemo.cs#15)]
     [!code-vb[System.Windows.Forms.DataGridViewClipboardDemo#15](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/VB/datagridviewclipboarddemo.vb#15)]  
  
## <a name="example"></a>예제  
 다음 전체 코드 예제에서는 셀을 클립보드에 복사하는 방법을 보여 줍니다. 이 예제는 <xref:System.Windows.Forms.DataGridView.GetClipboardContent%2A?displayProperty=nameWithType> 메서드를 사용하여 선택된 셀을 클립보드에 복사하는 단추를 포함하고 클립보드 내용을 텍스트 상자에 표시합니다.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewClipboardDemo#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/CS/datagridviewclipboarddemo.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewClipboardDemo#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewClipboardDemo/VB/datagridviewclipboarddemo.vb#00)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 코드에는 다음이 필요합니다.  
  
- N:System 및 N:System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.ClipboardCopyMode%2A>
- <xref:System.Windows.Forms.DataGridView.GetClipboardContent%2A>
- [Windows Forms DataGridView 컨트롤에서 선택 및 클립보드 사용](selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)
