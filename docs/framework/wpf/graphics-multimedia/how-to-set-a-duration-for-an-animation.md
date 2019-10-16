---
title: '방법: 애니메이션 지속 시간 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], duration
- Timelines [WPF], description
- duration of animations [WPF]
ms.assetid: 155034ef-7d00-4416-a73c-b1713992d2eb
ms.openlocfilehash: bdae1689ffeb8c54d756b9debbd26d57a052892d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651157"
---
# <a name="how-to-set-a-duration-for-an-animation"></a>방법: 애니메이션 지속 시간 설정
A <xref:System.Windows.Media.Animation.Timeline> 시간의 세그먼트와 세그먼트의 길이 타임 라인의 의해 결정 됩니다 나타내는 <xref:System.Windows.Duration>합니다. 경우는 <xref:System.Windows.Media.Animation.Timeline> 끝에 도달 하면 해당 기간의 재생이 중지 합니다. 경우는 <xref:System.Windows.Media.Animation.Timeline> 자식 타임 라인에도 재생을 중지 합니다. 애니메이션의 경우는 <xref:System.Windows.Duration> 애니메이션 걸리는 전환에서 해당 시작 값 끝 값을 지정 합니다.  
  
 지정할 수 있습니다는 <xref:System.Windows.Duration> 제한 된 특정 시간 또는 특수 한 값을 가진 <xref:System.Windows.Duration.Automatic%2A> 또는 <xref:System.Windows.Duration.Forever%2A>합니다. 애니메이션에서 정의 되 고 유한 길이가 항상 있어야 하므로 애니메이션의 지속 시간 값을 반드시 해야-그러지 애니메이션 사실을 해당 대상 값 사이 전환 하는 방법을 알지 못합니다. 컨테이너 타임 라인 (<xref:System.Windows.Media.Animation.TimelineGroup> 개체)와 같은 <xref:System.Windows.Media.Animation.Storyboard> 하 고 <xref:System.Windows.Media.Animation.ParallelTimeline>, 기본 기간이 <xref:System.Windows.Duration.Automatic%2A>, 즉, 마지막 자식의 재생이 중지 되 면 자동으로 종료 합니다.  
  
 다음 예제에서는, 너비, 높이 및 채우기 색에서을 <xref:System.Windows.Shapes.Rectangle> 애니메이션 효과가 적용 됩니다. 애니메이션의 인지 된 속도 제어 하 고 컨테이너 타임 라인의 기간을 사용 하 여 자식 타임 라인이 기간 재정의 포함 하 여 애니메이션 효과 애니메이션 및 컨테이너 타임 라인의 기간 설정 됩니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[timingbehaviors_snip#DurationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/DurationExample.xaml#durationexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Duration>
- [애니메이션 개요](animation-overview.md)
