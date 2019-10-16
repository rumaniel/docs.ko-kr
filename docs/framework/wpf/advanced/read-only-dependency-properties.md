---
title: 읽기 전용 종속성 속성
ms.date: 03/30/2017
helpviewer_keywords:
- dependency properties [WPF], read-only
- read-only dependency properties [WPF]
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
ms.openlocfilehash: aa6893b100311ead74f610dd20f327d130dff74a
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401646"
---
# <a name="read-only-dependency-properties"></a>읽기 전용 종속성 속성
이 항목에서는 기존 읽기 전용 종속성 속성과 사용자 지정 읽기 전용 종속성 속성을 만드는 시나리오 및 방법을 포함하여 읽기 전용 종속성 속성을 설명합니다.  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>필수 구성 요소  
 이 항목에서는 종속성 속성을 구현하는 기본 시나리오와 메타데이터가 사용자 지정 종속성 속성에 적용되는 방법을 이해하고 있다고 가정합니다. 컨텍스트는 [사용자 지정 종속성 속성](custom-dependency-properties.md) 및 [종속성 속성 메타데이터](dependency-property-metadata.md)를 참조하세요.  
  
<a name="existing"></a>   
## <a name="existing-read-only-dependency-properties"></a>기존 읽기 전용 종속성 속성  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 프레임워크에 정의된 일부 종속성 속성은 읽기 전용입니다. 일반적으로 읽기 전용 종속성 속성을 지정하는 이유는 상태 결정에 이러한 속성을 사용해야 하지만 많은 요소가 해당 상태에 영향을 미치는 경우 속성을 해당 상태로 설정하는 것은 사용자 인터페이스 디자인 측면에서 바람직하지 않기 때문입니다. 예를 들어 속성 <xref:System.Windows.UIElement.IsMouseOver%2A> 은 단순히 마우스 입력에서 확인 된 것과 같은 상태입니다. 실제 마우스 입력을 우회하여 프로그래밍 방식으로 이 값을 설정하는 시도는 예측이 불가능하고 이로 인해 불일치가 발생합니다.  
  
 설정이 불가능하기 때문에 읽기 전용 종속성 속성은 정상적으로는 종속성 속성이 솔루션(값, 유효성 검사, 애니메이션, 상속에 직접 스타일 지정 가능한 데이터 바인딩)을 제공하는 많은 시나리오에 적절하지 않습니다. 설정 불가능하지만 읽기 전용 종속성 속성에는 속성 시스템의 종속성 시스템을 통해 지원되는 몇 가지 추가 기능이 있습니다. 가장 중요한 나머지 기능은 읽기 전용 종속성 속성은 속성 트리거로 사용될 수 있다는 것입니다. 일반 CLR (공용 언어 런타임) 속성을 사용 하 여 트리거를 활성화할 수 없습니다. 이 속성은 종속성 속성 이어야 합니다. 앞서 언급 <xref:System.Windows.UIElement.IsMouseOver%2A> 한 속성은 컨트롤에 대 한 스타일을 정의 하는 데 매우 유용할 수 있는 시나리오의 완벽 한 예입니다. 여기에는 배경, 전경 또는 유사 속성 사용자가 컨트롤의 정의 된 영역 위로 마우스를 가져가면 컨트롤이 변경 됩니다. 읽기 전용 종속성 속성의 변경 내용은 속성 시스템의 기본 무효화 프로세스를 통해 검색 및 보고할 수 있고, 실제로 속성 트리거 기능을 내부적으로 지원합니다.  
  
<a name="new"></a>   
## <a name="creating-custom-read-only-dependency-properties"></a>사용자 지정 읽기 전용 종속성 속성 만들기  
 위 섹션에서 읽기 전용 종속성 속성이 많은 일반적인 종속성 속성 시나리오에 적용되지 않는 이유를 확인해야 합니다. 하지만 적절한 시나리오가 있는 경우 자체 읽기 전용 종속성 속성을 만들려고 할 수 있습니다.  
  
 읽기 전용 종속성 속성을 만드는 프로세스의 많은 부분은 [사용자 지정 종속성 속성](custom-dependency-properties.md) 및 [종속성 속성 구현](how-to-implement-a-dependency-property.md) 항목에 설명된 것과 같습니다. 세 가지 중요한 차이점이 있습니다.  
  
- 속성을 등록할 때 속성 등록을 <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A> 위해 일반 <xref:System.Windows.DependencyProperty.Register%2A> 메서드 대신 메서드를 호출 합니다.  
  
- CLR "래퍼" 속성을 구현할 때 래퍼에 설정 된 구현이 없음을 확인 하 여 노출 하는 공용 래퍼에 대 한 읽기 전용 상태의 불일치를 발생 시 키 지 않도록 합니다.  
  
- 읽기 전용 등록 <xref:System.Windows.DependencyPropertyKey> <xref:System.Windows.DependencyProperty>에서 반환 되는 개체는 대신입니다. 이 필드는 멤버로 저장해야 하지만 일반적으로 형식의 public 멤버로 설정하지 않습니다.  
  
 지원하는 private 필드 또는 값이 무엇이든 관계없이 읽기 전용 종속성 속성은 결정한 논리가 무엇이든 이를 사용하여 충분히 쓰기 가능합니다. 그러나 처음에 또는 런타임 논리의 일부로 속성을 설정 하는 가장 간단한 방법은 속성 시스템을 우회 하 고 개인 지원 필드를 직접 설정 하는 대신 속성 시스템의 Api를 사용 하는 것입니다. 특히 형식의 <xref:System.Windows.DependencyObject.SetValue%2A> <xref:System.Windows.DependencyPropertyKey>매개 변수를 허용 하는의 시그니처가 있습니다. 응용 프로그램 논리 내에서 프로그래밍 방식으로이 값을 설정 하는 방법과 위치는 종속성 속성을 처음 등록할 때 <xref:System.Windows.DependencyPropertyKey> 생성 된에 대 한 액세스를 설정 하는 방법에 영향을 줍니다. private로 설정할 수 있는 클래스 내에서 이 논리를 모두 처리할 경우 또는 어셈블리의 다른 부분에서 클래스를 설정해야 하는 경우 이 클래스를 internal로 설정할 수 있습니다. 한 가지 방법은 저장 된 <xref:System.Windows.DependencyObject.SetValue%2A> 속성 값을 변경 해야 함을 클래스 인스턴스에 알리는 관련 이벤트의 클래스 이벤트 처리기 내에서를 호출 하는 것입니다. 또 다른 방법은 등록 하는 동안 쌍을 이루는 <xref:System.Windows.PropertyChangedCallback> 및 <xref:System.Windows.CoerceValueCallback> 콜백을 이러한 속성의 메타 데이터의 일부로 사용 하 여 종속성 속성을 결합 하는 것입니다.  
  
 는 <xref:System.Windows.DependencyPropertyKey> private 이며 코드 외부의 속성 시스템에서 전파 되지 않으므로 읽기 전용 종속성 속성은 읽기-쓰기 종속성 속성 보다 보안을 설정 하는 것이 좋습니다. 읽기-쓰기 종속성 속성의 경우 식별 필드는 명시적 또는 암시적으로 public이므로 속성을 광범위하게 설정할 수 있습니다. 자세한 내용은 [종속성 속성 보안](dependency-property-security.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [종속성 속성 개요](dependency-properties-overview.md)
- [사용자 지정 종속성 속성](custom-dependency-properties.md)
- [스타일 지정 및 템플릿](../controls/styling-and-templating.md)
