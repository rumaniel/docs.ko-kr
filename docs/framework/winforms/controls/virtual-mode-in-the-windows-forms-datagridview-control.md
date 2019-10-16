---
title: Windows Forms DataGridView 컨트롤의 가상 모드
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], virtual mode
ms.assetid: feae5d43-2848-4b1a-8ea7-77085dc415b5
ms.openlocfilehash: f284835578221ad1fe859f260e37bb829cd64b2d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009138"
---
# <a name="virtual-mode-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 가상 모드
가상 모드를 사용 하 여 간의 상호 작용을 관리할 수 있습니다는 <xref:System.Windows.Forms.DataGridView> 컨트롤 및 사용자 지정 데이터 캐시 합니다. 가상 모드 구현 하려면 합니다 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성을 `true` 하 고 하나 이상의이 항목에서 설명 하는 이벤트를 처리 합니다. 일반적으로 처리 하는 적어도 `CellValueNeeded` 컨트롤에 대 한 조회 데이터 캐시에서 값을 사용 하도록 설정 하는 이벤트입니다.  
  
## <a name="bound-mode-and-virtual-mode"></a>바인딩된 모드와 가상 모드  
 가상 모드는 보완 하거나 바인딩된 모드를 대체 해야 하는 경우에 필요 합니다. 설정한 바인딩 모드로 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성 및 컨트롤을 자동으로 지정된 된 소스에서 데이터를 로드 하 고 사용자 변경 내용을 다시 제출 합니다. 표시 되는 바인딩된 열을 제어할 수 있습니다 하 고 데이터 원본 자체에 일반적으로 정렬 하는 등의 작업을 처리 합니다.  
  
## <a name="supplementing-bound-mode"></a>바인딩된 모드를 보완합니다.  
 바인딩된 열과 함께 바인딩되지 않은 열을 표시 하 여 바인딩된 모드를 보완할 수 있습니다. 이 "혼합된 모드" 라고도 하 고 계산 된 값 또는 사용자 인터페이스 (UI)을 제어 하는 등을 표시 하는 데 유용 합니다.  
  
 바인딩되지 않은 열이 외부 데이터 원본 이기 때문에 데이터 원본의 정렬 작업에 의해 무시 됩니다. 따라서 혼합된 모드에서 정렬을 사용 하는 경우 로컬 캐시에 바인딩되지 않은 데이터를 관리 하며 수 있도록 가상 모드 구현 된 <xref:System.Windows.Forms.DataGridView> 컨트롤 상호 작용 합니다.  
  
 가상 모드를 사용 하 여 바인딩되지 않은 열에서 해당 값을 유지 하는 방법에 대 한 자세한 내용은 예제를 참조 합니다 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A?displayProperty=nameWithType> 속성 및 <xref:System.Windows.Forms.DataGridViewComboBoxColumn?displayProperty=nameWithType> 클래스 참조 항목입니다.  
  
## <a name="replacing-bound-mode"></a>바인딩된 모드를 대체합니다.  
 바인딩된 모드는 성능 요구를 충족 하지 않습니다, 경우에 가상 모드 이벤트 처리기를 통해 사용자 지정 캐시에서 모든 데이터를 관리할 수 있습니다. 예를 들어-just-in-time 데이터 로드만 검색 하는 메커니즘을 구현 하 여 가상 모드를 사용할 수 있습니다 만큼의 데이터 네트워크에 연결 된 데이터베이스에서 최적의 성능을 위해 필요 합니다. 이 시나리오는 제한 된 양의 RAM 또는 저장소 공간이 있는 클라이언트 컴퓨터 또는 많은 양의 느린 네트워크 연결을 통해 데이터를 사용 하 여 작업할 때 특히 유용 합니다.  
  
 Just-in-time 시나리오에서 가상 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드 사용 하 여 가상 모드 구현](implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)합니다.  
  
## <a name="virtual-mode-events"></a>가상 모드 이벤트  
 데이터 읽기 전용 이면는 `CellValueNeeded` 이벤트 유일한 이벤트 처리 해야 할 수 있습니다. 추가 가상 모드 이벤트 사용자 편집, 행 추가 및 삭제 및 행 수준 트랜잭션을 같은 특정 기능을 사용 하도록 설정할 수 있습니다.  
  
 일부 표준 <xref:System.Windows.Forms.DataGridView> 이벤트 (예: 사용자 추가 또는 행을 삭제 하거나 값 셀 때 발생 하는 이벤트는 편집, 구문 분석, 유효성을 검사 하거나 형식)는 가상 모드에 유용 합니다. 또한 일반적으로 하지 셀 도구 설명 텍스트, 셀 및 행 오류 텍스트, 셀 및 행 바로 가기 메뉴 데이터 및 행 높이 데이터와 같은 바인딩된 데이터 원본에 저장 된 값을 유지 관리할 수 있도록 하는 이벤트를 처리할 수 있습니다.  
  
 행 수준 커밋 범위를 사용 하 여 읽기/쓰기 데이터를 관리 하기 위해 가상 모드 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [연습: Forms DataGridView 컨트롤의 Windows에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)합니다.  
  
 셀 수준 커밋 범위를 사용 하 여 가상 모드 구현 하는 예제를 참조 하세요.를 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성 참조 항목입니다.  
  
 다음 이벤트가 발생만 때 합니다 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성이 `true`합니다.  
  
|이벤트(event)|설명|  
|-----------|-----------------|  
|<xref:System.Windows.Forms.DataGridView.CellValueNeeded>|셀 값을 표시 하기 위해 데이터 캐시에서 검색할 컨트롤에서 사용 합니다. 이 이벤트는 바인딩되지 않은 열에서 셀에 대해서만 발생합니다.|  
|<xref:System.Windows.Forms.DataGridView.CellValuePushed>|데이터 캐시를 셀에 대 한 사용자 입력에 적용 하는 컨트롤에서 사용 합니다. 이 이벤트는 바인딩되지 않은 열에서 셀에 대해서만 발생합니다.<br /><br /> 호출 된 <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> 메서드 외부에서 캐시 된 값을 변경 하는 경우는 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 현재 값을 컨트롤에 표시 되는지 확인 하는 데 현재에서 유효한 자동 크기 조정 모드를 적용 하는 이벤트 처리기입니다.|  
|<xref:System.Windows.Forms.DataGridView.NewRowNeeded>|컨트롤에서 데이터 캐시에 새 행에 대 한 필요성을 나타내는 데 사용 합니다.|  
|<xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>|컨트롤 행에 커밋되지 않은 변경 내용이 있는지 여부를 결정 하기 위해 사용 합니다.|  
|<xref:System.Windows.Forms.DataGridView.CancelRowEdit>|컨트롤에서 행을 캐시 된 값으로 되돌려야 함을 나타내는 데 사용 합니다.|  
  
 다음 이벤트는 가상 모드에 유용 하지만 관계 없이 사용할 수는 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성을 설정 합니다.  
  
|이벤트|설명|  
|------------|-----------------|  
|<xref:System.Windows.Forms.DataGridView.UserDeletingRow><br /><br /> <xref:System.Windows.Forms.DataGridView.UserDeletedRow><br /><br /> <xref:System.Windows.Forms.DataGridView.RowsRemoved><br /><br /> <xref:System.Windows.Forms.DataGridView.RowsAdded>|행이 삭제 됩니다 또는 데이터 캐시를 적절 하 게 업데이트할 추가, 알려줄 때를 나타내는 컨트롤에서 사용 합니다.|  
|<xref:System.Windows.Forms.DataGridView.CellFormatting><br /><br /> <xref:System.Windows.Forms.DataGridView.CellParsing><br /><br /> <xref:System.Windows.Forms.DataGridView.CellValidating><br /><br /> <xref:System.Windows.Forms.DataGridView.CellValidated><br /><br /> <xref:System.Windows.Forms.DataGridView.RowValidating><br /><br /> <xref:System.Windows.Forms.DataGridView.RowValidated>|표시 및 구문 분석 하 고 사용자 입력의 유효성을 검사 하려면 셀 값의 형식 컨트롤에서 사용 합니다.|  
|<xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded>|컨트롤에서 셀 도구 설명 텍스트를 검색할 때 사용 때 합니다 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성을 설정 또는 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성은 `true`합니다.<br /><br /> 셀 도구 설명을 표시 되는 경우에만 합니다 <xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A> 속성 값이 `true`합니다.|  
|<xref:System.Windows.Forms.DataGridView.CellErrorTextNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowErrorTextNeeded>|컨트롤에서 셀 또는 행을 오류 텍스트를 검색할 때 사용 때 합니다 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성을 설정 또는 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성은 `true`합니다.<br /><br /> 호출 된 <xref:System.Windows.Forms.DataGridView.UpdateCellErrorText%2A> 메서드 또는 <xref:System.Windows.Forms.DataGridView.UpdateRowErrorText%2A> 메서드 현재 값을 컨트롤에 표시 되는지 확인 하려면 셀 또는 행을 오류 텍스트를 변경한 경우.<br /><br /> 셀 및 행 오류 문자 모양을 표시 됩니다 때 합니다 <xref:System.Windows.Forms.DataGridView.ShowCellErrors%2A> 하 고 <xref:System.Windows.Forms.DataGridView.ShowRowErrors%2A> 속성 값은 `true`합니다.|  
|<xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded>|컨트롤에서 셀 또는 행을 검색할 때 사용 <xref:System.Windows.Forms.ContextMenuStrip> 때 컨트롤 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성을 설정 또는 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성이 `true`합니다.|  
|<xref:System.Windows.Forms.DataGridView.RowHeightInfoNeeded><br /><br /> <xref:System.Windows.Forms.DataGridView.RowHeightInfoPushed>|컨트롤에서를 검색 하거나 데이터 캐시의 행 높이 정보를 저장 하는 데 사용 합니다. 호출 된 <xref:System.Windows.Forms.DataGridView.UpdateRowHeightInfo%2A> 메서드 외부의 캐시 된 행 높이 정보를 변경 하는 경우는 <xref:System.Windows.Forms.DataGridView.RowHeightInfoPushed> 이벤트 처리기를 현재 값을 컨트롤의 표시에 사용 되는지 확인 합니다.|  
  
## <a name="best-practices-in-virtual-mode"></a>가상 모드에 대 한 모범 사례  
 많은 양의 데이터를 효율적으로 사용 하기 위해 가상 모드를 구현 하는 경우 또한 하려는 작동 하는지 확인 하는 효율적으로 사용 하 여는 <xref:System.Windows.Forms.DataGridView> 컨트롤 자체입니다. 셀 스타일, 자동 크기 조정, 선택, 그리고 공유 하는 행의 효율적인 사용에 대 한 자세한 내용은 참조 [Windows Forms DataGridView 컨트롤의 크기 조정에 대 한 모범 사례](best-practices-for-scaling-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>
- [Windows Forms DataGridView 컨트롤의 성능 조정](performance-tuning-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기를 조정하는 최선의 방법](best-practices-for-scaling-the-windows-forms-datagridview-control.md)
- [연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤에서 Just-In-Time 데이터 로드를 사용하여 가상 모드 구현](implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)
