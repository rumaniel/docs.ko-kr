---
title: 형식 변환 함수(Visual Basic)
ms.date: 10/24/2018
f1_keywords:
- vb.CUShort
- vb.csng
- vb.CDate
- CByte
- CSng
- vb.CDec
- CBool
- CStr
- vb.CULng
- CDec
- CVErr
- CDbl
- CShort
- vb.CObj
- vb.CVErr
- CULng
- vb.cdbl
- vb.cbool
- CObj
- CDate
- CLng
- vb.cstr
- vb.cbyte
- vb.clng
- vb.CChar
- CUShort
- vb.CUInt
- vb.cint
- vb.CShort
- CInt
- CUInt
- CChar
helpviewer_keywords:
- CDate function
- CByte function
- Integer data type [Visual Basic], converting
- string conversion [Visual Basic], conversion functions
- fractions
- data types [Visual Basic], converting
- text, converting
- CDec function
- Char data type [Visual Basic], converting
- type conversion [Visual Basic], functions for
- Single data type [Visual Basic], converting
- numbers [Visual Basic], rounding
- rounding numbers [Visual Basic], type conversion
- CUShort function
- Long data type [Visual Basic], converting
- return values [Visual Basic], data types
- single-precision numbers [Visual Basic], converting
- data type conversion [Visual Basic], functions for
- CStr function
- times [Visual Basic], converting
- CSng function
- conversions [Visual Basic], type conversion functions
- CBool function
- CDbl function
- CUInt function
- Currency data type [Visual Basic], conversion functions
- numbers [Visual Basic], converting
- Double data type [Visual Basic], converting
- CLng function
- CSByte function
- double-precision numbers
- Decimal data type [Visual Basic], converting
- Boolean data type [Visual Basic], converting
- integers [Visual Basic], type conversion functions
- dates [Visual Basic], converting
- CULng function
- CInt function
- Date data type [Visual Basic], converting
- Byte data type [Visual Basic], converting
- String data type [Visual Basic], converting
- CChar function
- banker's rounding
- Short data type [Visual Basic], converting
- rounding numbers [Visual Basic], banker's rounding
- type conversion [Visual Basic], Visual Basic vs. .NET Framework
ms.assetid: d9d8d165-f967-44ff-a6cd-598e4740a99e
ms.openlocfilehash: 6b448fa23368f7a0848c44362337b0ccc70b6162
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592069"
---
# <a name="type-conversion-functions-visual-basic"></a>형식 변환 함수(Visual Basic)
이러한 함수는 인라인으로 컴파일됩니다. 즉, 변환 코드는 식을 계산 하는 코드의 일부입니다. 변환을 수행 하는 프로시저에 대 한 호출이 없을 수도 있으므로 성능이 향상 됩니다. 각 함수는 식을 특정 데이터 형식으로 강제 변환 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
CBool(expression)  
CByte(expression)  
CChar(expression)  
CDate(expression)  
CDbl(expression)  
CDec(expression)  
CInt(expression)  
CLng(expression)  
CObj(expression)  
CSByte(expression)  
CShort(expression)  
CSng(expression)  
CStr(expression)  
CUInt(expression)  
CULng(expression)  
CUShort(expression)  
```  
  
## <a name="part"></a>부분  
 `expression`  
 필수. 원본 데이터 형식의 식입니다.  
  
## <a name="return-value-data-type"></a>반환 값 데이터 형식  
 함수 이름은 다음 표에 나와 있는 것 처럼 반환 되는 값의 데이터 형식을 결정 합니다.  
  
|함수 이름|반환 데이터 형식|@No__t-0 인수의 범위|  
|-------------------|----------------------|-------------------------------------|  
|`CBool`|[Boolean 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|모든 유효한 `Char` 또는 `String` 또는 숫자 식입니다.|  
|`CByte`|[Byte 데이터 형식](../../../visual-basic/language-reference/data-types/byte-data-type.md)|<xref:System.Byte.MinValue?displayProperty=nameWithType> <xref:System.Byte.MaxValue?displayProperty=nameWithType> (255) (부호 없음); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic는 `CByte` 함수를 사용 하 여 부동 소수점에서 바이트 변환의 성능을 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
|`CChar`|[Char 데이터 형식](../../../visual-basic/language-reference/data-types/char-data-type.md)|모든 유효한 `Char` 또는 `String` 식 `String`의 첫 번째 문자만 변환 됩니다. 값은 0에서 65535 (부호 없음)이 될 수 있습니다.|  
|`CDate`|[Date 데이터 형식](../../../visual-basic/language-reference/data-types/date-data-type.md)|날짜 및 시간에 대 한 유효한 표현입니다.|  
|`CDbl`|[Double 데이터 형식](../../../visual-basic/language-reference/data-types/double-data-type.md)|-1.79769313486231570 e + 308 ~-4.94065645841246544 E-324 (음수 값의 경우) 4.94065645841246544 e-324 ~ 1.79769313486231570 E + 308 (양수 값)|  
|`CDec`|[Decimal 데이터 형식](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|0으로 크기가 조정 된 숫자, 즉 소수 자릿수가 없는 숫자의 경우 +/-79228162514264337593543950335입니다. 28 자리의 소수 자릿수가 포함 된 숫자의 경우 범위는 +/-7.9228162514264337593543950335입니다. 0이 아닌 가장 작은 숫자는 0.0000000000000000000000000001 (+/-1E-28)입니다.|  
|`CInt`|[Integer 데이터 형식](../../../visual-basic/language-reference/data-types/integer-data-type.md)|<xref:System.Int32.MinValue?displayProperty=nameWithType> (-2147483648) ~ <xref:System.Int32.MaxValue?displayProperty=nameWithType> (2147483647); 소수 부분은 반올림 됩니다. <sup>1</sup> <br/><br/>Visual Basic 15.8부터 Visual Basic는 `CInt` 함수를 사용 하 여 부동 소수점과 정수 변환의 성능을 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오. |  
|`CLng`|[Long 데이터 형식](../../../visual-basic/language-reference/data-types/long-data-type.md)|<xref:System.Int64.MinValue?displayProperty=nameWithType> (-9223372036854775808) ~ <xref:System.Int64.MaxValue?displayProperty=nameWithType> (9223372036854775807); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic는 `CLng` 함수를 사용 하 여 부동 소수점에서 64 비트 정수 변환의 성능을 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
|`CObj`|[Object 데이터 형식](../../../visual-basic/language-reference/data-types/object-data-type.md)|모든 유효한 식입니다.|  
|`CSByte`|[SByte 데이터 형식](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|<xref:System.SByte.MinValue?displayProperty=nameWithType> (-128) ~ <xref:System.SByte.MaxValue?displayProperty=nameWithType> (127); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic는 `CSByte` 함수를 사용 하 여 부동 소수점에서 부호 있는 바이트 변환의 성능을 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
|`CShort`|[Short 데이터 형식](../../../visual-basic/language-reference/data-types/short-data-type.md)|<xref:System.Int16.MinValue?displayProperty=nameWithType> (-32768) ~ <xref:System.Int16.MaxValue?displayProperty=nameWithType> (32767); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic는 `CShort` 함수를 사용 하 여 부동 소수점의 성능을 16 비트 정수 변환으로 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
|`CSng`|[Single 데이터 형식](../../../visual-basic/language-reference/data-types/single-data-type.md)|-3.402823 e + 38 ~-1.401298 E-45 (음수 값의 경우) 1.401298 e-45부터 3.402823 E + 38 까지의 양수 값입니다.|  
|`CStr`|[String 데이터 형식](../../../visual-basic/language-reference/data-types/string-data-type.md)|@No__t-0에 대 한 `expression` 인수에 따라 반환 됩니다. [CStr 함수의 반환 값을](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md)참조 하세요.|  
|`CUInt`|[UInteger 데이터 형식](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|<xref:System.UInt32.MinValue?displayProperty=nameWithType> <xref:System.UInt32.MaxValue?displayProperty=nameWithType> (4294967295) (부호 없음); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic은 `CUInt` 함수를 사용 하 여 부동 소수점에서 부호 없는 정수 변환의 성능을 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
|`CULng`|[ULong 데이터 형식](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|@no__t (0) ~ <xref:System.UInt64.MaxValue?displayProperty=nameWithType> (18446744073709551615) (부호 없음); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic는 `CULng` 함수를 사용 하 여 부동 소수점에서 부호 없는 정수 (long)로 변환 하는 성능을 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
|`CUShort`|[UShort 데이터 형식](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|<xref:System.UInt16.MinValue?displayProperty=nameWithType> <xref:System.UInt16.MaxValue?displayProperty=nameWithType> (65535) (부호 없음); 소수 부분은 반올림 됩니다. <sup>1</sup><br/><br/>Visual Basic 15.8부터 Visual Basic는 `CUShort` 함수를 사용 하 여 부동 소수점을 부호 없는 16 비트 정수 변환으로 최적화 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 예는 [CInt 예제](#cint-example) 섹션을 참조 하십시오.|  
  
 <sup>1</sup> 소수 부분에는 *은행원의 반올림*이라고 하는 특수 한 형식의 반올림이 적용 될 수 있습니다. 자세한 내용은 "주의"를 참조 하십시오.  
  
## <a name="remarks"></a>설명  
 규칙에 따라 <xref:System.Convert> 클래스 또는 개별 형식 구조 나 클래스에서 `ToString()`과 같은 .NET Framework 메서드에 기본 설정으로 Visual Basic 형식 변환 함수를 사용 해야 합니다. Visual Basic 함수는 Visual Basic 코드와의 최적의 상호 작용을 위해 디자인 되었으며 소스 코드를 더 짧고 읽기 쉽게 만듭니다. 또한 .NET Framework 변환 메서드는 Visual Basic 함수와 동일한 결과를 생성 하지 않습니다. 예를 들어 `Boolean`을 `Integer`로 변환 합니다. 자세한 내용은 [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)을 참조 하세요.  

Visual Basic 15.8부터, 다음 메서드에서 반환 하는 <xref:System.Single> 또는 @no__t 값을 정수 변환 함수 (`CByte`, `CShort`, `CInt`) 중 하나에 전달할 때 부동 소수점-정수 변환의 성능이 최적화 됩니다 @no__ t-5, `CSByte`, `CUShort` `CUInt`, `CULng`):

- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Single)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Single)?displayProperty=nameWithType>
- <xref:System.Math.Ceiling(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Floor(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Round(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Truncate(System.Double)?displayProperty=nameWithType>

이러한 최적화를 통해 많은 수의 정수 변환을 수행 하는 코드를 신속 하 게 2 배까지 실행할 수 있습니다. 다음 예제에서는 이러한 최적화 된 부동 소수점-정수 변환을 보여 줍니다.

```vb
Dim s As Single = 173.7619
Dim d As Double = s 

Dim i1 As Integer = CInt(Fix(s))               ' Result: 173
Dim b1 As Byte = CByte(Int(d))                 ' Result: 173
Dim s1 AS Short = CShort(Math.Truncate(s))     ' Result: 173
Dim i2 As Integer = CInt(Math.Ceiling(d))      ' Result: 174
Dim i3 As Integer = CInt(Math.Round(s))        ' Result: 174
```

## <a name="behavior"></a>동작  
  
- **형.** 일반적으로 데이터 형식 변환 함수를 사용 하 여 작업 결과를 기본 데이터 형식이 아닌 특정 데이터 형식으로 강제 변환할 수 있습니다. 예를 들어, 단일 전체 자릿수, 배정밀도 또는 정수 연산이 일반적으로 발생 하는 경우에는 `CDec`을 사용 하 여 소수 연산을 강제로 적용 합니다.  
  
- **변환에 실패 했습니다.** 함수에 전달 된 @no__t 0이 변환 될 데이터 형식의 범위를 벗어나면 <xref:System.OverflowException>이 발생 합니다.  
  
- **소수 부분.** 비정 수 값을 정수 계열 형식으로 변환 하는 경우 정수 변환 함수 (`CByte`, `CInt`, `CLng`, `CSByte`, `CShort`, `CUInt`, @no__t, @no__t)는 소수 부분을 제거 하 고 값을 가장 가까운 정수로 반올림 합니다.  
  
     소수 부분이 정확히 0.5 인 경우 정수 변환 함수는 해당 정수를 가장 가까운 짝수로 반올림 합니다. 예를 들어 0.5는 0으로 반올림 되 고 1.5 및 2.5는 모두 2로 반올림 됩니다. 이를 *은행원의 반올림*이라고 하며, 이러한 숫자를 여러 개 더하는 경우 누적 될 수 있는 바이어스를 보정 하기 위한 것입니다.  
  
     `CInt` 및 `CLng`은 숫자의 소수 부분을 반올림 하지 않고 잘라내는 <xref:Microsoft.VisualBasic.Conversion.Int%2A> 및 <xref:Microsoft.VisualBasic.Conversion.Fix%2A> 함수와 다릅니다. 또한 `Fix` 및 `Int`은 사용자가 전달 하는 것과 동일한 데이터 형식의 값을 항상 반환 합니다.  
  
- **날짜/시간 변환입니다.** @No__t-0 함수를 사용 하 여 값을 날짜 및 시간으로 변환할 수 있는지 확인 합니다. `CDate`은 날짜 리터럴과 시간 리터럴은 인식 하지만 숫자 값은 인식 하지 않습니다. Visual Basic 6.0 `Date` 값을 Visual Basic 2005 이상 버전의 `Date` 값으로 변환 하려면 <xref:System.DateTime.FromOADate%2A?displayProperty=nameWithType> 메서드를 사용할 수 있습니다.  
  
- **중립 날짜/시간 값입니다.** [날짜 데이터 형식](../../../visual-basic/language-reference/data-types/date-data-type.md) 에는 항상 날짜 및 시간 정보가 포함 됩니다. 형식 변환의 목적을 위해 Visual Basic은 1/1/0001 (1 년 1 월 1 일)을 날짜의 *중립 값* 으로 간주 하 고 00:00:00 (자정)을 시간에 대 한 중립 값으로 간주 합니다. @No__t-0 값을 문자열로 변환 하는 경우-1 @no__t 결과 문자열에 중립 값을 포함 하지 않습니다. 예를 들어 `#January 1, 0001 9:30:00#`을 문자열로 변환 하는 경우 결과는 "9:30:00 AM"입니다. 날짜 정보는 표시 되지 않습니다. 그러나 날짜 정보는 원래 `Date` 값에 계속 제공 되며 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> 함수와 같은 함수를 사용 하 여 복구할 수 있습니다.  
  
- **문화권 민감도.** 문자열을 포함 하는 형식 변환 함수는 응용 프로그램의 현재 문화권 설정에 따라 변환을 수행 합니다. 예를 들어 `CDate`은 시스템의 로캘 설정에 따라 날짜 형식을 인식 합니다. 요일, 월 및 연도를 로캘의 올바른 순서로 제공 해야 합니다. 그렇지 않으면 날짜가 올바르게 해석 되지 않을 수 있습니다. "수요일"과 같이 요일 문자열이 포함 된 경우에는 자세한 날짜 형식을 인식할 수 없습니다.  
  
     로캘에서 지정 된 값 이외의 형식으로 값의 문자열 표현으로 변환 해야 하는 경우에는 Visual Basic 형식 변환 함수를 사용할 수 없습니다. 이렇게 하려면 해당 값 형식의 `ToString(IFormatProvider)` 및 `Parse(String, IFormatProvider)` 메서드를 사용 합니다. 예를 들어 문자열을 `Double`로 변환 하는 경우 <xref:System.Double.Parse%2A?displayProperty=nameWithType>을 사용 하 고, `Double` 형식의 값을 문자열로 변환할 때 <xref:System.Double.ToString%2A?displayProperty=nameWithType>를 사용 합니다.  
  
## <a name="ctype-function"></a>CType Function  
 [CType 함수](../../../visual-basic/language-reference/functions/ctype-function.md) 는 두 번째 인수인 `typename`을 사용 하 고 `expression`를 `typename`으로 강제 변환 합니다. @no__t 여기서-4는 유효한 변환이 있는 모든 데이터 형식, 구조체, 클래스 또는 인터페이스 일 수 있습니다.  
  
 @No__t-0과 다른 형식 변환 키워드를 비교 하려면 [DirectCast operator](../../../visual-basic/language-reference/operators/directcast-operator.md) 및 [TryCast operator](../../../visual-basic/language-reference/operators/trycast-operator.md)를 참조 하세요.  
  
## <a name="cbool-example"></a>CBool 예  
 다음 예에서는 `CBool` 함수를 사용 하 여 식을 `Boolean` 값으로 변환 합니다. 식이 0이 아닌 값으로 계산 되는 경우 `CBool` @no__t 반환 합니다. 그렇지 않으면-2 @no__t 반환 합니다.  
  
 [!code-vb[VbVbalrFunctions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#1)]  
  
## <a name="cbyte-example"></a>CByte 예제  
 다음 예에서는 `CByte` 함수를 사용 하 여 식을 `Byte`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#2)]  
  
## <a name="cchar-example"></a>CChar 예  
 다음 예에서는 `CChar` 함수를 사용 하 여 `String` 식의 첫 번째 문자를 `Char` 형식으로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#3)]  
  
 @No__t에 대 한 입력 인수는-1 또는 `String` @no__t 데이터 형식 이어야 합니다. @No__t-1은 숫자 데이터 형식을 사용할 수 없기 때문에 `CChar`을 사용 하 여 숫자를 문자로 변환할 수 없습니다. 다음 예제에서는 코드 포인트 (문자 코드)를 나타내는 숫자를 가져와 해당 문자로 변환 합니다. @No__t-0 함수를 사용 하 여 숫자 문자열을 가져오고 `CInt`을 사용 하 여 문자열을 `Integer` 형식으로 변환 하 고 `ChrW`을 사용 하 여 숫자를 `Char` 형식으로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#4)]  
  
## <a name="cdate-example"></a>CDate 예  
 다음 예에서는 `CDate` 함수를 사용 하 여 문자열을 `Date` 값으로 변환 합니다. 일반적으로 날짜와 시간을 문자열로 하드 코딩 하는 것은 권장 되지 않습니다. 대신 #Feb 12, 1969 # 및 #4:45:23 PM #과 같은 날짜 리터럴과 시간 리터럴을 사용 합니다.  
  
 [!code-vb[VbVbalrFunctions#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#5)]  
  
## <a name="cdbl-example"></a>CDbl 예  
 [!code-vb[VbVbalrFunctions#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#6)]  
  
## <a name="cdec-example"></a>CDec 예  
 다음 예에서는 `CDec` 함수를 사용 하 여 숫자 값을 `Decimal`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#7)]  
  
## <a name="cint-example"></a>CInt 예  
 다음 예에서는 `CInt` 함수를 사용 하 여 값을 `Integer`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#8)]  

## <a name="clng-example"></a>CLng 예제
 다음 예에서는 `CLng` 함수를 사용 하 여 값을 `Long`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#9)]  
  
## <a name="cobj-example"></a>CObj 예제  
 다음 예에서는 `CObj` 함수를 사용 하 여 숫자 값을 `Object`로 변환 합니다. @No__t-0 변수 자체는 할당 된 @no__t 1 값을 가리키는 4 바이트 포인터만 포함 합니다.  
  
 [!code-vb[VbVbalrFunctions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#10)]  
  
## <a name="csbyte-example"></a>CSByte 예제  
 다음 예에서는 `CSByte` 함수를 사용 하 여 숫자 값을 `SByte`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#11)]  
  
## <a name="cshort-example"></a>CShort 예제  
 다음 예에서는 `CShort` 함수를 사용 하 여 숫자 값을 `Short`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#12)]  
  
## <a name="csng-example"></a>CSng 예제  
 다음 예에서는 `CSng` 함수를 사용 하 여 값을 `Single`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#13)]  
  
## <a name="cstr-example"></a>CStr 예  
 다음 예에서는 `CStr` 함수를 사용 하 여 숫자 값을 `String`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#14)]  
  
 다음 예에서는 `CStr` 함수를 사용 하 여 `Date` 값을 `String` 값으로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#15)]  
  
 `CStr`은 항상 현재 로캘의 표준 약식 형식 (예: "6/15/2003 4:35:47 PM")으로 `Date` 값을 렌더링 합니다. 그러나 `CStr`은 날짜 00:00:00와 시간에 대해 1/1/0001의 *중립 값* 을 표시 하지 않습니다.  
  
 @No__t-0에서 반환 되는 값에 대 한 자세한 내용은 [CStr 함수의 반환 값](../../../visual-basic/language-reference/functions/return-values-for-the-cstr-function.md)을 참조 하세요.  
  
## <a name="cuint-example"></a>Uint 예제  
 다음 예에서는 `CUInt` 함수를 사용 하 여 숫자 값을 `UInteger`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#16)]  
  
## <a name="culng-example"></a>CULng 예제  
 다음 예에서는 `CULng` 함수를 사용 하 여 숫자 값을 `ULong`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#17)]  
  
## <a name="cushort-example"></a>CUShort 예제  
 다음 예에서는 `CUShort` 함수를 사용 하 여 숫자 값을 `UShort`로 변환 합니다.  
  
 [!code-vb[VbVbalrFunctions#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#18)]  
  
## <a name="see-also"></a>참조

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- <xref:Microsoft.VisualBasic.Conversion.Int%2A>
- <xref:Microsoft.VisualBasic.Conversion.Fix%2A>
- <xref:Microsoft.VisualBasic.Strings.Format%2A>
- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:Microsoft.VisualBasic.Conversion.Oct%2A>
- <xref:Microsoft.VisualBasic.Conversion.Str%2A>
- <xref:Microsoft.VisualBasic.Conversion.Val%2A>
- [변환 함수](../../../visual-basic/language-reference/functions/conversion-functions.md)
- [Visual Basic 형식 변환](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
