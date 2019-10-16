---
title: 표준 TimeSpan 서식 문자열
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- format specifiers, standard time interval
- format strings
- standard time interval format strings
- standard format strings, time intervals
- format specifiers, time intervals
- time intervals [.NET Framework], formatting
- time [.NET Framework], formatting
- formatting [.NET Framework], time
- standard TimeSpan format strings
- formatting [.NET Framework], time intervals
ms.assetid: 9f6c95eb-63ae-4dcc-9c32-f81985c75794
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bc2ca7a94ffb19f62f354bdfc3040490b57e2689
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968545"
---
# <a name="standard-timespan-format-strings"></a>표준 TimeSpan 서식 문자열
<a name="Top"></a> 표준 <xref:System.TimeSpan> 형식 문자열은 단일 형식 지정자를 사용하여 서식 지정 작업으로 생성되는 <xref:System.TimeSpan> 값의 텍스트 표현을 정의합니다. 공백을 포함하여 문자가 두 개 이상 포함된 형식 문자열은 사용자 지정 <xref:System.TimeSpan> 형식 문자열로 해석됩니다. 자세한 내용은 [사용자 지정 TimeSpan 서식 문자열](../../../docs/standard/base-types/custom-timespan-format-strings.md)을 참조하세요.  
  
 <xref:System.TimeSpan> 값의 문자열 표현은 <xref:System.TimeSpan.ToString%2A?displayProperty=nameWithType>과 같이 복합 서식 지정을 지원하는 메서드 및 <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드의 오버로드 호출을 통해 생성됩니다. 자세한 내용은 [서식 지정 형식](../../../docs/standard/base-types/formatting-types.md) 및 [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md)을 참조하세요. 다음 예제에서는 서식 지정 작업에 표준 형식 문자열을 사용하는 방법을 보여 줍니다.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/formatexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/formatexample1.vb#2)]  
  
 표준 <xref:System.TimeSpan> 형식 문자열은 구문 분석 작업에 필요한 입력 문자열 서식을 정의하기 위해 <xref:System.TimeSpan.ParseExact%2A?displayProperty=nameWithType> 및 <xref:System.TimeSpan.TryParseExact%2A?displayProperty=nameWithType> 메서드에서도 사용됩니다. 구문 분석 시에는 값의 문자열 표현이 해당 값으로 변환됩니다. 다음 예제에서는 구문 분석 작업에 표준 형식 문자열을 사용하는 방법을 보여 줍니다.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/parseexample1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/parseexample1.vb#3)]  
  
<a name="top"></a> 다음 표에는 표준 시간 간격 형식 지정자가 나와 있습니다.  
  
|형식 지정자|name|설명|예제|  
|----------------------|----------|-----------------|--------------|  
|"c"|상수(고정) 형식|이 지정자는 문화권을 구분하지 않으며 형식은 `[-][d'.']hh':'mm':'ss['.'fffffff]`입니다.<br /><br /> "t" 및 "T" 형식 문자열은 같은 결과를 생성합니다.<br /><br /> 추가 정보: [상수("c") 형식 지정자](#Constant).|`TimeSpan.Zero` -> 00:00:00<br /><br /> `New TimeSpan(0, 0, 30, 0)` -> 00:30:00<br /><br /> `New TimeSpan(3, 17, 25, 30, 500)` -> 3.17:25:30.5000000|  
|"g"|일반 약식|이 지정자는 필요한 내용만 출력하고 문화권을 구분하며 형식은 `[-][d':']h':'mm':'ss[.FFFFFFF]`입니다.<br /><br /> 추가 정보: [일반 약식("g") 형식 지정자](#GeneralShort).|`New TimeSpan(1, 3, 16, 50, 500)` -> 1:3:16:50.5(en-US)<br /><br /> `New TimeSpan(1, 3, 16, 50, 500)` -> 1:3:16:50,5(fr-FR)<br /><br /> `New TimeSpan(1, 3, 16, 50, 599)` -> 1:3:16:50.599(en-US)<br /><br /> `New TimeSpan(1, 3, 16, 50, 599)` -> 1:3:16:50,599(fr-FR)|  
|"G"|일반 긴 형식|이 지정자는 항상 일 수와 7자리 소수 자릿수를 출력하고 문화권을 구분하며 형식은 `[-]d':'hh':'mm':'ss.fffffff`입니다.<br /><br /> 추가 정보: [일반 긴("G") 형식 지정자](#GeneralLong).|`New TimeSpan(18, 30, 0)` -> 0:18:30:00.0000000(en-US)<br /><br /> `New TimeSpan(18, 30, 0)` -> 0:18:30:00,0000000(fr-FR)|  
  
<a name="Constant"></a>   
## <a name="the-constant-c-format-specifier"></a>상수("c") 형식 지정자  
 "c" 형식 지정자는 <xref:System.TimeSpan> 값의 문자열 표현을 다음 형식으로 반환합니다.  
  
 [-][*d*.]*hh*:*mm*:*ss*[.*fffffff*]  
  
 대괄호 ([ 및 ]) 안의 요소는 선택적 요소입니다. 마침표(.)와 콜론(:)은 리터럴 기호입니다. 다음 표에서는 나머지 요소에 대해 설명합니다.  
  
|요소|설명|  
|-------------|-----------------|  
|*-*|음수 시간 간격을 나타내는 선택적 음수 기호입니다.|  
|*d*|앞에 오는 0이 없는 선택적 일 수입니다.|  
|*hh*|"00"부터 "23" 범위의 시간입니다.|  
|*mm*|"00"부터 "59" 범위의 분입니다.|  
|*ss*|"0"부터 "59" 범위의 초입니다.|  
|*fffffff*|선택적인 초의 소수 부분입니다.  값 범위는 "0000001"(틱 1개 또는 1천만 분의 1초)에서 "9999999"(9,999,999천만 분의 1초 또는 1초-틱 1개)까지입니다.|  
  
 "g" 및 "G" 형식 지정자와 달리 "c" 형식 지정자는 문화권을 구분하지 않으며, .NET Framework 4 이전의 모든 .NET Framework 버전에 공통적으로 적용되는 고정된 <xref:System.TimeSpan> 값의 문자열 표현을 생성합니다. “c”는 기본 <xref:System.TimeSpan> 형식 문자열입니다. 즉, <xref:System.TimeSpan.ToString?displayProperty=nameWithType> 메서드는 “c” 형식 문자열을 사용하여 시간 간격 값의 서식을 지정합니다.  
  
> [!NOTE]
> <xref:System.TimeSpan>은 "c" 표준 형식 문자열과 동작이 동일한 "t" 및 "T" 표준 형식 문자열도 지원합니다.  
  
 다음 예제에서는 두 <xref:System.TimeSpan> 개체를 인스턴스화한 다음 해당 개체를 사용하여 산술 연산을 수행하고 결과를 표시합니다. 각 경우에서는 복합 서식을 사용하여 "c" 형식 지정자를 통해 <xref:System.TimeSpan> 값을 표시합니다.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardc1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardc1.vb#1)]  
  
 [표로 이동](#Top)  
  
<a name="GeneralShort"></a>   
## <a name="the-general-short-g-format-specifier"></a>일반 약식("g") 형식 지정자  
 "g" <xref:System.TimeSpan> 형식 지정자는 필요한 요소만 포함하여 <xref:System.TimeSpan> 값의 문자열 표현을 압축 형식으로 반환합니다. 이 형식 지정자의 형식은 다음과 같습니다.  
  
 [-][*d*:]*h*:*mm*:*ss*[.*FFFFFFF*]  
  
 대괄호 ([ 및 ]) 안의 요소는 선택적 요소입니다. 콜론(:)은 리터럴 기호입니다. 다음 표에서는 나머지 요소에 대해 설명합니다.  
  
|요소|설명|  
|-------------|-----------------|  
|*-*|음수 시간 간격을 나타내는 선택적 음수 기호입니다.|  
|*d*|앞에 오는 0이 없는 선택적 일 수입니다.|  
|*h*|앞에 오는 0이 없는 "0"부터"23" 범위의 시간입니다.|  
|*mm*|"00"부터 "59" 범위의 분입니다.|  
|*ss*|"00"부터 "59" 범위의 초입니다.|  
|*.*|초 소수 구분 기호입니다. 사용자 재정의가 없는 지정한 문화권의 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> 속성과 같습니다.|  
|*FFFFFFF*|초의 소수 부분입니다. 최대한 적은 자릿수가 표시됩니다.|  
  
 "G" 형식 지정자와 마찬가지로 "g" 형식 지정자도 지역화됩니다. 해당 초 소수 구분 기호는 현재 문화권 또는 지정한 문화권의 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> 속성을 기준으로 합니다.  
  
 다음 예제에서는 두 <xref:System.TimeSpan> 개체를 인스턴스화한 다음 해당 개체를 사용하여 산술 연산을 수행하고 결과를 표시합니다. 각 경우에서는 복합 서식을 사용하여 "g" 형식 지정자를 통해 <xref:System.TimeSpan> 값을 표시합니다. 또한 현재 시스템 문화권(여기서는 영어 - 미국 또는 en-US) 및 프랑스어 - 프랑스(fr-FR) 문화권의 서식 규칙을 사용하여 <xref:System.TimeSpan> 값의 서식을 지정합니다.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardshort1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardshort1.vb#4)]  
  
 [표로 이동](#Top)  
  
<a name="GeneralLong"></a>   
## <a name="the-general-long-g-format-specifier"></a>일반 긴("G") 형식 지정자  
 "G" <xref:System.TimeSpan> 형식 지정자는 항상 일 수와 초의 소수 부분을 모두 포함하는 긴 형식으로 <xref:System.TimeSpan> 값의 문자열 표현을 반환합니다. "G" 표준 형식 지정자에서 생성 되는 문자열의 형식은 다음과 같습니다.  
  
 [-]*d*:*hh*:*mm*:*ss*.*fffffff*  
  
 대괄호 ([ 및 ]) 안의 요소는 선택적 요소입니다. 콜론(:)은 리터럴 기호입니다. 다음 표에서는 나머지 요소에 대해 설명합니다.  
  
|요소|설명|  
|-------------|-----------------|  
|*-*|음수 시간 간격을 나타내는 선택적 음수 기호입니다.|  
|*d*|앞에 오는 0이 없는 일 수입니다.|  
|*hh*|"00"부터 "23" 범위의 시간입니다.|  
|*mm*|"00"부터 "59" 범위의 분입니다.|  
|*ss*|"00"부터 "59" 범위의 초입니다.|  
|*.*|초 소수 구분 기호입니다. 사용자 재정의가 없는 지정한 문화권의 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> 속성과 같습니다.|  
|*fffffff*|초의 소수 부분입니다.|  
  
 "G" 형식 지정자와 마찬가지로 "g" 형식 지정자도 지역화됩니다. 해당 초 소수 구분 기호는 현재 문화권 또는 지정한 문화권의 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A> 속성을 기준으로 합니다.  
  
 다음 예제에서는 두 <xref:System.TimeSpan> 개체를 인스턴스화한 다음 해당 개체를 사용하여 산술 연산을 수행하고 결과를 표시합니다. 각 경우에서는 복합 서식을 사용하여 "G" 형식 지정자를 통해 <xref:System.TimeSpan> 값을 표시합니다. 또한 현재 시스템 문화권(여기서는 영어 - 미국 또는 en-US) 및 프랑스어 - 프랑스(fr-FR) 문화권의 서식 규칙을 사용하여 <xref:System.TimeSpan> 값의 서식을 지정합니다.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardlong1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardlong1.vb#5)]  
  
 [표로 이동](#Top)  
  
## <a name="see-also"></a>참고 항목

- [형식 서식 지정](../../../docs/standard/base-types/formatting-types.md)
- [사용자 지정 TimeSpan 서식 문자열](../../../docs/standard/base-types/custom-timespan-format-strings.md)
- [Parsing Strings](../../../docs/standard/base-types/parsing-strings.md)
