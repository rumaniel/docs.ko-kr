---
title: '방법: 자식 Timeline을 사용하여 애니메이션 단순화'
ms.date: 03/30/2017
helpviewer_keywords:
- simplifying animations by child timelines [WPF]
- animation [WPF], simplifying by child timelines
- child timelines [WPF]
ms.assetid: 8335d770-d13d-42bd-8dfa-63f92c0327e2
ms.openlocfilehash: 21a297208be045eea79d6f5ca6c8eac016d26345
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61804015"
---
# <a name="how-to-simplify-animations-by-using-child-timelines"></a>방법: 자식 Timeline을 사용하여 애니메이션 단순화
이 예제에서는 자식을 사용 하 여 애니메이션 단순화 <xref:System.Windows.Media.Animation.ParallelTimeline> 개체입니다. <xref:System.Windows.Media.Animation.Storyboard> 유형의 <xref:System.Windows.Media.Animation.Timeline> 있기 타임 라인에 대 한 대상 정보를 제공 합니다. 사용 하 여를 <xref:System.Windows.Media.Animation.Storyboard> 타임 라인 대상 개체 및 속성 정보를 포함 한 정보를 제공 합니다.  
  
 애니메이션을 시작 하려면 사용 하 여 하나 이상의 <xref:System.Windows.Media.Animation.ParallelTimeline> 개체의 중첩 된 자식 요소로 <xref:System.Windows.Media.Animation.Storyboard>합니다. 이러한 <xref:System.Windows.Media.Animation.ParallelTimeline> 개체 다른 애니메이션과 포함 될 수 있으며 따라서 복잡 한 애니메이션에서 타이밍 시퀀스를 캡슐화 수 있습니다. 예를 들어, 애니메이트 하는 경우는 <xref:System.Windows.Controls.TextBlock> 과 같은 여러 셰이프 <xref:System.Windows.Media.Animation.Storyboard>에 대 한 애니메이션을 구분할 수 있습니다 합니다 <xref:System.Windows.Controls.TextBlock> 와 별도의 각 셰이프를 <xref:System.Windows.Media.Animation.ParallelTimeline>입니다. 때문에 각 <xref:System.Windows.Media.Animation.ParallelTimeline> 에 자체 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> 및 모든 자식 요소를 <xref:System.Windows.Media.Animation.ParallelTimeline> 이 기준으로 시작 <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A>, 타이밍은 더욱 효과적으로 캡슐화 합니다.  
  
 다음 예제에서는 두 가지 텍스트에 애니메이션을 적용 (<xref:System.Windows.Controls.TextBlock> 개체)에서 동일한 <xref:System.Windows.Media.Animation.Storyboard>입니다. A <xref:System.Windows.Media.Animation.ParallelTimeline> 중 하나의 애니메이션을 캡슐화 합니다 <xref:System.Windows.Controls.TextBlock> 개체입니다.  
  
 **성능 참고 사항:** 중첩 시킬 수 있지만 <xref:System.Windows.Media.Animation.Storyboard> 타임 라인, 서로의 내부 <xref:System.Windows.Media.Animation.ParallelTimeline>가 중첩 오버 헤드를 덜 필요 하기 때문에 더 적합 합니다. (합니다 <xref:System.Windows.Media.Animation.Storyboard> 클래스에서 상속 된 <xref:System.Windows.Media.Animation.ParallelTimeline> 클래스입니다.)  
  
## <a name="example"></a>예제  
 [!code-xaml[Timelines_snip#ParallelTimelineWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Timelines_snip/CS/ParallelTimelineExample.xaml#paralleltimelinewholepage)]  
  
## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [Storyboard 애니메이션 간의 HandoffBehavior 지정](how-to-specify-handoffbehavior-between-storyboard-animations.md)
