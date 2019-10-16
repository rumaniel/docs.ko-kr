---
title: '연습: 양식에 표준 메뉴 항목 제공'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- menu items [Windows Forms], standard
- toolbars [Windows Forms], walkthroughs
- StatusStrip control [Windows Forms]
- ToolStrip control [Windows Forms]
ms.assetid: dac37d98-589e-4d6d-9673-6437e8943122
ms.openlocfilehash: ebfacadfee3ea069359a72ea0402751e9e6280d7
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211512"
---
# <a name="walkthrough-providing-standard-menu-items-to-a-form"></a>연습: 양식에 표준 메뉴 항목 제공

<xref:System.Windows.Forms.MenuStrip> 컨트롤을 사용하여 폼에 표준 메뉴를 제공할 수 있습니다.

이 연습에 사용 하는 방법을 보여 줍니다.는 <xref:System.Windows.Forms.MenuStrip> 표준 메뉴를 만들 수 있습니다. 사용자가 메뉴 항목을 선택 하는 경우에 폼 응답 합니다. 다음 태스크를이 연습에 설명 되어 있습니다.

- Windows Forms 프로젝트를 만드는 중입니다.

- 표준 메뉴를 만드는 중입니다.

- 만들기는 <xref:System.Windows.Forms.StatusStrip> 제어 합니다.

- 메뉴 항목 선택을 처리 합니다.

메뉴 항목 선택 항목을 표시 하는 표준 메뉴를 사용 하 여 폼을 완료 하면 더는 <xref:System.Windows.Forms.StatusStrip> 제어 합니다.

이 항목의 코드를 단일 목록으로 복사하려면 [방법: 폼에 표준 메뉴 항목 제공](how-to-provide-standard-menu-items-to-a-form.md)합니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료 하려면 Visual Studio를 해야 합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. Visual Studio에서 호출 하는 Windows 응용 프로그램 프로젝트를 만듭니다 **StandardMenuForm** (**파일** > **New** > **프로젝트**   >  **시각적 C#**  하거나 **Visual Basic** > **클래식 데스크톱**  >  **Windows Forms 응용 프로그램**).

2. Windows Forms 디자이너에서 폼을 선택 합니다.

## <a name="create-a-standard-menu"></a>표준 메뉴 만들기

Windows Forms 디자이너를 자동으로 채울 수는 <xref:System.Windows.Forms.MenuStrip> 표준 메뉴 항목을 사용 하 여 제어 합니다.

1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.MenuStrip> 컨트롤을 폼으로 합니다.

2. 클릭 합니다 <xref:System.Windows.Forms.MenuStrip> 컨트롤의 스마트 태그 문자 모양 (![스마트 태그 문자 모양](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph")) 선택한 **표준 항목 삽입**합니다.

     <xref:System.Windows.Forms.MenuStrip> 컨트롤이 표준 메뉴 항목으로 채워집니다.

3. 클릭 합니다 **파일** 메뉴 항목을 해당 기본 메뉴 항목 및 해당 아이콘을 참조 하세요.

## <a name="create-a-statusstrip-control"></a>StatusStrip 컨트롤 만들기

사용 된 <xref:System.Windows.Forms.StatusStrip> Windows Forms 응용 프로그램에 대 한 상태를 표시 하는 컨트롤입니다. 현재 예제에서는 사용자가 선택한 메뉴 항목에 표시 됩니다는 <xref:System.Windows.Forms.StatusStrip> 제어 합니다.

1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.StatusStrip> 컨트롤을 폼으로 합니다.

     <xref:System.Windows.Forms.StatusStrip> 컨트롤은 자동으로 폼의 아래쪽에 도킹 합니다.

2. 클릭 합니다 <xref:System.Windows.Forms.StatusStrip> 컨트롤의 드롭다운 단추를 선택 **statuslabel은** 추가할를 <xref:System.Windows.Forms.ToolStripStatusLabel> 컨트롤을 <xref:System.Windows.Forms.StatusStrip> 제어 합니다.

## <a name="handle-item-selection"></a>항목 선택을 처리합니다

처리는 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> 메뉴 항목을 선택할 때 응답할 이벤트입니다.

1. 클릭 합니다 **파일** 만들기에서 만든 메뉴 항목을 표준 메뉴 섹션.

2. **속성** 창에서 **이벤트**를 클릭합니다.

3. 두 번 클릭 하 여 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> 이벤트입니다.

     Windows Forms 디자이너에 대 한 이벤트 처리기가 생성 된 <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> 이벤트입니다.

4. 이벤트 처리기에 다음 코드를 삽입 합니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#3)]

5. 삽입 된 `UpdateStatus` 폼에 유틸리티 메서드 정의 합니다.

     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#2)]

## <a name="checkpoint--test-your-form"></a>검사점-폼 테스트

1. 키를 눌러 **F5** 컴파일 및 폼을 실행 합니다.

2. 클릭 합니다 **파일** 메뉴 항목 메뉴를 엽니다.

3. 에 **파일** 메뉴 선택 항목 중 하나를 클릭 합니다.

     <xref:System.Windows.Forms.StatusStrip> 컨트롤 선택한 항목을 표시 합니다.

## <a name="next-steps"></a>다음 단계

이 연습에서는 표준 메뉴가 있는 폼을 만들었습니다. 사용할 수는 <xref:System.Windows.Forms.ToolStrip> 다양 한 용도로 다른 컨트롤의 패밀리:

- 사용 하 여 컨트롤에 대 한 바로 가기 메뉴를 만들 <xref:System.Windows.Forms.ContextMenuStrip>합니다. 자세한 내용은 [ContextMenu 구성 요소 개요](contextmenu-component-overview-windows-forms.md)합니다.

- 도킹 된 여러 문서 MDI (인터페이스) 양식을 만듭니다 <xref:System.Windows.Forms.ToolStrip> 컨트롤입니다. 자세한 내용은 [연습: 메뉴 병합 및 ToolStrip 컨트롤을 사용 하 여 MDI 폼 만들기](walkthrough-creating-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)합니다.

- 제공에 <xref:System.Windows.Forms.ToolStrip> 전문적인 모양 제어 합니다. 자세한 내용은 [방법: 응용 프로그램에 대 한 ToolStrip 렌더러 설정](how-to-set-the-toolstrip-renderer-for-an-application.md)합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [MenuStrip 컨트롤](menustrip-control-windows-forms.md)
