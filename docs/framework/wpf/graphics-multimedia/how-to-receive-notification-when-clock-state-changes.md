---
title: '방법: 시계 상태 변경 시 알림 받기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clocks [WPF], notification of state changes
- notifications [WPF], clocks' state changes
ms.assetid: ecb10fc9-d0c2-45c3-b0a1-7b11baa733da
ms.openlocfilehash: dc3fffb88ce59ceb908d6febd2f078820513b641
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942140"
---
# <a name="how-to-receive-notification-when-a-clocks-state-changes"></a>방법: 시계 상태 변경 시 알림 받기
시계의 <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> 이벤트가 발생할 때 해당 <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> 시계가 시작 되거나 중지 될 때와 같은 유효 하지 않게 합니다. 이 이벤트를 사용 하 여 직접 등록할 수 있습니다는 <xref:System.Windows.Media.Animation.Clock>를 사용 하 여 등록할 수 있습니다 또는 <xref:System.Windows.Media.Animation.Timeline>.  
  
 다음 예제에서는 <xref:System.Windows.Media.Animation.Storyboard> 두 개의 <xref:System.Windows.Media.Animation.DoubleAnimation> 개체 두 개의 사각형의 너비를 애니메이션을 적용 하는 데 사용 됩니다. <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 이벤트 clock 상태 변경 내용을 수신 대기 하는 데 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[timingbehaviors_snip#_graphicsmm_StateExampleMarkupWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml#_graphicsmm_stateexamplemarkupwholepage)]  
  
 [!code-csharp[timingbehaviors_snip#_graphicsmm_StateEventHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml.cs#_graphicsmm_stateeventhandlers)]
 [!code-vb[timingbehaviors_snip#_graphicsmm_StateEventHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/stateexample.xaml.vb#_graphicsmm_stateeventhandlers)]  
  
 다음 그림에서는 부모 타임 라인으로 입력 하는 다양 한 상태 애니메이션을 보여 줍니다 (*스토리 보드*)까지 진행 됩니다.  
  
 ![두 개의 애니메이션이 있는 Storyboard에 대 한 상태를 클록](./media/graphicsmm-3timelines.png "graphicsmm_3timelines")  
  
 다음 표에서는 시간을 보여 줍니다 *Animation1*의 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 이벤트가 발생 합니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
|시간 (초)|1|10|19|21|30|39|  
|상태|활성|활성|중지됨|활성|활성|중지됨|  
  
 다음 표에서는 시간을 보여 줍니다 *Animation2*의 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 이벤트가 발생 합니다.  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
|시간 (초)|1|10|11|19|21|29|31|39|  
|상태|활성|채우기|활성|중지됨|활성|채우기|활성|중지됨|  
  
 있음을 *Animation1*의 <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> 상태로 유지 하는 경우에 이벤트가 발생 10 초로 <xref:System.Windows.Media.Animation.ClockState.Active>합니다. 10 초 내에 상태가 변경 하지만에서 변경할 때문입니다 <xref:System.Windows.Media.Animation.ClockState.Active> 하 <xref:System.Windows.Media.Animation.ClockState.Filling> 다시 <xref:System.Windows.Media.Animation.ClockState.Active> 동일한 눈금에서.
