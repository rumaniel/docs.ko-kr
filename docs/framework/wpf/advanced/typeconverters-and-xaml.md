---
title: TypeConverter 및 XAML
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], TypeConverter class
ms.assetid: f6313e4d-e89d-497d-ac87-b43511a1ae4b
ms.openlocfilehash: 8c39fe75eea5042657cab533a0a557d966802a1b
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169014"
---
# <a name="typeconverters-and-xaml"></a>TypeConverter 및 XAML
이 항목에서는 문자열에서 형식 변환의 용도를 일반 XAML 언어 기능으로 소개합니다. .NET Framework에서 클래스는 <xref:System.ComponentModel.TypeConverter> XAML 특성 사용에서 속성 값으로 사용할 수 있는 관리 되는 사용자 지정 클래스에 대 한 구현의 일부로 특정 용도를 제공 합니다. 사용자 지정 클래스를 작성 하는 경우 클래스의 인스턴스를 XAML 설정 가능한 특성 값으로 사용할 수 있도록 하려면 클래스 <xref:System.ComponentModel.TypeConverterAttribute> 에를 적용 하거나 사용자 지정 <xref:System.ComponentModel.TypeConverter> 클래스를 작성 하거나 둘 다를 수행 해야 할 수 있습니다.  

## <a name="type-conversion-concepts"></a>형식 변환 개념  
  
### <a name="xaml-and-string-values"></a>XAML 및 문자열 값  
 XAML 파일에서 특성 값을 설정하는 경우 해당 값의 초기 형식은 일반 텍스트의 문자열입니다. 같은 <xref:System.Double> 다른 기본 형식도 처음에는 XAML 프로세서에 대 한 텍스트 문자열입니다.  
  
 XAML 프로세서에서 특성 값을 처리하려면 두 가지 정보가 필요합니다. 첫 번째 정보는 설정되는 속성의 값 형식입니다. 특성 값을 정의하고 XAML에서 처리되는 모든 문자열은 결국 해당 형식의 값으로 변환되거나 확인되어야 합니다. 값이 숫자 값과 같이 XAML 파서에서 인식되는 기본 형식인 경우 문자열의 직접 변환이 시도됩니다. 값이 열거형인 경우에는 문자열은 이름이 해당 열거형에 명명된 상수와 일치하는지 확인하는 데 사용됩니다. 값이 파서에서 인식되는 기본 형식이나 열거형이 아닌 경우 해당 형식은 변환된 문자열에 따라 형식의 인스턴스나 값을 제공할 수 있어야 합니다. 이렇게 하려면 형식 변환기 클래스를 지정합니다. 실제로 형식 변환기는 XAML 시나리오와 .NET 코드의 코드 호출에서 다른 클래스의 값을 제공하기 위한 도우미 클래스입니다.  
  
### <a name="using-existing-type-conversion-behavior-in-xaml"></a>XAML에서 기존 형식 변환 동작 사용  
 기본 XAML 개념에 대한 숙련도에 따라 자신도 모르게 기본 애플리케이션 XAML에서 형식 변환 동작을 이미 사용하고 있을 수 있습니다. 예를 들어 WPF는 형식 <xref:System.Windows.Point>값을 사용 하는 수백 개의 속성을 정의 합니다. 는 <xref:System.Windows.Point> 2 차원 좌표 공간의 좌표를 설명 하는 값 이며, 실제 <xref:System.Windows.Point.X%2A> 속성은 및 <xref:System.Windows.Point.Y%2A>뿐입니다. XAML에서 point를 지정 하는 경우 사용자가 제공 하는 <xref:System.Windows.Point.X%2A> 및 <xref:System.Windows.Point.Y%2A> 값 사이에 구분 기호 (일반적으로 쉼표)가 포함 된 문자열로 지정 합니다. 예: `<LinearGradientBrush StartPoint="0,0" EndPoint="1,1"/>`  
  
 이러한 단순 형식 <xref:System.Windows.Point> 및 XAML에서의 간단한 사용에도 형식 변환기가 포함 됩니다. 이 경우는 클래스 <xref:System.Windows.PointConverter>입니다.  
  
 클래스 수준에서 정의 <xref:System.Windows.Point> 된에 대 한 형식 변환기는에서 사용 하는 모든 속성의 <xref:System.Windows.Point>태그 사용을 간소화 합니다. 형식 변환기를 사용하지 않을 경우 위에 나온 동일한 예제에 훨씬 더 자세한 다음과 같은 태그가 필요합니다.  

```xaml
<LinearGradientBrush>
  <LinearGradientBrush.StartPoint>
    <Point X="0" Y="0"/>
  </LinearGradientBrush.StartPoint>
  <LinearGradientBrush.EndPoint>
    <Point X="1" Y="1"/>
  </LinearGradientBrush.EndPoint>
</LinearGradientBrush>
 ```
  
 형식 변환 문자열을 사용할지 보다 자세한 해당 구문을 사용할지 여부는 일반적으로 코딩 스타일에 따라 선택됩니다. XAML 도구 워크플로도 값 설정 방법에 영향을 줄 수 있습니다. 일부 XAML 도구는 디자이너 뷰 또는 고유한 serialization 메커니즘을 더 쉽게 왕복하기 때문에 가장 자세한 형식의 태그를 내보내는 경향이 있습니다.  
  
 기존 형식 변환기는 적용 <xref:System.ComponentModel.TypeConverterAttribute>된이 있는지 여부에 대 한 클래스 (또는 속성)를 검사 하 여 일반적으로 WPF 및 .NET Framework 형식에서 검색할 수 있습니다. 이 특성은 XAML 용도 및 기타 가능한 용도에서 해당 형식의 값을 지원하는 형식 변환기인 클래스의 이름을 지정합니다.  
  
### <a name="type-converters-and-markup-extensions"></a>형식 변환기 및 태그 확장명  
 태그 확장 및 형식 변환기는 적용되는 시나리오 및 XAML 프로세서 동작 측면에서 직교 역할을 채웁니다. 태그 확장명 사용에 컨텍스트를 사용할 수는 있지만 태그 확장에서 값을 제공하는 속성의 형식 변환 동작은 일반적으로 태그 확장명 구현에서 확인되지 않습니다. 즉, 태그 확장에서 텍스트 문자열을 해당 `ProvideValue` 출력으로 반환하는 경우에도 특정 속성이나 속성 값 형식에 적용될 때 해당 문자열의 형식 변환 동작은 호출되지 않습니다. 일반적으로 태그 확장의 목적은 문자열을 처리하고 관련된 형식 변환기 없이 개체를 반환하는 것입니다.  
  
 형식 변환기가 아니라 태그 확장이 필요한 일반적인 상황은 이미 존재하는 개체에 대한 참조를 만드는 경우입니다. 기껏해야 상태 비저장 형식 변환기만 새 인스턴스를 생성할 수 있으며, 이는 바람직하지 않을 수 있습니다. 태그 확장에 대한 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
### <a name="native-type-converters"></a>네이티브 형식 변환기  
 XAML 파서의 WPF 및 .NET Framework 구현에는 네이티브 형식 변환 처리를 사용하는 특정 형식이 있지만 일반적으로 이 형식은 기본 형식으로 간주되지 않습니다. 이러한 형식의 예로는 <xref:System.DateTime>이 있습니다. 이에 대 한 이유는 .NET Framework 아키텍처가 작동 하는 방식에 따라 달라 <xref:System.DateTime> 집니다. 형식은 mscorlib, .net의 가장 기본적인 라이브러리에 정의 되어 있습니다. <xref:System.DateTime>는 종속성을 도입 하는 다른 어셈블리에서 제공 되는 특성을 사용 하는 것으로<xref:System.ComponentModel.TypeConverterAttribute> 허용 되지 않습니다 (시스템에서). 따라서 특성에 따라 일반적인 형식 변환기 검색 메커니즘을 지원할 수 없습니다. 대신 XAML 파서에 이러한 네이티브 처리가 필요한 형식 목록이 있으며 실제 기본 형식이 처리되는 방법과 유사한 방법으로 이러한 형식을 처리합니다. 의 <xref:System.DateTime> 경우에 대 한 <xref:System.DateTime.Parse%2A>호출이 포함 됩니다.  
  
<a name="Implementing_a_Type_Converter"></a>   
## <a name="implementing-a-type-converter"></a>형식 변환기 구현  
  
### <a name="typeconverter"></a>TypeConverter  
 이전에 제공 된 <xref:System.Windows.PointConverter> 예제에서는클래스를언급했습니다.<xref:System.Windows.Point> XAML의 .NET 구현에서 XAML 용도에 사용 되는 모든 형식 변환기는 기본 클래스 <xref:System.ComponentModel.TypeConverter>에서 파생 되는 클래스입니다. 클래스 <xref:System.ComponentModel.TypeConverter> 는 XAML이 존재 하기 이전의 .NET Framework 버전에 있었지만, 원래 용도 중 하나는 비주얼 디자이너의 속성 대화 상자에 대 한 문자열 변환을 제공 하는 것입니다. XAML의 경우 문자열 특성 값 <xref:System.ComponentModel.TypeConverter> 의 구문 분석을 가능 하 게 하 고, 특정 개체 속성의 런타임 값을에 대 한 문자열에 다시 처리할 수 있는 문자열 변환의 기본 클래스가 포함 되도록의 역할이 확장 됩니다. 특성으로 직렬화 합니다.  
  
 <xref:System.ComponentModel.TypeConverter>는 XAML 처리를 위해 문자열과의 변환과 관련 된 네 가지 멤버를 정의 합니다.  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 이러한 방법 중 가장 중요 한 메서드 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>는입니다. 이 메서드는 입력 문자열을 필요한 개체 형식으로 변환합니다. 엄격 하 게 말해서 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> , 메서드를 구현 하 여 훨씬 더 광범위 한 형식을 변환기의 의도 된 대상 형식으로 변환 하 고 런타임 변환과 같이 xaml 이상으로 확장 하는 용도로 사용할 수 있습니다. 중요 한 입력을 <xref:System.String> 처리할 수 있는 코드 경로입니다.  
  
 다음으로 가장 중요 한 메서드 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>는입니다. 응용 프로그램을 태그 표현으로 변환 하는 경우 (예를 들어 XAML에 파일로 저장 하는 경우) <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 는 태그 표현을 생성 해야 합니다. 이 경우 XAML에 중요 한 코드 경로는의 `destinationType` <xref:System.String> 를 전달 하는 경우입니다.  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 및 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 은 서비스에서 <xref:System.ComponentModel.TypeConverter> 구현의 기능을 쿼리할 때 사용되는 지원 메서드입니다. 변환기의 동일한 변환 메서드에서 지원하는 형식 관련 케이스에 대해 `true` 를 반환하려면 이러한 메서드를 구현해야 합니다. XAML 용도에서는 일반적으로 <xref:System.String> 형식을 의미합니다.  
  
### <a name="culture-information-and-type-converters-for-xaml"></a>XAML에 대한 문화권 정보 및 형식 변환기  
 각 <xref:System.ComponentModel.TypeConverter> 구현에서는 변환에 유효한 문자열을 구성 하는 항목을 고유 하 게 해석할 수 있으며 매개 변수로 전달 되는 형식 설명을 사용 하거나 무시할 수도 있습니다. 문화권 및 XAML 형식 변환과 관련하여 중요한 고려 사항이 있습니다. XAML에서는 지역화 가능 문자열을 특성 값으로 사용할 수 있습니다. 그러나 해당 지역화 가능 문자열을 특정 문화권 요구 사항이 있는 형식 변환기 입력으로 사용할 수는 없습니다. XAML 특성 값에 대한 형식 변환기에는 `en-US` 문화권을 사용하는 고정 언어 구문 분석 동작이 반드시 포함되기 때문입니다. 이러한 제한의 디자인상 이유에 대한 자세한 내용은 XAML 언어 사양([\[MS-XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525))을 참조하세요.  
  
 문화권이 문제가 될 수 있는 경우에 대한 예로 일부 문화권에서는 숫자에 대한 소수점 구분 기호로 쉼표를 사용합니다. 이러한 사용은 일반적인 X,Y 형식이나 쉼표로 구분된 목록 같은 역사적 선례에 따라 쉼표를 구분 기호로 사용하는 많은 WPF XAML 형식 변환기의 동작과 충돌합니다. 주변 XAML에서 `Language` 또는 `xml:lang`을 `sl-SI` 문화권(이런 식으로 소수점에 쉼표를 사용하는 문화권의 예)으로 설정하여 문화권을 전달해도 문제가 해결되지 않습니다.  
  
### <a name="implementing-convertfrom"></a>ConvertFrom 구현  
 XAML을 지원하는 <xref:System.ComponentModel.TypeConverter> 구현으로 사용하려면 해당 변환기에 대한 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 메서드에서 문자열을 `value` 매개 변수로 허용해야 합니다. 문자열이 올바른 형식이 고 <xref:System.ComponentModel.TypeConverter> 구현으로 변환할 수 있는 경우 반환 된 개체가 속성에 필요한 형식으로 캐스트를 지원 해야 합니다. 그렇지 않은 경우 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 구현에서 `null`을 반환해야 합니다.  
  
 각 <xref:System.ComponentModel.TypeConverter> 구현에서는 변환에 유효한 문자열을 구성 하는 항목을 고유 하 게 해석할 수 있으며, 매개 변수로 전달 된 형식 설명 또는 문화권 컨텍스트를 사용 하거나 무시할 수도 있습니다. 그러나 WPF XAML 처리에서 모든 경우의 형식 설명 컨텍스트에 값을 전달할 수는 없으며 `xml:lang`을 기반으로 하는 문화권을 전달할 수도 없습니다.  
  
> [!NOTE]
> 중괄호 문자, 특히 {를 문자열 형식의 가능한 요소로 사용하지 마세요. 이러한 문자는 태그 확장명 시퀀스의 시작 및 종료로 예약되어 있습니다.  
  
### <a name="implementing-convertto"></a>ConvertTo 구현  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 는 serialization 지원에 잠재적으로 사용됩니다. <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 를 통해 사용자 지정 형식 및 해당 형식 변환기에 대해 Serialization을 지원하는 것은 절대적인 요구 사항이 아닙니다. 그러나 컨트롤을 구현하거나 클래스의 디자인 또는 기능의 일부로 serialization을 사용하는 경우에는 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>를 구현해야 합니다.  
  
 XAML <xref:System.ComponentModel.TypeConverter> 을지`value` 원하는 구현으로 사용 하려면 해당 변환기에 대 한 메서드에서매개변수로지원되는형식(또는값)의인스턴스를허용해야합니다.<xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 매개 변수가 형식인 <xref:System.String>경우 반환 된 개체를로 <xref:System.String>캐스팅할 수 있어야 합니다. `destinationType` 반환된 문자열은 `value`의 직렬화된 값을 나타내야 합니다. 이상적인 정보 손실 없이 동일한 변환기의 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 구현에 문자열이 전달 된 경우 선택 하는 serialization 형식은 동일한 값을 생성할 수 있어야 합니다.  
  
 값을 serialize 할 수 없거나 변환기에서 serialization을 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 지원 하지 않는 경우 구현은을 반환 `null`해야 하며이 경우 예외를 throw 할 수 있습니다. 그러나 예외를 throw 하는 경우에는 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 먼저를 사용 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 하 여 예외를 방지 하기 위해를 확인 하는 것이 좋습니다.  
  
 매개 `destinationType` 변수가 형식이 <xref:System.String>아닌 경우 고유한 변환기 처리를 선택할 수 있습니다. 일반적으로 basemost <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 은 특정 예외를 발생 시키는 기본 구현 처리로 돌아갑니다.  
  
### <a name="implementing-canconvertto"></a>CanConvertTo 구현  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 구현은 `true` 형식의 `destinationType` 에 대해 <xref:System.String>를 반환하고, 그렇지 않은 경우 기본 구현에서 결정합니다.  
  
### <a name="implementing-canconvertfrom"></a>CanConvertFrom 구현  
 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 구현은 <xref:System.String> 형식의 `sourceType`에 대해 `true`를 반환하고, 그렇지 않은 경우 기본 구현에서 결정합니다.  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## <a name="applying-the-typeconverterattribute"></a>TypeConverterAttribute 적용  
 사용자 지정 형식 변환기를 XAML 프로세서에서 사용자 지정 클래스에 대해 작동 하는 형식 변환기로 사용 하려면를 클래스 정의 <xref:System.ComponentModel.TypeConverterAttribute> 에 적용 해야 합니다. 특성을 통해 지정하는 <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> 은 사용자 지정 형식 변환기의 형식 이름이어야 합니다. XAML 프로세서에서 속성 형식이 사용자 지정 클래스 형식을 사용하는 값을 처리할 때 이 특성을 적용하면 문자열을 입력하고 개체 인스턴스를 반환할 수 있습니다.  
  
 또한 속성별로 형식 변환기를 제공할 수 있습니다. 를 <xref:System.ComponentModel.TypeConverterAttribute> 클래스 정의에 적용 하는 대신 속성 정의 (기본 정의는 포함 `get` / `set` 되지 않음)에 적용 합니다. 속성의 형식은 사용자 지정 형식 변환기에서 처리되는 형식과 일치해야 합니다. XAML 프로세서에서 해당 속성의 값을 처리할 때 이 특성을 적용하면 입력 문자열을 처리하고 개체 인스턴스를 반환할 수 있습니다. Microsoft .NET Framework의 속성 형식 또는 클래스 정의를 제어할 수 없고 클래스 정의를 적용할 <xref:System.ComponentModel.TypeConverterAttribute> 수 없는 일부 다른 라이브러리에서 속성 형식을 사용 하도록 선택 하는 경우에는 속성 형식 변환기 기술이 특히 유용 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ComponentModel.TypeConverter>
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [XAML 구문 정보](xaml-syntax-in-detail.md)
