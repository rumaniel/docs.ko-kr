---
title: '방법: MDI 자식 양식 만들기'
ms.date: 03/30/2017
dev_langs:
- CSharp
- CPP
- VB
helpviewer_keywords:
- MDI [Windows Forms], creating forms
- child forms
ms.assetid: 164b69bb-2eca-4339-ada3-0679eb2c6dda
ms.openlocfilehash: f5e8682caf658d159f044528f040b99676355448
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040110"
---
# <a name="how-to-create-mdi-child-forms"></a>방법: MDI 자식 폼 만들기

MDI 자식 폼은 [mdi (다중 문서 인터페이스) 응용 프로그램](multiple-document-interface-mdi-applications.md)의 필수적인 요소 이며, 이러한 폼은 사용자 상호 작용의 중심입니다.

다음 절차에서는 Visual Studio를 사용 하 여 대부분의 단어 처리 응용 프로그램 처럼 <xref:System.Windows.Forms.RichTextBox> 컨트롤을 표시 하는 MDI 자식 폼을 만듭니다. 컨트롤을 <xref:System.Windows.Forms.DataGridView> 컨트롤 <xref:System.Windows.Forms> , 컨트롤 등의 다른 컨트롤로 대체 하 여 다양 한 가능성을 가진 mdi 자식 창 (확장, mdi 응용 프로그램)을 만들 수 있습니다.

## <a name="create-mdi-child-forms"></a>MDI 자식 폼 만들기

1. Visual Studio에서 새 Windows Forms 응용 프로그램 프로젝트를 만듭니다. 폼의 **속성** 창에서 해당 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> `WindowsState` 속성을로 `true` 설정 하 고 속성을로 `Maximized`설정 합니다.

   그러면 폼이 자식 창의 MDI 컨테이너로 지정됩니다.

2. `Toolbox`에서 <xref:System.Windows.Forms.MenuStrip> 컨트롤을 폼으로 끌어서 놓습니다. 해당 `Text` 속성을 **File**로 설정 합니다.

3. **항목** 속성 옆에 있는 줄임표 (...)를 클릭 하 고 **추가** 를 클릭 하 여 두 개의 자식 도구 스트립 메뉴 항목을 추가 합니다. 이러한 항목에 대 한 속성을New및Window로설정`Text` 합니다.

4. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.

5. **새 항목 추가** 대화 상자에서 **템플릿** 창에서 **Windows Form** (Visual Basic 또는 시각적 개체 C#) 또는 **Windows Forms 응용 프로그램 (.net)** (visual C++)을 선택 합니다. **이름** 상자에서 폼의 이름을 **Form2**로 합니다. **열기** 를 선택 하 여 프로젝트에 양식을 추가 합니다.

    > [!NOTE]
    > 이 단계에서 만든 MDI 자식 폼은 표준 Windows Form입니다. 따라서 폼의 투명도를 제어할 수 있는 <xref:System.Windows.Forms.Form.Opacity%2A> 속성이 있습니다. 그러나 <xref:System.Windows.Forms.Form.Opacity%2A> 속성은 최상위 창에 사용하도록 설계되었습니다. 그리기 문제가 발생할 수 있으므로 MDI 자식 폼에는 사용하지 마세요.

     이 폼은 MDI 자식 폼에 대한 템플릿이 됩니다.

     **Windows Forms 디자이너** 열리고 **Form2**가 표시 됩니다.

6. **도구 상자**에서 **RichTextBox** 컨트롤을 폼으로 끌어 옵니다.

7. 속성 창 에서 `Anchor` 속성 `Dock` 을 **Top, Left** 로, 속성을 **Fill**로 설정 합니다.

   이렇게 하면 폼의 크기를 조정하는 경우에도 <xref:System.Windows.Forms.RichTextBox> 컨트롤이 MDI 자식 폼의 영역을 완전히 채웁니다.

8. **새** 메뉴 항목을 두 번 클릭 하 여 <xref:System.Windows.Forms.Control.Click> 해당 항목에 대 한 이벤트 처리기를 만듭니다.

9. 사용자가 **새** 메뉴 항목을 클릭할 때 새 MDI 자식 폼을 만들기 위해 다음과 유사한 코드를 삽입 합니다.

   > [!NOTE]
   > 다음 예제에서는 이벤트 처리기가 `MenuItem2`에 대한 <xref:System.Windows.Forms.Control.Click> 이벤트를 처리합니다. 응용 프로그램 아키텍처의 세부 사항에 따라 **새** 메뉴 항목이 아닐 수 있습니다 `MenuItem2`.

    ```vb
    Protected Sub MDIChildNew_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MenuItem2.Click
       Dim NewMDIChild As New Form2()
       'Set the Parent Form of the Child window.
       NewMDIChild.MdiParent = Me
       'Display the new form.
       NewMDIChild.Show()
    End Sub
    ```

    ```csharp
    protected void MDIChildNew_Click(object sender, System.EventArgs e){
       Form2 newMDIChild = new Form2();
       // Set the Parent Form of the Child window.
       newMDIChild.MdiParent = this;
       // Display the new form.
       newMDIChild.Show();
    }
    ```

    ```cpp
    private:
       void menuItem2_Click(System::Object ^ sender,
          System::EventArgs ^ e)
       {
          Form2^ newMDIChild = gcnew Form2();
          // Set the Parent Form of the Child window.
          newMDIChild->MdiParent = this;
          // Display the new form.
          newMDIChild->Show();
       }
    ```

   에서 C++Form1의 맨 위에 `#include` 다음 지시문을 추가 합니다.

   ```cpp
   #include "Form2.h"
   ```

10. **속성** 창의 맨 위에 있는 드롭다운 목록에서 **파일** 메뉴 스트립에 해당 하는 메뉴 스트립을 선택 하 고 속성을 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 창 <xref:System.Windows.Forms.ToolStripMenuItem>으로 설정 합니다.

    이렇게 하면 **창** 메뉴에서 활성 자식 창 옆에 확인 표시가 있는 열려 있는 MDI 자식 창 목록을 유지 관리할 수 있습니다.

11. **F5** 키를 눌러 응용 프로그램을 실행합니다. **파일** 메뉴에서 **새로** 만들기를 선택 하 여 **창** 메뉴 항목에서 추적 되는 새 MDI 자식 폼을 만들 수 있습니다.

    > [!NOTE]
    > MDI 자식 폼이 <xref:System.Windows.Forms.MainMenu> 구성 요소(일반적으로 메뉴 항목의 메뉴 구조 사용)를 포함하고 <xref:System.Windows.Forms.MainMenu> 구성 요소(일반적으로 메뉴 항목의 메뉴 구조 사용)가 있는 MDI 부모 폼 내에서 열린 경우 <xref:System.Windows.Forms.MenuItem.MergeType%2A> 속성(및 필요에 따라 <xref:System.Windows.Forms.MenuItem.MergeOrder%2A> 속성)을 설정했으면 메뉴 항목이 자동으로 병합됩니다. 두 <xref:System.Windows.Forms.MainMenu> 구성 요소와 자식 폼의 모든 메뉴 항목에 대한 <xref:System.Windows.Forms.MenuItem.MergeType%2A> 속성을 <xref:System.Windows.Forms.MenuMerge.MergeItems>로 설정합니다. 또한 두 메뉴의 메뉴 항목이 원하는 순서대로 표시되도록 <xref:System.Windows.Forms.MenuItem.MergeOrder%2A> 속성을 설정합니다. MDI 부모 폼을 닫을 경우 MDI 부모에 대한 <xref:System.Windows.Forms.Form.Closing> 이벤트가 발생하기 전에 각 MDI 자식 폼에서 <xref:System.Windows.Forms.Form.Closing> 이벤트가 발생합니다. MDI 자식의 <xref:System.Windows.Forms.Form.Closing> 이벤트를 취소해도 MDI 부모의 <xref:System.Windows.Forms.Form.Closing> 이벤트가 발생하지 않도록 방지되지는 않습니다. 그러나 MDI 부모의 <xref:System.Windows.Forms.Form.Closing> 이벤트에 대한 <xref:System.ComponentModel.CancelEventArgs> 인수가 이제 `true`로 설정됩니다. <xref:System.ComponentModel.CancelEventArgs> 인수를 `false`로 설정하여 MDI 부모 및 모든 MDI 자식 폼을 강제로 닫을 수 있습니다.

## <a name="see-also"></a>참고자료

- [MDI(다중 문서 인터페이스) 응용 프로그램](multiple-document-interface-mdi-applications.md)
- [방법: MDI 부모 폼 만들기](how-to-create-mdi-parent-forms.md)
- [방법: 활성 MDI 자식 확인](how-to-determine-the-active-mdi-child.md)
- [방법: 활성 MDI 자식으로 데이터 보내기](how-to-send-data-to-the-active-mdi-child.md)
- [방법: MDI 자식 폼 정렬](how-to-arrange-mdi-child-forms.md)
