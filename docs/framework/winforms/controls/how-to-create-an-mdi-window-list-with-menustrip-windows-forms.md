---
title: '방법: MenuStrip (Windows Forms)이 포함 된 MDI 창 목록 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- MDI [Windows Forms], creating window lists
- MenuStrip control [Windows Forms], creating window lists
ms.assetid: 04fb414b-811f-4a83-aab6-b4a24646dec5
ms.openlocfilehash: 229afc879be6407340e2fca6c3b2474475bcb5a6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64611964"
---
# <a name="how-to-create-an-mdi-window-list-with-menustrip-windows-forms"></a>방법: MenuStrip (Windows Forms)이 포함 된 MDI 창 목록 만들기
동일한 시간 및 복사에 열린 여러 문서 하 고 다른 한 문서에서 콘텐츠를 붙여 넣을 수 있는 응용 프로그램을 만들려면 (MDI) 다중 문서 인터페이스를 사용 합니다.  
  
 이 절차는 부모의 창 메뉴에 모든 활성 자식 폼 목록을 만드는 방법을 보여 줍니다.  
  
### <a name="to-create-an-mdi-window-list-on-a-menustrip"></a>MenuStrip에서 MDI 창 목록 만들기를  
  
1. 폼을 만들고 해당 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 속성을 `true`로 설정합니다.  
  
2. 폼에 <xref:System.Windows.Forms.MenuStrip>를 추가합니다.  
  
3. 두 개의 최상위 메뉴 항목을 추가 합니다 <xref:System.Windows.Forms.MenuStrip> 설정 및 해당 <xref:System.Windows.Forms.Control.Text%2A> 속성을 `&File` 및 `&Window`합니다.  
  
4. `&File` 메뉴 항목에 하위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 속성을 `&Open`로 설정합니다.  
  
5. 설정를 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 의 속성을 <xref:System.Windows.Forms.MenuStrip> 에 `&Window` <xref:System.Windows.Forms.ToolStripMenuItem>.  
  
6. 프로젝트에 폼을 추가 하 고 추가할 원하는 컨트롤 등 다른 <xref:System.Windows.Forms.MenuStrip>합니다.  
  
7. `&New`<xref:System.Windows.Forms.ToolStripMenuItem>의 <xref:System.Windows.Forms.Control.Click> 이벤트에 대한 이벤트 처리기를 만듭니다.  
  
8. 이벤트 처리기 내에서 만들고의 새 인스턴스를 표시 하려면 다음과 비슷한 코드를 삽입 `Form2` MDI 자식으로 `Form1`입니다.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As _  
    System.Object, ByVal e As System.EventArgs) Handles _  
    openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
    ```  
  
    ```csharp  
    private void newToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
    ```  
  
9. 다음과 같은 코드를 배치 합니다 `&New` <xref:System.Windows.Forms.ToolStripMenuItem> 이벤트 처리기를 등록 합니다.  
  
    ```vb  
    Private Sub newToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles newToolStripMenuItem.Click  
    ```  
  
    ```csharp  
    this.newToolStripMenuItem.Click += new System.EventHandler(this.newToolStripMenuItem_Click);  
    ```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `Form1` 및 `Form2`라는 두 개의 <xref:System.Windows.Forms.Form> 컨트롤  
  
- `menuStrip1`이라는 `Form1`의 <xref:System.Windows.Forms.MenuStrip> 컨트롤 및 `menuStrip2`라는 `Form2`의 <xref:System.Windows.Forms.MenuStrip> 컨트롤  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [방법: MDI 부모 폼 만들기](../advanced/how-to-create-mdi-parent-forms.md)
- [방법: MDI 자식 폼 만들기](../advanced/how-to-create-mdi-child-forms.md)
- [MenuStrip 컨트롤](menustrip-control-windows-forms.md)
