---
title: 정규식의 대체
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, substitutions
- replacement patterns
- metacharacters, substitutions
- .NET Framework regular expressions, substitutions
- constructs, substitutions
- substitutions
ms.assetid: d1f52431-1c7d-4dc6-8792-6b988256892e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4b079809fa76097cd575d96c70d17d1c6c85e3a1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968534"
---
# <a name="substitutions-in-regular-expressions"></a>정규식의 대체
<a name="Top"></a> 대체는 바꾸기 패턴에서만 인식되는 언어 요소입니다. 정규식 패턴을 사용하여 입력 문자열에서 일치하는 텍스트를 바꿀 텍스트의 전부 또는 일부를 정의합니다. 바꾸기 패턴은 리터럴 문자와 하나 이상의 대체로 구성될 수 있습니다. <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 매개 변수가 포함된 `replacement` 메서드의 오버로드와 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 메서드에 대해 바꾸기 패턴이 제공됩니다. 해당 메서드는 일치하는 패턴을 `replacement` 매개 변수에 정의된 패턴으로 바꿉니다.  
  
 .NET Framework에서 다음 표에 나와 있는 대체 요소를 정의합니다.  
  
|대체|설명|  
|------------------|-----------------|  
|$ *number*|*number*(여기서 *number* 는 10진수 값)로 식별되는 캡처 그룹과 일치하는 마지막 부분 문자열을 바꾸기 문자열에 포함합니다. 자세한 내용은 [번호 매겨진 그룹 대체](#Numbered)를 참조하십시오.|  
|${ *name* }|`(?<`*name*`> )` 에서 지정한 명명된 그룹과 일치하는 마지막 부분 문자열을 바꾸기 문자열에 포함합니다. 자세한 내용은 [명명된 그룹 대체](#Named)를 참조하십시오.|  
|$$|대체 문자열에 한 개의 "$" 리터럴을 포함합니다. 자세한 내용은 ["$" 기호 대체](#DollarSign)를 참조하십시오.|  
|$&|대체 문자열에 일치하는 전체 문자열의 복사본을 포함합니다. 자세한 내용은 [일치하는 전체 문자열 대체](#EntireMatch)를 참조하십시오.|  
|$\`|대체 문자열에서 일치하는 문자열 앞에 입력 문자열의 모든 텍스트를 포함합니다. 자세한 내용은 [일치하는 문자열 앞에 있는 텍스트 대체](#BeforeMatch)를 참조하십시오.|  
|$'|대체 문자열에서 일치하는 문자열 뒤에 입력 문자열의 모든 텍스트를 포함합니다. 자세한 내용은 [일치하는 문자열 뒤에 있는 텍스트 대체](#AfterMatch)를 참조하십시오.|  
|$+|대체 문자열에 캡처된 마지막 그룹을 포함합니다. 자세한 내용은 [캡처된 마지막 그룹 대체](#LastGroup)를 참조하십시오.|  
|$_|대체 문자열에 전체 입력 문자열을 포함합니다. 자세한 내용은 [전체 입력 문자열 대체](#EntireString)를 참조하십시오.|  
  
## <a name="substitution-elements-and-replacement-patterns"></a>요소 및 바꾸기 패턴 대체  
 대체는 바꾸기 패턴에서 인식되는 유일한 특수 구문입니다. 임의의 문자를 찾는 마침표(`.`) 및 문자 이스케이프 등 다른 정규식 언어 요소는 지원되지 않습니다. 마찬가지로, 대체 언어 요소는 바꾸기 패턴에서만 인식되고 정규식 패턴에는 사용할 수 없습니다.  
  
 컨텍스트마다 다른 의미를 가지지만 정규식 패턴이나 대체에 나타나는 유일한 문자는 `$` 문자입니다. 정규식 패턴에서 `$` 는 문자열의 끝 부분을 찾는 앵커입니다. 바꾸기 패턴에서 `$` 는 대체 시작을 나타냅니다.  
  
> [!NOTE]
> 정규식의 바꾸기 패턴과 유사한 기능으로, 역참조를 사용합니다. 역참조에 대한 자세한 내용은 [역참조 구문](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md)을 참조하십시오.  
  
<a name="Numbered"></a>   
## <a name="substituting-a-numbered-group"></a>번호 매겨진 그룹 대체  
 `$`*number* 언어 요소는 바꾸기 문자열에서 *number* 캡처 그룹과 일치하는 마지막 부분 문자열을 포함합니다. 여기서 *number* 는 캡처 그룹의 인덱스입니다. 예를 들어 바꾸기 패턴 `$1` 은 일치하는 부분 문자열이 처음 캡처한 그룹으로 대체됨을 나타냅니다. 번호가 매겨진 캡처링 그룹에 대한 자세한 내용은 [Grouping Constructs](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
 `$` 다음에 나오는 모든 숫자는 *number* 그룹에 속한 것으로 해석됩니다. 이런 것을 의도한 것이 아니라면, 그 대신 명명된 그룹을 대체할 수 있습니다. 예를 들어, `${1}1` 대신 `$11` 대체 문자열을 사용하여 대체 문자열을 숫자 "1"과 함께 처음으로 캡처된 그룹의 값으로 정의할 수 있습니다. 자세한 내용은 [명명된 그룹 대체](#Named)를 참조하십시오.  
  
 `(?<`*name*`>)` 구문을 사용하여 명시적으로 이름을 할당하지 않은 그룹을 캡처할 때는 1부터 시작하여 왼쪽에서 오른쪽으로 번호를 매깁니다. 명명된 그룹도 명명되지 않은 마지막 그룹의 인덱스보다 큰 1부터 시작하여 왼쪽에서 오른쪽으로 번호가 매겨집니다. 예를 들어 정규식 `(\w)(?<digit>\d)`에서 `digit` 명명된 그룹의 인덱스는 2입니다.  
  
 *number* 가 정규식 패턴에 정의된 올바른 캡처 그룹을 지정하지 않으면 `$`*number* 는 일치하는 문자열을 바꾸는 데 사용되는 리터럴 문자 시퀀스로 해석됩니다.  
  
 다음 예제에서는 `$`*number* 대체를 사용하여 10진수 값에서 통화 기호를 삭제합니다. 통화 값의 시작 부분이나 끝 부분에 있는 통화 기호를 제거하고 두 개의 가장 일반적인 소수 구분 기호("." 및 ",")를 인식합니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/numberedgroup1.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/numberedgroup1.vb#1)]  
  
 정규식 패턴 `\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\p{Sc}*`|통화 기호 문자를 0개 이상 찾습니다.|  
|`\s?`|0회 이상 나오는 공백 문자를 찾습니다.|  
|`\d+`|하나 이상의 10진수 숫자가 일치하는지 확인합니다.|  
|`[.,]?`|0-1개의 마침표 또는 쉼표를 찾습니다.|  
|`\d*`|0번 이상 나오는 10진수를 찾습니다.|  
|`(\s?\d+[.,]?\d*)`|공백, 하나 이상의 10진수 숫자, 0-1개의 마침표나 쉼표, 0-1개의 10진수 숫자가 차례로 표시된 문자열을 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다. 바꾸기 패턴이 `$1`이기 때문에 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 메서드를 호출하면 일치하는 전체 부분 문자열이 이 캡처된 그룹으로 바뀝니다.|  
  
 [맨 위로 이동](#Top)  
  
<a name="Named"></a>   
## <a name="substituting-a-named-group"></a>명명된 그룹 대체  
 `${`*name*`}` 언어 요소는 *name* 캡처 그룹과 일치하는 마지막 부분 문자열을 대체합니다. 여기서 *name* 은 `(?<`*name*`>)` 언어 요소가 정의한 캡처 그룹의 이름입니다. 명명된 캡처링 그룹에 대한 자세한 내용은 [Grouping Constructs](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
 *name* 이 정규식 패턴에 정의된 명명된 유효한 캡처 그룹을 지정하지 않지만 숫자로 구성된 경우, `${`*name*`}` 은 번호가 매겨진 그룹으로 해석됩니다.  
  
 *name* 이 명명된 유효한 캡처 그룹도, 정규식 패턴에 정의되어 번호가 매겨진 유효한 캡처 그룹도 지정하지 않는 경우, `${`*name*`}` 은 각 일치 항목을 바꾸는 데 사용되는 리터럴 문자 시퀀스로 해석됩니다.  
  
 다음 예제에서는 `${`*name*`}` 대체를 사용하여 10진수 값에서 통화 기호를 삭제합니다. 통화 값의 시작 부분이나 끝 부분에 있는 통화 기호를 제거하고 두 개의 가장 일반적인 소수 구분 기호("." 및 ",")를 인식합니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/namedgroup1.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/namedgroup1.vb#2)]  
  
 정규식 패턴 `\p{Sc}*(?<amount>\s?\d[.,]?\d*)\p{Sc}*` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\p{Sc}*`|통화 기호 문자를 0개 이상 찾습니다.|  
|`\s?`|0회 이상 나오는 공백 문자를 찾습니다.|  
|`\d+`|하나 이상의 10진수 숫자가 일치하는지 확인합니다.|  
|`[.,]?`|0-1개의 마침표 또는 쉼표를 찾습니다.|  
|`\d*`|0번 이상 나오는 10진수를 찾습니다.|  
|`(?<amount>\s?\d[.,]?\d*)`|공백, 하나 이상의 10진수 숫자, 0-1개의 마침표나 쉼표, 0-1개의 10진수 숫자가 차례로 표시된 문자열을 찾습니다. 이는 `amount`로 명명된 캡처링 그룹입니다. 바꾸기 패턴이 `${amount}`이기 때문에 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 메서드를 호출하면 일치하는 전체 부분 문자열이 이 캡처된 그룹으로 바뀝니다.|  
  
 [맨 위로 이동](#Top)  
  
<a name="DollarSign"></a>   
## <a name="substituting-a--character"></a>"$" 문자 대체  
 `$$` 대체는 바꾼 문자열에 리터럴 "$" 문자를 삽입합니다.  
  
 다음 예제에서는 <xref:System.Globalization.NumberFormatInfo> 개체를 사용하여 통화 문자열에서 현재 문화권의 통화 기호 및 배치를 확인합니다. 그런 다음 정규식 패턴과 바꾸기 패턴을 동적으로 작성합니다. 현재 문화권이 en-US인 컴퓨터에서 예제가 실행될 경우, 정규식 패턴 `\b(\d+)(\.(\d+))?` 및 바꾸기 패턴 `$$ $1$2`를 생성합니다. 바꾸기 패턴은 일치하는 텍스트를 통화 기호와 공백, 첫 번째 및 두 번째 캡처된 그룹이 차례로 표시된 문자열로 바꿉니다.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/dollarsign1.cs#8)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/dollarsign1.vb#8)]  
  
 정규식 패턴 `\b(\d+)(\.(\d+))?` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계 시작 부분에서 찾기를 시작합니다.|  
|`(\d+)`|하나 이상의 10진수 숫자가 일치하는지 확인합니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`\.`|마침표(소수 구분 기호)를 찾습니다.|  
|`(\d+)`|하나 이상의 10진수 숫자가 일치하는지 확인합니다. 이 그룹은 세 번째 캡처링 그룹입니다.|  
|`(\.(\d+))?`|한 개 이상의 숫자가 뒤에 오는 마침표를 0개 또는 1개 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|  
  
<a name="EntireMatch"></a>   
## <a name="substituting-the-entire-match"></a>일치하는 전체 문자열 대체  
 `$&` 대체는 바꾸기 문자열에 일치하는 전체 문자열을 포함합니다. 일치하는 문자열의 시작 부분이나 끝 부분에 부분 문자열을 추가하는 데 자주 사용됩니다. 예를 들어 `($&)` 바꾸기 패턴은 각 일치 항목의 시작과 끝에 괄호를 추가합니다. 일치하는 부분이 없으면 `$&` 대체가 아무 효과가 없습니다.  
  
 다음 예제에서는 `$&` 대체를 사용하여 문자열 배열에 저장된 책 제목의 시작 부분과 끝 부분에 따옴표를 추가합니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/entirematch1.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/entirematch1.vb#3)]  
  
 정규식 패턴 `^(\w+\s?)+$` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|입력 문자열의 시작 부분에서 일치 항목 찾기를 시작합니다.|  
|`(\w+\s?)+`|하나 이상의 단어 문자 다음에 0개 또는 1개의 공백 문자가 한 번 이상 나타나는 패턴을 찾습니다.|  
|`$`|입력 문자열의 끝 부분을 찾습니다.|  
  
 `"$&"` 바꾸기 패턴은 일치하는 문자열의 시작 부분과 끝 부분에 리터럴 따옴표를 추가합니다.  
  
 [맨 위로 이동](#Top)  
  
<a name="BeforeMatch"></a>   
## <a name="substituting-the-text-before-the-match"></a>일치하는 문자열 앞에 있는 텍스트 대체  
 ``$` `` 대체는 일치하는 문자열을 일치하는 문자열 앞의 전체 입력 문자열로 바꿉니다. 즉, 일치하는 텍스트를 제거하는 동안 일치하는 문자열까지의 입력 문자열을 복제합니다. 일치하는 텍스트 뒤에 나오는 텍스트는 결과 문자열에서 변경되지 않습니다. 입력 문자열에 일치하는 문자열이 여러 개이면 이전 일치 문자열로 텍스트가 바뀐 문자열이 아닌 원본 입력 문자열에서 바꾸기 텍스트가 파생됩니다. \(예제에서 그림을 제공합니다.\) 일치하는 부분이 없으면 ``$` `` 대체가 아무 효과가 없습니다.  
  
 다음 예제에서는 `\d+` 정규식 패턴을 사용하여 입력 문자열에서 하나 이상의 숫자가 연속적으로 표시된 부분을 찾습니다. 바꾸기 문자열 ``$` ``는 이 숫자를 일치하는 문자열 앞의 텍스트로 바꿉니다.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/before1.cs#4)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/before1.vb#4)]  
  
 이 예제에서는 입력 문자열 `"aa1bb2cc3dd4ee5"` 에 다섯 개의 일치 항목이 포함되어 있습니다. 다음 표에서는 ``$` `` 대체를 사용할 경우 정규식 엔진이 입력 문자열에서 일치하는 부분을 어떻게 바꾸는지 보여줍니다. 삽입된 텍스트는 결과 열에서 굵게 표시됩니다.  
  
|일치|위치|일치하는 문자열 앞에 있는 문자열|결과 문자열|  
|-----------|--------------|-------------------------|-------------------|  
|1|2|aa|aa**aa**bb2cc3dd4ee5|  
|2|5|aa1bb|aaaabb**aa1bb**cc3dd4ee5|  
|3|8|aa1bb2cc|aaaabbaa1bbcc**aa1bb2cc**dd4ee5|  
|4|11|aa1bb2cc3dd|aaaabbaa1bbccaa1bb2ccdd**aa1bb2cc3dd**ee5|  
|5|14|aa1bb2cc3dd4ee|aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddee**aa1bb2cc3dd4ee**|  
  
 [맨 위로 이동](#Top)  
  
<a name="AfterMatch"></a>   
## <a name="substituting-the-text-after-the-match"></a>일치하는 문자열 뒤에 있는 텍스트 대체  
 `$'` 대체는 일치하는 문자열을 일치하는 문자열 뒤의 전체 입력 문자열로 바꿉니다. 즉, 일치하는 텍스트를 제거하는 동안 일치하는 문자열 뒤의 입력 문자열을 복제합니다. 일치하는 텍스트 앞에 나오는 텍스트는 결과 문자열에서 변경되지 않습니다. 일치하는 부분이 없으면  `$'` 대체가 아무 효과가 없습니다.  
  
 다음 예제에서는 `\d+` 정규식 패턴을 사용하여 입력 문자열에서 하나 이상의 숫자가 연속적으로 표시된 부분을 찾습니다. 바꾸기 문자열 `$'` 는 이 숫자를 일치하는 문자열 뒤의 텍스트로 바꿉니다.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/after1.cs#5)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/after1.vb#5)]  
  
 이 예제에서는 입력 문자열 `"aa1bb2cc3dd4ee5"` 에 다섯 개의 일치 항목이 포함되어 있습니다. 다음 표에서는 `$'` 대체를 사용할 경우 정규식 엔진이 입력 문자열에서 일치하는 부분을 어떻게 바꾸는지 보여줍니다. 삽입된 텍스트는 결과 열에서 굵게 표시됩니다.  
  
|일치|위치|일치하는 문자열 뒤에 있는 문자열|결과 문자열|  
|-----------|--------------|------------------------|-------------------|  
|1|2|bb2cc3dd4ee5|aa**bb2cc3dd4ee5**bb2cc3dd4ee5|  
|2|5|cc3dd4ee5|aabb2cc3dd4ee5bb**cc3dd4ee5**cc3dd4ee5|  
|3|8|dd4ee5|aabb2cc3dd4ee5bbcc3dd4ee5cc**dd4ee5**dd4ee5|  
|4|11|ee5|aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5dd**ee5**ee5|  
|5|14|<xref:System.String.Empty?displayProperty=nameWithType>|aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5ddee5ee|  
  
 [맨 위로 이동](#Top)  
  
<a name="LastGroup"></a>   
## <a name="substituting-the-last-captured-group"></a>캡처된 마지막 그룹 대체  
 `$+` 대체는 일치하는 문자열을 캡처된 마지막 그룹으로 바꿉니다. 캡처된 그룹이 없거나 캡처된 마지막 그룹 값이 <xref:System.String.Empty?displayProperty=nameWithType>이면 `$+` 대체가 적용되지 않습니다.  
  
 다음 예제에서는 문자열에서 중복 단어를 확인한 다음 `$+` 대체를 사용하여 해당 단어가 한 번만 나타나도록 바꿉니다. <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션은 대소문자만 다르고 나머지는 동일한 단어를 중복으로 인식하도록 하는 데 사용됩니다.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/lastmatch1.cs#6)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/lastmatch1.vb#6)]  
  
 정규식 패턴 `\b(\w+)\s\1\b` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`(\w+)`|하나 이상의 단어 문자를 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`\s`|공백 문자를 찾습니다.|  
|`\1`|캡처된 첫 번째 그룹을 찾습니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 [맨 위로 이동](#Top)  
  
<a name="EntireString"></a>   
## <a name="substituting-the-entire-input-string"></a>전체 입력 문자열 대체  
 `$_` 대체는 일치하는 문자열을 전체 입력 문자열로 바꿉니다. 즉, 일치하는 텍스트를 제거한 다음 일치하는 텍스트를 포함한 전체 문자열로 바꿉니다.  
  
 다음 예제에서는 입력 문자열에서 하나 이상의 10진수 숫자를 찾습니다. `$_` 대체를 사용하여 전체 입력 문자열로 바꿉니다.  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/entire1.cs#7)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/entire1.vb#7)]  
  
 이 예제에서는 입력 문자열 `"ABC123DEF456"` 에 두 개의 일치 항목이 포함되어 있습니다. 다음 표에서는 `$_` 대체를 사용할 경우 정규식 엔진이 입력 문자열에서 일치하는 부분을 어떻게 바꾸는지 보여줍니다. 삽입된 텍스트는 결과 열에서 굵게 표시됩니다.  
  
|일치|위치|일치|결과 문자열|  
|-----------|--------------|-----------|-------------------|  
|1|3|123|ABC**ABC123DEF456**DEF456|  
|2|5|456|ABCABC123DEF456DEF**ABC123DEF456**|  
  
## <a name="see-also"></a>참고 항목

- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
