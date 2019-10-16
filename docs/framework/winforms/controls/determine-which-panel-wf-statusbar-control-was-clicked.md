---
title: '방법: Windows Forms StatusBar 컨트롤에서 클릭한 패널 확인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- status bars [Windows Forms], determining panel clicked
- panels [Windows Forms], determining clicked
- StatusBar control [Windows Forms], coding panel click events
- StatusBar control [Windows Forms], determining panel clicked
- PanelClick event [Windows Forms], determining panel clicked
- Panel control [Windows Forms], determining click
ms.assetid: d14c6092-04b2-4a07-8ddf-0dd11277ff5f
ms.openlocfilehash: 6229d8965949641105cd0e9708474c3249d52d1d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965718"
---
# <a name="how-to-determine-which-panel-in-the-windows-forms-statusbar-control-was-clicked"></a>방법: Windows Forms StatusBar 컨트롤에서 클릭한 패널 확인
> [!IMPORTANT]
> 및 <xref:System.Windows.Forms.StatusStrip> <xref:System.Windows.Forms.StatusBar> <xref:System.Windows.Forms.StatusBarPanel> <xref:System.Windows.Forms.StatusBar> 컨트롤은를 대체 하 고 및 <xref:System.Windows.Forms.StatusBarPanel> 컨트롤에 기능을 추가 합니다. 그러나 및 컨트롤은 이전 버전과의 호환성 및 향후 사용을 위해 유지 됩니다. <xref:System.Windows.Forms.ToolStripStatusLabel> 선택.  
  
 사용자 클릭에 응답 하도록 [StatusBar 컨트롤](statusbar-control-windows-forms.md) 컨트롤을 프로그래밍 하려면 <xref:System.Windows.Forms.StatusBar.PanelClick> 이벤트 내에서 case 문을 사용 합니다. 이벤트는 클릭 <xref:System.Windows.Forms.StatusBarPanel>한에 대 한 참조를 포함 하는 인수 (패널 인수)를 포함 합니다. 이 참조를 사용 하 여 클릭 한 패널의 인덱스를 확인 하 고 적절 하 게 프로그래밍할 수 있습니다.  
  
> [!NOTE]
> 컨트롤의 <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 속성이 로`true`설정 되어 있는지 확인 합니다. <xref:System.Windows.Forms.StatusBar>  
  
### <a name="to-determine-which-panel-was-clicked"></a>클릭 한 패널을 확인 하려면  
  
1. `Select Case` `switch case` C# C++이벤트 처리기에서 (Visual Basic) 또는 (visual 또는 visual) 문을 사용 하 여 이벤트 인수에서 클릭 된 패널의 인덱스를 검사 하 여 클릭 한 패널을 확인 합니다. <xref:System.Windows.Forms.StatusBar.PanelClick>  
  
     다음 코드 예제 <xref:System.Windows.Forms.StatusBar> 에서는 폼에 컨트롤, `StatusBar1`및 두 개의 <xref:System.Windows.Forms.StatusBarPanel> 개체, `StatusBarPanel1` 및 `StatusBarPanel2`가 있어야 합니다.  
  
    ```vb  
    Private Sub StatusBar1_PanelClick(ByVal sender As System.Object, ByVal e As System.Windows.Forms.StatusBarPanelClickEventArgs) Handles StatusBar1.PanelClick  
       Select Case StatusBar1.Panels.IndexOf(e.StatusBarPanel)  
         Case 0  
           MessageBox.Show("You have clicked Panel One.")  
         Case 1  
           MessageBox.Show("You have clicked Panel Two.")  
       End Select  
    End Sub  
    ```  
  
    ```csharp  
    private void statusBar1_PanelClick(object sender,   
    System.Windows.Forms.StatusBarPanelClickEventArgs e)  
    {  
       switch (statusBar1.Panels.IndexOf(e.StatusBarPanel))  
       {  
          case 0 :  
             MessageBox.Show("You have clicked Panel One.");  
             break;  
          case 1 :  
             MessageBox.Show("You have clicked Panel Two.");  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void statusBar1_PanelClick(System::Object ^  sender,  
          System::Windows::Forms::StatusBarPanelClickEventArgs ^  e)  
       {  
          switch (statusBar1->Panels->IndexOf(e->StatusBarPanel))  
          {  
             case 0 :  
                MessageBox::Show("You have clicked Panel One.");  
                break;  
             case 1 :  
                MessageBox::Show("You have clicked Panel Two.");  
                break;  
          }  
       }  
    ```  
  
     (시각적 C#개체, C++시각적 개체) 폼의 생성자에 다음 코드를 추가 하 여 이벤트 처리기를 등록 합니다.  
  
    ```csharp  
    this.statusBar1.PanelClick += new   
       System.Windows.Forms.StatusBarPanelClickEventHandler   
       (this.statusBar1_PanelClick);  
    ```  
  
    ```cpp  
    this->statusBar1->PanelClick += gcnew  
       System::Windows::Forms::StatusBarPanelClickEventHandler  
       (this, &Form1::statusBar1_PanelClick);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.StatusBar>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- [방법: 상태 표시줄 패널의 크기 설정](how-to-set-the-size-of-status-bar-panels.md)
- [연습: 런타임에 상태 표시줄 정보 업데이트](walkthrough-updating-status-bar-information-at-run-time.md)
- [StatusBar 컨트롤 개요](statusbar-control-overview-windows-forms.md)
