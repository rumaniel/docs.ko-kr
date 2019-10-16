---
title: .NET 정규식의 역참조 구문
description: 정규식의 역참조 구문을 사용하여 반복되는 텍스트 요소를 식별하는 방법을 알아봅니다.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- backreferences
- constructs, backreference
- .NET Framework regular expressions, backreference constructs
- regular expressions, backreference constructs
ms.assetid: 567a4b8d-0e79-49dc-8df9-f4b1aa376a2a
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 11df25617a618cdc835ca6555c671a187ce09f8d
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991651"
---
# <a name="backreference-constructs-in-regular-expressions"></a>정규식의 역참조 구문

역참조는 문자열 내에서 반복된 문자 또는 부분 문자열을 식별하는 편리한 방법을 제공합니다. 예를 들어 입력 문자열에 임의의 부분 문자열이 여러 번 포함되어 있으면 첫 번째 발생을 캡처링 그룹과 일치시킨 다음 역참조를 사용하여 부분 문자열의 후속 발생을 일치시킬 수 있습니다.

> [!NOTE]
> 대체 문자열에서 명명된 캡처링 그룹과 번호가 매겨진 캡처링 그룹을 참조하기 위해 별도의 구문이 사용됩니다. 자세한 내용은 [대체](substitutions-in-regular-expressions.md)를 참조하세요.

.NET에서는 번호가 매겨진 캡처링 그룹과 명명된 캡처링 그룹을 참조하기 위해 별도의 언어 요소를 정의합니다. 캡처링 그룹에 대한 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.

## <a name="numbered-backreferences"></a>번호가 매겨진 역참조

번호가 매겨진 역참조에는 다음 구문이 사용됩니다.

`\` *number*

여기서 *number*는 정규식에서 캡처링 그룹의 서수 위치입니다. 예를 들어 `\4`는 네 번째 캡처링 그룹의 내용을 찾습니다. *number*가 정규식 패턴에서 정의되지 않은 경우 구문 분석 오류가 발생하고 정규식 엔진이 <xref:System.ArgumentException>을 throw합니다. 예를 들어 `\b(\w+)\s\1` 정규식은 `(\w+)`가 식의 첫 번째이자 유일한 캡처링 그룹이기 때문에 유효합니다. 반면에 `\b(\w+)\s\2`는 `\2`로 번호가 매겨진 캡처링 그룹이 없기 때문에 유효하지 않으며 인수 예외를 throw합니다. 또한 *번호*가 특정 서수 위치에서 캡처링 그룹을 식별하지만 해당 캡처링 그룹이 서수 위치가 아닌 다른 숫자 이름을 할당받은 경우 정규식 파서는 <xref:System.ArgumentException>을 throw합니다.

8진수 이스케이프 코드(예: `\16`)와 동일한 표기법을 사용하는 `\`*number* 역참조 간의 모호성에 유의하세요. 이러한 모호성은 다음과 같이 해결됩니다.

- `\1`에서 `\9` 사이의 식은 항상 8진수 코드가 아니라 역참조로 해석됩니다.

- 다중 숫자 식의 첫 번째 숫자가 8 또는 9이면(예: `\80` 또는 `\91`) 식은 리터럴로 해석됩니다.

- `\10` 이상인 식은 이 숫자에 해당하는 역참조가 있을 경우 역참조로 간주되고, 없을 경우 8진수 코드로 해석됩니다.

- 정규식에 정의되지 않은 그룹 번호에 대한 역참조가 포함되어 있으면 구문 분석 오류가 발생하고 정규식 엔진이 <xref:System.ArgumentException>을 throw합니다.

모호성 문제가 발생하는 경우 명확하고 8진수 문자 코드와 혼동되지 않는 `\k<`*name*`>` 표기법을 사용할 수 있습니다. 마찬가지로, `\xdd` 등의 16진수 코드는 명확하며 역참조와 혼동되지 않습니다.

다음 예제에서는 문자열에서 2배 워드 문자를 찾습니다. 다음과 같은 요소로 구성된 `(\w)\1` 정규식을 정의합니다.

|요소|설명|
|-------------|-----------------|
|`(\w)`|단어 문자를 찾아 첫 번째 캡처링 그룹에 할당합니다.|
|`\1`|첫 번째 캡처링 그룹의 값과 일치하는 다음 문자를 찾습니다.|

[!code-csharp[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference1.cs#1)]
[!code-vb[RegularExpressions.Language.Backreferences#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference1.vb#1)]

## <a name="named-backreferences"></a>명명된 역참조

명명된 역참조는 다음 구문을 사용하여 정의됩니다.

`\k<` *name* `>`

또는

`\k'` *name* `'`

여기서 *name*은 정규식 패턴에 정의된 캡처링 그룹의 이름입니다. *name*이 정규식 패턴에서 정의되지 않은 경우 구문 분석 오류가 발생하고 정규식 엔진이 <xref:System.ArgumentException>을 throw합니다.

다음 예제에서는 문자열에서 2배 워드 문자를 찾습니다. 다음과 같은 요소로 구성된 `(?<char>\w)\k<char>` 정규식을 정의합니다.

|요소|설명|
|-------------|-----------------|
|`(?<char>\w)`|단어 문자를 찾아 이름이 `char`인 캡처링 그룹에 할당합니다.|
|`\k<char>`|`char` 캡처링 그룹의 값과 일치하는 다음 문자를 찾습니다.|

[!code-csharp[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference2.cs#2)]
[!code-vb[RegularExpressions.Language.Backreferences#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference2.vb#2)]

## <a name="named-numeric-backreferences"></a>명명된 숫자 역참조

`\k`를 사용하는 명명된 역참조에서 *이름*은 숫자의 문자열 표현일 수도 있습니다. 예를 들어 다음 예제에서는 `(?<2>\w)\k<2>` 정규식을 사용하여 문자열에서 2배 워드 문자를 찾습니다. 이 경우에 예제에서는 명시적으로 "2"라고 명명된 캡처링 그룹을 정의하고 따라서 역참조는 "2"라고 명명됩니다.

[!code-csharp[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference3.cs#3)]
[!code-vb[RegularExpressions.Language.Backreferences#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference3.vb#3)]

*이름*이 숫자의 문자열 표현이고 해당 이름을 가 진 캡처링 그룹이 없는 경우 `\k<`*이름*`>`은 역참조 `\` *숫자*와 같습니다. 여기서 *번호*는 캡처의 서수 위치입니다. 다음 예제에는 `char`라는 단일 캡처링 그룹이 있습니다. 역참조 구문은 `\k<1>`로 참조합니다. 예제의 출력이 표시한 대로 `char`가 첫 번째 캡처링 그룹이기 때문에 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType>에 대한 호출이 성공합니다.

[!code-csharp[Ordinal.Backreference](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference6.cs)]
[!code-vb[Ordinal.BackReference](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference6.vb)]

그러나 경우 *이름*이 숫자의 문자열 표현이고 해당 위치에 있는 캡처링 그룹이 명시적으로 숫자 이름을 할당받지 않은 경우 정규식 파서는 서수 위치를 기준으로 캡처링 그룹을 식별할 수 없습니다. 대신 <xref:System.ArgumentException>을 throw합니다. 다음 예제의 캡처링 그룹만이 “2”라고 명명됩니다. `\k` 구문을 사용하여 "1"이라는 역참조를 정의하기 때문에 정규식 파서는 첫 번째 캡처링 그룹을 식별할 수 없고 예외를 throw합니다.

[!code-csharp[Ordinal.Backreference](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference7.cs)]
[!code-vb[Ordinal.BackReference](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference7.vb)]

## <a name="what-backreferences-match"></a>역참조에서 찾는 대상

역참조는 그룹의 가장 최근 정의(왼쪽에서 오른쪽으로 찾을 경우 가장 왼쪽에 있는 정의)를 가리킵니다. 그룹에서 여러 개의 캡처를 만드는 경우 역참조는 가장 최근 캡처를 가리킵니다.

다음 예제에는 이름이 \1인 그룹을 다시 정의하는 정규식 패턴 `(?<1>a)(?<1>\1b)*`가 포함되어 있습니다. 다음 표에서는 정규식의 각 패턴에 대해 설명합니다.

|무늬|설명|
|-------------|-----------------|
|`(?<1>a)`|문자 “a”를 찾은 다음, 이름이 `1`인 캡처링 그룹에 결과를 할당합니다.|
|`(?<1>\1b)*`|이름이 `1`과 "b"로 지정된 그룹을 0번 이상 일치시키고, 이름이 `1`로 지정된 캡처링 그룹에 결과를 할당합니다.|

[!code-csharp[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference4.cs#4)]
[!code-vb[RegularExpressions.Language.Backreferences#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference4.vb#4)]

입력 문자열("aababb")과 정규식을 비교할 때 정규식 엔진은 다음 작업을 수행합니다.

1. 문자열의 시작 부분에서 시작하여 `(?<1>a)` 식으로 "a"를 찾습니다. `1` 그룹의 값은 이제 “a”입니다.

2. 두 번째 문자로 진행하여 `\1b` 또는 "ab" 식으로 "ab" 문자열을 찾습니다. 그런 다음 결과 "ab"를 `\1`에 할당합니다.

3. 네 번째 문자로 진행합니다. `(?<1>\1b)*` 식은 0번 이상 일치할 수 있으므로 `\1b` 식으로 "abb" 문자열을 찾습니다. 결과 "abb"를 `\1`에 다시 할당합니다.

이 예제에서 `*`는 반복 수량자로, 정규식 엔진이 정의되는 패턴을 찾을 수 없을 때까지 반복해서 평가됩니다. 반복 수량자는 그룹 정의를 지우지 않습니다.

그룹에서 부분 문자열을 캡처하지 않은 경우 해당 그룹에 대한 역참조가 정의되지 않으며 일치되지 않습니다. 이 내용은 다음과 같이 정의된 정규식 패턴 `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b`를 통해 확인할 수 있습니다.

|무늬|설명|
|-------------|-----------------|
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|
|`(\p{Lu}{2})`|두 개의 대문자를 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|
|`(\d{2})?`|두 개의 10진수를 0번 또는 한 번 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|
|`(\p{Lu}{2})`|두 개의 대문자를 찾습니다. 이 그룹은 세 번째 캡처링 그룹입니다.|
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|

두 번째 캡처링 그룹에서 정의된 두 개의 10진수가 없는 경우에도 입력 문자열이 이 정규식과 일치할 수 있습니다. 다음 예제에서는 일치가 성공해도 성공적인 두 캡처링 그룹 사이에 빈 캡처링 그룹이 있음을 보여 줍니다.

[!code-csharp[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.backreferences/cs/backreference5.cs#5)]
[!code-vb[RegularExpressions.Language.Backreferences#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.backreferences/vb/backreference5.vb#5)]

## <a name="see-also"></a>참고 항목

- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
