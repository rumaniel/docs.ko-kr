---
title: '방법: Windows Forms DataGridView 컨트롤에서 새 행에 대한 기본값 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data grids [Windows Forms], default values for new rows
- DataGridView control [Windows Forms], data entry
- rows [Windows Forms], specifying default values
- DataGridView control [Windows Forms], default values for new rows
ms.assetid: 8d127963-d9f8-4e4e-9f7f-beb66688f1f2
ms.openlocfilehash: 879c035366c4686ceff3250a63c6ae8d8d3cfec4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651954"
---
# <a name="how-to-specify-default-values-for-new-rows-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 새 행에 대한 기본값 지정
응용 프로그램 새로 추가 된 행에 대 한 값을 기본 차면 데이터 입력을 보다 편리 하 게 만들 수 있습니다. 사용 하 여 합니다 <xref:System.Windows.Forms.DataGridView> 클래스를 채울 수 있습니다 기본 값을 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 이벤트입니다. 이 이벤트는 사용자가 새 레코드에 대 한 행을 입력할 때 발생 합니다. 코드에서이 이벤트를 처리 하는 경우에 원하는 값이 선택한 셀을 채울 수 있습니다.  
  
 다음 코드 예제를 사용 하 여 새 행에 대 한 기본값을 지정 하는 방법에 설명 합니다 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> 이벤트입니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#120](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#120)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#120](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#120)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `dataGridView1`이라는 <xref:System.Windows.Forms.DataGridView> 컨트롤  
  
- A `NewCustomerId` 고유 생성에 대 한 함수 `CustomerID` 값입니다.  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 데이터 입력](data-entry-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤에서 새 레코드에 행 사용](using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)
