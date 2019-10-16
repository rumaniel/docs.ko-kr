---
title: 애니메이션 및 타이밍 시스템 개요
ms.date: 03/30/2017
helpviewer_keywords:
- timing system [WPF]
- animation [WPF]
ms.assetid: 172cd5a8-a333-4c81-9456-fafccc19f382
ms.openlocfilehash: f64431e7804ba6e068a3d05f512c6ead089d7712
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62020365"
---
# <a name="animation-and-timing-system-overview"></a>애니메이션 및 타이밍 시스템 개요
이 항목에서는 타이밍 시스템이 애니메이션을 사용 하는 방법에 대해 설명 합니다. <xref:System.Windows.Media.Animation.Timeline>, 및 <xref:System.Windows.Media.Animation.Clock> 클래스 속성에 애니메이션 효과를 합니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해하려면 [애니메이션 개요](animation-overview.md)에 설명된 대로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션을 사용하여 속성에 애니메이션 효과를 줄 수 있어야 합니다. 종속성 속성에 익숙한 것도 도움이 됩니다. 자세한 내용은 [종속성 속성 개요](../advanced/dependency-properties-overview.md)를 참조하세요.  
  
<a name="timelinesandclocks"></a>   
## <a name="timelines-and-clocks"></a>타임라인 및 시계  
 [애니메이션 개요](animation-overview.md) 하는 방법을 설명를 <xref:System.Windows.Media.Animation.Timeline> 나타냅니다 시간과 애니메이션의 세그먼트는 형식입니다 <xref:System.Windows.Media.Animation.Timeline> 출력 값을 생성 합니다. 자체적으로 <xref:System.Windows.Media.Animation.Timeline>, 이외의 아무 것도 수행 하지 시간의 세그먼트를 설명 하는 것입니다. 타임 라인의 <xref:System.Windows.Media.Animation.Clock> 실제 작업을 수행 하는 개체입니다. 마찬가지로 애니메이션 하지 실제로 속성 애니메이션 효과 주기: 애니메이션 클래스는 출력 값 계산 수 해야 하는 방법에 대해 설명 합니다. 이지만 <xref:System.Windows.Media.Animation.Clock> 애니메이션 속성에 적용 하는 애니메이션 출력 드라이브에 대해 생성 된 합니다.  
  
 A <xref:System.Windows.Media.Animation.Clock> 는 특수 유형의 개체에 대 한 타이밍 관련 런타임 상태를 유지 하는 <xref:System.Windows.Media.Animation.Timeline>합니다. 애니메이션 및 타이밍 시스템에 필수적인 3 개의 비트 정보를 제공 합니다. <xref:System.Windows.Media.Animation.Clock.CurrentTime%2A>, <xref:System.Windows.Media.Animation.Clock.CurrentProgress%2A>, 및 <xref:System.Windows.Media.Animation.Clock.CurrentState%2A>합니다. A <xref:System.Windows.Media.Animation.Clock> 에 설명 된 타이밍 동작을 사용 하 여 해당 현재 시간, 진행률 및 상태를 확인 해당 <xref:System.Windows.Media.Animation.Timeline>: <xref:System.Windows.Media.Animation.Timeline.Duration%2A>를 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>등입니다.  
  
 대부분의 경우에는 <xref:System.Windows.Media.Animation.Clock> 타임 라인에 대 한 자동으로 만들어집니다. 사용 하 여 애니메이션 효과 주는 경우는 <xref:System.Windows.Media.Animation.Storyboard> 또는 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 메서드 시계가 자동으로 타임 라인 및 애니메이션에 대 한 생성 되어 해당 대상된 속성에 적용 합니다. 만들 수도 있습니다는 <xref:System.Windows.Media.Animation.Clock> 를 사용 하 여 명시적으로 <xref:System.Windows.Media.Animation.Timeline.CreateClock%2A> 메서드의 프로그램 <xref:System.Windows.Media.Animation.Timeline>합니다. 합니다 <xref:System.Windows.Media.MediaTimeline.CreateClock%2A?displayProperty=nameWithType> 방법에 대 한 적절 한 유형의 시계를 만듭니다는 <xref:System.Windows.Media.Animation.Timeline> 에서 호출 됩니다. 경우는 <xref:System.Windows.Media.Animation.Timeline> 자식 타임 라인이 포함 만들면 <xref:System.Windows.Media.Animation.Clock> 에 개체도 합니다. 결과 <xref:System.Windows.Media.Animation.Clock> 개체의 구조와 일치 하는 트리로 정렬 되는 <xref:System.Windows.Media.Animation.Timeline> 에서 생성 된 개체 트리.  
  
 다양한 유형의 타임라인에 대한 여러 유형의 시계가 있습니다. 다음 표는 <xref:System.Windows.Media.Animation.Clock> 몇 가지 다른에 해당 하는 형식 <xref:System.Windows.Media.Animation.Timeline> 형식입니다.  
  
|타임라인 형식|시계 유형|시계 용도|  
|-------------------|----------------|-------------------|  
|애니메이션 (에서 상속 <xref:System.Windows.Media.Animation.AnimationTimeline>)|<xref:System.Windows.Media.Animation.AnimationClock>|종속성 속성에 대한 출력 값을 생성합니다.|  
|<xref:System.Windows.Media.MediaTimeline>|<xref:System.Windows.Media.MediaClock>|미디어 파일을 처리합니다.|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|<xref:System.Windows.Media.Animation.ClockGroup>|그룹 및 해당 자식 컨트롤 <xref:System.Windows.Media.Animation.Clock> 개체|  
|<xref:System.Windows.Media.Animation.Storyboard>|<xref:System.Windows.Media.Animation.ClockGroup>|그룹 및 해당 자식 컨트롤 <xref:System.Windows.Media.Animation.Clock> 개체|  
  
 적용할 수 있습니다 <xref:System.Windows.Media.Animation.AnimationClock> 호환 되는 종속성 속성을 사용 하 여 만든 개체는 <xref:System.Windows.Media.Animation.IAnimatable.ApplyAnimationClock%2A> 메서드.  
  
 많은 수의 유사한 개체에 애니메이션을 적용 하는 등 성능 집약적인 시나리오에서는 관리 사용자 고유의 <xref:System.Windows.Media.Animation.Clock> 사용 하 여 성능 이점을 제공할 수 있습니다.  
  
<a name="timemanager"></a>   
## <a name="clocks-and-the-time-manager"></a>시계 및 시간 관리자  
 개체에 애니메이션 효과 주기 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 관리 하는 시간 관리자가를 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 타임 라인을 위해 생성 된 개체입니다. 시간 관리자는 <xref:System.Windows.Media.MediaPlayer.Clock%2A> 개체 트리의 루트이며 해당 트리에서 시간의 흐름을 제어합니다.  시간 관리자는 각 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션에 대해 자동으로 만들어지며 애플리케이션 개발자에게 표시되지 않습니다. 시간 관리자에서 매초 여러 번 "틱"이 발생하는데 초당 발생하는 실제 틱 수는 사용 가능한 시스템 리소스에 따라 다릅니다. 각각이 틱 동안 시간 관리자는 모든의 상태를 계산 <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> 는 타이밍 트리의 개체입니다.  
  
 다음 그림에서는 시간 관리자 간의 관계를 보여 줍니다. 및 <xref:System.Windows.Media.Animation.AnimationClock>, 및 애니메이션된 종속성 속성입니다.  
  
 ![타이밍 시스템 구성 요소](./media/graphicsmm-clocks-1clock1prop.png "graphicsmm_clocks_1clock1prop")  
속성에 애니메이션 효과 주기  
  
 시간 관리자에서 틱의 시간 업데이트 마다 <xref:System.Windows.Media.Animation.ClockState.Active> <xref:System.Windows.Media.Animation.Clock> 응용 프로그램에서입니다. 경우는 <xref:System.Windows.Media.Animation.Clock> 는 <xref:System.Windows.Media.Animation.AnimationClock>를 사용 하 여는 <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> 메서드의 <xref:System.Windows.Media.Animation.AnimationTimeline> 에서 생성 된 현재 계산 출력 값입니다. 합니다 <xref:System.Windows.Media.Animation.AnimationClock> 제공 된 <xref:System.Windows.Media.Animation.AnimationTimeline> 현재 현지 시간, 일반적으로 속성의 기준 값 이므로 입력된 값 및 기본 대상 값을 사용 하 여 합니다. 애니메이션의 값을 검색 하는 경우 속성을 사용 하 여 합니다 <xref:System.Windows.DependencyObject.GetValue%2A> 의 출력을 가져오려면 메서드 또는 해당 CLR 접근자에 해당 <xref:System.Windows.Media.Animation.AnimationClock>합니다.  
  
#### <a name="clock-groups"></a>시계 그룹  
 이전 섹션의 다른 형식은 어떻게 설명 <xref:System.Windows.Media.Animation.Clock> 다양 한 유형의 타임 라인에 대 한 개체입니다. 다음 그림에서는 시간 관리자 간의 관계를 보여 줍니다.는 <xref:System.Windows.Media.Animation.ClockGroup>, <xref:System.Windows.Media.Animation.AnimationClock>, 및 애니메이션된 종속성 속성입니다. A <xref:System.Windows.Media.Animation.ClockGroup> 와 같은 다른 타임 라인을 그룹화 하는 타임 라인에 대해 생성 됩니다는 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션 및 다른 타임 라인을 그룹화 하는 클래스입니다.  
  
 ![타이밍 시스템 구성 요소](./media/graphicsmm-clocks-2clock1clockgroup2prop.png "graphicsmm_clocks_2clock1clockgroup2prop")  
ClockGroup  
  
#### <a name="composition"></a>컴퍼지션  
 여러 시계를 단일 속성에 연결할 수 있습니다. 이 경우 각 시계에서 이전 시계의 출력 값을 기준 값으로 사용합니다. 다음 그림에서는 3 개의 <xref:System.Windows.Media.Animation.AnimationClock> 동일한 속성에 적용 하는 개체입니다. Clock1은 애니메이션 속성의 기준 값을 해당 입력으로 사용하고 이를 사용하여 출력을 생성합니다. Clock2는 Clock1의 출력을 입력으로 받고 이를 사용하여 출력을 생성합니다. Clock3은 Clock2의 출력을 입력으로 받고 이를 사용하여 출력을 생성합니다. 여러 시계가 같은 속성에 동시에 영향을 주는 경우 컴퍼지션 체인에 있다고 합니다.  
  
 ![타이밍 시스템 구성 요소](./media/graphicsmm-clocks-2clock1prop.png "graphicsmm_clocks_2clock1prop")  
컴퍼지션 체인  
  
 입력과 출력 간의 관계가 만들어져 있지만 <xref:System.Windows.Media.Animation.AnimationClock> 개체 컴퍼지션 체인에 해당 타이밍 동작은 영향을 받지 않습니다. <xref:System.Windows.Media.Animation.Clock> 개체 (포함 <xref:System.Windows.Media.Animation.AnimationClock> 개체)는 부모에 대 한 계층적 종속성 <xref:System.Windows.Media.Animation.Clock> 개체입니다.  
  
 여러 시계가 같은 속성에 적용 하려면 사용 합니다 <xref:System.Windows.Media.Animation.HandoffBehavior.Compose> <xref:System.Windows.Media.Animation.HandoffBehavior> 적용 하는 경우를 <xref:System.Windows.Media.Animation.Storyboard>, 애니메이션 또는 <xref:System.Windows.Media.Animation.AnimationClock>합니다.  
  
#### <a name="ticks-and-event-consolidation"></a>틱 및 이벤트 통합  
 출력 값을 계산하는 것 외에도 시간 관리자는 틱을 발생시킬 때마다 다른 작업을 수행합니다. 각 시계의 상태를 결정하고 적절하게 이벤트를 발생시킵니다.  
  
 틱은 자주 발생하지만 틱 간에 많은 사항이 발생할 수 있습니다. 예를 들어, 한 <xref:System.Windows.Media.Animation.Clock> 중지, 시작 및 경우에 다시 중지 될 수 있습니다 해당 <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> 값 3 번 변경 됩니다. 이론적으로 <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> 타이밍 엔진이 이벤트를 통합 하는 반면; 이벤트가 단일 틱에서 여러 번 발생할 수 없습니다 있도록는 <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> 이벤트가 틱 당 한 번만 발생할 수 있습니다. 이 모든 타이밍 이벤트에 적용: 각 유형의 최대 하나의 이벤트에 대 한 발생을 지정 <xref:System.Windows.Media.Animation.Clock> 개체입니다.  
  
 경우는 <xref:System.Windows.Media.Animation.Clock> 상태를 전환 하 고 틱 간의 원래 상태로 반환 (에서 변경 하는 등 <xref:System.Windows.Media.Animation.ClockState.Active> 에 <xref:System.Windows.Media.Animation.ClockState.Stopped> 하 고 다시 <xref:System.Windows.Media.Animation.ClockState.Active>), 연결된 된 이벤트가 계속 발생 합니다.  
  
 타이밍 이벤트에 대한 자세한 내용은 [타이밍 이벤트 개요](timing-events-overview.md)를 참조하세요.  
  
<a name="currentvaluesbasevaluesofproperties"></a>   
## <a name="current-values-and-base-values-of-properties"></a>속성의 현재 값 및 기준 값  
 애니메이션 효과를 줄 수 있는 속성은 두 값(기준 값 및 현재 값)을 가질 수 있습니다. 해당 CLR 접근자를 사용 하 여 속성을 설정한 경우 또는 <xref:System.Windows.DependencyObject.SetValue%2A> 메서드, 설정한 기준 값입니다. 속성에 애니메이션 효과를 줄 수 없는 경우 해당 기준 값과 현재 값은 동일합니다.  
  
 속성에 애니메이션 효과 주는 경우 합니다 <xref:System.Windows.Media.Animation.AnimationClock> 속성의 설정 *현재* 값입니다. 해당 CLR 접근자를 통해 속성의 값을 검색 또는 <xref:System.Windows.DependencyObject.GetValue%2A> 의 출력을 반환 하는 메서드를 <xref:System.Windows.Media.Animation.AnimationClock> 때 합니다 <xref:System.Windows.Media.Animation.AnimationClock> 은 <xref:System.Windows.Media.Animation.ClockState.Active> 또는 <xref:System.Windows.Media.Animation.ClockState.Filling>합니다. 사용 하 여 속성의 기준 값을 검색할 수 있습니다는 <xref:System.Windows.Media.Animation.IAnimatable.GetAnimationBaseValue%2A> 메서드.  
  
## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [타이밍 이벤트 개요](timing-events-overview.md)
- [타이밍 동작 개요](timing-behaviors-overview.md)
