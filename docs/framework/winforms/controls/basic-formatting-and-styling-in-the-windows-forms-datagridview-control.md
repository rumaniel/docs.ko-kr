---
title: Windows Forms DataGridView 컨트롤에서 기본 형식 및 스타일 지정
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], formatting and styling
- data grids [Windows Forms], formatting
ms.assetid: b9b90836-1f56-4aa9-8db8-edc78fe830e8
ms.openlocfilehash: 5e967c1bbe54095cc11e48b014600158da7fe6a3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011686"
---
# <a name="basic-formatting-and-styling-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤에서 기본 형식 및 스타일 지정
`DataGridView` 컨트롤을 사용 하면 쉽게 셀의 기본 모양과 셀 값의 표시 형식을 정의할 수 있습니다. 모양을 정의할 수 있으며, 개별 셀, 특정 열과 행의 셀 또는 컨트롤의 모든 셀에 대 한 속성을 설정 하 여 스타일 서식 지정 된 `DataGridViewCellStyle` 다양 한를 통해 액세스 되는 개체 `DataGridView` 속성을 제어 합니다. 또한 처리 하 여 셀 값 등의 요인에 따라 동적으로 이러한 스타일을 수정할 수는 `CellFormatting` 이벤트입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 테두리 및 Windows Forms DataGridView 컨트롤의 모눈선 스타일 변경](change-the-border-and-gridline-styles-in-the-datagrid.md)  
 설정 하는 방법에 설명 `DataGridView` 컨트롤 테두리 및 셀 사이의 경계 줄의 모양을 정의 하는 속성입니다.  
  
 [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)  
 에 대해 설명 합니다 `DataGridViewCellStyle` 클래스 및 해당 형식의 속성은 컨트롤에서 셀을 표시 하는 방법을 정의 하려면 상호 작용 하는 방법을 합니다.  
  
 [방법: Windows Forms DataGridView 컨트롤에 대 한 기본 셀 스타일 설정](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)  
 사용 하는 방법에 설명 `DataGridViewCellStyle` 전체 컨트롤에 특정 행과 열에서 셀의 기본 모양을 정의 하는 속성입니다.  
  
 [방법: 형식 데이터에는 Windows Forms DataGridView 컨트롤](how-to-format-data-in-the-windows-forms-datagridview-control.md)  
 사용 하 여 셀 표시 값의 서식을 지정 하는 방법에 설명 `DataGridViewCellStyle` 속성입니다.  
  
 [방법: Windows Forms DataGridView 컨트롤의 글꼴 및 색 스타일 설정](how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)  
 사용 하는 방법에 설명 합니다 `DefaultCellStyle` 속성을 기본 설정 컨트롤의 모든 셀에 대 한 특성을 표시 합니다.  
  
 [방법: Windows Forms DataGridView 컨트롤에 대 한 행 스타일 교대로 반복 되는 설정](how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control.md)  
 다르게 표시 되는 교대로 반복 되는 행을 사용 하 여 컨트롤에서 장부와 비슷한 효과 만드는 방법을 설명 합니다.  
  
 [방법: 행 템플릿을 사용 하 여 Windows Forms DataGridView 컨트롤에서 행 사용자 지정](use-the-row-template-to-customize-rows-in-the-datagrid.md)  
 사용 하는 방법에 설명 합니다 `RowTemplate` 속성을 컨트롤의 모든 행에 사용할 행 속성을 설정 합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridView> 컨트롤에 대한 참조 설명서를 제공합니다.  
  
 <xref:System.Windows.Forms.DataGridViewCellStyle>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스입니다.  
  
 <xref:System.Windows.Forms.DataGridView.CellFormatting>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridView.CellFormatting> 이벤트입니다.  
  
 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 속성입니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Windows Forms DataGridView 컨트롤 사용자 지정](customizing-the-windows-forms-datagridview-control.md)  
 <xref:System.Windows.Forms.DataGridView> 셀 및 행의 사용자 지정 그리기를 수행하고 파생된 셀, 열 및 행 형식을 설명하는 항목을 제공합니다.  
  
 [Windows Forms DataGridView 컨트롤의 기본 열, 행 및 셀 기능](basic-column-row-and-cell-features-wf-datagridview-control.md)  
 셀, 행 및 열 속성을 사용 하는 일반적으로 설명 하는 항목을 제공 합니다.  
  
## <a name="see-also"></a>참고자료

- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
