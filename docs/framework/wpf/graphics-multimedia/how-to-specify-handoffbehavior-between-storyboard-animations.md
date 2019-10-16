---
title: '방법: 스토리보드 애니메이션 간의 HandoffBehavior 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- Storyboards [WPF], handoff behavior between animations
- animation [WPF], handoff behavior between
ms.assetid: 97bd6842-929b-49d9-813e-46553ae46472
ms.openlocfilehash: d7129d6a48bdf31dc4953bb450267ad3b38fdd17
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651040"
---
# <a name="how-to-specify-handoffbehavior-between-storyboard-animations"></a>방법: 스토리보드 애니메이션 간의 HandoffBehavior 지정
이 예제에서는 storyboard 애니메이션 간의 전달 동작을 지정 하는 방법을 보여 줍니다. 합니다 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> 의 속성 <xref:System.Windows.Media.Animation.BeginStoryboard> 새로운 애니메이션 지정 속성에 이미 적용 된 기존 애니메이션과 상호 작용 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 단추 위로 마우스 커서를 움직이면 확대 커지고 커서를 만듭니다. 단추 위로 마우스를 가져가면 다음 커서를 신속 하 게 제거 하는 경우 두 번째 애니메이션이 첫 번째 작업이 완료 되기 전에 적용 됩니다. 간의 차이 볼 수 있는 다음과 같은 두 개의 애니메이션이 겹칠 때의 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> 의 값 <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> 및 <xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace>합니다. 값이 <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> 애니메이션 값 간에 전환을 더 부드럽게 오버랩 애니메이션 결합 <xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace> 겹치는 이전 즉시 바꾸려면 새 애니메이션이 합니다.  
  
 [!code-xaml[timingbehaviors_snip#HandoffBehaviorWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/HandoffBehaviorExample.xaml#handoffbehaviorwholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.BeginStoryboard>
- <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>
- [애니메이션 개요](animation-overview.md)
- [애니메이션 및 타이밍 방법 항목](animation-and-timing-how-to-topics.md)
