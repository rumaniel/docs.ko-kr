---
title: Freezable 개체 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Freezable objects [WPF], description
- unfreezing Freezable objects [WPF]
- classes [WPF], Freezable
ms.assetid: 89c71692-4f43-4057-b611-67c6a8a863a2
ms.openlocfilehash: 05cd3c27430146f575c23011f53995aa07aaf99e
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991491"
---
# <a name="freezable-objects-overview"></a>Freezable 개체 개요

이 항목에서는 응용 프로그램 성능을 향상 시킬 수 <xref:System.Windows.Freezable> 있는 특수 기능을 제공 하는 개체를 효과적으로 사용 하 고 만드는 방법을 설명 합니다. Freezable 개체의 예로는 브러시, 펜, 변환, 기 하 도형 및 애니메이션이 있습니다.

<a name="whatisafreezable"></a>

## <a name="what-is-a-freezable"></a>Freezable 이란?

는 <xref:System.Windows.Freezable> 고정 해제 및 고정의 두 가지 상태를 가진 특수 한 형식의 개체입니다. 고정 되지 않은 경우 <xref:System.Windows.Freezable> 는 다른 개체 처럼 동작 하는 것 처럼 보입니다. 고정 된 경우는 <xref:System.Windows.Freezable> 더 이상 수정할 수 없습니다.

는 <xref:System.Windows.Freezable> 관찰자에 <xref:System.Windows.Freezable.Changed> 게 개체에 대 한 수정 사항을 알리기 위한 이벤트를 제공 합니다. 을 <xref:System.Windows.Freezable> 고정 하면 변경 알림에 리소스를 더 이상 사용할 필요가 없기 때문에 성능이 향상 될 수 있습니다. 고정 <xref:System.Windows.Freezable> 된는 스레드 간에 공유 될 수도 있고 고정 <xref:System.Windows.Freezable> 되지 않은은 사용할 수 없습니다.

클래스에는 많은 응용 프로그램이 있지만의 <xref:System.Windows.Freezable> 대부분의 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 개체는 그래픽 하위 시스템과 관련 되어 있습니다. <xref:System.Windows.Freezable>

<xref:System.Windows.Freezable> 클래스를 사용 하면 특정 그래픽 시스템 개체를 쉽게 사용할 수 있으며 응용 프로그램 성능을 향상 시킬 수 있습니다. 에서 <xref:System.Windows.Freezable> 상속 되는 형식의 예에는 <xref:System.Windows.Media.Brush>, <xref:System.Windows.Media.Transform>및 <xref:System.Windows.Media.Geometry> 클래스가 포함 됩니다. 관리 되지 않는 리소스가 포함 되어 있기 때문에 시스템은 이러한 개체를 수정 하기 위해 모니터링 한 다음 원래 개체가 변경 될 때 해당 관리 되지 않는 리소스를 업데이트 해야 합니다. 실제로 그래픽 시스템 개체를 수정 하지 않는 경우에도 시스템은 개체를 변경 하는 경우에도 개체를 모니터링 하는 리소스의 일부를 소비 해야 합니다.

예를 들어 <xref:System.Windows.Media.SolidColorBrush> 브러시를 만들어 단추의 배경을 그리는 데 사용 한다고 가정 합니다.

[!code-csharp[freezablesample_procedural#FrozenExamplePart1](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart1)]
[!code-vb[freezablesample_procedural#FrozenExamplePart1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart1)]

단추가 렌더링 되 면 그래픽 하위 시스템 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 은 사용자가 제공한 정보를 사용 하 여 픽셀 그룹을 페인트 하 여 단추의 모양을 만듭니다. 단색 브러시를 사용 하 여 단추를 그려야 하는 방식을 설명 했지만 단색 브러시는 실제로 그리기를 수행 하지 않습니다. 그래픽 시스템은 단추와 브러시에 대해 빠르고 낮은 수준의 개체를 생성 하 고 실제로 화면에 표시 되는 개체입니다.

브러시를 수정 하려면 해당 하위 수준 개체를 다시 생성 해야 합니다. Freezable 클래스는 해당 하는 생성 된 하위 수준 개체를 찾고 변경 될 때이를 업데이트 하는 기능을 브러시에 제공 합니다. 이 기능을 사용 하도록 설정 하면 브러시가 "고정 되지 않음"으로 간주 됩니다.

Freezable의 <xref:System.Windows.Freezable.Freeze%2A> 메서드를 사용 하면이 자동 업데이트 기능을 사용 하지 않도록 설정할 수 있습니다. 이 메서드를 사용 하 여 브러시가 "고정" 또는 수정할 수 없게 만들 수 있습니다.

> [!NOTE]
> 모든 Freezable 개체를 고정할 수 있는 것은 아닙니다. 이 발생 <xref:System.InvalidOperationException>하지 않도록 하려면 Freezable <xref:System.Windows.Freezable.CanFreeze%2A> 개체의 속성 값을 확인 하 여 고정을 시도 하기 전에 고정할 수 있는지 여부를 확인 합니다.

[!code-csharp[freezablesample_procedural#FrozenExamplePart2](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart2)]
[!code-vb[freezablesample_procedural#FrozenExamplePart2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart2)]

더 이상 freezable을 수정할 필요가 없는 경우 고정 하면 성능상의 이점을 얻을 수 있습니다. 이 예에서 브러시를 고정 하는 경우 그래픽 시스템에서 더 이상 변경 내용을 모니터링할 필요가 없습니다. 또한 그래픽 시스템은 브러시가 변경 되지 않는다는 것을 알고 있으므로 다른 최적화를 수행할 수 있습니다.

> [!NOTE]
> 편의상 freezable 개체는 명시적으로 고정 하지 않는 한 고정 되지 않은 상태로 유지 됩니다.

<a name="frozenfreezables"></a>

## <a name="using-freezables"></a>Freezable 사용

고정 되지 않은 freezable을 사용 하는 것은 다른 유형의 개체를 사용 하는 것과 같습니다. 다음 예제에서는 단추의 배경을 칠하는 데 사용한 색 <xref:System.Windows.Media.SolidColorBrush> 이 노랑에서 빨강으로 변경 됩니다. 그래픽 시스템은 백그라운드에서 작동 하 여 다음에 화면을 새로 고칠 때 단추를 노랑에서 빨강으로 자동으로 변경 합니다.

[!code-csharp[freezablesample_procedural#UnFrozenExampleShort](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#unfrozenexampleshort)]
[!code-vb[freezablesample_procedural#UnFrozenExampleShort](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#unfrozenexampleshort)]

### <a name="freezing-a-freezable"></a>Freezable 고정

수정할 수 없게 하려면 해당 <xref:System.Windows.Freezable.Freeze%2A> 메서드를 호출 합니다. <xref:System.Windows.Freezable> Freezable 개체가 포함 된 개체를 고정 하는 경우 해당 개체도 고정 됩니다. 예를 들어을 고정 하는 <xref:System.Windows.Media.PathGeometry>경우 포함 된 그림 및 선분은 고정 되어 있습니다.

다음 조건 중 하나에 해당 하는 경우 Freezable을 고정할 수 **없습니다** .

- 애니메이션 또는 데이터 바인딩된 속성이 있습니다.

- 동적 리소스에 의해 설정 된 속성이 있습니다. 동적 리소스에 대 한 자세한 내용은 [XAML 리소스](xaml-resources.md) 를 참조 하세요.

- 고정할 수 <xref:System.Windows.Freezable> 없는 하위 개체가 포함 되어 있습니다.

이러한 조건이 false 인 경우를 수정 하지 않으려는 경우에는 <xref:System.Windows.Freezable>이전에 설명한 성능 이점을 얻기 위해 고정 해야 합니다.

Freezable의 <xref:System.Windows.Freezable.Freeze%2A> 메서드를 호출 하면 더 이상 수정할 수 없습니다. 고정 된 개체를 수정 하려고 하면 <xref:System.InvalidOperationException> 이 throw 됩니다. 다음 코드는 고정 된 후에 브러시를 수정 하려고 하기 때문에 예외를 throw 합니다.

[!code-csharp[freezablesample_procedural#ExceptionExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#exceptionexample)]
[!code-vb[freezablesample_procedural#ExceptionExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#exceptionexample)]

이 예외가 발생 하지 않도록 하려면 <xref:System.Windows.Freezable.IsFrozen%2A> 메서드를 사용 하 여이 고정 <xref:System.Windows.Freezable> 되어 있는지 여부를 확인할 수 있습니다.

[!code-csharp[freezablesample_procedural#CheckIsFrozenExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
[!code-vb[freezablesample_procedural#CheckIsFrozenExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]

위의 코드 예제에서 메서드를 <xref:System.Windows.Freezable.Clone%2A> 사용 하 여 고정 된 개체의 수정 가능한 복사본을 만들었습니다. 다음 섹션에서는 복제에 대해 자세히 설명 합니다.

> [!NOTE]
> 고정 freezable에 애니메이션을 적용할 수 없으므로를 <xref:System.Windows.Freezable> <xref:System.Windows.Media.Animation.Storyboard>사용 하 여 애니메이션에 애니메이션을 적용 하려고 할 때 애니메이션 시스템이 고정 개체의 수정 가능한 복제본을 자동으로 만듭니다. 복제로 인 한 성능 오버 헤드를 없애려면 개체에 애니메이션 효과를 적용 하려는 경우 개체를 고정 되지 않은 상태로 둡니다. Storyboard에 애니메이션을 적용 하는 방법에 대 한 자세한 내용은 [Storyboard 개요](../graphics-multimedia/storyboards-overview.md)를 참조 하세요.

### <a name="freezing-from-markup"></a>태그에서 고정

태그로 선언 된 <xref:System.Windows.Freezable> 개체를 고정 하려면 `PresentationOptions:Freeze` 특성을 사용 합니다. 다음 예제 <xref:System.Windows.Media.SolidColorBrush> 에서는가 페이지 리소스로 선언 되 고 고정 되어 있습니다. 그런 다음 단추의 배경을 설정 하는 데 사용 됩니다.

[!code-xaml[FreezableSample#FreezeFromMarkupWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FreezableSample/CS/FreezeFromMarkupExample.xaml#freezefrommarkupwholepage)]

`Freeze` 특성을 사용 하려면 프레젠테이션 옵션 네임 스페이스 ( `http://schemas.microsoft.com/winfx/2006/xaml/presentation/options`)에 매핑해야 합니다. `PresentationOptions`이 네임 스페이스를 매핑하기 위한 권장 접두사는 다음과 같습니다.

```xaml
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"
```

모든 XAML 판독기는이 특성을 인식 하지 않으므로 [mc: ignorable 특성](mc-ignorable-attribute.md) 을 사용 하 여 `Presentation:Freeze` 특성을 무시할 수 있는 것으로 표시 하는 것이 좋습니다.

```xaml
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="PresentationOptions"
```

자세한 내용은 [mc: Ignorable 특성](mc-ignorable-attribute.md) 페이지를 참조 하세요.

### <a name="unfreezing-a-freezable"></a>Freezable을 "고정 해제" 합니다.

고정 한 후에 <xref:System.Windows.Freezable> 는를 수정 하거나 고정 취소할 수 없지만 <xref:System.Windows.Freezable.Clone%2A> 또는 <xref:System.Windows.Freezable.CloneCurrentValue%2A> 메서드를 사용 하 여 고정 되지 않은 클론을 만들 수 있습니다.

다음 예제에서 단추의 배경은 브러시로 설정 되 고 브러시는 고정 됩니다. 메서드를 <xref:System.Windows.Freezable.Clone%2A> 사용 하 여 브러시의 고정 되지 않은 복사본을 생성 합니다. 복제본이 수정 되 고 단추의 배경을 노란색에서 빨강으로 변경 하는 데 사용 됩니다.

[!code-csharp[freezablesample_procedural#CloneExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
[!code-vb[freezablesample_procedural#CloneExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]

> [!NOTE]
> 사용 하는 복제 방법에 관계 없이 애니메이션은 새 <xref:System.Windows.Freezable>에 복사 되지 않습니다.

<xref:System.Windows.Freezable.Clone%2A> 및<xref:System.Windows.Freezable.CloneCurrentValue%2A> 메서드는 freezable의 전체 복사본을 생성 합니다. Freezable에 고정 된 다른 freezable 개체가 포함 되어 있으면 해당 개체도 복제 되 고 수정할 수 있게 됩니다. 예를 들어 고정 <xref:System.Windows.Media.PathGeometry> 을 복제 하 여 수정할 수 있도록 하는 경우 포함 된 도형과 세그먼트만 복사 되 고 수정할 수 있게 됩니다.

<a name="createyourownfreezableclass"></a>

## <a name="creating-your-own-freezable-class"></a>사용자 고유의 Freezable 클래스 만들기

에서 <xref:System.Windows.Freezable> 파생 되는 클래스는 다음과 같은 기능을 제공 합니다.

- 특수 상태: 읽기 전용 (고정) 및 쓰기 가능 상태입니다.

- 스레드 보안: 고정 <xref:System.Windows.Freezable> 된는 스레드 간에 공유 될 수 있습니다.

- 자세한 변경 알림: 다른 <xref:System.Windows.DependencyObject>와 달리 Freezable 개체는 하위 속성 값이 변경 될 때 변경 알림을 제공 합니다.

- 쉬운 복제: Freezable 클래스가 이미 전체 복제를 만드는 여러 메서드를 구현 합니다.

는 <xref:System.Windows.Freezable> 의<xref:System.Windows.DependencyObject>형식 이므로 종속성 속성 시스템을 사용 합니다. 클래스 속성은 종속성 속성이 될 필요는 없지만 종속성 속성을 사용 하면 <xref:System.Windows.Freezable> 클래스가 종속성 속성을 염두에 두어야 하므로 작성 해야 하는 코드의 양이 줄어듭니다. 종속성 속성 시스템에 대 한 자세한 내용은 [종속성 속성 개요](dependency-properties-overview.md)를 참조 하세요.

모든 <xref:System.Windows.Freezable> 서브 클래스는 메서드 <xref:System.Windows.Freezable.CreateInstanceCore%2A> 를 재정의 해야 합니다. 클래스에서 모든 데이터에 대 한 종속성 속성을 사용 하면 작업이 완료 된 것입니다.

클래스에 종속성이 아닌 속성 데이터 멤버가 포함 된 경우에는 다음 메서드도 재정의 해야 합니다.

- <xref:System.Windows.Freezable.CloneCore%2A>

- <xref:System.Windows.Freezable.CloneCurrentValueCore%2A>

- <xref:System.Windows.Freezable.GetAsFrozenCore%2A>

- <xref:System.Windows.Freezable.GetCurrentValueAsFrozenCore%2A>

- <xref:System.Windows.Freezable.FreezeCore%2A>

또한 종속성 속성이 아닌 데이터 멤버에 액세스 하 고 쓰려면 다음 규칙을 따라야 합니다.

- 비 종속성 속성 데이터 멤버를 읽는 API의 시작 부분에서 <xref:System.Windows.Freezable.ReadPreamble%2A> 메서드를 호출 합니다.

- 종속성이 아닌 속성 데이터 멤버를 작성 하는 API의 시작 부분에서 <xref:System.Windows.Freezable.WritePreamble%2A> 메서드를 호출 합니다. API에서를 호출한 <xref:System.Windows.Freezable.WritePreamble%2A> 후에는 종속성이 아닌 속성 데이터 멤버도 읽을 경우에 대 <xref:System.Windows.Freezable.ReadPreamble%2A> 한 추가 호출을 수행할 필요가 없습니다.

- 비 종속성 <xref:System.Windows.Freezable.WritePostscript%2A> 속성 데이터 멤버에 쓰는 메서드를 종료 하기 전에 메서드를 호출 합니다.

클래스에 <xref:System.Windows.DependencyObject> 개체 인 비 종속성 속성 데이터 멤버가 포함 된 경우 멤버를로 `null`설정 하더라도 해당 값 중 <xref:System.Windows.Freezable.OnFreezablePropertyChanged%2A> 하나를 변경할 때마다 메서드를 호출 해야 합니다.

> [!NOTE]
> 기본 구현에 대 한 호출을 사용 <xref:System.Windows.Freezable> 하 여 재정의 하는 각 메서드를 시작 하는 것이 매우 중요 합니다.

사용자 지정 <xref:System.Windows.Freezable> 클래스의 예제는 [사용자 지정 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=159981)을 참조 하세요.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Freezable>
- [사용자 지정 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=159981)
- [종속성 속성 개요](dependency-properties-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
