---
title: '방법: 디자이너를 사용하여 ToolBar 컨트롤에 단추 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- toolbars [Windows Forms], adding buttons
- ToolBar control [Windows Forms], adding buttons
- ToolBar control [Windows Forms], adding separators
- examples [Windows Forms], toolbars
- ToolBar control [Windows Forms], adding drop-down menus
ms.assetid: d9ce3040-3e21-4e2d-80ae-b430982b2db8
ms.openlocfilehash: 4d7a49633599aabc96153e4793e50c1a4d6d092d
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666211"
---
# <a name="how-to-add-buttons-to-a-toolbar-control-using-the-designer"></a>방법: 디자이너를 사용하여 ToolBar 컨트롤에 단추 추가

> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip> 컨트롤은 <xref:System.Windows.Forms.ToolBar> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.ToolBar> 컨트롤을 계속 유지하도록 선택할 수 있습니다.

<xref:System.Windows.Forms.ToolBar> 컨트롤의 정수 부분은 컨트롤에 추가 하는 단추입니다. 메뉴 명령에 쉽게 액세스 하는 데 사용할 수 있습니다. 또는 메뉴 구조에서 사용할 수 없는 사용자에 게 명령을 노출 하기 위해 응용 프로그램의 사용자 인터페이스의 다른 영역에 배치할 수 있습니다.

다음 절차에는 <xref:System.Windows.Forms.ToolBar> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

### <a name="to-add-buttons-at-design-time"></a>디자인 타임에 단추를 추가 하려면

1. <xref:System.Windows.Forms.ToolBar> 컨트롤을 선택합니다.

2. **속성** 창에서 <xref:System.Windows.Forms.ToolBar.Buttons%2A> 속성을 클릭 하 여 선택 하 고 Visual Studio 속성 창 의 줄임표![단추 (...) 단추를 클릭 하 여 ToolBarButton을 엽니다.](./media/visual-studio-ellipsis-button.png)  **컬렉션 편집기**입니다.

3. **추가** 및 **제거** 단추를 사용 하 여 <xref:System.Windows.Forms.ToolBar> 컨트롤에서 단추를 추가 하 고 제거 합니다.

4. 편집기의 오른쪽 창에 표시 되는 **속성** 창에서 개별 단추의 속성을 구성 합니다. 다음 표에서는 고려해 야 할 몇 가지 중요 한 속성을 보여 줍니다.

    |속성|설명|
    |--------------|-----------------|
    |<xref:System.Windows.Forms.ToolBarButton.DropDownMenu%2A>|드롭다운 도구 모음 단추에 표시할 메뉴를 설정 합니다. 도구 모음 단추의 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 속성은로 <xref:System.Windows.Forms.ToolBarButtonStyle.DropDownButton>설정 해야 합니다. 이 속성은 <xref:System.Windows.Forms.ContextMenu> 클래스의 인스턴스를 참조로 사용 합니다.|
    |<xref:System.Windows.Forms.ToolBarButton.PartialPush%2A>|토글 스타일 도구 모음 단추가 부분적으로 푸시되는 지 여부를 설정 합니다. 도구 모음 단추의 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 속성은로 <xref:System.Windows.Forms.ToolBarButtonStyle.ToggleButton>설정 해야 합니다.|
    |<xref:System.Windows.Forms.ToolBarButton.Pushed%2A>|토글 스타일 도구 모음 단추가 현재 푸시된 상태 인지 여부를 설정 합니다. 도구 모음 단추의 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 속성은 또는 <xref:System.Windows.Forms.ToolBarButtonStyle.PushButton>로 <xref:System.Windows.Forms.ToolBarButtonStyle.ToggleButton> 설정 해야 합니다.|
    |<xref:System.Windows.Forms.ToolBarButton.Style%2A>|도구 모음 단추의 스타일을 설정 합니다. 는 <xref:System.Windows.Forms.ToolBarButtonStyle> 열거형의 값 중 하나 여야 합니다.|
    |<xref:System.Windows.Forms.ToolBarButton.Text%2A>|단추에 표시 되는 텍스트 문자열입니다.|
    |<xref:System.Windows.Forms.ToolBarButton.ToolTipText%2A>|단추에 대 한 도구 설명으로 표시 되는 텍스트입니다.|

5. **확인** 을 클릭 하 여 대화 상자를 닫고 지정 된 패널을 만듭니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolBar>
- [방법: 도구 모음 단추의 아이콘 정의](how-to-define-an-icon-for-a-toolbar-button.md)
- [방법: 도구 모음 단추에 대 한 트리거 메뉴 이벤트](how-to-trigger-menu-events-for-toolbar-buttons.md)
- [ToolBar 컨트롤 개요](toolbar-control-overview-windows-forms.md)
- [ToolBar 컨트롤](toolbar-control-windows-forms.md)
