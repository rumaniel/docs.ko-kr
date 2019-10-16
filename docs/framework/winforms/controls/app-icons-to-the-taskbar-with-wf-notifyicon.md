---
title: '방법: Windows Forms NotifyIcon 구성 요소를 사용하여 작업 표시줄에 애플리케이션 아이콘 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- TrayIcon
helpviewer_keywords:
- status area icons
- icons [Windows Forms], adding to taskbar
- NotifyIcon component
- taskbar [Windows Forms], adding icons
ms.assetid: d28c0fe6-aaf2-4df7-ad74-928d861a8510
ms.openlocfilehash: 05b6f300afea4671c1a847b116b378514ecb8b56
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959509"
---
# <a name="how-to-add-application-icons-to-the-taskbar-with-the-windows-forms-notifyicon-component"></a>방법: Windows Forms NotifyIcon 구성 요소를 사용하여 작업 표시줄에 애플리케이션 아이콘 추가

Windows Forms <xref:System.Windows.Forms.NotifyIcon> 구성 요소 작업 표시줄의 상태 알림 영역에 단일 아이콘을 표시 합니다. 여러 상태 영역에 여러 개의 아이콘을 표시 하려면 해야 <xref:System.Windows.Forms.NotifyIcon> 폼의 구성 요소입니다. 컨트롤에 대해 표시 되는 아이콘을 설정 하려면 사용 된 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 속성입니다. 코드를 작성할 수도 있습니다는 <xref:System.Windows.Forms.NotifyIcon.DoubleClick> 이벤트 처리기 아이콘을 두 번 클릭할 때 발생 하는 것입니다. 예를 들어, 표시 아이콘으로 표시 하는 백그라운드 프로세스를 구성 하려면 사용자에 대 한 대화 상자를 만들 수 있습니다.

> [!NOTE]
> <xref:System.Windows.Forms.NotifyIcon> 구성 요소를 사용자에 게 경고 작업 또는 이벤트를 발생 하는 알림 용도로 사용 또는 일종의 상태가 변경 되었습니다. 응용 프로그램을 사용 하 여 표준 상호 작용에 대 한 메뉴, 도구 모음 및 기타 사용자 인터페이스 요소를 사용 해야 합니다.

### <a name="to-set-the-icon"></a>아이콘을 설정 하려면

1. 값을 할당 합니다 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 속성입니다. 값 형식 이어야 합니다 `System.Drawing.Icon` .ico 파일에서 로드할 수 있습니다. 줄임표 단추를 클릭 하거나 코드에서 아이콘 파일을 지정할 수 있습니다 (![의 줄임표 단추 (...)의 Visual Studio 속성 창의](./media/visual-studio-ellipsis-button.png)) 옆에 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 속성에는 **속성** 다음에서 파일을 선택 하는 **열려** 나타나는 대화 상자.

2. <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 속성을 `true`으로 설정합니다.

3. 설정 된 <xref:System.Windows.Forms.NotifyIcon.Text%2A> 속성을 적절 한 도구 설명 문자열입니다.

     다음 코드 예제는 아이콘의 위치 설정 된 경로 **내 문서** 폴더입니다. 이 폴더는 Windows 운영 체제를 실행 하는 대부분의 컴퓨터에 포함 되도록 알 수 없으므로이 위치가 사용 됩니다. 또한이 위치를 선택 합니다. 최소한의 시스템 액세스 수준 가진 사용자가 안전 하 게 응용 프로그램을 실행할 수 있습니다. 다음 예제에서는 사용 하 여 폼을 <xref:System.Windows.Forms.NotifyIcon> 이미 추가 된 컨트롤입니다. 명명 된 아이콘 파일에 있어야 `Icon.ico`합니다.

    ```vb
    ' You should replace the bold icon in the sample below
    ' with an icon of your own choosing.
    NotifyIcon1.Icon = New _
       System.Drawing.Icon(System.Environment.GetFolderPath _
       (System.Environment.SpecialFolder.Personal) _
       & "\Icon.ico")
    NotifyIcon1.Visible = True
    NotifyIcon1.Text = "Antivirus program"
    ```

    ```csharp
    // You should replace the bold icon in the sample below
    // with an icon of your own choosing.
    // Note the escape character used (@) when specifying the path.
    notifyIcon1.Icon =
       new System.Drawing.Icon (System.Environment.GetFolderPath
       (System.Environment.SpecialFolder.Personal)
       + @"\Icon.ico");
    notifyIcon1.Visible = true;
    notifyIcon1.Text = "Antivirus program";
    ```

    ```cpp
    // You should replace the bold icon in the sample below
    // with an icon of your own choosing.
    notifyIcon1->Icon = gcnew
       System::Drawing::Icon(String::Concat
       (System::Environment::GetFolderPath
       (System::Environment::SpecialFolder::Personal),
       "\\Icon.ico"));
    notifyIcon1->Visible = true;
    notifyIcon1->Text = "Antivirus program";
    ```

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.NotifyIcon>
- <xref:System.Windows.Forms.NotifyIcon.Icon%2A>
- [방법: Windows Forms NotifyIcon 구성 요소를 사용 하 여 바로 가기 메뉴 연결](how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component.md)
- [NotifyIcon 구성 요소](notifyicon-component-windows-forms.md)
- [NotifyIcon 구성 요소 개요](notifyicon-component-overview-windows-forms.md)
