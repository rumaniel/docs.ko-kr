---
title: 사용자 지정 애니메이션 개요
ms.date: 03/30/2017
helpviewer_keywords:
- custom classes [WPF], animation
- key frames [WPF], custom
- custom key frames [WPF]
- animation [WPF], custom classes
- custom animation classes [WPF]
ms.assetid: 9be69d50-3384-4938-886f-08ce00e4a7a6
ms.openlocfilehash: b97c926da28eeb5385de71362a6cbc064ccc20cd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615433"
---
# <a name="custom-animations-overview"></a>사용자 지정 애니메이션 개요
이 항목에서는 사용자 지정 키 프레임, 애니메이션 클래스를 만들거나, 프레임당 콜백을 사용하여 애니메이션 시스템을 무시하는 방식으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 시스템을 확장하는 방법 및 시기에 대해 설명합니다.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목을 이해하려면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 제공하는 다양한 형식의 애니메이션에 대해 잘 알고 있어야 합니다. 자세한 내용은 From/To/By 애니메이션 개요, [키 프레임 애니메이션 개요](key-frame-animations-overview.md) 및 [경로 애니메이션 개요](path-animations-overview.md)를 참조하세요.  
  
 애니메이션 클래스에서 상속 하기 때문에 합니다 <xref:System.Windows.Freezable> 클래스 사용자에 게 익숙한 <xref:System.Windows.Freezable> 에서 상속 하는 방법과 개체 <xref:System.Windows.Freezable>합니다. 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조하세요.  
  
<a name="extendingtheanimationsystem"></a>   
## <a name="extending-the-animation-system"></a>애니메이션 시스템 확장  
 사용하려는 기본 제공 기능 수준에 따라, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 시스템을 확장하는 다양한 방법이 있습니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 엔진에는 다음과 같은 세 가지 기본 확장 지점이 있습니다.  
  
- 중 하나에서 상속 하 여 사용자 지정 키 프레임 개체를 만드는 합니다  *\<유형 >* 등의 키 프레임 클래스 <xref:System.Windows.Media.Animation.DoubleKeyFrame>합니다. 이 방법은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 엔진의 기본 제공 기능 대부분을 사용합니다.  
  
- 상속 하 여 사용자 고유의 애니메이션 클래스를 만듭니다 <xref:System.Windows.Media.Animation.AnimationTimeline> 중 하나는  *\<유형 >* AnimationBase 클래스입니다.  
  
- 프레임당 콜백을 사용하여 프레임별로 애니메이션을 생성합니다. 이 방법은 애니메이션 및 타이밍 시스템을 완전히 무시합니다.  
  
 다음 표에서는 애니메이션 시스템을 확장하기 위한 몇 가지 시나리오에 대해 설명합니다.  
  
|원하는 작업...|사용하는 방법|  
|-------------------------|-----------------------|  
|해당 *\<Type>* AnimationUsingKeyFrames를 갖는 형식에 대한 값 사이의 보간 사용자 지정|사용자 지정 키 프레임을 만듭니다. 자세한 내용은 [사용자 지정 키 프레임 만들기](#createacustomkeyframe) 섹션을 참조하세요.|  
|해당 *\<Type>* Animation을 갖는 형식에 대한 값 사이의 보간 이상을 사용자 지정합니다.|애니메이션 효과를 적용할 형식에 해당하는 *\<Type>* AnimationBase 클래스에서 상속하는 사용자 지정 애니메이션 클래스를 만듭니다. 자세한 내용은 [사용자 지정 애니메이션 클래스 만들기](#createacustomanimationtype) 섹션을 참조하세요.|  
|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션이 없는 형식에 애니메이션 효과 적용|사용 된 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 에서 상속 되는 클래스를 만들거나 <xref:System.Windows.Media.Animation.AnimationTimeline>합니다. 자세한 내용은 [사용자 지정 애니메이션 클래스 만들기](#createacustomanimationtype) 섹션을 참조하세요.|  
|프레임별로 계산되고 개체 상호 작용의 마지막 집합을 기준으로 하는 값을 사용하여 여러 개체에 애니메이션 효과 적용|프레임당 콜백을 사용합니다. 자세한 내용은 [프레임당 콜백 사용 만들기](#useperframecallback) 섹션을 참조하세요.|  
  
<a name="createacustomkeyframe"></a>   
## <a name="create-a-custom-key-frame"></a>사용자 지정 키 프레임 만들기  
 사용자 지정 키 프레임 클래스를 만드는 것은 애니메이션 시스템을 확장하는 가장 간단한 방법입니다. 이 방법은 키 프레임 애니메이션에 대해 다른 보간 방법을 사용하려는 경우에 사용합니다.  [키 프레임 애니메이션 개요](key-frame-animations-overview.md)에 설명된 것처럼 키 프레임 애니메이션은 키 프레임 개체를 사용하여 해당 출력 값을 생성합니다. 각 키 프레임 개체는 다음 세 가지 기능을 수행합니다.  
  
- 사용 하 여 대상 값 지정 해당 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 속성입니다.  
  
- 해당 값에 도달 해야 사용 하 여 시간을 지정 해당 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> 속성입니다.  
  
- InterpolateValueCore 메서드를 구현하여 이전 키 프레임의 값과 고유한 값 간을 보간합니다.  
  
 **구현 지침**  
  
 *\<Type>* KeyFrame 추상 클래스에서 파생하고 InterpolateValueCore 메서드를 구현합니다. InterpolateValueCore 메서드는 키 프레임의 현재 값을 반환합니다. 두 개의 매개 변수, 즉 이전 키 프레임의 값과 0~1 사이의 진행률 값을 사용합니다. 키 프레임이 방금 시작 했음을 나타내고 값이 1는 키 프레임이 막 완료 되었으며이에 지정 된 값을 반환 해야 하는 0 진행률 나타냅니다 해당 <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> 속성입니다.  
  
 때문에  *\<형식 >* KeyFrame 클래스에서 상속 합니다 <xref:System.Windows.Freezable> 클래스를 재정의 해야 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 클래스의 새 인스턴스를 반환 하는 핵심입니다. 이 클래스가 데이터를 저장하는 데 종속성 속성을 사용하지 않거나 생성 후 추가 초기화를 요구할 경우 추가 메서드를 재정의해야 할 수 있습니다. 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조하세요.  
  
 사용자 지정 *\<Type>* KeyFrame 애니메이션을 만든 후에 해당 형식에 대한 *\<Type>* AnimationUsingKeyFrames와 함께 사용할 수 있습니다.  
  
<a name="createacustomanimationtype"></a>   
## <a name="create-a-custom-animation-class"></a>사용자 지정 애니메이션 클래스 만들기  
 애니메이션 형식을 직접 만들면 개체에 애니메이션 효과를 적용하는 방식을 보다 강력하게 제어할 수 있습니다. 두 가지 권장 되는 애니메이션 형식을 직접 만드는:에서 파생할 수 있습니다 합니다 <xref:System.Windows.Media.Animation.AnimationTimeline> 클래스 또는  *\<유형 >* AnimationBase 클래스입니다. *\<Type>* Animation 또는 *\<Type>* AnimationUsingKeyFrames 클래스에서 파생하는 것은 권장되지 않습니다.  
  
### <a name="derive-from-typeanimationbase"></a>\<Type>AnimationBase에서 파생  
 *\<Type>* AnimationBase 클래스에서 파생하는 것이 새 애니메이션 형식을 만드는 가장 간단한 방법입니다. 이 방법은 해당하는 *\<Type>* AnimationBase 클래스가 이미 있는 형식에 대해 새 애니메이션을 만들려는 경우에 사용합니다.  
  
 **구현 지침**  
  
 *\<Type>* Animation 클래스에서 파생하고 GetCurrentValueCore 메서드를 구현합니다. GetCurrentValueCore 메서드는 애니메이션의 현재 값을 반환합니다. 세 가지 매개 변수를 사용: 권장 되는 시작 값, 제안 된 끝 값, 및 <xref:System.Windows.Media.Animation.AnimationClock>, 애니메이션의 진행률을 확인 하는 데 사용할 수 있는 합니다.  
  
 때문에  *\<형식 >* AnimationBase 클래스에서 상속 합니다 <xref:System.Windows.Freezable> 클래스를 재정의 해야 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 클래스의 새 인스턴스를 반환 하는 핵심입니다. 이 클래스가 데이터를 저장하는 데 종속성 속성을 사용하지 않거나 생성 후 추가 초기화를 요구할 경우 추가 메서드를 재정의해야 할 수 있습니다. 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조하세요.  
  
 자세한 내용은 애니메이션 효과를 적용할 형식의 *\<Type>* AnimationBase 클래스에 대한 GetCurrentValueCore 메서드 설명서를 참조하세요. 예제를 보려면 [사용자 지정 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=159981)을 참조하세요.  
  
 **대체 방법**  
  
 애니메이션 값이 보간되는 방식을 변경하려면 *\<Type>* KeyFrame 클래스 중 하나에서 파생하는 것을 고려하세요. 만드는 키 프레임은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 제공하는 해당 *\<Type>* AnimationUsingKeyFrames와 함께 사용할 수 있습니다.  
  
### <a name="derive-from-animationtimeline"></a>AnimationTimeline에서 파생  
 파생 되는 <xref:System.Windows.Media.Animation.AnimationTimeline> 일치 하는 아직 하는 형식에 대 한 애니메이션을 만들려는 경우 클래스 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 또는 하면 강력한 형식화 되지 않은 하는 애니메이션을 만들려고 할 합니다.  
  
 **구현 지침**  
  
 파생 된 <xref:System.Windows.Media.Animation.AnimationTimeline> 클래스 및 멤버를 재정의 합니다.  
  
- <xref:System.Windows.Freezable.CreateInstanceCore%2A> –를 재정의 해야 새 클래스를 구체적인 경우 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 클래스의 새 인스턴스를 반환 합니다.  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> – 애니메이션의 현재 값을 반환 하려면이 메서드를 재정의 합니다. 세 가지 매개 변수를 사용 합니다: 기본 원본 값, 기본 대상 값 및 <xref:System.Windows.Media.Animation.AnimationClock>합니다. 사용 하 여는 <xref:System.Windows.Media.Animation.AnimationClock> 현재 시간 또는 애니메이션에 대 한 진행률을 가져오려고 합니다. 기본 원본 및 대상 값을 사용할 것인지 여부를 선택할 수 있습니다.  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A> --애니메이션으로 지정 된 기본 대상 값을 사용 하는지 여부를 나타내려면이 속성을 재정의 하는 중의 <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> 메서드.  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A> –이 속성을 재정의 합니다 <xref:System.Type> 애니메이션의 출력 생성 합니다.  
  
 이 클래스가 데이터를 저장하는 데 종속성 속성을 사용하지 않거나 생성 후 추가 초기화를 요구할 경우 추가 메서드를 재정의해야 할 수 있습니다. 자세한 내용은 [Freezable 개체 개요](../advanced/freezable-objects-overview.md)를 참조하세요.  
  
 권장되는 패러다임([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션에서 사용)은 다음 두 상속 수준을 사용하는 것입니다.  
  
1. 만들기는 추상  *\<유형 >* AnimationBase 클래스에서 파생 되는 <xref:System.Windows.Media.Animation.AnimationTimeline>합니다. 이 클래스를 재정의 해야 합니다 <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A> 메서드. 또한 새 추상 메서드인 GetCurrentValueCore를 도입 하 고 재정의 <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> GetCurrentValueCore 호출 기본 원본 값 및 기본 대상 값 매개 변수 형식, 유효한 지 확인 하도록 합니다.  
  
2. 상속 되는 다른 클래스 만들기에서 새  *\<형식 >* AnimationBase 클래스 재정의 및 합니다 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 메서드, 도입한 GetCurrentValueCore 메서드 및 <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A> 속성.  
  
 **대체 방법**  
  
 에 해당 From/To/By 애니메이션 또는 키 프레임 애니메이션 하는 형식에 애니메이션을 적용 하려는 경우는 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>합니다. 이므로 약하게 형식화는 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 모든 형식의 값에 애니메이션 효과 주기 수입니다. 이 방식의 단점은 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> 불연속 보간만 지원 합니다.  
  
<a name="useperframecallback"></a>   
## <a name="use-per-frame-callback"></a>프레임당 콜백 사용  
 이 접근 방법은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애니메이션 시스템을 완전히 무시해야 할 때 사용합니다. 이 방법에 대한 한 가지 시나리오는 각 애니메이션이 새 방향으로 단계별로 이동하거나 애니메이션 개체의 위치가 개체 상호 작용의 마지막 집합에 따라 다시 계산되어야 하는 물리학 애니메이션입니다.  
  
 **구현 지침**  
  
 이 개요에 설명된 다른 방법과 달리, 프레임당 콜백을 사용하기 위해 사용자 지정 애니메이션 또는 키 프레임 클래스를 만들 필요가 없습니다.  
  
 에 등록 하는 대신는 <xref:System.Windows.Media.CompositionTarget.Rendering> 애니메이션 효과 적용할 개체가 포함 된 개체의 이벤트입니다. 이 이벤트 처리기 메서드는 프레임마다 한 번씩 호출됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]가 시각적 트리의 지속되는 렌더링 데이터를 컴퍼지션 트리로 마샬링할 때마다 이벤트 처리기 메서드가 호출됩니다.  
  
 이벤트 처리기에서 애니메이션 효과에 필요한 계산을 수행하고 이러한 값을 사용하여 애니메이션 효과를 적용하려는 개체의 속성을 설정합니다.  
  
 현재 프레임의 프레젠테이션 시간을 얻기 위해 합니다 <xref:System.EventArgs> 와 연결 된 이벤트로 캐스팅 될 수 <xref:System.Windows.Media.RenderingEventArgs>를 제공 하는 <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> 현재 프레임을 가져오는 데 사용할 수 있는 속성의 렌더링 시간.  
  
 자세한 내용은 참조는 <xref:System.Windows.Media.CompositionTarget.Rendering> 페이지입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Animation.AnimationTimeline>
- <xref:System.Windows.Media.Animation.IKeyFrame>
- [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)
- [Freezable 개체 개요](../advanced/freezable-objects-overview.md)
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [경로 애니메이션 개요](path-animations-overview.md)
- [애니메이션 개요](animation-overview.md)
- [애니메이션 및 타이밍 시스템 개요](animation-and-timing-system-overview.md)
- [사용자 지정 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=159981)
