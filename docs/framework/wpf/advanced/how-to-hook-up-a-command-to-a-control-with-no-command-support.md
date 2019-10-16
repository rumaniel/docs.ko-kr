---
title: '방법: 명령을 지원하지 않는 컨트롤에 명령 후크'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Control class [WPF], attaching a RoutedCommand
- classes [WPF], Control [WPF], attaching a RoutedCommand
- RoutedCommand class [WPF], attaching to a Control
- classes [WPF], RoutedCommand [WPF], attaching to a Control
ms.assetid: dad08f64-700b-46fb-ad3f-fbfee95f0dfe
ms.openlocfilehash: 3ae45c9a9e33a3cb53ada6e1e5430ae0f9e6c198
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "71263301"
---
# <a name="how-to-hook-up-a-command-to-a-control-with-no-command-support"></a>방법: 명령을 지원하지 않는 컨트롤에 명령 후크
다음 예제는 <xref:System.Windows.Input.RoutedCommand>를 명령에 대한 지원을 기본 제공하지 않는 <xref:System.Windows.Controls.Control>에 후크하는 방법을 보여줍니다.  여러 소스에 명령을 후크하는 전체 샘플은 [Create a Custom RoutedCommand Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)(사용자 지정 RoutedCommand 만들기 샘플)을 참조하세요.  
  
## <a name="example"></a>예제  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]는 애플리케이션 프로그래머가 자주 접하게 되는 공용 명령의 라이브러리를 제공합니다.  명령 라이브러리를 구성하는 클래스는 <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.ComponentCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.MediaCommands> 및 <xref:System.Windows.Documents.EditingCommands>입니다.  
  
 이러한 클래스를 구성하는 정적 <xref:System.Windows.Input.RoutedCommand> 개체는 명령 논리를 제공하지 않습니다.  명령 논리는 <xref:System.Windows.Input.CommandBinding>이 있는 명령과 연결됩니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 많은 컨트롤은 명령 라이브러리의 일부 명령에 대한 지원을 기본 제공합니다.  예를 들어 <xref:System.Windows.Controls.TextBox>는 <xref:System.Windows.Input.ApplicationCommands.Paste%2A>, <xref:System.Windows.Input.ApplicationCommands.Copy%2A>, <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.ApplicationCommands.Redo%2A> 및 <xref:System.Windows.Input.ApplicationCommands.Undo%2A> 등의 많은 애플리케이션 편집 명령을 지원합니다.  애플리케이션 개발자는 이러한 명령을 컨트롤과 함께 사용하기 위해 별도로 해야 하는 작업은 없습니다.  명령이 실행될 때 <xref:System.Windows.Controls.TextBox>가 명령 대상인 경우는 컨트롤에 내장되어 있는 <xref:System.Windows.Input.CommandBinding>을 사용하여 명령을 처리할 수 있습니다.  
  
 다음은 <xref:System.Windows.Input.ApplicationCommands.Open%2A> 명령에 대한 명령 소스로 <xref:System.Windows.Controls.Button>을 사용하는 방법을 표시합니다.  지정된 <xref:System.Windows.Input.CanExecuteRoutedEventHandler> 및 <xref:System.Windows.Input.CanExecuteRoutedEventHandler>를 <xref:System.Windows.Input.RoutedCommand>와 연결하는 <xref:System.Windows.Input.CommandBinding>을 만듭니다.  
  
 먼저, 명령 소스를 만듭니다.  <xref:System.Windows.Controls.Button>은 명령 소스로 사용됩니다.  
  
 [!code-xaml[commandWithHandler#CommandHandlerCommandSource](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandsource)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerButtonCommandSource](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbuttoncommandsource)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerButtonCommandSource](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbuttoncommandsource)]  
  
 다음으로, <xref:System.Windows.Input.ExecutedRoutedEventHandler> 및 <xref:System.Windows.Input.CanExecuteRoutedEventHandler>를 만듭니다.  <xref:System.Windows.Input.ExecutedRoutedEventHandler>는 단순히 <xref:System.Windows.MessageBox>를 열어 명령이 실행되었음을 나타냅니다.  <xref:System.Windows.Input.CanExecuteRoutedEventHandler>는 <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> 속성을 `true`로 설정합니다.  일반적으로 실행 가능 처리기는 현재 명령 대상에서 명령을 실행할 수 있는지 확인하려면 보다 강력한 확인 작업을 수행합니다.  
  
 [!code-csharp[commandWithHandler#CommandHandlerBothHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerbothhandlers)]
 [!code-vb[commandWithHandler#CommandHandlerBothHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerbothhandlers)]  
  
 마지막으로, <xref:System.Windows.Input.CommandBinding>은 라우팅된 이벤트 처리기를 <xref:System.Windows.Input.ApplicationCommands.Open%2A> 명령에 연결하는 애플리케이션의 <xref:System.Windows.Window> 루트에 만들어집니다.  
  
 [!code-xaml[commandWithHandler#CommandHandlerCommandBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
## <a name="see-also"></a>참고 항목

- [명령 개요](commanding-overview.md)
- [명령을 지원하는 컨트롤에 명령 후크](how-to-hook-up-a-command-to-a-control-with-command-support.md)
