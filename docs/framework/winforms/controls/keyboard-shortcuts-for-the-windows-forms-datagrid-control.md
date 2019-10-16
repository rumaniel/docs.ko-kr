---
title: Windows Forms DataGrid 컨트롤을 위한 바로 가기 키
ms.date: 03/30/2017
helpviewer_keywords:
- keyboard shortcuts [Windows Forms], DataGrid control
- DataGrid control [Windows Forms], navigation keys
ms.assetid: a01780f9-20d5-4f5f-808f-c790c9a007a5
ms.openlocfilehash: 6b4d566d377a3cda73bf8422caa798134d356f63
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962577"
---
# <a name="keyboard-shortcuts-for-the-windows-forms-datagrid-control"></a>Windows Forms DataGrid 컨트롤을 위한 바로 가기 키
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 다음 표에서는 Windows Forms <xref:System.Windows.Forms.DataGrid> 컨트롤 내에서 탐색 하는 데 사용할 수 있는 바로 가기 키를 나열 합니다.  
  
|작업|바로 가기|  
|------------|--------------|  
|셀 항목을 완성 하 고 다음 셀로 이동 합니다.<br /><br /> 포커스가 자식 테이블 링크에 있으면 해당 테이블로 이동 합니다.|Enter 키|  
|셀 편집 모드에 있는 경우 셀 편집을 취소 합니다.<br /><br /> 선택 윤곽이 선택 된 경우 행에 대 한 편집을 취소 합니다.|Esc|  
|셀을 편집할 때 삽입 지점 앞의 문자를 삭제 합니다.|백스페이스|  
|셀을 편집할 때 삽입 지점 뒤의 문자를 삭제 합니다.|DELETE|  
|현재 행의 첫 번째 셀로 이동 합니다.|홈|  
|현재 행의 마지막 셀로 이동 합니다.|END|  
|현재 셀에서 문자를 강조 표시 하 고 줄의 끝에 삽입 지점을 배치 합니다. 셀을 두 번 클릭 하는 것과 동일한 동작입니다.|F2|  
|포커스가 셀에 있는 경우 행의 다음 셀로 이동 합니다.<br /><br /> 포커스가 행의 마지막 셀에 있으면 행의 첫 번째 자식 테이블 링크로 이동 하 여 확장 합니다.<br /><br /> 포커스가 자식 링크에 있으면 다음 자식 링크로 이동 합니다.<br /><br /> 포커스가 마지막 자식 링크에 있는 경우 다음 행의 첫 번째 셀로 이동 합니다.|Tab|  
|포커스가 셀에 있는 경우 행의 이전 셀로 이동 합니다.<br /><br /> 포커스가 행의 첫 번째 셀에 있으면 이전 행의 마지막으로 확장 된 자식 테이블 링크로 이동 하거나 이전 행의 마지막 셀로 이동 합니다.<br /><br /> 포커스가 자식 링크에 있으면 이전 자식 링크로 이동 합니다.<br /><br /> 포커스가 첫 번째 자식 링크에 있으면 이전 행의 마지막 셀로 이동 합니다.|Shift+Tab|  
|탭 순서에서 다음 컨트롤로 이동 합니다.|Ctrl+Tab|  
|탭 순서에서 이전 컨트롤로 이동 합니다.|Ctrl+Shift+Tab|  
|자식 테이블에 있는 경우 부모 테이블로 이동 합니다. 뒤로 단추를 클릭 하는 것과 동일한 동작입니다.|Alt+왼쪽 화살표|  
|자식 테이블 링크를 확장 합니다. ALT + 아래쪽 화살표는 선택한 항목만이 아니라 모든 링크를 확장 합니다.|ALT + 아래쪽 화살표 또는 CTRL + 더하기 기호|  
|자식 테이블 링크를 축소 합니다. ALT + 위쪽 화살표는 선택한 항목만이 아니라 모든 링크를 축소 합니다.|ALT + 위쪽 화살표 또는 CTRL + 빼기 기호|  
|화살표가 있는 가장 멀리 떨어진 셀로 이동 합니다.|CTRL + 화살표|  
|하위 테이블 링크를 제외 하 고 화살표 방향으로 한 행씩 선택 영역을 확장 합니다.|SHIFT + 위쪽/아래쪽 화살표|  
|화살표 (자식 테이블 링크 제외)의 방향으로 가장 멀리 있는 비어 있지 않은 행으로 선택을 확장 합니다.|CTRL + SHIFT + 위쪽 화살표/아래쪽 화살표|  
|왼쪽 위 셀로 이동 합니다.|Ctrl+Home|  
|오른쪽 아래 셀로 이동 합니다.|Ctrl+End|  
|선택 영역을 맨 위 행으로 확장 합니다.|Ctrl+Shift+Home|  
|선택 영역을 아래쪽 행으로 확장 합니다.|Ctrl+Shift+End|  
|현재 행 (자식 테이블 링크 제외)을 선택 합니다.|SHIFT + 스페이스바|  
|전체 그리드 (자식 테이블 링크 제외)를 선택 합니다.|Ctrl+A|  
|부모 행을 자식 테이블에 표시 합니다.|Ctrl+Page Down|  
|자식 테이블에서 부모 행을 숨깁니다.|Ctrl+Page Up|  
|자식 테이블 링크를 제외 하 고 한 화면 아래로 선택 영역을 확장 합니다.|Shift+Page Down|  
|자식 테이블 링크를 제외 하 고 한 화면 위로 선택 영역을 확장 합니다.|Shift+Page Up|  
|현재 행 <xref:System.Windows.Forms.DataGrid.EndEdit%2A> 에 대해 메서드를 호출 합니다.|Ctrl+Enter|  
|편집 모드 <xref:System.DBNull.Value?displayProperty=nameWithType> 에 있을 때 셀에 값을 입력 합니다.|Ctrl+0|  
  
## <a name="see-also"></a>참고자료

- [DataGrid 컨트롤 개요](datagrid-control-overview-windows-forms.md)
- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
