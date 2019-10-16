---
title: WPF 버전 4.5의 새로운 기능
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Presentation Foundation [WPF], what's new
- WPF [WPF], what's new
ms.assetid: db086ae4-70bb-4862-95db-2eaca5216bc3
ms.openlocfilehash: 0dbe038bed3fd62589b2f3906441e27761e0438a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649155"
---
# <a name="whats-new-in-wpf-version-45"></a>WPF 버전 4.5의 새로운 기능
<a name="introduction"></a> 이 항목에서는의 새로운 기능과 향상 된 기능에 대 한 정보가 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 4.5 버전입니다.  
  
 이 항목에는 다음과 같은 단원이 포함되어 있습니다.  
  
- [리본 컨트롤](#ribbon_control)  
  
- [그룹화된 큰 데이터 집합을 표시할 때의 성능 개선](#grouped_virtualization)  
  
- [VirtualizingPanel의 새로운 기능](#VirtualizingPanel)  
  
- [정적 속성에 바인딩](#static_properties)  
  
- [UI가 아닌 스레드에서 컬렉션 액세스](#xthread_access)  
  
- [동기적 및 비동기적으로 데이터 유효성 검사](#INotifyDataErrorInfo)  
  
- [데이터 바인딩 원본을 자동으로 업데이트](#delay)  
  
- [ICustomTypeProvider를 구현하는 형식에 바인딩](#ICustomTypeProvider)  
  
- [바인딩 식에서 데이터 바인딩 정보 검색](#binding_state)  
  
- [유효한 DataContext 개체 확인](#DisconnectedSource)  
  
- [데이터 값이 변경될 때 데이터의 위치 변경(라이브 셰이핑)](#live_shaping)  
  
- [이벤트에 대한 약한 참조 설정을 위한 지원 개선](#weak_event_pattern)  
  
- [Dispatcher 클래스에 대한 새로운 메서드](#async)  
  
- [이벤트에 대한 태그 확장](#events_markup_extenions)  
  
<a name="ribbon_control"></a>   
## <a name="ribbon-control"></a>리본 컨트롤  
 WPF 4.5와 함께 제공 되는 <xref:System.Windows.Controls.Ribbon.Ribbon> 빠른 실행 도구 모음, 응용 프로그램 메뉴 및 탭을 호스팅하는 컨트롤입니다.  자세한 내용은 [리본 개요](/visualstudio/vsto/ribbon-overview)를 참조하세요.  
  
<a name="grouped_virtualization"></a>   
## <a name="improved-performance-when-displaying-large-sets-of-grouped-data"></a>그룹화된 큰 데이터 집합을 표시할 때의 성능 개선  
 화면에 표시되는 항목에 따라 많은 수의 데이터 항목에서 사용자 인터페이스(UI) 요소의 하위 집합이 생성될 때 UI 가상화가 발생합니다. 합니다 <xref:System.Windows.Controls.VirtualizingPanel> 정의 <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A> 그룹화 된 데이터에 대 한 UI 가상화를 사용할 수 있는 속성을 연결 합니다.  데이터 그룹화에 대 한 자세한 내용은 참조 하는 방법. 데이터 정렬 및 그룹화 XAML에서 뷰를 사용 합니다.  데이터를 그룹화 하는 가상화 하는 방법에 대 한 자세한 내용은 참조는 <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizingWhenGrouping%2A> 연결 된 속성입니다.  
  
<a name="VirtualizingPanel"></a>   
## <a name="new-features-for-the-virtualizingpanel"></a>VirtualizingPanel의 새로운 기능  
  
1. 지정할 수 있습니다 있는지 여부를 <xref:System.Windows.Controls.VirtualizingPanel>와 같은 <xref:System.Windows.Controls.VirtualizingStackPanel>를 사용 하 여 부분 항목을 표시는 <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> 연결 된 속성입니다. 하는 경우 <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> 로 설정 된 <xref:System.Windows.Controls.ScrollUnit.Item>는 <xref:System.Windows.Controls.VirtualizingPanel> 완전히 표시 되는 항목만 표시 됩니다. 하는 경우 <xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A> 로 설정 된 <xref:System.Windows.Controls.ScrollUnit.Pixel>는 <xref:System.Windows.Controls.VirtualizingPanel> 부분적으로 표시 된 항목을 표시할 수 있습니다.  
  
2. 뷰포트 전후 캐시의 크기를 지정할 수 있습니다 때 합니다 <xref:System.Windows.Controls.VirtualizingPanel> 이 사용 하 여 가상화는 <xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A> 연결 된 속성입니다.  캐시는 항목이 가상화되지 않는 뷰포트 위 또는 아래 공간 양입니다.  캐시를 사용하면 뷰로 스크롤하는 동안 UI 요소가 생성되지 않도록 하여 성능을 향상시킬 수 있습니다. 캐시는 낮은 우선 순위에서 채워지므로 작업 중에는 애플리케이션이 응답하지 않게 됩니다. 합니다 <xref:System.Windows.Controls.VirtualizingPanel.CacheLengthUnit%2A?displayProperty=nameWithType> 속성에서 사용 되는 측정 단위를 결정 <xref:System.Windows.Controls.VirtualizingPanel.CacheLength%2A?displayProperty=nameWithType>합니다.  
  
<a name="static_properties"></a>   
## <a name="binding-to-static-properties"></a>정적 속성에 바인딩  
 데이터 바인딩 원본으로 정적 속성을 사용할 수 있습니다. 데이터 바인딩 엔진은 정적 이벤트가 발생할 경우 속성 값이 변경되는 것을 인식합니다.  예를 들어 `SomeClass` 클래스가 `MyProperty`라는 정적 속성을 정의하는 경우 `SomeClass`는 `MyProperty` 값이 변경될 때 발생하는 정적 이벤트를 정의할 수 있습니다.  정적 이벤트는 다음 서명 중 하나를 사용할 수 있습니다.  
  
- `public static event EventHandler MyPropertyChanged;`  
  
- `public static event EventHandler<PropertyChangedEventArgs> StaticPropertyChanged;`  
  
 첫 번째 경우에서 클래스 표시 라는 정적 이벤트를 *PropertyName* `Changed` 통과 하는 <xref:System.EventArgs> 이벤트 처리기에 있습니다.  두 번째 경우 클래스 라는 정적 이벤트를 노출 `StaticPropertyChanged` 통과 하는 <xref:System.ComponentModel.PropertyChangedEventArgs> 이벤트 처리기에 있습니다. 정적 속성을 구현하는 클래스에서 두 메서드 중 하나를 사용하여 속성-변경 알림이 발생하도록 선택할 수 있습니다.  
  
<a name="xthread_access"></a>   
## <a name="accessing-collections-on-non-ui-threads"></a>UI가 아닌 스레드에서 컬렉션 액세스  
 WPF를 사용하면 컬렉션을 만들지 않은 스레드에서 데이터 컬렉션을 액세스하고 수정할 수 있습니다.  이를 통해 데이터베이스와 같은 외부 원본에서 데이터를 수신하는 데 백그라운드 스레드를 사용하고 UI 스레드에 데이터를 표시할 수 있습니다.  다른 스레드를 사용하여 콜렉션을 수정하면 사용자 인터페이스는 사용자 상호 작용에 응답성을 유지합니다.  
  
<a name="INotifyDataErrorInfo"></a>   
## <a name="synchronously-and-asynchronously-validating-data"></a>동기적 및 비동기적으로 데이터 유효성 검사  
 <xref:System.ComponentModel.INotifyDataErrorInfo> 인터페이스를 사용자 지정 유효성 검사 규칙을 구현 하 여 유효성 검사 결과 비동기적으로 노출 하는 데이터 엔터티 클래스를 사용 합니다. 또한 이 인터페이스는 사용자 지정 오류 개체, 속성당 여러 오류, 속성 간 오류 및 엔터티 수준 오류도 지원합니다.  자세한 내용은 <xref:System.ComponentModel.INotifyDataErrorInfo>을 참조하세요.  
  
<a name="delay"></a>   
## <a name="automatically-updating-the-source-of-a-data-binding"></a>데이터 바인딩 원본을 자동으로 업데이트  
 데이터 바인딩을 사용 하 여 데이터 소스를 업데이트 하는 경우 사용할 수 있습니다는 <xref:System.Windows.Data.BindingBase.Delay%2A> 원본이 업데이트 되기 전에 대상에서 속성이 변경 된 후 전달할 시간을 지정 하는 속성입니다.  예를 들어 있다고 가정를 <xref:System.Windows.Controls.Slider> 있는 해당 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 양방향 속성 데이터가 데이터 개체의 속성에 바인딩할 하며 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 속성이 <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>.  이 예제에서는 사용자가 이동 합니다 <xref:System.Windows.Controls.Slider>, 각 픽셀 마다 원본이 업데이트는는 <xref:System.Windows.Controls.Slider> 이동 합니다.  원본 개체 슬라이더의 값을 일반적으로 필요한 경우에만 슬라이더의 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 변경 중지 합니다.  소스를 너무 자주 업데이트를 방지 하려면 사용 하 여 <xref:System.Windows.Data.BindingBase.Delay%2A> thumb이 이동을 중지 한 후 일정 기간 경과 될 때까지 소스 업데이트 되지 않아야 지정 합니다.  
  
<a name="ICustomTypeProvider"></a>   
## <a name="binding-to-types-that-implement-icustomtypeprovider"></a>ICustomTypeProvider를 구현하는 형식에 바인딩  
 WPF 데이터 바인딩을 구현 하는 개체를 지 원하는 <xref:System.Reflection.ICustomTypeProvider>, 사용자 지정 형식이 라고도 합니다.  다음과 같은 경우 사용자 지정 형식을 사용할 수 있습니다.  
  
1. 로 <xref:System.Windows.PropertyPath> 데이터 바인딩에 있습니다. 예를 들어 합니다 <xref:System.Windows.Data.Binding.Path%2A> 의 속성을 <xref:System.Windows.Data.Binding> 사용자 지정 형식의 속성을 참조할 수 있습니다.  
  
2. 값으로는 <xref:System.Windows.DataTemplate.DataType%2A> 속성입니다.  
  
3. 자동으로 생성 된 열을 결정 하는 형식으로는 <xref:System.Windows.Controls.DataGrid>합니다.  
  
<a name="binding_state"></a>   
## <a name="retrieving-data-binding-information-from-a-binding-expression"></a>바인딩 식에서 데이터 바인딩 정보 검색  
 특정 경우에 발생할 수 있습니다는 <xref:System.Windows.Data.BindingExpression> 의 <xref:System.Windows.Data.Binding> 및 바인딩의 원본 및 대상 개체에 대 한 정보가 필요 합니다.  원본 또는 대상 개체나 연결된 속성을 얻도록 새로운 API가 추가되었습니다.  경우는 <xref:System.Windows.Data.BindingExpression>, 다음 Api를 사용 하 여 원본 및 대상에 대 한 정보를 가져옵니다.  
  
|바인딩의 다음 값을 찾으려면|다음 API 사용|  
|---------------------------------------|------------------|  
|대상 개체|<xref:System.Windows.Data.BindingExpressionBase.Target%2A?displayProperty=nameWithType>|  
|대상 속성|<xref:System.Windows.Data.BindingExpressionBase.TargetProperty%2A?displayProperty=nameWithType>|  
|소스 개체|<xref:System.Windows.Data.BindingExpression.ResolvedSource%2A?displayProperty=nameWithType>|  
|원본 속성|<xref:System.Windows.Data.BindingExpression.ResolvedSourcePropertyName%2A?displayProperty=nameWithType>|  
|여부는 <xref:System.Windows.Data.BindingExpression> 속한를 <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingExpressionBase.BindingGroup%2A?displayProperty=nameWithType>|  
|소유자는 <xref:System.Windows.Data.BindingGroup>|<xref:System.Windows.Data.BindingGroup.Owner%2A>|  
  
<a name="DisconnectedSource"></a>   
## <a name="checking-for-a-valid-datacontext-object"></a>유효한 DataContext 개체 확인  
 경우가 여기서 합니다 <xref:System.Windows.FrameworkElement.DataContext%2A> 에서 항목 컨테이너의는 <xref:System.Windows.Controls.ItemsControl> 연결이 끊어지면 합니다.  항목 컨테이너에 있는 항목을 표시 하는 UI 요소는는 <xref:System.Windows.Controls.ItemsControl>합니다.  경우는 <xref:System.Windows.Controls.ItemsControl> 데이터가 컬렉션에 바인딩된 각 항목에 대해 항목 컨테이너가 생성 됩니다. 경우에 따라 항목 컨테이너는 시각적 트리에서 제거됩니다. 항목 컨테이너는 제거 되는 두 가지 일반적인 경우는 기본 컬렉션에서 항목이 제거 될 때 및에 가상화가 사용 하는 경우는 <xref:System.Windows.Controls.ItemsControl>합니다. 이러한 경우에는 <xref:System.Windows.FrameworkElement.DataContext%2A> 항목 컨테이너의 속성에서 반환 된 sentinel 개체로 설정 됩니다는 <xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A?displayProperty=nameWithType> 정적 속성입니다.  확인 해야 하는지 여부를 <xref:System.Windows.FrameworkElement.DataContext%2A> 값과 같음는 <xref:System.Windows.Data.BindingOperations.DisconnectedSource%2A> 개체에 액세스 하기 전에 <xref:System.Windows.FrameworkElement.DataContext%2A> 항목 컨테이너의 합니다.  
  
<a name="live_shaping"></a>   
## <a name="repositioning-data-as-the-datas-values-change-live-shaping"></a>데이터 값이 변경될 때 데이터의 위치 변경(라이브 셰이핑)  
 데이터의 컬렉션을 그룹화, 정렬 또는 필터링할 수 있습니다. WPF 4.5에서는 데이터가 수정되면 데이터를 다시 배열할 수 있습니다. 예를 들어, 애플리케이션에서 사용 하는 <xref:System.Windows.Controls.DataGrid> 따라 주식 시장에 주식, 주식을 나열 하려면 정렬 합니다. 주식에서 실시간 정렬을 사용 하도록 설정 하는 경우 <xref:System.Windows.Data.CollectionView>에서 주식의 위치는 <xref:System.Windows.Controls.DataGrid> 재고 값이 큰 이동 또는 보다 작은 다른 주식의 값입니다.   자세한 내용은 참조는 <xref:System.ComponentModel.ICollectionViewLiveShaping> 인터페이스입니다.  
  
<a name="weak_event_pattern"></a>   
## <a name="improved-support-for-establishing-a-weak-reference-to-an-event"></a>이벤트에 대한 약한 참조 설정을 위한 지원 개선  
 이벤트 구독자가 추가 인터페이스 구현 없이 참여할 수 있으므로 약한 이벤트 패턴을 구현하기가 더 쉬워졌습니다.  제네릭 <xref:System.Windows.WeakEventManager> 클래스에 있습니다 경우 전용 약한 이벤트 패턴에 참여 하려면 구독자 <xref:System.Windows.WeakEventManager> 특정 이벤트에 대해 존재 하지 않습니다.  자세한 내용은 [약한 이벤트 패턴](../advanced/weak-event-patterns.md)을 참조하세요.  
  
<a name="async"></a>   
## <a name="new-methods-for-the-dispatcher-class"></a>Dispatcher 클래스에 대한 새로운 메서드  
 Dispatcher 클래스는 동기 및 비동기 작업에 대해 새로운 메서드를 정의합니다.  동기 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> 오버 로드를 정의 하는 메서드를 <xref:System.Action> 또는 <xref:System.Func%601> 매개 변수입니다. 새 비동기 메서드를 <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>, 또한를 <xref:System.Action> 또는 <xref:System.Func%601> 콜백 매개 변수 및 반환을 <xref:System.Windows.Threading.DispatcherOperation> 또는 <xref:System.Windows.Threading.DispatcherOperation%601>합니다.   합니다 <xref:System.Windows.Threading.DispatcherOperation> 하 고 <xref:System.Windows.Threading.DispatcherOperation%601> 클래스 정의 <xref:System.Threading.Tasks.Task> 속성입니다.  호출 하는 경우 <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A>를 사용할 수는 `await` 키워드 중 하나를 사용 하 여 합니다 <xref:System.Windows.Threading.DispatcherOperation> 또는 연결 된 <xref:System.Threading.Tasks.Task>합니다. 동기적으로 대기 해야 하는 경우는 <xref:System.Threading.Tasks.Task> 에서 반환 하는 <xref:System.Windows.Threading.DispatcherOperation> 또는 <xref:System.Windows.Threading.DispatcherOperation%601>를 호출 합니다 <xref:System.Windows.Threading.TaskExtensions.DispatcherOperationWait%2A> 확장 메서드. 호출 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 작업이 호출 스레드에서 큐 대기는 경우 교착 상태가 발생 합니다. 사용에 대 한 자세한 내용은 <xref:System.Threading.Tasks.Task> 비동기 작업을 수행 하려면 참조 [작업 병렬 처리 (작업 병렬 라이브러리)](../../../standard/parallel-programming/task-based-asynchronous-programming.md)합니다.  
  
<a name="events_markup_extenions"></a>   
## <a name="markup-extensions-for-events"></a>이벤트에 대한 태그 확장  
 WPF 4.5에서는 이벤트에 대한 태그 확장을 지원합니다.  WPF는 이벤트에 사용될 태그 확장을 정의하지 않지만 타사에서 이벤트에 사용할 수 있는 태그 확장을 만들 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [.NET Framework의 새로운 기능](../../whats-new/index.md)
