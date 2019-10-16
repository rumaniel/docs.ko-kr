---
title: XAML 태그 확장명 개요
ms.date: 03/30/2017
helpviewer_keywords:
- markup extensions [XAML Services], custom
- XAML [XAML Services], markup extensions
ms.assetid: 261b2b11-2dc0-462f-8c66-55b8c9c6e436
ms.openlocfilehash: 68c03589294bcc8b58f1142331d4a889f0f18a3b
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736489"
---
# <a name="markup-extensions-for-xaml-overview"></a>XAML 태그 확장명 개요

태그 확장은 기본 형식이 나 특정 XAML 형식이 아닌 값을 가져오기 위한 XAML 기술입니다. 특성 사용과 관련하여 태그 확장은 여는 중괄호 `{` 의 알려진 문자 시퀀스를 사용하여 태그 확장 범위를 시작하고 닫는 중괄호 `}` 를 사용하여 종료합니다. .NET Framework XAML 서비스를 사용하는 경우 System.Xaml 어셈블리에서 미리 정의된 몇 가지 XAML 언어 태그 확장을 사용할 수 있습니다. System.Xaml에 정의된 <xref:System.Windows.Markup.MarkupExtension> 클래스에서 서브클래싱하고 고유한 태그 확장을 정의할 수도 있습니다. 또는 해당 프레임 워크를 이미 참조 하 고 있는 경우 특정 프레임 워크에 의해 정의 된 태그 확장을 사용할 수 있습니다.

태그 확장 사용법에 액세스하는 경우 XAML 개체 작성기는 <xref:System.Windows.Markup.MarkupExtension> 재정의의 서비스 연결 지점을 통해 사용자 지정 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A?displayProperty=nameWithType> 클래스에 서비스를 제공할 수 있습니다. 이 서비스는 사용법, 개체 작성기의 특정 기능, XAML 스키마 컨텍스트 등에 대한 컨텍스트를 가져오는 데 사용할 수 있습니다.

<a name="XAML_Defined_Markup_Extensions"></a>
## <a name="xaml-defined-markup-extensions"></a>XAML 정의 태그 확장

.NET Framework XAML 서비스는 XAML 언어 지원을 위해 여러 가지 태그 확장을 구현합니다. 이러한 태그 확장은 XAML 언어 사양의 일부에 해당합니다. 일반적인 사용법을 통해 알 수 있듯이 이러한 확장은 구문에서 `x:` 접두사로 식별할 수 있습니다. 이러한 XAML 언어 요소에 대 한 .NET Framework XAML 서비스 구현은 모두 <xref:System.Windows.Markup.MarkupExtension> 기본 클래스에서 파생 됩니다.

> [!NOTE]
> `x:` 접두사는 XAML 프로덕션의 루트 요소에서 XAML 언어 네임스페이스의 일반적인 XAML 네임스페이스 매핑에 사용됩니다. 예를 들어 다양 한 특정 프레임 워크에 대 한 Visual Studio 프로젝트 및 페이지 템플릿은이 `x:` 매핑을 사용 하 여 XAML 파일을 시작 합니다. 사용자 고유의 XAML 네임스페이스 매핑에서 다른 접두사 토큰을 선택할 수 있지만 이 설명서에서는 특정 프레임워크의 기본 XAML 네임스페이스나 다른 임의 CLR 또는 XML 네임스페이스와 달리 XAML 언어 XAML 네임 스페이스에서 정의된 부분인 해당 엔터티를 식별하는 방법으로 기본 `x:` 매핑을 가정합니다.

### <a name="xtype"></a>x:Type

`x:Type` 은 명명된 형식에 <xref:System.Type> 개체를 제공합니다. 이 기능은 기본 CLR 형식 및 형식 파생을 그룹화 모니커 또는 식별자로 사용하는 지연 메커니즘에서 가장 자주 사용됩니다. WPF 스타일 및 템플릿, `TargetType` 속성의 용도는 특정 예제입니다. 자세한 내용은 [x:Type Markup Extension](x-type-markup-extension.md)을 참조하세요.

### <a name="xstatic"></a>x:Static

`x:Static` 은 직접적으로 속성 값의 형식이 아니라 해당 형식으로 계산될 수 있는 값-형식 코드 엔터티에서 정적 값을 생성합니다. 잘 알려진 상수로 형식 정의에 이미 존재하는 값을 지정하는 데 유용합니다. 자세한 내용은 [x:Static Markup Extension](x-static-markup-extension.md)을 참조하세요.

### <a name="xnull"></a>x:Null

`x:Null` 은 `null` 을 XAML 멤버에 대한 값으로 지정합니다. 특정 형식의 디자인인지 더 큰 프레임워크 개념인지에 따라 `null` 이 속성의 기본값이나 빈 문자열 특성의 암시적 값이 아닌 경우가 있습니다. 자세한 내용은 [x:Null Markup Extension](x-null-markup-extension.md)을 참조하세요.

### <a name="xarray"></a>x:Array

`x:Array` 는 기본 요소 및 컨트롤 모델에서 제공하는 컬렉션 지원이 의도적으로 사용되지 않는 경우 XAML 구문에서 일반적인 배열 만들기를 지원합니다. 자세한 내용은 [x:Array Markup Extension](x-array-markup-extension.md)을 참조하세요. 특히 XAML 2009에서 배열은 확장이 아닌 언어 기본 형식으로 액세스됩니다. 자세한 내용은 [XAML 2009 Language Features](xaml-2009-language-features.md)을 참조하세요.

### <a name="xreference"></a>x:Reference

`x:Reference` 는 원래(2006) 언어 집합의 확장인 XAML 2009의 일부입니다. `x:Reference` 는 개체 그래프에 있는 다른 기존 개체에 대한 참조를 나타냅니다. 해당 개체는 `x:Name`으로 식별됩니다. 자세한 내용은 [x:Reference Markup Extension](x-reference-markup-extension.md)을 참조하세요.

### <a name="other-x-constructs"></a>기타 x: 만들고

XAML 언어 기능을 지원하는 다른 `x:` 구문도 있지만 이러한 구문은 태그 확장으로 구현되지 않습니다. 자세한 내용은 XAML 네임 스페이스 [(x:)를 참조 하세요. 언어 기능](xaml-namespace-x-language-features.md).

<a name="the_markupextension_base_class"></a>

## <a name="the-markupextension-base-class"></a>MarkupExtension 기본 클래스

System.Xaml의 XAML 판독기 및 XAML 작성기 기본 구현과 상호 작용할 수 있는 사용자 지정 태그 확장을 정의하려면 추상 <xref:System.Windows.Markup.MarkupExtension> 클래스에서 클래스를 파생시킵니다. 해당 클래스에는 재정의할 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>메서드가 한 개 있습니다. 태그 확장 사용에 대한 인수 및 일치하는 설정 가능한 속성을 지원하기 위해 추가 생성자도 정의해야 합니다.

<xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>을 통해 사용자 지정 태그 확장은 XAML 프로세서에서 태그 확장이 실제로 호출되는 환경을 보고하는 서비스 컨텍스트에 액세스할 수 있습니다. 로드 경로에서는 일반적으로 <xref:System.Xaml.XamlObjectWriter>입니다. 저장 경로에서는 일반적으로 <xref:System.Xaml.XamlXmlWriter>입니다. 각각은 서비스 공급자 패턴을 구현하는 내부 XAML 서비스 공급자 컨텍스트 클래스로 서비스 컨텍스트를 보고합니다. 사용 가능한 서비스 및 해당 서비스가 나타내는 의미에 대한 자세한 내용은 [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)을 참조하세요.

태그 확장 클래스는 공용 액세스 수준을 사용해야 합니다. XAML 프로세서는 해당 서비스를 사용하기 위해 태그 확장의 지원 클래스를 항상 인스턴스화할 수 있어야 합니다.

<a name="naming_the_support_type"></a>
## <a name="defining-the-support-type-for-a-custom-markup-extension"></a>사용자 지정 태그 확장에 대한 지원 형식 정의

.NET Framework XAML 서비스 또는.NET Framework XAML 서비스에 구축된 프레임워크를 사용하는 경우 태그 확장 지원 형식의 이름을 지정하는 방법에 대한 두 가지 옵션이 있습니다. 형식 이름은 관련 XAML 개체 작성기가 XAML에서 태그 확장 사용에 도달할 경우 태그 확장 지원 형식에 액세스하고 호출하는 방법과 관련이 있습니다. 다음 명명 전략 중 하나를 사용합니다.

- XAML 태그 사용 토큰과 정확하게 일치하도록 형식 이름을 지정합니다. 예를 들어 `{Collate ...}` 확장 사용을 지원하려면 지원 형식의 이름을 `Collate`로 지정합니다.
- 형식 이름이 사용 문자열 토큰과 접미사 `Extension`이 되도록 지정합니다. 예를 들어 `{Collate ...}` 확장 사용을 지원하려면 지원 형식의 이름을 `CollateExtension`로 지정합니다.

조회 순서는 `Extension`접미사가 있는 클래스 이름을 먼저 찾은 다음 `Extension` 접미사 없이 클래스 이름을 찾는 것입니다.
  
태그 사용 관점에서 `Extension` 접미사를 사용의 일부로 포함하는 것이 좋습니다. 그러나 `Extension` 이 실제로 클래스 이름의 일부인 것처럼 동작하며, 지원 클래스에 `Extension` 접미사가 없는 경우 XAML 개체 작성기에서 해당 사용에 대한 태그 확장 지원 클래스를 확인하지 못합니다.

### <a name="the-parameterless-constructor"></a>매개 변수가 없는 생성자

모든 태그 확장 지원 형식에 대해 매개 변수가 없는 public 생성자를 노출 해야 합니다. XAML 개체 작성기가 개체 요소 사용에서 태그 확장을 인스턴스화하는 모든 경우에는 매개 변수가 없는 생성자가 필요 합니다. 개체 요소 사용 지원은 태그 확장, 특히 serialization에 크게 기대하고 있습니다. 그러나 태그 확장의 특성 사용만 지원하려는 경우에는 public 생성자 없이 태그 확장을 구현할 수 있습니다.  

태그 확장 사용에 인수가 없는 경우 사용을 지원 하려면 매개 변수가 없는 생성자가 필요 합니다.

<a name="constructor_patterns_and_positional_arguments_for_a_custom_markup_extension"></a>
## <a name="constructor-patterns-and-positional-arguments-for-a-custom-markup-extension"></a>사용자 지정 태그 확장에 대한 생성자 패턴 및 위치 인수

원하는 인수가 사용되는 태그 확장의 경우 public 생성자가 원하는 사용 모드에 해당합니다. 즉, 태그 확장이 하나의 위치 인수를 유효한 사용으로 요구하도록 디자인된 경우 위치 인수를 사용하는 하나의 입력 매개 변수로 public 생성자를 지원해야 합니다.

예를 들어 `Collate` 태그 확장이 해당 모드를 나타내고 `CollationMode` 열거형 상수로 지정된 하나의 위치 인수가 있는 모드만 지원하도록 되어 있다고 가정합니다. 이런 경우 다음과 같은 형식의 생성자가 있어야 합니다.

```csharp
public Collate(CollationMode collationMode) {...}
```

기본적인 수준에서 태그 확장으로 전달된 인수는 태그의 특성 값에서 전달되기 때문에 문자열입니다. 모든 인수를 문자열로 만들고 해당 수준에서 입력 작업을 합니다. 그러나 태그 확장 인수가 지원 클래스에 전달되기 전에 발생하는 특정 처리에 액세스할 수 있습니다.

개념적으로 처리는 태그 확장이 만들려는 개체인 것처럼 작동한 다음 해당 멤버 값이 설정됩니다. 설정하도록 지정된 각 속성은 XAML을 구문 분석할 때 만든 개체에서 지정된 멤버를 설정하는 방법과 유사하게 계산됩니다. 다음과 같은 두 가지 중요한 차이점이 있습니다.
  
- 앞에서 설명한 대로 태그 확장 지원 형식은 XAML에서 인스턴스화하기 위해 매개 변수가 없는 생성자를 가질 필요가 없습니다. 해당 개체 생성은 텍스트 구문에서 가능한 인수가 위치 인수나 명명된 인수로 토큰화되고 계산될 때까지 지연되고 그때 적절한 생성자가 호출됩니다.
- 태그 확장 사용은 중첩할 수 있습니다. 가장 안쪽의 태그 확장이 먼저 계산됩니다. 따라서 이러한 사용을 가정하고 생성 매개 변수 중 하나를 값 변환기(예: 태그 확장)에서 생성해야 하는 형식으로 선언할 수 있습니다.

이러한 처리에 의존하는 경우는 이전 예제에 표시되어 있습니다. .NET Framework XAML 서비스 XAML 개체 작성기는 열거형 상수 이름을 기본 수준에서 열거된 값으로 처리합니다.

또한 태그 확장 위치 매개 변수의 텍스트 구문 처리에서는 생성 인수에 있는 형식과 연결된 형식 변환기를 사용할 수 있습니다.

사용에서 토큰 발생 순서가 할당된 생성자 매개 변수의 위치 순서에 해당하기 때문에 이러한 인수를 위치 인수라고 합니다. 예를 들어 다음과 같은 생성자 서명을 살펴보겠습니다.

```csharp
public Collate(CollationMode collationMode, object collateThis) {...}
```

XAML 프로세서는 이 태그 확장에 대해 두 개의 위치 인수를 예상합니다. `{Collate AlphaUp,{x:Reference circularFile}}`사용이 있는 경우 `AlphaUp` 토큰은 첫 번째 매개 변수로 전달되고 `CollationMode` 열거형 명명된 상수로 계산됩니다. 내부 `x:Reference` 의 결과는 두 번째 매개 변수를 전달되고 개체로 계산됩니다.

태그 확장 구문 및 처리에 대한 XAML 지정 규칙에서 쉼표는 해당 인수가 위치 인수인지 명명된 인수인지에 관계없이 인수 사이의 구분 기호입니다.

### <a name="duplicate-arity-of-positional-arguments"></a>위치 인수의 중복 인자

XAML 개체 작성기에서 위치 인수가 있는 태그 확장 사용이 발견되는 경우 해당 개수의 인수를 사용하는 여러 생성자 인수(중복 인자)가 있어도 반드시 오류가 발생하는 것은 아닙니다. 이 동작은 사용자 지정 가능한 XAML 스키마 컨텍스트 설정인 <xref:System.Xaml.XamlSchemaContextSettings.SupportMarkupExtensionsWithDuplicateArity%2A>에 따라 달라집니다. <xref:System.Xaml.XamlSchemaContextSettings.SupportMarkupExtensionsWithDuplicateArity%2A> 가 `true`인 경우 XAML 개체 작성기는 중복 인자라는 이유만으로 예외를 throw해서는 안 됩니다. 해당 지점을 벗어난 동작이 엄격하게 정의되지 않았습니다. 기본 디자인에서는 스키마 컨텍스트가 특정 매개 변수에 사용할 수 있는 형식 정보를 포함하고 중복 후보자와 일치하는 명시적 캐스팅을 시도하여 가장 잘 일치하는 서명을 확인한다고 가정합니다. 서명이 XAML 개체 작성기에서 실행되는 해당 특정 스키마 컨텍스트에서 적용되는 테스트를 통과할 수 없는 경우 예외가 throw될 수 있습니다.

기본적으로 <xref:System.Xaml.XamlSchemaContextSettings.SupportMarkupExtensionsWithDuplicateArity%2A> 는 .NET Framework XAML 서비스에 대한 CLR 기반 `false` 에서 <xref:System.Xaml.XamlSchemaContext> 입니다. 따라서 지원 형식의 생성자에 중복 인자가 있는 태그 확장 사용이 발견되는 경우 기본 <xref:System.Xaml.XamlObjectWriter> 는 예외를 throw합니다.

<a name="named_arguments_for_a_custom_markup_extension"></a>   
## <a name="named-arguments-for-a-custom-markup-extension"></a>사용자 지정 태그 확장에 대 한 명명 된 인수

XAML로 지정된 태그 확장은 사용에 명명된 인수 형태를 사용할 수도 있습니다. 첫 번째 토큰화 수준에서 텍스트 구문이 인수로 구분됩니다. 인수 내에 등호 기호(=)가 있는 인수는 명명된 인수로 식별됩니다. 또한 이러한 인수는 이름/값 쌍으로 토큰화됩니다. 이 경우 이름은 태그 확장 지원 형식의 설정 가능한 공용 속성 이름을 지정합니다. 명명된 인수 사용을 지원하려면 이러한 설정 가능한 공용 속성을 제공해야 합니다. 이 속성은 공용으로 유지되는 한 상속된 속성일 수 있습니다.

<a name="accessing_service_provider_context_from_a_markup_extension_implementation"></a>
## <a name="accessing-service-provider-context-from-a-markup-extension-implementation"></a>태그 확장 구현에서 서비스 공급자 컨텍스트 액세스

사용 가능한 서비스는 모든 값 변환기에서 동일합니다. 차이점은 각 값 변환기에서 서비스 컨텍스트를 수신하는 방법입니다. 서비스 액세스 및 사용 가능한 서비스는 [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)항목에 설명되어 있습니다.

<a name="property_element_usage_of_a_markup_extension"></a>
## <a name="property-element-usage-of-a-markup-extension"></a>태그 확장의 속성 요소 사용

태그 확장 사용에 대한 시나리오는 종종 특성 사용에서 태그 확장을 사용하여 설계됩니다. 그러나 지원 클래스를 정의하여 속성 요소 사용을 지원할 수도 있습니다.

태그 확장의 속성 요소 사용을 지원 하려면 매개 변수가 없는 public 생성자를 정의 합니다. 이 생성자는 정적 생성자가 아닌 인스턴스 생성자여야 합니다. 일반적으로 XAML 프로세서는 태그에서 처리 하는 모든 개체 요소에서 매개 변수가 없는 생성자를 호출 해야 하기 때문에이 작업이 필요 합니다. 여기에는 태그 확장 클래스가 개체 요소로 포함 됩니다. 고급 시나리오의 경우 클래스에 대해 기본이 아닌 생성 경로를 정의할 수 있습니다. 자세한 내용은 [X:FactoryMethod 지시문](x-factorymethod-directive.md)을 참조 하세요. 그러나 이러한 패턴을 태그 확장명 용도로 사용하면 디자이너와 원시 태그 사용자 모두 사용 패턴을 검색하기가 훨씬 더 어려워지므로 그렇게 해서는 안 됩니다.

<a name="attributing_for_a_custom_markup_extension"></a>
## <a name="attributing-for-a-custom-markup-extension"></a>사용자 지정 태그 확장에 대 한 특성 지정

디자인 환경과 특정 XAML 개체 작성기 시나리오를 모두 지원하려면 여러 가지 CLR 특성으로 태그 확장 지원 형식의 특성을 지정해야 합니다. 이러한 특성은 의도된 태그 확장 사용을 보고합니다.

 <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute> 는 <xref:System.Type> 에서 반환하는 개체 형식에 대한 <xref:System.Windows.Markup.ArrayExtension.ProvideValue%2A> 정보를 보고합니다. 순수 서명에 따라 <xref:System.Windows.Markup.ArrayExtension.ProvideValue%2A> 는 <xref:System.Object>를 반환합니다. 그러나 다양한 소비자는 보다 정확한 반환 형식 정보를 원할 수 있습니다. 여기에는 다음이 포함됩니다.

- 태그 확장 사용에 대한 형식 인식 지원을 제공할 수 있는 디자이너 및 IDE.
- 대상 클래스의 `SetMarkupExtension` 처리기 고급 구현으로, 알려진 특정 <xref:System.Windows.Markup.MarkupExtension> 구현을 이름별로 분기하는 대신 리플렉션을 사용하여 태그 확장의 반환 형식을 정의할 수 있습니다.

<a name="serialization_of_markup_extension_usages"></a>   
## <a name="serialization-of-markup-extension-usages"></a>태그 확장 사용의 Serialization

XAML 개체 작성기에서 태그 확장 사용을 처리하고 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>를 호출하면 이전의 태그 확장 사용에 대한 컨텍스트가 개체 그래프가 아닌 XAML 노드 스트림에 유지됩니다. 개체 그래프에서는 값만 유지됩니다. 원래 태그 확장 사용을 직렬화된 출력으로 유지해야 하는 다른 이유나 디자인 시나리오가 있는 경우 로드 경로 XAML 노드 스트림에서 태그 확장 사용을 추적하기 위한 고유 인프라를 설계해야 합니다. 로드 경로에서 노드 스트림의 요소를 다시 만드는 동작을 구현하고 저장 경로에서 serialization을 위해 XAML 작성기로 다시 재생하여 노드 스트림의 적절한 위치에 있는 값을 대체할 수 있습니다.

<a name="markup_extensions_in_the_xaml_node_stream"></a>
## <a name="markup-extensions-in-the-xaml-node-stream"></a>XAML 노드 스트림의 태그 확장

로드 경로에서 XAML 노드 스트림을 사용하여 작업하는 경우 태그 확장 사용은 개체로 노드 스트림에 나타납니다.

태그 확장 사용에서 위치 인수를 사용하는 경우 초기화 값을 가진 시작 개체로 표현됩니다. 대략적인 텍스트 표현으로 노드 스트림은 다음과 유사합니다.

 `StartObject` (<xref:System.Xaml.XamlType> 은 반환 형식이 아니라 태그 확장의 정의 형식임)

 `StartMember` ( <xref:System.Xaml.XamlMember> 의 이름은 `_InitializationText`임)

 `Value` (값은 사이의 구분 기호를 포함하는 문자열로의 위치 인수임)

 `EndMember`

 `EndObject`

명명된 인수를 사용하는 태그 확장 사용은 관련 이름의 멤버가 있는 개체로 표현되고, 각각은 텍스트 문자열 값으로 설정됩니다.

실제로 태그 확장의 `ProvideValue` 구현을 호출하려면 형식 매핑이 필요하고 태그 확장 지원 형식 인스턴스를 만들어야 하기 때문에 XAML 스키마 컨텍스트가 필요합니다. 이러한 이유로 태그 확장 사용이 기본 .NET Framework XAML 서비스 노드 스트림에서 이런 방식으로 유지됩니다. 로드 경로의 판독기 부분에서 필요한 XAML 스키마 컨텍스트를 사용할 수 없는 이유이기도 합니다.

일반적으로 저장 경로에서 XAML 노드 스트림을 사용하여 작업하는 경우 직렬화할 개체가 처음에는 태그 확장 사용 및 `ProvideValue` 결과에서 제공되었음을 알릴 수 있는 것이 개체 그래프 표현에 없습니다. 라운드트립에 대한 태그 확장 사용을 유지하면서 개체 그래프의 다른 변경 내용도 캡처해야 하는 시나리오에서는 원래 XAML 입력에서 태그 확장 사용에 대한 지식을 유지할 수 있는 고유한 기술을 고안해야 합니다. 예를 들어 태그 확장 사용을 복원하려면 저장 경로의 노드 스트림에서 작업하여 태그 확장 사용을 복원하거나 원래 XAML과 라운드트립 XAML 간에 병합을 수행해야 할 수 있습니다. WPF와 같은 일부 XAML 구현 프레임워크에서는 중간 형식(식)을 사용하여 태그 확장 사용에서 값을 제공한 경우를 나타낼 수 있습니다.

## <a name="see-also"></a>참조

- <xref:System.Windows.Markup.MarkupExtension>
- [XAML을 위한 형식 변환기 및 태그 확장명](type-converters-and-markup-extensions-for-xaml.md)
- [태그 확장 및 WPF XAML](../wpf/advanced/markup-extensions-and-wpf-xaml.md)
