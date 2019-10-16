---
title: '방법: Windows Forms DataGridView 컨트롤에서 셀 모양 사용자 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data grids [Windows Forms], customizing cells
- DataGridView control [Windows Forms], customizing cells
- cells [Windows Forms], customizing in DataGridView control
ms.assetid: 478b20c9-625c-4116-9c5c-5a16e6f4ec67
ms.openlocfilehash: 9b07c139689a9776f6f901c0f9fbe9d2d0303d56
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648142"
---
# <a name="how-to-customize-the-appearance-of-cells-in-the-windows-forms-datagridview-control"></a>방법: Windows Forms DataGridView 컨트롤에서 셀 모양 사용자 지정
처리 하 여 모든 셀의 모양을 사용자 지정할 수 있습니다 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.CellPainting> 이벤트입니다. 추출할 수 있습니다는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Drawing.Graphics> 에서 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs.Graphics%2A> 의 속성을 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs>합니다. 이 사용 하 여 <xref:System.Drawing.Graphics>, 전체의 모양에 영향을 줄 수 있습니다 <xref:System.Windows.Forms.DataGridView> 컨트롤 있지만 일반적으로 현재 칠하고 있는 셀의 모양에만 영향을 합니다. 합니다 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs.ClipBounds%2A> 의 속성을 <xref:System.Windows.Forms.DataGridViewCellPaintingEventArgs> 그리기 작업을 현재 칠하고 있는 셀을 제한할 수 있습니다.  
  
 다음 코드 예제에서 모든 셀에 올려진를 `ContactName` 사용 하 여 열을 <xref:System.Windows.Forms.DataGridView> 컨트롤의 색 구성표입니다. 각 셀의 텍스트 내용에서 그려집니다 <xref:System.Drawing.Color.Crimson%2A>와 동일한 색의 삽입 사각형이 그려집니다 및 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.GridColor%2A> 속성.  
  
## <a name="example"></a>예제  
 [!code-csharp[System.Windows.Forms.DataGridViewCellPainting#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCellPainting/CS/form1.cs#10)]
 [!code-vb[System.Windows.Forms.DataGridViewCellPainting#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCellPainting/VB/form1.vb#10)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- A <xref:System.Windows.Forms.DataGridView> 컨트롤인 `dataGridView1` 사용 하 여를 `ContactName` Northwind 샘플 데이터베이스의 Customers 테이블에서 같은 열.  
  
- System, System.Windows.Forms 및 System.Drawing 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.CellPainting>
- [Windows Forms DataGridView 컨트롤 사용자 지정](customizing-the-windows-forms-datagridview-control.md)
