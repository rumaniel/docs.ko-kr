---
title: '방법: Windows Forms TabControl을 사용하여 탭 추가 및 제거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tabs [Windows Forms], removing from pages
- TabPage control
- TabControl control [Windows Forms], adding and removing tabs
- tabs [Windows Forms], adding to pages
- tab pages
ms.assetid: 66d4dfca-41e8-44e3-9c80-fb7ac4cb1619
ms.openlocfilehash: 938f1210eaa3479822e752327123737a3286fe9a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64624055"
---
# <a name="how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol"></a>방법: Windows Forms TabControl을 사용하여 탭 추가 및 제거
기본적으로 <xref:System.Windows.Forms.TabControl> 컨트롤에는 두 개의 <xref:System.Windows.Forms.TabPage> 컨트롤입니다. 이러한 탭을 통해 액세스할 수 있습니다는 <xref:System.Windows.Forms.TabControl.TabPages%2A> 속성입니다.  
  
### <a name="to-add-a-tab-programmatically"></a>프로그래밍 방식으로 탭을 추가 하려면  
  
- 사용 된 <xref:System.Windows.Forms.TabControl.TabPageCollection.Add%2A> 메서드를 <xref:System.Windows.Forms.TabControl.TabPages%2A> 속성.  
  
    ```vb  
    Dim myTabPage As New TabPage()  
    myTabPage.Text = "TabPage" & (TabControl1.TabPages.Count + 1)  
    TabControl1.TabPages.Add(myTabPage)  
    ```  
  
    ```csharp  
    string title = "TabPage " + (tabControl1.TabCount + 1).ToString();  
    TabPage myTabPage = new TabPage(title);  
    tabControl1.TabPages.Add(myTabPage);  
    ```  
  
    ```cpp  
    String^ title = String::Concat("TabPage ",  
       (tabControl1->TabCount + 1).ToString());  
    TabPage^ myTabPage = gcnew TabPage(title);  
    tabControl1->TabPages->Add(myTabPage);  
    ```  
  
### <a name="to-remove-a-tab-programmatically"></a>프로그래밍 방식으로 탭을 제거 하려면  
  
- 선택한 탭을 제거 하려면 사용 합니다 <xref:System.Windows.Forms.TabControl.TabPageCollection.Remove%2A> 메서드는 <xref:System.Windows.Forms.TabControl.TabPages%2A> 속성.  
  
     또는  
  
- 모든 탭을 제거 하려면 사용 합니다 <xref:System.Windows.Forms.TabControl.TabPageCollection.Clear%2A> 메서드는 <xref:System.Windows.Forms.TabControl.TabPages%2A> 속성.  
  
    ```vb  
    ' Removes the selected tab:  
    TabControl1.TabPages.Remove(TabControl1.SelectedTab)  
    ' Removes all the tabs:  
    TabControl1.TabPages.Clear()  
    ```  
  
    ```csharp  
    // Removes the selected tab:  
    tabControl1.TabPages.Remove(tabControl1.SelectedTab);  
    // Removes all the tabs:  
    tabControl1.TabPages.Clear();  
    ```  
  
    ```cpp  
    // Removes the selected tab:  
    tabControl1->TabPages->Remove(tabControl1->SelectedTab);  
    // Removes all the tabs:  
    tabControl1->TabPages->Clear();  
    ```  
  
## <a name="see-also"></a>참고자료

- [TabControl 컨트롤 개요](tabcontrol-control-overview-windows-forms.md)
- [방법: 탭 페이지에 컨트롤 추가](how-to-add-a-control-to-a-tab-page.md)
- [방법: 탭 페이지를 사용 하지 않도록 설정](how-to-disable-tab-pages.md)
- [방법: Windows Forms TabControl의 모양 변경](how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)
