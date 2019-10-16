---
title: 공용 XAML 언어 기본 형식에 대한 기본 제공 형식
ms.date: 03/30/2017
helpviewer_keywords:
- XAML language primitives [XAML Services]
- XAML [XAML Services], built-in types
- x:String [XAML Services]
- x:TimeSpan [XAML Services]
- x:Byte [XAML Services]
- x:Double [XAML Services]
- XAML [XAML Services], types
- x:Uri [XAML Services]
- XAML built-in types [XAML Services]
- x:Int64 [XAML Services]
- x:Single [XAML Services]
- x:Int32 [XAML Services]
ms.assetid: 11de2f08-5b95-4989-b5ec-5178eb968184
ms.openlocfilehash: 85fd0c04a40b9de64979e4da1459dbf8953a93bf
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053888"
---
# <a name="built-in-types-for-common-xaml-language-primitives"></a>공용 XAML 언어 기본 형식에 대한 기본 제공 형식
XAML 2009에서는 CLR(공용 언어 런타임) 및 다른 프로그래밍 언어에서 자주 사용되는 기본 형식인 여러 가지 데이터 형식에 대해 XAML 언어 수준 지원을 제공합니다. XAML 2009는 `x:Object`, `x:Boolean`, `x:Char`, `x:String`, `x:Decimal`, `x:Single`, `x:Double`, `x:Int16`, `x:Int32`, `x:Int64`, `x:TimeSpan`, `x:Uri`, `x:Byte`및 `x:Array`같은 기본 형식에 대한 지원을 추가합니다.  
  
<a name="previous_techniques_for_language_primitives_in_xaml_markup"></a>   
## <a name="previous-techniques-for-language-primitives-in-xaml-markup"></a>XAML 태그의 언어 기본 형식에 대한 이전 기술  
 이전 WPF 버전에 대한 XAML에서는 .NET Framework에 대한 CLR 기본 형식 정의 클래스가 포함된 어셈블리 및 네임스페이스를 매핑하여 CLR 언어 기본 형식을 참조할 수 있습니다. 대부분이 mscorlib 어셈블리 및 <xref:System> 네임스페이스에 있습니다. 예를 들어 <xref:System.Int32>를 사용하려면 다음에 표시된 사용 예제를 사용하여 다음과 같은 매핑을 선언할 수 있습니다.  
  
```xaml  
<Application xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"   
xmlns:sys="clr-namespace:System;assembly=mscorlib">  
  <Application.Resources>  
    <sys:Int32 x:Key="intMeaning">42</sys:Int32>  
  </Application.Resources>  
</Application>  
```  
  
<a name="xaml_2009_language_primitives"></a>   
## <a name="xaml-2009-language-primitives"></a>XAML 2009 언어 기본 형식  
 규칙에 따라 `x:` 접두사를 포함하여 XAML 및 다른 모든 XAML 언어 요소에 대한 언어 기본 형식이 표시됩니다. 이 규칙은 XAML 언어 요소가 실제 태그에서 일반적으로 사용되는 방식입니다. WPF의 XAML에 대한 개념 설명서 및 XAML 사양에서도 이 규칙을 따릅니다.  
  
### <a name="xobject"></a>x:Object  
 CLR 백업의 경우 `x:Object` 기본 형식은 <xref:System.Object>에 해당합니다.  
  
 이 기본 형식은 일반적으로 애플리케이션 태그에서 사용되지 않지만 XAML 형식 시스템에서 할당 가능성을 확인하는 경우와 같은 일부 시나리오에는 유용할 수 있습니다.  
  
### <a name="xboolean"></a>x:Boolean  
 CLR 백업의 경우 `x:Boolean` 기본 형식은 <xref:System.Boolean>에 해당합니다.  
  
 XAML은 `x:Boolean`에 대한 값을 대/소문자 구분 없이 구문 분석합니다. 이때 `x:Bool` 로 대체할 수 없습니다. Xaml 언어 사양 정의에 대해서는 [ \[5.2.17 및 5.4.11를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xchar"></a>x:Char  
 CLR 백업의 경우 `x:Char` 기본 형식은 <xref:System.Char>에 해당합니다.  
  
 String 및 char 형식은 XML 수준에서 파일의 전체 인코딩과 상호 작용합니다. Xaml 언어 사양 정의에 대해서는 [ \[5.2.7 및 5.4.1를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xstring"></a>x:String  
 CLR 백업의 경우 `x:String` 기본 형식은 <xref:System.String>에 해당합니다.  
  
 String 및 char 형식은 XML 수준에서 파일의 전체 인코딩과 상호 작용합니다. Xaml 언어 사양 정의에 대해서는 [ \[5.2.6\] 섹션](https://go.microsoft.com/fwlink/?LinkId=114525)을 참조 하세요.  
  
### <a name="xdecimal"></a>x:Decimal  
 CLR 백업의 경우 `x:Decimal` 기본 형식은 <xref:System.Decimal>에 해당합니다.  
  
 XAML 구문 분석은 기본적으로 `en-US` 문화권에 따라 수행됩니다. `en-US` 문화권에서 10진수의 구성 요소에 올바른 구분 기호는 개발 환경의 문화권 설정이나 런타임에 XAML이 로드되는 최종 클라이언트 대상에 관계없이 항상 마침표(`.`)입니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.14 및 5.4.8를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xsingle"></a>x:Single  
 CLR 백업의 경우 `x:Single` 기본 형식은 <xref:System.Single>에 해당합니다.  
  
 숫자 값뿐만 아니라 `x:Single`에 대한 텍스트 구문도 `Infinity`, `-Infinity` 및 `NaN` 토큰을 허용합니다. 이러한 토큰은 대/소문자를 구분하여 처리됩니다.  
  
 텍스트 구문의 첫 번째 문자가`x:Single` 또는 `e` 인 경우 `E`은 과학적 표기법 형식의 값을 지원할 수 있습니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.8 및 5.4.2를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xdouble"></a>x:Double  
 CLR 백업의 경우 `x:Double` 기본 형식은 <xref:System.Double>에 해당합니다.  
  
 숫자 값뿐만 아니라 `x:Double`에 대한 텍스트 구문도 `Infinity`, `-Infinity` 및 `NaN` 토큰을 허용합니다. 이러한 토큰은 대/소문자를 구분하여 처리됩니다.  
  
 `x:Double` 은 과학적 표기법 형식의 값을 지원할 수 있습니다. `e` 또는 `E` 문자를 사용하여 지수 부분을 나타냅니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.9 및 5.4.3를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xint16"></a>x:Int16  
 CLR 백업의 경우 `x:Int16` 기본 형식은 <xref:System.Int16> 에 해당하고 `x:Int16` 은 부호가 있는 것으로 처리됩니다. XAML에서는 텍스트 구문에 더하기(`+`) 부호가 없으면 부호 있는 양수 값을 의미합니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.11 및 5.4.5를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xint32"></a>x:Int32  
 CLR 백업의 경우 `x:Int32` 기본 형식은 <xref:System.Int32>에 해당합니다. `x:Int32`는 부호가 있는 것으로 처리됩니다. XAML에서는 텍스트 구문에 더하기(`+`) 부호가 없으면 부호 있는 양수 값을 의미합니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.12 및 5.4.6를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xint64"></a>x:Int64  
 CLR 백업의 경우 `x:Int64` 기본 형식은 <xref:System.Int64>에 해당합니다. `x:Int64`는 부호가 있는 것으로 처리됩니다. XAML에서는 텍스트 구문에 더하기(`+`) 부호가 없으면 부호 있는 양수 값을 의미합니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.13 및 5.4.7를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xtimespan"></a>x:TimeSpan  
 CLR 백업의 경우 `x:TimeSpan` 기본 형식은 <xref:System.TimeSpan>에 해당합니다.  
  
 날짜/시간 형식에 대한 XAML 구문 분석은 기본적으로 `en-US` 문화권에 따라 수행됩니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.16 및 5.4.10를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xuri"></a>x:Uri  
 CLR 백업의 경우 `x:Uri` 기본 형식은 <xref:System.Uri>에 해당합니다.  
  
 프로토콜 확인은 `x:Uri`에 대한 XAML 정의의 일부가 아닙니다.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.15 및 5.4.9를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xbyte"></a>x:Byte  
 CLR 백업의 경우 `x:Byte` 기본 형식은 <xref:System.Byte>에 해당합니다. 는 <xref:System.Byte> unsigned로처리`x:Byte` 됩니다.  /   
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.10 및 5.4.4를\] ](https://go.microsoft.com/fwlink/?LinkId=114525)참조 하세요.  
  
### <a name="xarray"></a>x:Array  
 CLR 백업의 경우 `x:Array` 기본 형식은 <xref:System.Array>에 해당합니다.  
  
 XAML 2006에서는 태그 확장 구문을 사용하여 배열을 정의할 수 있습니다. 그러나 XAML 2009 구문은 태그 확장에 액세스할 필요가 없는 언어로 정의된 기본 형식입니다. XAML 2006 지원에 대한 자세한 내용은 [x:Array Markup Extension](x-array-markup-extension.md)을 참조하세요.  
  
 Xaml 언어 사양 정의에 대해서는 [ \[5.2.18\] 섹션](https://go.microsoft.com/fwlink/?LinkId=114525)을 참조 하세요.  
  
<a name="wpf_support"></a>   
## <a name="wpf-support"></a>WPF 지원  
 WPF에서 XAML 2009 기능을 사용할 수 있지만 태그로 컴파일되지 않은 XAML에만 사용할 수 있습니다. WPF에 대한 태그로 컴파일된 XAML 및 BAML 형식의 XAML은 현재 XAML 2009 키워드 및 기능을 지원하지 않습니다.  
  
 WPF와 함께 XAML 2009 기능을 사용할 수 있는 시나리오는 느슨한 XAML을 작성한 다음 <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType>를 사용하여 해당 XAML을 WPF 런타임 및 개체 그래프로 로드하는 경우입니다. WPF <xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType> 및 해당 <xref:System.Windows.Markup.XamlReader.Load%2A> 는 XAML 2009 언어 키워드 및 기능을 유효한 개체 그래프 표현으로 처리할 수 있습니다.
