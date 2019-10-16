---
title: 명령 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interfaces [WPF], ICommandSource
- command library [WPF]
- commands [WPF], definition of
- CommandBindings [WPF]
- ICommandSource interfaces [WPF]
- commanding [WPF]
- CommandManager [WPF]
ms.assetid: bc208dfe-367d-426a-99de-52b7e7511e81
ms.openlocfilehash: 192fe629493947ffe4e0aa8ade417b7701ff95b4
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004602"
---
# <a name="commanding-overview"></a>명령 개요
<a name="introduction"></a> 명령은 디바이스 입력보다 더 의미 있는 수준의 입력 처리를 제공하는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]의 입력 메커니즘입니다. 이러한 명령의 예로는 많은 애플리케이션의 **복사**, **잘라내기** 및 **붙여넣기** 작업을 들 수 있습니다.  
  
 이 개요에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 명령, 명령 모델의 일부인 클래스 및 애플리케이션에서 명령을 사용하고 만드는 방법을 정의합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
- [명령이란?](#commands_at_10000_feet)  
  
- [WPF의 간단한 명령 예제](#simple_command)  
  
- [WPF 명령의 네 가지 주요 개념](#Four_main_Concepts)  
  
- [명령 라이브러리](#Command_Library)  
  
- [사용자 지정 명령 만들기](#creating_commands)  
  
<a name="commands_at_10000_feet"></a>   
## <a name="what-are-commands"></a>명령이란?  
 명령의 목적에는 몇 가지가 있습니다. 첫 번째 목적은 명령을 실행하는 논리에서 명령을 호출하는 개체와 의미 체계를 분리하는 것입니다. 이렇게 하면 여러 소스에서 동일한 명령 논리를 호출할 수 있고 명령 논리가 여러 대상에 대해 사용자 지정될 수 있습니다. 예를 들어 다양한 사용자 작업이 명령을 사용하여 구현된 경우 이러한 작업을 사용하여 많은 애플리케이션에 사용되는 편집 작업인 **복사**, **잘라내기** 및 **붙여넣기**를 호출할 수 있습니다. 애플리케이션에서 단추를 클릭하거나, 메뉴에서 항목을 선택하거나, Ctrl+X 등의 키 조합을 사용하여 사용자가 선택한 개체 또는 텍스트를 잘라낼 수 있습니다. 명령을 사용하여 각 사용자 작업 형식을 동일한 논리에 바인딩할 수 있습니다.  
  
 명령의 또 다른 목적은 작업을 사용할 수 있는지 여부를 나타내는 것입니다. 개체 또는 텍스트 잘라내기의 경우 항목을 선택했을 때만 의미를 갖습니다. 사용자가 아무것도 선택하지 않고 개체 또는 텍스트를 잘라내려고 하면 작업이 수행되지 않습니다. 많은 애플리케이션에서는 사용자가 작업 수행 가능 여부를 알 수 있도록 단추 및 메뉴 항목을 사용하지 않도록 설정합니다. 명령은 <xref:System.Windows.Input.ICommand.CanExecute%2A> 메서드를 구현하여 작업이 가능한지 여부를 나타낼 수 있습니다. 단추는 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 이벤트를 구독할 수 있으며 <xref:System.Windows.Input.ICommand.CanExecute%2A>가 `false`로 반환되는 경우 비활성화되고 <xref:System.Windows.Input.ICommand.CanExecute%2A>가 `true`로 반환되는 경우 활성화됩니다.  
  
 명령의 의미 체계는 모든 애플리케이션 및 클래스에서 일관적일 수 있지만 작업의 논리는 수행된 특정 개체에 따라 다릅니다. 텍스트 클래스, 이미지 클래스 및 웹 브라우저에서 Ctrl+X 키 조합을 사용하면 **Cut** 명령이 호출되지만 **잘라내기** 작업을 수행하는 실제 논리는 잘라내기를 수행하는 애플리케이션에 의해 정의됩니다. <xref:System.Windows.Input.RoutedCommand>가 클라이언트를 사용하여 논리를 구현합니다. 텍스트 개체는 선택한 텍스트를 클립보드로 잘라낼 수 있지만 이미지 개체는 선택한 이미지를 잘라낼 수 있습니다. 애플리케이션에서 <xref:System.Windows.Input.CommandManager.Executed> 이벤트를 처리할 때 명령 대상에 대한 액세스 권한이 있어야 대상의 형식에 따라 적절한 작업을 수행할 수 있습니다.  
  
<a name="simple_command"></a>   
## <a name="simple-command-example-in-wpf"></a>WPF의 간단한 명령 예제  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 명령을 사용하는 가장 간단한 방법은 명령 라이브러리 클래스 중 하나에서 미리 정의된 <xref:System.Windows.Input.RoutedCommand>를 사용하거나, 명령 처리 및 명령 호출을 기본적으로 지원하는 컨트롤을 사용하는 것입니다.  <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령은 <xref:System.Windows.Input.ApplicationCommands> 클래스에서 미리 정의된 명령 중 하나입니다.  <xref:System.Windows.Controls.TextBox> 컨트롤은 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령을 처리하기 위한 논리를 기본 제공합니다.  <xref:System.Windows.Controls.MenuItem> 클래스는 명령 호출을 기본적으로 지원합니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.MenuItem>을 설정하는 방법을 보여줘 클릭하는 경우 <xref:System.Windows.Controls.TextBox>에 키보드 포커스가 있다는 가정 하에 <xref:System.Windows.Controls.TextBox>에서 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령을 호출합니다.  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewSimpleCommand](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewsimplecommand)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]  
  
<a name="Four_main_Concepts"></a>   
## <a name="four-main-concepts-in-wpf-commanding"></a>WPF 명령의 네 가지 주요 개념  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 라우트된 명령 모델은 명령, 명령 소스, 명령 대상 및 명령 바인딩 네 가지 주요 개념으로 나눌 수 있습니다.  
  
- *명령*은 실행할 작업입니다.  
  
- *명령 소스*는 명령을 호출하는 개체입니다.  
  
- *명령 대상*은 명령이 실행되는 개체입니다.  
  
- *명령 바인딩*은 명령 논리를 명령에 매핑하는 개체입니다.  
  
 이전 예제에서 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령은 명령이며, <xref:System.Windows.Controls.MenuItem>은 명령 원본이며, <xref:System.Windows.Controls.TextBox>는 명령 대상이며, 명령 바인딩은 <xref:System.Windows.Controls.TextBox> 컨트롤에 의해 제공됩니다.  <xref:System.Windows.Input.CommandBinding>이 항상 명령 대상 클래스인 컨트롤에 의해 제공되는 것은 아닙니다.  매우 자주 <xref:System.Windows.Input.CommandBinding>은 애플리케이션 개발자에 의해 만들어져야 하거나, <xref:System.Windows.Input.CommandBinding>은 명령 대상의 상위 항목에 연결될 수 있습니다.  
  
<a name="Commands"></a>   
### <a name="commands"></a>명령  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 명령은 <xref:System.Windows.Input.ICommand> 인터페이스를 구현하여 만듭니다.  <xref:System.Windows.Input.ICommand>는 두 개의 메서드 <xref:System.Windows.Input.ICommand.Execute%2A>, <xref:System.Windows.Input.ICommand.CanExecute%2A> 및 하나의 이벤트 <xref:System.Windows.Input.ICommand.CanExecuteChanged>를 노출합니다. <xref:System.Windows.Input.ICommand.Execute%2A>는 명령과 연결되는 작업을 수행합니다. <xref:System.Windows.Input.ICommand.CanExecute%2A>는 현재 명령 대상에서 명령을 실행할 수 있는지 여부를 결정합니다. 명령 작업을 중앙 집중식으로 관리하는 명령 관리자가, 발생했지만 명령 바인딩에서 아직 실행하지 않은 명령을 무효화할 수 있는 변경 사항을 명령 소스에서 감지한 경우 <xref:System.Windows.Input.ICommand.CanExecuteChanged>가 발생합니다.  <xref:System.Windows.Input.ICommand>의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 구현은 <xref:System.Windows.Input.RoutedCommand> 클래스이며 이 개요의 포커스입니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 주 입력 소스는 마우스, 키보드, 잉크 및 라우트된 명령입니다.  더 많은 디바이스 지향 입력이 <xref:System.Windows.RoutedEvent>를 사용하여 애플리케이션 페이지의 개체에 입력 이벤트가 발생했음을 알립니다.  <xref:System.Windows.Input.RoutedCommand>도 마찬가지입니다.  <xref:System.Windows.Input.RoutedCommand>의 <xref:System.Windows.Input.RoutedCommand.Execute%2A> 및 <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> 메서드는 명령에 대한 애플리케이션 논리를 포함하지 않지만 <xref:System.Windows.Input.CommandBinding>이 있는 개체를 찾을 때까지 요소 트리를 통해 터널링 및 버블링하는 라우팅된 이벤트를 발생시킵니다.  <xref:System.Windows.Input.CommandBinding>에는 이러한 이벤트에 대한 처리기가 포함되어 있으며 이는 명령을 수행하는 처리기입니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 이벤트 라우팅에 대한 자세한 내용은 [라우트된 이벤트 개요](routed-events-overview.md)를 참조하세요.  
  
 <xref:System.Windows.Input.RoutedCommand>의 <xref:System.Windows.Input.RoutedCommand.Execute%2A> 메서드는 명령 대상에서 <xref:System.Windows.Input.CommandManager.PreviewExecuted> 및 <xref:System.Windows.Input.CommandManager.Executed> 이벤트를 발생시킵니다.  <xref:System.Windows.Input.RoutedCommand>의 <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> 메서드는 명령 대상에서 <xref:System.Windows.Input.CommandManager.CanExecute> 및 <xref:System.Windows.Input.CommandManager.PreviewCanExecute> 이벤트를 발생시킵니다.  이러한 이벤트는 특정 명령에 대한 <xref:System.Windows.Input.CommandBinding>이 있는 개체를 찾을 때까지 요소 트리를 통해 터널링 및 버블링합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 여러 클래스에 분산된 라우팅된 일반적인 명령 집합, <xref:System.Windows.Input.MediaCommands>, <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.ComponentCommands> 및 <xref:System.Windows.Documents.EditingCommands>를 공급합니다.  이러한 클래스는 <xref:System.Windows.Input.RoutedCommand> 개체로만 구성되며 명령의 구현 논리는 포함되지 않습니다.  구현 논리는 명령이 실행 중인 개체에서 제공해야 합니다.  
  
<a name="Command_Sources"></a>   
### <a name="command-sources"></a>명령 소스  
 명령 소스는 명령을 호출하는 개체입니다.  명령 소스의 예는 <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.Button> 및 <xref:System.Windows.Input.KeyGesture>입니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 명령 소스는 일반적으로 <xref:System.Windows.Input.ICommandSource> 인터페이스를 구현합니다.  
  
 <xref:System.Windows.Input.ICommandSource>는 <xref:System.Windows.Input.ICommandSource.Command%2A>, <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 및 <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>의 세 가지 속성을 노출합니다.  
  
- <xref:System.Windows.Input.ICommandSource.Command%2A>는 명령 소스가 호출될 때 실행할 명령입니다.  
  
- <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>은 명령을 실행하는 개체입니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 <xref:System.Windows.Input.ICommandSource>의 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 속성은 <xref:System.Windows.Input.ICommand>가 <xref:System.Windows.Input.RoutedCommand>인 경우에만 적용 가능합니다.  <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>이 <xref:System.Windows.Input.ICommandSource>에서 설정되고 해당 명령이 <xref:System.Windows.Input.RoutedCommand>가 아닌 경우 명령 대상은 무시됩니다. <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>이 설정되어 있지 않으면 키보드 포커스가 있는 요소가 명령 대상이 됩니다.  
  
- <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>는 명령을 구현하는 처리기에 정보를 전달하는 데 사용되는 사용자 정의 데이터 형식입니다.  
  
 <xref:System.Windows.Input.ICommandSource>를 구현하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 클래스는 <xref:System.Windows.Controls.Primitives.ButtonBase>, <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Documents.Hyperlink> 및 <xref:System.Windows.Input.InputBinding>입니다.  <xref:System.Windows.Controls.Primitives.ButtonBase>, <xref:System.Windows.Controls.MenuItem> 및 <xref:System.Windows.Documents.Hyperlink>는 클릭할 때 명령을 호출하며, <xref:System.Windows.Input.InputBinding>은 이와 연결된 <xref:System.Windows.Input.InputGesture>가 수행될 때 명령을 호출합니다.  
  
 다음 예제에서는 <xref:System.Windows.Input.ApplicationCommands.Properties%2A> 명령에 대한 명령 소스로 <xref:System.Windows.Controls.ContextMenu>에서 <xref:System.Windows.Controls.MenuItem>을 사용하는 방법을 표시합니다.  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewCmdSourceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcmdsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCmdSource](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcmdsource)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCmdSource](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcmdsource)]  
  
 일반적으로 명령 소스는 <xref:System.Windows.Input.RoutedCommand.CanExecuteChanged> 이벤트에 수신됩니다.  이 이벤트는 현재 명령 대상에서 명령을 실행할 수 있는 기능이 변경되었을 수 있음을 명령 소스에 알립니다.  명령 소스는 <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> 메서드를 사용하여 <xref:System.Windows.Input.RoutedCommand>의 현재 상태를 쿼리할 수 있습니다.  명령을 실행할 수 없는 경우 명령 소스는 자체적으로 사용하지 않도록 설정될 수 있습니다.  예를 들어 명령을 실행할 수 없는 경우 <xref:System.Windows.Controls.MenuItem>은 자체적으로 회색으로 표시됩니다.  
  
 <xref:System.Windows.Input.InputGesture>는 명령 소스로 사용할 수 있습니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 두 가지 형식의 입력 제스처는 <xref:System.Windows.Input.KeyGesture> 및 <xref:System.Windows.Input.MouseGesture>입니다.  CTRL+C 같은 키보드 바로 가기 키로 <xref:System.Windows.Input.KeyGesture>를 생각할 수 있습니다.  <xref:System.Windows.Input.KeyGesture>는 <xref:System.Windows.Input.Key> 및 <xref:System.Windows.Input.ModifierKeys>의 집합으로 이뤄져 있습니다.  <xref:System.Windows.Input.MouseGesture>는 <xref:System.Windows.Input.MouseAction> 및 <xref:System.Windows.Input.ModifierKeys>의 선택적 집합으로 이뤄져 있습니다.  
  
 <xref:System.Windows.Input.InputGesture>를 명령 소스로 사용하려면 명령과 연결되어야 합니다. 이 작업을 수행하는 방법은 몇 가지가 있습니다.  한 가지 방법은 <xref:System.Windows.Input.InputBinding>을 사용하는 것입니다.  
  
 다음 예제에서는 <xref:System.Windows.Input.KeyGesture> 및 <xref:System.Windows.Input.RoutedCommand> 간에 <xref:System.Windows.Input.KeyBinding>을 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewXAMLKeyBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewxamlkeybinding)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewKeyBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewkeybinding)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewKeyBinding](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewkeybinding)]  
  
 <xref:System.Windows.Input.InputGesture>를 <xref:System.Windows.Input.RoutedCommand>에 연결하는 다른 방법은 <xref:System.Windows.Input.RoutedCommand>에서 <xref:System.Windows.Input.InputGesture>를 <xref:System.Windows.Input.InputGestureCollection>에 추가하는 것입니다.  
  
 다음 예제에서는 <xref:System.Windows.Input.RoutedCommand>의 <xref:System.Windows.Input.InputGestureCollection>에 <xref:System.Windows.Input.KeyGesture>를 추가하는 방법을 보여 줍니다.  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewKeyGestureOnCmd](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewkeygestureoncmd)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewKeyGestureOnCmd](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewkeygestureoncmd)]  
  
<a name="Command_Binding"></a>   
### <a name="commandbinding"></a>CommandBinding  
 <xref:System.Windows.Input.CommandBinding>은 명령을 구현하는 이벤트 처리기와 명령을 연결합니다.  
  
 <xref:System.Windows.Input.CommandBinding> 클래스에는 <xref:System.Windows.Input.CommandBinding.Command%2A> 속성과 <xref:System.Windows.Input.CommandBinding.PreviewExecuted>, <xref:System.Windows.Input.CommandBinding.Executed>, <xref:System.Windows.Input.CommandBinding.PreviewCanExecute> 및 <xref:System.Windows.Input.CommandBinding.CanExecute> 이벤트가 포함됩니다.  
  
 <xref:System.Windows.Input.CommandBinding.Command%2A>는 <xref:System.Windows.Input.CommandBinding>이 연결되어 있는 명령입니다.  <xref:System.Windows.Input.CommandBinding.PreviewExecuted> 및 <xref:System.Windows.Input.CommandBinding.Executed> 이벤트에 연결되는 이벤트 처리기는 명령 논리를 구현합니다.  <xref:System.Windows.Input.CommandBinding.PreviewCanExecute> 및 <xref:System.Windows.Input.CommandBinding.CanExecute> 이벤트에 연결된 이벤트 처리기는 현재 명령 대상에서 명령을 실행할 수 있는지 결정합니다.  
  
 다음 예제에서는 애플리케이션의 루트 <xref:System.Windows.Window>에서 <xref:System.Windows.Input.CommandBinding>을 만드는 방법을 보여 줍니다.  <xref:System.Windows.Input.CommandBinding>은 <xref:System.Windows.Input.ApplicationCommands.Open%2A> 명령을 <xref:System.Windows.Input.CommandManager.Executed> 및 <xref:System.Windows.Input.CommandBinding.CanExecute> 처리기와 연결합니다.  
  
 [!code-xaml[commandwithhandler#CommandHandlerCommandBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
 다음으로, <xref:System.Windows.Input.ExecutedRoutedEventHandler> 및 <xref:System.Windows.Input.CanExecuteRoutedEventHandler>를 만듭니다.  <xref:System.Windows.Input.ExecutedRoutedEventHandler>는 <xref:System.Windows.MessageBox>를 열어 명령이 실행됐다는 문자열을 표시합니다.  <xref:System.Windows.Input.CanExecuteRoutedEventHandler>는 <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> 속성을 `true`로 설정합니다.  
  
 [!code-csharp[commandwithhandler#CommandHandlerExecutedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerexecutedhandler)]
 [!code-vb[commandwithhandler#CommandHandlerExecutedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerexecutedhandler)]  
  
 [!code-csharp[commandwithhandler#CommandHandlerCanExecuteHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlercanexecutehandler)]
 [!code-vb[commandwithhandler#CommandHandlerCanExecuteHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlercanexecutehandler)]  
  
 <xref:System.Windows.Input.CommandBinding>은 애플리케이션 또는 컨트롤의 루트 <xref:System.Windows.Window> 같은 특정 개체에 연결됩니다.  <xref:System.Windows.Input.CommandBinding>이 연결된 개체는 바인딩의 범위를 정의합니다.  예를 들어 명령 대상의 상위 항목에 연결된 <xref:System.Windows.Input.CommandBinding>은 <xref:System.Windows.Input.CommandBinding.Executed> 이벤트로 연결할 수 있지만 명령 대상의 하위 항목에 연결된 <xref:System.Windows.Input.CommandBinding>은 연결할 수 없습니다.  이는 이벤트를 발생시키는 개체에서 <xref:System.Windows.RoutedEvent>를 터널링 및 버블링할 때 발생하는 직접적인 결과입니다.  
  
 일부 경우에 <xref:System.Windows.Input.CommandBinding>은 <xref:System.Windows.Controls.TextBox> 클래스와 <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.ApplicationCommands.Copy%2A> 및 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령 같은 명령 대상 자체에 연결됩니다. 그러나 <xref:System.Windows.Input.CommandBinding>을 주 <xref:System.Windows.Window> 또는 애플리케이션 개체와 같은 명령 대상의 상위 항목에 연결하는 것이 더 편리할 때가 종종 있습니다. 특히 동일한 <xref:System.Windows.Input.CommandBinding>을 여러 명령 대상에 대해 사용할 수 있는 경우 그렇습니다.  명령 인프라를 만들 때 이러한 디자인 사항을 결정해야 합니다.  
  
<a name="Commane_Target"></a>   
### <a name="command-target"></a>명령 대상  
 명령 대상은 명령이 실행되는 요소입니다.  <xref:System.Windows.Input.RoutedCommand>와 관련하여 명령 대상은 <xref:System.Windows.Input.CommandManager.Executed> 및 <xref:System.Windows.Input.CommandManager.CanExecute>의 라우팅이 시작하는 요소입니다.  앞서 지적한 것처럼 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 <xref:System.Windows.Input.ICommandSource>의 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 속성은 <xref:System.Windows.Input.ICommand>가 <xref:System.Windows.Input.RoutedCommand>인 경우에만 적용 가능합니다.  <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>이 <xref:System.Windows.Input.ICommandSource>에서 설정되고 해당 명령이 <xref:System.Windows.Input.RoutedCommand>가 아닌 경우 명령 대상은 무시됩니다.  
  
 명령 소스는 명령 대상을 명시적으로 설정할 수 있습니다.  명령 대상이 정의되지 않은 경우 키보드 포커스가 있는 요소가 명령 대상으로 사용됩니다.  키보드 포커스가 있는 요소를 명령 대상으로 사용하면 애플리케이션 개발자가 명령 대상을 추적하지 않고도 동일한 명령 소스를 사용하여 여러 대상에서 명령을 호출할 수 있다는 장점이 있습니다.  예를 들어 <xref:System.Windows.Controls.MenuItem>이 <xref:System.Windows.Controls.TextBox> 컨트롤 및 <xref:System.Windows.Controls.PasswordBox> 컨트롤이 있는 애플리케이션에서 **붙여넣기** 명령을 호출하는 경우 대상은 키보드 포커스가 있는 컨트롤에 따라 <xref:System.Windows.Controls.TextBox> 또는 <xref:System.Windows.Controls.PasswordBox>일 수 있습니다.  
  
 다음 예제에서는 태그 및 코드 숨김에서 명령 대상을 명시적으로 설정하는 방법을 보여 줍니다.  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewXAMLCommandTarget](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewxamlcommandtarget)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]  
  
<a name="Command_Manager"></a>   
### <a name="the-commandmanager"></a>CommandManager  
 <xref:System.Windows.Input.CommandManager>는 여러 명령 관련 함수를 제공합니다.  특정 요소에 <xref:System.Windows.Input.CommandManager.PreviewExecuted>, <xref:System.Windows.Input.CommandManager.Executed>, <xref:System.Windows.Input.CommandManager.PreviewCanExecute> 및 <xref:System.Windows.Input.CommandManager.CanExecute> 이벤트 처리기를 추가하고 제거하기 위한 정적 메서드 집합을 제공합니다.  특정 클래스에 <xref:System.Windows.Input.CommandBinding> 및 <xref:System.Windows.Input.InputBinding> 개체를 등록하기 위한 수단을 제공합니다.  <xref:System.Windows.Input.CommandManager>는 <xref:System.Windows.Input.CommandManager.RequerySuggested> 이벤트를 통해 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 이벤트가 발행할 경우 명령을 알리기 위한 수단을 제공합니다.  
  
 <xref:System.Windows.Input.CommandManager.InvalidateRequerySuggested%2A> 메서드는 <xref:System.Windows.Input.CommandManager>가 <xref:System.Windows.Input.CommandManager.RequerySuggested> 이벤트를 발생시키도록 합니다.  이는 명령을 사용 또는 사용하지 않도록 설정해야 하지만 <xref:System.Windows.Input.CommandManager>가 인식하는 조건이 아닌 경우에 유용합니다.  
  
<a name="Command_Library"></a>   
## <a name="command-library"></a>명령 라이브러리  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 미리 정의된 명령 집합을 제공합니다.  명령 라이브러리는 다음과 같은 <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.MediaCommands>, <xref:System.Windows.Documents.EditingCommands> 및 <xref:System.Windows.Input.ComponentCommands> 클래스로 구성됩니다.  이러한 클래스는 <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.NavigationCommands.BrowseBack%2A> 및 <xref:System.Windows.Input.NavigationCommands.BrowseForward%2A>, <xref:System.Windows.Input.MediaCommands.Play%2A>, <xref:System.Windows.Input.MediaCommands.Stop%2A> 및 <xref:System.Windows.Input.MediaCommands.Pause%2A> 같은 명령을 제공합니다.  
  
 이 중 많은 명령이 기본 입력 바인딩 집합을 포함합니다.  예를 들어 응용 프로그램에서 복사 명령을 처리 하도록 지정 하는 경우 자동으로 키보드 바인딩 "CTRL + C"가 표시 되 고, Tablet PC 펜 제스처 및 음성 정보와 같은 다른 입력 장치에 대 한 바인딩도 표시 됩니다.  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용하여 다양한 명령 라이브러리에서 명령을 참조할 때 일반적으로 정적 명령 특성을 노출하는 라이브러리 클래스의 클래스 이름을 생략할 수 있습니다. 일반적으로 명령 이름은 문자열처럼 명확하지 않으며 명령의 논리적 그룹화를 제공하기 위한 소유 유형이 존재하지만 명확성을 위해 반드시 필요하지는 않습니다. 예를 들어 더 자세한 `Command="ApplicationCommands.Cut"` 대신 `Command="Cut"`을 지정할 수 있습니다. 이는 명령의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서에 기본 제공된 편리한 메커니즘입니다. 더 자세히 말해, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서가 로드 시 참조하는 <xref:System.Windows.Input.ICommand>의 형식 변환기 동작입니다.  
  
<a name="creating_commands"></a>   
## <a name="creating-custom-commands"></a>사용자 지정 명령 만들기  
 명령 라이브러리 클래스의 명령이 사용자 요구 사항을 충족시키지 못하면 사용자가 직접 명령을 만들 수 있습니다.  두 가지 방법으로 사용자 지정 명령을 만들 수 있습니다.  첫 번째 방법은 처음부터 시작하여 <xref:System.Windows.Input.ICommand> 인터페이스를 구현하는 것입니다.  다른 방식이자 보다 일반적인 방식은 <xref:System.Windows.Input.RoutedCommand> 또는 <xref:System.Windows.Input.RoutedUICommand>를 만드는 것입니다.  
  
 사용자 지정 <xref:System.Windows.Input.RoutedCommand>를 만드는 예제는 [사용자 지정 RoutedCommand 샘플 만들기](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)를 참조하세요.  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Input.RoutedCommand>
- <xref:System.Windows.Input.CommandBinding>
- <xref:System.Windows.Input.InputBinding>
- <xref:System.Windows.Input.CommandManager>
- [입력 개요](input-overview.md)
- [라우트된 이벤트 개요](routed-events-overview.md)
- [ICommandSource 구현](how-to-implement-icommandsource.md)
- [방법: MenuItem @ no__t에 명령 추가
- [Create a Custom RoutedCommand Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)(사용자 지정 RoutedCommand 샘플 만들기)
