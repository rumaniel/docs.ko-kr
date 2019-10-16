---
title: '연습: 전문적인 스타일의 ToolStrip 컨트롤 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStripProfessionalRenderer class [Windows Forms]
- ToolStripRenderer class [Windows Forms]
- toolbars [Windows Forms], walkthroughs
- ToolStrip control [Windows Forms], creating professionally styled controls
ms.assetid: b52339ae-f1d3-494e-996e-eb455614098a
ms.openlocfilehash: 226e805d0240236899ee0cc290f1060a3b0aa391
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211766"
---
# <a name="walkthrough-creating-a-professionally-styled-toolstrip-control"></a>연습: 전문적인 스타일의 ToolStrip 컨트롤 만들기

응용 프로그램을 제공할 수 있습니다 <xref:System.Windows.Forms.ToolStrip> 에서 파생 된 고유한 클래스를 작성 하 여 전문적인 모양 및 동작을 제어 합니다 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 형식입니다.

이 연습에 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Forms.ToolStrip> 와 비슷한 복합 컨트롤을 만드는 컨트롤을 **탐색 창** Microsoft® Outlook®에서 제공 합니다. 다음 태스크를이 연습에 설명 되어 있습니다.

- Windows 컨트롤 라이브러리 프로젝트를 만드는 중입니다.

- StackView 컨트롤을 디자인 합니다.

- 사용자 지정 렌더러를 구현 합니다.

작업을 완료 하는 경우에 전문적인 모양의 Microsoft Office® XP 컨트롤을 사용 하 여 재사용 가능한 사용자 지정 클라이언트 컨트롤을 해야 합니다.

이 항목의 코드를 단일 목록으로 복사하려면 [방법: 전문적인 스타일의 ToolStrip 컨트롤 만들기](how-to-create-a-professionally-styled-toolstrip-control.md)합니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료 하려면 Visual Studio를 해야 합니다.

## <a name="create-the-control-library-project"></a>컨트롤 라이브러리 프로젝트를 만들려면

1. Visual Studio에서 라는 새 Windows 컨트롤 라이브러리 프로젝트를 만들 `StackViewLibrary`합니다.

2. **솔루션 탐색기**, 선택한 언어에 따라 "UserControl1.cs" 또는 "UserControl1.vb" 라는 소스 파일을 삭제 하 여 프로젝트의 기본 컨트롤을 삭제 합니다.

     자세한 내용은 [방법: 제거, 삭제 및 항목을 제외](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0ebzhwsk(v=vs.100))합니다.

3. 새 <xref:System.Windows.Forms.UserControl> 항목을 **StackViewLibrary** 프로젝트입니다. 새 소스 파일의 기본 이름을 지정 `StackView`합니다.

## <a name="design-the-stackview-control"></a>StackView 컨트롤 디자인

합니다 `StackView` 자식이 하나를 사용 하 여 복합 컨트롤 <xref:System.Windows.Forms.ToolStrip> 제어 합니다. 복합 컨트롤에 대 한 자세한 내용은 참조 하세요. [종류의 사용자 지정 컨트롤](varieties-of-custom-controls.md)합니다.

1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 디자인 화면입니다.

2. 에 **속성** 창에서 <xref:System.Windows.Forms.ToolStrip> 다음 표에 따라 컨트롤의 속성입니다.

    |속성|값|
    |--------------|-----------|
    |이름|`stackStrip`|
    |CanOverflow|`false`|
    |도킹|<xref:System.Windows.Forms.DockStyle.Bottom>|
    |글꼴|`Tahoma, 10pt, style=Bold`|
    |GripStyle|<xref:System.Windows.Forms.ToolStripGripStyle.Hidden>|
    |LayoutStyle|<xref:System.Windows.Forms.ToolStripLayoutStyle.VerticalStackWithOverflow>|
    |안쪽 여백|`0, 7, 0, 0`|
    |RenderMode|<xref:System.Windows.Forms.ToolStripRenderMode.Professional>|

3. Windows Forms 디자이너를 클릭 합니다 <xref:System.Windows.Forms.ToolStrip> 컨트롤의 **추가** 단추를 추가 <xref:System.Windows.Forms.ToolStripButton> 에 `stackStrip` 컨트롤.

4. 에 **속성** 창에서 <xref:System.Windows.Forms.ToolStripButton> 다음 표에 따라 컨트롤의 속성입니다.

    |속성|값|
    |--------------|-----------|
    |이름|`mailStackButton`|
    |CheckOnClick|true|
    |CheckState|<xref:System.Windows.Forms.CheckState.Checked>|
    |DisplayStyle|<xref:System.Windows.Forms.ToolStripItemDisplayStyle.ImageAndText>|
    |ImageAlign|<xref:System.Drawing.ContentAlignment.MiddleLeft>|
    |ImageScaling|<xref:System.Windows.Forms.ToolStripItemImageScaling.None>|
    |ImageTransparentColor|`238, 238, 238`|
    |여백|`0, 0, 0, 0`|
    |안쪽 여백|`3, 3, 3, 3`|
    |텍스트|**Mail**|
    |TextAlign|<xref:System.Drawing.ContentAlignment.MiddleLeft>|

5. 세 개 이상에 대 한 7 단계를 반복 <xref:System.Windows.Forms.ToolStripButton> 컨트롤입니다.

     컨트롤 이름을 `calendarStackButton`하십시오 `contactsStackButton`, 및 `tasksStackButton`합니다. 값을 설정 합니다 <xref:System.Windows.Forms.Control.Text%2A> 속성을 **달력**, **연락처**, 및 **작업**, 각각.

## <a name="handle-events"></a>이벤트 처리

두 이벤트를 확인 해야 합니다 `StackView` 컨트롤이 올바르게 동작 합니다. 처리는 <xref:System.Windows.Forms.UserControl.Load> 컨트롤을 올바르게 배치 하는 이벤트입니다. 처리를 <xref:System.Windows.Forms.ToolStripItem.Click> 각각에 대 한 이벤트 <xref:System.Windows.Forms.ToolStripButton> 제공 하는 `StackView` 비슷합니다 상태 동작을 제어를 <xref:System.Windows.Forms.RadioButton> 컨트롤입니다.

1. Windows Forms 디자이너에서 선택 된 `StackView` 제어 합니다.

2. **속성** 창에서 **이벤트**를 클릭합니다.

3. Load 이벤트 생성에 두 번 클릭 하 여 `StackView_Load` 이벤트 처리기입니다.

4. `StackView_Load` 이벤트 처리기에서 다음 코드를 복사하여 붙여 넣습니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#3)]

5. Windows Forms 디자이너에서 선택 된 `mailStackButton` 제어 합니다.

6. **속성** 창에서 **이벤트**를 클릭합니다.

7. 클릭 이벤트를 두 번 클릭 합니다.

     Windows Forms 디자이너에서 생성 된 `mailStackButton_Click` 이벤트 처리기입니다.

8. 이름 바꾸기는 `mailStackButton_Click` 이벤트 처리기를 `stackButton_Click`입니다.

     자세한 내용은 [이름 바꾸기 리팩터링 코드 기호](/visualstudio/ide/reference/rename)합니다.

9. 다음 코드를 삽입 합니다 `stackButton_Click` 이벤트 처리기입니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#4)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#4)]

10. Windows Forms 디자이너에서 선택 된 `calendarStackButton` 제어 합니다.

11. 에 **속성** 창에서 클릭 이벤트로는 `stackButton_Click` 이벤트 처리기입니다.

12. 10 및 11 for 단계를 반복 합니다 `contactsStackButton` 고 `tasksStackButton` 컨트롤입니다.

## <a name="define-icons"></a>아이콘 정의

각 `StackView` 단추에 연결 된 아이콘입니다. 편의 위해 각 아이콘으로 표시 됩니다 Base64로 인코딩된 문자열로 전에 deserialize 되는 <xref:System.Drawing.Bitmap> 에서 만들어집니다. 프로덕션 환경에서 리소스로 비트맵 데이터를 저장 하 고 Windows Forms 디자이너에 아이콘이 나타납니다. 자세한 내용은 [방법: Windows Forms에 배경 이미지 추가](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/dff9f95f(v=vs.100))합니다.

1. 코드 편집기에서 다음 코드를 삽입 합니다 `StackView` 클래스 정의 합니다. 이 코드에 대 한 비트맵을 초기화 합니다 <xref:System.Windows.Forms.ToolStripButton> 아이콘입니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#2)]

2. 호출을 추가 합니다 `InitializeImages` 의 메서드는 `StackView` 클래스 생성자입니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]

## <a name="implement-a-custom-renderer"></a>사용자 지정 렌더러를 구현 합니다.

대부분의 요소를 사용자 지정할 수 있습니다 합니다 `StackView` 컨트롤에서 파생 되는 클래스를 구현 합니다 <xref:System.Windows.Forms.ToolStripRenderer> 클래스입니다. 이 절차에서는 구현를 <xref:System.Windows.Forms.ToolStripProfessionalRenderer> 그립을 사용자 지정 및 그라데이션 배경을 그리는 클래스는 <xref:System.Windows.Forms.ToolStripButton> 컨트롤입니다.

1. 다음 코드를 삽입 합니다 `StackView` 정의 제어 합니다.

     정의 대 한 합니다 `StackRenderer` 클래스를 재정의 하는 <xref:System.Windows.Forms.ToolStripRenderer.RenderGrip>, <xref:System.Windows.Forms.ToolStripRenderer.RenderToolStripBorder>, 및 <xref:System.Windows.Forms.ToolStripRenderer.RenderButtonBackground> 사용자 지정 모양을 생성 하는 방법.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#10)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#10)]

2. 에 `StackView` 컨트롤의 생성자의 새 인스턴스를 만듭니다를 `StackRenderer` 클래스 및이 인스턴스를 할당 합니다 `stackStrip` 컨트롤의 <xref:System.Windows.Forms.ToolStrip.Renderer%2A> 속성.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]

## <a name="test-the-stackview-control"></a>StackView 컨트롤 테스트

합니다 `StackView` 컨트롤에서 파생 되는 <xref:System.Windows.Forms.UserControl> 클래스입니다. 따라서 컨트롤을 테스트할 수 있습니다 합니다 **UserControl 테스트 컨테이너**합니다. 자세한 내용은 [방법: UserControl의 런타임 동작 테스트](how-to-test-the-run-time-behavior-of-a-usercontrol.md)합니다.

1. 키를 눌러 **F5** 프로젝트를 빌드하고 시작 합니다 **UserControl 테스트 컨테이너**합니다.

2. 단추 위로 포인터를 `StackView` 컨트롤을 선택한 상태로의 모양을 확인 하려면 단추를 클릭 합니다.

## <a name="next-steps"></a>다음 단계

이 연습에서는 전문적인 모양의 Office XP 컨트롤을 사용 하 여 재사용 가능한 사용자 지정 클라이언트 컨트롤을 만들었습니다. 사용할 수는 <xref:System.Windows.Forms.ToolStrip> 다양 한 용도로 다른 컨트롤의 패밀리:

- 사용 하 여 컨트롤에 대 한 바로 가기 메뉴를 만들 <xref:System.Windows.Forms.ContextMenuStrip>합니다. 자세한 내용은 [ContextMenu 구성 요소 개요](contextmenu-component-overview-windows-forms.md)합니다.

- 자동으로 채워진된 표준 메뉴를 사용 하 여 폼을 만듭니다. 자세한 내용은 [연습: 폼에 표준 메뉴 항목 제공](walkthrough-providing-standard-menu-items-to-a-form.md)합니다.

- 도킹 된 여러 문서 MDI (인터페이스) 양식을 만듭니다 <xref:System.Windows.Forms.ToolStrip> 컨트롤입니다. 자세한 내용은 [방법: 메뉴 병합 및 ToolStrip 컨트롤을 사용 하 여 MDI 폼 만들기](how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [ToolStrip 컨트롤](toolstrip-control-windows-forms.md)
- [방법: 폼에 표준 메뉴 항목 제공](how-to-provide-standard-menu-items-to-a-form.md)
