---
title: 기본 요소 개요
ms.date: 03/30/2017
helpviewer_keywords:
- base elements [WPF]
ms.assetid: 2c997092-72c6-4767-bc84-74267f4eee72
ms.openlocfilehash: 3dfcaaf040a766e07eb46a0b943b7e023564fa1c
ms.sourcegitcommit: 83ecdf731dc1920bca31f017b1556c917aafd7a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67859952"
---
# <a name="base-elements-overview"></a>기본 요소 개요
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 클래스에는 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 설명서에서 일반적으로 기본 요소 클래스라고 하는 네 가지 클래스에서 파생된 클래스가 많습니다. 이러한 클래스는 <xref:System.Windows.UIElement>, <xref:System.Windows.FrameworkElement>를 <xref:System.Windows.ContentElement>, 및 <xref:System.Windows.FrameworkContentElement>합니다. 합니다 <xref:System.Windows.DependencyObject> 둘 다의 공통 기본 클래스 이므로 클래스와도 관련 <xref:System.Windows.UIElement> 및 <xref:System.Windows.ContentElement>  

<a name="base_apis"></a>   
## <a name="base-element-apis-in-wpf-classes"></a>WPF 클래스의 기본 요소 API  
 둘 다 <xref:System.Windows.UIElement> 하 고 <xref:System.Windows.ContentElement> 에서 파생 된 <xref:System.Windows.DependencyObject>, 약간 다른 경로 통해. 이 수준에서 분할 방법을 사용 하 여 처리를 <xref:System.Windows.UIElement> 또는 <xref:System.Windows.ContentElement> 사용자 인터페이스 및 응용 프로그램에서 사용 목적 무엇에 사용 됩니다. <xref:System.Windows.UIElement> 역시 <xref:System.Windows.Media.Visual> 내부 하위 수준 그래픽 지원을 노출 하는 클래스는 해당 클래스 계층 구조는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]합니다. <xref:System.Windows.Media.Visual> 독립적인 직사각형 화면 영역을 정의 하 여 렌더링 프레임 워크를 제공 합니다. 실제로 <xref:System.Windows.UIElement> 대형 개체 모델을 지 원하는 요소 렌더링 하기 위한 것 이며 레이아웃 영역 직사각형 화면 영역으로 표현할 수 있는 콘텐츠 모델은 더 개방적 일 다른 있도록을입니다 요소의 조합을 나타냅니다. <xref:System.Windows.ContentElement> 파생 되지 않습니다 <xref:System.Windows.Media.Visual>;는 해당 모델을 <xref:System.Windows.ContentElement> 판독기 또는 다음 요소를 해석 및 전체를 생성 하는 뷰어와 같은 다른 작업에 의해 사용할 수 <xref:System.Windows.Media.Visual> 에 대 한 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 사용할 합니다. 특정 <xref:System.Windows.UIElement> 클래스 콘텐츠 호스트는: 하나 이상의 호스팅과 렌더링을 제고 <xref:System.Windows.ContentElement> 클래스 (<xref:System.Windows.Controls.DocumentViewer> 이러한 클래스의 예로). <xref:System.Windows.ContentElement> 다소 작은 개체 모델을 사용 하 여 요소에 대 한 기본 클래스와는 더 많이 처리 텍스트, 정보 또는 문서는 콘텐츠 내에서 호스팅될 수로 사용 됩니다.는 <xref:System.Windows.UIElement>합니다.  
  
### <a name="framework-level-and-core-level"></a>프레임워크 수준 및 코어 수준  
 <xref:System.Windows.UIElement> 에 대 한 기본 클래스로 사용 됩니다 <xref:System.Windows.FrameworkElement>, 및 <xref:System.Windows.ContentElement> 에 대 한 기본 클래스로 사용 됩니다 <xref:System.Windows.FrameworkContentElement>합니다. 이 다음 수준의 클래스에 대 한 원인은 Api PresentationCore 및 PresentationFramework 어셈블리 간에 분할 되는 방법에 기존이 나누기를 사용 하 여 WPF 프레임 워크 수준에서 분리 된 WPF 코어 수준을 지원 하도록 합니다. WPF 프레임워크 수준은 프레젠테이션을 위한 레이아웃 관리자의 구현을 포함하여 기본 애플리케이션 요구 사항을 충족하는 보다 완벽한 솔루션을 제공합니다. WPF 코어 수준은 추가 어셈블리의 오버헤드 없이 대부분의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용할 수 있습니다. 이러한 구별 수준 매우 드물게 가장 일반적인 응용 프로그램 개발 시나리오에 대 한 문제 및 일반적을 고려 하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 전체적으로 Api 및 WPF 프레임 워크 수준과 WPF 코어 간의 차이점을 수준입니다. 전체 솔루션에 이미 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 컴퍼지션 및 레이아웃 구현이 있는 경우와 같이 애플리케이션 디자인에서 WPF 프레임워크 수준 기능의 실질적인 상당한 부분을 대체하도록 선택하는 경우에는 이러한 수준 구분에 대해 알고 있어야 합니다.  
  
<a name="subclassing_elements"></a>   
## <a name="choosing-which-element-to-derive-from"></a>파생될 요소 선택  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]을 확장하는 사용자 지정 클래스를 만드는 가장 실질적인 방법은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 클래스 중 하나에서 기존 클래스 계층 구조를 통해 필요한 기능을 가능한 많이 얻을 수 있는 클래스가 파생되는 것입니다. 이 섹션에서는 상속할 클래스를 결정하는 데 도움이 되는 가장 중요한 세 가지 요소 클래스와 함께 제공되는 기능을 나열합니다.  
  
 컨트롤을 구현 하는 경우는 아주에서 파생 시키기 위한 가장 일반적인 이유 중 하나를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 클래스 할 또는 실제 컨트롤, 컨트롤 패밀리 기본 클래스는 클래스에서 파생에서 최소를 <xref:System.Windows.Controls.Control> 기본 클래스입니다. 몇 가지 지침과 실제 예제는 [컨트롤 제작 개요](../controls/control-authoring-overview.md)를 참조하세요.  
  
 컨트롤을 만들지 않고 계층 구조의 더 높은 수준에 있는 클래스에서 파생되어야 하는 경우 다음 섹션이 각 기본 요소 클래스에 정의된 특성에 대한 지침으로 사용됩니다.  
  
 파생 된 클래스를 만든 경우 <xref:System.Windows.DependencyObject>를 상속 하는 다음 기능을 합니다.  
  
- <xref:System.Windows.DependencyObject.GetValue%2A> 및 <xref:System.Windows.DependencyObject.SetValue%2A> 지원 및 일반 속성 시스템 지원 합니다.  
  
- 종속성 속성 및 종속성 속성으로 구현되는 연결된 속성을 사용할 수 있는 기능  
  
 파생 된 클래스를 만들면 <xref:System.Windows.UIElement>, 그 외에에서 제공 하는 다음 기능이 상속 <xref:System.Windows.DependencyObject>:  
  
- 애니메이션 속성 값에 대한 기본 지원 - 자세한 내용은 [애니메이션 개요](../graphics-multimedia/animation-overview.md)를 참조하세요.  
  
- 기본 입력 이벤트 지원 및 명령 지원 - 자세한 내용은 [입력 개요](input-overview.md) 및 [명령 개요](commanding-overview.md)를 참조하세요.  
  
- 레이아웃 시스템에 정보를 제공하도록 재정의될 수 있는 가상 메서드  
  
 파생 된 클래스를 만들면 <xref:System.Windows.FrameworkElement>, 그 외에에서 제공 하는 다음 기능이 상속 <xref:System.Windows.UIElement>:  
  
- 스타일 지정 및 스토리보드 지원 - 자세한 내용은 <xref:System.Windows.Style> 하 고 [Storyboard 개요](../graphics-multimedia/storyboards-overview.md)합니다.  
  
- 데이터 바인딩 지원 - 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요.  
  
- 동적 리소스 참조 지원 - 자세한 내용은 [XAML 리소스](xaml-resources.md)를 참조하세요.  
  
- 속성 값 상속 지원 및 프레임워크 서비스(예: 데이터 바인딩, 스타일 또는 레이아웃의 프레임워크 구현)에 대한 속성 조건을 보고하는 데 도움이 되는 메타데이터의 기타 플래그 - 자세한 내용은 [프레임워크 속성 메타데이터](framework-property-metadata.md)를 참조하세요.  
  
- 논리 트리의 개념 - 자세한 내용은 [WPF의 트리](trees-in-wpf.md)를 참조하세요.  
  
- 레이아웃 시스템의 실제 WPF 프레임 워크 수준 구현에 대 한 지원을 포함 하는 <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> 레이아웃에 영향을 해당 속성을 검색할 수 있는 재정의 변경 합니다.  
  
 파생 된 클래스를 만들면 <xref:System.Windows.ContentElement>, 그 외에에서 제공 하는 다음 기능이 상속 <xref:System.Windows.DependencyObject>:  
  
- 애니메이션 지원 - 자세한 내용은 [애니메이션 개요](../graphics-multimedia/animation-overview.md)를 참조하세요.  
  
- 기본 입력 이벤트 지원 및 명령 지원 - 자세한 내용은 [입력 개요](input-overview.md) 및 [명령 개요](commanding-overview.md)를 참조하세요.  
  
 파생 된 클래스를 만들면 <xref:System.Windows.FrameworkContentElement>, 그 외에 제공한 다음 기능을 얻을 수 <xref:System.Windows.ContentElement>:  
  
- 스타일 지정 및 스토리보드 지원 - 자세한 내용은 <xref:System.Windows.Style> 하 고 [애니메이션 개요](../graphics-multimedia/animation-overview.md)합니다.  
  
- 데이터 바인딩 지원 - 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요.  
  
- 동적 리소스 참조 지원 - 자세한 내용은 [XAML 리소스](xaml-resources.md)를 참조하세요.  
  
- 속성 값 상속 지원 및 프레임워크 서비스(예: 데이터 바인딩, 스타일 또는 레이아웃의 프레임워크 구현)에 대한 속성 조건을 보고하는 데 도움이 되는 메타데이터의 기타 플래그 - 자세한 내용은 [프레임워크 속성 메타데이터](framework-property-metadata.md)를 참조하세요.  
  
- 레이아웃 시스템 수정에 대 한 액세스를 상속 하지 않습니다 (같은 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>). 레이아웃 시스템 구현은 에서만 사용할 <xref:System.Windows.FrameworkElement>합니다. 그러나 상속을 <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> 레이아웃 및 모든 콘텐츠 호스트를 보고 하는 속성에 대 한 변경 내용을 검색할 수 있는 재정의 합니다.  
  
 컨텐츠 모델은 다양한 클래스에서 사용할 수 있도록 문서화되어 있습니다. 클래스의 콘텐츠 모델은 파생될 적절한 클래스를 찾을 때 고려해야 할 요소입니다. 자세한 내용은 [WPF 콘텐츠 모델](../controls/wpf-content-model.md)을 참조하세요.  
  
<a name="other_base_classes"></a>   
## <a name="other-base-classes"></a>기타 기본 클래스  
  
### <a name="dispatcherobject"></a>DispatcherObject  
 <xref:System.Windows.Threading.DispatcherObject> 에 대 한 지원을 제공 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 스레딩 모델 및에 대 한 모든 개체를 만들 수 있습니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 와 연결할 응용 프로그램을 <xref:System.Windows.Threading.Dispatcher>입니다. 파생 되지 않은 경우에 <xref:System.Windows.UIElement>하십시오 <xref:System.Windows.DependencyObject>, 또는 <xref:System.Windows.Media.Visual>에서 파생 하는 것이 좋습니다 <xref:System.Windows.Threading.DispatcherObject> 이 스레딩 모델을 지원 하려면. 자세한 내용은 [스레딩 모델](threading-model.md)을 참조하세요.  
  
### <a name="visual"></a>시각적 개체  
 <xref:System.Windows.Media.Visual> 일반적으로 대략 직사각형 영역에 시각적으로 표현 필요한 2D 개체의 개념을 구현 합니다. 실제 렌더링을 <xref:System.Windows.Media.Visual> (이 자체 포함) 다른 클래스에서 발생 하지만 <xref:System.Windows.Media.Visual> 클래스에는 다양 한 수준에서 렌더링 프로세스에서 사용 되는 알려진된 형식을 제공 합니다. <xref:System.Windows.Media.Visual> 적중 테스트를 구현 하지만 적중 테스트 결과 보고 하는 이벤트를 노출 하지 않습니다 (이러한 <xref:System.Windows.UIElement>). 자세한 내용은 [시각적 계층 프로그래밍](../graphics-multimedia/visual-layer-programming.md)을 참조하세요.  
  
### <a name="freezable"></a>Freezable  
 <xref:System.Windows.Freezable> 변경할 수 없는 개체는 필수 또는 성능상의 이유로 필요한 경우 개체의 복사본을 생성 하는 방법을 제공 하 여 변경할 수 있는 개체의 불변성을 시뮬레이션 합니다. <xref:System.Windows.Freezable> 형식은 일반적으로 특정 애니메이션 뿐만 아니라 기 하 도형 및 브러시와 같은 그래픽 요소를 제공 합니다. 특히를 <xref:System.Windows.Freezable> 아닙니다를 <xref:System.Windows.Media.Visual>; 하위 속성이 포함 되는 속성을 포함할 수 있습니다 때는 <xref:System.Windows.Freezable> 다른 개체의 속성 값이 입력에 적용 됩니다 이러한 하위 속성이 렌더링에 영향을 줄 수 있습니다. 자세한 내용은 [Freezable 개체 개요](freezable-objects-overview.md)를 참조하세요.  
  
 <xref:System.Windows.Media.Animation.Animatable>  
  
 <xref:System.Windows.Media.Animation.Animatable> 가 <xref:System.Windows.Freezable> 특히 애니메이션 컨트롤 계층과 일부 유틸리티 멤버 현재 애니메이션이 적용 된 속성이 구별할 수 있도록에서 추가 되는 속성과 클래스를 파생 합니다.  
  
### <a name="control"></a>Control  
 <xref:System.Windows.Controls.Control> 컨트롤 또는 구성 요소는 기술에 따라 다양 하 게 표현 되는 개체의 형식에 대 한 의도 한 기본 클래스가입니다. 일반적으로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 클래스는 UI 컨트롤을 직접 나타내거나 컨트롤 컴퍼지션에 밀접하게 참여하는 클래스입니다. 기본 기능이 있는 <xref:System.Windows.Controls.Control> 컨트롤 템플릿 기능입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Control>
- [종속성 속성 개요](dependency-properties-overview.md)
- [컨트롤 제작 개요](../controls/control-authoring-overview.md)
- [WPF 아키텍처](wpf-architecture.md)
