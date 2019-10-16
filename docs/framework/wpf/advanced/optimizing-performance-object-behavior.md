---
title: '성능 최적화: 개체 동작'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- user interface virtualization [WPF]
- dependency properties [WPF], performance
- event handlers [WPF]
- object performance considerations [WPF]
- Freezable objects [WPF], performance
ms.assetid: 73aa2f47-1d73-439a-be1f-78dc4ba2b5bd
ms.openlocfilehash: 025c8691eb1aaf9483a222530a5590670ede486b
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68400473"
---
# <a name="optimizing-performance-object-behavior"></a>성능 최적화: 개체 동작
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 개체의 기본 동작을 이해하면 기능과 성능 간의 균형을 적절하게 조정할 수 있습니다.  

<a name="Not_Removing_Event_Handlers"></a>   
## <a name="not-removing-event-handlers-on-objects-may-keep-objects-alive"></a>개체에 대한 이벤트 처리기를 제거하지 않으면 개체가 활성 상태로 유지될 수 있음  
 개체가 해당 이벤트에 전달하는 대리자는 사실상 해당 개체에 대한 참조입니다. 따라서 이벤트 처리기는 예상보다 오래 개체의 활성 상태를 유지할 수 있습니다. 개체의 이벤트를 수신하도록 등록된 개체를 정리하려면 개체를 해제하기 전에 먼저 대리자를 제거해야 합니다. 불필요한 개체를 활성 상태로 유지하면 애플리케이션의 메모리 사용이 늘어납니다. 이러한 현상은 특히 개체가 논리적 트리 또는 시각적 트리의 루트인 경우 특히 그렇습니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에는 소스와 수신기 간의 개체 수명 관계를 추적하기 어려운 경우에 유용할 수 있는 이벤트에 대한 약한 이벤트 수신기 패턴이 도입되었습니다. 일부 기존 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이벤트에서 이 패턴을 사용하기도 합니다. 사용자 지정 이벤트를 사용하여 개체를 구현하는 경우 이 패턴이 유용할 수 있습니다. 자세한 내용은 [약한 이벤트 패턴](weak-event-patterns.md)을 참조하세요.  
  
 지정된 프로세스의 메모리 사용에 대한 정보를 제공할 수 있는 CLR 프로파일러 및 작업 집합 뷰어 등 여러 가지 도구가 있습니다. CLR 프로파일러에는 할당된 형식에 대한 히스토그램, 할당 및 호출 그래프, 다양한 세대의 가비지 수집을 보여 주는 시간 표시 막대, 이러한 수집 이후의 관리되는 힙에 대한 결과 상태, 메서드당 할당 및 어셈블리 로드를 보여 주는 호출 트리 등 할당 프로필에 대한 매우 유용한 여러 뷰가 포함되어 있습니다. 자세한 내용은 [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=117435)를 참조하세요.  
  
<a name="DPs_and_Objects"></a>   
## <a name="dependency-properties-and-objects"></a>종속성 속성 및 개체  
 일반적으로의 <xref:System.Windows.DependencyObject> 종속성 속성에 액세스 하는 것은 CLR 속성에 액세스 하는 것 보다 속도가 느립니다. 속성 값을 설정 하는 데는 약간의 성능 오버 헤드가 있지만 값 가져오기는 CLR 속성에서 값을 가져오는 것 만큼 빠릅니다. 이러한 약간의 성능 오버헤드가 발생하지만 종속성 속성이 데이터 바인딩, 애니메이션, 상속 및 스타일 지정과 같은 강력한 기능을 지원합니다. 자세한 내용은 [종속성 속성 개요](dependency-properties-overview.md)를 참조하세요.  
  
### <a name="dependencyproperty-optimizations"></a>DependencyProperty 최적화  
 애플리케이션에서 종속성 속성을 정의할 때는 매우 신중해야 합니다. 가 와<xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>같은 다른 메타 데이터 옵션 대신 렌더링 형식 메타 데이터 옵션에만 영향을주는경우해당메타데이터를재정의하여표시해야합니다.<xref:System.Windows.DependencyProperty> 속성 메타데이터 재정의 또는 가져오기에 대한 자세한 내용은 [종속성 속성 메타데이터](dependency-property-metadata.md)를 참조하세요.  
  
 모든 속성 변경이 실제로 측정, 정렬 및 렌더링에 영향을 미치는 것이 아니라면 속성 변경 처리기가 측정, 정렬 및 렌더링 단계를 수동으로 무효화하도록 하는 것이 더 효율적일 수 있습니다. 예를 들어 값이 설정된 한계보다 클 경우에만 배경을 다시 렌더링하도록 결정한 경우 속성 변경 처리기는 값이 설정된 한계를 초과하는 경우에만 렌더링을 무효화합니다.  
  
### <a name="making-a-dependencyproperty-inheritable-is-not-free"></a>DependencyProperty를 상속 가능하게 만드는 경우 성능에 미치는 영향  
 기본적으로 등록된 종속성 속성은 상속되지 않습니다. 그러나 어떤 속성이든 명시적으로 상속 가능하게 만들 수 있습니다. 이는 유용한 기능이지만 속성을 상속 가능한 속성으로 변환하면 속성 무효화를 위한 시간이 길어져서 성능에 영향을 미칩니다.  
  
### <a name="use-registerclasshandler-carefully"></a>RegisterClassHandler의 신중한 사용  
 를 호출 <xref:System.Windows.EventManager.RegisterClassHandler%2A> 하 여 인스턴스 상태를 저장할 수 있지만, 모든 인스턴스에서 처리기가 호출 되어 성능 문제가 발생할 수 있다는 것을 알고 있어야 합니다. 응용 프로그램 <xref:System.Windows.EventManager.RegisterClassHandler%2A> 에서 인스턴스 상태를 저장 해야 하는 경우에만를 사용 합니다.  
  
### <a name="set-the-default-value-for-a-dependencyproperty-during-registration"></a>등록 시 DependencyProperty에 대한 기본값 설정  
 기본값이 필요한를 <xref:System.Windows.DependencyProperty> 만들 때의 <xref:System.Windows.DependencyProperty.Register%2A> <xref:System.Windows.DependencyProperty>메서드에 매개 변수로 전달 되는 기본 메타 데이터를 사용 하 여 값을 설정 합니다. 생성자 또는 요소의 각 인스턴스에 속성 값을 설정하는 기술보다 이 기술을 사용합니다.  
  
### <a name="set-the-propertymetadata-value-using-register"></a>레지스터를 사용하여 PropertyMetadata 값 설정  
 를 만들 <xref:System.Windows.DependencyProperty>때 <xref:System.Windows.DependencyProperty.Register%2A> 또는 <xref:System.Windows.PropertyMetadata> 메서드<xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 중 하나를 사용 하 여를 설정할 수 있습니다. 개체에는를 호출 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>하는 정적 생성자가 있을 수 있지만이는 최적의 솔루션이 아니므로 성능에 영향을 줍니다. 최상의 성능을 위해를 호출 하 <xref:System.Windows.PropertyMetadata> <xref:System.Windows.DependencyProperty.Register%2A>는 동안를 설정 합니다.  
  
<a name="Freezable_Objects"></a>   
## <a name="freezable-objects"></a>Freezable 개체  
 는 <xref:System.Windows.Freezable> 고정 해제 및 고정의 두 가지 상태를 가진 특수 한 형식의 개체입니다. 가능할 때마다 개체를 고정하면 애플리케이션 성능이 향상되며 해당 작업 집합을 줄일 수 있습니다. 자세한 내용은 [Freezable 개체 개요](freezable-objects-overview.md)를 참조하세요.  
  
 <xref:System.Windows.Freezable> 각<xref:System.Windows.Freezable.Changed> 에는 변경 될 때마다 발생 하는 이벤트가 있습니다. 그러나 변경 알림은 애플리케이션 성능을 저하시킵니다.  
  
 각각 <xref:System.Windows.Shapes.Rectangle> 동일한<xref:System.Windows.Media.Brush> 개체를 사용 하는 다음 예제를 살펴보십시오.  
  
 [!code-csharp[Performance#PerformanceSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet2)]
 [!code-vb[Performance#PerformanceSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet2)]  
  
 기본적 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 으로는 개체의 <xref:System.Windows.Shapes.Shape.Fill%2A> 속성을 무효화 <xref:System.Windows.Shapes.Rectangle> 하기 <xref:System.Windows.Media.SolidColorBrush> 위해 개체 <xref:System.Windows.Freezable.Changed> 의 이벤트에 대 한 이벤트 처리기를 제공 합니다. 이 경우 <xref:System.Windows.Media.SolidColorBrush> 에서 <xref:System.Windows.Freezable.Changed> 이벤트를 발생 시켜야 할 때마다 각각 <xref:System.Windows.Shapes.Rectangle>에 대해 콜백 함수를 호출 해야 합니다. 이러한 콜백 함수 호출을 누적 하면 상당한 성능 저하가 발생 합니다. 또한 이 시점에서 처리기를 추가 및 제거하면 애플리케이션에서 이 작업을 위해 전체 목록을 통과해야 하므로 성능에 상당한 영향을 미칩니다. 응용 프로그램 시나리오가를 변경 <xref:System.Windows.Media.SolidColorBrush>하지 않는 경우 이벤트 처리기를 불필요 하 게 유지 관리 <xref:System.Windows.Freezable.Changed> 하는 비용을 지불 하 게 됩니다.  
  
 을 고정 <xref:System.Windows.Freezable> 하면 변경 알림을 유지 관리 하는 데 더 이상 리소스를 확장 필요가 없기 때문에 성능이 향상 될 수 있습니다. 아래 표에서는 <xref:System.Windows.Media.SolidColorBrush> <xref:System.Windows.Freezable.IsFrozen%2A> 속성이로 `true`설정 되어 있지 않은 경우와 비교 하 여 간단한의 크기를 보여 줍니다. 여기서는 <xref:System.Windows.Shapes.Shape.Fill%2A> 10 <xref:System.Windows.Shapes.Rectangle> 개의 개체 속성에 브러시 하나를 적용 한다고 가정 합니다.  
  
|**상태**|**Size**|  
|---------------|--------------|  
|시키면<xref:System.Windows.Media.SolidColorBrush>|212바이트|  
|고정 되지 않음<xref:System.Windows.Media.SolidColorBrush>|972바이트|  
  
 다음 코드 샘플에서는 이러한 개념을 보여 줍니다.  
  
 [!code-csharp[Performance#PerformanceSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet3)]
 [!code-vb[Performance#PerformanceSnippet3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet3)]  
  
### <a name="changed-handlers-on-unfrozen-freezables-may-keep-objects-alive"></a>고정되지 않은 Freezable에 대한 처리기를 변경하면 개체가 활성 상태로 유지될 수 있음  
 개체가 <xref:System.Windows.Freezable> 개체의 <xref:System.Windows.Freezable.Changed> 이벤트에 전달 하는 대리자는 사실상 해당 개체에 대 한 참조입니다. 따라서 이벤트 <xref:System.Windows.Freezable.Changed> 처리기는 개체가 예상 보다 오래 유지 될 수 있습니다. 개체의<xref:System.Windows.Freezable>이벤트를 수신 하도록 등록 된 개체를 정리 하는 경우 개체를 해제 하기 전에 해당 대리자를 제거 하는 것이 중요 합니다. <xref:System.Windows.Freezable.Changed>  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 이벤트를 <xref:System.Windows.Freezable.Changed> 내부적으로 후크 합니다. 예를 들어 값으로를 사용 <xref:System.Windows.Freezable> 하는 모든 종속성 속성은 자동으로 이벤트를 <xref:System.Windows.Freezable.Changed> 수신 대기 합니다. <xref:System.Windows.Shapes.Shape.Fill%2A> 를<xref:System.Windows.Media.Brush>사용 하는 속성은이 개념을 보여 줍니다.  
  
 [!code-csharp[Performance#PerformanceSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet4)]
 [!code-vb[Performance#PerformanceSnippet4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet4)]  
  
 `myBrush` <xref:System.Windows.Shapes.Rectangle> 에 <xref:System.Windows.Freezable.Changed> <xref:System.Windows.Media.SolidColorBrush> 대 한 할당에서 개체를 가리키는 대리자가 개체의 이벤트에 추가 됩니다. `myRectangle.Fill` 이는 다음 코드에서 실제로 `myRect`를 가비지 수집에 적합하게 만들지 않음을 의미합니다.  
  
 [!code-csharp[Performance#PerformanceSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet5)]
 [!code-vb[Performance#PerformanceSnippet5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet5)]  
  
 이 경우 `myBrush` 여전히 활성 상태를 `myRectangle` 유지 하 고 <xref:System.Windows.Freezable.Changed> 이벤트를 발생 시킬 때 다시 호출 합니다. 새 `myBrush` <xref:System.Windows.Shapes.Shape.Fill%2A> 의 속성에를 할당 하면에 `myBrush`또 다른 이벤트 처리기가 추가 됩니다. <xref:System.Windows.Shapes.Rectangle>  
  
 이러한 형식의 개체를 정리 하는 권장 방법은 <xref:System.Windows.Media.Brush> <xref:System.Windows.Shapes.Shape.Fill%2A> 속성에서을 제거 하 여 <xref:System.Windows.Freezable.Changed> 이벤트 처리기를 제거 하는 것입니다.  
  
 [!code-csharp[Performance#PerformanceSnippet6](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet6)]
 [!code-vb[Performance#PerformanceSnippet6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet6)]  
  
<a name="User_Interface_Virtualization"></a>   
## <a name="user-interface-virtualization"></a>사용자 인터페이스 가상화  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]또한는 데이터 바인딩된 자식 콘텐츠 <xref:System.Windows.Controls.StackPanel> 를 자동으로 "가상화" 하는 요소의 변형을 제공 합니다. 여기서 가상화라는 단어는 화면에 표시되는 항목에 따라 많은 수의 데이터 항목에서 개체의 하위 집합이 생성되는 기술을 가리킵니다. 특정 시점에 화면에 표시되는 것보다 많은 개수의 UI 요소를 생성하는 것은 메모리 및 프로세서 측면에서 비효율적입니다. <xref:System.Windows.Controls.VirtualizingStackPanel>에서 <xref:System.Windows.Controls.VirtualizingPanel>제공 하는 기능을 통해 표시 되는 항목을 계산 하 고 <xref:System.Windows.Controls.ItemsControl> , (예 <xref:System.Windows.Controls.ListBox> : <xref:System.Windows.Controls.ListView>또는)에서를 사용 하 여 표시 되는 <xref:System.Windows.Controls.ItemContainerGenerator> 항목에 대 한 요소만 만듭니다.  
  
 성능을 최적화하기 위해 이러한 항목에 대한 시각적 개체는 화면에 보이는 경우에만 생성되거나 활성 상태를 유지합니다. 컨트롤의 가시 영역에 더 이상 존재하지 않는 시각적 개체는 제거될 수 있습니다. 이는 데이터 개체가 로컬 컬렉션에 전혀 존재하지 않고 필요에 따라 스트리밍되는 데이터 가상화와 혼동해서는 안 됩니다.  
  
 아래 표에서는 5000 <xref:System.Windows.Controls.TextBlock> 요소를 <xref:System.Windows.Controls.StackPanel> 및 <xref:System.Windows.Controls.VirtualizingStackPanel>에 추가 하 고 렌더링 하는 데 경과 된 시간을 보여 줍니다. 이 시나리오에서 측정은 패널 요소가 텍스트 문자열을 표시 하는 시간에 텍스트 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 문자열을 <xref:System.Windows.Controls.ItemsControl> 개체의 속성에 연결 하는 시간을 나타냅니다.  
  
|**호스트 패널**|**렌더링 시간(ms)**|  
|--------------------|----------------------------|  
|<xref:System.Windows.Controls.StackPanel>|3210|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|46|  
  
## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 성능 최적화](optimizing-wpf-application-performance.md)
- [애플리케이션 성능 계획](planning-for-application-performance.md)
- [하드웨어 이용](optimizing-performance-taking-advantage-of-hardware.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
- [2차원 그래픽 및 이미징](optimizing-performance-2d-graphics-and-imaging.md)
- [응용 프로그램 리소스](optimizing-performance-application-resources.md)
- [텍스트](optimizing-performance-text.md)
- [데이터 바인딩](optimizing-performance-data-binding.md)
- [기타 성능 권장 사항](optimizing-performance-other-recommendations.md)
