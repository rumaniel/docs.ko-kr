---
title: Windows Forms DataGridView 컨트롤의 크기 조정에 대한 모범 사례
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], row sharing
- data grids [Windows Forms], best practices
- DataGridView control [Windows Forms], shared rows
- DataGridView control [Windows Forms], best practices
- best practices [Windows Forms], dataGridView control
- DataGridView control [Windows Forms], scaling
ms.assetid: 8321a8a6-6340-4fd1-b475-fa090b905aaf
ms.openlocfilehash: 65afd73c166332f08003c3b3bfcc70e488d0373a
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663549"
---
# <a name="best-practices-for-scaling-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 크기 조정에 대한 모범 사례

<xref:System.Windows.Forms.DataGridView> 컨트롤은 최대 확장성을 제공 하도록 설계 되었습니다. 많은 양의 데이터를 표시 해야 할 경우 많은 양의 메모리를 소비 하거나 (UI) 사용자 인터페이스의 응답성을 저하 시 키 지 않으려면이 항목에 설명 된 지침을 따라야 합니다. 이 항목에서는 다음과 같은 문제를 설명합니다.

- 셀 스타일을 효율적으로 사용

- 바로 가기 메뉴를 효율적으로 사용

- 효율적으로 자동 크기 조정 사용

- 선택한 셀, 행 및 열 컬렉션을 효율적으로 사용

- 공유 행 사용

- 행의 공유가 해제 차단

특별 한 성능 요구 사항에 있는 경우에 가상 모드 구현 하 고 고유한 데이터 관리 작업을 제공할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드](data-display-modes-in-the-windows-forms-datagridview-control.md)합니다.

## <a name="using-cell-styles-efficiently"></a>셀 스타일을 효율적으로 사용

각 셀, 행 및 열에는 자체 스타일 정보를 가질 수 있습니다. 스타일 정보에 저장 됩니다 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체입니다. 여러 개인에 대 한 셀 스타일 개체를 만드는 <xref:System.Windows.Forms.DataGridView> 많은 양의 데이터를 사용 하는 경우에 특히 요소 비효율적일 수 있습니다. 성능에 영향을 방지 하려면 다음 지침을 따르십시오.

- 개별 셀 스타일 속성을 설정 하지 마세요 <xref:System.Windows.Forms.DataGridViewCell> 또는 <xref:System.Windows.Forms.DataGridViewRow> 개체입니다. 여기에 지정 된 행 개체를 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 속성입니다. 행 템플릿을 복제는 각 새 행 템플릿의 셀 스타일 개체의 자체 복사본을 받게 됩니다. 최대 확장성을 위해 아래에 있는 셀 스타일 속성을 설정 합니다 <xref:System.Windows.Forms.DataGridView> 수준입니다. 예를 들어 설정 된 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType> 속성 대신 <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType> 속성입니다.

- 일부 셀에 기본 서식 이외의 형식에 필요한 경우 사용 하 여 동일한 <xref:System.Windows.Forms.DataGridViewCellStyle> 셀, 행 또는 열 그룹에서 인스턴스. 직접 형식의 속성을 설정 하지 마십시오 <xref:System.Windows.Forms.DataGridViewCellStyle> 개별 셀, 행 및 열에 있습니다. 셀 스타일 공유의 예제를 참조 하세요. [방법: Windows Forms DataGridView 컨트롤에 기본 셀 스타일 설정](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)합니다. 셀 스타일을 개별적으로 처리 하 여 설정 하는 경우 성능 저하를 방지할 수도 있습니다는 <xref:System.Windows.Forms.DataGridView.CellFormatting> 이벤트 처리기입니다. 예는 [방법: Windows Forms DataGridView 컨트롤에서 데이터 형식 사용자 지정](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)합니다.

- 셀의 스타일을 결정 하는 경우 사용 합니다 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=nameWithType> 속성 대신 <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType> 속성입니다. 에 액세스 하는 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 속성의 새 인스턴스를 만듭니다는 <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스 속성에 이미 사용 하지 않은 경우. 또한이 개체 일부 스타일은 행, 열 또는 컨트롤에서 상속 하는 경우에 하지 셀에 대 한 전체 스타일 정보를 포함할 수 있습니다. 셀 스타일 상속에 대 한 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.

## <a name="using-shortcut-menus-efficiently"></a>바로 가기 메뉴를 효율적으로 사용

각 셀, 행 및 열에는 자체 바로 가기 메뉴를 가질 수 있습니다. 바로 가기 메뉴에는 <xref:System.Windows.Forms.DataGridView> 컨트롤이 표시 됩니다 <xref:System.Windows.Forms.ContextMenuStrip> 컨트롤입니다. 셀 스타일 개체의 경우와 마찬가지로 여러 개인에 대 한 바로 가기 메뉴를 만드는 <xref:System.Windows.Forms.DataGridView> 요소 성능이 저하 됩니다. 이러한 성능 저하를 방지 하려면 다음 지침을 따르십시오.

- 개별 셀 및 행에 대 한 바로 가기 메뉴를 만들지 마세요. 컨트롤에 새 행이 추가 되 면 해당 바로 가기 메뉴와 함께 복제 되는 행 템플릿을 포함 합니다. 최대 확장성을 위해만: 컨트롤을 사용 하 여 <xref:System.Windows.Forms.Control.ContextMenuStrip%2A> 전체 컨트롤에 대 한 단일 바로 가기 메뉴를 지정 하는 속성입니다.

- 여러 행 또는 셀에 대 한 여러 바로 가기 메뉴를 해야 하는 경우를 처리 합니다 <xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded> 또는 <xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded> 이벤트입니다. 이러한 이벤트를 통해 하 바로 가기 메뉴 개체를 관리할 수 있습니다. 직접 성능을 조정할 수 있습니다.

## <a name="using-automatic-resizing-efficiently"></a>효율적으로 자동 크기 조정 사용

행, 열 및 머리글 자동으로 크기를 조정할 수 셀 내용 변경으로 클리핑 없이 셀의 전체 내용이 표시 되도록 합니다. 크기 조정 모드를 변경 크기를 조정할 수도 행, 열 및 헤더입니다. 올바른 크기를 결정 하는 <xref:System.Windows.Forms.DataGridView> 컨트롤 수용 해야 하는 각 셀의 값을 검사 해야 합니다. 큰 데이터 집합을 사용 하 여 작업을이 분석 자동 크기 조정이 발생할 때 컨트롤의 성능을 저하 될 수 있습니다. 성능 저하를 방지 하려면 다음 지침을 사용 합니다.

- 자동 크기 조정에 사용 하지 마십시오는 <xref:System.Windows.Forms.DataGridView> 대량의 행 집합을 사용 하 여 제어 합니다. 자동 크기 조정, 표시 된 행을 기반으로 크기 조정에만 사용 않으면. 가상 모드에 표시 된 행만을 사용 합니다.

  - 행 및 열에 대 한 사용 합니다 `DisplayedCells` 또는 `DisplayedCellsExceptHeaders` 필드를 <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>, <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>, 및 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> 열거형입니다.

  - 행 머리글을 사용 합니다 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode.AutoSizeToDisplayedHeaders> 또는 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode.AutoSizeToFirstHeader> 필드를 <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode> 열거형.

- 최대 확장성을 위해 자동 크기 조정 전원을 끄고 프로그래밍 방식으로 크기 조정을 사용 합니다.

자세한 내용은 [Windows Forms DataGridView 컨트롤의 크기 조정 옵션](sizing-options-in-the-windows-forms-datagridview-control.md)합니다.

## <a name="using-the-selected-cells-rows-and-columns-collections-efficiently"></a>선택한 셀, 행 및 열 컬렉션의 효율적인 사용

<xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 큰 선택 항목을 사용 하 여 컬렉션을 효율적으로 수행 하지 않습니다. <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 하 고 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 컬렉션도 비효율적일 수 있습니다, 낮은 수준에 있지만 일반적인 셀 보다 더 적은 행 수 있기 때문에 <xref:System.Windows.Forms.DataGridView> 컨트롤과 행 보다 더 적은 열이 많습니다. 이러한 컬렉션을 사용 하 여 작업할 때 성능 저하를 방지 하려면 다음 지침을 사용 합니다.

- 결정할 여부를 모든 셀에는 <xref:System.Windows.Forms.DataGridView> 의 내용에 액세스 하기 전에 선택한를 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 컬렉션의 반환 값을 확인 합니다 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A> 메서드. 그러나 Note,이 메서드 공유가 행을 발생할 수 있습니다. 자세한 내용은 다음 단원을 참조하세요.

- 사용 하지 않도록 합니다 <xref:System.Collections.ICollection.Count%2A> 의 속성은 <xref:System.Windows.Forms.DataGridViewSelectedCellCollection?displayProperty=nameWithType> 선택된 된 셀의 수를 확인 하려면. 대신 합니다 <xref:System.Windows.Forms.DataGridView.GetCellCount%2A?displayProperty=nameWithType> 메서드를 전달 합니다 <xref:System.Windows.Forms.DataGridViewElementStates.Selected?displayProperty=nameWithType> 값. 마찬가지로, 사용 된 <xref:System.Windows.Forms.DataGridViewRowCollection.GetRowCount%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Forms.DataGridViewColumnCollection.GetColumnCount%2A?displayProperty=nameWithType> 선택한 행 및 열 컬렉션에 액세스 하는 것이 아니라 선택한 요소 수를 결정 하는 방법입니다.

- 셀 기반 선택 모드를 방지 합니다. 대신, 설정 된 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType> 속성을 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect?displayProperty=nameWithType>합니다.

## <a name="using-shared-rows"></a>행 공유 사용

효율적인 메모리 사용에 이루어집니다는 <xref:System.Windows.Forms.DataGridView> 공유 행을 제어 합니다. 행의 인스턴스를 공유 하 여 해당 모양 및 동작에 대 한 최대한 많은 정보를 공유는 <xref:System.Windows.Forms.DataGridViewRow> 클래스입니다.

행 인스턴스를 공유 메모리를 저장 하는 동안 행 쉽게 공유 될 수 있습니다. 예를 들어, 사용자가 직접 셀에 때마다 해당 행 공유는 해제 됩니다. 이 피할 수 없는, 때문에 매우 많은 양의 데이터를 사용 하는 경우에 하 고 사용자가 프로그램을 실행할 때마다 비교적 작은 부분 데이터 상호 작용 하는 경우에이 항목의 지침은 유용 합니다.

행을 공유할 수 없는에 바인딩되지 않은 <xref:System.Windows.Forms.DataGridView> 셀의 값이 포함 된 경우를 제어 합니다. 경우는 <xref:System.Windows.Forms.DataGridView> 컨트롤 외부 데이터 원본에 바인딩되어 있거나 셀 값 행을 공유할 수 있도록 하는 개체를 셀 대신 컨트롤 외부에 저장 됩니다 가상 모드를 구현 하 고 고유한 데이터 원본을 제공 하는 경우.

행 개체를 행의 상태 및 셀이 들어 있는 열의 상태에서 모든 셀의 상태를 확인할 수 있습니다 하는 경우에 공유할 수 있습니다. 수 더 이상 해당 행과 열의 상태에서 확인할 수 있도록 셀의 상태를 변경 하는 경우에 행을 공유할 수 없습니다.

예를 들어, 다음 상황에 행을 공유할 수 없습니다.

- 행 선택 된 열에 없는 단일 선택한 셀을 포함 합니다.

- 행에 들어 있는 셀과 해당 <xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A> 또는 <xref:System.Windows.Forms.DataGridViewCell.ContextMenuStrip%2A> 속성 집합입니다.

- 이 행에는 <xref:System.Windows.Forms.DataGridViewComboBoxCell> 사용 하 여 해당 <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A> 속성 집합입니다.

바인딩된 모드 또는 가상 모드에서 제공할 수 있습니다 도구 설명 및 바로 가기 메뉴 개별 셀에 대 한 처리를 <xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded> 및 <xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded> 이벤트입니다.

합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤에 행이 추가 될 때마다 공유 행을 사용 하려고 자동으로 <xref:System.Windows.Forms.DataGridViewRowCollection>합니다. 행이 공유 되도록 다음 지침을 따르세요.

- 호출 하지는 `Add(Object[])` 오버 로드는 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> 메서드 및 `Insert(Object[])` 오버 로드는 <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> 메서드를 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType> 컬렉션입니다. 이러한 오버 로드는 자동으로 공유 되지 않는 행을 만듭니다.

- 해야에 지정 된 행을 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=nameWithType> 같은 경우에 속성을 공유할 수 있습니다.

  - 호출 하는 경우는 `Add()` 또는 `Add(Int32)` 오버 로드는 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> 메서드 또는 `Insert(Int32,Int32)` 오버 로드는 <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> 메서드의 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType> 컬렉션입니다.

  - 값을 증가 하는 경우는 <xref:System.Windows.Forms.DataGridView.RowCount%2A?displayProperty=nameWithType> 속성입니다.

  - 설정 하는 경우는 <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=nameWithType> 속성입니다.

- 해야 하는 지정 된 행을 `indexSource` 를 호출할 때 매개 변수를 공유할 수 있습니다를 <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopy%2A>, 및 <xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopies%2A> 의 메서드를 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType> 컬렉션입니다.

- 호출 하는 경우 지정 된 행 수 공유 해야 합니다 `Add(DataGridViewRow)` 오버 로드는 <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A> 메서드를를 <xref:System.Windows.Forms.DataGridViewRowCollection.AddRange%2A> 메서드를를 `Insert(Int32,DataGridViewRow)` 오버 로드는 <xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A> 메서드를 및 <xref:System.Windows.Forms.DataGridViewRowCollection.InsertRange%2A> 메서드의 합니다 <xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType>컬렉션입니다.

행 공유 되는지 여부를 확인 하려면 사용 합니다 <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=nameWithType> 행 개체를 검색 한 다음 개체의 메서드 <xref:System.Windows.Forms.DataGridViewBand.Index%2A> 속성입니다. 공유 행 갖습니다는 <xref:System.Windows.Forms.DataGridViewBand.Index%2A> 속성 값-1입니다.

## <a name="preventing-rows-from-becoming-unshared"></a>행의 공유가 해제 차단

공유 행 코드 또는 사용자 작업의 결과로 공유 해제 될 수 있습니다. 성능에 영향을 방지 하려면 행의 공유가 피해 야 합니다. 응용 프로그램 개발 하는 동안 처리할 수 있습니다는 <xref:System.Windows.Forms.DataGridView.RowUnshared> 행의 공유가 결정 하는 이벤트입니다. 행 공유 문제를 디버그할 때 유용 합니다.

행의 공유가 해제를 방지 하려면 다음 지침을 따르십시오.

- 인덱싱을 방지 합니다 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션 또는 사용 하 여 반복을 `foreach` 루프입니다. 일반적으로 행에 직접 액세스 해야 하지 않습니다. <xref:System.Windows.Forms.DataGridView> 행에서 작동 하는 메서드는 행 인스턴스를 사용 하지 않고 행 인덱스 인수를 사용 합니다. 또한 행 관련 이벤트에 대 한 처리기 공유가 하지 않고 행을 조작 하는 데 사용할 수 있는 행 속성을 사용 하 여 이벤트 인수 개체를 표시 합니다.

- 사용 하 여 행 개체에 액세스 해야 할 경우는 <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=nameWithType> 메서드 및 실제 행의 인덱스를 전달 합니다. 그러나 Note,이 메서드를 통해 검색 하는 공유 행 개체를 수정 합니다.이 개체를 공유 하는 모든 행 수정 됩니다. 하지만 새 레코드에 대 한 행와 공유 되지 다른 행 다른 행을 수정 하는 경우 영향 수 있도록 합니다. 또한 note는 공유 행으로 표시 하는 다른 행에 다른 바로 가기 메뉴 있을 수 있습니다. 해당 바로 가기 메뉴는 공유 행 인스턴스에서를 검색 하려면 사용 된 <xref:System.Windows.Forms.DataGridViewRow.GetContextMenuStrip%2A> 메서드 및 실제 행의 인덱스를 전달 합니다. 공유 행에 액세스할 경우 <xref:System.Windows.Forms.DataGridViewRow.ContextMenuStrip%2A> 속성 대신는-1의 공유 행 인덱스를 사용 하 고 해당 바로 가기 메뉴를 검색 하지 것입니다.

- 인덱싱을 방지는 <xref:System.Windows.Forms.DataGridViewRow.Cells%2A?displayProperty=nameWithType> 컬렉션입니다. 새 공유가 해제 되 고 부모 행의 셀에 직접 액세스 하면 <xref:System.Windows.Forms.DataGridViewRow>합니다. 셀 관련 이벤트 처리기는 행 공유가 발생 하지 않고 셀을 조작 하는 데 사용할 수 있는 셀 속성을 사용 하 여 이벤트 인수 개체를 받습니다. 사용할 수도 있습니다는 <xref:System.Windows.Forms.DataGridView.CurrentCellAddress%2A> 셀에 직접 액세스 하지 않고 현재 셀의 행 및 열 인덱스를 검색할 속성입니다.

- 셀 기반 선택 모드를 방지 합니다. 이러한 모드 하면 행이 공유 되지 않게 됩니다. 대신, 설정 된 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType> 속성을 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect?displayProperty=nameWithType>합니다.

- 처리 하지 않는 합니다 <xref:System.Windows.Forms.DataGridViewRowCollection.CollectionChanged?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.DataGridView.RowStateChanged?displayProperty=nameWithType> 이벤트입니다. 이러한 이벤트 하면 행이 공유 되지 않게 됩니다. 또한 호출 하지 마십시오는 <xref:System.Windows.Forms.DataGridViewRowCollection.OnCollectionChanged%2A?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.DataGridView.OnRowStateChanged%2A?displayProperty=nameWithType> 메서드를 이러한 이벤트를 발생 시킵니다.

- 액세스 하지 않는 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A?displayProperty=nameWithType> 컬렉션 때 합니다 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType> 속성 값이 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>, <xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>, <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>, 또는 <xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>합니다. 이렇게 하면 선택한 모든 행의 공유 되지 않게 됩니다.

- 호출 하지 마십시오는 <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A?displayProperty=nameWithType> 메서드. 이 메서드는 행의 공유가 해제 발생할 수 있습니다.

- 호출 하지 마십시오는 <xref:System.Windows.Forms.DataGridView.SelectAll%2A?displayProperty=nameWithType> 메서드 때 합니다 <xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType> 속성 값이 <xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>합니다. 이렇게 하면 모든 행의 공유 되지 않게 됩니다.

- 설정 하지 않으면 합니다 <xref:System.Windows.Forms.DataGridViewCell.ReadOnly%2A> 또는 <xref:System.Windows.Forms.DataGridViewCell.Selected%2A> 셀 속성 `false` 해당 열에 해당 하는 속성은 설정 하는 경우 `true`합니다. 이렇게 하면 모든 행의 공유 되지 않게 됩니다.

- 액세스 하지 않는 <xref:System.Windows.Forms.DataGridViewRowCollection.List%2A?displayProperty=nameWithType> 속성입니다. 이렇게 하면 모든 행의 공유 되지 않게 됩니다.

- 호출 하지 마십시오 합니다 `Sort(IComparer)` 오버 로드는 <xref:System.Windows.Forms.DataGridView.Sort%2A> 메서드. 사용자 지정 비교자를 사용 하 여 정렬 하면 모든 행의 공유가 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [Windows Forms DataGridView 컨트롤의 성능 조정](performance-tuning-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 가상 모드](virtual-mode-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드](data-display-modes-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에 대 한 기본 셀 스타일 설정](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기 조정 옵션](sizing-options-in-the-windows-forms-datagridview-control.md)
