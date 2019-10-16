---
title: '방법: 문자열을 숫자로 변환 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 02/11/2019
helpviewer_keywords:
- conversions [C#]
- conversions [C#], string to int
- converting strings to int [C#]
- strings [C#], converting to int
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
ms.openlocfilehash: 377074bf09cf1e24ec022cee506588a9dcb8cb80
ms.sourcegitcommit: 77e33b682db39955e331b8e8eda4ef1925a24e78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70133711"
---
# <a name="how-to-convert-a-string-to-a-number-c-programming-guide"></a>방법: 문자열을 숫자로 변환(C# 프로그래밍 가이드)

다양한 숫자 형식(`int`, `long`, `double` 등)에 있는 `Parse` 또는 `TryParse` 메서드를 호출하거나 <xref:System.Convert?displayProperty=nameWithType> 클래스의 메서드를 사용하여 [문자열](../../language-reference/keywords/string.md)을 숫자로 변환할 수 있습니다.  
  
 문자열이 있는 경우 `TryParse` 메서드(예: [`int.TryParse("11", out number)`](xref:System.Int32.TryParse%2A)) 또는 `Parse` 메서드([`var number = int.Parse("11")`](xref:System.Int32.Parse%2A))를 호출하면 약간 더 효율적이고 간단합니다.  <xref:System.Convert> 메서드 사용은 <xref:System.IConvertible>을 구현하는 일반 개체에 더 유용합니다.  
  
 `Parse` 또는 `TryParse` 메서드는 <xref:System.Int32?displayProperty=nameWithType> 형식과 같이 문자열에 포함되는 숫자 형식에서 사용할 수 있습니다.  <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> 메서드는 <xref:System.Int32.Parse%2A>를 내부적으로 사용합니다.  `Parse` 메서드는 변환된 숫자를 반환합니다. `TryParse` 메서드는 변환에 성공했는지 여부를 나타내는 <xref:System.Boolean> 값을 반환하고 변환된 숫자를 [`out` 매개 변수](../../language-reference/keywords/out.md)로 반환합니다. 문자열이 유효한 형식이 아닌 경우 `Parse`는 예외를 throw하는 반면, `TryParse`는 [false](../../language-reference/keywords/false-literal.md)를 반환합니다. `Parse` 메서드를 호출할 때는 항상 예외 처리를 사용하여 구문 분석 작업이 실패하는 이벤트에서 <xref:System.FormatException>을 catch해야 합니다.  
  
## <a name="calling-the-parse-and-tryparse-methods"></a>Parse 및 TryParse 메서드 호출

`Parse` 및 `TryParse` 메서드는 문자열의 시작과 끝에 있는 공백을 무시하지만 다른 모든 문자는 적절한 숫자 형식(`int`, `long`, `ulong`, `float`, `decimal` 등)을 구성하는 문자여야 합니다.  숫자를 구성하는 문자열 내에 공백이 있으면 오류가 발생합니다.  예를 들어 `decimal.TryParse`를 사용하여 “10”, “10.3” 또는 “  10  ”은 구문 분석할 수 있지만 이 메서드를 사용하여 “10X”, “1 0”(공백 포함), “10 .3”(공백 포함), “10e1”(`float.TryParse` 사용) 등에서 10을 구문 분석할 수는 없습니다. 또한 값이 `null` 또는 <xref:System.String.Empty?displayProperty=nameWithType>인 문자열이 구문 분석되지 않습니다. <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType> 메서드를 호출하여 구문 분석하기 전에 Null 또는 빈 문자열을 확인할 수 있습니다. 

다음 예제에서는 `Parse` 및 `TryParse` 호출이 성공하는 경우와 실패하는 경우를 모두 보여 줍니다.  
  
[!code-csharp[Parse and TryParse](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse/program.cs)]  

다음 예제에서는 선행 숫자(16진수 문자 포함) 및 숫자가 아닌 후행 문자를 포함해야 하는 문자열을 구문 분석하는 한 가지 방법을 보여 줍니다. <xref:System.Int32.TryParse%2A> 메서드를 호출하기 전에 문자열 시작 부분의 유효한 문자를 새 문자열에 할당합니다. 구문 분석할 문자열에 포함된 문자 수가 적으므로 예제에서는 <xref:System.String.Concat%2A?displayProperty=nameWithType> 메서드를 호출하여 새 문자열에 유효한 문자를 할당합니다. 더 큰 문자열의 경우 <xref:System.Text.StringBuilder> 클래스를 대신 사용할 수 있습니다. 
  
[!code-csharp[Removing invalid characters](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse2/program.cs)]  

## <a name="calling-the-convert-methods"></a>변환 메서드 호출

다음 표에는 문자열을 숫자로 변환하는 데 사용할 수 있는 <xref:System.Convert> 클래스의 일부 메서드가 나와 있습니다.  
  
|숫자 형식|메서드|  
|------------------|------------|  
|`decimal`|<xref:System.Convert.ToDecimal%28System.String%29>|  
|`float`|<xref:System.Convert.ToSingle%28System.String%29>|  
|`double`|<xref:System.Convert.ToDouble%28System.String%29>|  
|`short`|<xref:System.Convert.ToInt16%28System.String%29>|  
|`int`|<xref:System.Convert.ToInt32%28System.String%29>|  
|`long`|<xref:System.Convert.ToInt64%28System.String%29>|  
|`ushort`|<xref:System.Convert.ToUInt16%28System.String%29>|  
|`uint`|<xref:System.Convert.ToUInt32%28System.String%29>|  
|`ulong`|<xref:System.Convert.ToUInt64%28System.String%29>|  
  
 다음 예제에서는 <xref:System.Convert.ToInt32%28System.String%29?displayProperty=nameWithType> 메서드를 호출하여 입력 문자열을 [int](../../language-reference/builtin-types/integral-numeric-types.md)로 변환합니다. 예제에서는 이 메서드에서 throw할 수 있는 두 가지 가장 일반적인 예외인 <xref:System.FormatException>과 <xref:System.OverflowException>을 catch합니다. <xref:System.Int32.MaxValue?displayProperty=nameWithType>을 초과하지 않고 결과 숫자를 증분할 수 있는 경우 예제에서는 결과에 1을 더하고 출력을 표시합니다.  
  
[!code-csharp[Parsing with Convert methods](~/samples/snippets/csharp/programming-guide/string-to-number/convert/program.cs)]  
  
## <a name="see-also"></a>참고 항목

- [유형](./index.md)
- [방법: 문자열이 숫자 값을 나타내는지 확인](../strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
- [샘플: .NET Core WinForms 서식 유틸리티(C#)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs)
