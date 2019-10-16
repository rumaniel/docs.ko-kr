---
title: XAML을 위한 형식 변환기 개요
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converters
- XAML [XAML Services], TypeConverter
- type conversion for XAML [XAML Services]
ms.assetid: 51a65860-efcb-4fe0-95a0-1c679cde66b7
ms.openlocfilehash: e401b40e1c11504e3c27d5b3601d71ef8f5821e1
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169012"
---
# <a name="type-converters-for-xaml-overview"></a>XAML을 위한 형식 변환기 개요
형식 변환기는 XAML 태그의 문자열에서 개체 그래프의 특정 개체로 변환하는 논리를 개체 작성기에 제공합니다. .NET Framework XAML 서비스에서 형식 변환기는 <xref:System.ComponentModel.TypeConverter>에서 파생되는 클래스여야 합니다. 또한 일부 변환기는 XAML 저장 경로를 지원하며 serialization 태그에서 개체를 문자열 형식으로 직렬화하는 데 사용할 수 있습니다. 이 항목에서는 XAML의 형식 변환기가 호출되는 방법 및 시기에 대해 설명하고 <xref:System.ComponentModel.TypeConverter>의 메서드 재정의에 대한 구현 권장 사항을 제공합니다.  
  
<a name="type_conversion_concepts"></a>   
## <a name="type-conversion-concepts"></a>형식 변환 개념  
 다음 섹션에서는 XAML에서 문자열을 사용하는 방법 및 .NET Framework XAML 서비스의 개체 작성기에서 형식 변환기를 사용하여 XAML 소스에 있는 일부 문자열 값을 처리하는 방법에 대한 기본 개념을 설명합니다.  
  
### <a name="xaml-and-string-values"></a>XAML 및 문자열 값  
 XAML 파일에서 특성 값을 설정하는 경우 해당 값의 초기 형식은 일반적인 의미에서 문자열이고 XML 의미에서 문자열 특성 값입니다. <xref:System.Double> 과 같은 다른 기본 형식도 처음에는 XAML 프로세서의 문자열입니다.  
  
 대부분의 경우 XAML 프로세서에서 특성 값을 처리하려면 두 가지 정보가 필요합니다. 첫 번째 정보는 설정되는 속성의 값 형식입니다. 특성 값을 정의하고 XAML에서 처리되는 모든 문자열은 결국 해당 형식의 값으로 변환되거나 확인되어야 합니다. 값이 숫자 값과 같이 XAML 파서에서 인식되는 기본 형식인 경우 문자열의 직접 변환이 시도됩니다. 특성에 대한 값이 열거형을 참조하는 경우에는 제공된 문자열에서 이름이 해당 열거형에 명명된 상수와 일치하는지 확인합니다. 값이 파서에서 인식되는 기본 형식이나 열거형의 상수 이름이 아닌 경우 적용 가능한 형식에서 변환된 문자열을 기반으로 하는 값이나 참조를 제공할 수 있어야 합니다.  
  
> [!NOTE]
> XAML 언어 지시문은 형식 변환기를 사용하지 않습니다.  
  
### <a name="type-converters-and-markup-extensions"></a>형식 변환기 및 태그 확장  
 태그 확장 사용은 속성 형식 및 기타 고려 사항을 확인하기 전에 XAML 프로세서에서 처리되어야 합니다. 예를 들어 일반적으로 특성으로 설정되는 속성에 형식 변환이 있지만 특별한 경우에는 태그 확장 사용으로 설정되는 경우 태그 확장 동작이 먼저 처리됩니다. 태그 확장이 필요한 일반적인 상황은 이미 존재하는 개체에 대한 참조를 만드는 경우입니다. 이 시나리오에서는 상태 비저장 형식 변환기만 새 인스턴스를 생성할 수 있으며, 이는 바람직하지 않을 수 있습니다. 태그 확장에 대한 자세한 내용은 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md)를 참조하세요.  
  
### <a name="native-type-converters"></a>네이티브 형식 변환기  
 WPF 및 .NET XAML 서비스 구현에는 네이티브 형식 변환 처리를 포함 하는 특정 CLR 형식이 있지만 이러한 CLR 형식은 기본 형식으로 간주 되지 않습니다. 이러한 형식의 예로는 <xref:System.DateTime>이 있습니다. 한 가지 이유는 <xref:System.DateTime> 형식이 .NET에서 가장 기본적인 라이브러리인 mscorlib에서 정의되는 .NET Framework 아키텍처의 작동 방식입니다. <xref:System.DateTime> 은 종속성을 도입하는 다른 어셈블리에서 제공하는 특성을 사용할 수 없습니다(<xref:System.ComponentModel.TypeConverterAttribute> 는 시스템 제공). 따라서 특성을 사용하는 일반적인 형식 변환기 검색 메커니즘을 지원할 수 없습니다. 대신 XAML 파서에 네이티브 처리가 필요한 형식 목록이 있으며 실제 기본 형식이 처리되는 방법과 유사한 방법으로 이러한 형식을 처리합니다. <xref:System.DateTime>의 경우 이 처리에서 <xref:System.DateTime.Parse%2A>를 호출합니다.  
  
<a name="Implementing_a_Type_Converter"></a>   
## <a name="implementing-a-type-converter"></a>형식 변환기 구현  
 다음 섹션에서는 <xref:System.ComponentModel.TypeConverter> 클래스의 API에 대해 설명합니다.  
  
### <a name="typeconverter"></a>TypeConverter  
 .NET Framework XAML 서비스에서 XAML 용도에 사용되는 모든 형식 변환기는 기본 클래스 <xref:System.ComponentModel.TypeConverter>에서 파생되는 클래스입니다. <xref:System.ComponentModel.TypeConverter> 클래스는 XAML이 존재하기 이전에 .NET Framework 버전에 있었으며, 원래 <xref:System.ComponentModel.TypeConverter> 시나리오 중 하나는 비주얼 디자이너의 속성 편집기에 문자열 변환을 제공했습니다.  
  
 XAML의 경우 <xref:System.ComponentModel.TypeConverter> 의 역할이 확장됩니다. XAML 용도에서 <xref:System.ComponentModel.TypeConverter> 는 특정 to-string 및 from-string 변환을 지원하는 기본 클래스입니다. From-string에서는 XAML에서 문자열 특성 값을 구문 분석할 수 있습니다. To-string에서는 serialization을 위해 특정 개체 속성의 런타임 값을 XAML의 특성으로 다시 처리할 수 있습니다.  
  
 <xref:System.ComponentModel.TypeConverter> 는 XAML 처리를 위한 to-string 및 from-string 변환과 관련된 네 가지 멤버를 정의합니다.  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 이러한 멤버 중 가장 중요한 메서드는 입력 문자열을 필요한 개체 형식으로 변환하는 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>입니다. <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 메서드는 광범위한 형식을 변환기의 지정된 대상 형식으로 변환하기 위해 구현할 수 있습니다. 따라서 런타임 변환 지원과 같이 XAML 이상으로 확장되는 용도로 사용할 수 있습니다. 그러나 XAML 용도에서는 <xref:System.String> 입력을 처리할 수 있는 코드 경로만 중요합니다.  
  
 다음으로 중요한 메서드는 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>입니다. 애플리케이션이 태그 표현으로 변환되는 경우(예: 파일로 XAML에 저장되는 경우) <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 는 XAML 텍스트 작성기에서 태그 표현을 생성하는 더 큰 시나리오에 포함됩니다. 이 경우 XAML에 중요한 코드 경로는 호출자가 `destinationType` 의 <xref:System.String>을 전달하는 경우입니다.  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 및 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 은 서비스에서 <xref:System.ComponentModel.TypeConverter> 구현의 기능을 쿼리할 때 사용되는 지원 메서드입니다. 변환기의 동일한 변환 메서드에서 지원하는 형식 관련 케이스에 대해 `true` 를 반환하려면 이러한 메서드를 구현해야 합니다. XAML 용도에서는 일반적으로 <xref:System.String> 형식을 의미합니다.  
  
### <a name="culture-information-and-type-converters-for-xaml"></a>XAML에 대한 문화권 정보 및 형식 변환기  
 각 <xref:System.ComponentModel.TypeConverter> 구현에서는 변환에 유효한 문자열을 고유하게 해석할 수 있으며 매개 변수로 전달되는 형식 설명을 사용하거나 무시할 수도 있습니다. 문화권 및 XAML 형식 변환에서 중요한 고려 사항은 XAML에서 지역화 가능한 문자열을 특성 값으로 사용할 수 있지만 이러한 지역화 가능한 문자열을 특정 문화권 요구 사항이 있는 형식 변환기 입력으로 사용할 수 없다는 점입니다. 이러한 제한은 XAML 특성 값에 대한 형식 변환기에서 `en-US` 문화권을 사용하는 고정 언어 XAML 처리 동작을 반드시 포함하기 때문입니다. 이러한 제한의 디자인 이유에 대 한 자세한 내용은 xaml 언어 사양 ([\[MS-xaml\]](https://go.microsoft.com/fwlink/?LinkId=114525)) 또는 [WPF 전역화 및 지역화 개요](../wpf/advanced/wpf-globalization-and-localization-overview.md)를 참조 하세요.  
  
 문화권이 문제가 될 수 있는 경우에 대한 예로 일부 문화권에서는 문자열 형식의 숫자에 대한 소수점 구분 기호로 마침표 대신 쉼표를 사용합니다. 이러한 사용은 쉼표를 구분 기호로 사용하는 기존의 많은 형식 변환기의 동작과 충돌합니다. 주변 XAML에서 `xml:lang` 을 통해 문화권을 전달하면 문제가 해결되지 않습니다.  
  
### <a name="implementing-convertfrom"></a>ConvertFrom 구현  
 XAML을 지원하는 <xref:System.ComponentModel.TypeConverter> 구현으로 사용하려면 해당 변환기에 대한 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 메서드에서 문자열을 `value` 매개 변수로 허용해야 합니다. 문자열이 올바른 형식이고 <xref:System.ComponentModel.TypeConverter> 구현으로 변환할 수 있는 경우 반환된 개체가 속성에 필요한 형식으로 캐스트를 지원해야 합니다. 그렇지 않은 경우 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 구현에서 `null`을 반환해야 합니다.  
  
 각 <xref:System.ComponentModel.TypeConverter> 구현에서는 변환에 유효한 문자열을 구성하는 항목을 고유하게 해석할 수 있으며 매개 변수로 전달되는 문화권 컨텍스트나 형식 설명을 사용하거나 무시할 수도 있습니다. 그러나 WPF XAML 처리에서 모든 경우의 형식 설명 컨텍스트에 값을 전달할 수는 없으며 `xml:lang`에 기반을 둔 문화권을 전달할 수도 없습니다.  
  
> [!NOTE]
> 중괄호 ({}), 특히 여는 중괄호 ({)를 문자열 형식의 요소로 사용 하지 마세요. 이러한 문자는 태그 확장 시퀀스의 시작 및 종료로 예약되어 있습니다.  
  
 형식 변환기가 .NET Framework XAML 서비스 개체 작성기에서 XAML 서비스에 액세스할 수 있어야 하지만 컨텍스트에 대한 <xref:System.IServiceProvider.GetService%2A> 호출에서 해당 서비스를 반환하지 않는 경우 예외를 throw하는 것이 적합합니다.  
  
### <a name="implementing-convertto"></a>ConvertTo 구현  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 는 serialization 지원에 잠재적으로 사용됩니다. <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 를 통해 사용자 지정 형식 및 해당 형식 변환기에 대해 Serialization을 지원하는 것은 절대적인 요구 사항이 아닙니다. 그러나 컨트롤을 구현하거나 클래스의 디자인 또는 기능의 일부로 serialization을 사용하는 경우에는 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>를 구현해야 합니다.  
  
 XAML을 지원하는 <xref:System.ComponentModel.TypeConverter> 구현으로 사용하려면 해당 변환기에 대한 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 메서드에서 `value` 매개 변수로 지원되는 형식(또는 값)의 인스턴스를 허용해야 합니다. `destinationType` 매개 변수가 <xref:System.String>형식인 경우 반환된 개체는 <xref:System.String>으로 캐스트될 수 있어야 합니다. 반환된 문자열은 `value`의 직렬화된 값을 나타내야 합니다. 이상적으로 선택한 serialization 형식은 해당 문자열이 동일한 변환기의 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 구현에 전달된 경우와 동일한 값을 생성할 수 있어야 하며 정보가 크게 손실되지 않아야 합니다.  
  
 값을 직렬화할 수 없거나 변환기에서 serialization을 지원하지 않는 경우 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 구현은 `null` 을 반환하고 예외를 throw할 수 있습니다. 그러나 예외를 throw하는 경우에는 먼저 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 를 확인하여 예외를 방지하는 가장 좋은 방법이 지원되도록 해당 변환을 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 구현의 일부로 사용할 수 없음을 보고해야 합니다.  
  
 `destinationType` 매개 변수가 <xref:System.String>형식이 아닌 경우 고유한 변환기 처리를 선택할 수 있습니다. 일반적으로 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 에서 특정 예외를 발생시키는 기본 구현 처리로 돌아갑니다.  
  
 형식 변환기가 .NET Framework XAML 서비스 개체 작성기에서 XAML 서비스에 액세스할 수 있어야 하지만 컨텍스트에 대한 <xref:System.IServiceProvider.GetService%2A> 호출에서 해당 서비스를 반환하지 않는 경우 예외를 throw하는 것이 적합합니다.  
  
### <a name="implementing-canconvertfrom"></a>CanConvertFrom 구현  
 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 구현은 `true` 형식의 `sourceType` 에 대해 <xref:System.String> 를 반환하고, 그렇지 않은 경우 기본 구현에서 결정합니다. <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>에서 예외를 throw하지 않습니다.  
  
### <a name="implementing-canconvertto"></a>CanConvertTo 구현  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 구현은 `true` 형식의 `destinationType` 에 대해 <xref:System.String>를 반환하고, 그렇지 않은 경우 기본 구현에서 결정합니다. <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>에서 예외를 throw하지 않습니다.  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## <a name="applying-the-typeconverterattribute"></a>TypeConverterAttribute 적용  
 사용자 지정 형식 변환기를 .NET Framework XAML 서비스를 통해 사용자 지정 클래스에 대해 작동 하는 형식 변환기로 사용 하려면를 클래스 정의 <xref:System.ComponentModel.TypeConverterAttribute> 에 적용 해야 합니다. 특성을 통해 지정하는 <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> 은 사용자 지정 형식 변환기의 형식 이름이어야 합니다. XAML 프로세서에서 속성 형식이 사용자 지정 클래스 형식을 사용하는 값을 처리할 때 이 특성을 적용하면 문자열을 입력하고 개체 인스턴스를 반환할 수 있습니다.  
  
 또한 속성별로 형식 변환기를 제공할 수 있습니다. 를 <xref:System.ComponentModel.TypeConverterAttribute> 클래스 정의에 적용 하는 대신 속성 정의 (기본 정의는 포함 `get` / `set` 되지 않음)에 적용 합니다. 속성의 형식은 사용자 지정 형식 변환기에서 처리되는 형식과 일치해야 합니다. XAML 프로세서에서 해당 속성의 값을 처리할 때 이 특성을 적용하면 입력 문자열을 처리하고 개체 인스턴스를 반환할 수 있습니다. Microsoft .NET Framework의 속성 형식 또는 클래스 정의를 제어할 수 없고 클래스 정의를 적용할 <xref:System.ComponentModel.TypeConverterAttribute> 수 없는 일부 다른 라이브러리에서 속성 형식을 사용 하도록 선택 하는 경우에는 속성 형식 변환기 기술이 특히 유용 합니다.  
  
 연결된 사용자 지정 멤버에 형식 변환 동작을 제공하려면 연결된 멤버에 대한 구현 패턴의 <xref:System.ComponentModel.TypeConverterAttribute> 접근자 메서드에 `Get` 를 적용합니다.  
  
<a name="accessing_service_provider_context_from_a_markup_extension_implementation"></a>   
## <a name="accessing-service-provider-context-from-a-markup-extension-implementation"></a>태그 확장 구현에서 서비스 공급자 컨텍스트 액세스  
 사용 가능한 서비스는 모든 값 변환기에서 동일합니다. 차이점은 각 값 변환기에서 서비스 컨텍스트를 수신하는 방법입니다. 서비스 액세스 및 사용 가능한 서비스는 [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)항목에 설명되어 있습니다.  
  
<a name="type_converters_in_the_xaml_node_stream"></a>   
## <a name="type-converters-in-the-xaml-node-stream"></a>XAML 노드 스트림의 형식 변환기  
 XAML 노드 스트림을 사용하여 작업하는 경우 형식 변환기의 동작 또는 최종 결과가 아직 실행되지 않습니다. 로드 경로에서 로드하기 위해 결국 형식 변환이 필요한 특성 문자열은 시작 멤버 및 종료 멤버 내에서 텍스트 값으로 유지됩니다. 결국 이 작업에 필요한 형식 변환기는 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=nameWithType> 속성을 사용하여 확인할 수 있습니다. 그러나 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=nameWithType>에서 유효한 값을 가져오려면 기본 멤버를 통해 이러한 정보에 액세스할 수 있는 XAML 스키마 컨텍스트 또는 멤버에서 사용하는 개체 값의 형식을 사용해야 합니다. 또한 형식 변환 동작을 호출하려면 형식 매핑이 필요하고 변환기 인스턴스를 만들어야 하므로 XAML 스키마 컨텍스트가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ComponentModel.TypeConverterAttribute>
- [XAML을 위한 형식 변환기 및 태그 확장명](type-converters-and-markup-extensions-for-xaml.md)
- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
