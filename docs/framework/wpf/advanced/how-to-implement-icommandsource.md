---
title: '방법: ICommandSource 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ICommandSource interfaces [WPF], implementing
ms.assetid: 7452dd39-6e11-44bf-806a-31d87f3772ac
ms.openlocfilehash: 218a17f221598ac29213bd28a0f04adb16bc933b
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59107369"
---
# <a name="how-to-implement-icommandsource"></a>방법: ICommandSource 구현
이 예제에는 구현 하 여 명령 소스를 만드는 방법을 보여 줍니다 <xref:System.Windows.Input.ICommandSource>합니다.  명령 소스는 명령을 호출 하는 방법을 인식 하는 개체입니다.  합니다 <xref:System.Windows.Input.ICommandSource> 세 가지 멤버를 노출 하는 인터페이스: <xref:System.Windows.Input.ICommandSource.Command%2A>를 <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>, 및 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>합니다.  <xref:System.Windows.Input.ICommandSource.Command%2A> 호출 되는 명령이입니다. <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> 명령 소스에서 명령을 처리 하는 메서드로 전달 되는 사용자 정의 데이터 형식입니다. <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 는 명령이 실행 되는 개체입니다.  
  
 이 예제에서는 클래스는 서브 클래스를 만들 합니다 <xref:System.Windows.Controls.Slider> 컨트롤과 구현 <xref:System.Windows.Input.ICommandSource>합니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 다양 한 구현 하는 클래스를 제공 <xref:System.Windows.Input.ICommandSource>와 같은 <xref:System.Windows.Controls.Button>를 <xref:System.Windows.Controls.MenuItem>, 및 <xref:System.Windows.Controls.ListBoxItem>합니다.  명령 소스는 명령을 호출 하는 방법을 정의 합니다.   <xref:System.Windows.Controls.Button> 및 <xref:System.Windows.Controls.MenuItem> 클릭할 때 명령을 호출 합니다.  <xref:System.Windows.Controls.ListBoxItem> 두 번 클릭할 때 명령을 호출 합니다. 이러한 클래스에만 명령이 될 원본에 해당 <xref:System.Windows.Input.ICommandSource.Command%2A> 속성을 설정 합니다.  
  
 이 예제에서는 슬라이더를 이동 하는 경우 명령을 호출할 또는 보다 정확 하 게 때는 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 속성이 변경 될 합니다.  
  
 다음은 클래스 정의 합니다.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceClassDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourceclassdefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceClassDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourceclassdefinition)]  
  
 다음 단계를 구현 하는 것은 <xref:System.Windows.Input.ICommandSource> 멤버입니다.  이 예제에서는 속성으로 구현 됩니다 <xref:System.Windows.DependencyProperty> 개체입니다.  이렇게 하면 데이터 바인딩을 사용 하 여 속성을 수 있습니다.  에 대 한 자세한 내용은 합니다 <xref:System.Windows.DependencyProperty> 클래스를 참조 하십시오 합니다 [종속성 속성 개요](dependency-properties-overview.md)합니다.  데이터 바인딩에 대 한 자세한 내용은 참조는 [데이터 바인딩 개요](../data/data-binding-overview.md)합니다.  
  
 만 <xref:System.Windows.Input.ICommandSource.Command%2A> 속성은 다음과 같습니다.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandpropertydefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandpropertydefinition)]  
  
 다음은는 <xref:System.Windows.DependencyProperty> 콜백 변경 합니다.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandChanged](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandchanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandChanged](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandchanged)]  
  
 다음 단계를 추가 및 제거 명령 소스와 연결 된 명령입니다.  <xref:System.Windows.Input.ICommandSource.Command%2A> 속성 단순히 덮어쓸 수 없습니다 새 명령을 추가 되 면 이전 명령과 사용 하 여 이벤트 처리기를 연결 하기 때문에 있는 경우 하나를 먼저 제거 해야 합니다.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcehookunhookcommands)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcehookunhookcommands)]  
  
 마지막 단계에 대 한 논리를 만드는 것은 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 처리기 및 <xref:System.Windows.Input.ICommand.Execute%2A> 메서드.  
  
 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 이벤트 현재 명령 대상에서 실행할 명령의 실행 가능성이 변경 된 경우 명령 소스를 알립니다.  일반적으로 호출 명령 소스는이 이벤트를 받을 때의 <xref:System.Windows.Input.ICommand.CanExecute%2A> 명령에는 메서드.  현재 명령 대상에서 명령을 실행할 수 없습니다, 하는 경우 명령 소스는 일반적으로 자체적으로 비활성화 됩니다.  명령이 현재 명령 대상에서를 실행 하는 경우 명령 소스는 일반적으로 자체적으로 활성화 됩니다.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandCanExecuteChanged](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandcanexecutechanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandCanExecuteChanged](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandcanexecutechanged)]  
  
 마지막 단계는 <xref:System.Windows.Input.ICommand.Execute%2A> 메서드.  명령이 <xref:System.Windows.Input.RoutedCommand>, <xref:System.Windows.Input.RoutedCommand> <xref:System.Windows.Input.RoutedCommand.Execute%2A> 방법이 고, 그렇지 않으면 호출 합니다 <xref:System.Windows.Input.ICommand> <xref:System.Windows.Input.ICommand.Execute%2A> 메서드가 호출 됩니다.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandExecute](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandexecute)]
 [!code-vb[ImplementICommandSource#ImplementICommandExecute](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandexecute)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Input.ICommandSource>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.Input.RoutedCommand>
- [명령 개요](commanding-overview.md)
