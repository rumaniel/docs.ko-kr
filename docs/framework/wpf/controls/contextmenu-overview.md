---
title: ContextMenu 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ContextMenu
- ContextMenu controls [WPF], about ContextMenu controls
ms.assetid: 16909c42-799a-4561-91e0-7d69dcfeea91
ms.openlocfilehash: 1818718d3ca9e8f56da99d6e504b41b217bfd980
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053264"
---
# <a name="contextmenu-overview"></a>ContextMenu 개요
합니다 <xref:System.Windows.Controls.ContextMenu> 클래스는 컨텍스트별을 사용 하 여 기능을 노출 하는 요소를 나타냅니다. <xref:System.Windows.Controls.Menu>합니다. 일반적으로 사용자를 노출 합니다 <xref:System.Windows.Controls.ContextMenu> 에서 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 마우스 단추를 마우스 오른쪽 단추로 클릭 합니다. 이 항목에서는 소개 합니다 <xref:System.Windows.Controls.ContextMenu> 요소에서 사용 하는 방법의 예제를 제공 하 고 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 및 코드입니다.  

<a name="contextmenu_control"></a>   
## <a name="contextmenu-control"></a>ContextMenu 컨트롤  
 <xref:System.Windows.Controls.ContextMenu> 특정 컨트롤에 연결 됩니다. 합니다 <xref:System.Windows.Controls.ContextMenu> 요소를 사용 하면 예를 들어, 특정 컨트롤과 관련 된 옵션 또는 명령을 지정 하는 항목의 목록을 사용 하 여 사용자를 표시 하는 <xref:System.Windows.Controls.Button>합니다. 사용자가 컨트롤을 마우스 오른쪽 단추로 클릭하면 메뉴가 표시됩니다. 일반적으로 클릭 하는 <xref:System.Windows.Controls.MenuItem> 명령을 실행 하는 응용 프로그램 또는 하위 메뉴를 엽니다.  
  
<a name="creating_contextmenus"></a>   
## <a name="creating-contextmenus"></a>ContextMenu 만들기  
 다음 예제를 만드는 방법을 보여는 <xref:System.Windows.Controls.ContextMenu> 하위 메뉴가 있는 합니다. <xref:System.Windows.Controls.ContextMenu> 컨트롤 단추 컨트롤에 연결 됩니다.  
  
 [!code-xaml[ContextMenu#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml#1)]  
  
 [!code-csharp[ContextMenu#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ContextMenu#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ContextMenu/VisualBasic/Pane1.xaml.vb#2)]  
  
<a name="applying_styles_to_contextmenu"></a>   
## <a name="applying-styles-to-a-contextmenu"></a>ContextMenu에 스타일 적용  
 컨트롤을 사용 하 여 <xref:System.Windows.Style>에서의 동작과 모양을 대폭 변경할 수 있습니다는 <xref:System.Windows.Controls.ContextMenu> 사용자 지정 컨트롤을 작성 하지 않고도 합니다. 시각적 속성을 설정하는 것 외에 컨트롤의 파트에 스타일을 적용할 수도 있습니다. 예를 들어, 속성을 사용 하 여 컨트롤의 파트의 동작을 변경할 수 있습니다 또는 파트를 추가 하거나 레이아웃을 변경할 수는 <xref:System.Windows.Controls.ContextMenu>합니다. 다음 예제에서는 표시 스타일을 추가 하는 여러 방법을 <xref:System.Windows.Controls.ContextMenu> 컨트롤입니다.  
  
 첫 번째 예제는 스타일에서 현재 시스템 설정을 사용하는 방법을 보여 주는 `SimpleSysResources`라는 스타일을 정의합니다. 예제 <xref:System.Windows.SystemColors.MenuHighlightBrushKey%2A> 으로 <xref:System.Windows.Controls.Control.Background%2A> 색 및 <xref:System.Windows.SystemColors.MenuTextBrushKey%2A> 으로 <xref:System.Windows.Controls.Control.Foreground%2A> 의 색을 <xref:System.Windows.Controls.ContextMenu>.  
  
```xaml  
<Style x:Key="SimpleSysResources" TargetType="{x:Type MenuItem}">  
  <Setter Property = "Background" Value=   
    "{DynamicResource {x:Static SystemColors.MenuHighlightBrushKey}}"/>  
  <Setter Property = "Foreground" Value=   
    "{DynamicResource {x:Static SystemColors.MenuTextBrushKey}}"/>  
</Style>  
```  
  
 다음 예제에서는 합니다 <xref:System.Windows.Trigger> 의 모양을 변경 하는 요소를 <xref:System.Windows.Controls.Menu> 에서 발생 하는 이벤트에 대 한 응답에는 <xref:System.Windows.Controls.ContextMenu>. 사용자의 모양 메뉴 위로 마우스를 이동 하는 경우는 <xref:System.Windows.Controls.ContextMenu> 항목을 변경 합니다.  
  
```xaml  
<Style x:Key="Triggers" TargetType="{x:Type MenuItem}">  
  <Style.Triggers>  
    <Trigger Property="MenuItem.IsMouseOver" Value="true">  
      <Setter Property = "FontSize" Value="16"/>  
      <Setter Property = "FontStyle" Value="Italic"/>  
      <Setter Property = "Foreground" Value="Red"/>  
    </Trigger>  
  </Style.Triggers>  
</Style>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.Style>
- <xref:System.Windows.Controls.Menu>
- <xref:System.Windows.Controls.MenuItem>
- [ContextMenu](contextmenu.md)
- [ContextMenu 스타일 및 템플릿](contextmenu-styles-and-templates.md)
- [WPF Controls Gallery Sample](https://go.microsoft.com/fwlink/?LinkID=160053)(WPF 컨트롤 갤러리 샘플)
