---
title: 정규식 동작 정보
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, behavior
- .NET Framework regular expressions, behavior
ms.assetid: 0ee1a6b8-caac-41d2-917f-d35570021b10
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f4d7cbd00dbf94900185643490b952ced7887965
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895225"
---
# <a name="details-of-regular-expression-behavior"></a>정규식 동작 정보
.NET Framework 정규식 엔진은 Perl, Python, Emacs 및 Tcl에서 사용하는 것과 같은 기존의 NFA(Nondeterministic Finite Automaton) 엔진을 통합하는 역추적 정규식 일치 도구입니다. 이를 통해 해당 awk, egrep 또는 lex와 같은 빠르지만 제한적인 순수 정규식 DFA(Deterministic Finite Automaton) 엔진과 구분합니다. 또한 표준화되지만 느린 POSIX NFA과도 구분합니다. 다음 섹션에서는 세 가지 유형의 정규식 엔진을 설명하고 기존 NFA 엔진을 사용하여 .NET Framework의 정규식을 구현하는 이유를 설명합니다.  
  
## <a name="benefits-of-the-nfa-engine"></a>NFA 엔진의 이점  
 DFA 엔진에서 패턴 일치를 수행하는 경우 해당 처리 순서는 입력 문자열에 의해 결정됩니다. 엔진은 입력 문자열의 처음부터 시작해서 순차적으로 다음 문자가 정규식 패턴과 일치하는지 여부를 확인합니다. 가능한 가장 긴 문자열을 찾도록 보장할 수 있습니다. 동일한 문자를 두 번 테스트하지 않기 때문에 DFA 엔진은 역추적을 지원하지 않습니다. 그러나 DFA 엔진에 유한 상태만 포함되기 때문에 역참조를 사용하는 패턴과 일치하지 않으며 명시적 확장을 생성하지 않기 때문에 하위 식을 캡처할 수 없습니다.  
  
 DFA 엔진과 달리 기존의 NFA 엔진이 패턴 일치를 수행할 경우 해당 처리 순서는 정규식 패턴에 의해 결정됩니다. 특정 언어 요소를 처리하는 경우와 같이 엔진은 탐욕적 일치를 사용합니다. 즉, 가능한 한 입력 문자열의 수만큼 찾습니다. 하지만 성공적으로 하위 식을 찾은 후에 해당 상태를 저장하기도 합니다. 일치에 결국 실패하면 엔진이 추가 일치를 시도할 수 있도록 저장된 상태로 돌아갈 수 있습니다. 정규식에서 이후 언어 요소가 일치할 수 있도록 성공적인 하위 식 찾기를 포기하는 이 프로세스를 ‘역추적’이라고 합니다.  NFA 엔진은 역추적을 사용하여 특정 순서에 따라 정규식에서 가능한 모든 확장을 테스트하고 첫 번째 일치 항목을 수락합니다. 기존의 NFA 엔진이 성공적으로 일치를 수행하기 위해 정규식의 특정 확장을 구성하기 때문에 하위 식 일치 및 일치 역참조를 캡처할 수 있습니다. 그러나 기존의 NFA가 역추적하기 때문에 다른 경로를 통해 그 상태가 된 경우 여러 번 동일한 상태가 될 수 있습니다. 결과적으로 최악의 경우 상당히 느리게 실행될 수 있습니다. 기존 NFA 엔진이 발견한 첫 번째 이치를 수용하기 때문에 다른 일치 항목(더 긴 일치일 가능성이 높음)도 밝히지 않은 상태로 둘 수 있습니다.  
  
 POSIX NFA 엔진은 가장 긴 일치 항목을 발견했다고 보장할 수 있을 때까지 역추적을 계속한다는 점을 제외하면 기존의 NFA 엔진과 같습니다. 결과적으로 POSIX NFA 엔진은 기존 NFA 엔진보다 느립니다. 따라서 POSIX NFA 엔진을 사용하는 경우 역추적 검사의 순서를 변경하여 긴 일치 항목보다 짧은 일치 항목을 우선할 수 없습니다.  
  
 기존의 NFA 엔진은 DFA 또는 POSIX NFA 엔진보다 일치하는 문자열을 효율적으로 제어하기 때문에 프로그래머로부터 선호되었습니다. 최악의 경우 실행 속도가 느려질 수 있지만 모호성을 줄이고 역추적을 제한하는 패턴을 사용하여 선형 또는 다항 시간에서 일치 항목을 찾도록 조정할 수 있습니다. 즉, NFA 엔진은 강력함과 유연성을 제공하는 대신 성능이 떨어지지만 대부분의 경우에 정규식을 잘 작성하여 역추적이 성능을 기하급수적으로 저하시키지 않도록 방지한다면 사용 가능한 적절한 성능을 제공합니다.  
  
> [!NOTE]
> 과도한 역추적으로 인해 발생한 성능 저하 및 이를 해결하는 정규식을 만드는 방법에 대한 자세한 내용은 [역추적](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)을 참조하세요.  
  
## <a name="net-framework-engine-capabilities"></a>.NET Framework 엔진 기능  
 기존 NFA 엔진의 이점을 누리려면 .NET Framework 정규식 엔진에는 프로그래머가 역추적 엔진을 조정할 수 있는 일련의 구문이 포함되어 있습니다. 이러한 구문을 사용하여 일치 항목을 빠르게 찾거나 다른 일치 항목에 대한 특정 확장을 우선할 수 있습니다.  
  
 .NET Framework 정규식 엔진의 다른 기능은 다음과 같습니다.  
  
- 게으른 수량자: `??`, `*?`, `+?`, `{`*n*`,`*m*`}?` 이러한 구문은 역추적 엔진이 최소 반복 횟수를 먼저 검색하도록 지시합니다. 반면, 일반적인 탐욕적 수량자는 먼저 최대 반복 횟수를 찾으려고 합니다. 다음 예제에서는 둘 사이의 차이점을 보여 줍니다. 정규식은 숫자로 끝나는 문장을 찾고 캡처링 그룹은 해당 숫자를 추출하려고 합니다. 정규식 `.+(\d+)\.`은 탐욕적 수량자 `.+`를 포함하며 이로 인해 정규식 엔진은 번호의 마지막 숫자만 캡처하게 됩니다. 반대로 정규식 `.+?(\d+)\.`은 게으른 수량자 `.+?`를 포함하며 이로 인해 정규식 엔진은 전체 번호를 캡처하게 됩니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lazy1.cs#1)]
     [!code-vb[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lazy1.vb#1)]  
  
     이 정규식의 최대 일치 버전 및 최소 일치 버전은 다음 표와 같이 정의됩니다.
  
    |무늬|설명|  
    |-------------|-----------------|  
    |`.+`(탐욕적 수량자)|적어도 한 번 문자를 찾습니다. 그러면 정규식 엔진이 전체 문자열을 검색하고 필요한 패턴의 나머지 부분을 찾는 데 필요한 역추적을 수행합니다.|  
    |`.+?`(게으른 수량자)|적어도 한 번 문자를 찾지만 가능한 한 적게 일치합니다.|  
    |`(\d+)`|적어도 하나의 숫자 문자를 찾아 첫 번째 캡처링 그룹에 할당합니다.|  
    |`\.`|마침표를 찾습니다.|  
  
     수량자에 대한 자세한 내용은 [수량자](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)를 참조하세요.  
  
- 긍정 lookahead: `(?=`*subexpression*`)`. 이 기능을 사용하면 역추적 검사 엔진이 하위 식을 찾은 후에 텍스트의 동일한 지점으로 돌아오게 합니다. 동일한 위치에서 시작하는 여러 패턴을 확인하여 전체 텍스트를 검색하는 데 유용합니다. 이를 통해 엔진은 찾은 텍스트에 부분 문자열을 포함하지 않고 부분 문자열이 일치 항목의 끝에 존재하는지 확인할 수도 있습니다. 다음 예제에서는 긍정 lookahead를 사용하여 문장 부호 기호가 뒤에 오지 않는 문장에 있는 단어를 추출합니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead1.cs#2)]
     [!code-vb[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead1.vb#2)]  
  
     `\b[A-Z]+\b(?=\P{P})` 정규식은 다음 테이블과 같이 정의됩니다.  
  
    |무늬|설명|  
    |-------------|-----------------|  
    |`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
    |`[A-Z]+`|알파벳 임의의 문자를 1회 이상 찾습니다. <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드가 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션으로 호출되므로 이 비교는 대/소문자를 구분하지 않습니다.|  
    |`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
    |`(?=\P{P})`|다음 문자가 문장 부호 기호인지 확인하기 위해 앞을 살펴봅니다. 그렇지 않은 경우 일치가 성공합니다.|  
  
     긍정 lookahead 어설션에 대한 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
- 부정 lookahead: `(?!`*subexpression*`)`. 이 기능은 하위 식이 일치에 실패하는 경우 식을 찾는 기능을 추가합니다. 이 기능은 정리 작업에 특히 유용합니다. 포함해야 하는 사례에 대한 식보다 제거해야 하는 경우에 대한 식을 제공하는 것이 더 간단하기 때문입니다. 예를 들어 "non"으로 시작하지 않는 단어에 대한 식을 작성하기가 어렵습니다. 다음 예제에서는 부정 lookahead를 사용하여 파일을 제외합니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead2.cs#3)]
     [!code-vb[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead2.vb#3)]  
  
     정규식 패턴 `\b(?!non)\w+\b` 는 다음 테이블과 같이 정의됩니다.  
  
    |무늬|설명|  
    |-------------|-----------------|  
    |`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
    |`(?!non)`|현재 문자열이 "non"으로 시작하지 않으면 조회합니다. 그렇지 않으면 검색이 실패합니다.|  
    |`(\w+)`|하나 이상의 단어 문자를 찾습니다.|  
    |`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
     부정 lookahead 어설션에 대한 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
- 조건부 평가: `(?(`*expression*`)`*yes*`|`*no*`)` 및 `(?(`*name*`)`*yes*`|`*no*`)`. 여기서 *expression*은 일치시킬 하위 식이고, *name*은 캡처 그룹의 이름이고, *yes*는 *expression*이 일치하거나 *name*이 올바른 비어 있지 않은 캡처된 그룹인 경우 일치시킬 문자열이고, *no*는 *expression*이 일치하지 않거나 *name*이 유효하고 비어 있지 않은 캡처된 그룹이 아닌 경우 일치시킬 하위 식입니다. 엔진은 이 기능을 통해 이전 하위 식이 일치 결과 및 너비 0인 어설션 결과에 따라 둘 이상의 대체 패턴을 사용하여 검색할 수 있습니다. 따라서 이전 하위 식이 일치하는지 여부에 따라 하위 식을 찾도록 허용하는 더 강력한 형식의 역참조가 가능합니다. 다음 예제의 정규식은 공용으로 사용하고 내부적으로 사용하려는 단락을 모두 찾습니다. 내부적으로 사용하려는 단락은 `<PRIVATE>` 태그로 시작합니다. 정규식 패턴 `^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$`은 조건부 평가를 사용하여 공용으로 사용하고 내부적으로 사용하려는 단락의 콘텐츠를 별도의 캡처링 그룹에 할당합니다. 이러한 단락은 다르게 처리될 수 있습니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/conditional1.cs#4)]
     [!code-vb[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/conditional1.vb#4)]  
  
     이 정규식 패턴은 다음 테이블과 같이 정의됩니다.  
  
    |무늬|설명|  
    |-------------|-----------------|  
    |`^`|줄의 시작 부분에서 일치 항목 찾기를 시작합니다.|  
    |`(?<Pvt>\<PRIVATE\>\s)?`|0개 또는 1개의 뒤에 공백 문자가 있는 `<PRIVATE>` 문자열을 찾습니다. `Pvt`로 명명된 캡처 그룹에 일치 항목을 할당합니다.|  
    |`(?(Pvt)((\w+\p{P}?\s)+)`|`Pvt` 캡처링 그룹이 있는 경우 뒤에 0개 이상의 문장 구분 기호와 하나의 공백 문자가 오는 하나 이상의 단어 문자를 한 번 이상 찾습니다. 첫 번째 캡처링 그룹에 부분 문자열을 할당합니다.|  
    |<code>&#124;((\w+\p{P}?\s)+))</code>|`Pvt` 캡처링 그룹이 없는 경우 뒤에 0개 이상의 문장 구분 기호와 하나의 공백 문자가 오는 하나 이상의 단어 문자를 한 번 이상 찾습니다. 세 번째 캡처링 그룹에 부분 문자열을 할당합니다.|  
    |`\r?$`|줄의 끝 또는 문자열의 끝을 찾습니다.|  
  
     조건부 평가에 대한 자세한 내용은 [교체 구문](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)을 참조하세요.  
  
- 균형 조정 그룹 정의: `(?<`*name1*`-`*name2*`>` *subexpression*`)`. 정규식 엔진은 이 기능을 통해 괄호 또는 열고 닫는 대괄호와 같은 중첩된 구문을 추적할 수 있습니다. 예제는 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
- 역추적하지 않는 하위 식(최대 일치 하위 식): `(?>`*subexpression*`)`. 식이 보유한 독립 항목을 실행하는 것처럼 역추적 엔진은 이 기능을 통해 하위 식이 보유한 첫 번째 일치 항목만을 찾는다고 보장할 수 있습니다. 이 생성자를 사용하지 않는 경우 더 큰 식의 역추적 검색은 하위 식의 동작을 변경할 수 있습니다. 예를 들어 정규식 `(a+)\w`이 "a" 문자의 시퀀스를 따르는 단어 문자와 함께 하나 이상의 "a" 문자를 찾고 "a" 문자의 시퀀스를 첫 번째 캡처 그룹에 할당합니다. 하지만 입력 문자열의 마지막 문자가 "a"인 경우 `\w` 언어 요소에 의해 찾게 되며 캡처된 그룹에 포함되지 않습니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking2.vb#7)]  
  
     정규식 `((?>a+))\w`은 이러한 동작을 방지합니다. 연속되는 모든 "a" 문자를 역추적하지 않고 찾기 때문에 첫 번째 캡처링 그룹에는 연속되는 모든 "a" 문자가 있습니다. "a" 문자의 뒤에 "a" 이외의 문자가 적어도 하나 이상 있지 않으면 검색에 실패합니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking1.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking1.vb#8)]  
  
     역추적하지 않는 하위 식에 대한 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
- 오른쪽에서 왼쪽 찾기는 <xref:System.Text.RegularExpressions.RegexOptions.RightToLeft?displayProperty=nameWithType> 옵션을 <xref:System.Text.RegularExpressions.Regex> 클래스 생성자 또는 고정 인스턴스 일치 메서드에 제공하여 지정됩니다. 이 기능은 왼쪽에서 오른쪽이 아닌 오른쪽에서 왼쪽으로 찾는 경우에 유용하고 패턴의 왼쪽이 아닌 패턴의 오른쪽 부분에서 찾기를 시작하는 경우 효율적입니다. 다음 예제와 같이 오른쪽에서 왼쪽 찾기를 사용하면 탐욕적 수량자의 동작을 변경할 수 있습니다. 예제에서는 숫자로 끝나는 문장에 대해 두 개의 검색을 수행합니다. 오른쪽에서 왼쪽 검색이 6자리 모두와 일치하는 반면 탐욕적 수량자를 사용하는 왼쪽에서 오른쪽 검색 `+`은 문장에서 6자리 중 하나와 일치합니다. 정규식 패턴에 대한 설명은 이 섹션 앞부분의 게으른 수량자를 보여 주는 예제를 참조하세요.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/rtl1.cs#6)]
     [!code-vb[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/rtl1.vb#6)]  
  
     오른쪽에서 왼쪽 찾기에 대한 자세한 내용은 [정규식 옵션](../../../docs/standard/base-types/regular-expression-options.md)을 참조하세요.  
  
- 긍정 및 부정 lookbehind: 긍정 lookbehind의 경우 `(?<=`*subexpression*`)`, 부정 lookbehind의 경우 `(?<!`*subexpression*`)`. 이 기능은 이 항목의 앞부분에서 설명한 lookahead와 비슷합니다. 정규식 엔진을 사용하면 오른쪽에서 왼쪽 찾기를 완료할 수 있기 때문에 정규식은 무제한 lookbehind를 허용합니다. 긍정 및 부정 lookbehind는 중첩된 하위 식이 외부 식의 상위 집합인 경우 중첩된 수량자를 방지하는 데도 사용될 수 있습니다. 이러한 중첩된 수량자가 있는 정규식은 종종 성능이 저하됩니다. 예를 들어 다음 예제에서는 문자열이 영숫자 문자로 시작하고 끝나고 문자열의 다른 문자가 큰 하위 집합 중 하나임을 확인합니다. 이 식은 이메일 주소의 유효성을 검사하는 데 사용되는 정규식의 일부를 형성합니다. 자세한 내용은 [방법: 문자열이 올바른 이메일 형식인지 확인](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md)을 참조하세요.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookbehind1.cs#5)]
     [!code-vb[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookbehind1.vb#5)]  
  
     ``^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$`` 정규식은 다음 테이블과 같이 정의됩니다.  
  
    |무늬|설명|  
    |-------------|-----------------|  
    |`^`|문자열의 시작 부분에서 검색을 시작합니다.|  
    |`[A-Z0-9]`|숫자 또는 영숫자 문자를 찾습니다. 비교는 대소문자를 구분하지 않습니다.|  
    |<code>([-!#$%&'.*+/=?^\`{}&#124;~\w])\*</code>|단어 문자 또는 -, !, #, $, %, &, ', ., \*, +, /, =, ?, ^, \`, {, }, &#124;이나 ~의 문자로 구성된 0개 이상의 일치 항목을 찾습니다.|  
    |`(?<=[A-Z0-9])`|영숫자만 또는 숫자여야 하는 이전 문자를 확인합니다. 비교는 대소문자를 구분하지 않습니다.|  
    |`$`|문자열의 끝 부분에서 일치 항목 찾기를 끝냅니다.|  
  
     긍정 및 부정 lookbehind에 대한 자세한 내용은 [그룹화 구문](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[역추적](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)|대체 일치 항목을 찾는 정규식 역추적 분기에 대한 정보를 제공합니다.|  
|[컴파일 및 다시 사용](../../../docs/standard/base-types/compilation-and-reuse-in-regular-expressions.md)|성능 향상을 위해 정규식을 컴파일하고 다시 사용하는 방법에 대한 정보를 제공합니다.|  
|[스레드로부터의 안전성](../../../docs/standard/base-types/thread-safety-in-regular-expressions.md)|정규식 스레드로부터의 안전성에 대한 정보를 제공하고 정규식 개체에 대한 액세스를 동기화해야 하는 경우를 설명합니다.|  
|[.NET Framework 정규식](../../../docs/standard/base-types/regular-expressions.md)|정규식의 프로그래밍 언어 측면에 대한 개요를 제공합니다.|  
|[정규식 개체 모델](../../../docs/standard/base-types/the-regular-expression-object-model.md)|정규식 클래스를 사용하는 방법을 보여 주는 코드 예제 및 정보를 제공합니다.|  
|[정규식 예제](../../../docs/standard/base-types/regular-expression-examples.md)|일반적인 애플리케이션에서 정규식 사용을 보여 주는 코드 예제를 포함합니다.|  
|[정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)|정규식을 정의하는 데 사용할 수 있는 문자, 연산자 및 생성자 집합에 대한 정보를 제공합니다.|  
  
## <a name="reference"></a>참조  
 <xref:System.Text.RegularExpressions?displayProperty=nameWithType>
