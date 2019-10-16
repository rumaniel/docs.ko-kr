---
title: '방법: 애니메이션 반복'
ms.date: 03/30/2017
helpviewer_keywords:
- RepeatBehavior property of timelines [WPF]
- repeating animating [WPF]
- Timelines RepeatBehavior property [WPF]
- animation [WPF], repeating
ms.assetid: e6f3b068-eeeb-47fd-8d40-8848c31f1e1e
ms.openlocfilehash: a80f72b0e67c13890d4befcbd5ab7c4a92a93fe7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942092"
---
# <a name="how-to-repeat-an-animation"></a>방법: 애니메이션 반복
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 속성을 <xref:System.Windows.Media.Animation.Timeline> 애니메이션의 반복 동작을 제어 하기 위해.  
  
## <a name="example"></a>예제  
 합니다 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 속성을 <xref:System.Windows.Media.Animation.Timeline> 애니메이션이 단순 지속 시간을 반복 횟수를 제어 합니다. 사용 하 여 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>를 지정할 수 있습니다는 <xref:System.Windows.Media.Animation.Timeline> 동안 특정 횟수 만큼 반복 (반복 횟수) 또는 지정된 된 기간에 대 한 합니다. 두 경우 모두 애니메이션 하는 요청 된 횟수 또는 기간을 입력 하는 데 필요한 만큼 시작-끝 실행을 통해 이동 합니다.  
  
 기본적으로 타임 라인 반복 실행 횟수가 한 번만 재생 되 고 반복 되지 않는 1.0 적용 합니다. 그러나 설정 하는 경우는 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 의 속성을 <xref:System.Windows.Media.Animation.Timeline> 에 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>, 타임 라인이 무기한 반복 합니다.  
  
 다음 예제에서는 사용 하는 방법의 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 애니메이션의 반복 동작을 제어 하는 속성입니다. 예제에서는 애니메이션을 적용 합니다 <xref:System.Windows.FrameworkElement.Width%2A> 다른 유형의 반복 동작을 사용 하 여 각 사각형을 사용 하 여 5 개의 사각형의 속성입니다.  
  
 [!code-xaml[timingbehaviors_snip#RepeatBehaviorWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/RepeatBehaviorExample.xaml#repeatbehaviorwholepage)]  
  
 전체 샘플을 참조 하세요 [애니메이션 타이밍 동작 샘플](https://go.microsoft.com/fwlink/?LinkID=159970)합니다.  
  
## <a name="see-also"></a>참고자료

- [주기가 반복되는 동안 애니메이션 값 누적](how-to-accumulate-animation-values-during-repeat-cycles.md)
- [타임라인을 자동으로 뒤집을지 여부 지정](how-to-specify-whether-a-timeline-automatically-reverses.md)
- [애니메이션 및 타이밍 방법 항목](animation-and-timing-how-to-topics.md)
- [애니메이션 개요](animation-overview.md)
- [애니메이션 타이밍 동작 샘플](https://go.microsoft.com/fwlink/?LinkID=159970)
