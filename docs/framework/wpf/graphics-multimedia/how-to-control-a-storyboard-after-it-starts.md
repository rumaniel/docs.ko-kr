---
title: '방법: 스토리 보드가 시작 된 후 제어'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], controlling after start
ms.assetid: 040f13f0-69f9-4ab5-be2b-079f4f80c7c0
ms.openlocfilehash: de30cfdb49df721cb4d6845dc67464e8a5b61f93
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855868"
---
# <a name="how-to-control-a-storyboard-after-it-starts"></a>방법: 스토리 보드가 시작 된 후 제어

이 예제에서는 코드를 사용 하 여를 <xref:System.Windows.Media.Animation.Storyboard> 시작한 후 제어 하는 방법을 보여 줍니다. 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]storyboard를 제어 하려면 및 <xref:System.Windows.TriggerAction> 개체 <xref:System.Windows.Trigger> 를 사용 합니다. 예를 들어 [이벤트 트리거를 사용 하 여 storyboard를 시작한 후 제어를](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)참조 하세요.

Storyboard를 시작 하려면 해당 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드를 사용 합니다 .이 메서드는 스토리 보드의 애니메이션을 애니메이션 효과를 주는 속성에 배포 하 고 스토리 보드를 시작 합니다.

Storyboard를 제어 가능 하 게 만들려면 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 메서드를 사용 하 고 **true** 를 두 번째 매개 변수로 지정 합니다. 그런 다음 storyboard의 대화형 메서드를 사용 하 여 스토리 보드를 일시 중지, 다시 시작, 검색, 중지, 속도를 늘리거나 줄일 수 있습니다. 다음은 storyboard의 대화형 메서드 목록입니다.

- <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>: 스토리 보드를 일시 중지 합니다.

- <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>: 일시 중지 된 스토리 보드를 다시 시작 합니다.

- <xref:System.Windows.Media.Animation.Storyboard.SetSpeedRatio%2A>: 스토리 보드의 대화형 속도를 설정 합니다.

- <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>: 지정 된 위치에서 storyboard를 검색 합니다.

- <xref:System.Windows.Media.Animation.Storyboard.SeekAlignedToLastTick%2A>: 지정 된 위치에 대 한 storyboard를 검색 합니다. <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 메서드와 달리이 작업은 다음 틱 보다 먼저 처리 됩니다.

- <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>: 스토리 보드를 채우기 기간 (있는 경우)으로 이동 합니다.

- <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>: 스토리 보드를 중지 합니다.

다음 예제에서는 스토리 보드를 대화형으로 제어 하기 위해 여러 storyboard 메서드를 사용 합니다.

> [!NOTE]
> 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]트리거를 사용 하 여 스토리 보드를 제어 하는 예를 보려면 [시작 후 이벤트 트리거를 사용 하 여 스토리 보드 제어를](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)참조 하세요.

## <a name="example"></a>예제

[!code-csharp[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ControlStoryboardExample.cs#controlstoryboardexampleusingwholepage)]
[!code-vb[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/controlstoryboardexample.vb#controlstoryboardexampleusingwholepage)]

## <a name="see-also"></a>참고자료

- [Storyboard를 시작한 후 이벤트 트리거를 사용하여 제어](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)
