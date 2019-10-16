---
title: Windows Forms DataGridView 컨트롤 사용자 지정
ms.date: 03/30/2017
helpviewer_keywords:
- data grids [Windows Forms], customization
- DataGridView control [Windows Forms], customization
ms.assetid: 01ea5d4c-a736-4596-b0e9-a67a1b86e15f
ms.openlocfilehash: ab8d1f07c608aca4f14f5e73860f8c3e263a4610
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011433"
---
# <a name="customizing-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤 사용자 지정
`DataGridView` 컨트롤 모양과 해당 셀, 행 및 열의 기본 동작 (모양 및 느낌)을 조정 하는 데 사용할 수 있는 몇 가지 속성을 제공 합니다. 그러나 기능 보다 우수한 특별 한 요구 사항이 있는 경우는 <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스, 소유자 컨트롤에 대 한 그리기를 구현 하거나 수도 사용자 지정 셀, 열 및 행 키를 만들어 해당 기능을 확장 합니다.  
  
 그릴 셀 및 행 직접, 다양 한 처리할 수 있습니다 `DataGridView` 그리기 이벤트입니다. 를 기존 기능을 수정 하거나 새 기능을 제공 하려면 기존에서 파생 된 고유한 형식을 만들 수 있습니다 `DataGridViewCell`, `DataGridViewColumn`, 및 `DataGridViewRow` 형식입니다. 또한 선택한 셀이 편집 모드일 때 컨트롤을 표시 하는 파생된 형식을 생성 하 여 새로운 편집 기능을 제공할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: Windows Forms DataGridView 컨트롤에서 셀 모양 사용자 지정](customize-the-appearance-of-cells-in-the-datagrid.md)  
 처리 하는 방법에 설명 합니다 <xref:System.Windows.Forms.DataGridView.CellPainting> 그리기 위해 이벤트 셀을 수동으로.  
  
 [방법: Windows Forms DataGridView 컨트롤에서 행 모양 사용자 지정](customize-the-appearance-of-rows-in-the-datagrid.md)  
 처리 하는 방법에 설명 합니다 <xref:System.Windows.Forms.DataGridView.RowPrePaint> 및 <xref:System.Windows.Forms.DataGridView.RowPostPaint> 여러 열으로 확장 하기 위해 사용자 지정, 그라데이션 배경이 있는 행을 그리기 및 콘텐츠는 이벤트입니다.  
  
 [방법: Windows Forms DataGridView 컨트롤에서 셀 및 열은 동작과 모양을 확장 하 여 사용자 지정](customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)  
 파생 된 사용자 지정 형식을 만드는 방법을 설명 합니다 `DataGridViewCell` 고 `DataGridViewColumn` 에 마우스 포인터가 있을 때 셀을 강조 표시 하기 위해.  
  
 [방법: Windows Forms DataGridView 컨트롤의 단추 열에서 단추를 사용 하지 않도록 설정](disable-buttons-in-a-button-column-in-the-datagrid.md)  
 파생 된 사용자 지정 형식을 만드는 방법을 설명 합니다 <xref:System.Windows.Forms.DataGridViewButtonCell> 및 <xref:System.Windows.Forms.DataGridViewButtonColumn> 단추 열에서 비활성화 된 단추를 표시 하기 위해.  
  
 [방법: Windows Forms DataGridView 셀에서 컨트롤을 호스트](how-to-host-controls-in-windows-forms-datagridview-cells.md)  
 구현 하는 방법에 설명 합니다 `IDataGridViewEditingControl` 인터페이스에서 파생 된 사용자 지정 형식을 만들고 `DataGridViewCell` 및 `DataGridViewColumn` 표시 하기 위해를 <xref:System.Windows.Forms.DateTimePicker> 셀 편집 모드에 있을 때이 컨트롤입니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridView> 컨트롤에 대한 참조 설명서를 제공합니다.  
  
 <xref:System.Windows.Forms.DataGridViewCell>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridViewCell> 클래스입니다.  
  
 <xref:System.Windows.Forms.DataGridViewRow>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridViewRow> 클래스입니다.  
  
 <xref:System.Windows.Forms.DataGridViewColumn>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.DataGridViewColumn> 클래스입니다.  
  
 <xref:System.Windows.Forms.IDataGridViewEditingControl>  
 에 대 한 참조 설명서를 제공 합니다 <xref:System.Windows.Forms.IDataGridViewEditingControl> 인터페이스입니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)  
 컨트롤의 기본 모양과 셀 데이터의 표시 형식을 수정하는 방법을 설명하는 항목을 제공합니다.  
  
## <a name="see-also"></a>참고자료

- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
- [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)
