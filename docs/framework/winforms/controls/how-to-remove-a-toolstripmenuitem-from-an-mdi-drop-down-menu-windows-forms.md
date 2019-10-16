---
title: '방법: (Windows Forms) MDI 드롭 다운 메뉴에서 ToolStripMenuItem 제거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- menu items [Windows Forms], removing from MDI drop-down menus
- MenuStrip control [Windows Forms], merging
- MenuStrip control [Windows Forms], removing
- MDI [Windows Forms], merging menu items
ms.assetid: bdafe60d-82ee-45bc-97fe-eeefca6e54c1
ms.openlocfilehash: 378410977c31a446b34bf907dfd438a2a799c84a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662301"
---
# <a name="how-to-remove-a-toolstripmenuitem-from-an-mdi-drop-down-menu-windows-forms"></a>방법: (Windows Forms) MDI 드롭 다운 메뉴에서 ToolStripMenuItem 제거
일부 애플리케이션에서는 MDI(다중 문서 인터페이스) 자식 창의 종류가 MDI 부모 창과 다를 수 있습니다. 예를 들어 MDI 부모는 스프레드시트이고 MDI 자식은 차트일 수 있습니다. 이 경우 다른 종류의 MDI 자식 창이 활성화될 때 MDI 부모 메뉴의 내용을 MDI 자식 메뉴의 내용으로 업데이트하려고 합니다.  
  
 다음 절차에서는 합니다 <xref:System.Windows.Forms.Form.IsMdiContainer%2A>, <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>를 <xref:System.Windows.Forms.MergeAction>, 및 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> MDI 부모 메뉴의 드롭다운 부분에서 메뉴 항목을 제거 하는 속성입니다. MDI 자식 창을 닫으면 MDI 부모 메뉴에 제거 메뉴 항목을 복원 합니다.  
  
### <a name="to-remove-a-menustrip-from-an-mdi-drop-down-menu"></a>MDI 드롭 다운 메뉴에 MenuStrip를 제거 하려면  
  
1. 폼을 만들고 해당 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 속성을 `true`로 설정합니다.  
  
2. `Form1`에 <xref:System.Windows.Forms.MenuStrip>을 추가하고 <xref:System.Windows.Forms.MenuStrip>의 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 속성을 `true`로 설정합니다.  
  
3. `Form1`<xref:System.Windows.Forms.MenuStrip>에 최상위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.Control.Text%2A> 속성을 `&File`로 설정합니다.  
  
4. 세 하위 메뉴 항목을 추가 합니다 `&File` 메뉴 항목 집합과 해당 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 속성을 `&Open`를 `&Import from`, 및 `E&xit`합니다.  
  
5. 두 개의 하위 메뉴 항목을 추가 합니다 `&Import from` 하위 메뉴 항목 집합과 해당 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 속성을 `&Word` 및 `&Excel`합니다.  
  
6. 프로젝트에 폼을 추가하고, 폼에 <xref:System.Windows.Forms.MenuStrip>을 추가한 다음 `Form2`<xref:System.Windows.Forms.MenuStrip>의 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 속성을 `true`로 설정합니다.  
  
7. `Form2`<xref:System.Windows.Forms.MenuStrip>에 최상위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 속성을 `&File`로 설정합니다.  
  
8. 추가 `&Import from` 하위 메뉴 항목을 합니다 `&File` 의 메뉴 `Form2`, 추가 `&Word` 하위 메뉴 항목을는 `&File` 메뉴.  
  
9. 설정 합니다 <xref:System.Windows.Forms.MergeAction> 및 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 의 속성을 `Form2` 다음 표에 나와 있는 것 처럼 메뉴 항목.  
  
    |Form2 메뉴 항목|MergeAction 값|MergeIndex 값|  
    |---------------------|-----------------------|----------------------|  
    |파일|MatchOnly|-1|  
    |가져오기|MatchOnly|-1|  
    |단어|제거|-1|  
  
10. `Form1`에 대 한 이벤트 처리기를 만듭니다를 <xref:System.Windows.Forms.Control.Click> 이벤트를 `&Open` <xref:System.Windows.Forms.ToolStripMenuItem>합니다.  
  
11. 이벤트 처리기에서 만들고의 새 인스턴스를 표시 하려면 다음 코드 예제와 비슷한 코드를 삽입 `Form2` MDI 자식으로 `Form1`:  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
    ```  
  
    ```csharp  
    private void openToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
    ```  
  
12. `&Open`<xref:System.Windows.Forms.ToolStripMenuItem>에 다음 코드 예제와 비슷한 코드를 배치하여 이벤트 처리기를 등록합니다.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles openToolStripMenuItem.Click  
    ```  
  
    ```csharp  
    this.openToolStripMenuItem.Click += new _  
    System.EventHandler(this.openToolStripMenuItem_Click);  
    ```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `Form1` 및 `Form2`라는 두 개의 <xref:System.Windows.Forms.Form> 컨트롤  
  
- `menuStrip1`이라는 `Form1`의 <xref:System.Windows.Forms.MenuStrip> 컨트롤 및 `menuStrip2`라는 `Form2`의 <xref:System.Windows.Forms.MenuStrip> 컨트롤  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- [방법: MDI 부모 폼 만들기](../advanced/how-to-create-mdi-parent-forms.md)
- [방법: MDI 자식 폼 만들기](../advanced/how-to-create-mdi-child-forms.md)
- [MenuStrip 컨트롤 개요](menustrip-control-overview-windows-forms.md)
