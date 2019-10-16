---
title: '방법: 문자열 검색(C# 가이드)'
ms.date: 02/21/2018
helpviewer_keywords:
- searching strings [C#]
- strings [C#], searching with String methods
- strings [C#], searching with regular expressions
ms.assetid: fb1d9a6d-598d-4a35-bd5f-b86012edcb2b
ms.openlocfilehash: b9c27e419d37b6c0730f214d3b2b9bbdf7e30d11
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57202875"
---
# <a name="how-to-search-strings"></a>방법: 문자열 검색

문자열에서 텍스트를 검색하는 두 가지 기본 전략을 사용할 수 있습니다. <xref:System.String> 클래스의 메서드는 특정 텍스트를 검색합니다. 정규식은 텍스트에서 패턴을 검색합니다.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

<xref:System.String?displayProperty=nameWithType> 클래스의 별칭인 [string](../language-reference/keywords/string.md) 형식은 문자열 내용을 검색하기 위한 여러 가지 유용한 메서드를 제공합니다. 그중에 <xref:System.String.Contains%2A>, <xref:System.String.StartsWith%2A>, <xref:System.String.EndsWith%2A>, <xref:System.String.IndexOf%2A>, <xref:System.String.LastIndexOf%2A>입니다. <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 클래스는 텍스트에서 패턴을 검색하는 풍부한 어휘를 제공합니다. 이 문서에서는 이러한 기술 및 요구 사항에 대해 최상의 메서드를 선택하는 방법을 알아봅니다.

## <a name="does-a-string-contain-text"></a>문자열에 텍스트가 포함되어 있나요?

<xref:System.String.Contains%2A?displayProperty=nameWithType>, <xref:System.String.StartsWith%2A?displayProperty=nameWithType> 및 <xref:System.String.EndsWith%2A?displayProperty=nameWithType> 메서드는 특정 텍스트의 문자열을 검색합니다. 다음 예에서는 이러한 메서드 각각 및 대/소문자 구분 검색을 사용하는 변형을 보여줍니다.

[!code-csharp-interactive[search strings using methods](../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs#1)]

앞의 예제에서는 이러한 메서드를 사용하는 경우 중요한 사항을 보여줍니다. 검색은 기본적으로 **대/소문자를 구분**합니다. <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType> 열거형 값을 사용하여 대/소문자 구분 검색을 지정합니다.

## <a name="where-does-the-sought-text-occur-in-a-string"></a>검색된 텍스트가 있는 문자열의 위치는 어디인가요?

<xref:System.String.IndexOf%2A> 및 <xref:System.String.LastIndexOf%2A> 메서드도 문자열에서 텍스트를 검색합니다. 이러한 메서드는 검색되는 텍스트의 위치를 반환합니다. 텍스트를 찾을 수 없으면 `-1`을 반환합니다. 다음 예제에서는 "메서드"라는 단어의 첫 번째 및 마지막 항목에 대한 검색을 보여주고, 그 사이에 텍스트를 표시합니다.
  
[!code-csharp-interactive[search strings for indices](../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs#2)]

## <a name="finding-specific-text-using-regular-expressions"></a>정규식을 사용하여 특정 텍스트 찾기

<xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 클래스를 사용하여 문자열을 검색할 수 있습니다. 이 검색은 단순한 텍스트 패턴에서 복잡한 텍스트 패턴까지 복잡성의 범위를 지정할 수 있습니다.

다음 코드 예제에서는 문장에서 "the" 또는 "their"라는 문자를 검색하고 대/소문자를 무시합니다. 고정 메서드 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType>은 검색을 수행합니다. 검색할 문자열 및 검색 패턴을 입력합니다. 이 경우에 세 번째 인수는 대/소문자 구분 검색을 지정합니다. 자세한 내용은 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType>을 참조하세요.  

검색 패턴은 검색할 텍스트를 설명합니다. 다음 표에서는 검색 패턴의 각 요소에 대해 설명합니다. (아래 표에서는 C# 문자열에서 `\\`로 이스케이프되어야 하는 단일 `\`을 사용합니다.)

| pattern  | 의미     |
| -------- |-------------|
| the      | 텍스트 "the" 일치 |
| (eir)?   | “eir”과 0 또는 1개 항목 일치 |
| \s       | 공백 문자 찾기    |
  
[!code-csharp-interactive[Search using regular expressions](../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs#3)]
  
> [!TIP]
> 정확한 문자열을 검색하는 경우 일반적으로 `string` 메서드를 사용하는 것이 좋습니다. 원본 문자열인 몇 가지 패턴을 검색하는 경우 정규식을 사용하는 것이 좋습니다.

## <a name="does-a-string-follow-a-pattern"></a>문자열은 패턴을 따르나요?

다음 코드는 정규식을 사용하여 배열에서 각 문자열 형식의 유효성을 검사합니다. 유효성 검사에서는 각 문자열이 전화 번호의 형식을 사용해야 합니다. 이 경우 3개의 숫자 그룹이 대시로 구분되고, 처음 두 그룹에는 세 자리 숫자가 포함되며, 세 번째 그룹에는 네 자리 숫자가 포함됩니다. 검색 패턴은 정규식 `^\\d{3}-\\d{3}-\\d{4}$`을 사용합니다. 자세한 내용은 [정규식 언어 - 빠른 참조](../../standard/base-types/regular-expression-language-quick-reference.md)를 참조하세요.

| pattern  | 의미                             |
| -------- |-------------------------------------|
| ^        | 문자열의 시작 부분 일치 |
| \d{3}    | 정확히 3자리 문자 일치  |
| -        | '-' 문자 일치           |
| \d{3}    | 정확히 3자리 문자 일치  |
| -        | '-' 문자 일치           |
| \d{4}    | 정확히 4자리 문자 일치  |
| $        | 문자열의 끝 일치       |

[!code-csharp-interactive[csProgGuideStrings#4](../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs#4)]

이 단일 검색 패턴은 많은 유효한 문자열과 일치합니다. 단일 텍스트 문자열이 아닌 패턴을 검색하거나 유효성을 확인하기 위해 정규식을 사용하는 것이 좋습니다.

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/strings)의 코드를 확인하여 이러한 샘플을 시험해 볼 수 있습니다. 또는 샘플을 [zip 파일로](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/strings.zip) 다운로드할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../programming-guide/index.md)
- [문자열](../programming-guide/strings/index.md)
- [LINQ 및 문자열](../programming-guide/concepts/linq/linq-and-strings.md)
- <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>
- [.NET Framework 정규식](../../standard/base-types/regular-expressions.md)
- [정규식 언어 - 빠른 참조](../../standard/base-types/regular-expression-language-quick-reference.md)
- [.NET에서 문자열 사용에 대한 모범 사례](../../standard/base-types/best-practices-strings.md)
