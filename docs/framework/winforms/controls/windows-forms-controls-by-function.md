---
title: 기능별 Windows Forms 컨트롤
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], by function
- Windows Forms, controls by function
- Windows Forms controls, list of
ms.assetid: 5e65a6c3-5d6f-480d-beb8-b28f865f07e3
ms.openlocfilehash: 366b7412a61cac9d3706500adaee34fa8659fba2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922712"
---
# <a name="windows-forms-controls-by-function"></a>기능별 Windows Forms 컨트롤
Windows Forms는 다양 한 기능을 수행 하는 컨트롤 및 구성 요소를 제공 합니다. 다음 표에서는 일반 함수에 따라 Windows Forms 컨트롤 및 구성 요소를 나열 합니다. 또한 동일한 함수를 제공 하는 여러 컨트롤이 있는 경우에는 대체 된 컨트롤에 대 한 메모와 함께 권장 컨트롤이 나열 됩니다. 별도의 후속 테이블에서 대체 된 컨트롤은 권장 되는 대체 항목으로 나열 됩니다.  
  
> [!NOTE]
> 다음 표에서는 Windows Forms에서 사용할 수 있는 모든 컨트롤이 나 구성 요소를 나열 하지 않습니다. 보다 포괄적인 목록은 [Windows Forms에서 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md) 을 참조 하세요.  
  
## <a name="recommended-controls-and-components-by-function"></a>기능에 권장 되는 컨트롤 및 구성 요소  
  
|함수|컨트롤|설명|  
|--------------|-------------|-----------------|  
|데이터 표시|<xref:System.Windows.Forms.DataGridView> 컨트롤|<xref:System.Windows.Forms.DataGridView> 컨트롤은 데이터를 표시 하기 위한 사용자 지정 가능한 테이블을 제공 합니다. <xref:System.Windows.Forms.DataGridView> 클래스를 사용 하면 셀, 행, 열 및 테두리를 사용자 지정할 수 있습니다. **참고:**  컨트롤 <xref:System.Windows.Forms.DataGridView> 은 <xref:System.Windows.Forms.DataGrid> 컨트롤에 없는 다양 한 기본 및 고급 기능을 제공 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤과 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md) 을 참조 하세요.|  
|데이터 바인딩 및 탐색|<xref:System.Windows.Forms.BindingSource> 구성 요소|통화 관리, 변경 알림 및 기타 서비스를 제공 하 여 폼의 컨트롤을 데이터에 간편 하 게 바인딩할 수 있습니다.|  
||<xref:System.Windows.Forms.BindingNavigator> 컨트롤|폼의 데이터를 탐색 하 고 조작 하기 위한 도구 모음 형식 인터페이스를 제공 합니다.|  
|텍스트 편집|<xref:System.Windows.Forms.TextBox> 컨트롤|런타임에 사용자가 편집 하거나 프로그래밍 방식으로 변경할 수 있는 디자인 타임에 입력 한 텍스트를 표시 합니다.|  
||<xref:System.Windows.Forms.RichTextBox> 컨트롤|텍스트를 일반 텍스트 또는 RTF (서식 있는 텍스트) 형식으로 표시할 수 있습니다.|  
||<xref:System.Windows.Forms.MaskedTextBox> 컨트롤|사용자 입력의 형식을 제한 합니다.|  
|정보 표시 (읽기 전용)|<xref:System.Windows.Forms.Label> 컨트롤|사용자가 직접 편집할 수 없는 텍스트를 표시합니다.|  
||<xref:System.Windows.Forms.LinkLabel> 컨트롤|텍스트를 웹 스타일 링크로 표시 하 고 사용자가 특수 텍스트를 클릭 하면 이벤트를 트리거합니다. 일반적으로 텍스트는 다른 창이 나 웹 사이트에 대 한 링크입니다.|  
||<xref:System.Windows.Forms.StatusStrip> 컨트롤|일반적으로 부모 폼의 맨 아래에 있는 프레임 영역을 사용 하 여 응용 프로그램의 현재 상태에 대 한 정보를 표시 합니다.|  
||<xref:System.Windows.Forms.ProgressBar> 컨트롤|사용자에 게 작업의 현재 진행률을 표시 합니다.|  
|웹 페이지 표시|<xref:System.Windows.Forms.WebBrowser> 컨트롤|사용자가 해당 양식 내에서 웹 페이지를 탐색할 수 있도록 합니다.|  
|목록에서 선택|<xref:System.Windows.Forms.CheckedListBox> 컨트롤|각각 확인란이 함께 표시 되는 스크롤 가능한 항목 목록을 표시 합니다.|  
||<xref:System.Windows.Forms.ComboBox> 컨트롤|항목의 드롭다운 목록을 표시 합니다.|  
||<xref:System.Windows.Forms.DomainUpDown> 컨트롤|사용자가 위쪽 및 아래쪽 단추를 사용 하 여 스크롤할 수 있는 텍스트 항목의 목록을 표시 합니다.|  
||<xref:System.Windows.Forms.ListBox> 컨트롤|텍스트와 그래픽 항목 (아이콘)의 목록을 표시 합니다.|  
||<xref:System.Windows.Forms.ListView> 컨트롤|네 가지 보기 중 하나로 항목을 표시 합니다. 보기에는 텍스트만, 작은 아이콘을 포함 하는 텍스트, 아이콘이 많은 텍스트 및 자세히 보기가 포함 됩니다.|  
||<xref:System.Windows.Forms.NumericUpDown> 컨트롤|사용자가 위쪽 및 아래쪽 단추를 사용 하 여 스크롤할 수 있는 숫자 목록을 표시 합니다.|  
||<xref:System.Windows.Forms.TreeView> 컨트롤|선택적 확인란 또는 아이콘이 있는 텍스트로 구성 될 수 있는 노드 개체의 계층적 컬렉션을 표시 합니다.|  
|그래픽 표시|<xref:System.Windows.Forms.PictureBox> 컨트롤|비트맵, 아이콘 등의 그래픽 파일을 프레임에 표시 합니다.|  
|그래픽 저장소|<xref:System.Windows.Forms.ImageList> 컨트롤|이미지에 대 한 리포지토리로 사용 됩니다. <xref:System.Windows.Forms.ImageList>컨트롤과 여기에 포함 된 이미지는 한 응용 프로그램에서 다음 응용 프로그램으로 다시 사용할 수 있습니다.|  
|값 설정|<xref:System.Windows.Forms.CheckBox> 컨트롤|텍스트에 대 한 확인란 및 레이블을 표시 합니다. 일반적으로 옵션을 설정 하는 데 사용 됩니다.|  
||<xref:System.Windows.Forms.CheckedListBox> 컨트롤|각각 확인란이 함께 표시 되는 스크롤 가능한 항목 목록을 표시 합니다.|  
||<xref:System.Windows.Forms.RadioButton> 컨트롤|설정 하거나 해제할 수 있는 단추를 표시 합니다.|  
||<xref:System.Windows.Forms.TrackBar> 컨트롤|사용자가 눈금을 따라 "thumb"을 이동 하 여 눈금의 값을 설정할 수 있습니다.|  
|날짜 설정|<xref:System.Windows.Forms.DateTimePicker> 컨트롤|사용자가 날짜 또는 시간을 선택할 수 있는 그래픽 달력을 표시 합니다.|  
||<xref:System.Windows.Forms.MonthCalendar> 컨트롤|사용자가 날짜 범위를 선택할 수 있는 그래픽 달력을 표시 합니다.|  
|대화 상자|<xref:System.Windows.Forms.ColorDialog> 컨트롤|사용자가 인터페이스 요소의 색을 설정할 수 있는 색 선택 대화 상자를 표시 합니다.|  
||<xref:System.Windows.Forms.FontDialog> 컨트롤|사용자가 글꼴 및 해당 특성을 설정할 수 있는 대화 상자를 표시 합니다.|  
||<xref:System.Windows.Forms.OpenFileDialog> 컨트롤|사용자가 파일을 탐색 하 고 선택할 수 있는 대화 상자를 표시 합니다.|  
||<xref:System.Windows.Forms.PrintDialog> 컨트롤|사용자가 프린터를 선택 하 고 해당 특성을 설정할 수 있는 대화 상자를 표시 합니다.|  
||<xref:System.Windows.Forms.PrintPreviewDialog> 컨트롤|컨트롤 <xref:System.Drawing.Printing.PrintDocument> 구성 요소가 인쇄 될 때 표시 되는 모양을 표시 하는 대화 상자를 표시 합니다.|  
||<xref:System.Windows.Forms.FolderBrowserDialog> 컨트롤|사용자가 폴더를 찾아보고, 만들고, 선택할 수 있는 대화 상자를 표시 합니다.|  
||<xref:System.Windows.Forms.SaveFileDialog> 컨트롤|사용자가 파일을 저장할 수 있는 대화 상자를 표시 합니다.|  
|메뉴 컨트롤|<xref:System.Windows.Forms.MenuStrip> 컨트롤|사용자 지정 메뉴를 만듭니다. **참고:**  는 <xref:System.Windows.Forms.MenuStrip> <xref:System.Windows.Forms.MainMenu> 컨트롤을 대체 하도록 디자인 되었습니다.|  
||<xref:System.Windows.Forms.ContextMenuStrip> 컨트롤|사용자 지정 상황에 맞는 메뉴를 만듭니다. **참고:**  는 <xref:System.Windows.Forms.ContextMenuStrip> <xref:System.Windows.Forms.ContextMenu> 컨트롤을 대체 하도록 디자인 되었습니다.|  
|명령|<xref:System.Windows.Forms.Button> 컨트롤|프로세스를 시작, 중지 또는 중단 합니다.|  
||<xref:System.Windows.Forms.LinkLabel> 컨트롤|텍스트를 웹 스타일 링크로 표시 하 고 사용자가 특수 텍스트를 클릭 하면 이벤트를 트리거합니다. 일반적으로 텍스트는 다른 창이 나 웹 사이트에 대 한 링크입니다.|  
||<xref:System.Windows.Forms.NotifyIcon> 컨트롤|백그라운드에서 실행 중인 응용 프로그램을 나타내는 작업 표시줄의 상태 알림 영역에 아이콘을 표시 합니다.|  
||<xref:System.Windows.Forms.ToolStrip> 컨트롤|Microsoft Windows XP, Microsoft Office, Microsoft Internet Explorer, 사용자 지정 모양과 느낌, 테마를 포함 하거나 포함 하지 않고 오버플로 및 런타임 항목 다시 정렬을 지 원하는 도구 모음을 만듭니다. **참고:**  컨트롤은 <xref:System.Windows.Forms.ToolBar> 컨트롤을 대체 하도록 디자인 되었습니다. <xref:System.Windows.Forms.ToolStrip>|  
|사용자 도움말|<xref:System.Windows.Forms.HelpProvider> 구성 요소|컨트롤에 대한 팝업 또는 온라인 도움말을 제공합니다.|  
||<xref:System.Windows.Forms.ToolTip> 구성 요소|사용자가 컨트롤에 포인터를 놓을 때 컨트롤의 용도에 대 한 간단한 설명을 표시 하는 팝업 창을 제공 합니다.|  
|다른 컨트롤 그룹화|<xref:System.Windows.Forms.Panel> 컨트롤|레이블 없는 스크롤 가능한 프레임에서 컨트롤 집합을 그룹화 합니다.|  
||<xref:System.Windows.Forms.GroupBox> 컨트롤|레이블이 지정 된 비스크롤형 frame의 컨트롤 집합 (예: 라디오 단추)을 그룹화 합니다.|  
||<xref:System.Windows.Forms.TabControl> 컨트롤|그룹화 된 개체를 효율적으로 구성 하 고 액세스할 때 사용할 탭 페이지를 제공 합니다.|  
||<xref:System.Windows.Forms.SplitContainer> 컨트롤|이동 가능한 막대로 구분 된 두 개의 패널을 제공 합니다. **참고:**  컨트롤은 <xref:System.Windows.Forms.Splitter> 컨트롤을 대체 하도록 디자인 되었습니다. <xref:System.Windows.Forms.SplitContainer>|  
||<xref:System.Windows.Forms.TableLayoutPanel> 컨트롤|행과 열로 구성된 표로 내용을 동적으로 레이아웃하는 패널을 나타냅니다.|  
||<xref:System.Windows.Forms.FlowLayoutPanel> 컨트롤|가로 또는 세로로 해당 내용을 동적으로 펼쳐지는 패널을 나타냅니다.|  
|오디오|<xref:System.Media.SoundPlayer> 컨트롤|.Wav 형식의 소리 파일을 재생 합니다. 소리를 비동기적으로 로드 하거나 재생할 수 있습니다.|  
  
## <a name="superseded-controls-and-components-by-function"></a>함수로 대체 된 컨트롤 및 구성 요소  
  
|함수|대체 된 컨트롤|권장 대체|  
|--------------|------------------------|-----------------------------|  
|데이터 표시|<xref:System.Windows.Forms.DataGrid>|<xref:System.Windows.Forms.DataGridView>|  
|정보 표시 (읽기 전용 컨트롤)|<xref:System.Windows.Forms.StatusBar>|<xref:System.Windows.Forms.StatusStrip>|  
|메뉴 컨트롤|<xref:System.Windows.Forms.ContextMenu>|<xref:System.Windows.Forms.ContextMenuStrip>|  
||<xref:System.Windows.Forms.MainMenu>|<xref:System.Windows.Forms.MenuStrip>|  
|명령|<xref:System.Windows.Forms.ToolBar>|<xref:System.Windows.Forms.ToolStrip>|  
||<xref:System.Windows.Forms.StatusBar>|<xref:System.Windows.Forms.StatusStrip>|  
|폼 레이아웃|<xref:System.Windows.Forms.Splitter>|<xref:System.Windows.Forms.SplitContainer>|  
  
## <a name="see-also"></a>참고자료

- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
- [.NET Framework에서 사용자 지정 Windows Forms 컨트롤 개발](developing-custom-windows-forms-controls.md)
