---
title: DataGrid 컨트롤에서의 기본 키보드 및 마우스 동작
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid [WPF], keyboard behavior
- DataGrid [WPF], mouse behavior
- keyboard behavior [WPF], DataGrid
- mouse behavior [WPF], DataGrid
ms.assetid: 563b8854-ca39-4d97-8235-17eaa0f93c8d
ms.openlocfilehash: a518c6123b21ae62742071a0b26c6a09fa272b17
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591269"
---
# <a name="default-keyboard-and-mouse-behavior-in-the-datagrid-control"></a>DataGrid 컨트롤에서의 기본 키보드 및 마우스 동작
이 항목에서는 사용자 상호 작용 하는 방법을 설명 합니다 <xref:System.Windows.Controls.DataGrid> 키보드 및 마우스를 사용 하 여 제어 합니다.  
  
 와 일반적인 상호 작용을 <xref:System.Windows.Controls.DataGrid> 탐색, 선택 및 편집을 포함 합니다. 선택 동작에 영향을 받는 합니다 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 고 <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A> 속성입니다. 이 항목에서 설명한 동작을 유발 하는 기본값은 <xref:System.Windows.Controls.DataGridSelectionMode.Extended?displayProperty=nameWithType> 고 <xref:System.Windows.Controls.DataGridSelectionUnit.FullRow?displayProperty=nameWithType>입니다. 이러한 값을 변경 하면 설명에서 다른 동작이 발생할 수 있습니다. 편집 컨트롤의 표준 키보드 동작을 재정의할 수 있습니다 셀 편집 모드의 경우는 <xref:System.Windows.Controls.DataGrid>합니다.  
  
## <a name="default-keyboard-behavior"></a>기본 키보드 동작  
 다음 표에서 대 한 기본 키보드 동작을 <xref:System.Windows.Controls.DataGrid>입니다.  
  
|키 또는 키 조합|설명|  
|----------------------------|-----------------|  
|아래쪽 화살표|현재 셀의 바로 아래 셀으로 포커스를 이동합니다. 포커스가 있는 마지막 행 이면 아무 작업도 수행 하지 아래쪽 화살표 키를 눌러 합니다.|  
|위쪽 화살표|현재 셀 바로 위 셀으로 포커스를 이동합니다. 포커스를 첫 번째 행 이면 아무 작업도 수행 하지 위쪽 화살표 키를 눌러 합니다.|  
|왼쪽 화살표|행의 이전 셀으로 포커스를 이동합니다. 포커스가 행의 첫 번째 셀에 있는 경우 아무 작업도 수행 하지 왼쪽 화살표 키를 누르십시오.|  
|오른쪽 화살표|행의 다음 셀으로 포커스를 이동합니다. 포커스가 행의 마지막 셀에 있는 경우 아무 작업도 수행 하지 오른쪽 화살표 키를 누르십시오.|  
|홈|현재 행에서 첫 번째 셀으로 포커스를 이동합니다.|  
|End |현재 행의 마지막 셀으로 포커스를 이동합니다.|  
|Page Down|행 그룹화 되지 않은 경우 완전 하 게 표시 되는 행 수가 컨트롤을 아래로 스크롤합니다. 열을 변경 하지 않고 완전히 표시 되는 마지막 행 포커스를 이동 합니다.<br /><br /> 행을 그룹화 하는 경우의 마지막 행에 포커스를 이동 합니다 <xref:System.Windows.Controls.DataGrid> 열을 변경 하지 않고 있습니다.|  
|Page Up|행 그룹화 되지 않은 경우 컨트롤을 위로 스크롤합니다 완벽 하 게 표시 되는 행의 수입니다. 열을 변경 하지 않고 표시 되는 첫 번째 행에 포커스를 이동 합니다.<br /><br /> 행을 그룹화 하는 경우 첫 번째 행에 포커스를 이동 합니다 <xref:System.Windows.Controls.DataGrid> 열을 변경 하지 않고 있습니다.|  
|Tab|현재 행에서 다음 셀으로 포커스를 이동합니다. 행의 마지막 셀에 포커스가 있으면 포커스가 다음 행에서 첫 번째 셀으로 이동 합니다. 컨트롤의 마지막 셀에 포커스가 있으면 부모 컨테이너의 탭 순서의 다음 컨트롤로 포커스를 이동 합니다.<br /><br /> 현재 셀이 편집 모드에 있고 TAB을 누르면 포커스가 현재 행에서를 이동 하려면, 모든 행에 대 한 변경 내용이 커밋되기 포커스를 변경 하기 전에 하는 경우.|  
|Shift+Tab|현재 행에서 이전 셀으로 포커스를 이동합니다. 포커스가 행의 첫 번째 셀에 이미 있으면 이전 행의 마지막 셀으로 포커스를 이동 합니다. 컨트롤의 첫 번째 셀에 포커스가 있으면 포커스가 부모 컨테이너의 탭 순서에서 이전 컨트롤로 이동 합니다.<br /><br /> 현재 셀이 편집 모드에 있고 TAB을 누르면 포커스가 현재 행에서를 이동 하려면, 모든 행에 대 한 변경 내용이 커밋되기 포커스를 변경 하기 전에 하는 경우.|  
|Ctrl+아래쪽 화살표|현재 열의 마지막 셀으로 포커스를 이동합니다.|  
|Ctrl+위쪽 화살표|현재 열의 첫째 셀으로 포커스를 이동합니다.|  
|Ctrl+오른쪽 화살표|현재 행의 마지막 셀으로 포커스를 이동합니다.|  
|Ctrl+왼쪽 화살표|현재 행에서 첫 번째 셀으로 포커스를 이동합니다.|  
|Ctrl+Home|컨트롤의 첫 번째 셀으로 포커스를 이동합니다.|  
|Ctrl+End|컨트롤의 마지막 셀으로 포커스를 이동합니다.|  
|Ctrl+Page Down|PAGE DOWN과 동일 합니다.|  
|Ctrl+Page Up|PAGE UP과 동일 합니다.|  
|F2|경우는 <xref:System.Windows.Controls.DataGrid.IsReadOnly%2A?displayProperty=nameWithType> 속성은 `false` 하며 <xref:System.Windows.Controls.DataGridColumn.IsReadOnly%2A?displayProperty=nameWithType> 속성이 `false` 현재 열에 대 한 현재 셀을 셀 편집 모드로 전환 합니다.|  
|Enter 키|현재 셀 및 행 변경 내용을 커밋하고 현재 셀의 바로 아래 셀으로 포커스를 이동 합니다. 마지막 행에 포커스가 있으면 포커스가 이동 하지 않고 모든 변경 내용을 커밋합니다.|  
|Esc|컨트롤 편집 모드인 경우에 편집을 취소 하 고 컨트롤에서 수행한 모든 변경 내용이 되돌립니다. 기본 데이터 원본 구현 하는 경우 <xref:System.ComponentModel.IEditableObject>, esc 키를 두 번째로 전체 행에 대 한 편집 모드를 취소 합니다.|  
|백스페이스|셀을 편집할 때 커서를 앞에 있는 문자를 삭제 합니다.|  
|Delete|셀을 편집할 때 커서 뒤의 문자를 삭제 합니다.|  
|Ctrl+Enter|포커스를 이동 하지 않고 현재 셀의 모든 변경 사항을 커밋합니다.|  
|Ctrl+A|경우 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 로 설정 된 <xref:System.Windows.Controls.DataGridSelectionMode.Extended>, 모든 행을 선택 합니다 <xref:System.Windows.Controls.DataGrid>합니다.|  
  
## <a name="selection-keys"></a>선택 키  
 경우는 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 속성이 <xref:System.Windows.Controls.DataGridSelectionMode.Extended>, 탐색 동작을 변경 되지 않지만 다중 행 선택을 수정 됩니다 (CTRL + SHIFT 포함)는 shift 키를 누른 채 키보드를 사용 하 여 탐색 합니다. 탐색을 시작 하기 전에 컨트롤을 앵커 행으로 현재 행을 표시 합니다. Shift 키로 이동 하면 선택 영역 앵커 행과 현재 행 사이의 모든 행을 포함 합니다.  
  
 다음 선택 키를 사용 하 여 다중 행 선택을 수정합니다.  
  
- Shift+아래쪽 화살표  
  
- Shift+위쪽 화살표  
  
- Shift+Page Down  
  
- Shift+Page Up  
  
- Ctrl+Shift+아래쪽 화살표  
  
- Ctrl+Shift+위쪽 화살표  
  
- Ctrl+Shift+Home  
  
- Ctrl+Shift+End  
  
## <a name="default-mouse-behavior"></a>기본 마우스 동작  
 다음 표에서 대 한 기본 마우스 동작을 <xref:System.Windows.Controls.DataGrid>입니다.  
  
|마우스 작업|설명|  
|------------------|-----------------|  
|선택 하지 않은 행을 클릭 합니다.|현재 행 및 현재 셀을 클릭 한 셀을 클릭 한 행으로 만듭니다.|  
|현재 셀을 클릭 합니다.|현재 셀을 편집 모드로 전환 합니다.|  
|열 머리글 셀을 끌어 옵니다.|경우는 <xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A?displayProperty=nameWithType> 속성은 `true` 하며 <xref:System.Windows.Controls.DataGridColumn.CanUserReorder%2A?displayProperty=nameWithType> 속성이 `true` 새 위치를 삭제할 수 있도록 현재 열에 대 한 열을 이동 합니다.|  
|열 머리글 구분 기호를 끌어 옵니다.|경우는 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> 속성은 `true` 하며 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> 속성이 `true` 현재 열에 대 한 열 크기를 조정 합니다.|  
|열 머리글 구분선을 두 번 클릭|경우는 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> 속성은 `true` 및 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> 속성이 `true` 현재 열의 자동 크기 사용 하 여 열을 <xref:System.Windows.Controls.DataGridLength.Auto%2A> 크기 조정 모드입니다.|  
|열 머리글 셀을 클릭 합니다.|경우는 <xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A?displayProperty=nameWithType> 속성은 `true` 하며 <xref:System.Windows.Controls.DataGridColumn.CanUserSort%2A?displayProperty=nameWithType> 속성이 `true` 현재 열에 대 한 열을 정렬 합니다.<br /><br /> 이미 정렬 된 열 머리글을 클릭 하는 열의 정렬 방향을 반전 됩니다.<br /><br /> 클릭 한 순서 대로 여러 열을 기준으로 정렬 됩니다 여러 열 머리글을 클릭 하는 동안 SHIFT 키를 누릅니다.|  
|CTRL + 행을 클릭 합니다.|경우 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 로 설정 된 <xref:System.Windows.Controls.DataGridSelectionMode.Extended>, 연속 되지 않은 다중 행 선택 영역을 수정 합니다.<br /><br /> 행은 이미 선택 되어 있으면 행을 선택 취소 합니다.|  
|SHIFT + 행을 클릭 합니다.|하는 경우 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 로 설정 된 <xref:System.Windows.Controls.DataGridSelectionMode.Extended>, 인접 한 다중 행 선택을 수정 합니다.|  
|행 그룹 머리글을 클릭 합니다.|확장 또는 그룹을 축소 합니다.|  
|왼쪽된 위 모퉁이에 있는 모든 선택 단추를 클릭 합니다 <xref:System.Windows.Controls.DataGrid>|경우 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 로 설정 된 <xref:System.Windows.Controls.DataGridSelectionMode.Extended>, 모든 행을 선택 합니다 <xref:System.Windows.Controls.DataGrid>합니다.|  
  
## <a name="mouse-selection"></a>마우스 선택  
 경우는 <xref:System.Windows.Controls.DataGrid.SelectionMode%2A> 속성이 <xref:System.Windows.Controls.DataGridSelectionMode.Extended>, CTRL 또는 shift 키를 누른 채 행을 클릭 하면 다중 행 선택을 수정 됩니다.  
  
 CTRL 키를 눌러 행을 클릭 하면 다른 모든 행은 현재 선택 상태로 유지 하는 동안 행의 선택 상태가 변경 됩니다. 인접 하지 않은 행을 선택 하려면이 작업을 수행 합니다.  
  
 SHIFT 키를 누르면 하는 동안 행을 클릭 하면 선택 클릭 하기 전에 현재 행의 위치에 있는 앵커 행과 현재 행 사이의 모든 행을 포함 합니다. 이후에 shift 키를 누른 채 클릭 앵커 행이 아닌 현재 행이 변경 됩니다. 인접 한 행의 범위를 선택 하려면이 작업을 수행 합니다.  
  
 인접 하지 않은 범위의 인접 한 행을 선택 하려면 CTRL + SHIFT은 결합할 수 있습니다. 이렇게 하려면 shift 키를 사용 하 여 첫 번째 범위를 선택 하에서 앞에서 설명한 대로 클릭 합니다. 행의 첫 번째 범위를 선택한 후 ctrl 키를 사용 + 다음 범위에서 첫 번째 행을 선택 하려면 클릭 한 다음 CTRL + SHIFT를 누른 채 다음 범위에서 마지막 행을 클릭 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.DataGrid>
- <xref:System.Windows.Controls.DataGrid.SelectionMode%2A>
