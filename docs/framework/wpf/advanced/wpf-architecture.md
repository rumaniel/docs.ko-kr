---
title: WPF 아키텍처
ms.date: 03/30/2017
helpviewer_keywords:
- properties [WPF], attached
- attached properties [WPF]
- architecture [WPF]
- unmanaged components [WPF]
- affinity thread [WPF]
- Storyboards [WPF]
- milcore [WPF]
- components [WPF], unmanaged
- painter's algorithm
- interfaces [WPF], INotifyPropertyChange
- CommandBindings [WPF]
- data templates [WPF]
- thread [WPF], affinity
ms.assetid: 8579c10b-76ab-4c52-9691-195ce02333c8
ms.openlocfilehash: 39cf4b60262afb1e3745a82c734391385669f5d3
ms.sourcegitcommit: 3eeea78f52ca771087a6736c23f74600cc662658
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2019
ms.locfileid: "68671916"
---
# <a name="wpf-architecture"></a>WPF 아키텍처
이 항목에서는 Windows Presentation Foundation (WPF) 클래스 계층 구조 둘러보기를 제공 합니다. 이 항목은 대부분의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 주요 하위 시스템을 다루며 이들이 어떻게 상호 작용하는지를 설명하고, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 설계자가 선택한 몇 가지 사항에 대해서 자세히 설명합니다.  

<a name="System_Object"></a>   
## <a name="systemobject"></a>System.Object  
 기본 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 프로그래밍 모델은 관리 코드를 통해 노출됩니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 초기 디자인 단계에서는 시스템의 관리되는 구성 요소와 관리되지 않는 구성 요소를 정확하게 구분하는 방법에 대한 많은 논쟁이 있었습니다. CLR은 개발 작업을 더 생산적이 고 강력한 기능을 제공 하는 많은 기능을 제공 합니다 (메모리 관리, 오류 처리, 공용 유형 시스템 등). 단,이 경우에는 비용이 듭니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 주요 구성 요소는 아래 그림에 설명되어 있습니다. 다이어그램의 빨간색 섹션(PresentationFramework, PresentationCore 및 milcore)은 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 주요 코드 부분입니다. 이 중에서 하나(milcore)만 관리되지 않는 구성 요소입니다. Milcore는 DirectX와 긴밀 하 게 통합 될 수 있도록 비관리 코드로 작성 됩니다. 의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 모든 디스플레이는 DirectX 엔진을 통해 수행 되며 하드웨어 및 소프트웨어를 효율적으로 렌더링할 수 있습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에는 메모리 및 실행에 대한 세부적인 제어도 필요합니다. Milcore의 컴퍼지션 엔진은 성능이 매우 중요 하므로 CLR의 많은 이점을 제공 하 여 성능을 향상 시킬 수 있습니다.  
  
 ![.NET Framework 내 WPF의 위치.](./media/wpf-architect1.PNG "wpf_architect1")  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 관리되는 부분과 관리되지 않는 부분 간 통신에 대해서는 이 항목의 뒷부분에서 설명합니다. 관리되는 프로그래밍 모델의 나머지 부분은 아래에 설명되어 있습니다.  
  
<a name="System_Threading_DispatcherObject"></a>   
## <a name="systemthreadingdispatcherobject"></a>System.Threading.DispatcherObject  
 의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 대부분 개체는 동시성 <xref:System.Windows.Threading.DispatcherObject>및 스레딩을 처리 하기 위한 기본 구문을 제공 하는에서 파생 됩니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 디스패처에 의해 구현된 메시징 시스템을 기반으로 합니다. 이는 친숙한 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 메시지 펌프와 유사하게 작동합니다. 사실 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 디스패처는 User32 메시지를 사용하여 크로스 스레드 호출을 수행합니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서 동시성을 논의할 때는 두 가지 핵심 개념인 디스패처와 스레드 선호도를 반드시 이해해야 합니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 디자인 단계에서 목표는 단일 실행 스레드로 이동하되 스레드가 아닌 "선호" 모델로 이동하는 것이었습니다. 스레드 선호도는 일부 형식의 상태를 저장하기 위해 구성 요소가 실행 스레드의 ID를 사용할 때 발생합니다. 이에 대한 가장 일반적인 형태는 TLS(스레드 로컬 저장소)를 사용하여 상태를 저장하는 것입니다. 스레드 선호도는 각 논리적 실행 스레드가 운영 체제에서 하나의 실제 스레드에만 소속될 수 있도록 합니다. 따라서 메모리를 많이 소비할 수 있습니다. 결국 WPF의 스레딩 모델은 스레드 선호도가 있는 단일 스레딩된 실행의 기존 User32 스레딩 모델과 계속 동기화됩니다. 이에 대한 주요 이유는 상호 운용성 때문입니다. [!INCLUDE[TLA2#tla_ole2.0](../../../../includes/tla2sharptla-ole2-0-md.md)], 클립보드, Internet Explorer 등의 시스템의 경우 모두 STA(단일 스레드 선호도) 실행이 필요합니다.  
  
 STA 스레딩이 포함된 개체가 있다면 스레드 간에 통신하고 올바른 스레드에 있는지를 확인할 수 있는 방법이 필요합니다. 여기에서 디스패처의 역할이 필요합니다. 디스패처는 우선 순위가 지정된 여러 개의 큐가 있는 기본 메시지 디스패치 시스템입니다. 메시지의 예로 원시 입력 알림(마우스 이동), 프레임워크 기능(레이아웃) 또는 사용자 명령(이 메서드 실행)을 들 수 있습니다. 에서 <xref:System.Windows.Threading.DispatcherObject>파생 하 여 STA 동작을 포함 하는 CLR 개체를 만들고 만들 때 디스패처에 대 한 포인터를 지정 합니다.  
  
<a name="System_Windows_DependencyObject"></a>   
## <a name="systemwindowsdependencyobject"></a>System.Windows.DependencyObject  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]를 빌드하는 데 사용된 기본 아키텍처 방법 중 하나는 메서드나 이벤트보다 속성을 선호하는 것이었습니다. 속성은 선언적이며 작업 대신 의도를 보다 쉽게 지정할 수 있습니다. 또한 모델 중심 또는 데이터 중심의 시스템을 지원하여 사용자 인터페이스 콘텐츠를 표시했습니다. 이 방법을 통해 애플리케이션의 동작을 보다 효과적으로 제어하기 위해 사용자가 바인딩할 수 있는 것보다 더 많은 속성을 의도적으로 만들 수 있었습니다.  
  
 속성으로 제어 되는 시스템을 더 확보 하려면 CLR에서 제공 하는 것 보다 더 다양 한 속성 시스템이 필요 합니다. 간단한 예로 변경 알림을 들 수 있습니다. 양방향 바인딩을 사용하기 위해서는 바인드의 양쪽이 변경 알림을 지원해야 합니다. 동작이 속성 값에 연결되려면 속성 값이 변경될 때 알림을 받아야 합니다. Microsoft .NET 프레임 워크에는 개체가 변경 알림을 게시할 수 있도록 하는 **INotifyPropertyChange**인터페이스가 있습니다. 단,이 인터페이스는 선택 사항입니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 <xref:System.Windows.DependencyObject> 형식에서 파생 된 다양 한 속성 시스템을 제공 합니다. 속성 시스템은 속성 식 간의 종속성을 추적하고 종속성이 변경될 때 속성 값의 유효성을 자동으로 다시 검사하는 면에서 진정한 "종속성" 속성 시스템입니다. 예를 들어를 상속 하는 속성 ( <xref:System.Windows.Controls.Control.FontSize%2A>예:)이 있는 경우 값을 상속 하는 요소의 부모에서 속성이 변경 되 면 시스템이 자동으로 업데이트 됩니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 속성 시스템의 기반은 속성 식의 개념입니다. 이 첫 릴리스의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서는 속성 식 시스템이 닫혀 있고 식이 모두 프레임워크의 일부로 제공됩니다. 속성 시스템에 하드 코드된 상속, 스타일 설정 또는 데이터 바인딩이 없고 대신 프레임워크 내의 이후 계층에 의해 제공되는 이유는 식 때문입니다.  
  
 속성 시스템은 밀도가 낮은 속성 값 스토리지도 제공합니다. 개체에 수십 또는 수백 개의 속성이 있을 수 있고 대부분의 값은 기본 상태(상속됨, 스타일에 의해 설정됨 등)로 되어 있으므로 개체의 모든 인스턴스에서 모든 속성을 정의할 필요는 없습니다.  
  
 속성 시스템의 마지막 새 기능은 연결된 속성이라는 개념입니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 요소는 컴퍼지션 및 구성 요소 재사용 원칙에 따라 빌드됩니다. <xref:System.Windows.Controls.Grid> 레이아웃 요소와 같은 일부 포함 요소에는 자식 요소에 대 한 추가 데이터가 필요 하 여 해당 동작 (예: 행/열 정보)을 제어 하는 경우가 종종 있습니다. 이러한 모든 속성을 모든 요소와 연결하는 대신 개체가 다른 개체에 대한 속성 정의를 제공할 수 있습니다. 이는 JavaScript의 "expando" 기능과 유사합니다.  
  
<a name="System_Windows_Media_Visual"></a>   
## <a name="systemwindowsmediavisual"></a>System.Windows.Media.Visual  
 시스템이 정의되면 다음 단계는 화면에서 픽셀을 그리는 것입니다. 클래스 <xref:System.Windows.Media.Visual> 는 시각적 개체의 트리를 빌드하기 위해 제공 합니다. 각 개체에는 해당 지침을 렌더링 하는 방법에 대 한 그리기 명령 및 메타 데이터 (클리핑, 변환 등)가 필요 합니다. <xref:System.Windows.Media.Visual>는 매우 가볍고 유연 하도록 설계 되었으므로 대부분의 기능에는 공용 API 노출이 없으며 보호 된 콜백 함수에 크게 의존 합니다.  
  
 <xref:System.Windows.Media.Visual>는 컴퍼지션 시스템의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 진입점입니다. <xref:System.Windows.Media.Visual>는 이러한 두 하위 시스템, 즉 관리 되는 API와 관리 되지 않는 milcore 간의 연결 지점입니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 milcore에 의해 관리되는 관리되지 않는 데이터 구조를 이동하여 데이터를 표시합니다. 컴포지션 노드라고 하는 이 구조는 각 노드에 렌더링 명령이 있는 계층적 디스플레이 트리를 나타냅니다. 아래 그림의 오른쪽에 있는 이 트리에는 메시징 프로토콜을 통해서만 액세스할 수 있습니다.  
  
 프로그래밍할 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]때이 메시징 프로토콜 <xref:System.Windows.Media.Visual> 을 통해 컴퍼지션 트리와 내부적으로 통신 하는 요소 및 파생 형식을 만듭니다. <xref:System.Windows.Media.Visual> 의[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 각은 하나, 없음 또는 여러 컴퍼지션 노드를 만들 수 있습니다.  
  
 ![Windows Presentation Foundation 시각적 트리.](./media/wpf-architecture2.PNG "wpf_architecture2")  
  
 여기에서 알아 두어야 할 매우 중요한 아키텍처 정보가 있습니다. 그것은 바로 시각 요소 및 그리기 명령의 전체 트리가 캐시된다는 사실입니다. 그래픽 측면에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 유지된 렌더링 시스템을 사용합니다. 이로 인해 시스템은 사용자 코드에 대한 콜백을 차단하는 컴포지션 시스템 없이 높은 화면 주사율로 다시 그릴 수 있습니다. 따라서 응답하지 않는 애플리케이션이 나타나지 않게 됩니다.  
  
 다이어그램에서 놓치기 쉬운 또 다른 중요한 정보는 시스템이 실제로 컴포지션을 수행하는 방법입니다.  
  
 User32.dll 및 GDI에서 시스템은 직접 실행 모드 클리핑 시스템에서 작동 합니다. 구성 요소를 렌더링해야 할 때는 시스템이 구성 요소가 픽셀과 닿을 수 없는 곳의 바깥에 클리핑 경계를 설정한 다음 구성 요소가 해당 상자에서 픽셀을 그려야 합니다. 이 시스템은 무언가 변경될 때 영향을 받는 구성 요소만 처리하면 되기 때문에 메모리가 제약된 시스템에서 잘 작동합니다. 단일 픽셀의 색상에 두 개의 구성 요소가 관여하는 경우는 없습니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 "페인터 알고리즘" 그리기 모델을 사용합니다. 즉, 각 구성 요소를 클리핑하는 대신 각 구성 요소가 디스플레이의 뒤쪽에서 앞쪽으로 렌더링해야 합니다. 따라서 각 구성 요소가 이전 구성 요소의 디스플레이에 그릴 수 있습니다. 이 모델의 장점은 복잡하고 부분적인 투명 모양이 가능하다는 것입니다. 오늘날의 최신 그래픽 하드웨어를 사용 하 여이 모델은 상대적으로 빠릅니다 (User32.dll/GDI를 만든 경우는 아님).  
  
 앞에서 언급했듯이 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 핵심 방법은 보다 선언적인 "속성 중심의" 프로그래밍 모델로 이동하는 것입니다. 시각적 시스템에서는 두 가지 흥미로운 장소에서 이러한 이동이 눈에 띕니다.  
  
 첫째, 유지된 모드 그래픽 시스템을 고려해 보면 명령적 DrawLine/DrawLine 형식 모델에서 데이터 지향 모델인 new Line()/new Line()으로 이동하는 것입니다. 이러한 데이터 중심 렌더링으로의 이동으로 인해 속성을 사용하여 그리기 지침에 대한 복잡한 작업을 표현할 수 있습니다. 에서 <xref:System.Windows.Media.Drawing> 파생 되는 형식은 실제로 렌더링을 위한 개체 모델입니다.  
  
 둘째, 애니메이션 시스템을 평가할 경우 거의 모든 내용이 선언적인 것을 볼 수 있습니다. 개발자가 다음 위치 또는 다음 색상을 컴퓨팅하도록 하는 대신 애니메이션을 애니메이션 개체의 속성 집합으로 표현할 수 있습니다. 그런 다음 이 애니메이션은 개발자 또는 디자이너의 의도(예: 5초 이내에 이 단추를 다른 곳으로 이동)를 표현할 수 있으며 시스템은 이를 완료하기 위한 가장 효율적인 방법을 파악할 수 있습니다.  
  
<a name="System_Windows_UIElement"></a>   
## <a name="systemwindowsuielement"></a>System.Windows.UIElement  
 <xref:System.Windows.UIElement>레이아웃, 입력 및 이벤트를 포함 하 여 핵심 하위 시스템을 정의 합니다.  
  
 레이아웃은 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 핵심 개념입니다. 대부분의 시스템에는 고정된 레이아웃 모델 집합(HTML은 세 가지 레이아웃 모델인 흐름, 절대 및 테이블을 지원함)이 있거나 레이아웃 모델이 아예 없습니다(User32는 실제로 절대 위치 지정만 지원함). [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 개발자 및 디자이너가 명령적 논리 대신 속성 값을 중심으로 운영될 수 있는 유연하고 확장 가능한 레이아웃 모델을 원한다는 가정에서 출발했습니다. 수준에서 레이아웃에 대 한 기본 계약이 도입 되었습니다. and <xref:System.Windows.UIElement.Arrange%2A> 는를 사용 <xref:System.Windows.UIElement.Measure%2A> 하는 2 단계 모델입니다. <xref:System.Windows.UIElement>  
  
 <xref:System.Windows.UIElement.Measure%2A>구성 요소에서 수행할 크기를 결정할 수 있습니다. 이는 부모 요소가 자식에 <xref:System.Windows.UIElement.Arrange%2A> 게 최적의 위치와 크기를 결정 하기 위해 여러 시간을 측정 하도록 요청 하는 상황이 많기 때문에에서 별도의 단계입니다. 부모 요소가 자식 요소에게 측정을 요구한다는 사실은 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 또 다른 주요 방법인 콘텐츠에 맞는 크기를 나타냅니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 내에 있는 모든 컨트롤은 콘텐츠의 기본 크기에 맞게 크기가 조정되는 기능을 지원합니다. 이에 따라 지역화가 훨씬 간단해지고 크기 조정에 따른 요소의 동적 레이아웃이 가능합니다. <xref:System.Windows.UIElement.Arrange%2A> 단계를 통해 부모는 위치를 지정 하 고 각 자식의 최종 크기를 결정할 수 있습니다.  
  
 대부분의 경우에는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] <xref:System.Windows.Media.Visual> 및 관련 개체의 출력 측면에 대해 이야기 하는 데 많은 시간이 소요 됩니다. 입력 측면에도 새로운 내용이 매우 많습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 입력 모델에서 가장 근본적인 변화는 입력 이벤트가 시스템을 통해 라우트되는 일관된 모델입니다.  
  
 입력은 커널 모드 디바이스 드라이버의 신호로 시작되며 Windows 커널 및 User32가 관련된 복잡한 프로세스를 통해 올바른 프로세스 및 스레드로 라우트됩니다. 입력에 해당하는 User32 메시지가 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]로 라우트되면 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 원시 입력 메시지로 변환되고 디스패처로 전송됩니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 원시 입력 이벤트를 여러 개의 실제 이벤트로 변환하여 "MouseEnter"와 같은 기능이 시스템의 낮은 수준에서 구현될 수 있도록 합니다. 이 경우 이러한 기능의 배달이 보장됩니다.  
  
 각 입력 이벤트는 최소한 두 개의 이벤트인 "미리 보기" 이벤트와 실제 이벤트로 변환됩니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에 있는 모든 이벤트는 요소 트리를 통해 라우트되는 개념입니다. 이벤트는 트리의 대상에서 루트로 이동 하는 경우 "버블링" 이라고 하며, 루트에서 시작 하 여 대상으로 이동 하는 경우 "터널" 이라고 합니다. 입력 미리 보기 이벤트는 터널링되어 트리에 있는 각 요소가 이벤트를 필터링하거나 이벤트에 대한 작업을 수행할 수 있는 기회를 제공합니다. 그런 다음 일반(미리 보기 아님) 이벤트가 대상에서 루트로 위로 버블링됩니다.  
  
 이러한 터널링 단계와 버블링 단계 간의 구분으로 인해 컴포지션 영역에서 키보드 액셀러레이터 같은 기능이 일관된 방식으로 구현됩니다. User32에서는 지원하고자 하는 모든 가속기를 포함하는 단일 글로벌 테이블을 보유하여 키보드 액셀러레이터를 구현합니다(예: "새로 만들기"에 Ctrl+N 매핑). 애플리케이션의 디스패처에서는 User32의 입력 메시지를 탐지하고 등록된 액셀러레이터와 일치하는 것이 있는지 확인하는 **TranslateAccelerator**를 호출합니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서는 시스템이 완전히 "구성 가능"하기 때문에, 즉 모든 요소가 키보드 액셀러레이터를 처리하고 사용할 수 있기 때문에 이 방법이 작동하지 않습니다. 입력에 이 2단계 모델을 사용하면 구성 요소가 자체적인 "TranslateAccelerator"를 구현할 수 있습니다.  
  
 이 한 단계를 더 수행 하기 <xref:System.Windows.UIElement> 위해에서는 commandbindings 개념도 소개 합니다. 명령 시스템을 통해 개발자는를 구현 <xref:System.Windows.Input.ICommand>하는 것과 같은 명령 끝점을 기준으로 기능을 정의할 수 있습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 명령 바인딩을 통해 요소가 입력 제스처(예: Ctrl+N)와 명령(예: 새로 만들기) 사이의 매핑을 정의할 수 있습니다. 입력 제스처와 명령 정의는 모두 확장이 가능하며 사용 중에 함께 연결될 수 있습니다. 최종 사용자가 애플리케이션 내에서 사용할 키 바인딩을 사용자 지정하는 작업 등이 간단해집니다.  
  
 항목의 이 시점에서는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 "핵심" 기능, 즉 PresentationCore 어셈블리에 구현된 기능에 초점이 맞춰집니다. 빌드할 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]때 기본 부분 (예: **측정** 및 **정렬**의 레이아웃에 대 한 계약) 및 프레임 워크 조각 (예:와 같은 <xref:System.Windows.Controls.Grid>특정 레이아웃의 구현)을 명확 하 게 구분 하는 것이 바람직한 방법입니다. 성과. 목표는 외부 개발자가 필요한 경우 자체적인 프레임워크를 만들 수 있도록 스택의 아래쪽에 확장 가능성 지점을 제공하는 것이었습니다.  
  
<a name="System_Windows_FrameworkElement"></a>   
## <a name="systemwindowsframeworkelement"></a>System.Windows.FrameworkElement  
 <xref:System.Windows.FrameworkElement>는 두 가지 방법으로 확인할 수 있습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 낮은 계층에 도입되는 하위 시스템에 대한 정책 및 사용자 지정 집합을 소개한다는 것이며, 다른 한 가지는 새로운 하위 시스템 집합을 소개한다는 것입니다.  
  
 에서 <xref:System.Windows.FrameworkElement> 도입 된 기본 정책은 응용 프로그램 레이아웃을 중심으로 합니다. <xref:System.Windows.FrameworkElement>는에 의해 <xref:System.Windows.UIElement> 도입 된 기본 레이아웃 계약을 기반으로 하며 레이아웃 작성자가 일관 된 속성 기반 레이아웃 의미 체계 집합을 쉽게 사용할 수 있게 해 주는 레이아웃 "슬롯"의 개념을 추가 합니다. <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> <xref:System.Windows.FrameworkElement> , ,<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>및 와같은속성은레이아웃컨테이너내에서일관적인동작에서파생된모든구성요소를제공합니다.<xref:System.Windows.FrameworkElement.Margin%2A> <xref:System.Windows.FrameworkElement.MinWidth%2A>  
  
 <xref:System.Windows.FrameworkElement>는의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]핵심 계층에 있는 다양 한 기능에 더 쉽게 API를 노출할 수도 있습니다. 예 <xref:System.Windows.FrameworkElement> 를 들어는 <xref:System.Windows.FrameworkElement.BeginStoryboard%2A> 메서드를 통해 애니메이션에 직접 액세스할 수 있습니다. 는 <xref:System.Windows.Media.Animation.Storyboard> 속성 집합에 대해 여러 애니메이션을 스크립팅 하는 방법을 제공 합니다.  
  
 에서 가장 중요 한 <xref:System.Windows.FrameworkElement> 두 가지는 데이터 바인딩 및 스타일입니다.  
  
 의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 데이터 바인딩 하위 시스템은 응용 프로그램 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]을 만들기 위해 사용 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 하거나 ASP.NET 하는 사용자에 게 비교적 친숙 해야 합니다. 이러한 각 시스템에는 특정 요소에 있는 하나 이상의 속성을 데이터 조각에 바인딩하려고 한다는 것을 간단하게 표현할 수 있는 방법이 있습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 속성 바인딩, 변환 및 목록 바인딩을 완전히 지원합니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서 데이터 바인딩의 가장 흥미로운 기능 중 하나는 새로 도입된 데이터 템플릿입니다. 데이터 템플릿을 사용하면 어떤 데이터 조각을 시각화해야 하는지를 선언적으로 명시할 수 있습니다. 데이터에 바인딩할 수 있는 사용자 지정 사용자 인터페이스를 만드는 대신 역으로, 생성될 디스플레이를 데이터가 결정하도록 할 수 있습니다.  
  
 스타일 지정은 실제로는 데이터 바인딩의 간단한 형태입니다. 스타일 지정을 사용하면 공유된 정의에 있는 속성 집합을 하나 이상의 요소 인스턴스에 바인딩할 수 있습니다. 스타일은 <xref:System.Windows.FrameworkElement.Style%2A> 속성을 설정 하 여 명시적 참조를 통해 요소에 적용 되거나 스타일을 요소의 CLR 형식과 연결 하 여 암시적으로 적용 됩니다.  
  
<a name="System_Windows_Controls_Control"></a>   
## <a name="systemwindowscontrolscontrol"></a>System.Windows.Controls.Control  
 컨트롤의 가장 중요한 기능은 템플릿 설정입니다. WPF의 컴퍼지션 시스템을 유지된 모드 렌더링 시스템으로 생각하는 경우에는 템플릿 설정을 통해 컨트롤이 매개 변수가 있는 선언적 방식으로 렌더링되고 있음을 설명할 수 있습니다. 는 <xref:System.Windows.Controls.ControlTemplate> 컨트롤에서 제공 하는 속성에 대 한 바인딩을 사용 하 여 자식 요소 집합을 만드는 스크립트에 불과합니다.  
  
 <xref:System.Windows.Controls.Control>템플릿 작성자가 컨트롤의 표시를 <xref:System.Windows.Controls.Control.Foreground%2A>사용자 지정 <xref:System.Windows.Controls.Control.Padding%2A>하는 데 사용할 수 있는 몇 가지 스톡 속성 (, <xref:System.Windows.Controls.Control.Background%2A>,)의 이름을 지정 합니다. 컨트롤 구현은 데이터 모델 및 상호 작용 모델을 제공합니다. 상호 작용 모델은 명령 집합(예: 창 닫기)과 입력 제스처에 대한 바인딩(예: 창의 위쪽 모서리에 있는 빨간색 X 클릭)을 정의합니다. 데이터 모델은 상호 작용 모델을 사용자 지정하거나 디스플레이를 사용자 지정하기 위한 속성 집합을 제공합니다. 사용자 지정 대상은 템플릿에 의해 결정됩니다.  
  
 데이터 모델(속성), 상호 작용 모델(명령 및 이벤트) 및 디스플레이 모델(템플릿)이 이렇게 구분됨에 따라 컨트롤의 모양 및 동작을 완전히 사용자 지정할 수 있습니다.  
  
 컨트롤 데이터 모델의 공통적인 측면은 콘텐츠 모델입니다. 와 같은 <xref:System.Windows.Controls.Button>컨트롤을 살펴보면 형식의 <xref:System.Object>"Content" 라는 속성이 있음을 알 수 있습니다. 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ASP.NET에서이 속성은 일반적으로 문자열 이지만 단추에 추가할 수 있는 콘텐츠 형식을 제한 합니다. 단추의 콘텐츠는 간단한 문자열, 복잡한 데이터 개체 또는 전체 요소 트리일 수가 있습니다. 데이터 개체의 경우 데이터 템플릿이 사용되어 디스플레이를 구성합니다.  
  
<a name="Summary"></a>   
## <a name="summary"></a>요약  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 동적인 데이터 중심 프레젠테이션 시스템을 만들 수 있도록 디자인되었습니다. 시스템의 모든 부분은 동작을 구현하는 속성 집합을 통해 개체를 만듭니다. 데이터 바인딩은 시스템의 기초적인 부분이며 모든 계층과 통합됩니다.  
  
 일반 애플리케이션은 디스플레이를 만든 다음 일부 데이터에 바인딩합니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서는 컨트롤에 대한 모든 것과 디스플레이의 모든 측면이 일부 데이터 바인딩 형식에 의해 생성됩니다. 단추 내의 텍스트는 단추 내에 구성된 컨트롤을 만들고 해당 디스플레이를 단추의 콘텐츠 속성에 바인딩하여 표시됩니다.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 기반 응용 프로그램의 개발을 시작하면 매우 친숙하다는 느낌을 받을 것입니다. 사용 하거나 ASP.NET 하 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 는 것과 거의 동일한 방법으로 속성을 설정 하 고, 개체를 사용 하 고, 데이터 바인딩을 설정할 수 있습니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]의 아키텍처를 보다 자세히 살펴 보면 근본적으로 데이터를 응용 프로그램의 핵심 요소로 처리하는 보다 다양한 응용 프로그램을 만들 수 있는 가능성이 있다는 사실을 발견하게 될 것입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.UIElement>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.Threading.DispatcherObject>
- <xref:System.Windows.Input.CommandBinding>
- <xref:System.Windows.Controls.Control>
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [레이아웃](layout.md)
- [애니메이션 개요](../graphics-multimedia/animation-overview.md)
