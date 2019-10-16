---
title: 속성 값 상속
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [WPF], property values
- value inheritance [WPF]
- properties [WPF], value inheritance
ms.assetid: d7c338f9-f2bf-48ed-832c-7be58ac390e4
ms.openlocfilehash: eb757d039437d9954a2b648c5f758dffa3fee3d2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958358"
---
# <a name="property-value-inheritance"></a>속성 값 상속
속성 값 상속은 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 속성 시스템의 기능입니다. 속성 값 상속을 통해 요소 트리의 자식 요소가 부모 요소에서 특정 속성 값을 얻어 가장 근접한 부모 요소의 아무 곳에서나 설정되었을 때 해당 값을 상속합니다. 부모 요소는 속성 값 상속을 통해 값을 얻었을 수 있으므로 시스템이 완전히 페이지 루트로 되돌아갈 수 있습니다. 속성 값 상속은 기본 속성 시스템 동작이 아닙니다. 속성이 자식 요소에서 속성 값 상속을 시작하게 하려면 특정 메타데이터 설정을 사용하여 속성을 설정해야 합니다.  

<a name="Property_Value_Inheritance_is_Containment_Inheritance"></a>   
## <a name="property-value-inheritance-is-containment-inheritance"></a>속성 값 상속은 포함 상속임  
 여기서 "상속"이라는 용어는 파생 클래스가 기본 클래스에서 멤버 정의를 상속하는 형식 및 일반적인 개체 지향 프로그램의 컨텍스트에서 사용하는 상속과 완전히 같은 개념은 아닙니다. 해당 상속의 의미는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서도 유효합니다. 다양한 기본 클래스에 정의되는 속성은 요소로 사용될 때 파생 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 클래스의 특성으로 표시되고 코드의 멤버로 표시됩니다. 속성 값 상속의 경우 특히 요소 트리 내의 부모-자식 관계에 따라 요소 간에 속성 값을 상속하는 방식이 영향을 미칩니다. 해당 요소 트리는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 태그에서 애플리케이션을 정의할 때 요소 내부에 다른 요소를 중첩할 경우 대부분 직접 표시됩니다. 다른 개체의 지정된 컬렉션에 개체를 추가하여 개체 트리를 프로그래밍 방식으로 만들 수도 있고 속성 값 상속은 런타임에 완료된 트리에서 동일한 방식으로 수행됩니다.  
  
<a name="Practical_Applications_of_Property_Value_Inheritance"></a>   
## <a name="practical-applications-of-property-value-inheritance"></a>속성 값 상속의 실제 애플리케이션  
 Api [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에는 속성 상속이 설정 된 여러 속성이 포함 되어 있습니다. 일반적으로 이러한 속성은 페이지당 한 번만 속성을 설정하는 것이 적절하지만 해당 속성이 기본 요소 클래스 중 하나의 멤버이기도 하므로 대부분의 자식 요소에도 존재하는 속성을 포함합니다. 예를 들어 속성 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 은 이동 된 콘텐츠가 페이지에 표시 되 고 정렬 되어야 하는 방향을 제어 합니다. 일반적으로 모든 자식 요소에서 텍스트 흐름 개념을 일관성 있게 처리하려고 합니다. 어떤 이유로 사용자 또는 환경 작업에 의해 요소 트리의 몇몇 수준에서 다시 설정된 흐름 방향은 일반적으로 전체적으로 다시 설정되어야 합니다. <xref:System.Windows.FrameworkElement.FlowDirection%2A> 속성이 상속 되 면 응용 프로그램의 각 페이지에 대 한 프레젠테이션 요구를 포함 하는 요소 트리의 수준에서 값을 한 번만 설정 하거나 다시 설정 해야 합니다. 초기 기본값도 이 방식으로 상속됩니다. 속성 값 상속 모델에서는 드물지만 다양한 흐름 방향을 의도적으로 포함하는 경우 개별 요소가 값을 다시 설정할 수 있습니다.  
  
<a name="Making_a_Custom_Property_Inheritable"></a>   
## <a name="making-a-custom-property-inheritable"></a>사용자 지정 속성을 상속 가능으로 설정  
 사용자 지정 속성의 메타데이터를 변경하여 자체 사용자 지정 속성을 상속 가능으로 설정할 수도 있습니다. 하지만 속성을 상속 가능으로 지정할 경우 성능상 몇 가지 사항을 고려해야 합니다. 속성에 설정된 로컬 값이 없거나 스타일, 템플릿 또는 데이터 바인딩을 통해 얻은 값이 없는 경우 상속 가능 속성은 논리 트리에서 모든 자식 요소에 할당된 속성 값을 제공합니다.  
  
 속성을 값 상속에 참여하도록 설정하려면 [연결된 속성 등록](how-to-register-an-attached-property.md)에 설명된 대로 사용자 지정 연결된 속성을 만듭니다. 메타 데이터 (<xref:System.Windows.FrameworkPropertyMetadata>)를 사용 하 여 속성을 등록 하 고 해당 메타 데이터 내의 옵션 설정에서 "Inherits" 옵션을 지정 합니다. 또한 속성에 설정된 기본값이 있는지 확인합니다. 이제 이 값이 상속되기 때문입니다. 속성을 연결된 속성으로 등록하더라도 "연결되지 않은" 종속성 속성의 경우처럼 소유자 형식에서 get/set 액세스에 대한 속성 “래퍼”를 만들어야 할 수 있습니다. 이 작업을 수행한 후에는 소유자 형식이 나 파생 형식에 대 한 직접 속성 래퍼를 사용 하 여 상속 가능한 속성을 설정 하거나 연결 된 속성 구문을 <xref:System.Windows.DependencyObject>사용 하 여 설정할 수 있습니다.  
  
 연결 된 속성은 전역 속성과 개념적으로 유사 합니다. 에서 값을 확인 <xref:System.Windows.DependencyObject> 하 고 유효한 결과를 가져올 수 있습니다. 연결 된 속성에 대 한 일반적인 시나리오는 자식 요소에서 속성 값을 설정 하는 것입니다. 해당 하는 속성은 항상 각 요소<xref:System.Windows.DependencyObject>에대한연결된속성으로암시적으로존재하는연결된속성인경우더효과적입니다.  
  
> [!NOTE]
> 속성 값 상속은 연결된 종속성 속성에도 적용되는 것처럼 보일 수 있지만 런타임 트리의 특정 요소 경계를 통한 연결되지 않은 속성에 대한 상속 동작은 정의되지 않습니다. 항상 사용 하 여 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 지정 하는 속성을 등록 하려면 <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> 메타 데이터에서입니다.  
  
<a name="InheritanceContext"></a>   
## <a name="inheriting-property-values-across-tree-boundaries"></a>트리 경계를 넘어 속성 값 상속  
 속성 상속은 요소 트리를 통과하는 방식으로 수행됩니다. 이 트리는 일반적으로 논리 트리와 비슷합니다. 그러나와 <xref:System.Windows.Media.Brush>같이 요소 트리를 정의 하는 태그에 WPF 핵심 수준 개체를 포함할 때마다 불연속 논리 트리를 만들었습니다. 논리적 트리는 WPF 프레임 워크 수준 개념 이므로 진정한 <xref:System.Windows.Media.Brush>논리적 트리는를 통해 개념적으로 확장 되지 않습니다. 의 <xref:System.Windows.LogicalTreeHelper>메서드를 사용 하는 경우 결과에 반영 된이를 확인할 수 있습니다. 그러나 상속 가능한 속성이 연결 된 속성으로 등록 되 고 의도적인 상속 차단 경계 (예: <xref:System.Windows.Controls.Frame>)가없는한,속성값상속은논리적트리에서이차이를연결하고,상속된값은계속전달할수있습니다.)가 발견 되었습니다.  
  
## <a name="see-also"></a>참고자료

- [종속성 속성 메타데이터](dependency-property-metadata.md)
- [연결된 속성 개요](attached-properties-overview.md)
- [종속성 속성 값 우선 순위](dependency-property-value-precedence.md)
