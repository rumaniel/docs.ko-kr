---
title: '방법: Windows Forms를 사용하여 다중 창 사용자 인터페이스 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SplitContainer control [Windows Forms], examples
- ListView control [Windows Forms], examples
- RichTextBox control [Windows Forms], examples
- Panel control [Windows Forms], examples
- TreeView control [Windows Forms], examples
- Splitter control [Windows Forms], examples
ms.assetid: e79f6bcc-3740-4d1e-b46a-c5594d9b7327
ms.openlocfilehash: 8650ba3b8011e50779080e31d94727609f2d08f1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61747097"
---
# <a name="how-to-create-a-multipane-user-interface-with-windows-forms"></a>방법: Windows Forms를 사용하여 다중 창 사용자 인터페이스 만들기
다음 절차를 사용 하 여 Microsoft Outlook에서 사용 하는 비슷한 다중 창 사용자 인터페이스를 만듭니다는 **폴더** 목록에는 **메시지** 창 및 **미리보기** 창입니다. 이 정렬 폼에 컨트롤을 도킹을 통해 주로 수행 됩니다.  
  
 컨트롤을 고정 하면 부모 컨테이너의 가장자리 컨트롤은 고정 시킬 확인할 수 있습니다. 따라서 설정 하는 경우는 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Right>, 컨트롤의 오른쪽 가장자리 부모 컨트롤의 오른쪽 가장자리에 도킹 됩니다. 또한 컨트롤의 도킹된 가장자리 컨테이너 컨트롤과의 일치 하도록 크기가 조정 됩니다. 방법에 대 한 자세한 내용은 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 속성을 참조 하십시오 [방법: Windows Forms에서 컨트롤을 도킹](how-to-dock-controls-on-windows-forms.md)합니다.  
  
 정렬에 중점을 두고이 절차는 <xref:System.Windows.Forms.SplitContainer> 및 기타 컨트롤이 폼에, 응용 프로그램을 Microsoft Outlook을 모방 하는 기능을 추가 하는 방법에 없습니다.  
  
 내에서 모든 컨트롤을 배치 하면이 사용자 인터페이스를 만들려면를 <xref:System.Windows.Forms.SplitContainer> 포함 하는 컨트롤을 <xref:System.Windows.Forms.TreeView> 왼쪽 패널에서 컨트롤입니다. 오른쪽 패널을 <xref:System.Windows.Forms.SplitContainer> 컨트롤에 두 번째 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 <xref:System.Windows.Forms.ListView> 컨트롤 위의 <xref:System.Windows.Forms.RichTextBox> 컨트롤. 이러한 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 폼에 다른 컨트롤의 독립적인 크기 조정을 사용 합니다. 자신만의 사용자 지정 사용자 인터페이스를 작성 하는이 절차에 설명 된 기술을 조정할 수 있습니다.  
  
### <a name="to-create-an-outlook-style-user-interface-programmatically"></a>Outlook 스타일 사용자 인터페이스를 프로그래밍 방식으로 만들려면  
  
1. 양식 내에서 사용자 인터페이스를 구성 하는 각 컨트롤을 선언 합니다. 예를 들어 사용 합니다 <xref:System.Windows.Forms.TreeView>, <xref:System.Windows.Forms.ListView>, <xref:System.Windows.Forms.SplitContainer>, 및 <xref:System.Windows.Forms.RichTextBox> Microsoft Outlook 사용자 인터페이스를 모방 하기 위해 컨트롤입니다.  
  
    ```vb  
    Private WithEvents treeView1 As System.Windows.Forms.TreeView  
    Private WithEvents listView1 As System.Windows.Forms.ListView  
    Private WithEvents richTextBox1 As System.Windows.Forms.RichTextBox  
    Private WithEvents splitContainer1 As _  
        System.Windows.Forms.SplitContainer  
    Private WithEvents splitContainer2 As _  
        System.Windows.Forms.SplitContainer  
    ```  
  
    ```csharp  
    private System.Windows.Forms.TreeView treeView1;  
    private System.Windows.Forms.ListView listView1;  
    private System.Windows.Forms.RichTextBox richTextBox1;  
    private System.Windows.Forms. SplitContainer splitContainer2;  
    private System.Windows.Forms. SplitContainer splitContainer1;  
    ```  
  
2. 사용자 인터페이스를 정의 하는 프로시저를 만듭니다. 다음 코드 형식에는 Microsoft Outlook의 사용자 인터페이스와 유사 합니다 되도록 속성을 설정 합니다. 그러나 다른 컨트롤을 사용 하 여 또는 다르게에 도킹 하 여 것 시키면는 다른 사용자 인터페이스를 만드는 것도 그만큼 용이 합니다.  
  
    ```vb  
    Public Sub CreateOutlookUI()  
        ' Create an instance of each control being used.  
        Me.components = New System.ComponentModel.Container()  
        Me.treeView1 = New System.Windows.Forms.TreeView()  
        Me.listView1 = New System.Windows.Forms.ListView()  
        Me.richTextBox1 = New System.Windows.Forms.RichTextBox()  
        Me.splitContainer1 = New System.Windows.Forms.SplitContainer()  
        Me.splitContainer2= New System.Windows.Forms. SplitContainer()  
  
        ' Should you develop this into a working application,  
        ' use the AddHandler method to hook up event procedures here.  
  
        ' Set properties of TreeView control.  
        ' Use the With statement to avoid repetitive code.  
        With Me.treeView1  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 0  
            .Nodes.Add("treeView")  
        End With  
  
    ' Set properties of ListView control.  
       With Me.listView1  
          .Dock = System.Windows.Forms.DockStyle.Top  
          .TabIndex = 2  
          .Items.Add("listView")  
       End With  
  
    ' Set properties of RichTextBox control.  
       With Me.richTextBox1  
          .Dock = System.Windows.Forms.DockStyle.Fill  
          .TabIndex = 3  
          .Text = "richTextBox1"  
       End With  
  
        ' Set properties of the first SplitContainer control.  
        With Me.splitContainer1  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 1  
            .SplitterWidth = 4  
            .SplitterDistance = 150  
            .Orientation = Orientation.Horizontal  
            .Panel1.Controls.Add(Me.listView1)  
            .Panel2.Controls.Add(Me.richTextBox1)  
    End With  
  
        ' Set properties of the second SplitContainer control.  
        With Me.splitContainer2  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 4  
            .SplitterWidth = 4  
            .SplitterDistance = 100  
            .Panel1.Controls.Add(Me.treeView1)  
            .Panel2.Controls.Add(Me.SplitContainer1)  
    End With  
  
    ' Add the main SplitContainer control to the form.  
        Me.Controls.Add(Me.splitContainer2)  
        Me.Text = "Intricate UI Example"  
    End Sub  
    ```  
  
    ```csharp  
    public void createOutlookUI()  
    {  
        // Create an instance of each control being used.  
        treeView1 = new System.Windows.Forms.TreeView();  
        listView1 = new System.Windows.Forms.ListView();  
        richTextBox1 = new System.Windows.Forms.RichTextBox();  
        splitContainer2 = new System.Windows.Forms.SplitContainer();  
        splitContainer1 = new System.Windows.Forms.SplitContainer();  
  
        // Insert code here to hook up event methods.  
  
        // Set properties of TreeView control.  
        treeView1.Dock = System.Windows.Forms.DockStyle.Fill;  
        treeView1.TabIndex = 0;  
        treeView1.Nodes.Add("treeView");  
  
        // Set properties of ListView control.  
        listView1.Dock = System.Windows.Forms.DockStyle.Top;  
        listView1.TabIndex = 2;  
        listView1.Items.Add("listView");  
  
        // Set properties of RichTextBox control.  
        richTextBox1.Dock = System.Windows.Forms.DockStyle.Fill;  
        richTextBox1.TabIndex = 3;  
        richTextBox1.Text = "richTextBox1";  
  
        // Set properties of first SplitContainer control.  
        splitContainer1.Dock = System.Windows.Forms.DockStyle.Fill;  
        splitContainer2.TabIndex = 1;  
        splitContainer2.SplitterWidth = 4;  
        splitContainer2.SplitterDistance = 150;  
        splitContainer2.Orientation = Orientation.Horizontal;  
        splitContainer2.Panel1.Controls.Add(this.listView1);  
        splitContainer2.Panel1.Controls.Add(this.richTextBox1);  
  
        // Set properties of second SplitContainer control.  
        splitContainer2.Dock = System.Windows.Forms.DockStyle.Fill;  
        splitContainer2.TabIndex = 4;  
        splitContainer2.SplitterWidth = 4;  
        splitContainer2.SplitterDistance = 100;  
        splitContainer2.Panel1.Controls.Add(this.treeView1);  
        splitContainer2.Panel1.Controls.Add(this.splitContainer1);  
  
        // Add the main SplitContainer control to the form.  
        this.Controls.Add(this.splitContainer2);  
        this.Text = "Intricate UI Example";  
    }  
    ```  
  
3. Visual basic에서는 방금 만든 프로시저 호출을 추가 합니다 `New()` 프로시저입니다. 시각적 개체의 C#를 폼 클래스의 생성자에이 코드 줄을 추가 합니다.  
  
    ```vb  
    ' Add this to the New procedure.  
    CreateOutlookUI()  
    ```  
  
    ```csharp  
    // Add this to the form class's constructor.  
    createOutlookUI();  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.SplitContainer>
- [SplitContainer 컨트롤](splitcontainer-control-windows-forms.md)
- [방법: 디자이너를 사용 하 여 Windows Forms로 다중 창 사용자 인터페이스 만들기](create-a-multipane-user-interface-with-wf-using-the-designer.md)
