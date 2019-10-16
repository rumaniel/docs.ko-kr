---
title: '방법: 디자이너를 사용하여 도구 모음 단추에 대한 아이콘 정의'
ms.date: 03/30/2017
helpviewer_keywords:
- toolbars [Windows Forms], adding icons to buttons
- examples [Windows Forms], toolbars
- images [Windows Forms], toolbar buttons
- buttons [Windows Forms], images
- icons [Windows Forms], toolbar buttons
- ToolBar control [Windows Forms], adding icons to buttons
ms.assetid: d848f38e-67f2-49d4-8e88-01c845c06c02
ms.openlocfilehash: 49e93f12bebbf409e6b3a06634556b9103c85f44
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666199"
---
# <a name="how-to-define-an-icon-for-a-toolbar-button-using-the-designer"></a>방법: 디자이너를 사용하여 도구 모음 단추에 대한 아이콘 정의

> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip> 컨트롤은 <xref:System.Windows.Forms.ToolBar> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.ToolBar> 컨트롤을 계속 유지하도록 선택할 수 있습니다.

<xref:System.Windows.Forms.ToolBar>사용자가 쉽게 식별할 수 있도록 단추 내에 아이콘을 표시할 수 있습니다. 이는 <xref:System.Windows.Forms.ImageList> 구성 요소에 이미지를 추가 하 고 <xref:System.Windows.Forms.ToolBar> 컨트롤에 연결 하는 과정을 통해 이루어집니다.

다음 절차에는 <xref:System.Windows.Forms.ToolBar> 컨트롤과 <xref:System.Windows.Forms.ImageList> 구성 요소를 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

### <a name="to-set-an-icon-for-a-toolbar-button-at-design-time"></a>디자인 타임에 도구 모음 단추에 대 한 아이콘을 설정 하려면

1. <xref:System.Windows.Forms.ImageList> 구성 요소에 이미지를 추가 합니다. 자세한 내용은 [방법: 디자이너](how-to-add-or-remove-imagelist-images-with-the-designer.md)를 사용 하 여 ImageList 이미지를 추가 하거나 제거 합니다.

2. 폼에서 <xref:System.Windows.Forms.ToolBar> 컨트롤을 선택 합니다.

3. **속성** 창에서 <xref:System.Windows.Forms.ToolBar> 컨트롤 <xref:System.Windows.Forms.ToolBar.ImageList%2A> 의속성을구성요소로설정합니다.<xref:System.Windows.Forms.ImageList>

4. ![](./media/visual-studio-ellipsis-button.png)컨트롤의 <xref:System.Windows.Forms.ToolBar.Buttons%2A> 속성을 클릭 하 여 선택 하 고 줄임표 (Visual Studio 속성 창의 줄임표 단추 (...) 단추를 클릭 하 여 ToolBarButton 컬렉션 편집기를 엽니다. <xref:System.Windows.Forms.ToolBar>

5. **추가** 단추를 사용 하 여 <xref:System.Windows.Forms.ToolBar> 컨트롤에 단추를 추가 합니다.

6. **ToolBarButton 컬렉션 편집기**의 오른쪽 창에 표시 되는 <xref:System.Windows.Forms.ToolBarButton.ImageIndex%2A> **속성** 창에서 각 도구 모음 단추의 속성을 목록에 있는 값 중 하나로 설정 합니다 .이 값은에 추가 된 이미지에서가져옵니다.<xref:System.Windows.Forms.ImageList> 구성 요소.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolBar>
- [방법: 도구 모음 단추에 대 한 트리거 메뉴 이벤트](how-to-trigger-menu-events-for-toolbar-buttons.md)
- [ToolBar 컨트롤](toolbar-control-windows-forms.md)
- [ImageList 구성 요소](imagelist-component-windows-forms.md)
