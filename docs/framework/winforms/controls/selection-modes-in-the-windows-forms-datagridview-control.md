---
title: Windows Forms DataGridView 컨트롤의 선택 모드
ms.date: 03/30/2017
helpviewer_keywords:
- selection [Windows Forms], modes in DataGridView control
- DataGridView control [Windows Forms], selection mode
ms.assetid: a3ebfd3d-0525-479d-9d96-d9e017289b36
ms.openlocfilehash: cfe80d5ccb73208f1c61a2ac6c9963343d398bcb
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046412"
---
# <a name="selection-modes-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 선택 모드

응용 프로그램에서 <xref:System.Windows.Forms.DataGridView> 컨트롤의 사용자 선택에 따라 작업을 수행 하려는 경우가 있습니다. 작업에 따라 가능한 선택의 종류를 제한 하는 것이 좋습니다. 예를 들어 응용 프로그램에서 현재 선택 된 레코드에 대 한 보고서를 인쇄할 수 있다고 가정 합니다. 이 경우 행의 아무 곳 이나 클릭 하면 항상 <xref:System.Windows.Forms.DataGridView> 전체 행을 선택 하 고 한 번에 한 행씩 선택할 수 있도록 컨트롤을 구성할 수 있습니다.

속성을 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType> 다음 <xref:System.Windows.Forms.DataGridViewSelectionMode> 열거형 값 중 하나로 설정 하 여 허용 되는 선택 항목을 지정할 수 있습니다.

|DataGridViewSelectionMode 값|Description|
|-------------------------------------|-----------------|
|<xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>|셀을 클릭 하면 해당 셀이 선택 됩니다. 행 및 열 머리글은 선택에 사용할 수 없습니다.|
|<xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>|셀을 클릭 하면 해당 셀이 선택 됩니다. 열 머리글을 클릭 하면 전체 열이 선택 됩니다. 열 머리글은 정렬에 사용할 수 없습니다.|
|<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>|셀 또는 열 머리글을 클릭 하면 전체 열이 선택 됩니다. 열 머리글은 정렬에 사용할 수 없습니다.|
|<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>|셀 또는 행 머리글을 클릭 하면 전체 행이 선택 됩니다.|
|<xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>|기본 선택 모드입니다. 셀을 클릭 하면 해당 셀이 선택 됩니다. 행 머리글을 클릭 하면 전체 행이 선택 됩니다.|

> [!NOTE]
> 런타임에 선택 모드를 변경 하면 현재 선택 영역이 자동으로 지워집니다.

기본적으로 사용자는 마우스를 사용 하 여 여러 행, 열 또는 셀을 선택 하 고, CTRL 또는 SHIFT 키를 눌러 선택 영역을 확장 또는 수정 하거나, 왼쪽 위 머리글 셀을 클릭 하 여 컨트롤의 모든 셀을 선택할 수 있습니다. 이 동작을 방지 하려면 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 속성을로 `false`설정 합니다.

<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> 및<xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect> 모드를 사용 하면 사용자가 행을 선택 하 고 delete 키를 눌러 행을 삭제할 수 있습니다. 사용자는 현재 셀이 편집 모드에 있지 않은 경우에만 행을 삭제할 <xref:System.Windows.Forms.DataGridView.AllowUserToDeleteRows%2A> 수 있고, 속성 `true`을로 설정 하 고, 기본 데이터 원본이 사용자 기반 행 삭제를 지원 합니다. 이러한 설정은 프로그래밍 행 삭제를 방지 하지 않습니다.

## <a name="programmatic-selection"></a>프로그래밍 방식 선택

현재 선택 모드는 프로그래밍 방식의 선택 및 사용자 선택의 동작을 제한 합니다. 컨트롤에 있는 셀, 행 또는 열의 `Selected` 속성을 설정 하 여 현재 선택 항목을 프로그래밍 방식으로 변경할 수 있습니다. <xref:System.Windows.Forms.DataGridView> 선택 모드에 따라 <xref:System.Windows.Forms.DataGridView.SelectAll%2A> 메서드를 통해 컨트롤의 모든 셀을 선택할 수도 있습니다. 선택을 취소 하려면 <xref:System.Windows.Forms.DataGridView.ClearSelection%2A> 메서드를 사용 합니다.

속성이로 `true`설정 된 경우 요소의 `Selected` 속성을 변경 하 <xref:System.Windows.Forms.DataGridView> 여 선택 영역에서 요소를 추가 하거나 제거할 수 있습니다. <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 그렇지 않으면 한 요소 `Selected` 에 대 `true` 한 속성을로 설정 하면 선택 영역에서 다른 요소가 자동으로 제거 됩니다.

<xref:System.Windows.Forms.DataGridView.CurrentCell%2A> 속성 값을 변경 해도 현재 선택 항목은 변경 되지 않습니다.

컨트롤의 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>, 및 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 속성을 통해 현재 선택 된 셀, 행 또는 열의 컬렉션을 검색할 수 있습니다. <xref:System.Windows.Forms.DataGridView> 컨트롤의 모든 셀이 선택 되어 있으면 이러한 속성에 액세스 하는 것은 비효율적입니다. 이 경우 성능 저하를 방지 하려면 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A> 메서드를 먼저 사용 합니다. 또한 이러한 컬렉션에 액세스 하 여 선택한 셀, 행 또는 열 수를 결정 하는 것은 비효율적입니다. 대신 <xref:System.Windows.Forms.DataGridView.GetCellCount%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.GetRowCount%2A>또는 <xref:System.Windows.Forms.DataGridViewElementStates.Selected> 메서드를 사용 하 여 값을 전달 해야 합니다. <xref:System.Windows.Forms.DataGridViewColumnCollection.GetColumnCount%2A>

> [!TIP]
> 선택한 셀을 프로그래밍 방식으로 사용 하는 방법을 보여 주는 예제 코드는 <xref:System.Windows.Forms.DataGridView> 클래스 개요에서 찾을 수 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.MultiSelect%2A>
- <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>
- <xref:System.Windows.Forms.DataGridViewSelectionMode>
- [Windows Forms DataGridView 컨트롤에서 선택 및 클립보드 사용](selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤의 선택 모드 설정](how-to-set-the-selection-mode-of-the-windows-forms-datagridview-control.md)
