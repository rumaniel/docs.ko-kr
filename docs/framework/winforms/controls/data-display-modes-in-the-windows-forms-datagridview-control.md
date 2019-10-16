---
title: Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], display modes
- data grids [Windows Forms], display modes
- DataGridView control [Windows Forms], display modes
ms.assetid: 9755a030-3f3f-4705-a661-ba5a48a81875
ms.openlocfilehash: 673780909f6d66168548893e99d79bbfec70a0e0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62011434"
---
# <a name="data-display-modes-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드
<xref:System.Windows.Forms.DataGridView> 세 가지 모드로 컨트롤 데이터를 표시할 수 있습니다: 바인딩, 바인딩 해제 됨 및 가상. 요구 사항에 따라 가장 적합 한 모드를 선택 합니다.  
  
## <a name="unbound"></a>바인딩 해제  
 바인딩되지 않은 모드는 상대적으로 적은 양의 프로그래밍 방식으로 관리 하는 데이터를 표시 하기 위한 적합 합니다. 연결 하지 않는 것을 <xref:System.Windows.Forms.DataGridView> 바인딩된 모드와 같이 데이터 원본에 직접 제어 합니다. 대신 채워야 컨트롤을 직접 일반적으로 사용 하 여를 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A?displayProperty=nameWithType> 메서드.  
  
 바인딩되지 않은 모드는 정적, 읽기 전용 데이터 또는 외부 데이터 저장소와 상호 작용 하는 사용자 고유의 코드를 제공 하려는 경우에 특히 유용할 수 있습니다. 그러나 사용자가 외부 데이터 원본을 사용 하 여 상호 작용할 때, 일반적으로 사용 바인딩된 모드입니다.  
  
 읽기 전용을 사용 하는 예제에 대 한 언바운드 <xref:System.Windows.Forms.DataGridView>를 참조 하세요 [방법: 바인딩되지 않은 Windows Forms DataGridView 컨트롤 만들기](how-to-create-an-unbound-windows-forms-datagridview-control.md)합니다.  
  
## <a name="bound"></a>바인딩된  
 바인딩된 모드는 자동 상호 데이터 저장소를 사용 하 여 데이터를 관리 하기 위한 적합 합니다. 연결할 수 있습니다 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤을 설정 하 여 해당 데이터 원본에 직접는 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성입니다. 데이터 바인딩된 컨트롤을 사용 하는 경우 데이터 행을 푸시하고 사용자의 명시적 관리 하지 않아도 됩니다. 경우는 <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A> 속성은 `true`, 데이터 원본에 각 열에는 해당 컨트롤에서 만들어야 하는 열 하면 합니다. 사용자 자신의 열 만들기를 원하는 경우이 속성을 설정할 수 있습니다 `false` 사용 하 여는 <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A> 속성을 구성할 때 각 열을 바인딩합니다. 기본적으로 생성 되는 형식 이외의 열 형식을 사용 하려는 경우에 유용 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)합니다.  
  
 범위를 사용 하는 예제에 대 한 <xref:System.Windows.Forms.DataGridView> 제어 내용은 [연습: Forms DataGridView 컨트롤을 Windows의 데이터 유효성 검사](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)합니다.  
  
 바인딩되지 않은 열을 추가할 수도 있습니다는 <xref:System.Windows.Forms.DataGridView> 바인딩된 모드에서 제어 합니다. 특정 행에서 작업을 수행할 수 있는 단추 또는 링크의 열을 표시 하려는 경우에 유용 합니다. 바인딩된 열에서 계산 된 값을 사용 하 여 열을 표시 하는 것이 유용 합니다. 에 대 한 처리기에서 계산 된 열에 대 한 셀 값을 채울 수 있습니다는 <xref:System.Windows.Forms.DataGridView.CellFormatting> 이벤트입니다. 그러나 사용 중인 경우를 <xref:System.Data.DataSet> 또는 <xref:System.Data.DataTable> 데이터 원본으로 하려는 사용를 <xref:System.Data.DataColumn.Expression%2A?displayProperty=nameWithType> 속성을 대신 계산된 열을 만듭니다. 이 경우에 <xref:System.Windows.Forms.DataGridView> 컨트롤은 데이터 원본에 다른 열과 마찬가지로 계산된 열을 처리 합니다.  
  
 바인딩된 모드로 바인딩되지 않은 열을 기준으로 정렬 하는 것은 지원 되지 않습니다. 사용자가 편집 가능한 값을 포함 하는 바인딩된 모드에 바인딩되지 않은 열을 만들면 컨트롤은 바인딩된 열을 정렬할 때 이러한 값을 유지 하려면 가상 모드를 구현 해야 합니다.  
  
## <a name="virtual"></a>가상  
 가상 모드를 사용 하 여 사용자 고유의 데이터 관리 작업을 구현할 수 있습니다. 이 컨트롤이 바인딩된 열을 기준으로 정렬 될 때 바인딩된 모드로 바인딩되지 않은 열 값을 유지 해야 합니다. 가상 모드의 주된 용도 것 인데, 성능을 최적화 하기 위해 많은 양의 데이터와 상호 작용할 때.  
  
 연결 하는 <xref:System.Windows.Forms.DataGridView> 캐시를 관리 하는 컨트롤 및 데이터 행을 푸시하고 때 코드 컨트롤입니다. 메모리 사용 공간을 작게 유지 하기 위해 캐시 비슷해야 크기가 현재 표시 된 행의 수입니다. 보기에 새 행을 스크롤 하는 사용자, 코드는 캐시에서 새 데이터를 요청 하 고 필요에 따라 메모리에서 이전 데이터를 플러시합니다.  
  
 가상 모드 구현 하는 경우에 새 행을 필요한 경우 데이터 모델 및 롤백 새 행을 추가 해야 하는 경우 추적 해야 합니다. 이 기능의 정확한 구현은 데이터 모델을 구현 하 고 데이터 모델의 트랜잭션 의미 체계에 따라 달라 집니다. 셀 또는 행 수준에서 커밋 범위 인지 여부입니다.  
  
 가상 모드에 대 한 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤에서 가상 모드](virtual-mode-in-the-windows-forms-datagridview-control.md)합니다. 가상 모드 이벤트를 사용 하는 방법을 보여 주는 예제를 참조 하세요. [연습: Forms DataGridView 컨트롤의 Windows에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.VirtualMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)
- [연습: 만들기는 바인딩되지 않은 Windows Forms DataGridView 컨트롤](walkthrough-creating-an-unbound-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에 데이터 바인딩](how-to-bind-data-to-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 가상 모드](virtual-mode-in-the-windows-forms-datagridview-control.md)
- [연습: Windows Forms DataGridView 컨트롤에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)
