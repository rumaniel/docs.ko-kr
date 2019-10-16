---
title: '방법: Windows Forms LinkLabel 컨트롤의 모양 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- LinkLabel properties
- LinkLabel control [Windows Forms], changing appearance of links
- links [Windows Forms], changing appearance
- examples [Windows Forms], LinkLabel control
- LinkLabel control [Windows Forms], examples
ms.assetid: fdc5854f-5162-4457-8cbe-1042feb2d132
ms.openlocfilehash: f0a5805561509501ca38a7fec6b4731af190e3c3
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59322019"
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-linklabel-control"></a>방법: Windows Forms LinkLabel 컨트롤의 모양 변경
표시 되는 텍스트를 변경할 수는 <xref:System.Windows.Forms.LinkLabel> 다양 한 목적에 맞게 컨트롤을 합니다. 예를 들어, 것이 일반적으로 사용자에 게 나타내기 위해 텍스트에 밑줄을 특정 색으로 표시를 설정 하 여 텍스트를 클릭할 수 있습니다. 사용자가 텍스트 색을 다른 색으로 변경 됩니다. 이 동작을 제어 하려면 5 개의 서로 다른 속성을 설정할 수 있습니다: 합니다 <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>, <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>를 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>, 및 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 속성입니다.  
  
### <a name="to-change-the-appearance-of-a-linklabel-control"></a>LinkLabel 컨트롤의 모양을 변경 하려면  
  
1. 설정 된 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A> 및 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> 속성을 원하는 색입니다.  
  
     이렇게 하려면 중 하나에서 프로그래밍 방식으로 또는 디자인 타임에는 **속성** 창입니다.  
  
    ```vb  
    ' You can set the color using decimal values for red, green, and blue  
    LinkLabel1.LinkColor = Color.FromArgb(0, 0, 255)  
    ' Or you can set the color using defined constants  
    LinkLabel1.VisitedLinkColor = Color.Purple  
    ```  
  
    ```csharp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1.LinkColor = Color.FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1.VisitedLinkColor = Color.Purple;  
    ```  
  
    ```cpp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1->LinkColor = Color::FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1->VisitedLinkColor = Color::Purple;  
    ```  
  
2. 설정 된 <xref:System.Windows.Forms.LinkLabel.Text%2A> 을 적절 한 캡션에 속성입니다.  
  
     이렇게 하려면 중 하나에서 프로그래밍 방식으로 또는 디자인 타임에는 **속성** 창입니다.  
  
    ```vb  
    LinkLabel1.Text = "Click here to see more."  
    ```  
  
    ```csharp  
    linkLabel1.Text = "Click here to see more.";  
    ```  
  
    ```cpp  
    linkLabel1->Text = "Click here to see more.";  
    ```  
  
3. 설정 된 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 속성을 캡션의 어느 부분을 링크로 표시 됩니다.  
  
     합니다 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 값으로 표시 됩니다는 <xref:System.Windows.Forms.LinkArea> 두 숫자, 시작 문자 위치와 문자 개수를 포함 하 합니다. 이렇게 하려면 중 하나에서 프로그래밍 방식으로 또는 디자인 타임에는 **속성** 창입니다.  
  
    ```vb  
    LinkLabel1.LinkArea = new LinkArea(6,4)  
    ```  
  
    ```csharp  
    linkLabel1.LinkArea = new LinkArea(6,4);  
    ```  
  
    ```cpp  
    linkLabel1->LinkArea = LinkArea(6,4);  
    ```  
  
4. 설정 된 <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> 속성을 <xref:System.Windows.Forms.LinkBehavior.AlwaysUnderline>를 <xref:System.Windows.Forms.LinkBehavior.HoverUnderline>, 또는 <xref:System.Windows.Forms.LinkBehavior.NeverUnderline>합니다.  
  
     로 설정 된 경우 <xref:System.Windows.Forms.LinkBehavior.HoverUnderline>에 의해 지정 된 캡션 부분 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 위에 포인터를 놓을 때만 밑줄이 됩니다.  
  
5. 에 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 이벤트 처리기를 설정 합니다 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 속성을 `true`입니다.  
  
     링크를 방문 했을 때 색으로 모양을 어떤 방식으로든에서를 일반적으로 변경 하는 것이 있습니다. 텍스트에서 지정 된 색으로 변경 됩니다는 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> 속성입니다.  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked (ByVal sender As Object, _  
       ByVal e As EventArgs) Handles LinkLabel1.LinkClicked  
       ' Change the color of the link text  
       ' by setting LinkVisited to True.  
       LinkLabel1.LinkVisited = True  
       ' Then do whatever other action is appropriate  
    End Sub  
    ```  
  
    ```csharp  
    protected void LinkLabel1_LinkClicked(object sender, System.EventArgs e)  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to True.  
       linkLabel1.LinkVisited = true;  
       // Then do whatever other action is appropriate  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to True.  
          linkLabel1->LinkVisited = true;  
          // Then do whatever other action is appropriate  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>
- <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>
- <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>
- <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>
- [LinkLabel 컨트롤 개요](linklabel-control-overview-windows-forms.md)
- [방법: Windows Forms LinkLabel 컨트롤을 사용 하 여 페이지를 웹 또는 개체에 연결](link-to-an-object-or-web-page-with-wf-linklabel-control.md)
- [LinkLabel 컨트롤](linklabel-control-windows-forms.md)
