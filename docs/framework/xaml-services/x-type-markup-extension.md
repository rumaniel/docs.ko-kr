---
title: x:Type 태그 확장
ms.date: 03/30/2017
f1_keywords:
- x:TypeExtension
- Type
- x:Type
- xType
- TypeExtension
helpviewer_keywords:
- x:Type markup extension [XAML Services]
- XAML [XAML Services], x:Type markup extension
- XAML [XAML Services], TargetType attribute
- TargetType attribute [XAML Services]
- Type markup extension in XAML [XAML Services]
ms.assetid: e0e0ce6f-e873-49c7-8ad7-8b840eb353ec
ms.openlocfilehash: bf62987c61c1d4f6aefce515f79e997b41272b56
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622970"
---
# <a name="xtype-markup-extension"></a>x:Type 태그 확장
CLR 제공 <xref:System.Type> 개체는 지정된 된 XAML 형식에 대 한 기본 형식입니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object property="{x:Type prefix:typeNameValue}" .../>  
```  
  
## <a name="xaml-object-element-usage"></a>XAML 개체 요소 사용  
  
```xaml  
<x:Type TypeName="prefix:typeNameValue"/>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`prefix`|선택 사항입니다. 기본이 아닌 XAML 네임 스페이스에 매핑되는 접두사입니다. 접두사 지정 자주 필요 하지 않습니다. 설명 부분을 참조하세요.|  
|`typeNameValue`|필수 요소. 현재 기본 XAML 네임 스페이스; 확인할 수 있는 형식 이름 지정 된 접두사 경우 매핑됩니다 또는 `prefix` 제공 됩니다.|  
  
## <a name="remarks"></a>설명  
 합니다 `x:Type` 태그 확장에는 비슷한 기능을 합니다 `typeof()` C# 연산자 또는 `GetType` Microsoft Visual Basic의 연산자입니다.  
  
 합니다 `x:Type` 형식을 사용 하는 속성에 대 한 문자열에서 변환 동작을 제공 하는 태그 확장 <xref:System.Type>합니다. 입력은 XAML 형식입니다. 입력된 XAML 형식 및 CLR 출력 간의 관계 <xref:System.Type> 출력은 <xref:System.Type> 은 합니다 <xref:System.Xaml.XamlType.UnderlyingType%2A> 입력 <xref:System.Xaml.XamlType>, 필요한 조회 후 <xref:System.Xaml.XamlType> 기반으로 XAML 스키마 컨텍스트 및 합니다 <xref:System.Windows.Markup.IXamlTypeResolver>서비스 컨텍스트를 제공 합니다.  
  
 .NET Framework XAML 서비스에서이 태그 확장에 대 한 처리에서 정의 됩니다는 <xref:System.Windows.Markup.TypeExtension> 클래스입니다.  
  
 특정 프레임 워크 구현에서는 일부 속성을 수행할 <xref:System.Type> 으로 값 형식 이름의 직접 수락할 수 있습니다 (형식의 문자열 값 `Name`). 그러나이 동작을 구현 복잡 한 시나리오입니다. 예를 들어 다음에 나오는 "WPF 사용 정보" 섹션을 참조 합니다.  
  
 특성 구문은 이러한 태그 확장에 가장 많이 사용되는 구문입니다. `x:Type` 식별자 문자열 다음에 나오는 문자열 토큰은 기본 <xref:System.Windows.Markup.TypeExtension.TypeName%2A> 확장 클래스의 <xref:System.Windows.Markup.TypeExtension> 값으로 할당됩니다. 이 특성의 값은 CLR 형식에 따라.NET Framework XAML 서비스에 대 한 기본 XAML 스키마 컨텍스트에서 <xref:System.Reflection.MemberInfo.Name%2A> 원하는 형식의 포함 또는 <xref:System.Reflection.MemberInfo.Name%2A> 앞에 기본이 아닌 XAML 네임 스페이스에 대 한 접두사 매핑입니다.  
  
 `x:Type` 개체 요소 구문에서 태그 확장을 사용할 수 있습니다. 이 경우 값을 지정 하는 <xref:System.Windows.Markup.TypeExtension.TypeName%2A> 제대로 확장을 초기화 하기 위해 속성이 필요한 합니다.  
  
 그러나 `x:Type` 이 사용 하이 여 일반적이 지; 태그 확장 자세한 정보를 특성으로 사용할 수도 있습니다. `<object property="{x:Type TypeName=typeNameValue}" .../>`  
  
## <a name="wpf-usage-notes"></a>WPF 사용 정보  
  
### <a name="default-xaml-namespace-and-type-mapping"></a>기본 XAML Namespace 및 형식 매핑  
 WPF 프로그래밍에 대 한 기본 XAML 네임 스페이스는 대부분의 일반적인 XAML 시나리오에 필요한 XAML 형식이 포함 따라서 XAML 형식 값을 참조할 때 접두사를 피할 수 있습니다. 또는 기본 XAML 네임 스페이스에 매핑되지 않은 CLR 네임 스페이스에서 있지만 WPF 어셈블리에 포함 된 형식에 대 한 사용자 지정 어셈블리에서 형식을 참조 하는 경우 접두사를 매핑할 해야 할 수 있습니다. 매핑 CLR 네임 스페이스의 XAML 네임 스페이스 및 접두사에 대 한 자세한 내용은 참조 하세요. [XAML 네임 스페이스 및 WPF XAML에 대 한 매핑을 Namespace](../wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)합니다.  
  
### <a name="type-properties-that-support-typename-as-string"></a>해당 지원 Typename 문자열로 속성 입력  
 WPF 형식의 일부 속성의 값을 지정할 수 있는 기술을 지 원하는 <xref:System.Type> 없이 `x:Type` 태그 확장을 사용 합니다. 대신 형식 이름을 문자열로 값을 지정할 수 있습니다. 이 예가 <xref:System.Windows.Controls.ControlTemplate.TargetType%2A?displayProperty=nameWithType> 고 <xref:System.Windows.Style.TargetType%2A?displayProperty=nameWithType>입니다. 형식 변환기 또는 태그 확장을 통해이 동작에 대 한 지원을 제공 하지 됩니다. 대신,이 지연 동작을 통해 구현 <xref:System.Windows.FrameworkElementFactory>합니다.  
  
 Silverlight는 비슷한 규칙을 지원합니다. 사실 Silverlight 현재 지원 하지 않습니다 `{x:Type}` XAML 언어 지원, 받아들이지 않는 및 `{x:Type}` WPF Silverlight XAML 마이그레이션을 지원 하기 위한 몇 가지 환경 외부에서 사용 합니다. 따라서 문자열로 typename 동작은 모든 Silverlight 네이티브 속성 평가에 기본 제공 되는 <xref:System.Type> 값입니다.  
  
## <a name="xaml-2009"></a>XAML 2009  
 제네릭 형식 및 기능 동작을 수정에 대 한 추가 지원을 제공 하는 XAML 2009 `x:TypeArguments` 및 `x:Type` 이 지원을 제공 합니다.  
  
- `x:TypeArguments` 및의 관련된 개체 요소를 제네릭 개체 인스턴스화에 대 한 루트 이외의 요소에 있을 수 있습니다. 자세한 내용은의 "XAML 2009" 섹션을 참조 하세요 [X:typearguments Directive](x-typearguments-directive.md)합니다.  
  
- XAML 2009 태그에서 제네릭 형식의 제약 조건을 지정 하는 구문을 지원 합니다. 사용할 수 있습니다 `x:TypeArguments`, `x:Type`, 또는 두 기능을 조합 합니다.  
  
- WPF XAML 구현 에서도 부하 유형을 사용 하는 특정 프레임 워크에 대 한 암시적 형식 변환 동작에이 기능을 추가 대 한 XAML 2009를 처리할 때 <xref:System.Type>합니다.  
  
 Wpf에서 느슨한 XAML (태그 컴파일되지 않은 XAML)의 경우에 XAML 2009 기능을 사용할 수 있습니다. WPF에 대한 태그로 컴파일된 XAML 및 BAML 형식의 XAML은 현재 XAML 2009 키워드 및 기능을 지원하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Style>
- [스타일 지정 및 템플릿](../wpf/controls/styling-and-templating.md)
- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](../wpf/advanced/markup-extensions-and-wpf-xaml.md)
