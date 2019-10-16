---
title: StaticResource 태그 확장
ms.date: 03/30/2017
f1_keywords:
- StaticResource
- StaticResourceExtension
helpviewer_keywords:
- XAML [WPF], StaticResource markup extension
- StaticResource markup extensions [WPF]
ms.assetid: 97af044c-71f1-4617-9a94-9064b68185d2
ms.openlocfilehash: 7392be182aedeeebe6b7092f9868c1fabfaafcb7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963453"
---
# <a name="staticresource-markup-extension"></a>StaticResource 태그 확장
이미 정의 된 리소스에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 대 한 참조를 조회 하 여 모든 속성 특성에 대 한 값을 제공 합니다. 해당 리소스에 대 한 조회 동작은 로드 시간 조회와 비슷하며, 이전에는 다른 응용 프로그램 소스 뿐만 아니라 현재 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지의 태그에서 로드 된 리소스를 검색 하 여 해당 리소스 값을 런타임 개체의 속성 값입니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xml  
<object property="{StaticResource key}" .../>  
```  
  
## <a name="xaml-object-element-usage"></a>XAML 개체 요소 사용  
  
```xml  
<object>  
  <object.property>  
<StaticResource ResourceKey="key" .../>  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`key`|요청한 리소스의 키입니다. 리소스를 태그에서 만들었거나 코드에서 리소스를 만든 경우를 호출할 <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> 때 `key` 매개 변수로 제공 된 경우이 키는 처음에 [x:Key 지시문](../../xaml-services/x-key-directive.md) 에 의해 할당 되었습니다.|  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]
> 는 `StaticResource` 파일[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 내에서 어휘 적으로 정의 된 리소스에 대 한 전방 참조를 만들려고 해서는 안 됩니다. 이 작업을 수행 하는 것은 지원 되지 않으며 이러한 참조가 실패 하더라도를 <xref:System.Windows.ResourceDictionary> 나타내는 내부 해시 테이블이 검색 되 면 전방 참조를 시도 하면 로드 시 성능 저하가 발생 합니다. 최상의 결과를 위해 전방 참조를 피할 수 있도록 리소스 사전의 컴퍼지션을 조정 합니다. 전방 참조를 방지할 수 없는 경우 [DynamicResource 태그 확장](dynamicresource-markup-extension.md) 을 대신 사용 합니다.  
  
 지정 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 된는 페이지, 응용 프로그램, 사용 가능한 컨트롤 테마 및 외부 리소스 또는 시스템 리소스의 특정 수준에서 [x:Key 지시문](../../xaml-services/x-key-directive.md) 으로 식별 되는 기존 리소스와 일치 해야 합니다. 리소스 조회는 해당 순서로 발생 합니다. 정적 및 동적 리소스의 리소스 조회 동작에 대 한 자세한 내용은 [XAML 리소스](xaml-resources.md)를 참조 하세요.  
  
 리소스 키는 [XamlName 문법](../../xaml-services/xamlname-grammar.md)에 정의 된 임의의 문자열일 수 있습니다. 리소스 키는 등의 다른 개체 형식일 <xref:System.Type>수도 있습니다. <xref:System.Type> 키는 암시적 스타일 키를 통해 컨트롤을 테마에 따라 스타일을 지정 하는 방법에 대 한 기본입니다. 자세한 내용은 [컨트롤 제작 개요](../controls/control-authoring-overview.md)를 참조하십시오.  
  
 리소스를 참조 하는 다른 선언적 방법은 [DynamicResource 태그 확장](dynamicresource-markup-extension.md)입니다.  
  
 특성 구문은 이러한 태그 확장에 가장 많이 사용되는 구문입니다. `StaticResource` 식별자 문자열 다음에 나오는 문자열 토큰은 기본 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 확장 클래스의 <xref:System.Windows.StaticResourceExtension> 값으로 할당됩니다.  
  
 `StaticResource`개체 요소 구문에 사용할 수 있습니다. 이 경우 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 속성의 값을 지정 해야 합니다.  
  
 `StaticResource` 속성을 다음과 같이 속성=값 쌍으로 지정하는 자세한 특성 사용 구문에도 <xref:System.Windows.StaticResourceExtension.ResourceKey%2A>을 사용할 수 있습니다.  
  
```xml  
<object property="{StaticResource ResourceKey=key}" .../>  
```  
  
 자세한 정보 표시는 대개 설정 가능한 속성이 둘 이상이거나 일부 속성이 선택 사항인 확장의 경우에 유용합니다. `StaticResource`에는 설정 가능한 속성이 하나뿐이고 이 속성은 필수적 속성이므로 자세한 정보 표시를 사용하지 않는 것이 일반적입니다.  
  
 프로세서 구현에서이 태그 <xref:System.Windows.StaticResourceExtension> 확장에 대 한 처리는 클래스에 의해 정의 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `StaticResource`은 태그 확장입니다. 태그 확장은 특성 값을 리터럴 값 또는 처리기 이름이 아닌 다른 값이 되도록 이스케이프해야 하는 요구 사항이 있는 경우 일반적으로 구현되며 이러한 요구 사항은 특정 형식 또는 속성에 형식 변환기를 배치하는 것보다 더 포괄적입니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 모든 태그 확장은 특성 구문에서 { 및 } 문자를 사용합니다. 이러한 문자는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서가 태그 확장이 특성을 처리해야 함을 인식하는 데 사용되는 규칙입니다. 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [스타일 지정 및 템플릿](../controls/styling-and-templating.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [XAML 리소스](xaml-resources.md)
- [리소스 및 코드](resources-and-code.md)
