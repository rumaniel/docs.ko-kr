---
title: .NET 정규식의 앵커
description: 정규식 패턴에서 앵커를 사용하는 방법을 알아봅니다.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- atomic zero-width assertions
- regular expressions, anchors
- regular expressions, atomic zero-width assertions
- anchors, in regular expressions
- metacharacters, atomic zero-width assertions
- metacharacters, anchors
- .NET Framework regular expressions, anchors
- .NET Framework regular expressions, atomic zero-width assertions
ms.assetid: 336391f6-2614-499b-8b1b-07a6837108a7
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 5f722977928604e5876e52a7329eef5c933bf2a7
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046465"
---
# <a name="anchors-in-regular-expressions"></a>정규식의 앵커
<a name="top"></a> 앵커 또는 원자성 너비가 0인 어설션은 문자열에서 일치 항목이 나타나야 하는 위치를 지정합니다. 검색 식에서 앵커를 사용하면 정규식 엔진은 문자열을 통과하거나 문자를 사용하지 않고, 지정된 위치에서만 일치 항목을 검색합니다. 예를 들어 `^` 기호는 줄이나 문자열의 시작 부분에서 일치 항목 찾기를 시작하도록 지정합니다. 따라서 정규식 `^http:` 은 줄의 시작 부분에 나타날 때만 "http:"을 찾습니다. 다음 표에서는 .NET의 정규식에서 지원하는 앵커를 보여 줍니다.  
  
|앵커|설명|  
|------------|-----------------|  
|`^`|기본적으로 일치 항목은 문자열의 시작 부분에서 발생해야 합니다. 다중 선에서는 줄의 시작 부분에서 발생해야 합니다. 자세한 내용은 [문자열 또는 줄의 시작](#Start)을 참조하세요.|  
|`$`|기본적으로 일치 항목은 문자열의 끝부분 또는 문자열의 끝부분 `\n` 앞에서 발생해야 합니다. 다중 선에서는 줄의 끝부분 또는 줄의 끝 `\n` 앞에서 발생해야 합니다. 자세한 내용은 [문자열 또는 줄의 끝](#End)을 참조하세요.|  
|`\A`|일치 항목이 문자열의 시작 부분에만 있어야 합니다(여러 줄 지원 없음). 자세한 내용은 [문자열의 시작만](#StartOnly)을 참조하세요.|  
|`\Z`|일치 항목이 문자열의 끝이나 문자열의 끝에 있는 `\n` 앞에 있어야 합니다. 자세한 내용은 [문자열의 끝 또는 줄 바꿈 종료 전](#EndOrNOnly)을 참조하세요.|  
|`\z`|일치 항목이 문자열의 끝 부분에만 있어야 합니다. 자세한 내용은 [문자열의 끝만](#EndOnly)을 참조하세요.|  
|`\G`|일치 항목이 이전 일치 항목이 종료된 위치에서 시작해야 합니다. 자세한 내용은 [연속 일치](#Contiguous)를 참조하세요.|  
|`\b`|일치 항목이 단어 경계에 있어야 합니다. 자세한 내용은 [단어 경계](#WordBoundary)를 참조하세요.|  
|`\B`|일치 항목이 단어 경계에 있으면 안 됩니다. 자세한 내용은 [비단어 경계](#NonwordBoundary)를 참조하세요.|  
  
<a name="Start"></a>   
## <a name="start-of-string-or-line-"></a>문자열 또는 줄의 시작: ^  
 기본적으로 `^` 앵커는 다음 패턴이 문자열의 첫 번째 문자 위치에서 시작하도록 지정합니다. `^` 기호를 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션과 함께 사용하는 경우([정규식 옵션](../../../docs/standard/base-types/regular-expression-options.md) 참조) 일치 항목이 각 줄의 시작 부분에 있어야 합니다.  
  
 다음 예제에서는 일부 전문 야구팀이 있던 기간(년)에 대한 정보를 추출하는 정규식에서 `^` 앵커를 사용합니다. 이 예제에서는 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드의 오버로드 두 개를 호출합니다.  
  
- <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29> 오버로드에 대한 호출은 입력 문자열에서 정규식 패턴과 일치하는 첫 번째 하위 문자열만 찾습니다.  
  
- <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29> 매개 변수를 `options` 으로 설정한 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 오버로드에 대한 호출은 모든 하위 문자열 5개를 찾습니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/startofstring1.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/startofstring1.vb#1)]  
  
 정규식 패턴 `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|입력 문자열의 시작 부분(또는 메서드가 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션과 함께 호출될 경우 줄의 시작 부분)에서 일치 항목 찾기를 시작합니다.|  
|`((\w+(\s?)){2,}`|단어 문자 하나 이상과 0 또는 공백 하나 순으로 두 번 이상 나타내는 일치 항목을 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다. 이 식은 두 번째 및 세 번째 캡처링 그룹도 정의합니다. 두 번째는 캡처된 단어로 구성되고 세 번째는 캡처된 공백으로 구성됩니다.|  
|`,\s`|쉼표, 공백 문자 순의 일치 항목을 찾습니다.|  
|`(\w+\s\w+)`|단어 문자 하나 이상, 공백, 단어 문자 하나 이상 순의 일치 항목을 찾습니다. 이 그룹은 네 번째 캡처링 그룹입니다.|  
|`,`|쉼표 하나를 찾습니다.|  
|`\s\d{4}`|공백, 10 진수 4개 순의 일치 항목을 찾습니다.|  
|<code>(-(\d{4}&#124;present))?</code>|하이픈과 10진수 4개 또는 문자열 "present" 순으로 나타나는 일치 항목 0개 또는 하나를 찾습니다. 이 그룹은 6번째 캡처 그룹입니다. 7번째 캡처 그룹도 포함됩니다.|  
|`,?`|쉼표 0개 또는 1개를 찾습니다.|  
|<code>(\s\d{4}(-(\d{4}&#124;present))?,?)+</code>|공백, 10진수 4개, 하이픈과 10진수 4개 또는 문자열 "present", 쉼표 0개 또는 하나 순으로 나타나는 일치 항목 하나 이상을 찾습니다. 이 그룹은 5번째 캡처 그룹입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="End"></a>   
## <a name="end-of-string-or-line-"></a>문자열 또는 줄의 끝: $  
 `$` 앵커는 선행 패턴이 입력 문자열의 끝이나 입력 문자열 끝에 있는 `\n` 앞에 나타나도록 지정합니다.  
  
 `$` 를 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션과 함께 사용하면 일치 항목이 줄의 끝 부분에 나타날 수도 있습니다. `$` 는 `\n` 과 일치하지만 `\r\n` (캐리지 리턴 및 줄 바꿈 문자 조합 또는 CR/LF)과는 일치하지 않습니다. CR/LF 문자 조합을 찾으려면 정규식 패턴에 `\r?$` 를 포함합니다.  
  
 다음 예제에서는 `$` 앵커를 [문자열 또는 줄의 시작](#Start) 섹션의 예제에서 사용된 정규식 패턴에 추가합니다. 텍스트 5줄을 포함하는 원래 입력 문자열에서 사용될 경우 <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29?displayProperty=nameWithType> 메서드는 일치 항목을 찾을 수 없습니다. 이는 첫 번째 줄의 끝 부분이 `$` 패턴과 일치하지 않기 때문입니다. 원래 입력 문자열을 문자열 배열로 분할하면 <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29?displayProperty=nameWithType> 메서드는 5줄의 각 줄을 찾는 데 성공합니다. <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 매개 변수를 `options` 으로 설정하여 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType>메서드를 호출하면 정규식 패턴에서 캐리지 리턴 요소(\u+000D)를 고려하지 않으므로 일치 항목이 발견되지 않습니다. 그러나 `$` 를 `\r?$`로 바꿔서 정규식 패턴을 수정할 경우 <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 매개 변수를 `options` 으로 설정하여 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 메서드를 다시 호출하면 일치 항목 5개가 발견됩니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring1.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring1.vb#2)]  
  
 [맨 위로 이동](#top)  
  
<a name="StartOnly"></a>   
## <a name="start-of-string-only-a"></a>문자열의 시작만: \A  
 `\A` 앵커는 일치 항목 찾기가 입력 문자열의 시작 부분에서 수행되도록 지정합니다. `^` 는 `\A` 옵션을 무시한다는 점을 제외하고 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 앵커와 동일합니다. 따라서 여러 줄 입력 문자열에서 첫 번째 줄의 시작 부분만 찾을 수 있습니다.  
  
 다음 예제는 `^` 및 `$` 앵커에 대한 예제와 비슷합니다. 일부 전문 야구팀이 있던 기간(년)에 대한 정보를 추출하는 정규식에서 `\A` 앵커를 사용합니다. 입력 문자열은 5줄을 포함합니다. <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=nameWithType> 메서드에 대한 호출은 입력 문자열에서 정규식 패턴과 일치하는 첫 번째 하위 문자열만 찾습니다. 예제에서 볼 수 있듯이 <xref:System.Text.RegularExpressions.RegexOptions.Multiline> 옵션은 아무 영향도 주지 않습니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/startofstring2.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/startofstring2.vb#3)]  
  
 [맨 위로 이동](#top)  
  
<a name="EndOrNOnly"></a>   
## <a name="end-of-string-or-before-ending-newline-z"></a>문자열의 끝 또는 줄 바꿈 종료 전: \Z  
 `\Z` 앵커는 일치 항목 찾기가 입력 문자열의 끝이나 입력 문자열의 끝에 있는 `\n` 앞에서 수행되도록 지정합니다. `$` 는 `\Z` 옵션을 무시한다는 점을 제외하고 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 앵커와 동일합니다. 따라서 여러 줄 문자열에서는 마지막 줄의 끝이나 `\n`앞의 마지막 줄만 찾을 수 있습니다.  
  
 `\Z` 는 `\n` 과 일치하지만 `\r\n` (CR/LF 문자 조합)과는 일치하지 않습니다. CR/LF를 찾으려면 정규식 패턴에 `\r?\Z` 를 포함합니다.  
  
 다음 예제에서는 일부 전문 야구팀이 있던 기간(년)에 대한 정보를 추출하는 `\Z` 문자열 또는 줄의 시작 [섹션의 예제와 비슷한 정규식에서](#Start) 앵커를 사용합니다. 정규식 `\r?\Z` 의 하위 식 `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z` 는 문자열 끝과 일치하고 `\n` 또는 `\r\n`으로 끝나는 문자열과도 일치합니다. 따라서 배열의 각 요소는 정규식 패턴과 일치합니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring2.cs#4)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring2.vb#4)]  
  
 [맨 위로 이동](#top)  
  
<a name="EndOnly"></a>   
## <a name="end-of-string-only-z"></a>문자열의 끝만: \z  
 `\z` 앵커는 일치 항목 찾기가 입력 문자열의 끝 부분에서 수행되도록 지정합니다. `$` 언어 요소와 같이 `\z` 는 <xref:System.Text.RegularExpressions.RegexOptions.Multiline?displayProperty=nameWithType> 옵션을 무시합니다. `\Z` 언어 요소와 달리 `\z` 는 문자열 끝에서 `\n` 문자를 찾지 않습니다. 따라서 입력 문자열의 마지막 줄만 찾을 수 있습니다.  
  
 다음 예제에서는 일부 전문 야구팀이 있던 기간(년)에 대한 정보를 추출하는 이전 섹션의 예제와 동일한 정규식에서 `\z` 앵커를 사용합니다. 예제에서는 정규식 패턴 `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z`를 사용하여 문자열 배열에서 요소 5개를 각각 찾으려고 합니다. 문자열 중 두 개는 캐리지 리턴 및 줄 바꿈 문자로 끝나고, 하나는 줄 바꿈 문자로 끝나고, 두 개는 캐리지 리턴과 줄 바꿈 문자가 둘 다 없이 끝납니다. 출력과 같이 캐리지 리턴이나 줄 바꿈 문자가 없는 문자열만 패턴과 일치합니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring3.cs#5)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring3.vb#5)]  
  
 [맨 위로 이동](#top)  
  
<a name="Contiguous"></a>   
## <a name="contiguous-matches-g"></a>연속 일치: \G  
 `\G` 앵커는 일치 항목 찾기가 이전 일치 항목 찾기가 끝난 지점에서 수행되도록 지정합니다. 이 앵커를 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 또는 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 메서드와 함께 사용하면 모든 일치 항목이 연속으로 나타납니다.  
  
 다음 예제에서는 정규식을 사용하여 쉼표로 구분된 문자열에서 설치류의 이름을 추출합니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/contiguous1.cs#6)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/contiguous1.vb#6)]  
  
 정규식 `\G(\w+\s?\w*),?` 는 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\G`|마지막 일치 항목 찾기가 종료된 위치에서 시작합니다.|  
|`\w+`|하나 이상의 단어 문자를 찾습니다.|  
|`\s?`|0개 또는 1개의 공백을 찾습니다.|  
|`\w*`|0개 이상의 단어 문자를 찾습니다.|  
|`(\w+\s?\w*)`|단어 문자 하나 이상, 공백 0개 이상, 단어 문자 0개 이상 순의 일치 항목을 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`,?`|리터럴 쉼표 문자 0개 또는 하나를 찾습니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="WordBoundary"></a>   
## <a name="word-boundary-b"></a>단어 경계: \b  
 `\b` 앵커는 일치 항목 찾기가 단어 문자( `\w` 언어 요소)와 비단어 문자( `\W` 언어 요소) 사이 경계에서 수행되도록 지정합니다. 단어 문자는 영숫자 문자 및 밑줄로 구성되고, 비단어 문자는 영숫자나 밑줄이 아닌 문자입니다. 자세한 내용은 [문자 클래스](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)를 참조하세요. 일치 항목은 문자열의 시작 또는 끝의 단어 경계에 있을 수도 있습니다.  
  
 `\b` 앵커는 하위 식이 단어의 시작이나 끝이 아닌 전체 단어와 일치하는지 확인하는 데 자주 사용됩니다. 다음 예제의 정규식 `\bare\w*\b` 는 이 사용법을 보여 줍니다. 하위 문자열 "are"로 시작하는 단어를 찾습니다. 예제 출력에서는 `\b` 가 입력 문자열의 시작 및 끝과 둘 다 일치함을 보여 줍니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/word1.cs#7)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/word1.vb#7)]  
  
 정규식 패턴은 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`are`|"are"를 찾습니다.|  
|`\w*`|0개 이상의 단어 문자를 찾습니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="NonwordBoundary"></a>   
## <a name="non-word-boundary-b"></a>비단어 경계: \B  
 `\B` 앵커는 일치 항목 찾기가 단어 경계에서 수행되지 않도록 지정합니다. `\b` 앵커와 반대 작업을 수행합니다.  
  
 다음 예제에서는 `\B` 앵커를 사용하여 단어에서 하위 문자열 "qu"를 찾습니다. 정규식 패턴 `\Bqu\w+` 는 단어를 시작하지 않고 단어의 끝으로 계속되는 "qu"로 시작하는 하위 문자열을 찾습니다.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/nonword1.cs#8)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/nonword1.vb#8)]  
  
 정규식 패턴은 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\B`|단어 경계에서 일치 항목 찾기를 시작하지 않습니다.|  
|`qu`|"qu" 하위 문자열을 찾습니다.|  
|`\w+`|하나 이상의 단어 문자를 찾습니다.|  
  
## <a name="see-also"></a>참고 항목

- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
- [정규식 옵션](../../../docs/standard/base-types/regular-expression-options.md)
