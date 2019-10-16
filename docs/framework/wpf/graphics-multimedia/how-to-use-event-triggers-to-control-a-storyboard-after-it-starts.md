---
title: '방법: 스토리보드가 시작되면 이벤트 트리거를 사용하여 제어'
ms.date: 03/30/2017
helpviewer_keywords:
- triggers [WPF], controlling Storyboards
- event triggers [WPF], controlling Storyboards
- Storyboards [WPF], controlling after start
ms.assetid: 3b115594-6a93-4972-b24d-61aa16f1c15f
ms.openlocfilehash: 32591edd065a8122b84ff14102f672ccf6001d67
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855854"
---
# <a name="how-to-use-event-triggers-to-control-a-storyboard-after-it-starts"></a>방법: 스토리보드가 시작되면 이벤트 트리거를 사용하여 제어

이 예제에서는가 시작 된 후 <xref:System.Windows.Media.Animation.Storyboard> 을 제어 하는 방법을 보여 줍니다. 를 사용 <xref:System.Windows.Media.Animation.Storyboard> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]하 여를 시작 하려면 <xref:System.Windows.Media.Animation.BeginStoryboard>애니메이션을 적용 하는 개체 및 속성에 애니메이션을 배포한 다음 storyboard를 시작 하는를 사용 합니다. 속성을<xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> 지정 하 여 이름을 지정 하면 제어 가능한 storyboard로 설정 됩니다. <xref:System.Windows.Media.Animation.BeginStoryboard> 그런 다음 스토리 보드를 시작한 후 대화형으로 제어할 수 있습니다.

다음 스토리 보드 작업을 개체와 <xref:System.Windows.EventTrigger> 함께 사용 하 여 스토리 보드를 제어 합니다.

- <xref:System.Windows.Media.Animation.PauseStoryboard>: 스토리 보드를 일시 중지 합니다.

- <xref:System.Windows.Media.Animation.ResumeStoryboard>: 일시 중지 된 스토리 보드를 다시 시작 합니다.

- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: 스토리 보드 속도를 변경 합니다.

- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>: 스토리 보드가 있는 경우 해당 채우기 기간의 끝까지 storyboard를 이동 합니다.

- <xref:System.Windows.Media.Animation.StopStoryboard>: 스토리 보드를 중지 합니다.

- <xref:System.Windows.Media.Animation.RemoveStoryboard>: 스토리 보드를 제거 하 여 리소스를 해제 합니다.

## <a name="example"></a>예제

다음 예제에서는 제어 가능한 storyboard 작업을 사용 하 여 스토리 보드를 대화형으로 제어 합니다.

> [!NOTE]
> 코드를 사용 하 여 스토리 보드를 제어 하는 예제를 보려면 [대화형 메서드를 사용 하 여 시작 된 후 Storyboard 제어](how-to-control-a-storyboard-after-it-starts.md)를 참조 하세요.

[!code-xaml[timingbehaviors_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/ControlStoryboardExample.xaml#controlstoryboardexampleusingwholepage)]

추가 예제는 [애니메이션 예제 갤러리](https://go.microsoft.com/fwlink/?LinkID=159969)를 참조 하세요.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.ResumeStoryboard>
- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>
- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>
- <xref:System.Windows.Media.Animation.PauseStoryboard>
- <xref:System.Windows.Media.Animation.StopStoryboard>
- <xref:System.Windows.Media.Animation.SeekStoryboard>
- [대화형 메서드를 사용하여 이미 시작된 Storyboard 제어](how-to-control-a-storyboard-after-it-starts.md)
- [애니메이션 개요](animation-overview.md)
- [Storyboard 개요](storyboards-overview.md)
