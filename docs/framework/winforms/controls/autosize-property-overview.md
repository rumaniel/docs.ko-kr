---
title: AutoSize 속성 개요
ms.date: 03/30/2017
helpviewer_keywords:
- sizing [Windows Forms], automatic
- layout [Windows Forms], AutoSize
- automatic sizing
- AutoSizeMode property
ms.assetid: 62fd82a2-9565-4f65-925b-9d1e66dc4e7d
ms.openlocfilehash: eb87616c2ddcf9a4ab62245d365763ee57ffb964
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211196"
---
# <a name="autosize-property-overview"></a>AutoSize 속성 개요
합니다 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성으로 지정 된 값을 사용 하도록 필요한 경우 해당 크기를 변경 하려면 컨트롤을 사용 하면는 <xref:System.Windows.Forms.Control.PreferredSize%2A> 속성입니다. 설정 하 여 특정 컨트롤에 대 한 크기 조정 동작을 조정 합니다 `AutoSizeMode` 속성입니다.

## <a name="autosize-behavior"></a>AutoSize 동작
 일부 컨트롤만 지원 합니다 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성입니다. 또한 일부 지 원하는 컨트롤을 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성도 지원 합니다.는 `AutoSizeMode` 속성.

 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성에는 특정 컨트롤 형식 및 값에 따라 다르게 동작을 생성 합니다 `AutoSizeMode` 속성이 있으면 속성입니다. 다음 표에서 항상 true 인 동작 및 각각에 대해 간략히 설명 합니다.

|항상 true 동작|설명|
|--------------------------|-----------------|
|자동 크기 조정에 런타임 기능입니다.|즉, 해당 하지 증가 또는 컨트롤 축소 있고 다음 영향을 주지 않습니다.|
|컨트롤 크기의 값을 변경 하는 경우 해당 <xref:System.Windows.Forms.Control.Location%2A> 속성 항상 일정 하 게 유지 합니다.|컨트롤의 내용을 증가 하 게 경우, 오른쪽으로 이동 하 고 아래로 컨트롤 증가 합니다. 컨트롤 왼쪽으로 증가 하지 않습니다.|
|합니다 <xref:System.Windows.Forms.Control.Dock%2A> 하 고 <xref:System.Windows.Forms.Control.Anchor%2A> 속성 경우에 적용 됩니다 <xref:System.Windows.Forms.Control.AutoSize%2A> 는 `true`합니다.|컨트롤의 값 <xref:System.Windows.Forms.Control.Location%2A> 속성이 올바른 값으로 조정 됩니다.<br /><br /> **참고** 는 <xref:System.Windows.Forms.Label> 컨트롤은이 규칙의 예외입니다. 도킹 된 값을 설정 하는 경우 <xref:System.Windows.Forms.Label> 컨트롤의 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성을 `true`는 <xref:System.Windows.Forms.Label> 컨트롤이 늘어나지 것입니다.|
|컨트롤의 <xref:System.Windows.Forms.Control.MaximumSize%2A> 하 고 <xref:System.Windows.Forms.Control.MinimumSize%2A> 속성은 적용 항상 값에 관계 없이 해당 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성입니다.|<xref:System.Windows.Forms.Control.MaximumSize%2A> 하 고 <xref:System.Windows.Forms.Control.MinimumSize%2A> 속성은 받지 않습니다는 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성입니다.|
|기본적으로 설정 합니다. 최소 크기가 없습니다.|즉, 컨트롤에서 축소로 설정 되어 있으면 <xref:System.Windows.Forms.Control.AutoSize%2A> 컨트롤에 내용이, 값 및 해당 <xref:System.Windows.Forms.Control.Size%2A> 속성은 0, 0입니다. 이 경우 지점에 사용자 컨트롤은 축소 하 고 즉시 표시 되지 않습니다.|
|컨트롤을 구현 하지 않는 경우는 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 메서드를 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 에 할당 된 마지막 값을 반환 하는 메서드는 <xref:System.Windows.Forms.Control.Size%2A> 속성.|즉, 해당 설정이 <xref:System.Windows.Forms.Control.AutoSize%2A> 에 `true` 영향을 주지 것입니다.|
|컨트롤에는 <xref:System.Windows.Forms.TableLayoutPanel> 셀까지 셀에 맞게 축소 항상 해당 <xref:System.Windows.Forms.Control.MinimumSize%2A> 에 도달 하면 합니다.|이 크기는 최대 크기에 맞게 적용 됩니다. 이 경우가 아니라면 셀의 일부인 경우는 <xref:System.Windows.Forms.SizeType.AutoSize> 행 또는 열입니다.|

## <a name="autosizemode-property"></a>AutoSizeMode 속성
 합니다 `AutoSizeMode` 속성은 기본값 보다 세부적으로 제어를 제공 <xref:System.Windows.Forms.Control.AutoSize%2A> 동작 합니다. `AutoSizeMode` 속성 어떻게 컨트롤 크기가 자동으로 조정 해당 콘텐츠를 지정 합니다. 콘텐츠를 예를 들어 수에 대 한 텍스트를 <xref:System.Windows.Forms.Button> 컨트롤이 나 컨테이너에 대 한 자식 컨트롤입니다.

 다음 표는 <xref:System.Windows.Forms.AutoSizeMode> 설정 및 동작에 대 한 설명을 각 설정 이끌어 냅니다.

|AutoSizeMode 설정|동작|
|--------------------------|--------------|
|GrowAndShrink|컨트롤이 증가 나 내용에 맞게 늘어나거나 축소 합니다.<br /><br /> 합니다 <xref:System.Windows.Forms.Control.MinimumSize%2A> 하 고 <xref:System.Windows.Forms.Control.MaximumSize%2A> 의 현재 값을 제외한 값을 적용할는 <xref:System.Windows.Forms.Control.Size%2A> 속성은 무시 됩니다.<br /><br /> 이것이 컨트롤과 같은 동작을 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성과 아니요 `AutoSizeMode` 속성.|
|GrowOnly|컨트롤 내용을 포함 하는 데 필요한 만큼 증가 하지만 지정 된 값 보다 작게 축소 되지 것입니다 해당 <xref:System.Windows.Forms.Control.Size%2A> 속성입니다.<br /><br /> 이것이 `AutoSizeMode`의 기본값입니다.|

## <a name="controls-that-support-the-autosize-property"></a>AutoSize 속성을 지 원하는 컨트롤
 다음 표에서 지 원하는 컨트롤에는 <xref:System.Windows.Forms.Control.AutoSize%2A> 고 `AutoSizeMode` 속성입니다.

|자동 크기 조정 지원|컨트롤 종류|
|----------------------|------------------|
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> 지원 되는 속성입니다.<br />-더 `AutoSizeMode` 속성입니다.|<xref:System.Windows.Forms.CheckBox><br /><br /> <xref:System.Windows.Forms.DomainUpDown><br /><br /> <xref:System.Windows.Forms.Label><br /><br /> <xref:System.Windows.Forms.LinkLabel><br /><br /> <xref:System.Windows.Forms.MaskedTextBox> (<xref:System.Windows.Forms.TextBox> 기본)<br /><br /> <xref:System.Windows.Forms.NumericUpDown><br /><br /> <xref:System.Windows.Forms.RadioButton><br /><br /> <xref:System.Windows.Forms.TextBox><br /><br /> <xref:System.Windows.Forms.TrackBar>|
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> 지원 되는 속성입니다.<br />-   `AutoSizeMode` 지원 되는 속성입니다.|<xref:System.Windows.Forms.Button><br /><br /> <xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.FlowLayoutPanel><br /><br /> <xref:System.Windows.Forms.Form><br /><br /> <xref:System.Windows.Forms.GroupBox><br /><br /> <xref:System.Windows.Forms.Panel><br /><br /> <xref:System.Windows.Forms.TableLayoutPanel>|
|-더 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성입니다.|<xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.ComboBox><br /><br /> <xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DateTimePicker><br /><br /> <xref:System.Windows.Forms.ListBox><br /><br /> <xref:System.Windows.Forms.ListView><br /><br /> <xref:System.Windows.Forms.MaskedTextBox><br /><br /> <xref:System.Windows.Forms.MonthCalendar><br /><br /> <xref:System.Windows.Forms.ProgressBar><br /><br /> <xref:System.Windows.Forms.PropertyGrid><br /><br /> <xref:System.Windows.Forms.RichTextBox><br /><br /> <xref:System.Windows.Forms.SplitContainer><br /><br /> <xref:System.Windows.Forms.TabControl><br /><br /> <xref:System.Windows.Forms.TabPage><br /><br /> <xref:System.Windows.Forms.TreeView><br /><br /> <xref:System.Windows.Forms.WebBrowser><br /><br /> <xref:System.Windows.Forms.ScrollBar>|

## <a name="autosize-in-the-design-environment"></a>디자인 환경에서 자동 크기 조정
 다음 표에서 컨트롤의 크기 조정 동작을 디자인 타임의 값을 기반으로 해당 <xref:System.Windows.Forms.Control.AutoSize%2A> 고 `AutoSizeMode` 속성입니다.

 재정의 <xref:System.Windows.Forms.Design.ControlDesigner.SelectionRules%2A> 속성을 지정된 된 컨트롤을 사용자 크기 조정이 불가능 상태 인지 여부를 결정 합니다. 다음 표에 "없습니다" 의미 <xref:System.Windows.Forms.Design.SelectionRules.Moveable> 만 "수 있음" 의미 <xref:System.Windows.Forms.Design.SelectionRules.AllSizeable> 고 <xref:System.Windows.Forms.Design.SelectionRules.Moveable>입니다.

|자동 크기 조정 설정|디자인 타임 크기 조정 동작|
|-----------------------|---------------------------------|
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `true`<br />-더 `AutoSizeMode` 속성입니다.|사용자는 다음과 같은 컨트롤을 제외 하 고 디자인 타임에 컨트롤의 크기를 조정할 수 없습니다.<br /><br /> -   <xref:System.Windows.Forms.TextBox><br />-   <xref:System.Windows.Forms.MaskedTextBox><br />-   <xref:System.Windows.Forms.RichTextBox><br />-   <xref:System.Windows.Forms.TrackBar>|
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `true`<br />-   `AutoSizeMode` = <xref:System.Windows.Forms.AutoSizeMode.GrowAndShrink>|사용자는 디자인 타임에 컨트롤의 크기를 조정할 수 없습니다.|
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `true`<br />-   `AutoSizeMode` = <xref:System.Windows.Forms.AutoSizeMode.GrowOnly>|사용자는 디자인 타임에 컨트롤의 크기를 조정할 수 있습니다. 경우는 <xref:System.Windows.Forms.Control.Size%2A> 속성을 설정 하면 사용자 컨트롤의 크기를 늘릴 수만 있습니다.|
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> = `false`또는 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성이 숨겨집니다.|사용자는 디자인 타임에 컨트롤의 크기를 조정할 수 있습니다.|

> [!NOTE]
> Visual Studio 어두운 영역에 Windows Forms 디자이너, 생산성을 극대화 하는 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성에 대 한는 <xref:System.Windows.Forms.Form> 클래스입니다. 디자인 타임에 폼 것 처럼 동작 합니다 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성이 `false`해당 실제 설정에 관계 없이 합니다. 런타임 시에 특별 한 조정 없이 이루어집니다, 그리고 및 <xref:System.Windows.Forms.Control.AutoSize%2A> 속성이 적용 되는지 속성 설정으로 지정 된 대로 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.AutoSize%2A>
- <xref:System.Windows.Forms.Control.PreferredSize%2A>
- <xref:System.Windows.Forms.Control.GetPreferredSize%2A>
