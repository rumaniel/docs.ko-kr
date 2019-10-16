---
title: '방법: 명령 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CommandBindings [WPF]
- commanding [WPF]
ms.assetid: d8016266-58d9-48f7-8298-a86b7ed49fbd
ms.openlocfilehash: bf01066a35672e1996f193abc6d76153e5e9dd46
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032002"
---
# <a name="how-to-enable-a-command"></a>방법: 명령 사용
다음 예제에서 명령을 사용 하는 방법을 보여 줍니다 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]합니다.  연결 하는 방법을 보여를 <xref:System.Windows.Input.RoutedCommand> 에 <xref:System.Windows.Controls.Button>, 만들기를 <xref:System.Windows.Input.CommandBinding>를 구현 하는 이벤트 처리기를 만들고를 <xref:System.Windows.Input.RoutedCommand>.  명령에 대 한 자세한 내용은 참조는 [명령 개요](commanding-overview.md)합니다.  
  
## <a name="example"></a>예제  
 코드의 첫 번째 섹션을 만듭니다는 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], 구성를 <xref:System.Windows.Controls.Button> 및 <xref:System.Windows.Controls.StackPanel>를 만들고를 <xref:System.Windows.Input.CommandBinding> 와 명령 처리기를 연결 하는 <xref:System.Windows.Input.RoutedCommand>합니다.  
  
 <xref:System.Windows.Input.ICommandSource.Command%2A> 의 속성을 <xref:System.Windows.Controls.Button> 연관 된를 <xref:System.Windows.Input.ApplicationCommands.Close%2A> 명령입니다.  
  
 합니다 <xref:System.Windows.Input.CommandBinding> 에 추가 되는 <xref:System.Windows.Input.CommandBindingCollection> 루트의 <xref:System.Windows.Window>합니다. <xref:System.Windows.Input.CommandBinding.Executed> 하 고 <xref:System.Windows.Input.CommandBinding.CanExecute> 이벤트 처리기는이 바인딩에 연결 및 연결 된는 <xref:System.Windows.Input.ApplicationCommands.Close%2A> 명령입니다.  
  
 없이 <xref:System.Windows.Input.CommandBinding> 명령 논리가만 명령을 호출 하는 메커니즘입니다.  경우는 <xref:System.Windows.Controls.Button> 를 클릭 하면는 <xref:System.Windows.Input.CommandManager.PreviewExecuted> <xref:System.Windows.RoutedEvent> 뒤에 명령 대상에서 발생 합니다 <xref:System.Windows.Input.CommandManager.Executed> <xref:System.Windows.RoutedEvent>.  이러한 이벤트를 찾고 요소 트리를 탐색 한 <xref:System.Windows.Input.CommandBinding> 해당 특정 명령에 대 한 합니다.  때문에 주목할 만한 것 <xref:System.Windows.RoutedEvent> 터널을 버블 요소 트리를 통해 기울여야 위치에서는 <xref:System.Windows.Input.CommandBinding> 것입니다.   경우는 <xref:System.Windows.Input.CommandBinding> 형제 명령 대상의 다른 노드로의 경로에 있지 않은 대상에 <xref:System.Windows.RoutedEvent>, <xref:System.Windows.Input.CommandBinding> 에 액세스할 수 없습니다.  
  
 [!code-xaml[EnableCloseCommand#CloseCommandBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml#closecommandbinding)]  
  
 [!code-csharp[EnableCloseCommand#CloseCommandBindingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandbindingcodebehind)]
 [!code-vb[EnableCloseCommand#CloseCommandBindingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandbindingcodebehind)]  
  
 구현 코드의 다음 섹션의 <xref:System.Windows.Input.CommandManager.Executed> 고 <xref:System.Windows.Input.CommandBinding.CanExecute> 이벤트 처리기입니다.  
  
 <xref:System.Windows.Input.CommandManager.Executed> 처리기 열려 있는 파일을 닫는 메서드를 호출 합니다.  <xref:System.Windows.Input.CommandBinding.CanExecute> 파일이 열려 있는지 여부를 확인 하기 위한 메서드를 호출 하는 처리기.  파일이 열려 있으면 <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> 로 설정 된 `true`이 고, 그렇지 않으면로 설정 된 `false`합니다.  
  
 [!code-csharp[EnableCloseCommand#CloseCommandHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandhandler)]
 [!code-vb[EnableCloseCommand#CloseCommandHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandhandler)]  
  
## <a name="see-also"></a>참고자료

- [명령 개요](commanding-overview.md)
