---
title: .NET 정규식의 교체 구문
description: 정규식에서 조건부 일치를 위해 교체 구문을 사용하는 방법을 알아봅니다.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- either/or matching
- alternative matching patterns
- regular expressions, alternation constructs
- alternation constructs
- optional matching patterns
- constructs, alternation
- .NET Framework regular expressions, alternation constructs
ms.assetid: 071e22e9-fbb0-4ecf-add1-8d2424f9f2d1
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: c6f33023d747ce20964c7cb83a66d6764b6030cd
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736610"
---
# <a name="alternation-constructs-in-regular-expressions"></a>정규식의 교체 구문

교체 구문은 either/or 또는 조건부 일치를 허용하도록 정규식을 수정합니다. .NET에서는 다음 세 가지 교체 구문을 지원합니다.

- [&#124;를 사용한 패턴 일치](#Either_Or)
- [(?(expression)yes&#124;no)를 사용한 조건부 일치](#Conditional_Expr)
- [유효한 캡처 그룹을 기준으로 조건부 일치](#Conditional_Group)

<a name="Either_Or"></a>
## <a name="pattern-matching-with-124"></a>&#124;를 사용한 패턴 일치

세로 막대(`|`) 문자를 사용하여 일련의 패턴 중 하나를 찾을 수 있습니다. 여기서 `|` 문자는 각 패턴을 구분합니다.

긍정 문자 클래스처럼 `|` 문자를 사용하여 여러 단일 문자의 하나를 찾을 수 있습니다. 다음 예제에서는 긍정 문자 클래스 및 either/or 패턴 일치를 둘다 `|` 문자와 함께 사용하여 문자열에서 단어 "gray" 또는 "grey" 항목을 찾습니다. 이 경우 `|` 문자는 더 자세한 정규식을 생성합니다.

[!code-csharp[RegularExpressions.Language.Alternation#1](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation1.cs#1)]
[!code-vb[RegularExpressions.Language.Alternation#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation1.vb#1)]

`|` 문자를 사용하는 정규식인 `\bgr(a|e)y\b`는 다음 테이블과 같이 해석됩니다.

|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계를 시작합니다.|  
|`gr`|문자 "gr"을 찾습니다.|  
|<code>(a&#124;e)</code>|"a" 또는 "e"를 찾습니다.|  
|`y\b`|단어 경계에서 "y"를 찾습니다.|  

`|` 문자를 사용하여 문자 리터럴과 정규식 언어 요소의 조합을 포함할 수 있는 여러 문자나 하위 식을 통해 either/or 일치 항목을 찾을 수도 있습니다. 문자 클래스는 이 기능을 제공하지 않습니다. 다음 예제에서는 `|` 문자를 사용하여 미국 SSN(사회 보장 번호)(*ddd*-*dd*-*dddd* 형식의 9자리 숫자) 또는 미국 EIN(고용주 식별 번호)(*dd*-*ddddddd* 형식의 9자리 숫자)을 추출합니다.

[!code-csharp[RegularExpressions.Language.Alternation#2](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation2.cs#2)]
[!code-vb[RegularExpressions.Language.Alternation#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation2.vb#2)]  

정규식 `\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b`는 다음 테이블과 같이 해석됩니다.
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계를 시작합니다.|  
|<code>(\d{2}-\d{7}&#124;\d{3}-\d{2}-\d{4})</code>|10진수 2개, 하이픈, 10진수 7개 순의 일치 항목이나 10진수 3개, 하이픈, 10진수 2개, 또 다른 하이픈, 10진수 4개 순의 일치 항목을 찾습니다.|  
|`\d`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
<a name="Conditional_Expr"></a>   
## <a name="conditional-matching-with-an-expression"></a>식을 사용한 조건부 일치

이 언어 요소는 초기 패턴을 찾을지 여부에 따라 두 패턴의 하나를 찾으려고 합니다. 사용되는 구문은 다음과 같습니다.  

`(?(` *expression* `)` *yes* `|` *no* `)`

여기서 *expression* 은 일치 항목을 찾을 초기 패턴이고, *yes* 는 *expression* 과 일치할 경우 일치 항목을 찾을 패턴이고, *no* 는 *expression* 이 일치하지 않을 경우 일치 항목을 찾을 선택적 패턴입니다. 정규식 엔진은 *expression* 을 너비가 0인 어설션으로 처리합니다. 즉, 정규식 엔진은 *expression*을 계산한 후 입력 스트림에서 앞으로 이동하지 않습니다. 따라서 이 구문은 다음 구문과 같습니다.

`(?(?=` *식* `)` *예* `|` *no* `)`

여기서 `(?=`*expression*`)`은 너비가 0인 어설션 구문입니다. 자세한 내용은 [그룹화 구문](grouping-constructs-in-regular-expressions.md)을 참조하세요. 정규식 엔진이 *expression*을 앵커(너비가 0인 어설션)로 해석하기 때문에 *expression*은 너비가 0인 어설션(자세한 내용은 [앵커](anchors-in-regular-expressions.md) 참조) 또는 *yes*에도 포함되는 하위 식이어야 합니다. 그러지 않으면, *yes* 패턴을 찾을 수 없습니다.  
  
> [!NOTE]
> *expression*이 이름이나 숫자가 지정된 캡처링 그룹인 경우 교체 구문은 캡처 테스트로 해석됩니다. 자세한 내용은 다음 섹션인 [유효한 캡처 그룹을 기준으로 조건부 일치](#Conditional_Group)를 참조하세요. 즉, 정규식 엔진은 캡처된 하위 문자열을 찾으려고 하지 않지만, 대신 그룹의 존재 여부를 테스트합니다.  
  
다음 예제는 [&#124;를 사용한 Either/Or 패턴 일치](#Either_Or) 섹션에 나타나는 예제의 변형입니다. 조건부 일치를 사용하여 단어 경계 뒤의 처음 문자 3개가 숫자 2개, 하이픈 순의 문자열인지를 확인합니다. 해당 문자열이면 미국 EIN(고용주 식별 번호)을 찾으려고 합니다. 그러지 않으면 미국 SSN(사회 보장 번호)을 찾으려고 합니다.

[!code-csharp[RegularExpressions.Language.Alternation#3](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation3.cs#3)]
[!code-vb[RegularExpressions.Language.Alternation#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation3.vb#3)]

정규식 패턴 `\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b`는 다음 테이블과 같이 해석됩니다.

|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계를 시작합니다.|  
|`(?(\d{2}-)`|다음 문자 3개가 숫자 2개, 하이픈 순으로 구성되는지를 확인합니다.|  
|`\d{2}-\d{7}`|이전 패턴이 일치하면 숫자 2개, 하이픈, 숫자 7개 순의 일치 항목을 찾습니다.|  
|`\d{3}-\d{2}-\d{4}`|이전 패턴이 일치하지 않으면 10진수 3개, 하이픈, 10진수 2개, 또 다른 하이픈, 10진수 4개 순의 일치 항목을 찾습니다.|  
|`\b`|단어 경계를 찾습니다.|  

<a name="Conditional_Group"></a>
## <a name="conditional-matching-based-on-a-valid-captured-group"></a>유효한 캡처 그룹을 기준으로 조건부 일치

이 언어 요소는 지정된 캡처링 그룹에 일치시켰는지 여부에 따라 두 패턴 중 하나에 일치시키려고 시도합니다. 사용되는 구문은 다음과 같습니다.

`(?(` *name* `)` *예* `|` *no* `)`

또는

`(?(` *number* `)` *예* `|` *no* `)`

여기서 *name* 은 이름이고, *number* 는 캡처 그룹 수이고, *yes* 는 *name* 또는 *number* 에 일치 항목이 있을 경우 일치 항목을 찾을 식이고, *no* 는 일치 항목이 없을 경우 일치 항목을 찾을 선택적 식입니다.

*name* 이 정규식 패턴에서 사용되는 캡처 그룹의 이름에 해당하지 않을 경우에는 교체 구문이 앞 섹션에서 설명한 대로 식 테스트로 해석됩니다. 일반적으로 이는 *expression* 이 `false`로 계산됨을 의미합니다. *number* 가 정규식 패턴에 사용되는 번호 매기기 캡처 그룹에 해당하지 않는 경우 정규식 엔진이 <xref:System.ArgumentException>을 throw합니다.

다음 예제는 [&#124;를 사용한 Either/Or 패턴 일치](#Either_Or) 섹션에 나타나는 예제의 변형입니다. 숫자 2개, 하이픈 순으로 구성된 `n2` 라는 캡처 그룹을 사용합니다. 교체 구문은 입력 문자열에서 이 캡처 그룹이 일치했는지를 테스트합니다. 일치한다면 교체 구문은 9자리 미국 EIN(고용주 식별 번호)을 찾으려고 합니다. 일치하지 않는다면 9자리 미국 SSN(사회 보장 번호)을 찾으려고 합니다.

[!code-csharp[RegularExpressions.Language.Alternation#4](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation4.cs#4)]
[!code-vb[RegularExpressions.Language.Alternation#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation4.vb#4)]

정규식 패턴 `\b(?<n2>\d{2}-)?(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b`는 다음 테이블과 같이 해석됩니다.

|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계를 시작합니다.|  
|`(?<n2>\d{2}-)?`|숫자 2개, 하이픈 순의 일치 항목 0개 또는 1개를 찾습니다. 이 캡처링 그룹의 이름을 `n2`로 지정합니다.|  
|`(?(n2)`|`n2` 가 입력 문자열에서 일치하는지 여부를 테스트합니다.|  
|`\d{7}`|`n2` 가 일치하는 경우 일곱 개의 10진수를 일치시킵니다.|  
|<code>&#124;\d{3}-\d{2}-\d{4}</code>|`n2` 가 일치하지 않는 경우 세 10진수, 하이픈, 두 10진수, 다른 하이픈 및 네 10진수를 일치시킵니다.|  
|`\b`|단어 경계를 찾습니다.|  

다음 예제에서는 명명된 그룹 대신 번호가 있는 그룹을 사용하는 이 예제의 변형을 보여 줍니다. 정규식 패턴은 `\b(\d{2}-)?(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b`입니다.

[!code-csharp[RegularExpressions.Language.Alternation#5](~/samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.alternation/cs/alternation5.cs#5)]
[!code-vb[RegularExpressions.Language.Alternation#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.alternation/vb/alternation5.vb#5)]

## <a name="see-also"></a>참고 항목

- [정규식 언어 - 빠른 참조](regular-expression-language-quick-reference.md)
