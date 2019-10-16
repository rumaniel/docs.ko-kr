---
title: 사용자 지정 형식 및 라이브러리에 대한 XAML 관련 CLR 특성
ms.date: 03/30/2017
helpviewer_keywords:
- CLR attributes for custom types [XAML Services]
ms.assetid: 5dfb299a-b6e2-41b8-8694-e6ac987547f1
ms.openlocfilehash: a264ec3fa1232a058a3bfbabbe8b84712cf87322
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956405"
---
# <a name="xaml-related-clr-attributes-for-custom-types-and-libraries"></a>사용자 지정 형식 및 라이브러리에 대한 XAML 관련 CLR 특성
이 항목에서는 .NET Framework XAML 서비스에 의해 정의 되는 CLR (공용 언어 런타임) 특성에 대해 설명 합니다. 또한 응용 프로그램에 대 한 XAML 관련 시나리오를 포함 하는 .NET Framework에 정의 된 다른 CLR 특성도 어셈블리 또는 형식에 대해 설명 합니다. 이러한 CLR 특성을 사용 하 여 어셈블리, 형식 또는 멤버를 특성으로 사용 하면 형식과 관련 된 XAML 형식 시스템 정보를 제공 합니다. Xaml 노드 스트림을 직접 처리 하거나 전용 XAML 판독기와 XAML 작성기를 통해 .NET Framework XAML 서비스를 사용 하는 모든 XAML 소비자에 게 정보가 제공 됩니다.  
  
## <a name="xaml-related-clr-attributes-for-custom-types-and-custom-members"></a>사용자 지정 형식 및 사용자 지정 멤버에 대 한 XAML 관련 CLR 특성  
 CLR 특성을 사용 하려면 전체 CLR을 사용 하 여 형식을 정의 해야 합니다. 그렇지 않으면 이러한 특성을 사용할 수 없습니다. CLR을 사용 하 여 형식 지원을 정의 하는 경우 .NET Framework XAML 서비스 XAML 작성기에서 사용 하는 기본 XAML 스키마 컨텍스트는 지원 어셈블리에 대해 리플렉션을 통해 CLR 특성을 읽을 수 있습니다.  
  
 다음 섹션에서는 사용자 지정 형식 또는 사용자 지정 멤버에 적용할 수 있는 XAML 관련 특성에 대해 설명 합니다. 각 CLR 특성은 XAML 형식 시스템과 관련 된 정보를 전달 합니다. 로드 경로에서 특성을 사용 하는 정보는 xaml 판독기가 유효한 XAML 노드 스트림을 만드는 데 도움이 되거나 XAML 작성기가 유효한 개체 그래프를 생성 하는 데 도움이 됩니다. 저장 경로에서 특성이 지정 된 정보는 xaml 판독기가 XAML 형식 시스템 정보를 다시 구성 하는 유효한 XAML 노드 스트림을 만드는 데 도움이 됩니다. 또는 XAML 작성기 또는 다른 XAML 소비자에 대 한 serialization 힌트 또는 요구 사항을 선언 합니다.  
  
### <a name="ambientattribute"></a>AmbientAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.AmbientAttribute>  
  
 **적용 대상:** 연결할 수 있는 속성을 `get` 지 원하는 클래스, 속성 또는 접근자 멤버입니다.  
  
 **인수의** 없음  
  
 <xref:System.Windows.Markup.AmbientAttribute>속성이 나 특성 형식을 사용 하는 모든 속성이 XAML의 앰비언트 속성 개념에서 해석 되어야 함을 나타냅니다. 앰비언트 개념은 XAML 프로세서가 멤버의 형식 소유자를 결정하는 방법과 관련됩니다. 앰비언트 속성은 개체 그래프를 만들 때 파서 컨텍스트에서 값을 사용할 수 있어야 하지만 직접 XAML 노드 집합에 대해 일반적인 형식 멤버 조회가 일시 중단 되는 속성입니다.  
  
 앰비언트 개념은 CLR 특성을 정의 <xref:System.AttributeTargets>하는 방법에 따라 속성으로 표시 되지 않는 연결 가능한 멤버에 적용 될 수 있습니다. 메서드 특성 사용은 XAML에 연결할 수 있는 사용을 지 원하는 `get` 접근자의 경우에만 적용 해야 합니다.  
  
### <a name="constructorargumentattribute"></a>ConstructorArgumentAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.ConstructorArgumentAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 단일 생성자 인수와 일치 하는 속성의 이름을 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.ConstructorArgumentAttribute>매개 변수가 없는 생성자 구문을 사용 하 여 개체를 초기화할 수 있고 지정 된 이름의 속성이 생성 정보를 제공 하도록 지정 합니다. 이 정보는 주로 XAML serialization용입니다. 자세한 내용은 <xref:System.Windows.Markup.ConstructorArgumentAttribute>을 참조하세요.  
  
### <a name="contentpropertyattribute"></a>ContentPropertyAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.ContentPropertyAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 특성 사용 형식의 멤버 이름을 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.ContentPropertyAttribute>인수에 의해 이름이 지정 된 속성이 해당 형식에 대 한 XAML 콘텐츠 속성으로 사용 됨을 나타냅니다. XAML 콘텐츠 속성 정의는 정의 형식에 할당할 수 있는 모든 파생 형식에 상속 됩니다. 특정 파생 형식에를 적용 <xref:System.Windows.Markup.ContentPropertyAttribute> 하 여 특정 파생 형식에 대 한 정의를 재정의할 수 있습니다.  
  
 XAML 콘텐츠 속성으로 사용 되는 속성의 경우 속성에 대 한 속성 요소 태그 지정은 XAML 사용에서 생략 될 수 있습니다. 일반적으로 콘텐츠 및 포함 모델에 대해 간소화 된 XAML 태그의 수준을 올리는 XAML 콘텐츠 속성을 지정 합니다. 하나의 멤버만 XAML 콘텐츠 속성으로 지정할 수 있기 때문에 일부 형식의 컨테이너 속성을 XAML 콘텐츠 속성으로 지정 해야 하는 것에 대 한 디자인 선택 항목이 있을 수 있습니다. 다른 컨테이너 속성은 명시적 속성 요소와 함께 사용 해야 합니다.  
  
 Xaml 노드 스트림에서 xaml 콘텐츠 속성은 `StartMember` <xref:System.Xaml.XamlMember>여전히의 속성 이름을 사용 `EndMember` 하 여 및 노드를 생성 합니다. 멤버가 XAML 콘텐츠 속성 인지 확인 하려면 <xref:System.Xaml.XamlType> `StartObject` 위치에서 값을 검사 하 <xref:System.Xaml.XamlType.ContentProperty%2A>고 값을 가져옵니다.  
  
### <a name="contentwrapperattribute"></a>ContentWrapperAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.ContentWrapperAttribute>  
  
 **적용 대상:** 클래스, 특히 컬렉션 형식입니다.  
  
 **인수의** 외부 콘텐츠의 콘텐츠 래퍼 형식으로 사용할 형식을 지정 하는입니다.<xref:System.Type>  
  
 <xref:System.Windows.Markup.ContentWrapperAttribute>외부 콘텐츠를 래핑하는 데 사용할 연결 된 컬렉션 형식에 하나 이상의 형식을 지정 합니다. 외부 콘텐츠를 콘텐츠 속성의 형식에 형식 시스템 제약 조건이 캡처하지 않으면 소유 하는 형식에 대 한 XAML 사용은 지원 가능한 콘텐츠 사례의 모든 사례를 가리킵니다. 특정 유형의 콘텐츠를 강력한 형식의 일반에서 문자열을 지원할 수 있습니다에 대 한이 XAML이 지원 되는 예를 들어 <xref:System.Collections.ObjectModel.Collection%601>합니다. 콘텐츠 래퍼는 기존 태그 규칙을 텍스트 관련 콘텐츠 모델 마이그레이션과 같이 컬렉션에 대해 conception 할당 가능한 값의 XAML로 마이그레이션하는 데 유용 합니다.  
  
 콘텐츠 래퍼 유형을 두 개 이상 지정 하려면 특성을 여러 번 적용 합니다.  
  
### <a name="dependsonattribute"></a>DependsOnAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.DependsOnAttribute>  
  
 **적용 대상:** 속성  
  
 **인수의** 특성 사용 형식에 대 한 다른 멤버의 이름을 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.DependsOnAttribute>특성 사용 속성이 다른 속성의 값에 종속 됨을 나타냅니다. 속성 정의에이 특성을 적용 하면 종속 속성 XAML 개체에에서 먼저 처리 됩니다. 사용법 <xref:System.Windows.Markup.DependsOnAttribute> 유효한 개체 만들기에 대 한 구문 분석 하는 특정 순서를 야 합니다. 여기서 형식에서 속성의 예외적인 경우를 지정 합니다.  
  
 속성 정의에 여러 <xref:System.Windows.Markup.DependsOnAttribute> 사례를 적용할 수 있습니다.  
  
### <a name="markupextensionreturntypeattribute"></a>MarkupExtensionReturnTypeAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute>  
  
 **적용 대상:** <xref:System.Windows.Markup.MarkupExtension> 파생 형식으로 예상 되는 클래스입니다.  
  
 **인수의** `ProvideValue` 특성 <xref:System.Type> 의결과로가장정확하게예측할형식을지정하는입니다.<xref:System.Windows.Markup.MarkupExtension>  
  
 자세한 내용은 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md)합니다.  
  
### <a name="namescopepropertyattribute"></a>NameScopePropertyAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.NameScopePropertyAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 에서는 두 가지 형식의 특성을 지원 합니다.  
  
- 특성 사용 형식에 대 한 속성의 이름을 지정 하는 문자열입니다.  
  
- 속성의 이름과 명명 된 속성을 정의 하는 형식에 <xref:System.Type> 대 한를 지정 하는 문자열입니다. 이 폼은 연결 가능한 멤버를 XAML 이름 범위 속성으로 지정 하는 데 사용할 수 있습니다.  
  
 <xref:System.Windows.Markup.NameScopePropertyAttribute>특성 사용 클래스에 대 한 XAML 이름 범위 값을 제공 하는 속성을 지정 합니다. Xaml 이름 범위 속성은 실제 xaml 이름 범위, 해당 저장소 <xref:System.Windows.Markup.INameScope> 및 해당 동작을 구현 하 고 유지 하는 개체를 참조 해야 합니다.  
  
### <a name="runtimenamepropertyattribute"></a>RuntimeNamePropertyAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 특성 사용 형식에 대 한 런타임 이름 속성의 이름을 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>XAML [X:Name 지시문](x-name-directive.md)에 매핑되는 특성 사용 형식의 속성을 보고 합니다. 속성은 형식 <xref:System.String> 이어야 하며 읽기/쓰기 여야 합니다.  
  
 정의는 정의 형식에 할당할 수 있는 모든 파생 형식에 상속 됩니다. 특정 파생 형식에를 적용 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 하 여 특정 파생 형식에 대 한 정의를 재정의할 수 있습니다.  
  
### <a name="trimsurroundingwhitespaceattribute"></a>TrimSurroundingWhitespaceAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>  
  
 **적용 대상:** 유형  
  
 **인수의** 없음  
  
 <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>는 공백 유효 콘텐츠 내에 자식 요소로 나타날 수 있는 특정 형식에 적용 됩니다 (가 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>있는 컬렉션에서 콘텐츠 보유). <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>는 주로 저장 경로와 관련이 있지만를 검사 <xref:System.Xaml.XamlType.TrimSurroundingWhitespace%2A?displayProperty=nameWithType>하 여 로드 경로의 XAML 형식 시스템에서 사용할 수 있습니다. 자세한 내용은 [XAML의 공백 처리](whitespace-processing-in-xaml.md)를 참조 하세요.  
  
### <a name="typeconverterattribute"></a>TypeConverterAttribute  
 **참조 설명서:**  <xref:System.ComponentModel.TypeConverterAttribute>  
  
 **적용 대상:** 클래스, 속성, 메서드 (유일 하 게 XAML 유효한 메서드 대/소문자 `get` 는 연결 가능한 멤버를 지 원하는 접근자).  
  
 **인수의** <xref:System.Type>의 <xref:System.ComponentModel.TypeConverter>입니다.  
  
 <xref:System.ComponentModel.TypeConverterAttribute>XAML 컨텍스트에서는 사용자 지정 <xref:System.ComponentModel.TypeConverter>를 참조 합니다. 이 <xref:System.ComponentModel.TypeConverter> 는 사용자 지정 형식 또는 해당 형식의 멤버에 대 한 형식 변환 동작을 제공 합니다.  
  
 형식에 <xref:System.ComponentModel.TypeConverterAttribute> 특성을 적용 하 여 형식 변환기 구현을 참조 합니다. 클래스, 구조체 또는 인터페이스의 XAML에 대 한 형식 변환기를 정의할 수 있습니다. 열거형에 대해 형식 변환을 제공할 필요는 없으며, 기본적으로 변환을 사용할 수 있습니다.  
  
 형식 변환기는 태그의 특성 또는 초기화 텍스트에 사용 되는 문자열을 원하는 대상 형식으로 변환할 수 있어야 합니다. 자세한 내용은 [Typeconverter 및 XAML](../wpf/advanced/typeconverters-and-xaml.md)합니다.  
  
 형식의 모든 값에 적용 하는 대신 XAML에 대 한 형식 변환기 동작 특정 속성에 설정할 수도 있습니다. 적용 하는 예에서 <xref:System.ComponentModel.TypeConverterAttribute> 속성 정의에 (외부 정의 특정 없습니다 `get` 및 `set` 정의).  
  
 사용자 지정 연결 가능한 멤버의 XAML 사용에 대 한 형식 변환기 동작을 적용 하 여 할당할 수 있습니다 <xref:System.ComponentModel.TypeConverterAttribute> 에 `get` XAML 사용을 지 원하는 메서드 접근자입니다.  
  
 는 XAML이 존재 하기 전에 .NET Framework에 있었지만형식변환기모델은다른용도를제공했습니다.<xref:System.ComponentModel.TypeConverterAttribute> <xref:System.ComponentModel.TypeConverter> 를 참조 하 고 사용 <xref:System.ComponentModel.TypeConverterAttribute>하려면를 정규화 하거나에 대 한 `using` <xref:System.ComponentModel>문을 제공 해야 합니다. 또한 프로젝트에 시스템 어셈블리를 포함 해야 합니다.  
  
### <a name="uidpropertyattribute"></a>UidPropertyAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.UidPropertyAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 이름으로 관련 속성을 참조 하는 문자열입니다.  
  
 [X:Uid 지시문](x-uid-directive.md)의 별칭을 지정 하는 클래스의 CLR 속성을 나타냅니다.  
  
### <a name="usableduringinitializationattribute"></a>UsableDuringInitializationAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.UsableDuringInitializationAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 부울입니다. 특성의 용도에 사용 되는 경우 항상로 `true`지정 해야 합니다.  
  
 이 형식이 XAML 개체 그래프를 만드는 동안 하향식으로 빌드되는지 여부를 나타냅니다. 이는 프로그래밍 모델의 정의와 밀접 하 게 관련 된 고급 개념입니다. 자세한 내용은 <xref:System.Windows.Markup.UsableDuringInitializationAttribute>을 참조하세요.  
  
### <a name="valueserializerattribute"></a>ValueSerializerAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.ValueSerializerAttribute>  
  
 **적용 대상:** 클래스, 속성, 메서드 (유일 하 게 XAML 유효한 메서드 대/소문자 `get` 는 연결 가능한 멤버를 지 원하는 접근자).  
  
 **인수의** 특성을 사용 하는 형식의 모든 속성 또는 특성을 사용 하는 특정 속성을 serialize 할 때 사용할 값 serializer 지원 클래스를 지정 하는입니다.<xref:System.Type>  
  
 <xref:System.Windows.Markup.ValueSerializer>보다 <xref:System.ComponentModel.TypeConverter> 많은 상태와 컨텍스트가 필요한 값 serialization 클래스를 지정 합니다. <xref:System.Windows.Markup.ValueSerializer>연결 가능한 멤버에 대 한 정적 <xref:System.Windows.Markup.ValueSerializerAttribute> `get` 접근자 메서드에 특성을 적용 하 여 연결할 수 있는 멤버와 연결할 수 있습니다. 값 serialization도 적용 됩니다. 대리자 아니라 열거형, 인터페이스 및 구조체에 대 한 합니다.  
  
### <a name="whitespacesignificantcollectionattribute"></a>WhitespaceSignificantCollectionAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>  
  
 **적용 대상:** 클래스, 혼합 된 콘텐츠를 호스팅할 것으로 예상 되는 컬렉션 형식, 즉, 개체 요소 주위의 공백이 UI 표현에 중요할 수 있습니다.  
  
 **인수의** 없음  
  
 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>컬렉션 형식이 XAML 프로세서에 의해 공백으로 처리 되어야 함을 나타냅니다 .이는 컬렉션 내 XAML 노드 스트림의 값 노드 생성에 영향을 미칩니다. 자세한 내용은 [XAML의 공백 처리](whitespace-processing-in-xaml.md)를 참조 하세요.  
  
### <a name="xamldeferloadattribute"></a>XamlDeferLoadAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XamlDeferLoadAttribute>  
  
 **적용 대상:** 클래스, 속성  
  
 **인수의** 에서는 두 가지 특성 형식 형식 (문자열 또는 형식 <xref:System.Type>)을 지원 합니다. [https://docs.microsoft.com/azure/active-directory/develop/scenario-protected-web-api-overview](<xref:System.Windows.Markup.XamlDeferLoadAttribute>) 을 참조하세요.  
  
 클래스 또는 속성에 XAML에 대 한 지연 된 로드 사용법 (예: 템플릿 동작의 경우) 및 지연 동작 및 해당 대상/콘텐츠 형식을 지 원하는 클래스를 보고를 나타냅니다.  
  
### <a name="xamlsetmarkupextensionattribute"></a>XamlSetMarkupExtensionAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 콜백의 이름을로 합니다.  
  
 클래스에서 태그 확장을 사용 하 여 하나 이상의 해당 속성에 대 한 값을 제공 하 고, XAML 작성기가 클래스의 모든 속성에 대해 태그 확장 설정 작업을 수행 하기 전에 호출 해야 하는 처리기를 참조할 수 있음을 나타냅니다.  
  
### <a name="xamlsettypeconverterattribute"></a>XamlSetTypeConverterAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XamlSetTypeConverterAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 콜백의 이름을로 합니다.  
  
 클래스에서 형식 변환기를 사용 하 여 하나 이상의 해당 속성에 대 한 값을 제공 하 고, 클래스의 모든 속성에 대해 형식 변환기 설정 작업을 수행 하기 전에 XAML 작성기에서 호출 해야 하는 처리기를 참조할 수 있음을 나타냅니다.  
  
### <a name="xmllangpropertyattribute"></a>XmlLangPropertyAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XmlLangPropertyAttribute>  
  
 **적용 대상:** 클래스  
  
 **인수의** 특성 사용 형식 `xml:lang` 에 대 한 별칭으로 지정할 속성의 이름을 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.XmlLangPropertyAttribute>XML `lang` 지시문에 매핑되는 특성 사용 형식의 속성을 보고 합니다. 속성은 형식이 <xref:System.String>아니어도 되지만 문자열에서 할당할 수 있어야 합니다. 형식 변환기를 속성의 형식과 연결 하거나 특정 속성을 사용 하 여이를 수행할 수 있습니다. 속성은 읽기/쓰기가 가능 해야 합니다.  
  
 매핑의 `xml:lang` 시나리오는 런타임 개체 모델이 XMLDOM을 사용 하 여 특별히 처리 하지 않고도 XML 지정 언어 정보에 액세스할 수 있도록 하는 것입니다.  
  
 정의는 정의 형식에 할당할 수 있는 모든 파생 형식에 상속 됩니다. 특정 파생 형식에를 적용 <xref:System.Windows.Markup.XmlLangPropertyAttribute> 하 여 특정 파생 형식에 대 한 정의를 재정의할 수 있습니다. 단,이는 드문 시나리오입니다.  
  
## <a name="xaml-related-clr-attributes-at-the-assembly-level"></a>어셈블리 수준에서 XAML 관련 CLR 특성  
 다음 섹션에서는 형식 또는 멤버 정의에 적용 되지 않고 어셈블리에 적용 되는 XAML 관련 특성에 대해 설명 합니다. 이러한 특성은 XAML에서 사용할 사용자 지정 형식을 포함 하는 라이브러리를 정의 하는 전반적인 목표와 관련이 있습니다. 일부 특성은 XAML 노드 스트림에 직접 영향을 주지는 않지만 다른 소비자가 사용할 수 있도록 노드 스트림에서 전달 됩니다. 정보의 소비자에는 XAML 네임 스페이스 정보 및 관련 접두사 정보가 필요한 디자인 환경 또는 serialization 프로세스가 포함 됩니다. XAML 스키마 컨텍스트 (.NET Framework XAML 서비스 기본값 포함)도이 정보를 사용 합니다.  
  
### <a name="xmlnscompatiblewithattribute"></a>XmlnsCompatibleWithAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>  
  
 **인수의**  
  
- 포함에 대 한 XAML 네임 스페이스의 식별자를 지정 하는 문자열입니다.  
  
- 이전 인수에서 XAML 네임 스페이스를 포함 수 있는 XAML 네임 스페이스의 식별자를 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>다른 XAML 네임 스페이스에서 XAML 네임 스페이스를 스페이스가 수 있도록 지정 합니다. 일반적으로 포함하는 XAML 네임스페이스는 미리 정의된 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>에 표시됩니다. 이 기술은 라이브러리의 XAML 어휘 버전을 관리 하 고 이전 버전의 어휘에 대해 이전에 정의 된 태그와 호환 되도록 하는 데 사용할 수 있습니다.  
  
### <a name="xmlnsdefinitionattribute"></a>XmlnsDefinitionAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XmlnsDefinitionAttribute>  
  
 **인수의**  
  
- 정의할 XAML 네임 스페이스의 식별자를 지정 하는 문자열입니다.  
  
- CLR 네임 스페이스의 이름을 나타내는 문자열입니다. CLR 네임 스페이스는 어셈블리에서 public 형식을 정의 해야 하며 CLR 네임 스페이스 형식 중 하나 이상이 XAML 사용을 위한 것 이어야 합니다.  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>xaml 네임 스페이스와 CLR 네임 스페이스 사이에서 어셈블리 별로 매핑을 지정 합니다 .이는 XAML 개체 작성기 또는 XAML 스키마 컨텍스트에서 형식 확인에 사용 됩니다.  
  
 하나 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 이상의 어셈블리에 적용할 수 있습니다. 이 작업은 다음과 같은 이유를 조합 하 여 수행할 수 있습니다.  
  
- 라이브러리 디자인에는 런타임 API 액세스의 논리적 구성에 대 한 여러 CLR 네임 스페이스가 포함 되어 있습니다. 그러나 동일한 XAML 네임 스페이스를 참조 하 여 해당 네임 스페이스의 모든 형식을 XAML에서 사용할 수 있도록 하려고 합니다. 이 경우 값 <xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A> 은 같지만 값은 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 다른 <xref:System.Windows.Markup.XmlnsDefinitionAttribute.ClrNamespace%2A> 여러 특성을 적용 합니다. 이는 프레임 워크 또는 응용 프로그램이 일반적으로 사용 되는 기본 XAML 네임 스페이스를 사용 하는 XAML 네임 스페이스에 대 한 매핑을 정의 하는 경우 특히 유용 합니다.  
  
- 라이브러리 디자인에는 여러 CLR 네임 스페이스가 포함 되어 있으며, 이러한 CLR 네임 스페이스의 형식 사용 사이에 XAML 네임 스페이스를 명확 하 게 구분 하려고 합니다.  
  
- 어셈블리에 CLR 네임 스페이스를 정의 하 고 둘 이상의 XAML 네임 스페이스를 통해 해당 네임 스페이스에 액세스할 수 있도록 하려고 합니다. 이 시나리오는 동일한 코드 베이스를 사용 하 여 여러 어휘를 지원할 때 발생 합니다.  
  
- 하나 이상의 CLR 네임 스페이스에서 XAML 언어 지원을 정의 합니다. 이러한 값은 <xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A> 이어야 `http://schemas.microsoft.com/winfx/2006/xaml`합니다.  
  
### <a name="xmlnsprefixattribute"></a>XmlnsPrefixAttribute  
 **참조 설명서:**  <xref:System.Windows.Markup.XmlnsPrefixAttribute>  
  
 **인수의**  
  
- XAML 네임 스페이스의 식별자를 지정 하는 문자열입니다.  
  
- 권장 접두사를 지정 하는 문자열입니다.  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>XAML 네임 스페이스에 사용할 권장 접두사를 지정 합니다. 접두사는 .NET Framework xaml 서비스 <xref:System.Xaml.XamlXmlWriter>에 의해 serialize 되는 xaml 파일의 요소 및 특성을 쓰거나 xaml 구현 라이브러리가 xaml 편집 기능이 있는 디자인 환경과 상호 작용 하는 경우에 유용 합니다.  
  
 하나 <xref:System.Windows.Markup.XmlnsPrefixAttribute> 이상의 어셈블리에 적용할 수 있습니다. 이 작업은 다음과 같은 이유를 조합 하 여 수행할 수 있습니다.  
  
- 어셈블리에서 둘 이상의 XAML 네임 스페이스에 대 한 형식을 정의 합니다. 이 경우 각 XAML 네임 스페이스에 대해 서로 다른 접두사 값을 정의 해야 합니다.  
  
- 여러 어휘를 지원 하 고 각 어휘 및 XAML 네임 스페이스에 대해 서로 다른 접두사를 사용 합니다.  
  
- 어셈블리에서 XAML 언어 지원을 정의 하 고에 대 한 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> `http://schemas.microsoft.com/winfx/2006/xaml`를 포함 합니다. 이 경우 일반적으로 접두사 `x`의 수준을 올립니다.  
  
> [!NOTE]
> .NET Framework XAML 서비스는 XAML 관련 특성도 <xref:System.Windows.Markup.RootNamespaceAttribute>정의 합니다. 이 특성은 프로젝트 시스템 지원에 대 한 어셈블리 수준 특성이 며 XAML 사용자 지정 형식과는 관련이 없습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Attribute>
- [.NET Framework XAML 서비스에서 사용할 사용자 지정 형식 정의](defining-custom-types-for-use-with-net-framework-xaml-services.md)
