---
title: 프레임워크 속성 메타데이터
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WPF], framework properties
- framework property metadata [WPF]
ms.assetid: 9962f380-b885-4b61-a62e-457397083fea
ms.openlocfilehash: c08cf28880d86331e3b561f1749333d401ba903e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964212"
---
# <a name="framework-property-metadata"></a>프레임워크 속성 메타데이터
프레임워크 속성 메타데이터는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 아키텍처의 WPF 프레임워크 수준에 있는 것으로 간주되는 개체 요소의 속성용으로 보고됩니다. 일반적으로 WPF 프레임 워크 수준 지정에는 렌더링, 데이터 바인딩 및 속성 시스템 구체화와 같은 기능이 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프레젠테이션 api 및 실행 파일에 의해 처리 됩니다. 이러한 시스템에서 프레임워크 속성 메타데이터를 쿼리하여 특정 요소 속성의 기능별 특성을 결정합니다.  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>필수 구성 요소  
 이 항목에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 클래스에서 기존 종속성 속성의 소비자 관점에서 종속성 속성을 이해하고 [종속성 속성 개요](dependency-properties-overview.md)를 읽었다고 가정합니다. [종속성 속성 메타데이터](dependency-property-metadata.md)도 읽어야 합니다.  
  
<a name="What_Is_Communicated_by_Framework_Property"></a>   
## <a name="what-is-communicated-by-framework-property-metadata"></a>프레임워크 속성 메타데이터로 통신하는 내용  
 프레임워크 속성 메타데이터는 다음 범주로 구분할 수 있습니다.  
  
- 요소에 영향을 주는 보고 레이아웃 속성<xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A>( <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsRender%2A>,) 속성이 각 측면에 영향을 주는 경우 메타 데이터에서 이러한 플래그를 설정할 수 있으며, 클래스의 메서드 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 를  /  <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 구현 하 여 특정 렌더링 동작 및 정보를 레이아웃에 제공할 수도 있습니다. 컴퓨터. 일반적으로 이러한 구현에서는 해당 레이아웃 속성이 속성 메타데이터에서 참인 종속성 속성의 속성 무효화를 확인하고 해당 무효화만 새로운 레이아웃 전달을 요청해야 합니다.  
  
- 요소의 부모 요소에 영향을 주는 보고 레이아웃 속성 (<xref:System.Windows.FrameworkPropertyMetadata.AffectsParentArrange%2A>,) <xref:System.Windows.FrameworkPropertyMetadata.AffectsParentMeasure%2A> 이러한 플래그를 기본적으로 설정 하는 몇 가지 <xref:System.Windows.Documents.FixedPage.Left%2A?displayProperty=nameWithType> 예 <xref:System.Windows.Documents.Paragraph.KeepWithNext%2A?displayProperty=nameWithType>는 및입니다.  
  
- <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>. 기본적으로 종속성 속성은 값을 상속하지 않습니다. <xref:System.Windows.FrameworkPropertyMetadata.OverridesInheritanceBehavior%2A>상속의 경로를 시각적 트리로 이동할 수 있도록 하 여 일부 컨트롤 작성 시나리오에 필요 합니다.  
  
    > [!NOTE]
    > 속성 값 컨텍스트에서 “상속”이라는 용어는 종속성 속성에 특정한 것입니다. 즉, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 속성 시스템의 WPF 프레임워크 수준 기능때문에 자식 요소가 부모 요소에서 실제 종속성 속성 값을 상속할 수 있습니다. 파생된 유형을 통한 멤버 상속 및 관리된 코드 유형과는 직접적인 관련이 없습니다. 자세한 내용은 [속성 값 상속](property-value-inheritance.md)을 참조하십시오.  
  
- 보고 데이터 바인딩 특성 (<xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A>, <xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A>) 기본적으로 프레임워크의 종속성 속성은 단방향 바인딩 동작을 통한 데이터 바인딩을 지원합니다. 데이터 바인딩을 사용 하지 않도록 설정할 수 있습니다 .이는 유연 하 고 확장 가능 하기 때문에 기본 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] api에는 이러한 속성에 대 한 많은 예가 없다는 것입니다. 구성 요소 부분 (<xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> 예:)에서 컨트롤의 동작을 결합 하는 속성에 대 한 양방향 기본값을 포함 하도록 바인딩을 설정 하거나 양방향 바인딩이<xref:System.Windows.Controls.TextBox.Text%2A> 사용자에 게 공통적이 고 예상 되는 시나리오인 경우를 예로 들 수 있습니다. 데이터 바인딩 관련 메타데이터를 변경하면 기본값에만 영향을 미칩니다. 바인딩별 변경에서는 해당 기본값을 항상 변경할 수 있습니다. 바인딩 모드와 일반적인 바인딩에 대한 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요.  
  
- 속성이 저널링을 지 원하는 응용 프로그램 또는 서비스에 의해 저널링 되어야 하는지<xref:System.Windows.FrameworkPropertyMetadata.Journal%2A>여부를 보고 합니다 (). 일반 요소에는 기본적으로 저널링을 사용하지 않지만, 특정 사용자 입력 컨트롤에 대해서는 선택적으로 사용합니다. 이 속성은 저널링의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 구현을 포함하여 저널링 서비스를 통해 읽어야 하며, 일반적으로 탐색 단계 간에 지속되어야 하는 목록의 사용자 선택 항목과 같은 사용자 컨트롤에 설정됩니다. 저널에 대한 자세한 내용은 [탐색 개요](../app-development/navigation-overview.md)를 참조하세요.  
  
<a name="Reading_FrameworkPropertyMetadata"></a>   
## <a name="reading-frameworkpropertymetadata"></a>FrameworkPropertyMetadata 읽기  
 위에서 연결 된 각 속성은가 직접 기본 클래스 <xref:System.Windows.FrameworkPropertyMetadata> <xref:System.Windows.UIPropertyMetadata>에 추가 하는 특정 속성입니다. 이러한 각 속성은 기본적으로 `false`입니다. 이러한 속성의 값을 알고 있는 속성에 대 한 메타 데이터 요청은 반환 된 메타 데이터를로 <xref:System.Windows.FrameworkPropertyMetadata>캐스팅 한 다음 필요에 따라 개별 속성의 값을 확인 하는 것이 중요 합니다.  
  
<a name="Specifying_Metadata"></a>   
## <a name="specifying-metadata"></a>메타데이터 지정  
 새 종속성 속성 등록에 메타 데이터를 적용 하기 위해 새 메타 데이터 인스턴스를 만들 때 사용할 메타 데이터 클래스를 선택할 수 있습니다. 기본 <xref:System.Windows.PropertyMetadata> 클래스 또는 파생 클래스 ( <xref:System.Windows.FrameworkPropertyMetadata>예:)를 선택할 수 있습니다. 일반적으로 속성에 속성 <xref:System.Windows.FrameworkPropertyMetadata> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시스템과 상호 작용이 있고 레이아웃 및 데이터 바인딩과 같은 함수를 사용 하는 경우 특히를 사용 해야 합니다. 보다 정교한 시나리오를 위한 또 다른 옵션은에서 <xref:System.Windows.FrameworkPropertyMetadata> 파생 하 여 해당 멤버에 전달 된 추가 정보를 사용 하 여 사용자 고유의 메타 데이터 보고 클래스를 만드는 것입니다. 또는 또는 <xref:System.Windows.PropertyMetadata> <xref:System.Windows.UIPropertyMetadata> 를 사용 하 여 구현 기능에 대 한 지원 수준을 통신할 수 있습니다.  
  
 기존 속성<xref:System.Windows.DependencyProperty.AddOwner%2A> 또는 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 를 호출 하는 경우에는 항상 원래 등록에서 사용 하는 메타 데이터 형식으로를 재정의 해야 합니다.  
  
 <xref:System.Windows.FrameworkPropertyMetadata> 인스턴스를 만드는 경우 다음과 같은 두 가지 방법으로 프레임 워크 속성 특성을 전달 하는 특정 속성의 값으로 해당 메타 데이터를 채울 수 있습니다.  
  
1. 매개 변수 <xref:System.Windows.FrameworkPropertyMetadata> 를 `flags` 허용 하는 생성자 시그니처를 사용 합니다. 이 매개 변수는 <xref:System.Windows.FrameworkPropertyMetadataOptions> 열거형 플래그의 원하는 모든 조합 값으로 채워야 합니다.  
  
2. `flags` 매개 변수 없이 서명 중 하나를 사용 하 고 원하는 각 특성 변경에 대해 각 <xref:System.Windows.FrameworkPropertyMetadata> 보고 `true` 부울 속성을로 설정 합니다. 이 작업을 수행하는 경우 이 종속성 속성이 있는 요소를 생성하기 전에 이러한 속성을 설정해야 합니다. `flags` 매개 변수를 방지하는 동작을 허용하기 위해 부울 속성은 읽기-쓰기가 되며 여전히 메타데이터를 채우지만, 속성을 사용하기 전에 메타데이터를 적절하게 봉인해야 합니다. 따라서 메타데이터를 요청한 후에 속성을 설정하려는 것은 올바른 작업이 아닙니다.  
  
<a name="Framework_Property_Metadata_Merge_Behavior"></a>   
## <a name="framework-property-metadata-merge-behavior"></a>프레임워크 속성 메타데이터 병합 동작  
 프레임워크 속성 메타데이터를 재정의할 때, 여러 다른 메타데이터 특성을 병합하거나 대체합니다.  
  
- <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>이 병합 됩니다. 새 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>를 추가 하는 경우 해당 콜백은 메타 데이터에 저장 됩니다. 재정의에를 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 지정 하지 않는 경우의 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 값은 메타 데이터에서 지정 된 가장 가까운 상위 항목에서 참조로 승격 됩니다.  
  
- 에 대 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 한 실제 속성 시스템 동작은 계층 구조에 있는 모든 메타 데이터 소유자에 대 한 구현이 속성 시스템에 의해 실행 되 고 가장 많이 파생 된 클래스의 콜백이 되기 때문에 테이블에 추가 됩니다. 먼저 호출 됩니다. 상속된 콜백은 한 번만 실행되며, 메타데이터에 해당 콜백을 둔 클래스가 소유하는 것으로 계산됩니다.  
  
- <xref:System.Windows.PropertyMetadata.DefaultValue%2A>이 대체 됩니다. 재정의에를 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 지정 하지 않는 경우의 <xref:System.Windows.PropertyMetadata.DefaultValue%2A> 값은 메타 데이터에서 지정 된 가장 가까운 상위 항목에서 나옵니다.  
  
- <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>구현은 대체 됩니다. 새 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>를 추가 하는 경우 해당 콜백은 메타 데이터에 저장 됩니다. 재정의에를 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 지정 하지 않는 경우의 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 값은 메타 데이터에서 지정 된 가장 가까운 상위 항목에서 참조로 승격 됩니다.  
  
- 속성 시스템 동작은 즉시 메타 데이터 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 의만 호출 된다는 것입니다. 계층의 다른 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 구현에 대 한 참조는 유지 되지 않습니다.  
  
- 열거형의 <xref:System.Windows.FrameworkPropertyMetadataOptions> 플래그는 비트 or 연산으로 결합 됩니다.  을 지정 <xref:System.Windows.FrameworkPropertyMetadataOptions>하는 경우 원래 옵션을 덮어쓰지 않습니다.  옵션을 변경 하려면에 <xref:System.Windows.FrameworkPropertyMetadata>해당 하는 속성을 설정 합니다. 예를 들어 <xref:System.Windows.FrameworkPropertyMetadata> 원래 개체가 <xref:System.Windows.FrameworkPropertyMetadataOptions.NotDataBindable?displayProperty=nameWithType> 플래그를 설정 하는 경우를로 `false`설정 <xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A?displayProperty=nameWithType> 하 여 변경할 수 있습니다.  
  
 이 동작은에 의해 <xref:System.Windows.FrameworkPropertyMetadata.Merge%2A>구현 되며 파생 된 메타 데이터 클래스에서 재정의할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.DependencyProperty.GetMetadata%2A>
- [종속성 속성 메타데이터](dependency-property-metadata.md)
- [종속성 속성 개요](dependency-properties-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
