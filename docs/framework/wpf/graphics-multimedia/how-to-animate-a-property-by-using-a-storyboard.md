---
title: '방법: 스토리보드를 사용하여 속성에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], Storyboards
- Storyboards [WPF], animation
ms.assetid: f4a314e9-1da2-4367-85fc-1232487efa7a
ms.openlocfilehash: a7a2656d84d37d3e2726df009a07ccf29661df07
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963037"
---
# <a name="how-to-animate-a-property-by-using-a-storyboard"></a>방법: 스토리보드를 사용하여 속성에 애니메이션 효과 주기
이 예제에서는를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하 여 속성에 애니메이션 효과를 주는 방법을 보여 줍니다. 을 <xref:System.Windows.Media.Animation.Storyboard>사용 하 여 속성에 애니메이션 효과를 주려면 애니메이션 효과를 적용할 각 속성에 대 한 애니메이션을 만들고 애니메이션 <xref:System.Windows.Media.Animation.Storyboard> 을 포함 하는을 만듭니다.  
  
 속성 형식에 따라 사용할 애니메이션 형식이 결정됩니다. 예를 들어 <xref:System.Double> 값을 사용 하는 속성에 애니메이션 효과를 <xref:System.Windows.Media.Animation.DoubleAnimation>주려면를 사용 합니다. <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 및<xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 연결 된 속성은 애니메이션이 적용 되는 개체 및 속성을 지정 합니다.  
  
 에서 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]storyboard를 시작 하려면 <xref:System.Windows.Media.Animation.BeginStoryboard> 작업과 <xref:System.Windows.EventTrigger>를 사용 합니다. 는 <xref:System.Windows.EventTrigger> 속성<xref:System.Windows.EventTrigger.RoutedEvent%2A> 에 <xref:System.Windows.Media.Animation.BeginStoryboard> 지정 된 이벤트가 발생할 때 작업을 시작 합니다. 작업 <xref:System.Windows.Media.Animation.BeginStoryboard> 은를 <xref:System.Windows.Media.Animation.Storyboard>시작 합니다.  
  
 다음 예제에서는 개체 <xref:System.Windows.Media.Animation.Storyboard> 를 사용 하 여 <xref:System.Windows.Controls.Button> 두 컨트롤에 애니메이션 효과를 적용 합니다. 첫 번째 단추의 크기 <xref:System.Windows.FrameworkElement.Width%2A> 를 변경 하려면에 애니메이션을 적용 합니다. 두 번째 단추의 색을 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 변경 하려면 <xref:System.Windows.Media.SolidColorBrush> 의 속성을 사용 하 여 애니메이션 효과가 적용 되 <xref:System.Windows.Controls.Control.Background%2A> 는 단추의를 설정 합니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[AnimatePropertyStoryboards#1](~/samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/StoryboardExample.xaml#1)]  
  
> [!NOTE]
> 애니메이션은 <xref:System.Windows.Controls.Control> 또는 <xref:System.Windows.FrameworkElement> <xref:System.Windows.Freezable> 와같은<xref:System.Windows.Media.Brush> 개체와 <xref:System.Windows.FrameworkElement.Name%2A> 또는 등의개체를모두대상으로할수있지만프레임워크요소만속성을가집니다.<xref:System.Windows.Media.Transform> <xref:System.Windows.Controls.Panel> 애니메이션의 대상으로 지정될 수 있게 freezable에 이름을 할당하려면 이전 예제와 같이 [x:Name 지시문](../../xaml-services/x-name-directive.md)을 사용합니다.  
  
 코드를 사용 하는 경우에는에 <xref:System.Windows.NameScope> <xref:System.Windows.FrameworkElement> 대 한를 만들고 <xref:System.Windows.FrameworkElement>개체 이름을 등록 하 여 애니메이션 효과를 적용 해야 합니다. 코드에서 애니메이션을 시작 하려면를 사용 하 <xref:System.Windows.Media.Animation.BeginStoryboard> 여 작업 <xref:System.Windows.EventTrigger>을 사용 합니다. 필요에 따라 이벤트 처리기 및 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 의 <xref:System.Windows.Media.Animation.Storyboard>메서드를 사용할 수 있습니다. 다음 예제에서는 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드를 사용하는 방법을 보여 줍니다.  
  
 [!code-csharp[AnimatePropertyStoryboards#11](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimatePropertyStoryboards/CSharp/StoryboardExample.cs#11)]
 [!code-vb[AnimatePropertyStoryboards#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AnimatePropertyStoryboards/VisualBasic/StoryboardExample.vb#11)]  
  
 애니메이션 및 Storyboard에 대한 자세한 내용은 [애니메이션 개요](animation-overview.md)를 참조하세요.  
  
 코드를 사용 하는 경우 속성에 애니메이션 효과를 <xref:System.Windows.Media.Animation.Storyboard> 주기 위해 개체를 사용 하는 것으로 제한 되지 않습니다. 자세한 내용 및 예제에 대해서는 [Storyboard를 사용하지 않고 속성에 애니메이션 효과 주기](how-to-animate-a-property-without-using-a-storyboard.md) 및 [AnimationClock을 사용하여 속성에 애니메이션 효과 적용](how-to-animate-a-property-by-using-an-animationclock.md)을 참조하세요.
