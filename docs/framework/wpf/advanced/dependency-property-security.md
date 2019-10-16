---
title: 종속성 속성 보안
ms.date: 03/30/2017
helpviewer_keywords:
- wrappers [WPF], access
- wrappers [WPF], security
- dependency properties [WPF], security
- security [WPF], wrappers
- validation [WPF], dependency properties
- dependency properties [WPF], access
- security [WPF], dependency properties
ms.assetid: d10150ec-90c5-4571-8d35-84bafa2429a4
ms.openlocfilehash: d9dd9306980b80f7845c10e8c0ccb59f29821245
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940834"
---
# <a name="dependency-property-security"></a>종속성 속성 보안
종속성 속성은 일반적으로 public 속성으로 간주됩니다. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 속성 시스템의 특성으로 인해 종속성 속성 값에 대한 보안을 보장할 수 없습니다.  

<a name="AccessSecurity"></a>   
## <a name="access-and-security-of-wrappers-and-dependency-properties"></a>래퍼 및 종속성 속성의 액세스 및 보안  
 일반적으로 종속성 속성은 인스턴스에서 속성을 가져오거나 설정 하는 과정을 간소화 하는 "래퍼" CLR (공용 언어 런타임) 속성을 사용 하 여 구현 됩니다. 그러나 래퍼는 실질적으로 종속성 속성과 상호 작용할 때 사용 되 <xref:System.Windows.DependencyObject.GetValue%2A> 는 <xref:System.Windows.DependencyObject.SetValue%2A> 기본 및 정적 호출을 구현 하는 편리한 메서드입니다. 다른 방법으로 생각 하면 속성은 전용 필드가 아니라 종속성 속성에 의해 지원 되는 CLR (공용 언어 런타임) 속성으로 노출 됩니다. 래퍼에 적용되는 보안 메커니즘은 속성 시스템 동작 및 기본 종속성 속성의 액세스와 관련이 없습니다. 래퍼에 대 한 보안 요구를 설정 하면 편의 메서드를 사용 하는 것만 방지 되며 또는 <xref:System.Windows.DependencyObject.GetValue%2A> <xref:System.Windows.DependencyObject.SetValue%2A>에 대 한 호출을 차단 하지는 않습니다. 마찬가지로 래퍼에 보호된 액세스 또는 개인 액세스 수준을 적용해도 효과적인 보안을 제공하지는 않습니다.  
  
 사용자 고유의 종속성 속성을 작성 하는 경우 해당 저장소로 인해 호출자가 해당 <xref:System.Windows.DependencyProperty> 속성의 실제 액세스 수준에 대 한 잘못 된 정보를 얻지 못하도록 래퍼 및 식별자 필드를 public 멤버로 선언 해야 합니다. 종속성 속성으로 구현 됩니다.  
  
 사용자 지정 종속성 속성의 경우 속성을 읽기 전용 종속성 속성으로 등록할 수 있으며,이는 해당 속성 <xref:System.Windows.DependencyPropertyKey> 에 대 한 참조를 보유 하지 않는 사용자가 속성을 설정 하는 것을 방지 하는 효과적인 방법을 제공 합니다. 자세한 내용은 [읽기 전용 종속성 속성](read-only-dependency-properties.md)을 참조하세요.  
  
> [!NOTE]
> <xref:System.Windows.DependencyProperty> 식별자 필드 private를 선언 하는 것은 사용할 수 없으며, 사용자 지정 클래스의 즉시 노출 되는 네임 스페이스를 줄이는 데 사용할 수 있습니다. 그러나 이러한 속성은 공용 언어와 동일한 의미에서 "private"으로 간주 되어서는 안 됩니다. 런타임 (CLR) 언어 정의는 다음 섹션에 설명 된 이유로 해당 액세스 수준을 정의 합니다.  
  
<a name="PropertySystemExposure"></a>   
## <a name="property-system-exposure-of-dependency-properties"></a>종속성 속성의 속성 시스템 노출  
 일반적으로는 유용 하지 않으며, public이 아닌 모든 액세스 수준으로을 <xref:System.Windows.DependencyProperty> 선언 하는 것은 잠재적으로 잘못 될 수 있습니다. 해당 액세스 수준 설정은 다른 사용자가 선언하는 클래스에서 인스턴스에 대한 참조를 가져올 수 없도록만 합니다. 그러나 클래스 또는 파생 클래스 인스턴스의 특정 속성을 식별 하는 수단 <xref:System.Windows.DependencyProperty> 으로를 반환 하는 속성 시스템의 여러 측면이 있으며,이 식별자는 여전히 <xref:System.Windows.DependencyObject.SetValue%2A> 호출에서 사용할 수 있습니다. 원래 정적 식별자가 public이 아닌 것으로 선언 된 경우입니다. 또한 가상 <xref:System.Windows.DependencyObject.OnPropertyChanged%2A> 메서드는 값이 변경 된 모든 기존 종속성 속성의 정보를 수신 합니다. 또한 메서드는 <xref:System.Windows.DependencyObject.GetLocalValueEnumerator%2A> 로컬로 설정 된 값이 있는 인스턴스의 속성에 대 한 식별자를 반환 합니다.  
  
### <a name="validation-and-security"></a>유효성 검사 및 보안  
 에 수요 <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> 를 적용 하 고 속성을 설정 하는 것을 방지 하기 위해 요청 실패에 대 한 유효성 검사 오류를 예상 하는 것은 적절 한 보안 메커니즘이 아닙니다. 이러한 호출자가 응용 프로그램 도메인 <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> 내에서 작동 하는 경우를 통해 적용 되는 집합 값 무효화도 억제 될 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [사용자 지정 종속성 속성](custom-dependency-properties.md)
