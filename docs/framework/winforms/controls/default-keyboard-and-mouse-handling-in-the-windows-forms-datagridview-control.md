---
title: Windows Forms DataGridView 컨트롤의 기본 키보드 및 마우스 처리
ms.date: 02/13/2018
helpviewer_keywords:
- data grids [Windows Forms], mouse handling
- DataGridView control [Windows Forms], navigation keys
- keyboards [Windows Forms], default handling in DataGridView control
- DataGridView control [Windows Forms], keyboard handling
- mouse [Windows Forms], default handling in DataGridView control
- DataGridView control [Windows Forms], mouse handling
- navigation keys [Windows Forms], DataGridView control
ms.assetid: 4519b928-bfc8-4e8b-bb9c-b1e76a0ca552
ms.openlocfilehash: 97b8c8c3e418586bbc0053c358a2924484115a26
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969137"
---
# <a name="default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 기본 키보드 및 마우스 처리

다음 표에서는 사용자가 키보드와 마우스를 통해 <xref:System.Windows.Forms.DataGridView> 컨트롤과 상호 작용할 수 있는 방법을 설명 합니다.  
  
> [!NOTE]
> 키보드 동작을 사용자 지정 하기 위해와 <xref:System.Windows.Forms.Control.KeyDown>같은 표준 키보드 이벤트를 처리할 수 있습니다. 그러나 편집 모드에서 호스팅된 편집 컨트롤은 키보드 입력을 수신 하 고 키보드 이벤트는 <xref:System.Windows.Forms.DataGridView> 컨트롤에 대해 발생 하지 않습니다. 편집 컨트롤 이벤트를 처리 하려면 <xref:System.Windows.Forms.DataGridView.EditingControlShowing> 이벤트 처리기의 편집 컨트롤에 처리기를 연결 합니다. 또는 <xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.DataGridView.ProcessDialogKey%2A> 및 메서드<xref:System.Windows.Forms.DataGridView.ProcessDataGridViewKey%2A> 를 재정의 하 여 하위 클래스에서 키보드 동작을 사용자 지정할 수 있습니다.  
  
## <a name="default-keyboard-handling"></a>기본 키보드 처리  
  
### <a name="basic-navigation-and-entry-keys"></a>기본 탐색 및 항목 키  
  
|키 또는 키 조합|설명|  
|----------------------------|-----------------|  
|아래쪽 화살표|포커스를 현재 셀 바로 아래의 셀로 이동 합니다. 포커스가 마지막 행에 있는 경우 아무 작업도 수행 하지 않습니다.|  
|왼쪽 화살표|포커스를 행의 이전 셀로 이동 합니다. 포커스가 행의 첫 번째 셀에 있으면는 아무 작업도 수행 하지 않습니다.|  
|오른쪽 화살표|포커스를 행의 다음 셀로 이동 합니다. 포커스가 행의 마지막 셀에 있으면는 아무 작업도 수행 하지 않습니다.|  
|위쪽 화살표|포커스를 현재 셀 바로 위의 셀로 이동 합니다. 포커스가 첫 번째 행에 있는 경우 아무 작업도 수행 하지 않습니다.|  
|홈|포커스를 현재 행의 첫 번째 셀로 이동 합니다.|  
|END|포커스를 현재 행의 마지막 셀로 이동 합니다.|  
|Page Down|컨트롤을 완전히 표시 되는 행 수 만큼 아래로 스크롤합니다. 열을 변경 하지 않고 마지막으로 표시 된 행으로 포커스를 이동 합니다.|  
|Page Up|컨트롤을 완전히 표시 되는 행 수 만큼 위로 스크롤합니다. 열을 변경 하지 않고 첫 번째로 표시 된 행으로 포커스를 이동 합니다.|  
|Tab|속성 값이 `false`이면 포커스를 현재 행의 다음 셀로 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 포커스가 행의 마지막 셀에 이미 있는 경우는 포커스를 다음 행의 첫 번째 셀로 이동 합니다. 포커스가 컨트롤의 마지막 셀에 있는 경우는 부모 컨테이너의 탭 순서에서 다음 컨트롤로 포커스를 이동 합니다.<br /><br /> 속성 값이 `true`이면 포커스가 부모 컨테이너의 탭 순서에서 다음 컨트롤로 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A>|  
|Shift+Tab|속성 값이 인 `false`경우 현재 행의 이전 셀로 포커스를 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 포커스가 행의 첫 번째 셀에 이미 있는 경우는 포커스를 이전 행의 마지막 셀로 이동 합니다. 포커스가 컨트롤의 첫 번째 셀에 있으면 부모 컨테이너의 탭 순서에서 이전 컨트롤로 포커스를 이동 합니다.<br /><br /> 속성 값이 `true`이면 포커스가 부모 컨테이너의 탭 순서에서 이전 컨트롤로 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A>|  
|Ctrl+Tab|속성 값이 `false`이면 포커스가 부모 컨테이너의 탭 순서에서 다음 컨트롤로 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A><br /><br /> 속성 값이 `true`이면 포커스를 현재 행의 다음 셀로 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 포커스가 행의 마지막 셀에 이미 있는 경우는 포커스를 다음 행의 첫 번째 셀로 이동 합니다. 포커스가 컨트롤의 마지막 셀에 있는 경우는 부모 컨테이너의 탭 순서에서 다음 컨트롤로 포커스를 이동 합니다.|  
|Ctrl+Shift+Tab|속성 값이 `false`이면 포커스가 부모 컨테이너의 탭 순서에서 이전 컨트롤로 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A><br /><br /> 속성 값이 인 `true`경우 현재 행의 이전 셀로 포커스를 이동 합니다. <xref:System.Windows.Forms.DataGridView.StandardTab%2A> 포커스가 행의 첫 번째 셀에 이미 있는 경우는 포커스를 이전 행의 마지막 셀로 이동 합니다. 포커스가 컨트롤의 첫 번째 셀에 있으면 부모 컨테이너의 탭 순서에서 이전 컨트롤로 포커스를 이동 합니다.|  
|CTRL + 화살표|화살표 방향으로 가장 멀리 있는 셀로 포커스를 이동 합니다.|  
|Ctrl+Home|포커스를 컨트롤의 첫 번째 셀로 이동 합니다.|  
|Ctrl+End|포커스를 컨트롤의 마지막 셀로 이동 합니다.|  
|CTRL + PAGE DOWN/UP|PAGE DOWN 또는 PAGE UP와 동일 합니다.|  
|F2|<xref:System.Windows.Forms.DataGridView.EditMode%2A> 속성 값이 <xref:System.Windows.Forms.DataGridViewEditMode.EditOnF2> 또는<xref:System.Windows.Forms.DataGridViewEditMode.EditOnKeystrokeOrF2>인 경우 현재 셀을 셀 편집 모드로 전환 합니다.|
|F3|<xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType> 속성 값이 인 <xref:System.Windows.Forms.DataGridViewColumnSortMode.Automatic>경우 현재 열을 정렬 합니다. 현재 열 머리글을 클릭 하는 것과 같습니다. .NET Framework 4.7.2부터 사용할 수 있습니다. 이 기능을 사용 하려면 응용 프로그램이 4.7.2 이상 버전을 .NET Framework 대상으로 하거나 AppContext 스위치를 사용 하 여 내게 필요한 옵션 개선 기능을 명시적으로 선택 해야 합니다.|  
|F4|현재 셀이 <xref:System.Windows.Forms.DataGridViewComboBoxCell>이면 셀을 편집 모드로 전환 하 고 드롭다운 목록을 표시 합니다.|  
|ALT + 위쪽/아래쪽 화살표|현재 셀이 <xref:System.Windows.Forms.DataGridViewComboBoxCell>이면 셀을 편집 모드로 전환 하 고 드롭다운 목록을 표시 합니다.|  
|스페이스바|현재 <xref:System.Windows.Forms.DataGridViewButtonCell>셀이, <xref:System.Windows.Forms.DataGridViewCheckBoxCell> <xref:System.Windows.Forms.DataGridView.CellClick> 또는 이면 및<xref:System.Windows.Forms.DataGridView.CellContentClick> 이벤트를 발생 시킵니다. <xref:System.Windows.Forms.DataGridViewLinkCell> 현재 셀이 <xref:System.Windows.Forms.DataGridViewButtonCell>이면 단추를 누릅니다. 현재 셀이 <xref:System.Windows.Forms.DataGridViewCheckBoxCell>이면에서도 확인 상태를 변경 합니다.|  
|Enter 키|현재 셀과 행의 모든 변경 내용을 커밋하고 포커스를 현재 셀 바로 아래의 셀로 이동 합니다. 포커스가 마지막 행에 있으면는 포커스를 이동 하지 않고 모든 변경 내용을 커밋합니다.|  
|Esc|컨트롤이 편집 모드에 있으면에서 편집을 취소 합니다. 컨트롤이 편집 모드에 있지 않은 경우에는 편집을 지 원하는 데이터 소스에 컨트롤이 바인딩되거나 행 수준 커밋 범위를 사용 하 여 가상 모드가 구현 된 경우 현재 행에 대 한 모든 변경 내용을 되돌립니다.|  
|백스페이스|셀을 편집할 때 삽입 지점 앞의 문자를 삭제 합니다.|  
|DELETE|셀을 편집할 때 삽입 지점 뒤의 문자를 삭제 합니다.|  
|Ctrl+Enter|포커스를 이동 하지 않고 현재 셀의 변경 내용을 커밋합니다. 또한 편집을 지 원하는 데이터 소스에 컨트롤이 바인딩되거나 행 수준 커밋 범위를 사용 하 여 가상 모드가 구현 된 경우 현재 행에 대 한 변경 내용을 커밋합니다.|  
|Ctrl+0|셀을 <xref:System.DBNull.Value?displayProperty=nameWithType> 편집할 수 있는 경우 현재 셀에 값을 입력 합니다. 기본적으로 <xref:System.DBNull> 셀 값의 표시 값은 현재 셀에 적용 되는 <xref:System.Windows.Forms.DataGridViewCellStyle> 의 <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 속성 값입니다.|  
  
### <a name="selection-keys"></a>선택 키

 속성이로 `false` 설정 되 고 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 속성이로 <xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>설정 된 경우 탐색 키를 사용 하 여 현재 셀을 변경 하면 선택 항목이 새 셀로 변경 됩니다. <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> SHIFT, CTRL 및 ALT 키는이 동작에 영향을 주지 않습니다.  
  
 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 가 <xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect> 또는 로<xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>설정 된 경우 동일한 동작이 발생 하지만 다음과 같이 추가 됩니다.  
  
|키 또는 키 조합|Description|  
|----------------------------|-----------------|  
|SHIFT + 스페이스바|전체 행 또는 열을 선택 합니다 (행 또는 열 머리글을 클릭 하는 것과 동일).|  
|탐색 키 (화살표 키, PAGE UP/DOWN, HOME, END)|전체 행 또는 열을 선택한 경우 현재 셀을 새 행 또는 열로 변경 하면 선택 영역 모드에 따라 전체 새 행 또는 열이 선택 됩니다.|  
  
 가 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 로 `false` 설정 되 고 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 가 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> 또는<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>로 설정 된 경우 키보드를 사용 하 여 현재 셀을 새 행 이나 열로 변경 하면 선택 항목이 전체 새 행 또는 열로 이동 합니다. SHIFT, CTRL 및 ALT 키는이 동작에 영향을 주지 않습니다.  
  
 가 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 로`true`설정 된 경우 탐색 동작은 변경 되지 않지만 shift 키를 누르면 (CTRL + shift를 포함) 키보드를 사용 하 여 탐색 하면 다중 셀 선택이 수정 됩니다. 탐색이 시작 되기 전에 컨트롤은 현재 셀을 앵커 셀로 표시 합니다. SHIFT 키를 누르는 동안 이동할 때 앵커 셀과 현재 셀 사이의 모든 셀이 선택 영역에 포함 됩니다. 컨트롤의 다른 셀은 이미 선택 되어 있는 경우 선택 된 상태로 유지 되지만 키보드 탐색이 앵커 셀과 현재 셀 사이에 일시적으로 배치 하면 선택이 취소 될 수 있습니다.  
  
 가 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 로 `true` 설정 되 고 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 가 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> 또는<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>로 설정 된 경우 앵커 셀과 현재 셀의 동작은 동일 하지만 전체 행 또는 열만 선택 되거나 선택이 취소 됩니다.  
  
## <a name="default-mouse-handling"></a>기본 마우스 처리
  
### <a name="basic-mouse-handling"></a>기본 마우스 처리
  
> [!NOTE]
> 마우스 왼쪽 단추로 셀을 클릭 하면 현재 셀이 항상 변경 됩니다. 마우스 오른쪽 단추를 사용 하 여 셀을 클릭 하면 바로 가기 메뉴가 열립니다 (있는 경우).  
  
|마우스 작업|Description|  
|------------------|-----------------|  
|마우스 왼쪽 단추 아래로|클릭 한 셀을 현재 셀로 만들고 <xref:System.Windows.Forms.DataGridView.CellMouseDown?displayProperty=nameWithType> 이벤트를 발생 시킵니다.|  
|마우스 왼쪽 단추 위로|<xref:System.Windows.Forms.DataGridView.CellMouseUp?displayProperty=nameWithType> 이벤트를 발생시킵니다.|  
|마우스 왼쪽 단추 클릭|<xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=nameWithType> 및<xref:System.Windows.Forms.DataGridView.CellMouseClick?displayProperty=nameWithType> 이벤트를 발생 시킵니다.|  
|마우스 왼쪽 단추를 누른 후 열 머리글 셀에 끌기|<xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=nameWithType> 속성이 인`true`경우 새 위치로 열을 끌어 놓을 수 있도록 열을 이동 합니다.|  
  
### <a name="mouse-selection"></a>마우스 선택

 마우스 가운데 단추 또는 마우스 휠에는 선택 동작이 연결 되지 않습니다.  
  
 속성이로 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 설정 되 <xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>고 속성이로 설정 된 경우 다음과 같은 동작이 발생 합니다. `false` <xref:System.Windows.Forms.DataGridView.MultiSelect%2A>  
  
|마우스 작업|설명|  
|------------------|-----------------|  
|마우스 왼쪽 단추 클릭|사용자가 셀을 클릭 하는 경우에는 현재 셀만 선택 합니다. 사용자가 행 또는 열 머리글을 클릭 하면 선택 동작이 발생 하지 않습니다.|  
|마우스 오른쪽 단추 클릭|하나를 사용할 수 있는 경우 바로 가기 메뉴를 표시 합니다.|  
  
 선택 모드에 따라 행 또는 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 열 머리글을 클릭 <xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>하면 전체 행 또는 열을 선택 하 고 현재 셀을 행 또는 열의 첫 번째 셀로 설정 한다는 점을 제외 하 고가 또는로 <xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect> 설정 된 경우에도 동일한 동작이 발생 합니다.  
  
 가 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> 또는 로<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>설정 된 경우 행 또는 열의 셀을 클릭 하면 전체 행 또는 열이 선택 됩니다.  
  
 가 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 로`true`설정 된 경우 CTRL 또는 SHIFT 키를 누르면 셀을 클릭 하면 다중 셀 선택이 수정 됩니다.  
  
 CTRL 키를 눌러 셀을 클릭 하면 다른 모든 셀의 현재 선택 상태가 유지 되는 동안 셀의 선택 상태가 변경 됩니다.  
  
 SHIFT 키를 누르는 동안 셀 또는 일련의 셀을 클릭 하면 첫 번째 클릭 이전에 현재 셀의 위치에 있는 앵커 셀과 현재 셀 사이의 모든 셀이 선택 영역에 포함 됩니다. 포인터를 클릭 하 여 여러 셀로 끌면 끌기 작업을 시작할 때 클릭 된 셀이 앵커 셀이 됩니다. SHIFT 키를 누른 상태에서 현재 셀을 변경 하 되 앵커 셀은 변경 하지 않고 계속 클릭 합니다. 컨트롤의 다른 셀은 이미 선택 되어 있는 경우 선택 된 상태로 유지 되지만 마우스 탐색이 고정 셀과 현재 셀 사이에 일시적으로 배치 하면 선택이 취소 될 수 있습니다.  
  
 가 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 로 `true` 설정 되 고 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 가 <xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect> 또는<xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>로 설정 된 경우 SHIFT 키를 누르면 행 또는 열 머리글 (선택 모드에 따라)을 클릭 하면 기존에 선택한 전체 행 또는 열이 선택 항목이 있습니다. 그렇지 않으면 선택을 취소 하 고 전체 행 또는 열에 대 한 새 선택을 시작 합니다. 그러나 CTRL 키를 누르면 행 또는 열 머리글을 클릭 하면 현재 선택 영역을 수정 하지 않고 클릭 된 행 또는 열을 현재 선택에서 추가 하거나 제거 합니다.  
  
 가 <xref:System.Windows.Forms.DataGridView.MultiSelect%2A> 로 `true` 설정 되 고 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> 가 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> 또는<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>로 설정 된 경우 SHIFT 또는 CTRL 키를 누르면 해당 셀을 클릭 하면 전체 행과 열만 영향을 받는 경우를 제외 하 고 동일한 방식으로 동작 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
