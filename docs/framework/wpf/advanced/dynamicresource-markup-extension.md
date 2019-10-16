---
title: DynamicResource 태그 확장
ms.date: 03/30/2017
f1_keywords:
- DynamicResource
- DynamicResourceExtension
helpviewer_keywords:
- XAML [WPF], DynamicResource markup extension
- DynamicResource markup extensions [WPF]
ms.assetid: 7324f243-03af-4c2b-b0db-26ac6cdfcbe4
ms.openlocfilehash: 06355c64d36d2688ef027c1940688d4c87e51ec8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964794"
---
# <a name="dynamicresource-markup-extension"></a>DynamicResource 태그 확장
정의 된 리소스에 대 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 한 참조로 해당 값을 지연 시켜 속성 특성에 대 한 값을 제공 합니다. 해당 리소스에 대 한 조회 동작은 런타임 조회와 유사 합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xml  
<object property="{DynamicResource key}" .../>  
```  
  
## <a name="xaml-property-element-usage"></a>XAML 속성 요소 사용  
  
```xml  
<object>  
  <object.property>  
    <DynamicResource ResourceKey="key" .../>  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`key`|요청한 리소스의 키입니다. 리소스를 태그에서 만들었거나 코드에서 리소스를 만든 경우를 호출할 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> 때 `key` 매개 변수로 제공 된 경우이 키는 처음에 [x:Key 지시문](../../xaml-services/x-key-directive.md) 에 의해 할당 되었습니다.|  
  
## <a name="remarks"></a>설명  
 는 `DynamicResource` 초기 컴파일 중에 임시 식을 만들고 요청 된 리소스 값이 실제로 개체를 생성 하는 데 필요할 때까지 리소스 조회를 지연 합니다. 이는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지가 로드 된 후에 발생할 수 있습니다. 리소스 값은 현재 페이지 범위에서 시작 하는 모든 활성 리소스 사전에 대 한 키 검색에 따라 검색 되며, 컴파일의 자리 표시자 식으로 대체 됩니다.  
  
> [!IMPORTANT]
> 종속성 속성 우선 순위 `DynamicResource` 면에서 식은 동적 리소스 참조가 적용 되는 위치와 동일 합니다. 이전에 `DynamicResource` 식이 로컬 값 `DynamicResource` 으로 포함 된 속성의 로컬 값을 설정 하면이 완전히 제거 됩니다. 자세한 내용은 [종속성 속성 값 우선 순위](dependency-property-value-precedence.md)를 참조하세요.  
  
 특정 리소스 액세스 시나리오는 `DynamicResource` [StaticResource 태그 확장이](staticresource-markup-extension.md)아니라에 특히 적합 합니다. `DynamicResource` 및 `StaticResource` 의 상대적인 장점 및 성능 영향에 대한 자세한 내용은 [XAML리소스](xaml-resources.md)를 참조하세요.  
  
 지정 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 된는 페이지, 응용 프로그램, 사용 가능한 컨트롤 테마 및 외부 리소스 또는 시스템 리소스의 특정 수준에서 [x:Key 지시문](../../xaml-services/x-key-directive.md) 에 의해 결정 되는 기존 리소스와 일치 해야 하며 리소스 조회가 수행 됩니다. 이 순서 대로. 정적 및 동적 리소스의 리소스 조회에 대 한 자세한 내용은 [XAML 리소스](xaml-resources.md)를 참조 하세요.  
  
 리소스 키는 [XamlName 문법](../../xaml-services/xamlname-grammar.md)에 정의 된 모든 문자열일 수 있습니다. 리소스 키는 등의 다른 개체 형식일 <xref:System.Type>수도 있습니다. 키는 <xref:System.Type> 테마를 기준으로 컨트롤의 스타일을 지정 하는 방법에 대 한 기본입니다. 자세한 내용은 [컨트롤 제작 개요](../controls/control-authoring-overview.md)를 참조하십시오.  
  
 과 <xref:System.Windows.FrameworkElement.FindResource%2A>같은 리소스 값을 조회 하기 위한 api는에서 `DynamicResource`사용 하는 것과 동일한 리소스 조회 논리를 따릅니다.  
  
 리소스를 참조 하는 다른 선언적 방법은 [StaticResource 태그 확장](staticresource-markup-extension.md)입니다.  
  
 특성 구문은 이러한 태그 확장에 가장 많이 사용되는 구문입니다. `DynamicResource` 식별자 문자열 다음에 나오는 문자열 토큰은 기본 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 확장 클래스의 <xref:System.Windows.DynamicResourceExtension> 값으로 할당됩니다.  
  
 `DynamicResource`개체 요소 구문에 사용할 수 있습니다. 이 경우 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 속성의 값을 지정 해야 합니다.  
  
 `DynamicResource` 속성을 다음과 같이 속성=값 쌍으로 지정하는 자세한 특성 사용 구문에도 <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A>을 사용할 수 있습니다.  
  
```xml  
<object property="{DynamicResource ResourceKey=key}" .../>  
```  
  
 자세한 정보 표시는 대개 설정 가능한 속성이 둘 이상이거나 일부 속성이 선택 사항인 확장의 경우에 유용합니다. `DynamicResource`에는 설정 가능한 속성이 하나뿐이고 이 속성은 필수적 속성이므로 자세한 정보 표시를 사용하지 않는 것이 일반적입니다.  
  
 프로세서 구현에서이 태그 <xref:System.Windows.DynamicResourceExtension> 확장에 대 한 처리는 클래스에 의해 정의 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `DynamicResource`은 태그 확장입니다. 태그 확장은 특성 값을 리터럴 값 또는 처리기 이름이 아닌 다른 값이 되도록 이스케이프해야 하는 요구 사항이 있는 경우 일반적으로 구현되며 이러한 요구 사항은 특정 형식 또는 속성에 형식 변환기를 배치하는 것보다 더 포괄적입니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 모든 태그 확장은 특성 구문에서 { 및 } 문자를 사용합니다. 이러한 문자는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서가 태그 확장이 특성을 처리해야 함을 인식하는 데 사용되는 규칙입니다. 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [XAML 리소스](xaml-resources.md)
- [리소스 및 코드](resources-and-code.md)
- [x:Key 지시문](../../xaml-services/x-key-directive.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [StaticResource 태그 확장](staticresource-markup-extension.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
