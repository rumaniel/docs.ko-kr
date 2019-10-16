---
title: Binding 태그 확장
ms.date: 03/30/2017
f1_keywords:
- Binding
helpviewer_keywords:
- Binding markup extensions [WPF]
- XAML [WPF], Binding markup extension
ms.assetid: 83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63
ms.openlocfilehash: 6776c89db474668b3aed0e38a3e18359bf93399d
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991474"
---
# <a name="binding-markup-extension"></a>Binding 태그 확장
속성 값을 데이터 바인딩된 값으로 지연 하 여 중간 식 개체를 만들고 런타임에 요소 및 바인딩에 적용 되는 데이터 컨텍스트를 해석 합니다.  
  
## <a name="binding-expression-usage"></a>바인딩 식 사용  
  
```xaml  
<object property="{Binding}" .../>  
-or-  
<object property="{Binding  bindProp1=value1[, bindPropN=valueN]*}" ...  
/>  
-or-  
<object property="{Binding path}" .../>  
-or  
<object property="{Binding path[, bindPropN=valueN]*}" .../>  
```  
  
## <a name="syntax-notes"></a>구문 정보  
 이러한 구문에서 및 `[]` `*` 는 리터럴이 아닙니다. 이러한 값은 0 개 이상의 *bindprop*`=`*값* 쌍을 사용할 `,` 수 있음을 나타내는 표기법의 일부 이며, 해당 값과 이전 *bindprop*`=`*값* 쌍 사이에 구분 기호가 있습니다.  
  
 "바인딩 확장을 사용 하 여 설정할 수 있는 바인딩 속성" 섹션에 나열 된 속성은 모두 <xref:System.Windows.Data.Binding> 개체 요소의 특성을 사용 하 여 설정할 수 있습니다. 그러나의 <xref:System.Windows.Data.Binding>태그 확장 사용은 아닙니다. CLR <xref:System.Windows.Data.Binding> 클래스의 속성을 설정 하는 특성의 일반적인 XAML 처리만 있습니다. 즉 `<Binding` , *bindProp1* value1`="` *bindpropn*값*en* <xref:System.Windows.Data.Binding> 은 개체 요소 사용의 특성에 대 한 동일한 구문입니다.`"]*/>` `="``"[` 식을 사용 하 `Binding` 는 대신 의 <xref:System.Windows.Data.Binding>특정 속성에 대 한 xaml 특성 사용에 대 한 자세한 내용은 .NET Framework 클래스 라이브러리에서의 <xref:System.Windows.Data.Binding> 관련 속성의 "XAML 특성 사용" 섹션을 참조 하세요.  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`bindProp1, bindPropN`|설정할 <xref:System.Windows.Data.Binding> 또는<xref:System.Windows.Data.BindingBase> 속성의 이름입니다. 일부 속성은 `Binding` 확장을 사용 하 여 설정할 수 없으며 일부 `Binding` 속성은 추가 중첩 된 태그 확장을 통해서만 식 내에서 설정할 수 있습니다. <xref:System.Windows.Data.Binding> "바인딩 확장을 사용 하 여 설정할 수 있는 바인딩 속성" 섹션을 참조 하세요.|  
|`value1, valueN`|속성을 설정할 값. 특성 값의 처리는 궁극적으로 설정 되는 특정 <xref:System.Windows.Data.Binding> 속성의 형식 및 논리와 관련이 있습니다.|  
|`path`|암시적 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> 속성을 설정 하는 경로 문자열입니다. [XAML 구문 PropertyPath](propertypath-xaml-syntax.md)도 참조 하세요.|  
  
## <a name="unqualified-binding"></a>정규화 되지 않은 {Binding}  
 " `{Binding}` 바인딩 식 사용"에 표시 된 사용법은의 <xref:System.Windows.Data.Binding> `null`초기 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> 를 포함 하는 기본값이 포함 된 개체를 만듭니다. 이는 생성 <xref:System.Windows.Data.Binding> 된이 런타임 데이터 컨텍스트에서 설정 <xref:System.Windows.Data.Binding.Source%2A?displayProperty=nameWithType> 되는 등의 주요 데이터 바인딩 속성 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> 에 의존 하는 경우에도 많은 시나리오에서 유용 합니다. 데이터 컨텍스트 개념에 대 한 자세한 내용은 [데이터 바인딩](../data/data-binding-wpf.md)을 참조 하세요.  
  
## <a name="implicit-path"></a>암시적 경로  
 태그 `Binding` 확장은를 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> 개념적 "기본 속성"으로 사용 합니다. `Path=` 여기서은 식에 표시 하지 않아도 됩니다. 암시적 경로를 사용 `Binding` 하 여 식을 지정 하는 경우 <xref:System.Windows.Data.Binding> 속성을 이름으로 지정 하는 다른 `bindProp` = `value` 쌍 보다 먼저 암시적 경로가 식에서 먼저 표시 되어야 합니다. 예를 들어 `{Binding PathString}`, 여기서 `PathString` 은 태그 확장 사용으로 <xref:System.Windows.Data.Binding> 만든에서의 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> 값으로 계산 되는 문자열입니다. 쉼표 구분 기호 뒤에 다른 명명 된 속성 (예: `{Binding LastName, Mode=TwoWay}`)을 사용 하 여 암시적 경로를 추가할 수 있습니다.  
  
## <a name="binding-properties-that-can-be-set-with-the-binding-extension"></a>바인딩 확장을 사용 하 여 설정할 수 있는 바인딩 속성  
 이 항목에 표시 된 `bindProp` 구문은 `Binding` 태그 확장을 통해 설정 될 수 있는 또는 <xref:System.Windows.Data.Binding> 의 <xref:System.Windows.Data.BindingBase> 읽기/쓰기 속성이 많기 때문에 제네릭 = `value` 근사값을 사용 합니다. 식 구문입니다. 암시적인 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>를 제외 하 고 순서에 관계 없이 설정할 수 있습니다. 를 명시적으로 지정 `Path=`하는 옵션을 사용할 수 있으며,이 경우 임의의 순서로 설정할 수 있습니다. 기본적으로 아래 목록에서 쉼표로 구분 된 쌍을 사용 하 여 `bindProp` = `value` 0 개 이상의 속성을 설정할 수 있습니다.  
  
 이러한 속성 값 중 일부에는 XAML의 텍스트 구문에서 네이티브 형식 변환을 지원 하지 않으므로 특성 값으로 설정 하기 위해 태그 확장이 필요한 개체 형식이 필요 합니다. 자세한 내용은 각 속성에 대 한 .NET Framework 클래스 라이브러리의 XAML 특성 사용 섹션을 참조 하세요. 추가 태그 확장 사용 여부와 상관 없이 XAML 특성 구문에 사용 하는 문자열은 기본적으로 `Binding` 식에 지정 하는 값과 동일 합니다. 단, 각각 `bindProp` =에따옴표를넣지않습니다.식에서 `value` `Binding`  
  
- <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>: 가능한 바인딩 그룹을 식별 하는 문자열입니다. 이는 비교적 고급 바인딩 개념입니다. 에 대 한 참조 <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>페이지를 참조 하세요.  
  
- <xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다.  
  
- <xref:System.Windows.Data.Binding.Converter%2A>: 식에서 `bindProp` `value` 문자열로 설정할 = 수 있지만 이렇게 하려면 [StaticResource 태그 확장과](staticresource-markup-extension.md)같은 값에 대 한 개체 참조가 필요 합니다. 이 경우 값은 사용자 지정 변환기 클래스의 인스턴스입니다.  
  
- <xref:System.Windows.Data.Binding.ConverterCulture%2A>: 표준 기반 식별자로 식에서 설정 가능 합니다. 에 대 한 <xref:System.Windows.Data.Binding.ConverterCulture%2A>참조 항목을 참조 하세요.  
  
- <xref:System.Windows.Data.Binding.ConverterParameter%2A>: 식에서 `bindProp` `value` 문자열로 설정할 = 수 있지만이는 전달 되는 매개 변수의 유형에 따라 달라 집니다. 값에 대 한 참조 형식을 전달 하는 경우이 사용에는 중첩 된 [StaticResource 태그 확장과](staticresource-markup-extension.md)같은 개체 참조가 필요 합니다.  
  
- <xref:System.Windows.Data.Binding.ElementName%2A>: 함께 사용할 <xref:System.Windows.Data.Binding.RelativeSource%2A> 수 없는 <xref:System.Windows.Data.Binding.Source%2A>경우와 및입니다. 이러한 각 바인딩 속성은 특정 바인딩 방법을 나타냅니다. [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조 하세요.  
  
- <xref:System.Windows.Data.BindingBase.FallbackValue%2A>: 식에서 `bindProp` `value` 문자열로 설정할 = 수 있지만이는 전달 되는 값의 형식에 따라 달라 집니다. 참조 형식을 전달 하는 경우에는 중첩 된 [StaticResource 태그 확장과](staticresource-markup-extension.md)같은 개체 참조가 필요 합니다.  
  
- <xref:System.Windows.Data.Binding.IsAsync%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다.  
  
- <xref:System.Windows.Data.Binding.Mode%2A>: *값* 은 <xref:System.Windows.Data.BindingMode> 열거형의 상수 이름입니다. 예를 들어, `{Binding Mode=OneWay}`을 입력합니다.  
  
- <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다.  
  
- <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다.  
  
- <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다.  
  
- <xref:System.Windows.Data.Binding.Path%2A>: 데이터 개체 또는 일반 개체 모델에 대 한 경로를 설명 하는 문자열입니다. 형식은이 항목에서 적절 하 게 설명할 수 없는 개체 모델을 트래버스하는 여러 가지 규칙을 제공 합니다. [PROPERTYPATH XAML 구문](propertypath-xaml-syntax.md)을 참조 하세요.  
  
- <xref:System.Windows.Data.Binding.RelativeSource%2A>: 및 <xref:System.Windows.Data.Binding.ElementName%2A> <xref:System.Windows.Data.Binding.Source%2A>와 함께 사용할 수 없습니다. 이러한 각 바인딩 속성은 특정 바인딩 방법을 나타냅니다. [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조 하세요. 값을 지정 하려면 중첩 된 [RelativeSource MarkupExtension](relativesource-markupextension.md) 사용이 필요 합니다.  
  
- <xref:System.Windows.Data.Binding.Source%2A>: 함께 사용할 <xref:System.Windows.Data.Binding.RelativeSource%2A> 수 없는 <xref:System.Windows.Data.Binding.ElementName%2A>경우와 및입니다. 이러한 각 바인딩 속성은 특정 바인딩 방법을 나타냅니다. [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조 하세요. 에는 중첩 된 확장 사용이 필요 합니다. 일반적으로 키가 지정 된 리소스 사전의 개체 데이터 소스를 참조 하는 [StaticResource 태그 확장이](staticresource-markup-extension.md) 필요 합니다.  
  
- <xref:System.Windows.Data.BindingBase.StringFormat%2A>: 바인딩된 데이터의 문자열 형식 규칙을 설명 하는 문자열입니다. 이는 비교적 고급 바인딩 개념입니다. 에 대 한 참조 <xref:System.Windows.Data.BindingBase.StringFormat%2A>페이지를 참조 하세요.  
  
- <xref:System.Windows.Data.BindingBase.TargetNullValue%2A>: 식에서 `bindProp` `value` 문자열로 설정할 = 수 있지만이는 전달 되는 매개 변수의 유형에 따라 달라 집니다. 값에 대 한 참조 형식을 전달 하는 경우에는 중첩 된 [StaticResource 태그 확장과](staticresource-markup-extension.md)같은 개체 참조가 필요 합니다.  
  
- <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>: *값* 은 <xref:System.Windows.Data.UpdateSourceTrigger> 열거형의 상수 이름입니다. 예를 들어, `{Binding UpdateSourceTrigger=LostFocus}`을 입력합니다. 특정 컨트롤에는이 바인딩 속성에 대 한 기본값이 다를 수 있습니다. [https://docs.microsoft.com/azure/active-directory/develop/scenario-protected-web-api-overview](<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>) 을 참조하세요.  
  
- <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다. 설명 부분을 참조하세요.  
  
- <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A>: 부울은 또는 `true` `false`중 하나일 수 있습니다. 기본값은 `false`입니다. 설명 부분을 참조하세요.  
  
- <xref:System.Windows.Data.Binding.XPath%2A>: XML 데이터 소스의 XMLDOM에 대 한 경로를 설명 하는 문자열입니다. [XMLDataProvider 및 XPath 쿼리를 사용 하 여 XML 데이터에 바인딩을](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)참조 하세요.  
  
 다음은 `Binding` 태그 확장/ <xref:System.Windows.Data.Binding> `{Binding}` 식 형식을 사용 하 여 설정할 수 없는의 속성입니다.  
  
- <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>:이 속성에는 콜백 구현에 대 한 참조가 필요 합니다. 이벤트 처리기 이외의 콜백/메서드는 XAML 구문에서 참조할 수 없습니다.  
  
- <xref:System.Windows.Data.Binding.ValidationRules%2A>: 속성은 개체의 <xref:System.Windows.Controls.ValidationRule> 제네릭 컬렉션을 사용 합니다. 이는 <xref:System.Windows.Data.Binding> 개체 요소의 속성 요소로 표시 될 수 있지만 `Binding` 식에서 사용 하기 위한 특성 구문 분석 기술은 쉽게 사용할 수 있습니다. 에 대 한 참조 <xref:System.Windows.Data.Binding.ValidationRules%2A>항목을 참조 하세요.  
  
- <xref:System.Windows.Data.Binding.XmlNamespaceManager%2A>  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]
> 종속성 속성 우선 순위 `Binding` 면에서 식은 로컬로 설정 된 값과 동일 합니다. 이전에 `Binding` 식이 `Binding` 있던 속성의 로컬 값을 설정 하면이 완전히 제거 됩니다. 자세한 내용은 [종속성 속성 값 우선 순위](dependency-property-value-precedence.md)를 참조하세요.  
  
 기본 수준에서 데이터 바인딩을 설명 하는 방법은이 항목에서 다루지 않습니다. [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조 하세요.  
  
> [!NOTE]
> <xref:System.Windows.Data.MultiBinding>및 <xref:System.Windows.Data.PriorityBinding> 는[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 확장 구문을 지원 하지 않습니다. 대신 속성 요소를 사용 합니다. 및에 대 한 <xref:System.Windows.Data.MultiBinding> 참조 <xref:System.Windows.Data.PriorityBinding>항목을 참조 하세요.  
  
 XAML에 대 한 부울 값은 대/소문자를 구분 하지 않습니다. 예를 들어 `{Binding NotifyOnValidationError=true}` 또는 `{Binding NotifyOnValidationError=True}`를 지정할 수 있습니다.  
  
 데이터 유효성 검사와 관련 `Binding` 된 바인딩은 일반적으로 `{Binding ...}` 식이 아니라 명시적 요소에 의해 지정 되며 식에서 또는 <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 를 설정 하는 것은 일반적이 지 않습니다. 이는 도우미 속성 <xref:System.Windows.Data.Binding.ValidationRules%2A> 을 식 형식으로 쉽게 설정할 수 없기 때문입니다. 자세한 내용은 [바인딩 유효성 검사 구현](../data/how-to-implement-binding-validation.md)을 참조 하세요.  
  
 `Binding`은 태그 확장입니다. 태그 확장은 특성 값을 리터럴 값 또는 처리기 이름이 아닌 다른 값으로 이스케이프 해야 하는 요구 사항이 있는 경우 일반적으로 구현 되며, 요구 사항은 특정 형식 또는 속성에 대 한 특성이 있는 형식 변환기 보다 더 전역적입니다. Xaml의 모든 태그 확장은 특성 `{` 구문 `}` 에서 및 문자를 사용 합니다 .이는 xaml 프로세서에서 태그 확장이 문자열 내용을 처리 해야 한다는 것을 인식 하는 데 사용 되는 규칙입니다. 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
 `Binding`는 WPF의 xaml 구현에 대 한 <xref:System.Windows.Data.Binding> 확장 기능을 구현 하는 클래스가 XAML과 관련이 없는 몇 가지 다른 메서드 및 속성을 구현 한다는는 이례적인 태그 확장입니다. 다른 멤버는 XAML 태그 확장으로 <xref:System.Windows.Data.Binding> 작동 하는 것 외에도 많은 데이터 바인딩 시나리오를 처리할 수 있는 더 다양 한 자체 포함 클래스를 만들기 위한 것입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Data.Binding>
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
