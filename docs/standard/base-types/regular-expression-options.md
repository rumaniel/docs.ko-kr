---
title: 정규식 옵션
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, options
- constructs, options
- .NET Framework regular expressions, options
- inline option constructs
- options parameter
ms.assetid: c82dc689-7e82-4767-a18d-cd24ce5f05e9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d9cfdcbe1e533f70cdd37b5d0512c781c6c05d22
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957349"
---
# <a name="regular-expression-options"></a>정규식 옵션

<a name="Top"></a> 기본적으로 입력 문자열을 정규식 패턴의 리터럴 문자와 비교할 때는 대/소문자를 구분하고, 정규식 패턴의 공백은 리터럴 공백 문자로 해석되며, 정규식의 캡처링 그룹은 명시적 및 암시적으로 명명됩니다. 정규식 옵션을 지정하여 기본 정규식 동작의 이러한 측면과 몇 가지 다른 측면을 수정할 수 있습니다. 다음 테이블에 나열되어 있는 이러한 옵션은 정규식 패턴의 일부로 인라인으로 포함되거나, <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 클래스 생성자 또는 정적 패턴 일치 메서드에 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType> 열거형 값으로 제공될 수 있습니다.

|RegexOptions 멤버|인라인 문자|효과|
|-------------------------|----------------------|------------|
|<xref:System.Text.RegularExpressions.RegexOptions.None>|사용할 수 없음|기본 동작을 사용합니다. 자세한 내용은 [기본 옵션](#Default)을 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase>|`i`|대/소문자를 구분하지 않는 일치를 사용합니다. 자세한 내용은 [대/소문자를 구분하지 않는 일치](#Case)를 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.Multiline>|`m`|여러 줄 모드를 사용합니다. 여기서 `^` 및 `$`는 각 줄의 시작 부분 및 끝 부분과 일치합니다(입력 문자열의 시작 부분 및 끝 부분 대신). 자세한 내용은 [여러 줄 모드](#Multiline)를 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.Singleline>|`s`|한 줄 모드를 사용합니다. 여기서 마침표(.)는 모든 문자와 일치합니다(`\n`을 제외한 모든 문자 대신). 자세한 내용은 [한 줄 모드](#Singleline)를 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture>|`n`|명명되지 않은 그룹을 캡처하지 않습니다. 유효한 캡처는 `(?<`*name*`>` *subexpression*`)` 형식의 명시적으로 명명되거나 번호가 매겨진 그룹 뿐입니다. 자세한 내용은 [명시적 캡처만 해당](#Explicit)을 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.Compiled>|사용할 수 없음|정규식을 어셈블리로 컴파일합니다. 자세한 내용은 [컴파일된 정규식](#Compiled)을 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace>|`x`|이스케이프되지 않은 공백을 패턴에서 제외하고 숫자 기호(`#`) 뒤에 주석을 사용하도록 설정합니다. 자세한 내용은 [공백 무시](#Whitespace)를 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.RightToLeft>|사용할 수 없음|검색 방향을 변경합니다. 검색이 왼쪽에서 오른쪽으로 대신 오른쪽에서 왼쪽으로 이동합니다. 자세한 내용은 [오른쪽에서 왼쪽 모드](#RightToLeft)를 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.ECMAScript>|사용할 수 없음|식에 대해 ECMAScript와 호환되는 동작을 사용하도록 설정합니다. 자세한 내용은 [ECMAScript 일치 동작](#ECMAScript)을 참조하세요.|
|<xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant>|사용할 수 없음|언어의 문화권 차이를 무시합니다. 자세한 내용은 [고정 문화권을 사용한 비교](#Invariant)를 참조하세요.|

## <a name="specifying-the-options"></a>옵션 지정

정규식에 대한 옵션은 다음과 같은 세 가지 방법 중 하나로 지정할 수 있습니다.

- `options` 클래스 생성자 또는 정적(Visual Basic의 경우 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>) 패턴 일치 메서드(예: `Shared` 또는 <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType>)의 <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 매개 변수에 지정합니다. `options` 매개 변수는 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType> 열거형 값의 비트 OR 조합입니다.

  클래스 생성자의 `options` 매개 변수를 사용하여 <xref:System.Text.RegularExpressions.Regex> 인스턴스에 옵션을 제공하면 해당 옵션이 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType> 속성에 할당됩니다. 그러나 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType> 속성은 정규식 패턴 자체에 인라인 옵션을 반영하지는 않습니다.

  다음 예제에서 이에 대해 설명합니다. 이 예제에서는 `options` 메서드의 <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 매개 변수를 사용하여 대/소문자를 구분하지 않는 일치를 사용하도록 설정하고 문자 "d"로 시작하는 단어를 식별할 때 패턴 공백을 무시합니다.

  [!code-csharp[Conceptual.Regex.Language.Options#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/example1.cs#6)]
  [!code-vb[Conceptual.Regex.Language.Options#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/example1.vb#6)]

- `(?imnsx-imnsx)` 구문을 사용하여 정규식 패턴에 인라인 옵션을 적용합니다. 이 옵션은 옵션이 정의된 지점에서 패턴의 끝 부분까지 또는 다른 인라인 옵션에 의해 옵션이 정의되지 않은 지점까지 패턴에 적용됩니다. <xref:System.Text.RegularExpressions.Regex> 인스턴스의 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType> 속성은 이러한 인라인 옵션을 반영하지 않습니다. 자세한 내용은 [기타 구문](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md) 항목을 참조하세요.

  다음 예제에서 이에 대해 설명합니다. 이 예제에서는 인라인 옵션을 사용하여 대/소문자를 구분하지 않는 일치를 사용하도록 설정하고 문자 "d"로 시작하는 단어를 식별할 때 패턴 공백을 무시합니다.

  [!code-csharp[Conceptual.Regex.Language.Options#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/example1.cs#7)]
  [!code-vb[Conceptual.Regex.Language.Options#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/example1.vb#7)]

- `(?imnsx-imnsx:`*subexpression*`)` 구문을 사용하여 정규식 패턴의 특정 그룹화 구문에 인라인 옵션을 적용합니다. 옵션 집합 앞에 기호가 없으면 집합이 설정되고, 옵션 집합 앞에 빼기 기호가 있으면 집합이 해제됩니다. `?`는 옵션의 사용 여부에 따라 필요한 언어 구문의 고정 부분입니다. 이 옵션은 해당 그룹에만 적용됩니다. 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.

  다음 예제에서 이에 대해 설명합니다. 이 예제에서는 그룹화 구문에 인라인 옵션을 사용하여 대/소문자를 구분하지 않는 일치를 사용하도록 설정하고 문자 "d"로 시작하는 단어를 식별할 때 패턴 공백을 무시합니다.

  [!code-csharp[Conceptual.Regex.Language.Options#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/example1.cs#8)]
  [!code-vb[Conceptual.Regex.Language.Options#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/example1.vb#8)]

옵션이 인라인으로 지정된 경우 옵션 또는 옵션 집합 앞에 빼기 기호(`-`)가 있으면 해당 옵션이 해제됩니다. 예를 들어, 인라인 구문 `(?ix-ms)`는 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 및 <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> 옵션을 설정하고 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 및 <xref:System.Text.RegularExpressions.RegexOptions.Singleline?displayProperty=nameWithType> 옵션을 해제합니다. 모든 정규식 옵션은 기본적으로 해제되어 있습니다.

> [!NOTE]
> 생성자 또는 메서드 호출의 `options` 매개 변수에 지정된 정규식 옵션이 정규식 패턴에 인라인으로 지정된 옵션과 충돌하는 경우 인라인 옵션이 사용됩니다.

다음 5개의 정규식 옵션은 옵션 매개 변수와 인라인으로 모두 설정할 수 있습니다.

- <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.Singleline?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType>

다음 5개의 정규식 옵션은 `options` 매개 변수를 사용하여 설정할 수 있지만 인라인으로는 설정할 수 없습니다.

- <xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.RightToLeft?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant?displayProperty=nameWithType>

- <xref:System.Text.RegularExpressions.RegexOptions.ECMAScript?displayProperty=nameWithType>

## <a name="determining-the-options"></a>옵션 확인

읽기 전용 <xref:System.Text.RegularExpressions.Regex> 속성 값을 검색하여 <xref:System.Text.RegularExpressions.Regex.Options%2A?displayProperty=nameWithType> 개체를 인스턴스화했을 때 해당 개체에 제공된 옵션을 확인할 수 있습니다. 이 속성은 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> 메서드에 의해 만들어진 컴파일된 정규식에 대해 정의된 옵션을 확인하는 데 특히 유용합니다.

<xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType>을 제외한 모든 옵션의 존재 유무를 테스트하려면 <xref:System.Text.RegularExpressions.Regex.Options%2A?displayProperty=nameWithType> 속성 값 및 관심 있는 <xref:System.Text.RegularExpressions.RegexOptions> 값으로 AND 작업을 수행합니다. 그런 다음 결과가 해당 <xref:System.Text.RegularExpressions.RegexOptions> 값과 같은지 테스트합니다. 다음 예제에서는 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션이 설정되었는지 테스트합니다.

[!code-csharp[Conceptual.Regex.Language.Options#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/determine1.cs#19)]
[!code-vb[Conceptual.Regex.Language.Options#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/determine1.vb#19)]

<xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType>에 대해 테스트하려면 다음 예제에 표시된 것처럼 <xref:System.Text.RegularExpressions.Regex.Options%2A?displayProperty=nameWithType> 속성 값이 <xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType>과 같은지 확인합니다.

[!code-csharp[Conceptual.Regex.Language.Options#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/determine1.cs#20)]
[!code-vb[Conceptual.Regex.Language.Options#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/determine1.vb#20)]

다음 섹션에는 .NET의 정규식에서 지원하는 옵션이 나열되어 있습니다.

<a name="Default"></a>

## <a name="default-options"></a>기본 옵션

<xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType> 옵션은 지정된 옵션이 없고 정규식 엔진에서 해당 기본 동작을 사용함을 나타냅니다. 여기에는 다음과 같은 사항이 포함됩니다.

- 패턴이 ECMAScript 정규식이 아니라 정식으로 해석됩니다.

- 정규식 패턴이 입력 문자열에서 왼쪽에서 오른쪽으로 일치됩니다.

- 비교는 대/소문자를 구분합니다.

- `^` 및 `$` 언어 요소는 입력 문자열의 시작 부분 및 끝 부분과 일치합니다.

- `.` 언어 요소는 `\n`을 제외한 모든 문자와 일치합니다.

- 정규식 패턴의 모든 공백은 리터럴 공백 문자로 해석됩니다.

- 패턴을 입력 문자열과 비교할 때 현재 문화권의 규칙이 사용됩니다.

- 정규식 패턴의 캡처링 그룹은 명시적 및 암시적입니다.

> [!NOTE]
> <xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType> 옵션과 동일한 인라인 옵션은 없습니다. 정규식 옵션이 인라인으로 적용된 경우 기본 동작은 특정 옵션을 해제하여 옵션별로 복원됩니다. 예를 들어, `(?i)`는 대/소문자를 구분하지 않는 비교를 설정하고 `(?-i)`는 기본 대/소문자를 구분하는 비교를 복원합니다.

<xref:System.Text.RegularExpressions.RegexOptions.None?displayProperty=nameWithType> 옵션은 정규식 엔진의 기본 동작을 나타내므로 메서드 호출에 명시적으로 지정되는 경우가 드뭅니다. 대신 생성자 또는 정적 패턴 일치 메서드가 `options` 매개 변수 없이 호출됩니다.

[맨 위로 이동](#Top)

<a name="Case"></a>

## <a name="case-insensitive-matching"></a>대/소문자를 구분하지 않는 일치

<xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase> 옵션 또는 `i` 인라인 옵션은 대/소문자를 구분하지 않는 일치를 제공합니다. 기본적으로 현재 문화권의 대/소문자 사용 규칙이 사용됩니다.

다음 예제에서는 "the"로 시작하는 모든 단어와 일치하는 정규식 패턴 `\bthe\w*\b`를 정의합니다. <xref:System.Text.RegularExpressions.Regex.Match%2A> 메서드에 대한 첫 번째 호출에서 기본 대/소문자를 구분하는 비교를 사용하므로 출력은 문장을 시작하는 문자열 "The"가 일치하지 않음을 나타냅니다. <xref:System.Text.RegularExpressions.Regex.Match%2A> 메서드가 옵션이 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase>로 설정된 상태로 호출되면 이 문자열이 일치합니다.

[!code-csharp[Conceptual.Regex.Language.Options#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/case1.cs#1)]
[!code-vb[Conceptual.Regex.Language.Options#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/case1.vb#1)]

다음 예제에서는 대/소문자를 구분하지 않는 비교를 제공하기 위해 `options` 매개 변수 대신 인라인 옵션을 사용하도록 이전 예제의 정규식 패턴을 수정합니다. 첫 번째 패턴은 문자열 "the"에서 문자 "t"에만 적용되는 그룹화 구문에 대/소문자를 구분하지 않는 옵션을 정의합니다. 옵션 구문이 패턴의 시작 부분에서 발생하므로 두 번째 패턴은 대/소문자를 구분하지 않는 옵션을 전체 정규식에 적용합니다.

[!code-csharp[Conceptual.Regex.Language.Options#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/case2.cs#2)]
[!code-vb[Conceptual.Regex.Language.Options#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/case2.vb#2)]

[맨 위로 이동](#Top)

<a name="Multiline"></a>

## <a name="multiline-mode"></a>여러 줄 모드

<xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션 또는 `m` 인라인 옵션은 정규식 엔진이 여러 줄로 구성된 입력 문자열을 처리할 수 있게 해줍니다. 이 옵션은 `^` 및 `$` 언어 요소가 입력 문자열의 시작 부분 및 끝 부분 대신 줄의 시작 부분 및 끝 부분과 일치하도록 해당 언어 요소의 해석을 변경합니다.

기본적으로 `$`는 입력 문자열의 끝 부분과만 일치합니다. <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션을 지정하면 줄 바꿈 문자(`\n`) 또는 입력 문자열의 끝 부분과 일치합니다. 그러나 캐리지 리턴/줄 바꿈 문자 조합과는 일치하지 않습니다. 성공적으로 일치시키려면 단순히 `\r?$`만 사용할 것이 아니라 하위 식 `$`를 사용합니다.

다음 예제에서는 볼링하는 사람의 이름과 점수를 추출하여 이를 내림차순으로 정렬하는 <xref:System.Collections.Generic.SortedList%602> 컬렉션에 추가합니다. <xref:System.Text.RegularExpressions.Regex.Matches%2A> 메서드가 두 번 호출됩니다. 첫 번째 메서드 호출에서 정규식은 `^(\w+)\s(\d+)$`이며 옵션이 설정되지 않았습니다. 출력에 표시된 것처럼, 정규식 엔진이 입력 패턴을 입력 문자열의 시작 부분 및 끝 부분과 함께 일치시킬 수 없어 찾은 일치 항목이 없습니다. 두 번째 메서드 호출에서 정규식은 `^(\w+)\s(\d+)\r?$`로 변경되었으며 옵션이 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType>으로 설정되었습니다. 출력에 표시된 것처럼, 이름 및 점수가 성공적으로 일치되었으며 점수가 내림차순으로 표시되었습니다.

[!code-csharp[Conceptual.Regex.Language.Options#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/multiline1.cs#3)]
[!code-vb[Conceptual.Regex.Language.Options#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/multiline1.vb#3)]

정규식 패턴 `^(\w+)\s(\d+)\r*$`는 다음 테이블과 같이 정의됩니다.

|무늬|설명|
|-------------|-----------------|
|`^`|줄의 시작 부분에서 시작합니다.|
|`(\w+)`|하나 이상의 단어 문자를 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|
|`\s`|공백 문자를 찾습니다.|
|`(\d+)`|하나 이상의 10진수 숫자가 일치하는지 확인합니다. 이 그룹은 두 번째 캡처링 그룹입니다.|
|`\r?`|0개 또는 1개의 캐리지 리턴 문자를 찾습니다.|
|`$`|줄의 끝 부분에서 끝납니다.|

다음 예제는 인라인 옵션 `(?m)`를 사용하여 여러 줄 옵션을 설정한다는 점을 제외하고는 이전 예제와 동일합니다.

[!code-csharp[Conceptual.Regex.Language.Options#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/multiline2.cs#4)]
[!code-vb[Conceptual.Regex.Language.Options#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/multiline2.vb#4)]

[맨 위로 이동](#Top)

<a name="Singleline"></a>

## <a name="single-line-mode"></a>한 줄 모드

<xref:System.Text.RegularExpressions.RegexOptions.Singleline?displayProperty=nameWithType> 옵션 또는 `s` 인라인 옵션은 정규식 엔진이 입력 문자열이 한 줄로 구성된 것처럼 입력 문자열을 처리하도록 합니다. 이 옵션은 마침표(`.`) 언어 요소가 줄 바꿈 문자 `\n` 또는 \u000A를 제외한 모든 문자와 일치하는 대신 모든 문자와 일치하도록 해당 언어 요소의 동작을 변경하여 그렇게 합니다.

다음 예제에서는 `.` 옵션을 사용할 때 <xref:System.Text.RegularExpressions.RegexOptions.Singleline?displayProperty=nameWithType> 언어 요소의 동작이 변경되는 방법을 보여 줍니다. 정규식 `^.+`는 문자열의 시작 부분에서 시작하여 모든 문자를 찾습니다. 기본적으로 일치는 첫 번째 줄의 끝 부분에서 끝납니다. 정규식 패턴은 캐리지 리턴 문자, `\r` 또는 \u000D와 일치하지만 `\n`과는 일치하지 않습니다. <xref:System.Text.RegularExpressions.RegexOptions.Singleline?displayProperty=nameWithType> 옵션은 전체 입력 문자열을 한 줄로 해석하기 때문에 `\n`을 포함하여 입력 문자열의 모든 문자와 일치합니다.

[!code-csharp[Conceptual.Regex.Language.CharacterClasses#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.characterclasses/cs/any2.cs#5)]
[!code-vb[Conceptual.Regex.Language.CharacterClasses#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.characterclasses/vb/any2.vb#5)]

다음 예제는 인라인 옵션 `(?s)`를 사용하여 한 줄 모드를 사용하도록 설정한다는 점을 제외하고는 이전 예제와 동일합니다.

[!code-csharp[Conceptual.Regex.Language.Options#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/singleline1.cs#5)]
[!code-vb[Conceptual.Regex.Language.Options#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/singleline1.vb#5)]

[맨 위로 이동](#Top)

<a name="Explicit"></a>

## <a name="explicit-captures-only"></a>명시적 캡처만 해당

기본적으로 캡처링 그룹은 정규식 패턴에 괄호를 사용하여 정의됩니다. 명명된 그룹은 `(?<`*name*`>`*subexpression*`)` 언어 옵션에 의해 이름 또는 번호가 할당되는 반면, 명명되지 않은 그룹은 인덱스로 액세스할 수 있습니다. <xref:System.Text.RegularExpressions.GroupCollection> 개체에서 명명되지 않은 그룹은 명명된 그룹 앞에 있습니다.

그룹화 구문은 일반적으로 여러 언어 요소에 수량자를 적용하는 데만 사용되고, 캡처된 부분 문자열은 관심을 두는 부분이 아닙니다. 예를 들어, 다음 정규식

`\b\(?((\w+),?\s?)+[\.!?]\)?`

가 문서에서 마침표, 느낌표 또는 물음표로 끝나는 문장만 추출하려는 의도로 사용된 경우 결과 문장(<xref:System.Text.RegularExpressions.Match> 개체로 표현됨)만 관심을 두는 부분입니다. 컬렉션의 개별 단어는 관심을 두는 부분이 아닙니다.

정규식 엔진이 <xref:System.Text.RegularExpressions.GroupCollection> 및 <xref:System.Text.RegularExpressions.CaptureCollection> 컬렉션 개체를 둘 다 채워야 하므로 이후에 사용되지 않는 캡처링 그룹에는 비용이 많이 들 수 있습니다. 대안으로 <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType> 옵션 또는 `n` 인라인 옵션을 사용하여 유효한 캡처만 `(?<`*name*`>` *subexpression*`)` 구문에 의해 지정된, 명시적으로 명명되거나 번호가 매겨진 그룹임을 지정할 수 있습니다.

다음 예제에서는 `\b\(?((\w+),?\s?)+[\.!?]\)?` 메서드가 <xref:System.Text.RegularExpressions.Regex.Match%2A> 옵션을 사용하여 호출된 경우와 이 옵션을 사용하지 않고 호출된 경우에 <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType> 정규식 패턴에서 반환하는 일치 항목에 대한 정보를 표시합니다. 첫 번째 메서드 호출의 출력이 보여 주는 것처럼, 정규식 엔진은 캡처된 부분 문자열에 대한 정보로 <xref:System.Text.RegularExpressions.GroupCollection> 및 <xref:System.Text.RegularExpressions.CaptureCollection> 컬렉션 개체를 완전히 채웁니다. 두 번째 메서드는 `options`가 <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType>로 설정된 상태로 호출되었기 때문에 그룹에 대한 정보를 캡처하지 않습니다.

[!code-csharp[Conceptual.Regex.Language.Options#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/explicit1.cs#9)]
[!code-vb[Conceptual.Regex.Language.Options#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/explicit1.vb#9)]

정규식 패턴 `\b\(?((?>\w+),?\s?)+[\.!?]\)?`는 다음 표와 같이 정의됩니다.

|무늬|설명|
|-------------|-----------------|
|`\b`|단어 경계에서 시작합니다.|
|`\(?`|0개 또는 1개의 여는 괄호("(")를 찾습니다.|
|`(?>\w+),?`|하나 이상의 단어 문자 다음에 0개 또는 1개의 쉼표가 있는 일치 항목을 찾습니다. 단어 문자를 찾을 때 역추적하지 않습니다.|
|`\s?`|0회 이상 나오는 공백 문자를 찾습니다.|
|`((\w+),?\s?)+`|하나 이상의 단어 문자 다음에 0개 또는 1개의 쉼표 및 0개 또는 1개의 공백 문자가 한 번 이상 나타나는 조합을 찾습니다.|
|`[\.!?]\)?`|세 가지 문장 부호 기호 다음에 0개 또는 1개의 닫는 괄호(")")가 있는 모든 일치 항목을 찾습니다.|

또한 `(?n)` 인라인 요소를 사용하여 자동 캡처를 억제할 수 있습니다. 다음 예제에서는 `(?n)` 옵션 대신 <xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture?displayProperty=nameWithType> 인라인 요소를 사용하도록 이전 정규식 패턴을 수정합니다.

[!code-csharp[Conceptual.Regex.Language.Options#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/explicit2.cs#10)]
[!code-vb[Conceptual.Regex.Language.Options#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/explicit2.vb#10)]

마지막으로, 인라인 그룹 요소 `(?n:)`를 사용하여 그룹별로 자동 캡처를 억제할 수 있습니다. 다음 예제에서는 바깥쪽 그룹 `((?>\w+),?\s?)`에서 명명되지 않은 캡처를 억제하도록 이전 패턴을 수정합니다. 여기서는 안쪽 그룹에서도 명명되지 않은 캡처가 억제됩니다.

[!code-csharp[Conceptual.Regex.Language.Options#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/explicit3.cs#11)]
[!code-vb[Conceptual.Regex.Language.Options#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/explicit3.vb#11)]

[맨 위로 이동](#Top)

<a name="Compiled"></a>

## <a name="compiled-regular-expressions"></a>컴파일된 정규식

기본적으로 .NET의 정규식은 해석됩니다. <xref:System.Text.RegularExpressions.Regex> 개체가 인스턴스화되거나 정적 <xref:System.Text.RegularExpressions.Regex> 메서드가 호출되면 정규식 패턴이 일련의 사용자 지정 opcode로 구문 분석되고 해석기는 이러한 opcode를 사용하여 정규식을 실행합니다. 여기에는 절충 사항이 수반됩니다. 즉, 정규식 엔진의 초기화 비용은 런타임 성능을 희생하여 최소화됩니다.

<xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 옵션을 사용하여, 해석된 정규식 대신 컴파일된 정규식을 사용할 수 있습니다. 이 경우 패턴이 정규식 엔진에 전달되면 일련의 opcode로 구문 분석된 다음, 공용 언어 런타임으로 직접 전달될 수 있는 MSIL(Microsoft Intermediate Language)로 변환됩니다. 컴파일된 정규식은 초기화 시간을 희생하여 런타임 성능을 최대화합니다.

> [!NOTE]
> 정규식은 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 값을 `options` 클래스 생성자 또는 정적 패턴 일치 메서드의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 제공해서만 컴파일할 수 있으며, 인라인 옵션으로는 사용할 수 없습니다.

컴파일된 정규식은 정적 정규식과 인스턴스 정규식 둘 다에 대한 호출에 사용할 수 있습니다. 정적 정규식에서 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 옵션은 정규식 패턴 일치 메서드의 `options` 매개 변수에 전달됩니다. 인스턴스 정규식에서 이 옵션은 `options` 클래스 생성자의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 전달됩니다. 따라서 두 가지 경우 모두에서 성능이 향상됩니다.

그러나 이 성능 향상은 다음 조건에서만 발생합니다.

- 특정 정규식을 나타내는 <xref:System.Text.RegularExpressions.Regex> 개체가 정규식 패턴 일치 메서드에 대한 여러 번의 호출에 사용됩니다.

- <xref:System.Text.RegularExpressions.Regex> 개체가 범위를 벗어날 수 없어 재사용될 수 있습니다.

- 정적 정규식이 정규식 패턴 일치 메서드에 대한 여러 번의 호출에 사용됩니다. (정적 메서드 호출에 사용된 정규식이 정규식 엔진에 의해 캐시되므로 성능 향상이 가능합니다.)

> [!NOTE]
> <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 옵션은 미리 정의된 컴파일된 정규식을 포함하는 특수 목적 어셈블리를 만드는 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> 메서드와는 관련이 없습니다.

[맨 위로 이동](#Top)

<a name="Whitespace"></a>

## <a name="ignore-white-space"></a>공백 무시

기본적으로 정규식 패턴에서 공백은 중요합니다. 공백은 정규식 엔진이 입력 문자열에서 공백 문자를 강제로 일치시키도록 합니다. 따라서 정규식 "`\b\w+\s`"와 "`\b\w+`"는 거의 동일한 정규식입니다. 또한 정규식 패턴에 숫자 기호(#)가 있으면 이는 일치시킬 리터럴 문자로 해석됩니다.

<xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> 옵션 또는 `x` 인라인 옵션은 이 기본 동작을 다음과 같이 변경합니다.

- 정규식 패턴에서 이스케이프되지 않은 공백은 무시됩니다. 정규식 패턴의 일부가 되려면 공백 문자가 이스케이프되어야 합니다(예: `\s` 또는 “`\`”로).

- 숫자 기호(#)는 리터럴 문자가 아니라 주석의 시작 부분으로 해석됩니다. 정규식 패턴에서 모든 텍스트는 # 문자부터 문자열의 끝 부분까지 주석으로 해석됩니다.

그러나 다음 경우에 정규식의 공백 문자는 <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> 옵션을 사용하더라도 무시되지 않습니다.

- 문자 클래스 내의 공백은 항상 리터럴로 해석됩니다. 예를 들어, 정규식 패턴 `[ .,;:]`는 모든 단일 공백 문자, 마침표, 쉼표, 세미콜론 또는 콜론과 일치합니다.

- 중괄호로 묶은 수량자 내에는 공백이 허용되지 않습니다(예: `{`*n*`}`, `{`*n*`,}` 및 `{`*n*`,`*m*`}`). 예를 들어, 정규식 패턴 `\d{1, 3}`는 공백 문자를 포함하고 있기 때문에 1자리에서 3자리까지의 숫자로 이루어진 어떠한 숫자 시퀀스와도 일치하지 않습니다.

- 언어 요소를 도입하는 문자 시퀀스 내에는 공백이 허용되지 않습니다. 예:

  - 언어 요소 `(?:`*subexpression*`)`는 비 캡처링 그룹을 나타내고, 요소의 `(?:` 부분은 공백을 포함할 수 없습니다. `(? :`*subexpression*`)` 패턴은 정규식 엔진이 패턴을 구문 분석할 수 없고 `( ?:`*subexpression*`)` 패턴이 *subexpression*과 일치하지 않으므로 런타임에 <xref:System.ArgumentException>을 throw합니다.

  - 유니코드 범주 또는 명명된 블록을 나타내는 언어 요소 `\p{`*name*`}`는 요소의 `\p{` 부분에 공백을 포함할 수 없습니다. 공백을 포함하는 경우 이 요소가 런타임에 <xref:System.ArgumentException>을 throw합니다.

이 옵션을 사용하면 일반적으로 구문 분석 및 이해가 어려운 정규식을 단순화하는 데 도움이 됩니다. 이 옵션은 가독성을 향상시키고 정규식을 문서화할 수 있게 해줍니다.

다음 예제에서는 다음과 같은 정규식 패턴을 정의합니다.

`\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence.`

이 패턴은 <xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace?displayProperty=nameWithType> 옵션을 사용하여 패턴 공백을 무시하는 점을 제외하고는 [명시적 캡처만 해당](#Explicit) 섹션에 정의된 패턴과 유사합니다.

[!code-csharp[Conceptual.Regex.Language.Options#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/whitespace1.cs#12)]
[!code-vb[Conceptual.Regex.Language.Options#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/whitespace1.vb#12)]

다음 예제에서는 인라인 옵션 `(?x)`를 사용하여 패턴 공백을 무시합니다.

[!code-csharp[Conceptual.Regex.Language.Options#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/whitespace2.cs#13)]
[!code-vb[Conceptual.Regex.Language.Options#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/whitespace2.vb#13)]

[맨 위로 이동](#Top)

<a name="RightToLeft"></a>

## <a name="right-to-left-mode"></a>오른쪽에서 왼쪽 모드

기본적으로 정규식 엔진은 왼쪽에서 오른쪽으로 검색합니다. <xref:System.Text.RegularExpressions.RegexOptions.RightToLeft?displayProperty=nameWithType> 옵션을 사용하여 검색 방향을 반대로 할 수 있습니다. 검색은 자동으로 문자열의 마지막 문자 위치에서 시작됩니다. 시작 위치 매개 변수를 포함한 패턴 일치 메서드의 경우(예: <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.Int32%29?displayProperty=nameWithType>) 시작 위치는 검색이 시작될 가장 오른쪽 문자 위치의 인덱스입니다.

> [!NOTE]
> 오른쪽에서 왼쪽 패턴 모드는 <xref:System.Text.RegularExpressions.RegexOptions.RightToLeft?displayProperty=nameWithType> 값을 `options` 클래스 생성자 또는 정적 패턴 일치 메서드의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 제공해서만 사용할 수 있으며, 인라인 옵션으로는 사용할 수 없습니다.

<xref:System.Text.RegularExpressions.RegexOptions.RightToLeft?displayProperty=nameWithType> 옵션은 검색 방향만 변경하며 오른쪽에서 왼쪽으로 정규식 패턴을 해석하지는 않습니다. 예를 들어, 정규식 `\bb\w+\s`는 문자 "b"로 시작하고 뒤에 공백 문자가 있는 단어와 일치합니다. 다음 예제에서 입력 문자열은 하나 이상의 "b" 문자를 포함하는 세 단어로 구성됩니다. 첫 번째 단어는 "b"로 시작하고, 두 번째 단어는 "b"로 끝나며, 세 번째 단어는 단어 중간에 두 개의 "b" 문자를 포함합니다. 예제의 출력이 보여 주는 것처럼, 첫 번째 단어만 정규식 패턴과 일치합니다.

[!code-csharp[Conceptual.Regex.Language.Options#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/righttoleft1.cs#17)]
[!code-vb[Conceptual.Regex.Language.Options#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/righttoleft1.vb#17)]

lookahead 어설션(`(?=`*subexpression*`)` 언어 요소) 및 lookbehind 어설션(`(?<=`*subexpression*`)` 언어 요소)은 방향을 변경하지 않습니다. lookahead 어설션은 오른쪽을 확인하고, lookbehind 어설션은 왼쪽을 확인합니다. 예를 들어, 정규식 `(?<=\d{1,2}\s)\w+,?\s\d{4}`에서는 lookbehind 어설션을 사용하여 월 이름 앞에 있는 날짜에 대해 테스트합니다. 그런 다음 정규식은 월 및 연도를 일치시킵니다. lookahead 및 lookbehind 어설션에 대한 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.

[!code-csharp[Conceptual.Regex.Language.Options#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/righttoleft2.cs#18)]
[!code-vb[Conceptual.Regex.Language.Options#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/righttoleft2.vb#18)]

이 정규식 패턴은 다음 테이블과 같이 정의됩니다.

|무늬|설명|
|-------------|-----------------|
|`(?<=\d{1,2}\s)`|일치 항목의 시작 부분 앞에는 한 개 또는 두 개의 10진수와 그 뒤에 공백이 하나 있어야 합니다.|
|`\w+`|하나 이상의 단어 문자를 찾습니다.|
|`,?`|0개 또는 1개의 쉼표 문자를 찾습니다.|
|`\s`|공백 문자를 찾습니다.|
|`\d{4}`|네 개의 10진수를 찾습니다.|

[맨 위로 이동](#Top)

<a name="ECMAScript"></a>

## <a name="ecmascript-matching-behavior"></a>ECMAScript 일치 동작

기본적으로 정규식 엔진은 정규식 패턴을 입력 텍스트에 일치시킬 때 정식 동작을 사용합니다. 그러나 <xref:System.Text.RegularExpressions.RegexOptions.ECMAScript?displayProperty=nameWithType> 옵션을 지정하여 ECMAScript 일치 동작을 사용하도록 정규식 엔진에 지시할 수 있습니다.

> [!NOTE]
> ECMAScript와 호환되는 동작은 <xref:System.Text.RegularExpressions.RegexOptions.ECMAScript?displayProperty=nameWithType> 값을 `options` 클래스 생성자 또는 정적 패턴 일치 메서드의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 제공해서만 사용할 수 있으며, 인라인 옵션으로는 사용할 수 없습니다.

<xref:System.Text.RegularExpressions.RegexOptions.ECMAScript?displayProperty=nameWithType> 옵션은 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 및 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션과만 조합할 수 있습니다. 정규식에 다른 옵션을 사용하면 <xref:System.ArgumentOutOfRangeException>이 발생합니다.

ECMAScript의 동작과 정식 정규식의 동작은 문자 클래스 구문, 자신을 참조하는 캡처링 그룹 및 8진수 대 역참조 해석의 세 가지 영역에서 다릅니다.

- 문자 클래스 구문. 정식 정규식은 유니코드를 지원하는 반면 ECMAScript는 지원하지 않으므로, ECMAScript의 문자 클래스의 구문이 더 제한되어 있으며 일부 문자 클래스 언어 요소는 다른 의미를 지닙니다. 예를 들어, ECMAScript는 유니코드 범주 또는 블록 요소 `\p` 및 `\P`와 같은 언어 요소를 지원하지 않습니다. 마찬가지로, 단어 문자와 일치하는 `\w` 요소는 ECMAScript를 사용할 경우 `[a-zA-Z_0-9]` 문자 클래스와 동일하고 정식 동작을 사용할 경우 `[\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}\p{Lm}]`와 동일합니다. 자세한 내용은 [문자 클래스](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)를 참조하세요.

  다음 예제에서는 정식 패턴 일치와 ECMAScript 패턴 일치 간의 차이점을 보여 줍니다. 이 예제에서는 뒤에 공백 문자가 있는 단어와 일치하는 정규식 `\b(\w+\s*)+`를 정의합니다. 입력은 두 개의 문자열로 구성되어 있는데, 한 문자열은 라틴 문자 집합을 사용하고 다른 문자열은 키릴 자모 문자 집합을 사용합니다. 출력에 표시된 것처럼, ECMAScript 일치를 사용하는 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 메서드에 대한 호출은 키릴 자모 단어와 일치하지 않는 반면 정식 일치를 사용하는 메서드 호출은 이러한 단어와 일치합니다.

  [!code-csharp[Conceptual.Regex.Language.Options#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/ecmascript1.cs#16)]
  [!code-vb[Conceptual.Regex.Language.Options#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/ecmascript1.vb#16)]

- 자신을 참조하는 캡처링 그룹. 자신에 대한 역참조가 있는 정규식 캡처 클래스는 각 캡처 반복으로 업데이트되어야 합니다. 다음 예제에서 보여 주는 것처럼, 이 기능은 정규식 `((a+)(\1) ?)+`가 ECMAScript를 사용할 경우에는 입력 문자열 " aa aaaa aaaaaa "과 일치하고 정식 일치를 사용할 경우에는 일치하지 않도록 합니다.

  [!code-csharp[Conceptual.Regex.Language.Options#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/ecmascript2.cs#21)]
  [!code-vb[Conceptual.Regex.Language.Options#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/ecmascript2.vb#21)]

  정규식은 다음 테이블과 같이 정의됩니다.

  |무늬|설명|
  |-------------|-----------------|
  |(a+)|문자 "a"를 1개 이상 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|
  |(\1)|첫 번째 캡처링 그룹에 의해 캡처된 부분 문자열을 찾습니다. 이 그룹은 세 번째 캡처링 그룹입니다.|
  |?|0개 또는 1개의 공백 문자를 찾습니다.|
  |((a+)(\1) ?)+|하나 이상의 "a" 문자 다음에 첫 번째 캡처링 그룹과 일치하는 문자열이 있고 그 다음에 0개 또는 1개의 공백 문자가 한 번 이상 나타나는 패턴을 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|

- 8진수 이스케이프와 역참조 간의 모호성 해결. 다음 테이블에는 정식 정규식과 ECMAScript 정규식에서 8진수 대 역참조 해석의 차이점이 요약되어 있습니다.

  |정규식|정식 동작|ECMAScript 동작|
  |------------------------|------------------------|-------------------------|
  |`\0` 뒤에 0-2자리의 8진수|8진수로 해석됩니다. 예를 들어, `\044`는 항상 8진수 값으로 해석되며 "$"를 의미합니다.|동일한 동작입니다.|
  |`\` 뒤에 1-9의 숫자 한 개, 그 뒤에 추가 10진수가 없음|역참조로 해석됩니다. 예를 들어, `\9`는 9번째 캡처링 그룹이 없더라도 항상 역참조 9를 의미합니다. 캡처링 그룹이 없는 경우 정규식 파서는 <xref:System.ArgumentException>을 throw합니다.|한 자리 10진수 캡처링 그룹이 있는 경우 해당 숫자를 역참조합니다. 그러지 않으면 값이 리터럴로 해석됩니다.|
  |`\` 뒤에 1-9의 숫자 한 개, 그 뒤에 추가 10진수가 있음|숫자가 10진수 값으로 해석됩니다. 해당 캡처링 그룹이 있는 경우 식이 역참조로 해석됩니다.<br /><br /> 그러지 않으면 최대 8진수 377까지 선행 8진수가 해석됩니다. 즉, 값의 낮은 8비트만 고려합니다. 나머지 숫자는 리터럴로 해석됩니다. 예를 들어, `\3000` 식에서 캡처링 그룹 300이 있는 경우 역참조 300으로 해석됩니다. 캡처링 그룹 300이 없는 경우 8진수 300 뒤에 0이 있는 것으로 해석됩니다.|가능한 한 많은 숫자를 캡처를 참조할 수 있는 10진수 값으로 변환하여 역참조로 해석됩니다. 숫자를 변환할 수 없는 경우 최대 8진수 377까지 선행 8진수를 사용하여 8진수로 해석됩니다. 나머지 숫자는 리터럴로 해석됩니다.|

[맨 위로 이동](#Top)

<a name="Invariant"></a>

## <a name="comparison-using-the-invariant-culture"></a>고정 문화권을 사용한 비교

기본적으로 정규식 엔진은 대/소문자를 구분하지 않는 비교를 수행할 때 현재 문화권의 대/소문자 사용 규칙을 사용하여 동일한 대문자와 소문자를 확인합니다.

그러나 이 동작은 일부 비교 형식에는 바람직하지 않은데, 특히 사용자 입력을 시스템 리소스의 이름과 비교할 때 그렇습니다(예: 암호, 파일 또는 URL). 다음 예제에서는 이러한 상황을 시나리오로 보여 줍니다. 이 코드는 URL 앞에 **FILE://** 가 있는 모든 리소스에 대한 액세스를 차단하도록 작성되었습니다. 이 정규식에서는 정규식 `$FILE://`를 사용하여 문자열에 대해 대/소문자를 구분하지 않는 일치를 시도합니다. 그러나 현재 시스템 문화권이 tr-TR(터키어-터키)인 경우 "I"는 "i"의 대문자에 해당하는 문자가 아닙니다. 따라서 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드에 대한 호출에서 `false`를 반환하고 파일에 대한 액세스가 허용됩니다.

[!code-csharp[Conceptual.Regex.Language.Options#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/culture1.cs#14)]
[!code-vb[Conceptual.Regex.Language.Options#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/culture1.vb#14)]

> [!NOTE]
> 대/소문자를 구분하고 고정 문화권을 사용하는 문자열 비교에 대한 자세한 내용은 [문자열 사용에 대한 유용한 정보](../../../docs/standard/base-types/best-practices-strings.md)를 참조하세요.

현재 문화권의 대/소문자를 구분하지 않는 비교를 사용하는 대신 <xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant?displayProperty=nameWithType> 옵션을 지정하여 언어의 문화적 차이를 무시하고 고정 문화권의 규칙을 사용할 수 있습니다.

> [!NOTE]
> 고정 문화권을 사용하는 비교는 <xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant?displayProperty=nameWithType> 값을 `options` 클래스 생성자 또는 정적 패턴 일치 메서드의 <xref:System.Text.RegularExpressions.Regex> 매개 변수에 제공해서만 사용할 수 있으며, 인라인 옵션으로는 사용할 수 없습니다.

다음 예제는 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType>를 포함하는 옵션을 사용하여 정적 <xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant?displayProperty=nameWithType> 메서드를 호출한다는 점을 제외하고 이전 예제와 동일합니다. 현재 문화권이 터키어(터키)로 설정된 경우에도 정규식 엔진은 성공적으로 "FILE"과 "file"을 일치시키고 파일 리소스에 대한 액세스를 차단할 수 있습니다.

[!code-csharp[Conceptual.Regex.Language.Options#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.options/cs/culture1.cs#15)]
[!code-vb[Conceptual.Regex.Language.Options#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.options/vb/culture1.vb#15)]

## <a name="see-also"></a>참고 항목

- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
