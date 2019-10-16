---
title: '연습: 메뉴 병합 및 ToolStrip 컨트롤을 사용하여 MDI 양식 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms]
- ToolStripPanel control [Windows Forms]
- MDI [Windows Forms], creating forms
- multiple document interface forms
- MDI forms
- ToolStrip control [Windows Forms]
- MDI forms [Windows Forms], creating
- MDI forms [Windows Forms], walkthroughs
ms.assetid: fbab4221-74af-42d0-bbf4-3c97f7b2e544
ms.openlocfilehash: 5853760231cbece27805923c009d83e16c9b0a5e
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211554"
---
# <a name="walkthrough-creating-an-mdi-form-with-menu-merging-and-toolstrip-controls"></a>연습: 메뉴 병합 및 ToolStrip 컨트롤을 사용하여 MDI 양식 만들기

<xref:System.Windows.Forms?displayProperty=nameWithType> 네임스페이스는 MDI(다중 문서 인터페이스) 애플리케이션을 지원하고 <xref:System.Windows.Forms.MenuStrip> 컨트롤은 메뉴 병합을 지원합니다. MDI 폼은 <xref:System.Windows.Forms.ToolStrip> 컨트롤일 수도 있습니다.

이 연습에 사용 하는 방법을 보여 줍니다. <xref:System.Windows.Forms.ToolStripPanel> MDI 폼을 사용 하 여 컨트롤입니다. 폼은 자식 메뉴와 메뉴 병합도 지원합니다. 다음 태스크를이 연습에 설명 되어 있습니다.

- Windows Forms 프로젝트를 만드는 중입니다.

- 양식에 대 한 주 메뉴를 만드는 중입니다. 메뉴의 실제 이름을 달라 집니다.

- 추가 합니다 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤을 **도구 상자**합니다.

- 자식 폼을 만드는 중입니다.

- 정렬 <xref:System.Windows.Forms.ToolStripPanel> z 순서를 기준으로 컨트롤입니다.

메뉴 병합 및 이동 가능한 지 원하는 MDI 폼 작업을 완료 하면 더 <xref:System.Windows.Forms.ToolStrip> 컨트롤입니다.

이 항목의 코드를 단일 목록으로 복사하려면 [방법: 메뉴 병합 및 ToolStrip 컨트롤을 사용 하 여 MDI 폼 만들기](how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)합니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료 하려면 Visual Studio를 해야 합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. Visual Studio에서 라는 Windows 응용 프로그램 프로젝트를 만듭니다 **MdiForm** (**파일** > **New** > **프로젝트**  >  **시각적 C#**  하거나 **Visual Basic** > **클래식 데스크톱**  >   **Windows Forms 응용 프로그램**).

2. Windows Forms 디자이너에서 폼을 선택 합니다.

3. 속성 창에서 값을 설정 합니다 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 에 `true`입니다.

## <a name="create-the-main-menu"></a>주 메뉴 만들기

MDI 부모 폼 주 메뉴를 포함합니다. 주 메뉴에 항목 이라는 하나의 메뉴 **창을**합니다. 사용 하 여 합니다 **창을** 메뉴 항목을 자식 폼을 만들 수 있습니다. 자식 폼의 메뉴 항목은 주 메뉴에 병합 됩니다.

1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.MenuStrip> 컨트롤을 폼으로 합니다.

2. 추가 <xref:System.Windows.Forms.ToolStripMenuItem> 에 <xref:System.Windows.Forms.MenuStrip> 제어 하 고 이름을 **창**합니다.

3. <xref:System.Windows.Forms.MenuStrip> 컨트롤을 선택합니다.

4. 속성 창에서 값을 설정 합니다 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 속성을 `ToolStripMenuItem1`입니다.

5. 하위 항목을 추가 합니다 **창을** 메뉴 항목을 선택한 후 이름을 하위 항목 **새로 만들기**합니다.

6. 속성 창에서 클릭 **이벤트**합니다.

7. 두 번 클릭 하 여 <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트입니다.

     Windows Forms 디자이너에 대 한 이벤트 처리기가 생성 된 <xref:System.Windows.Forms.ToolStripItem.Click> 이벤트입니다.

8. 이벤트 처리기에 다음 코드를 삽입 합니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.MdiForm#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.MdiForm#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/VB/Form1.vb#2)]

## <a name="add-the-toolstrippanel-control-to-the-toolbox"></a>ToolStripPanel 컨트롤을 도구 상자에 추가

사용 하는 경우 <xref:System.Windows.Forms.MenuStrip> 있어야 하는 MDI 폼을 사용 하 여 컨트롤을 <xref:System.Windows.Forms.ToolStripPanel> 제어 합니다. 추가 해야 합니다는 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤을 합니다 **도구 상자** Windows Forms 디자이너에서 MDI 폼을 만들려고 합니다.

1. 열기는 **도구 상자**를 클릭 하 고는 **모든 Windows Forms** 탭을 사용할 수 있는 Windows Forms 컨트롤을 표시 합니다.

2. 바로 가기 메뉴를 열고 마우스 오른쪽 단추로 클릭 **선택 항목**합니다.

3. 에 **도구 상자 항목 선택** 대화 상자에서 아래쪽으로 스크롤하여 합니다 **이름** 열을 찾을 때까지 **ToolStripPanel**합니다.

4. 확인란을 선택 **ToolStripPanel**를 클릭 하 고 **확인**합니다.

     합니다 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤에 표시 합니다 **도구 상자**합니다.

## <a name="create-a-child-form"></a>자식 폼 만들기

이 절차에서는 자체는 별도 자식 폼 클래스를 정의 합니다 <xref:System.Windows.Forms.MenuStrip> 제어 합니다. 이 폼에 대 한 메뉴 항목은 부모 폼의 설정과 병합 됩니다.

1. 라는 새 폼을 추가 `ChildForm` 프로젝트에 있습니다.

     자세한 내용은 [방법: Windows Forms 프로젝트에 추가](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/y2xxdce3(v=vs.100))합니다.

2. **도구 상자**를 끌어를 <xref:System.Windows.Forms.MenuStrip> 컨트롤을 자식 폼입니다.

3. 클릭 합니다 <xref:System.Windows.Forms.MenuStrip> 컨트롤의 스마트 태그 문자 모양 (![스마트 태그 문자 모양](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))를 선택한 후 **항목 편집**합니다.

4. 에 **항목 컬렉션 편집기** 대화 상자에서 새 <xref:System.Windows.Forms.ToolStripMenuItem> 라는 **ChildMenuItem** 자식 메뉴.

     자세한 내용은 [ToolStrip 항목 컬렉션 편집기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233643(v=vs.100))합니다.

## <a name="test-the-form"></a>형식 테스트

1. 키를 눌러 **F5** 컴파일 및 폼을 실행 합니다.

2. 클릭 합니다 **창을** 메뉴 항목 메뉴를 연 마우스 클릭 **새로 만들기**합니다.

     새 자식 폼을 폼의 MDI 클라이언트 영역에 생성 됩니다. 자식 폼의 메뉴가 주 메뉴와 병합 됩니다.

3. 자식 폼을 닫습니다.

     자식 폼의 메뉴가 주 메뉴에서 제거 됩니다.

4. 클릭 **새로 만들기** 여러 번입니다.

     자식 폼이 자동으로 나열 합니다 **창** 때문에 메뉴 항목는 <xref:System.Windows.Forms.MenuStrip> 컨트롤의 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 속성에 할당 됩니다.

## <a name="add-toolstrip-support"></a>ToolStrip 지원 추가

이 절차에서는 추가 4 <xref:System.Windows.Forms.ToolStrip> MDI 부모 폼에 컨트롤을 합니다. 각 <xref:System.Windows.Forms.ToolStrip> 컨트롤 내에 추가 되는 <xref:System.Windows.Forms.ToolStripPanel> 폼의 가장자리에 도킹 된 컨트롤입니다.

1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤을 폼으로 합니다.

2. 사용 하 여는 <xref:System.Windows.Forms.ToolStripPanel> 선택 컨트롤을 두 번 클릭 합니다 <xref:System.Windows.Forms.ToolStrip> 에서 제어를 **도구 상자**.

     A <xref:System.Windows.Forms.ToolStrip> 컨트롤에서 만드는 <xref:System.Windows.Forms.ToolStripPanel> 제어 합니다.

3. <xref:System.Windows.Forms.ToolStripPanel> 컨트롤을 선택합니다.

4. 속성 창에서 컨트롤의 값을 변경 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Left>입니다.

     <xref:System.Windows.Forms.ToolStripPanel> 주 메뉴 아래 폼의 왼쪽에 도킹을 제어 합니다. MDI 클라이언트 영역에 맞게 조정 된 <xref:System.Windows.Forms.ToolStripPanel> 제어 합니다.

5. 1 ~ 4 단계를 반복 합니다.

     새 도킹 <xref:System.Windows.Forms.ToolStripPanel> 폼의 맨 위에 컨트롤입니다.

     합니다 <xref:System.Windows.Forms.ToolStripPanel> 주 메뉴 아래 하지만 첫 번째 오른쪽이 컨트롤이 도킹 되 <xref:System.Windows.Forms.ToolStripPanel> 제어 합니다. 이 단계에서는 올바른 배치에 z-순서의 중요성을 보여 줍니다 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤입니다.

6. 두 개 이상에 대해 1 ~ 4 단계를 반복 <xref:System.Windows.Forms.ToolStripPanel> 컨트롤입니다.

     새 도킹 <xref:System.Windows.Forms.ToolStripPanel> 오른쪽 아래 폼의 컨트롤입니다.

## <a name="arrange-toolstrippanel-controls-by-z-order"></a>ToolStripPanel 컨트롤 Z 순서로 정렬

도킹 된 위치의 <xref:System.Windows.Forms.ToolStripPanel> MDI 폼의 컨트롤로 z-순서에서 컨트롤의 위치에 따라 결정 됩니다. 문서 개요 창에서 컨트롤의 z 순서를 쉽게 정렬할 수 있습니다.

1. 에 **보기** 메뉴에서 클릭 **다른 Windows**를 클릭 하 고 **문서 개요**합니다.

     배열에 <xref:System.Windows.Forms.ToolStripPanel> 이전 절차에서 컨트롤 표준이 아닙니다. 즉, z-순서가 잘못 되었습니다. 문서 개요 창 컨트롤의 z 순서를 변경 하려면 사용 합니다.

2. 문서 개요 창에서 선택 **ToolStripPanel4**합니다.

3. 아래쪽 화살표 단추를 클릭까지 반복 해 서 **ToolStripPanel4** 목록의 맨 아래에 합니다.

     합니다 **ToolStripPanel4** 컨트롤 다른 컨트롤 아래에 있는 폼의 아래쪽에 도킹 됩니다.

4. 선택 **ToolStripPanel2**합니다.

5. 컨트롤의 세 번째 위치 목록에서 아래쪽 화살표 단추를 한 번을 클릭 합니다.

     합니다 **ToolStripPanel2** 컨트롤 주 메뉴 아래 및 위의 다른 컨트롤을 폼의 위쪽에 도킹 됩니다.

6. 다양 한 컨트롤을 선택 합니다 **문서 개요** 창 z-순서에서 다른 위치로 이동 합니다. Z 순서 도킹 된 컨트롤의 배치에 미치는 note 합니다. CTRL + Z를 사용 하 여 또는 **실행 취소** 에 **편집** 변경 내용을 취소 하는 메뉴입니다.

## <a name="checkpoint---test-your-form"></a>검사점-폼 테스트

1. 키를 눌러 **F5** 컴파일 및 폼을 실행 합니다.

2. 그립을 클릭 한 <xref:System.Windows.Forms.ToolStrip> 컨트롤을 폼에 컨트롤을 다른 위치로 끌어 놓습니다.

     끌어 놓을 수 있습니다는 <xref:System.Windows.Forms.ToolStrip> 간에 제어 <xref:System.Windows.Forms.ToolStripPanel> 다른 컨트롤입니다.

## <a name="next-steps"></a>다음 단계

사용 하 여 MDI 부모 폼이 연습에서는 만든 <xref:System.Windows.Forms.ToolStrip> 컨트롤과 메뉴 병합 합니다. 사용할 수는 <xref:System.Windows.Forms.ToolStrip> 다양 한 용도로 다른 컨트롤의 패밀리:

- 사용 하 여 컨트롤에 대 한 바로 가기 메뉴를 만들 <xref:System.Windows.Forms.ContextMenuStrip>합니다. 자세한 내용은 [ContextMenu 구성 요소 개요](contextmenu-component-overview-windows-forms.md)합니다.

- 자동으로 채워진된 표준 메뉴를 사용 하 여 폼을 생성 합니다. 자세한 내용은 [연습: 폼에 표준 메뉴 항목 제공](walkthrough-providing-standard-menu-items-to-a-form.md)합니다.

- 제공에 <xref:System.Windows.Forms.ToolStrip> 전문적인 모양 제어 합니다. 자세한 내용은 [방법: 응용 프로그램에 대 한 ToolStrip 렌더러 설정](how-to-set-the-toolstrip-renderer-for-an-application.md)합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [방법: MDI 부모 폼 만들기](../advanced/how-to-create-mdi-parent-forms.md)
- [방법: MDI 자식 폼 만들기](../advanced/how-to-create-mdi-child-forms.md)
- [방법: MDI 드롭 다운 메뉴에 MenuStrip 삽입](how-to-insert-a-menustrip-into-an-mdi-drop-down-menu-windows-forms.md)
- [ToolStrip 컨트롤](toolstrip-control-windows-forms.md)
