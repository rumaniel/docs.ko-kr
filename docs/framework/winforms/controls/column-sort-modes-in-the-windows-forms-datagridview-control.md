---
title: Windows Forms DataGridView 컨트롤의 열 정렬 모드
ms.date: 03/30/2017
helpviewer_keywords:
- data grids [Windows Forms], sort modes
- DataGridView control [Windows Forms], sort mode
ms.assetid: 43715887-2df9-4da7-bcf1-b9c7c842b2bf
ms.openlocfilehash: d0d743ccae38d101eda5bb9780b33ae18dfb608a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918458"
---
# <a name="column-sort-modes-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 열 정렬 모드
<xref:System.Windows.Forms.DataGridView>열에는 세 가지 정렬 모드가 있습니다. 각 열에 대 한 정렬 모드는 다음 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> <xref:System.Windows.Forms.DataGridViewColumnSortMode> 열거형 값 중 하나로 설정할 수 있는 열의 속성을 통해 지정 됩니다.  
  
|`DataGridViewColumnSortMode` 값|Description|  
|----------------------------------------|-----------------|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode.Automatic>|텍스트 상자 열에 대 한 기본값입니다. 열 머리글을 선택에 사용 하지 않으면 열 머리글을 클릭 하면 자동으로 <xref:System.Windows.Forms.DataGridView> 이 열을 기준으로 정렬 하 고 정렬 순서를 나타내는 문자 모양을 표시 합니다.|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode.NotSortable>|텍스트 상자 열이 아닌 열에 대 한 기본값입니다. 프로그래밍 방식으로이 열을 정렬할 수 있습니다. 그러나 정렬 하기 위한 것이 아니므로 정렬 문자를 위한 공간이 예약 되어 있지 않습니다.|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode.Programmatic>|이 열을 프로그래밍 방식으로 정렬할 수 있으며 공간은 정렬 문자 모양으로 예약 됩니다.|  
  
 의미 있는 순서를 지정할 수 있는 값이 포함 된 경우 기본적으로 <xref:System.Windows.Forms.DataGridViewColumnSortMode.NotSortable> 로 설정 된 열에 대 한 정렬 모드를 변경 하는 것이 좋습니다. 예를 들어 항목 상태를 나타내는 숫자가 포함 된 데이터베이스 열이 있는 경우 이미지 열을 데이터베이스 열에 바인딩하여 이러한 숫자를 해당 아이콘으로 표시할 수 있습니다. 그런 다음 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType> 이벤트 처리기에서 숫자 셀 값을 이미지 표시 값으로 변경할 수 있습니다. 이 경우 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 속성을로 <xref:System.Windows.Forms.DataGridViewColumnSortMode.Automatic> 설정 하면 사용자가 열을 정렬할 수 있습니다. 자동 정렬을 사용 하면 숫자에 해당 하는 상태에 자연 시퀀스가 없더라도 사용자가 동일한 상태의 항목을 그룹화 할 수 있습니다. 확인란 열은 동일한 상태의 항목을 그룹화 하는 데 자동 정렬이 유용한 또 다른 예입니다.  
  
 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 설정에 관계 없이 <xref:System.Windows.Forms.DataGridView> 모든 열 또는 여러 열의 값을 프로그래밍 방식으로 정렬할 수 있습니다. 프로그래밍 방식 정렬은 정렬에 고유한 UI (사용자 인터페이스)를 제공 하거나 사용자 지정 정렬을 구현 하려는 경우에 유용 합니다. 예를 들어 열 머리글 선택을 사용 하도록 <xref:System.Windows.Forms.DataGridView> 선택 모드를 설정 하는 경우 사용자 고유의 정렬 UI를 제공 하는 것이 유용 합니다. 이 경우 열 헤더를 정렬에 사용할 수는 없지만 헤더에서 적절 한 정렬 문자 모양을 표시 하려면 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 속성을로 <xref:System.Windows.Forms.DataGridViewColumnSortMode.Programmatic>설정 합니다.  
  
 프로그래밍 정렬 모드로 설정 된 열은 자동으로 정렬 문자 모양을 표시 하지 않습니다. 이러한 열에 대해 <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=nameWithType> 속성을 설정 하 여 문자 모양을 직접 표시 해야 합니다. 사용자 지정 정렬의 유연성을 원하는 경우이 작업이 필요 합니다. 예를 들어 여러 열을 기준 <xref:System.Windows.Forms.DataGridView> 으로 정렬 하는 경우 여러 정렬 문자 모양을 표시 하거나 정렬 문자 모양을 표시 하지 않을 수 있습니다.  
  
 모든 열을 프로그래밍 방식으로 <xref:System.Windows.Forms.DataGridView> 정렬할 수 있지만 단추 열과 같은 일부 열에는 의미 있는 순서를 지정할 수 있는 값이 포함 되지 않을 수 있습니다. 이러한 열의 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 속성 <xref:System.Windows.Forms.DataGridViewColumnSortMode.NotSortable> 설정은 정렬에 사용 되지 않음을 나타냅니다. 따라서 정렬 문자 모양에 대 한 헤더에 공간을 예약할 필요가 없습니다.  
  
 을 <xref:System.Windows.Forms.DataGridView> 정렬할 때 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> 및 <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 속성의 값을 확인 하 여 정렬 열과 정렬 순서를 모두 확인할 수 있습니다. 이러한 값은 사용자 지정 정렬 작업 후에는 의미가 없습니다. 사용자 지정 정렬에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 사용자 지정 정렬 섹션을 참조 하십시오.  
  
 바인딩된 열과 바인딩되지 않은 열을 모두 포함 하는 컨트롤을정렬하는경우바인딩되지않은열의값은자동으로유지관리할수없습니다.<xref:System.Windows.Forms.DataGridView> 이러한 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 값을 유지 하려면 속성을로 `true` 설정 하 고 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 및 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 이벤트를 처리 하 여 가상 모드를 구현 해야 합니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤](how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)에서 가상 모드를 구현 합니다. 바인딩된 모드로 바인딩되지 않은 열을 기준으로 정렬 하는 것은 지원 되지 않습니다.  
  
## <a name="programmatic-sorting"></a>프로그래밍 방식 정렬  
 메서드<xref:System.Windows.Forms.DataGridView.Sort%2A> 를 호출 하 <xref:System.Windows.Forms.DataGridView> 여 프로그래밍 방식으로를 정렬할 수 있습니다.  
  
 메서드의 오버 로드 <xref:System.Windows.Forms.DataGridViewColumn> 는 및 열거형값을매개변수로사용합니다.<xref:System.ComponentModel.ListSortDirection> `Sort(DataGridViewColumn,ListSortDirection)` <xref:System.Windows.Forms.DataGridView.Sort%2A> 이 오버 로드는 의미 있는 순서를 지정할 수 있는 값이 있는 열을 기준으로 정렬 하는 경우에 유용 하지만 자동 정렬에 대해서는 구성 하지 않습니다. 이 오버 로드를 호출 하 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> 고 속성 <xref:System.Windows.Forms.DataGridViewColumnSortMode.Automatic?displayProperty=nameWithType>값 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> 이 인 열을 전달 하면 및 <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 속성이 자동으로 설정 되 고 열 머리글에 적절 한 정렬 문자 모양이 표시 됩니다.  
  
> [!NOTE]
> 속성을 설정 하 여 <xref:System.Windows.Forms.DataGridView> 컨트롤이 외부 데이터 원본에 바인딩되면 바인딩되지 않은 열에 대해 메서드오버로드가작동하지않습니다.`Sort(DataGridViewColumn,ListSortDirection)` <xref:System.Windows.Forms.DataGridView.DataSource%2A> 또한 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성이 인 `true`경우 바인딩된 열에 대해서만이 오버 로드를 호출할 수 있습니다. 열이 데이터 바인딩 되었는지 여부를 확인 하려면 <xref:System.Windows.Forms.DataGridViewColumn.IsDataBound%2A> 속성 값을 확인 합니다. 바인딩 모드에서 바인딩되지 않은 열 정렬은 지원 되지 않습니다.  
  
## <a name="custom-sorting"></a>사용자 지정 정렬  
 메서드의 오버 로드 <xref:System.Windows.Forms.DataGridView> `Sort(IComparer)` 를 사용 하거나 이벤트를 <xref:System.Windows.Forms.DataGridView.SortCompare> 처리 하 여 사용자 지정할 수 있습니다. <xref:System.Windows.Forms.DataGridView.Sort%2A>  
  
 메서드 `Sort(IComparer)` 오버 로드는 인터페이스를 <xref:System.Collections.IComparer> 매개 변수로 구현 하는 클래스의 인스턴스를 사용 합니다. 이 오버 로드는 사용자 지정 정렬을 제공 하려는 경우에 유용 합니다. 예를 들어 열에 있는 값에 자연 정렬 순서가 없거나 자연 정렬 순서가 부적절 한 경우입니다. 이 경우 자동 정렬을 사용할 수 없지만 열 머리글을 클릭 하 여 사용자가 정렬 하도록 할 수도 있습니다. 선택 영역에 열 머리글을 사용 하지 않는 경우 <xref:System.Windows.Forms.DataGridView.ColumnHeaderMouseClick> 이벤트 처리기에서이 오버 로드를 호출할 수 있습니다.  
  
> [!NOTE]
> 메서드 `Sort(IComparer)` 오버 로드는 <xref:System.Windows.Forms.DataGridView> 컨트롤이 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 외부 데이터 소스에 바인딩되지 않고 속성 값이 인 `false`경우에만 작동 합니다. 외부 데이터 원본에 바인딩된 열의 정렬을 사용자 지정 하려면 데이터 원본에서 제공 하는 정렬 작업을 사용 해야 합니다. 가상 모드에서는 바인딩되지 않은 열에 대 한 고유한 정렬 작업을 제공 해야 합니다.  
  
 `Sort(IComparer)` 메서드 오버 로드를 사용 하려면 <xref:System.Collections.IComparer> 인터페이스를 구현 하는 고유한 클래스를 만들어야 합니다. 이 인터페이스를 사용 하려면 클래스에서 메서드 <xref:System.Collections.IComparer.Compare%2A?displayProperty=nameWithType> 를 구현 해야 합니다 <xref:System.Windows.Forms.DataGridView> .이 <xref:System.Windows.Forms.DataGridViewRow> 메서드는 `Sort(IComparer)` 메서드 오버 로드를 호출할 때가 개체를 입력으로 전달 합니다. 이를 통해 모든 열의 값을 기준으로 올바른 행 순서를 계산할 수 있습니다.  
  
 메서드 `Sort(IComparer)` 오버 로드는 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> <xref:System.Windows.Forms.DataGridView.SortOrder%2A> 및<xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=nameWithType> 속성을 설정 하지 않으므로 항상 속성을 설정 하 여 정렬 문자 모양을 표시 해야 합니다.  
  
 `Sort(IComparer)` 메서드 오버 로드에 대 한 대 안으로, <xref:System.Windows.Forms.DataGridView.SortCompare> 이벤트에 대 한 처리기를 구현 하 여 사용자 지정 정렬을 제공할 수 있습니다. 이 이벤트는 사용자가 자동 정렬을 위해 구성 된 열의 머리글을 클릭 하거나 `Sort(DataGridViewColumn,ListSortDirection)` <xref:System.Windows.Forms.DataGridView.Sort%2A> 메서드의 오버 로드를 호출할 때 발생 합니다. 이 이벤트는 컨트롤의 각 행 쌍에 대해 발생 하므로 올바른 순서를 계산할 수 있습니다.  
  
> [!NOTE]
> 속성이 설정 되거나 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 속성 값이 인 `true`경우 이벤트가발생하지않습니다.<xref:System.Windows.Forms.DataGridView.SortCompare> <xref:System.Windows.Forms.DataGridView.DataSource%2A>  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.Sort%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.SortedColumn%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.SortOrder%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 데이터 정렬](sorting-data-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤의 열에 대 한 정렬 모드 설정](set-the-sort-modes-for-columns-wf-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 정렬 사용자 지정](how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)
