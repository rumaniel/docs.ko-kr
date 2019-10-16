---
title: 소유자가 그린 기본 제공 컨트롤 지원
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [Windows Forms], owner
- drawing [Windows Forms], custom
- controls [Windows Forms], changing appearance
- custom drawing
- owner drawing
ms.assetid: 3823d01e-9610-43e6-864d-99f9b7c2b351
ms.openlocfilehash: f0d4b99f9ee0134fc7334a941dd5ef4fd7ba3df3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930189"
---
# <a name="controls-with-built-in-owner-drawing-support"></a>소유자가 그린 기본 제공 컨트롤 지원
사용자 지정 그리기라고도 하는 Windows Forms의 소유자 그리기는 특정 컨트롤을 시각적 모양으로 변경하는 기술입니다.  
  
> [!NOTE]
> 이 항목의 "컨트롤" 이라는 단어는 <xref:System.Windows.Forms.Control> 또는 <xref:System.ComponentModel.Component>에서 파생 되는 클래스를 의미 하는 데 사용 됩니다.  
  
 일반적으로 Windows는 컨트롤의 모양을 결정 <xref:System.Windows.Forms.Control.BackColor%2A> 하는 등의 속성 설정을 사용 하 여 자동으로 그리기를 처리 합니다. 소유자 그리기를 통해 속성을 사용하여 사용할 수 없는 모양의 요소를 변경하며 그리기 프로세스를 사용합니다. 예를 들어 많은 컨트롤을 사용하여 표시되는 텍스트의 색을 설정할 수 있지만 단색으로 제한됩니다. 소유자 그리기를 사용하면 검정과 빨강 부분에 있는 텍스트의 일부를 표시하는 같은 작업을 수행할 수 있습니다.  
  
 실제로 소유자 그리기는 양식에 그래픽을 그리는 것과 비슷합니다. 예를 들어 폼의 <xref:System.Windows.Forms.Control.Paint> 이벤트에 대 한 처리기에서 그래픽 메서드를 사용 하 여 `ListBox` 컨트롤을 에뮬레이트할 수 있지만 모든 사용자 조작을 처리 하는 사용자 고유의 코드를 작성 해야 합니다. 소유자 그리기를 통해 컨트롤은 사용자 코드를 사용하여 해당 콘텐츠를 그리지만 그렇지 않은 경우 해당 내장 기능을 모두 유지합니다. 각 항목의 다른 측면에 대한 기본 모양을 사용하는 동안 각 항목의 일부 측면을 사용자 지정하거나 컨트롤의 각 항목을 그릴 수 있는 그래픽 메서드를 사용할 수 있습니다.  
  
## <a name="owner-drawing-in-windows-forms-controls"></a>Windows Forms 컨트롤의 소유자 그리기  
 소유자 그리기를 지원하는 컨트롤에서 소유자 그리기를 수행하려면 일반적으로 하나의 속성을 설정하고 하나 이상의 이벤트를 처리합니다.  
  
 소유자 그리기를 지원하는 대부분의 컨트롤에는 컨트롤 자체가 그려질 때 해당 그리기 관련 이벤트가 발생할 지 여부를 나타내는 `OwnerDraw` 또는 `DrawMode` 속성이 있습니다.  
  
 `OwnerDraw` 또는 `DrawMode` 속성이 없는 컨트롤에는 자동으로 발생하는 그리기 이벤트를 제공하는 `DataGridView` 컨트롤이 포함되고 자체 그리기 관련 이벤트가 있는 외부 렌더링 클래스를 사용하여 그려지는 `ToolStrip` 컨트롤이 포함됩니다.  
  
 다양한 종류의 그리기 이벤트가 있지만 컨트롤 내에서 단일 항목을 그릴 수 있도록 일반적인 그리기 이벤트가 발생합니다. 이벤트 처리기는 그려지고 있는 항목 및 그리는 데 사용할 수 있는 도구에 대한 정보를 포함하는 `EventArgs` 개체를 수신합니다. 예를 들어이 개체는 일반적으로 부모 컬렉션 내의 항목 인덱스 번호, <xref:System.Drawing.Rectangle> 항목의 표시 경계를 나타내는 <xref:System.Drawing.Graphics> 및 그리기 메서드를 호출 하는 개체를 포함 합니다. 일부 이벤트에서 `EventArgs` 개체는 기본적으로 배경이나 포커스 영역과 같은 항목의 일부 측면을 그리도록 호출할 수 있는 메서드와 항목에 대한 추가 정보를 제공합니다.  
  
 소유자가 그린 사용자 지정 항목을 포함하는 재사용 가능한 컨트롤을 만들려면, 소유자 그리기를 지원하는 컨트롤 클래스에서 파생되는 새 클래스를 만듭니다. 그리기 이벤트를 처리하는 대신 적절한 `On`*EventName* 메서드 또는 새 클래스의 메소드에 대한 재정의에 소유자 그리기 코드를 포함합니다. 이 경우 컨트롤 사용자가 소유자 그리기 이벤트를 처리하고 추가 사용자 지정을 제공할 수 있도록 기본 클래스 `On`*EventName* 메서드를 호출하는지 확인하십시오.  
  
 다음 Windows Forms 컨트롤은 모든 버전의 .NET Framework에서 소유자 그리기를 지원합니다.  
  
- <xref:System.Windows.Forms.ListBox>  
  
- <xref:System.Windows.Forms.ComboBox>  
  
- <xref:System.Windows.Forms.MenuItem>(및 <xref:System.Windows.Forms.MainMenu> <xref:System.Windows.Forms.ContextMenu>에서 사용 됨)  
  
- <xref:System.Windows.Forms.TabControl>  
  
 다음 컨트롤은 .NET Framework 2.0 에서만 소유자 그리기를 지원 합니다.  
  
- <xref:System.Windows.Forms.ToolTip>  
  
- <xref:System.Windows.Forms.ListView>  
  
- <xref:System.Windows.Forms.TreeView>  
  
 다음 컨트롤은 소유자 그리기를 지원 하며 .NET Framework 2.0에서 새로 제공 됩니다.  
  
- <xref:System.Windows.Forms.DataGridView>  
  
- <xref:System.Windows.Forms.ToolStrip>  
  
 다음 섹션에서는 이 컨트롤에 대한 각각의 추가 세부 정보를 제공합니다.  
  
### <a name="listbox-and-combobox-controls"></a>ListBox 및 ComboBox 컨트롤  
 <xref:System.Windows.Forms.ListBox> 및<xref:System.Windows.Forms.ComboBox> 컨트롤을 사용 하면 컨트롤의 개별 항목을 모두 한 크기 또는 다양 한 크기로 그릴 수 있습니다.  
  
> [!NOTE]
> <xref:System.Windows.Forms.CheckedListBox> 컨트롤이 컨트롤<xref:System.Windows.Forms.ListBox> 에서 파생 되더라도 소유자 그리기를 지원 하지 않습니다.  
  
 각 항목을 동일한 크기로 그리려면 `DrawMode` 속성을로 <xref:System.Windows.Forms.DrawMode.OwnerDrawFixed> 설정 하 고 `DrawItem` 이벤트를 처리 합니다.  
  
 다른 크기를 사용 하 여 `DrawMode` 각 항목을 그리려면 속성을로 <xref:System.Windows.Forms.DrawMode.OwnerDrawVariable> 설정 하 고 `MeasureItem` 및 `DrawItem` 이벤트를 모두 처리 합니다. `MeasureItem` 이벤트를 사용하여 `DrawItem` 이벤트가 해당 항목에 대해 발생하기 전에 항목의 크기를 나타낼 수 있습니다.  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.ListBox.DrawMode%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ListBox.MeasureItem?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ListBox.DrawItem?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ComboBox.DrawMode%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ComboBox.MeasureItem?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ComboBox.DrawItem?displayProperty=nameWithType>  
  
- [방법: ComboBox 컨트롤에서 가변 크기 텍스트 만들기](how-to-create-variable-sized-text-in-a-combobox-control.md)  
  
### <a name="menuitem-component"></a>MenuItem 구성 요소  
 구성 요소는 <xref:System.Windows.Forms.MainMenu> 또는<xref:System.Windows.Forms.ContextMenu> 구성 요소의 단일 메뉴 항목을 나타냅니다. <xref:System.Windows.Forms.MenuItem>  
  
 를 그리려면 <xref:System.Windows.Forms.MenuItem>해당 `OwnerDraw` 속성을로 설정 하 `true` 고 해당 `DrawItem` 이벤트를 처리 합니다. `DrawItem` 이벤트가 발생하기 전에 메뉴 항목의 크기를 사용자 지정하려면, 항목의 `MeasureItem` 이벤트를 처리합니다.  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.MenuItem.OwnerDraw%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.MenuItem.DrawItem?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.MenuItem.MeasureItem?displayProperty=nameWithType>  
  
### <a name="tabcontrol-control"></a>TabControl 컨트롤  
 <xref:System.Windows.Forms.TabControl> 컨트롤을 사용 하면 컨트롤에서 개별 탭을 그릴 수 있습니다. 소유자 그리기는 탭에만 영향을 줍니다. 내용 <xref:System.Windows.Forms.TabPage> 에는 영향을 주지 않습니다.  
  
 에서 <xref:System.Windows.Forms.TabControl>각 탭을 그리려면 `DrawMode` 속성을<xref:System.Windows.Forms.TabDrawMode.OwnerDrawFixed> 로 설정 하 고 이벤트를처리합니다.`DrawItem` 이 이벤트는 탭이 컨트롤에 표시되는 경우에만 각 탭에 대해 한 번 발생합니다.  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.TabControl.DrawMode%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.TabControl.DrawItem?displayProperty=nameWithType>  
  
### <a name="tooltip-component"></a>ToolTip 구성 요소  
 구성 <xref:System.Windows.Forms.ToolTip> 요소를 사용 하면 표시 될 때 전체 도구 설명을 그릴 수 있습니다.  
  
 를 그리려면 <xref:System.Windows.Forms.ToolTip>해당 `OwnerDraw` 속성을로 설정 하 `true` 고 해당 `Draw` 이벤트를 처리 합니다. 이벤트가 발생 <xref:System.Windows.Forms.ToolTip>하기전의 크기를 사용자 지정 하려면 이벤트를 처리 <xref:System.Windows.Forms.PopupEventArgs.ToolTipSize%2A> 하고이벤트처리기에서속성을설정합니다.`Popup` `Draw`  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.ToolTip.OwnerDraw%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ToolTip.Draw?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ToolTip.Popup?displayProperty=nameWithType>  
  
### <a name="listview-control"></a>ListView 컨트롤  
 <xref:System.Windows.Forms.ListView> 컨트롤을 사용 하면 컨트롤에 개별 항목, 하위 항목 및 열 머리글을 그릴 수 있습니다.  
  
 소유자 그리기를 컨트롤에서 사용하려면 `OwnerDraw` 속성을 `true`(으)로 설정합니다.  
  
 컨트롤의 각 항목을 그리려면 `DrawItem` 이벤트를 처리합니다.  
  
 <xref:System.Windows.Forms.ListView.View%2A> 속성이로 <xref:System.Windows.Forms.View.Details>설정 된 경우 컨트롤에 각 하위 항목 또는 열 머리글을 그리려면 `DrawSubItem` 및 `DrawColumnHeader` 이벤트를 처리 합니다.  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.ListView.OwnerDraw%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ListView.DrawItem?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ListView.DrawSubItem?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.ListView.DrawColumnHeader?displayProperty=nameWithType>  
  
### <a name="treeview-control"></a>TreeView 컨트롤  
 <xref:System.Windows.Forms.TreeView> 컨트롤을 사용 하면 컨트롤에서 개별 노드를 그릴 수 있습니다.  
  
 각 노드에 표시 된 텍스트만 그리려면 `DrawMode` 속성을로 <xref:System.Windows.Forms.TreeViewDrawMode.OwnerDrawText> 설정 하 고 `DrawNode` 이벤트를 처리 하 여 텍스트를 그립니다.  
  
 각 노드의 요소를 모두 그리려면 `DrawMode` 속성을로 <xref:System.Windows.Forms.TreeViewDrawMode.OwnerDrawAll> 설정 하 고 `DrawNode` 이벤트를 처리 하 여 텍스트, 아이콘, 확인란, 더하기 및 빼기 기호, 노드를 연결 하는 선 등 필요한 요소를 그립니다.  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.TreeView.DrawMode%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.TreeView.DrawNode?displayProperty=nameWithType>  
  
### <a name="datagridview-control"></a>DataGridView 컨트롤  
 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하면 컨트롤의 개별 셀과 행을 그릴 수 있습니다.  
  
 개별 셀을 그리려면 `CellPainting` 이벤트를 처리합니다.  
  
 개별 행이나 행의 요소를 그리려면 `RowPrePaint` 및 `RowPostPaint` 이벤트 중 하나 또는 모두를 처리합니다. `RowPrePaint` 이벤트는 행의 셀이 그려지기 전에 발생하며 `RowPostPaint` 이벤트는 셀이 그려진 후에 발생합니다. 두 이벤트 및 `CellPainting` 이벤트 모두를 처리하여 별도로 행 배경, 개별 셀 및 행 전경을 그리거나, 필요한 곳에 특정 사용자 지정을 제공하고 행의 다른 요소에 대한 기본 표시를 사용할 수 있습니다.  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.DataGridView.CellPainting>  
  
- <xref:System.Windows.Forms.DataGridView.RowPrePaint>  
  
- <xref:System.Windows.Forms.DataGridView.RowPostPaint>  
  
- [방법: Windows Forms DataGridView 컨트롤에서 셀 모양 사용자 지정](customize-the-appearance-of-cells-in-the-datagrid.md)  
  
- [방법: Windows Forms DataGridView 컨트롤에서 행 모양 사용자 지정](customize-the-appearance-of-rows-in-the-datagrid.md)  
  
### <a name="toolstrip-control"></a>ToolStrip 컨트롤  
 <xref:System.Windows.Forms.ToolStrip>및 파생 된 컨트롤을 사용 하 여 모양의 모든 측면을 사용자 지정할 수 있습니다.  
  
 <xref:System.Windows.Forms.ToolStrip> 컨트롤에 대 한 사용자 지정 렌더링을 제공 하려면 <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.ToolStripPanel> <xref:System.Windows.Forms.ToolStripManager>, 또는 <xref:System.Windows.Forms.ToolStripContentPanel> `ToolStripRenderer` 의 `Renderer` 속성을 개체로 설정 하 고에서 제공 하는 여러 그리기 이벤트를 하나 이상 처리 합니다. `ToolStripRenderer` 클래스. 또는 `Renderer` 특정 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> `ToolStripRenderer` <xref:System.Windows.Forms.ToolStripSystemRenderer> EventName 메서드를구현하거나재정의하는,또는에서파생된고유한클래스의인스턴스로속성을설정합니다.`On`  
  
 코드 예제를 포함한 자세한 내용은 다음 항목을 참조하십시오.  
  
- <xref:System.Windows.Forms.ToolStripRenderer>  
  
- [방법: Windows Forms의 ToolStrip 컨트롤에 대 한 사용자 지정 렌더러 만들기 및 설정](create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)  
  
- [방법: ToolStrip 컨트롤 그리기 사용자 지정](how-to-custom-draw-a-toolstrip-control.md)  
  
## <a name="see-also"></a>참고자료

- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
