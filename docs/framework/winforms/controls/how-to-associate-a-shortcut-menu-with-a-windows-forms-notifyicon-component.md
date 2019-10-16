---
title: '방법: Windows Forms NotifyIcon 구성 요소에 바로 가기 메뉴 연결'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- context menus [Windows Forms], for background processes
- NotifyIcon component [Windows Forms], associating shortcut menus
- shortcut menus [Windows Forms], for background processes
ms.assetid: d68f3926-08d3-4f7d-949f-1981b29cf188
ms.openlocfilehash: bf5602d0526fdd97f0cc14382339095a793f13c3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922762"
---
# <a name="how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component"></a>방법: Windows Forms NotifyIcon 구성 요소에 바로 가기 메뉴 연결
> [!NOTE]
> 및 <xref:System.Windows.Forms.MenuStrip> 는이전<xref:System.Windows.Forms.MainMenu> 버전 의및<xref:System.Windows.Forms.ContextMenu> 컨트롤에 기능을 추가 하 고 추가 하지만를 선택 하는 경우 이전 버전과의 호환성 및 향후 사용에 대해 모두 유지 됩니다.<xref:System.Windows.Forms.ContextMenu> <xref:System.Windows.Forms.MainMenu> <xref:System.Windows.Forms.ContextMenuStrip>  
  
 <xref:System.Windows.Forms.NotifyIcon> 구성 요소가 작업 표시줄의 상태 알림 영역에 아이콘을 표시 합니다. 일반적으로 응용 프로그램에서는이 아이콘을 마우스 오른쪽 단추로 클릭 하 여 해당 아이콘이 나타내는 응용 프로그램에 명령을 보낼 수 있습니다. <xref:System.Windows.Forms.ContextMenu> 구성 요소를 <xref:System.Windows.Forms.NotifyIcon> 구성 요소와 연결 하 여 응용 프로그램에이 기능을 추가할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Windows.Forms.NotifyIcon> 작업 표시줄에 구성 요소의 인스턴스를 표시 하는 동안 시작 시 응용 프로그램을 최소화 하려면 기본 폼의 <xref:System.Windows.Forms.NotifyIcon> <xref:System.Windows.Forms.Form.WindowState%2A> 속성을로 <xref:System.Windows.Forms.FormWindowState.Minimized> 설정 하 고 구성 요소의 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 속성을 설정 해야 합니다. 는로 `true`설정 됩니다.  
  
### <a name="to-associate-a-shortcut-menu-with-the-notifyicon-component-at-design-time"></a>디자인 타임에 바로 가기 메뉴를 NotifyIcon 구성 요소와 연결 하려면  
  
1. 구성 요소를 폼에 추가 하 고 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 및 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 속성과 같은 중요 한 속성을 설정 합니다. <xref:System.Windows.Forms.NotifyIcon>  
  
     자세한 내용은 [방법: Windows Forms NotifyIcon 구성 요소](app-icons-to-the-taskbar-with-wf-notifyicon.md)를 사용 하 여 작업 표시줄에 응용 프로그램 아이콘을 추가 합니다.  
  
2. Windows Form에 구성 요소를 추가 합니다. <xref:System.Windows.Forms.ContextMenu>  
  
     런타임에 사용할 수 있도록 설정할 명령을 나타내는 메뉴 항목을 바로 가기 메뉴에 추가 합니다. 이는 액세스 키와 같은 메뉴 항목에 대 한 메뉴의 향상 된 기능을 추가 하는 데도 좋은 시간입니다.  
  
3. <xref:System.Windows.Forms.NotifyIcon> 구성 요소의 <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> 속성을 추가한 바로 가기 메뉴로 설정 합니다.  
  
     이 속성을 설정 하면 작업 표시줄의 아이콘을 클릭 하면 바로 가기 메뉴가 표시 됩니다.  
  
### <a name="to-associate-a-shortcut-menu-with-the-notifyicon-component-programmatically"></a>프로그래밍 방식으로 NotifyIcon 구성 요소에 바로 가기 메뉴를 연결 하려면  
  
1. 응용 <xref:System.Windows.Forms.NotifyIcon> 프로그램 <xref:System.Windows.Forms.ContextMenu> <xref:System.Windows.Forms.NotifyIcon> 에필요한속성<xref:System.Windows.Forms.ContextMenu> 설정이 무엇이 든 클래스 및 클래스의 인스턴스를 만듭니다. 구성 요소의 속성에는<xref:System.Windows.Forms.NotifyIcon.Visible%2A> <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 구성 요소).  
  
2. <xref:System.Windows.Forms.NotifyIcon> 구성 요소의 <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> 속성을 추가한 바로 가기 메뉴로 설정 합니다.  
  
     이 속성을 설정 하면 작업 표시줄의 아이콘을 클릭 하면 바로 가기 메뉴가 표시 됩니다.  
  
    > [!NOTE]
    > 다음 코드 예제에서는 기본 메뉴 구조를 만듭니다. 개발 중인 응용 프로그램에 맞는 메뉴 선택 항목을 사용자 지정 해야 합니다. 또한 이러한 메뉴 항목에 대 한 이벤트를 처리 하 <xref:System.Windows.Forms.MenuItem.Click> 는 코드를 작성 하려고 합니다.  
  
    ```vb  
    Public ContextMenu1 As New ContextMenu  
    Public NotifyIcon1 As New NotifyIcon  
  
    Public Sub CreateIconMenuStructure()  
       ' Add menu items to shortcut menu.  
       ContextMenu1.MenuItems.Add("&Open Application")  
       ContextMenu1.MenuItems.Add("S&uspend Application")  
       ContextMenu1.MenuItems.Add("E&xit")  
  
       ' Set properties of NotifyIcon component.  
       NotifyIcon1.Icon = New System.Drawing.Icon _   
          (System.Environment.GetFolderPath _   
          (System.Environment.SpecialFolder.Personal)  _   
          & "\Icon.ico")  
       NotifyIcon1.Text = "Right-click me!"  
       NotifyIcon1.Visible = True  
       NotifyIcon1.ContextMenu = ContextMenu1  
    End Sub  
    ```  
  
```csharp  
public NotifyIcon notifyIcon1 = new NotifyIcon();  
public ContextMenu contextMenu1 = new ContextMenu();  
  
public void createIconMenuStructure()  
{  
   // Add menu items to shortcut menu.  
   contextMenu1.MenuItems.Add("&Open Application");  
   contextMenu1.MenuItems.Add("S&uspend Application");  
   contextMenu1.MenuItems.Add("E&xit");  
  
   // Set properties of NotifyIcon component.  
   notifyIcon1.Icon = new System.Drawing.Icon  
      (System.Environment.GetFolderPath  
      (System.Environment.SpecialFolder.Personal)  
      + @"\Icon.ico");  
   notifyIcon1.Visible = true;  
   notifyIcon1.Text = "Right-click me!";  
   notifyIcon1.Visible = true;  
   notifyIcon1.ContextMenu = contextMenu1;  
}  
```  
  
```cpp  
public:  
   System::Windows::Forms::NotifyIcon ^ notifyIcon1;  
   System::Windows::Forms::ContextMenu ^ contextMenu1;  
  
   void createIconMenuStructure()  
   {  
      // Add menu items to shortcut menu.  
      contextMenu1->MenuItems->Add("&Open Application");  
      contextMenu1->MenuItems->Add("S&uspend Application");  
      contextMenu1->MenuItems->Add("E&xit");  
  
      // Set properties of NotifyIcon component.  
      notifyIcon1->Icon = gcnew System::Drawing::Icon  
          (String::Concat(System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::Personal),  
          "\\Icon.ico"));  
      notifyIcon1->Text = "Right-click me!";  
      notifyIcon1->Visible = true;  
      notifyIcon1->ContextMenu = contextMenu1;  
   }  
```  
  
> [!NOTE]
> 폼의 생성자 `notifyIcon1` 에 `contextMenu1,` 다음 문을 포함 하 여을 초기화 해야 합니다.  
  
```cpp  
notifyIcon1 = gcnew System::Windows::Forms::NotifyIcon();  
contextMenu1 = gcnew System::Windows::Forms::ContextMenu();  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.NotifyIcon>
- <xref:System.Windows.Forms.NotifyIcon.Icon%2A>
- [방법: Windows Forms NotifyIcon 구성 요소를 사용 하 여 작업 표시줄에 응용 프로그램 아이콘 추가](app-icons-to-the-taskbar-with-wf-notifyicon.md)
- [NotifyIcon 구성 요소](notifyicon-component-windows-forms.md)
- [NotifyIcon 구성 요소 개요](notifyicon-component-overview-windows-forms.md)
