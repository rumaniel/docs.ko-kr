---
title: ComponentResourceKey 태그 확장
ms.date: 03/30/2017
f1_keywords:
- ComponentResourceKey
- ComponentResourceKeyExtension
helpviewer_keywords:
- ComponentResourceKey markup extension [WPF]
- XAML [WPF], ComponentResourceKey markup extension
ms.assetid: d6bcdbe6-61b3-40a7-b381-4e02185b5a85
ms.openlocfilehash: b373b33fcc962e49aa220f31e24b1484a0a8cd98
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401597"
---
# <a name="componentresourcekey-markup-extension"></a>ComponentResourceKey 태그 확장
외부 어셈블리에서 로드 되는 리소스에 대 한 키를 정의 하 고 참조 합니다. 이렇게 하면 리소스 조회가 어셈블리 또는 클래스의 명시적 리소스 사전이 아닌 어셈블리의 대상 형식을 지정할 수 있습니다.  
  
## <a name="xaml-attribute-usage-setting-key-compact"></a>XAML 특성 사용 (설정 키, 압축)  
  
```xml  
<object x:Key="{ComponentResourceKey {x:Type targetTypeName}, targetID}" .../>  
```  
  
## <a name="xaml-attribute-usage-setting-key-verbose"></a>XAML 특성 사용 (설정 키, 자세한 정보)  
  
```xml  
<object x:Key="{ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}" .../>  
```  
  
## <a name="xaml-attribute-usage-requesting-resource-compact"></a>XAML 특성 사용 (리소스 요청, 압축)  
  
```xml  
<object property="{DynamicResource {ComponentResourceKey {x:Type targetTypeName}, targetID}}" .../>  
```  
  
## <a name="xaml-attribute-usage-requesting-resource-verbose"></a>XAML 특성 사용 (리소스 요청, 자세한 정보)  
  
```xml  
<object property="{DynamicResource {ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}}" .../>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`targetTypeName`|리소스 어셈블리에 정의 된 공용 CLR (공용 언어 런타임) 형식의 이름입니다.|  
|`targetID`|리소스의 키입니다. 리소스가 조회 `targetID` 될 때는 리소스의 [x:Key 지시문](../../xaml-services/x-key-directive.md) 과 유사 합니다.|  
  
## <a name="remarks"></a>설명  
 위의 사용에서 볼 수 있듯이 {`ComponentResourceKey`} 태그 확장 사용은 다음 두 위치에서 찾을 수 있습니다.  
  
- 컨트롤 작성자가 제공한 테마 리소스 사전 내에서 키의 정의입니다.  
  
- 컨트롤을 다시 템플릿을 지정 컨트롤의 테마에서 제공 하는 리소스에서 제공 되는 속성 값을 사용 하려는 경우 어셈블리에서 테마 리소스에 액세스 합니다.  
  
 테마에서 제공 되는 구성 요소 리소스를 참조 하는 경우 일반적으로 `{DynamicResource}` `{StaticResource}`대신를 사용 하는 것이 좋습니다. 이는 사용법에 나와 있습니다. `{DynamicResource}`사용자가 테마 자체를 변경할 수 있기 때문에를 사용 하는 것이 좋습니다. 테마를 지원 하기 위한 컨트롤 작성자의 의도와 가장 일치 하는 구성 요소 리소스가 필요한 경우 구성 요소 리소스 참조를 동적으로 사용 하도록 설정 해야 합니다.  
  
 는 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 리소스가 실제로 정의 된 대상 어셈블리에 있는 형식을 식별 합니다. 는 가정의된<xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 위치를 정확 하 게 파악 하는 것과 독립적으로 정의 하 고 사용할 수있지만결국에는참조된어셈블리를통해형식을확인해야합니다.`ComponentResourceKey`  
  
 의 <xref:System.Windows.ComponentResourceKey> 일반적인 용도는 클래스의 멤버로 노출 되는 키를 정의 하는 것입니다. 이러한 사용을 위해 태그 확장이 아니라 <xref:System.Windows.ComponentResourceKey> 클래스 생성자를 사용 합니다. 자세한 내용은 <xref:System.Windows.ComponentResourceKey> [컨트롤 제작 개요](../controls/control-authoring-overview.md)항목에서 또는 "테마 리소스의 키 정의 및 참조" 섹션을 참조 하세요.  
  
 키를 설정 하 고 키가 지정 된 리소스를 참조 하는 경우 일반적 `ComponentResourceKey` 으로 특성 구문은 태그 확장에 사용 됩니다.  
  
 표시 되는 압축 구문은 태그 확장 <xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=nameWithType> 의 생성자 시그니처와 위치 매개 변수 사용을 기반으로 합니다. `targetTypeName` 및`targetID` 가 제공 되는 순서는 중요 합니다. 자세한 구문은 <xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=nameWithType> 매개 변수가 없는 생성자를 사용 하 고 개체 요소의 진정한 특성 <xref:System.Windows.ComponentResourceKey.ResourceId%2A> 구문과 비슷한 방식으로 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 및를 설정 합니다. 자세한 구문에서 속성이 설정 되는 순서는 중요 하지 않습니다. 이러한 두 가지 대안 (압축 및 자세한 정보)의 관계와 메커니즘은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)항목에 자세히 설명 되어 있습니다.  
  
 기술적으로의 `targetID` 값은 임의의 개체 일 수 있으며, 문자열일 필요가 없습니다. 그러나 WPF에서 가장 일반적으로 사용 되는 것은 문자열 `targetID` 형식으로 값을 정렬 하는 것입니다. 이러한 문자열은 [XamlName 문법](../../xaml-services/xamlname-grammar.md)에서 유효 합니다.  
  
 `ComponentResourceKey`개체 요소 구문에 사용할 수 있습니다. 이 경우 확장을 제대로 초기화 하려면 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> 및 <xref:System.Windows.ComponentResourceKey.ResourceId%2A> 속성의 값을 모두 지정 해야 합니다.  
  
 판독기 구현에서이 태그 <xref:System.Windows.ComponentResourceKey> 확장에 대 한 처리는 클래스에 의해 정의 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `ComponentResourceKey`은 태그 확장입니다. 태그 확장은 특성 값을 리터럴 값 또는 처리기 이름이 아닌 다른 값이 되도록 이스케이프해야 하는 요구 사항이 있는 경우 일반적으로 구현되며 이러한 요구 사항은 특정 형식 또는 속성에 형식 변환기를 배치하는 것보다 더 포괄적입니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 모든 태그 확장은 특성 구문에서 { 및 } 문자를 사용합니다. 이러한 문자는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서가 태그 확장이 특성을 처리해야 함을 인식하는 데 사용되는 규칙입니다. 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.ComponentResourceKey>
- <xref:System.Windows.Controls.ControlTemplate>
- [컨트롤 제작 개요](../controls/control-authoring-overview.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
