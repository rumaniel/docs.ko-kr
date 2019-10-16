---
title: Windows Forms 애플리케이션에 대한 양방향 지원
ms.date: 09/30/2017
helpviewer_keywords:
- globalization [Windows Forms], bi-directional support in Windows
- Windows Forms, international
- localization [Windows Forms], bi-directional support in Windows
- bi-directional language support [Windows Forms], Windows applications
- Windows Forms, bi-directional support
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bb97d545da422a129ece1f432b3120e1a994c453
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956920"
---
# <a name="bi-directional-support-for-windows-forms-applications"></a>Windows Forms 애플리케이션에 대한 양방향 지원
Visual Studio를 사용 하 여 아랍어 및 히브리어와 같은 양방향 (오른쪽에서 왼쪽) 언어를 지 원하는 Windows 기반 응용 프로그램을 만들 수 있습니다. 여기에는 표준 폼, 대화 상자, MDI 폼 및 이러한 폼에서 사용할 수 있는 모든 컨트롤(즉, <xref:System.Windows.Forms.Control> 네임스페이스의 모든 개체)이 포함됩니다.

## <a name="culture-support"></a>문화권 지원
 문화권 및 UI 문화권 설정은 애플리케이션에서 날짜, 시간, 통화 및 기타 정보를 사용하는 방법을 결정합니다. 양방향 언어에 대한 문화권 및 UI 문화권 지원은 다른 언어의 경우와 동일합니다. 자세한 내용은 [전역 Windows forms 및 web forms을 위한 문화권 관련 클래스](/visualstudio/ide/culture-specific-classes-for-global-windows-forms-and-web-forms)를 참조 하세요.

## <a name="righttoleft-and-righttoleftlayout-properties"></a>RightToLeft 및 RightToLeftLayout 속성
 폼이 파생되는 기본 <xref:System.Windows.Forms.Control> 클래스는 폼과 해당 컨트롤의 읽기 순서를 변경하기 위해 설정할 수 있는 <xref:System.Windows.Forms.Control.RightToLeft%2A> 속성을 포함합니다. 폼의 <xref:System.Windows.Forms.Control.RightToLeft%2A> 속성을 설정하는 경우 기본적으로 폼의 컨트롤이 이 설정을 상속합니다. 그러나 대부분의 컨트롤에서 <xref:System.Windows.Forms.Control.RightToLeft%2A> 속성을 개별적으로 설정할 수도 있습니다. 또한 [How to: Windows Forms에 오른쪽에서 왼쪽으로 표시 되는 텍스트를 표시 합니다. @ no__t-0.

 <xref:System.Windows.Forms.Control.RightToLeft%2A> 속성의 효과는 컨트롤마다 다를 수 있습니다. 일부 컨트롤에서는 속성이 <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.TreeView> 및 <xref:System.Windows.Forms.ToolTip> 컨트롤과 같이 읽기 순서만 설정합니다. 다른 컨트롤에서는 <xref:System.Windows.Forms.Control.RightToLeft%2A> 속성이 읽기 순서와 레이아웃을 둘 다 변경합니다. 여기에는 <xref:System.Windows.Forms.RadioButton>, <xref:System.Windows.Forms.ComboBox> 및 <xref:System.Windows.Forms.CheckBox> 컨트롤이 포함됩니다. 다른 컨트롤에서는 레이아웃을 오른쪽에서 왼쪽으로 미러링하기 위해 <xref:System.Windows.Forms.Form.RightToLeftLayout%2A> 속성을 적용해야 합니다. 다음 표에서는 <xref:System.Windows.Forms.Control.RightToLeft%2A> 및 <xref:System.Windows.Forms.Form.RightToLeftLayout%2A> 속성이 개별 Windows Forms 컨트롤에 미치는 영향에 대한 세부 정보를 제공합니다.

|컨트롤/구성 요소|RightToLeft 속성의 효과|RightToLeftLayout 속성의 효과|미러링 필요 여부|
|------------------------|------------------------------------|------------------------------------------|-------------------------|
|<xref:System.Windows.Forms.Button>|RTL 읽기 순서를 설정합니다. <xref:System.Windows.Forms.ButtonBase.TextAlign%2A>, <xref:System.Windows.Forms.ButtonBase.ImageAlign%2A> 및 <xref:System.Windows.Forms.ButtonBase.TextImageRelation%2A>을 반대로 바꿉니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.CheckBox>|확인란이 텍스트 오른쪽에 표시됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.CheckedListBox>|모든 확인란이 텍스트 오른쪽에 표시됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ColorDialog>|영향을 받지 않습니다. 운영 체제의 언어에 따라 달라집니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ComboBox>|콤보 상자 컨트롤의 항목이 오른쪽 맞춤됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ContextMenu>|RTL 읽기 순서로 오른쪽 맞춤됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.DataGrid>|RTL 읽기 순서로 오른쪽 맞춤됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.DataGridView>|RTL 읽기 순서와 컨트롤 레이아웃 둘 다에 영향을 줍니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.DateTimePicker>|영향을 받지 않습니다. 운영 체제의 언어에 따라 달라집니다.|컨트롤을 미러링합니다.|예|
|<xref:System.Windows.Forms.DomainUpDown>|위로 및 아래로 단추를 왼쪽 맞춤합니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ErrorProvider>|지원되지 않음|효과 없음|아니요|
|<xref:System.Windows.Forms.FontDialog>|운영 체제의 언어에 따라 달라집니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.Form>|RTL 읽기 순서를 설정하고 스크롤 막대를 반대로 바꿉니다.|폼을 미러링합니다.|예|
|<xref:System.Windows.Forms.GroupBox>|캡션이 오른쪽 맞춤으로 표시됩니다. 이 속성은 자식 컨트롤에 상속될 수 있습니다.|오른쪽에서 왼쪽 미러링을 지원하려면 컨트롤 내에서 <xref:System.Windows.Forms.TableLayoutPanel>을 사용합니다.|아니요|
|<xref:System.Windows.Forms.HScrollBar>|스크롤 상자(thumb)를 오른쪽 맞춤하여 시작됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ImageList>|필요하지 않음|효과 없음|아니요|
|<xref:System.Windows.Forms.Label>|오른쪽 맞춤으로 표시됩니다. <xref:System.Windows.Forms.Label.TextAlign%2A> 및 <xref:System.Windows.Forms.Label.ImageAlign%2A>을 반대로 바꿉니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.LinkLabel>|오른쪽 맞춤으로 표시됩니다. <xref:System.Windows.Forms.Label.TextAlign%2A> 및 <xref:System.Windows.Forms.Label.ImageAlign%2A>을 반대로 바꿉니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ListBox>|항목이 오른쪽 맞춤됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.ListView>|읽기 순서를 RTL로 설정합니다. 요소가 왼쪽 맞춤으로 유지됩니다.|컨트롤을 미러링합니다.|예|
|<xref:System.Windows.Forms.MainMenu>|런타임(디자인 타임 아님)에 RTL 읽기 순서를 사용하여 오른쪽 맞춤으로 표시됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.MaskedTextBox>|텍스트를 오른쪽에서 왼쪽으로 표시합니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.MonthCalendar>|영향을 받지 않습니다. 운영 체제의 언어에 따라 달라집니다.|컨트롤을 미러링합니다.|예|
|<xref:System.Windows.Forms.NotifyIcon>|지원되지 않음|지원되지 않음|아니요|
|<xref:System.Windows.Forms.NumericUpDown>|위로 및 아래로 단추가 왼쪽 맞춤됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.OpenFileDialog>|오른쪽에서 왼쪽으로 운영 체제에서 포함 양식의 <xref:System.Windows.Forms.Control.RightToLeft> 속성을 <xref:System.Windows.Forms.RightToLeft.Yes?displayProperty=nameWithType>로 설정 하면 대화 상자가 문제의. |효과 없음|아니요|
|<xref:System.Windows.Forms.PageSetupDialog>|영향을 받지 않습니다. 운영 체제의 언어에 따라 달라집니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.Panel>|이 속성은 자식 컨트롤에 상속될 수 있습니다.|오른쪽에서 왼쪽을 지원하려면 컨트롤 내에서 <xref:System.Windows.Forms.TableLayoutPanel>을 사용합니다.|예|
|<xref:System.Windows.Forms.PictureBox>|지원되지 않음|효과 없음|아니요|
|<xref:System.Windows.Forms.PrintDialog>|영향을 받지 않습니다. 운영 체제의 언어에 따라 달라집니다.|효과 없음|아니요|
|<xref:System.Drawing.Printing.PrintDocument>|세로 스크롤 막대는 왼쪽 맞춤되고 가로 스크롤 막대는 왼쪽에서 시작됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.PrintPreviewDialog>|지원되지 않음|지원되지 않음|아니요|
|<xref:System.Windows.Forms.ProgressBar>|이 속성의 영향을 받지 않습니다.|컨트롤을 미러링합니다.|예|
|<xref:System.Windows.Forms.RadioButton>|라디오 단추가 텍스트 오른쪽에 표시됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.RichTextBox>|텍스트를 포함하는 컨트롤 요소가 RTL 읽기 순서를 사용하여 오른쪽에서 왼쪽으로 표시됩니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.SaveFileDialog>|영향을 받지 않습니다. 운영 체제의 언어에 따라 달라집니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.SplitContainer>|패널 레이아웃이 반대로 바뀝니다. 세로 스크롤 막대는 왼쪽에 표시되고 가로 스크롤 막대는 오른쪽에서 시작됩니다.|<xref:System.Windows.Forms.TableLayoutPanel>을 사용하여 자식 컨트롤의 순서를 미러링합니다.|아니요|
|<xref:System.Windows.Forms.Splitter>|지원되지 않음|효과 없음|아니요|
|<xref:System.Windows.Forms.StatusBar>|지원되지 않습니다. 대신 <xref:System.Windows.Forms.StatusStrip>을 사용합니다.|효과가 없습니다. 대신 <xref:System.Windows.Forms.StatusStrip>을 사용합니다.|아니요|
|<xref:System.Windows.Forms.TabControl>|이 속성의 영향을 받지 않습니다.|컨트롤을 미러링합니다.|예|
|<xref:System.Windows.Forms.TextBox>|RTL 읽기 순서를 사용하여 텍스트를 오른쪽에서 왼쪽으로 표시합니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.Timer>|필요하지 않음|필요하지 않음|아니요|
|<xref:System.Windows.Forms.ToolBar>|이 속성의 영향을 받지 않습니다. 대신 <xref:System.Windows.Forms.ToolStrip>을 사용합니다.|효과가 없습니다. 대신 <xref:System.Windows.Forms.ToolStrip>을 사용합니다.|예|
|<xref:System.Windows.Forms.ToolTip>|RTL 읽기 순서를 설정합니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.TrackBar>|스크롤 또는 추적이 오른쪽에서 시작됩니다. <xref:System.Windows.Forms.TrackBar.Orientation%2A>이 세로이면 눈금이 오른쪽에서 발생합니다.|효과 없음|아니요|
|<xref:System.Windows.Forms.TreeView>|RTL 읽기 순서만 설정합니다.|컨트롤을 미러링합니다.|예|
|<xref:System.Windows.Forms.UserControl>|세로 스크롤 막대는 왼쪽에 표시되고 가로 스크롤 막대는 오른쪽에 thumb이 있습니다.|직접 지원되지 않습니다. <xref:System.Windows.Forms.TableLayoutPanel>을 사용합니다.|아니요|
|<xref:System.Windows.Forms.VScrollBar>|스크롤 가능한 컨트롤의 오른쪽이 아닌 왼쪽에 표시됩니다.|효과 없음|아니요|

## <a name="encoding"></a>인코딩
 Windows Forms는 유니코드를 지원하므로 양방향 애플리케이션을 만들 때 모든 문자 집합을 포함할 수 있습니다. 그러나 모든 Windows Forms 컨트롤이 모든 플랫폼에서 유니코드를 지원하는 것은 아닙니다.

## <a name="gdi"></a>GDI+
 GDI +를 사용 하 여 오른쪽에서 왼쪽 읽기 순서로 텍스트를 그릴 수 있습니다. 텍스트를 그리는 데 사용되는 <xref:System.Drawing.Graphics.DrawString%2A> 메서드는 텍스트의 원점을 반대로 바꾸기 위해 <xref:System.Drawing.StringFormatFlags> 열거형의 <xref:System.Drawing.StringFormatFlags.DirectionRightToLeft> 멤버로 설정할 수 있는 `StringFormat` 매개 변수를 지원합니다.

## <a name="common-dialog-boxes"></a>일반 대화 상자
 파일 열기 대화 상자와 같은 시스템 도구는 Windows에 의해 제어됩니다. 이러한 도구는 운영 체제에서 언어 요소를 상속합니다. 올바른 언어 설정으로 Windows 버전을 사용하는 경우 이러한 대화 상자가 양방향 언어에서 제대로 작동합니다.

 마찬가지로, 메시지 상자도 운영 체제를 통해 양방향 텍스트를 지원합니다. 메시지 상자 단추의 캡션은 현재 언어 설정을 기반으로 합니다. 기본적으로 메시지 상자는 오른쪽에서 왼쪽 읽기 순서를 사용하지 않지만 매개 변수를 지정하여 메시지 상자가 표시될 때 읽기 순서를 변경할 수 있습니다.

## <a name="righttoleft-scrollbars-and-scrollablecontrol"></a>RightToLeft, Scrollbars 및 ScrollableControl
 현재 Windows Forms에는 <xref:System.Windows.Forms.Control.RightToLeft%2A>가 사용하도록 설정되고 <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A>이 <xref:System.Windows.Forms.RightToLeft.Yes>로 설정된 경우 <xref:System.Windows.Forms.ScrollableControl>에서 파생된 모든 클래스가 제대로 작동할 수 없게 하는 제한 사항이 있습니다. 예를 들어 <xref:System.Windows.Forms.Panel>과 같은 컨트롤이나 <xref:System.Windows.Forms.Panel>에서 파생된 컨테이너 클래스(예: <xref:System.Windows.Forms.FlowLayoutPanel> 또는 <xref:System.Windows.Forms.TableLayoutPanel>)를 폼에 배치한다고 가정해 보세요. 컨테이너의 <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A>을 <xref:System.Windows.Forms.RightToLeft.Yes>로 설정한 다음 컨테이너 내부에 있는 하나 이상 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 <xref:System.Windows.Forms.AnchorStyles.Right>로 설정하는 경우에는 스크롤 막대가 나타나지 않습니다. <xref:System.Windows.Forms.ScrollableControl>에서 파생된 클래스는 <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A>이 <xref:System.Windows.Forms.RightToLeft.No>로 설정된 것처럼 동작합니다.

 현재 유일한 해결 방법은 <xref:System.Windows.Forms.ScrollableControl>을 다른 <xref:System.Windows.Forms.ScrollableControl> 안에 중첩하는 것입니다. 예를 들어 이런 상황에서 <xref:System.Windows.Forms.TableLayoutPanel>이 작동해야 하는 경우 <xref:System.Windows.Forms.Panel> 컨트롤 내부에 배치하고 <xref:System.Windows.Forms.Panel>의 <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A>을 <xref:System.Windows.Forms.RightToLeft.Yes>로 설정할 수 있습니다.

## <a name="mirroring"></a>미러링
 *미러링*은 오른쪽에서 왼쪽으로 배치되도록 UI 요소의 레이아웃을 반대로 바꾸는 것을 가리킵니다. 예를 들어 미러링된 Windows Form에서는 최소화, 최대화 및 닫기 단추가 제목 표시줄에서 맨 오른쪽이 아니라 맨 왼쪽에 나타납니다.

 폼이나 컨트롤의 <xref:System.Windows.Forms.Control.RightToLeft%2A> 속성을 `true`로 설정하는 경우 폼에서 요소의 읽기 순서가 반대로 바뀌지만 이 설정은 레이아웃을 반대인 오른쪽에서 왼쪽으로 바꾸지 않습니다. 즉, 미러링이 발생하지 않습니다. 예를 들어 이 속성을 설정하면 양식의 제목 표시줄에 있는 **최소화**, **최대화** 및 **닫기** 단추가 양식의 왼쪽으로 이동하지 않습니다. 마찬가지로, <xref:System.Windows.Forms.TreeView> 컨트롤과 같은 일부 컨트롤은 아랍어 또는 히브리어에 맞게 표시되도록 변경하기 위해 미러링이 필요합니다. <xref:System.Windows.Forms.Form.RightToLeftLayout%2A> 속성을 설정하여 이러한 컨트롤을 미러링할 수 있습니다.

 다음과 같은 컨트롤의 미러링된 버전을 만들 수 있습니다.

- <xref:System.Windows.Forms.ColumnHeader.ListView%2A>

- <xref:System.Windows.Forms.Panel>

- <xref:System.Windows.Forms.StatusBar>

- <xref:System.Windows.Forms.TabControl>

- <xref:System.Windows.Forms.TabPage>

- <xref:System.Windows.Forms.ToolBar>

- <xref:System.Windows.Forms.TreeView>

 일부 컨트롤은 봉인됩니다. 따라서 해당 컨트롤에서 새 컨트롤을 파생시킬 수 없습니다. 여기에는 <xref:System.Windows.Forms.ImageList> 및 <xref:System.Windows.Forms.ProgressBar> 컨트롤이 포함됩니다.

## <a name="see-also"></a>참조

- [ASP.NET 웹 애플리케이션에 대한 양방향 지원](https://docs.microsoft.com/previous-versions/aspnet/6eedwbtt(v=vs.100))
