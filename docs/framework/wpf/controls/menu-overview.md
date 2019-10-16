---
title: Menu 개요
ms.date: 03/30/2017
helpviewer_keywords:
- Menu control [WPF]
- controls [WPF], Menu
ms.assetid: 67df6de5-db96-4c71-b752-af90729a6537
ms.openlocfilehash: a3250cfd3fd651cb4ed3c4fd6975f5b5c89195f9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942157"
---
# <a name="menu-overview"></a>Menu 개요
<xref:System.Windows.Controls.Menu> 클래스를 사용 하면 요소와 연결 된 명령 및 이벤트 처리기를 계층적 순서로 구성할 수 있습니다. 각 <xref:System.Windows.Controls.Menu> 의 컬렉션을 포함 하는 요소 <xref:System.Windows.Controls.MenuItem> 요소입니다.  

<a name="menu_control"></a>   
## <a name="menu-control"></a>Menu 컨트롤  
 <xref:System.Windows.Controls.Menu> 컨트롤에 명령 또는 응용 프로그램에 대 한 옵션을 지정 하는 항목의 목록을 제공 합니다. 일반적으로 클릭 하는 <xref:System.Windows.Controls.MenuItem> 명령을 실행 하는 응용 프로그램 또는 하위 메뉴를 엽니다.  
  
<a name="creating_menus"></a>   
## <a name="creating-menus"></a>메뉴 만들기  
 다음 예제는 <xref:System.Windows.Controls.Menu> 텍스트를 조작 하는 <xref:System.Windows.Controls.TextBox>합니다. <xref:System.Windows.Controls.Menu> 포함 <xref:System.Windows.Controls.MenuItem> 사용 하는 개체를 <xref:System.Windows.Controls.MenuItem.Command%2A>를 <xref:System.Windows.Controls.MenuItem.IsCheckable%2A>, 및 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 속성 및 <xref:System.Windows.Controls.MenuItem.Checked>를 <xref:System.Windows.Controls.MenuItem.Unchecked>, 및 <xref:System.Windows.Controls.MenuItem.Click> 이벤트입니다.  
  
 [!code-xaml[MenuItemCommandsAndEvents#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandsAndEvents/CSharp/Window1.xaml#1)]  
  
 [!code-csharp[MenuItemCommandsAndEvents#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandsAndEvents/CSharp/Window1.xaml.cs#2)]
 [!code-vb[MenuItemCommandsAndEvents#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandsAndEvents/VisualBasic/Window1.xaml.vb#2)]  
  
<a name="menus_with_shortcutkeys"></a>   
## <a name="menuitems-with-keyboard-shortcuts"></a>바로 가기 키가 있는 MenuItem  
 바로 가기 키는 호출 하는 키보드로 입력할 수 있는 문자 조합 <xref:System.Windows.Controls.Menu> 명령입니다. 예를 들어 **복사**의 바로 가기는 Ctrl+C입니다. 두 가지 속성 바로 가기 키 및 메뉴 항목 사용 —<xref:System.Windows.Controls.MenuItem.InputGestureText%2A> 또는 <xref:System.Windows.Controls.MenuItem.Command%2A>합니다.  
  
<a name="menus_inputgesturetext"></a>   
### <a name="inputgesturetext"></a>InputGestureText  
 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.MenuItem.InputGestureText%2A> 키보드 바로 가기 텍스트를 할당 하는 속성 <xref:System.Windows.Controls.MenuItem> 컨트롤입니다. 이렇게 해야만 메뉴 항목에 바로 가기 키가 배치됩니다.  명령을 사용 하 여 연결 하지는 않습니다는 <xref:System.Windows.Controls.MenuItem>합니다. 애플리케이션은 사용자 입력을 처리하여 작업을 수행해야 합니다.  
  
 [!code-xaml[MenuEvent#6](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuEvent/CSharp/Pane1.xaml#6)]  
  
<a name="menus_commands"></a>   
### <a name="command"></a>명령  
 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.MenuItem.Command%2A> 연결할 속성을 합니다 **열기** 및 **저장** 명령을 사용 하 여 <xref:System.Windows.Controls.MenuItem> 컨트롤입니다. Command 속성에서 사용 하 여 명령을 연결 뿐만 아니라는 <xref:System.Windows.Controls.MenuItem>, 바로 가기로 사용할 입력된 제스처 텍스트를 제공 합니다.  
  
 [!code-xaml[MenuEvent#8](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuEvent/CSharp/Pane1.xaml#8)]  
  
 합니다 <xref:System.Windows.Controls.MenuItem> 클래스에는 <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> 명령은 발생 하는 요소를 지정 하는 속성입니다. 경우 <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> 키보드 포커스가 있는 요소가 명령을 받습니다를 설정 하지 않으면. 명령에 대한 자세한 내용은 [명령 개요](../advanced/commanding-overview.md)를 참조하세요.  
  
<a name="menu_styling"></a>   
## <a name="menu-styling"></a>메뉴 스타일 설정  
 컨트롤 스타일 지정을 사용 하 여 대폭 변경할 수 있습니다의 모양 및 동작 <xref:System.Windows.Controls.Menu> 사용자 지정 컨트롤을 작성 하지 않고도 컨트롤입니다. 시각적 속성을 설정 하는 것 외에도 적용할 수도 있습니다는 <xref:System.Windows.Style> 컨트롤의 개별 파트에 속성을 통해 컨트롤의 파트의 동작을 변경 또는 추가 부분을 추가 또는 컨트롤의 레이아웃을 변경 합니다. 다음 예제에서는 추가 하는 여러 방법을 보여 줍니다는 <xref:System.Windows.Style> 에 <xref:System.Windows.Controls.Menu> 제어 합니다.  
  
 첫 번째 코드 예제에서는 정의 <xref:System.Windows.Style> 호출 `Simple` 스타일에서 현재 시스템 설정을 사용 하는 방법을 보여 주는 합니다. 코드에서는 `MenuHighlightBrush`의 색을 메뉴의 배경색으로 할당하고 `MenuTextBrush`를 메뉴의 전경색으로 할당합니다. 리소스 키를 사용하여 브러시를 할당하게 됩니다.  
  
 [!code-xaml[MenuStylesSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuStylesSnippet/CS/app.xaml#1)]  
  
 다음 샘플에서는 <xref:System.Windows.Trigger> 의 모양을 변경할 수 있도록 하는 요소는 <xref:System.Windows.Controls.MenuItem> 에서 발생 하는 이벤트에 대 한 응답에서을 <xref:System.Windows.Controls.Menu>입니다. 위로 마우스를 이동 하는 <xref:System.Windows.Controls.Menu>, 전경색 및 메뉴 항목의 글꼴 특성을 변경 합니다.  
  
 [!code-xaml[MenuStylesSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuStylesSnippet/CS/app.xaml#2)]  
  
## <a name="see-also"></a>참고자료

- [WPF Controls Gallery Sample](https://go.microsoft.com/fwlink/?LinkID=160053)(WPF 컨트롤 갤러리 샘플)
