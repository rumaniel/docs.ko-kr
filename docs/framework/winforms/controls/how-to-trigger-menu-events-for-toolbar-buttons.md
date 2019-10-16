---
title: '방법: Toolbar 단추에 대한 메뉴 이벤트 트리거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], toolbars
- ToolBar control [Windows Forms], click event handlers
- ToolBar control [Windows Forms], coding button click events
- toolbars [Windows Forms], click event handlers
ms.assetid: 98374f70-993d-4ca4-89fb-48fea6ce5b45
ms.openlocfilehash: 381b8ba08db6ff5bb817c9c89008dacb1085ac1b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956031"
---
# <a name="how-to-trigger-menu-events-for-toolbar-buttons"></a>방법: Toolbar 단추에 대한 메뉴 이벤트 트리거
> [!NOTE]
> <xref:System.Windows.Forms.ToolStrip> 컨트롤은 <xref:System.Windows.Forms.ToolBar> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.ToolBar> 컨트롤을 계속 유지하도록 선택할 수 있습니다.  
  
 Windows Form <xref:System.Windows.Forms.ToolBar> 에서 도구 모음 단추가 있는 컨트롤을 사용 하는 경우 사용자가 클릭 하는 단추를 알고 싶을 것입니다.  
  
 컨트롤의 이벤트에서 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> 클래스의 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A> 속성을 평가할 수 있습니다. <xref:System.Windows.Forms.ToolBar.ButtonClick> <xref:System.Windows.Forms.ToolBar> 아래 예제에서는 클릭한 단추를 나타내는 메시지 상자를 표시합니다. 자세한 내용은 <xref:System.Windows.Forms.MessageBox>를 참조하세요.  
  
 아래 예제에서는 Windows Form <xref:System.Windows.Forms.ToolBar> 에 컨트롤이 추가 된 것으로 가정 합니다.  
  
### <a name="to-handle-the-click-event-on-a-toolbar"></a>도구 모음에서 Click 이벤트를 처리하려면  
  
1. 프로시저에서 <xref:System.Windows.Forms.ToolBar> 컨트롤에 도구 모음 단추를 추가 합니다.  
  
    ```vb  
    Public Sub ToolBarConfig()  
    ' Instantiate the toolbar buttons, set their Text properties  
    ' and add them to the ToolBar control.  
       ToolBar1.Buttons.Add(New ToolBarButton("One"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Two"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Three"))  
    ' Add the event handler delegate.  
       AddHandler ToolBar1.ButtonClick, AddressOf Me.ToolBar1_ButtonClick  
    End Sub  
    ```  
  
    ```csharp  
    public void ToolBarConfig()   
    {  
       toolBar1.Buttons.Add(new ToolBarButton("One"));  
       toolBar1.Buttons.Add(new ToolBarButton("Two"));  
       toolBar1.Buttons.Add(new ToolBarButton("Three"));  
  
       toolBar1.ButtonClick +=   
          new ToolBarButtonClickEventHandler(this.toolBar1_ButtonClick);  
    }  
    ```  
  
    ```cpp  
    public:  
       void ToolBarConfig()  
       {  
          toolBar1->Buttons->Add(gcnew ToolBarButton("One"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Two"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Three"));  
  
          toolBar1->ButtonClick +=   
             gcnew ToolBarButtonClickEventHandler(this,  
             &Form1::toolBar1_ButtonClick);  
       }  
    ```  
  
2. <xref:System.Windows.Forms.ToolBar> 컨트롤 의<xref:System.Windows.Forms.ToolBar.ButtonClick> 이벤트에 대 한 이벤트 처리기를 추가 합니다. Case 전환 문과 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> 클래스를 사용 하 여 클릭 한 도구 모음 단추를 확인 합니다. 이에 따라 적절한 메시지 상자를 표시합니다.  
  
    > [!NOTE]
    > 이 예제에서 메시지 상자는 자리 표시자로만 사용되고 있습니다. 따라서 도구 모음 단추를 클릭할 때 실행할 다른 코드를 자유롭게 추가할 수 있습니다.  
  
    ```vb  
    Protected Sub ToolBar1_ButtonClick(ByVal sender As Object, _  
    ByVal e As ToolBarButtonClickEventArgs)  
    ' Evaluate the Button property of the ToolBarButtonClickEventArgs  
    ' to determine which button was clicked.  
       Select Case ToolBar1.Buttons.IndexOf(e.Button)  
         Case 0  
           MessageBox.Show("First toolbar button clicked")  
         Case 1  
           MessageBox.Show("Second toolbar button clicked")  
         Case 2  
           MessageBox.Show("Third toolbar button clicked")  
       End Select  
    End Sub  
    ```  
  
    ```csharp  
    protected void toolBar1_ButtonClick(object sender,  
    ToolBarButtonClickEventArgs e)  
    {  
       // Evaluate the Button property of the ToolBarButtonClickEventArgs  
       // to determine which button was clicked.  
       switch (toolBar1.Buttons.IndexOf(e.Button))  
       {  
          case 0 :  
             MessageBox.Show("First toolbar button clicked");  
             break;  
          case 1 :  
             MessageBox.Show("Second toolbar button clicked");  
             break;  
          case 2 :  
             MessageBox.Show("Third toolbar button clicked");  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    protected:  
       void toolBar1_ButtonClick(System::Object ^ sender,  
          ToolBarButtonClickEventArgs ^ e)  
       {  
         // Evaluate the Button property of the ToolBarButtonClickEventArgs  
         // to determine which button was clicked.  
          switch (toolBar1->Buttons->IndexOf(e->Button))  
          {  
             case 0 :  
                MessageBox::Show("First toolbar button clicked");  
                break;  
             case 1 :  
                MessageBox::Show("Second toolbar button clicked");  
                break;  
             case 2 :  
                MessageBox::Show("Third toolbar button clicked");  
                break;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolBar>
- [방법: ToolBar 컨트롤에 단추 추가](how-to-add-buttons-to-a-toolbar-control.md)
- [방법: 도구 모음 단추의 아이콘 정의](how-to-define-an-icon-for-a-toolbar-button.md)
- [ToolBar 컨트롤](toolbar-control-windows-forms.md)
