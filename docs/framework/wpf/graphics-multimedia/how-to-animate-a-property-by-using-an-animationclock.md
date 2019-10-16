---
title: '방법: AnimationClock을 사용하여 속성에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], properties [WPF], with AnimationClocks
- AnimationClocks [WPF]
ms.assetid: e6542021-714c-4675-9567-04f1c7380834
ms.openlocfilehash: 13d91e8589c40d84ba374ffc613388e24407796a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591283"
---
# <a name="how-to-animate-a-property-by-using-an-animationclock"></a>방법: AnimationClock을 사용하여 속성에 애니메이션 효과 주기
이 예제에 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Media.Animation.Clock> 속성 애니메이션을 적용 하는 개체입니다.  
  
 종속성 속성에 애니메이션을 적용하는 방법에는 다음 세 가지가 있습니다.  
  
- 만들기는 <xref:System.Windows.Media.Animation.AnimationTimeline> 를 사용 하 여 해당 속성을 사용 하 여 연결을 <xref:System.Windows.Media.Animation.Storyboard>입니다.  
  
- 개체를 사용 하 여 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 단일 적용 방법 <xref:System.Windows.Media.Animation.AnimationTimeline> 대상 속성에 있습니다.  
  
- 만들기는 <xref:System.Windows.Media.Animation.AnimationClock> 에서 <xref:System.Windows.Media.Animation.AnimationTimeline> 속성에 적용 합니다.  
  
 <xref:System.Windows.Media.Animation.Storyboard> 개체 및 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 방법을 사용 하면 직접 만들어 시계를 배포 하지 않고 속성에 애니메이션 효과를 (예를 참조 하십시오 [Storyboard를 사용 하 여 속성에 애니메이션 효과](how-to-animate-a-property-by-using-a-storyboard.md) 및 [를 속성 없이 애니메이션 효과 주기 스토리 보드를 사용 하 여](how-to-animate-a-property-without-using-a-storyboard.md)); 클록 생성 및 자동으로 배포 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.Animation.AnimationClock> 두 개의 비슷한 속성에 적용 합니다.  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 대화형으로 제어 하는 방법을 보여 주는 예는 <xref:System.Windows.Media.Animation.Clock> 시작 되 면 참조 [대화형으로 Clock 제어](how-to-interactively-control-a-clock.md)입니다.  
  
## <a name="see-also"></a>참고자료

- [Storyboard를 사용하여 속성에 애니메이션 효과 주기](how-to-animate-a-property-by-using-a-storyboard.md)
- [Storyboard를 사용하지 않고 속성에 애니메이션 효과 주기](how-to-animate-a-property-without-using-a-storyboard.md)
- [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)
