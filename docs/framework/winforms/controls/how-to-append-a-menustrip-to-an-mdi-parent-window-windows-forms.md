---
title: '방법: (Windows Forms) MDI 부모 창에 MenuStrip 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- MenuStrip control [Windows Forms], merging
- MenuStrip control [Windows Forms], appending
- MDI [Windows Forms], merging menu items
ms.assetid: ab70c936-b452-4653-b417-17be57bb795b
ms.openlocfilehash: fdd5a24d444e494caedeed56402658399e97b90a
ms.sourcegitcommit: 518e7634b86d3980ec7da5f8c308cc1054daedb7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2019
ms.locfileid: "66457502"
---
# <a name="how-to-append-a-menustrip-to-an-mdi-parent-window-windows-forms"></a>방법: (Windows Forms) MDI 부모 창에 MenuStrip 추가
일부 애플리케이션에서는 MDI(다중 문서 인터페이스) 자식 창의 종류가 MDI 부모 창과 다를 수 있습니다. 예를 들어 MDI 부모는 스프레드시트이고 MDI 자식은 차트일 수 있습니다. 이 경우 다른 종류의 MDI 자식 창이 활성화될 때 MDI 부모 메뉴의 내용을 MDI 자식 메뉴의 내용으로 업데이트하려고 합니다.  
  
 다음 절차에서는 <xref:System.Windows.Forms.Form.IsMdiContainer%2A>, <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>, <xref:System.Windows.Forms.MergeAction> 및 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 속성을 사용하여 MDI 자식 메뉴를 MDI 부모 메뉴에 추가합니다. MDI 자식 창을 닫으면 MDI 부모에서 추가된 메뉴가 제거됩니다.  
  
 도 참조 하세요 [다중 문서 MDI (인터페이스) 응용 프로그램](../advanced/multiple-document-interface-mdi-applications.md)합니다.  
  
### <a name="to-append-a-menu-item-to-an-mdi-parent"></a>MDI 부모에 메뉴 항목을 추가하려면  
  
1. 폼을 만들고 해당 <xref:System.Windows.Forms.Form.IsMdiContainer%2A> 속성을 `true`로 설정합니다.  
  
2. `Form1`에 <xref:System.Windows.Forms.MenuStrip>을 추가하고 <xref:System.Windows.Forms.MenuStrip>의 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 속성을 `true`로 설정합니다.  
  
3. `Form1`<xref:System.Windows.Forms.MenuStrip>의 <xref:System.Windows.Forms.ToolStripItem.Visible%2A> 속성을 `false`로 설정합니다.  
  
4. `Form1`<xref:System.Windows.Forms.MenuStrip>에 최상위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.Control.Text%2A> 속성을 `&File`로 설정합니다.  
  
5. `&File` 메뉴 항목에 하위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.Form.Text%2A> 속성을 `&Open`로 설정합니다.  
  
6. 프로젝트에 폼을 추가하고, 폼에 <xref:System.Windows.Forms.MenuStrip>을 추가한 다음 `Form2`<xref:System.Windows.Forms.MenuStrip>의 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 속성을 `true`로 설정합니다.  
  
7. `Form2`<xref:System.Windows.Forms.MenuStrip>에 최상위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.Form.Text%2A> 속성을 `&Special`로 설정합니다.  
  
8. `&Special` 메뉴 항목에 두 개의 하위 메뉴 항목을 추가하고 해당 <xref:System.Windows.Forms.Form.Text%2A> 속성을 각각 `Command&1` 및 `Command&2`로 설정합니다.  
  
9. `&Special`, `Command&1` 및 `Command&2` 메뉴 항목의 <xref:System.Windows.Forms.MergeAction> 속성을 <xref:System.Windows.Forms.MergeAction.Append>로 설정합니다.  
  
10. 이벤트 처리기를 만듭니다는 <xref:System.Windows.Forms.Control.Click> 의 이벤트를 `&Open` <xref:System.Windows.Forms.ToolStripMenuItem>합니다.  
  
11. 이벤트 처리기 내에서 다음 코드 예제와 비슷한 코드를 삽입하여 `Form2`의 새 인스턴스를 만들고 `Form1`의 MDI 자식으로 표시합니다.  
  
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
    this.openToolStripMenuItem.Click += new System.EventHandler(this.openToolStripMenuItem_Click);  
    ```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- `Form1` 및 `Form2`라는 두 개의 <xref:System.Windows.Forms.Form> 컨트롤  
  
- `menuStrip1`이라는 `Form1`의 <xref:System.Windows.Forms.MenuStrip> 컨트롤 및 `menuStrip2`라는 `Form2`의 <xref:System.Windows.Forms.MenuStrip> 컨트롤  
  
- <xref:System?displayProperty=nameWithType> 및 <xref:System.Windows.Forms?displayProperty=nameWithType> 어셈블리에 대한 참조
