---
title: '방법: 명령을 지원하는 컨트롤에 명령 후크'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Control class [WPF], attaching a RoutedCommand
- classes [WPF], Control [WPF], attaching a RoutedCommand
- RoutedCommand class [WPF], attaching to a Control
- classes [WPF], RoutedCommand [WPF], attaching to a Control
ms.assetid: 8d8592ae-0c91-469e-a1cd-d179c4544548
ms.openlocfilehash: 981fecf33b60c76ecab760185db7dab4bbb254d7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757250"
---
# <a name="how-to-hook-up-a-command-to-a-control-with-command-support"></a>방법: 명령을 지원하는 컨트롤에 명령 후크
다음 예제는 <xref:System.Windows.Input.RoutedCommand>를 명령에 대한 지원을 기본 제공하는 <xref:System.Windows.Controls.Control>에 후크하는 방법을 보여줍니다.  여러 소스에 명령을 후크하는 전체 샘플은 [Create a Custom RoutedCommand Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)(사용자 지정 RoutedCommand 만들기 샘플)을 참조하세요.  
  
## <a name="example"></a>예제  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]는 애플리케이션 프로그래머가 자주 접하게 되는 공용 명령의 라이브러리를 제공합니다.  명령 라이브러리를 구성하는 클래스는 <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.ComponentCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.MediaCommands> 및 <xref:System.Windows.Documents.EditingCommands>입니다.  
  
 이러한 클래스를 구성하는 정적 <xref:System.Windows.Input.RoutedCommand> 개체는 명령 논리를 제공하지 않습니다.  명령 논리는 <xref:System.Windows.Input.CommandBinding>이 있는 명령과 연결됩니다.  일부 컨트롤에는 일부 명령에 대한 CommandBindings가 기본 제공되어 있습니다.  이 메커니즘을 사용하면 명령의 의미 체계를 동일하게 유지하면서 실제 구현을 변경할 수 있습니다.  예를 들어 <xref:System.Windows.Controls.TextBox>는 이미지를 지원하도록 설계된 컨트롤과 다르게 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령을 처리하지만 붙여넣는 것의 의미에 대한 기본 개념은 동일하게 유지됩니다.  명령 논리는 명령에 의해 제공될 수 없으나 대신 컨트롤 또는 애플리케이션에 의해 제공되어야 합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 많은 컨트롤은 명령 라이브러리의 일부 명령에 대한 지원을 기본 제공합니다.  예를 들어 <xref:System.Windows.Controls.TextBox>는 <xref:System.Windows.Input.ApplicationCommands.Paste%2A>, <xref:System.Windows.Input.ApplicationCommands.Copy%2A>, <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.ApplicationCommands.Redo%2A> 및 <xref:System.Windows.Input.ApplicationCommands.Undo%2A> 등의 많은 애플리케이션 편집 명령을 지원합니다.  애플리케이션 개발자는 이러한 명령을 컨트롤과 함께 사용하기 위해 별도로 해야 하는 작업은 없습니다.  명령이 실행될 때 <xref:System.Windows.Controls.TextBox>가 명령 대상인 경우는 컨트롤에 내장되어 있는 <xref:System.Windows.Input.CommandBinding>을 사용하여 명령을 처리할 수 있습니다.  
  
 다음은 <xref:System.Windows.Controls.TextBox>가 명령 대상인 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령에 대한 명령 소스로 <xref:System.Windows.Controls.MenuItem>을 사용하는 방법을 표시합니다.  <xref:System.Windows.Controls.TextBox>가 붙여넣기를 수행하는 방법을 정의하는 모든 논리가 <xref:System.Windows.Controls.TextBox> 컨트롤에 기본 제공됩니다.  
  
 <xref:System.Windows.Controls.MenuItem>이 만들어지고 <xref:System.Windows.Controls.MenuItem.Command%2A> 속성이 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령으로 설정됩니다.  <xref:System.Windows.Controls.MenuItem.CommandTarget%2A>이 명시적으로 <xref:System.Windows.Controls.TextBox> 개체로 설정되지 않습니다.  <xref:System.Windows.Controls.MenuItem.CommandTarget%2A>이 설정되지 않는 경우 명령의 대상은 키보드 포커스가 있는 요소입니다.  키보드 포커스가 있는 요소가 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령을 지원하지 않거나 현재 붙여넣기 명령을 실행할 수 없는 경우(예를 들어 클립보드가 비어있는 경우) <xref:System.Windows.Controls.MenuItem>이 회색으로 표시됩니다.  
  
 [!code-xaml[MenuItemCommandTask_XAML#MenuItemCommanding](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask_XAML/CS/Window1.xaml#menuitemcommanding)]  
  
 [!code-csharp[MenuItemCommandTask#MenuItemCommandingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask/CSharp/Window1.xaml.cs#menuitemcommandingcodebehind)]
 [!code-vb[MenuItemCommandTask#MenuItemCommandingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandTask/VisualBasic/Window1.xaml.vb#menuitemcommandingcodebehind)]  
  
## <a name="see-also"></a>참고자료

- [명령 개요](commanding-overview.md)
- [명령을 지원하지 않는 컨트롤에 명령 후크](how-to-hook-up-a-command-to-a-control-with-no-command-support.md)
