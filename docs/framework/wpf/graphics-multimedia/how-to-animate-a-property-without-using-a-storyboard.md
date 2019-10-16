---
title: '방법: 스토리보드를 사용하지 않고 속성에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- non-Storyboard animation
- local animation [WPF]
- animation [WPF], non-Storyboard (local)
ms.assetid: d411db70-4df7-487d-82bc-95a7c1b2e7f8
ms.openlocfilehash: 71711c0392576930e97986078ec5926ff6ca9813
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963021"
---
# <a name="how-to-animate-a-property-without-using-a-storyboard"></a>방법: 스토리보드를 사용하지 않고 속성에 애니메이션 효과 주기
이 예제에서는를 <xref:System.Windows.Media.Animation.Storyboard>사용 하지 않고 속성에 애니메이션을 적용 하는 한 가지 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 기능은 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]에서 사용할 수 없습니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서 속성에 애니메이션 효과를 주는 방법에 대한 자세한 내용은 [Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)를 참조하세요.  
  
 속성에 로컬 애니메이션을 적용 하려면 <xref:System.Windows.UIElement.BeginAnimation%2A> 메서드를 사용 합니다. 이 메서드는 애니메이션 효과를 지정 <xref:System.Windows.DependencyProperty> 하는 및 해당 속성에 적용할 애니메이션을 지정 하는 두 개의 매개 변수를 사용 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 <xref:System.Windows.Controls.Button>너비 및 배경색에 애니메이션 효과를 주는 방법을 보여 줍니다.  
  
 [!code-cpp[animateproperty#11](~/samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](~/samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
 <xref:System.Windows.Media.Animation> 네임 스페이스의 다양 한 애니메이션 클래스는 다양 한 형식의 속성에 애니메이션 효과를 주기 위해 존재 합니다. 속성 애니메이션에 대한 자세한 내용은 [애니메이션 개요](animation-overview.md)를 참조하십시오. 종속성 속성(이 예제에 표시되는 속성의 형식) 및 해당 기능에 대한 자세한 내용은 [종속성 속성 개요](../advanced/dependency-properties-overview.md)를 참조하세요.  
  
 개체를 사용 <xref:System.Windows.Media.Animation.Storyboard> 하지 않고 애니메이션 효과를 주는 다른 방법이 있습니다. 자세한 내용은 [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.AnimationTimeline>
- <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>
- <xref:System.Windows.Media.Animation>
- <xref:System.Windows.Media.Animation.Storyboard>
- [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)
- [애니메이션 개요](animation-overview.md)
