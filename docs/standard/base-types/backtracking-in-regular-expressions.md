---
title: .NET 정규식의 역행 검사
description: 정규식 패턴 일치에서 역추적을 제어하는 방법을 알아봅니다.
ms.date: 11/12/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework regular expressions, backtracking
- alternative matching patterns
- optional matching patterns
- searching with regular expressions, backtracking
- pattern-matching with regular expressions, backtracking
- backtracking
- regular expressions [.NET Framework], backtracking
- strings [.NET Framework], regular expressions
- parsing text with regular expressions, backtracking
ms.assetid: 34df1152-0b22-4a1c-a76c-3c28c47b70d8
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 0831a22b0c1d3333cc37f86a764006c934597390
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968556"
---
# <a name="backtracking-in-regular-expressions"></a>정규식의 역행 검사
<a name="top"></a> 역추적은 정규식 패턴에 선택적인 [수량자](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md) 또는 [교체 구문](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)이 포함되어 있고 정규식 엔진이 일치 항목을 계속 검색하기 위해 이전에 저장된 상태로 되돌아갈 때 발생합니다. 역추적은 정규식 성능의 핵심입니다. 역추적을 사용하면 식의 성능과 유연성을 높일 수 있으며 매우 복잡한 패턴도 검색할 수 있습니다. 하지만 이러한 장점에는 단점이 수반됩니다. 역추적은 종종 정규식 엔진의 성능에 영향을 주는 가장 중요한 단일 요소입니다. 다행히도 개발자는 정규식 엔진의 동작과 역추적 사용 방식을 제어할 수 있습니다. 이 항목에서는 역추적의 작동 방식 및 역추적을 제어할 수 있는 방법에 대해 설명합니다.  
  
> [!NOTE]
> 일반적으로 .NET 정규식 엔진과 같은 NFA(Nondeterministic Finite Automaton) 엔진에서는 개발자가 효율적이고 속도가 빠른 정규식을 작성하도록 노력해야 합니다.  
  
 이 항목에는 다음과 같은 단원이 포함되어 있습니다.  
  
- [역추적을 사용하지 않는 선형 비교](#linear_comparison_without_backtracking)  
  
- [선택적인 수량자 또는 교체 구문을 사용한 역추적](#backtracking_with_optional_quantifiers_or_alternation_constructs)  
  
- [선택적인 중첩된 수량자를 사용한 역추적](#backtracking_with_nested_optional_quantifiers)  
  
- [역추적 제어](#controlling_backtracking)  
  
<a name="linear_comparison_without_backtracking"></a>   
## <a name="linear-comparison-without-backtracking"></a>역추적을 사용하지 않는 선형 비교  
 정규식 패턴에 선택적인 수량자 또는 교체 구문이 없으면 정규식 엔진이 선형 시간으로 실행됩니다. 즉, 정규식 엔진은 패턴에서 입력 문자열의 텍스트와 일치하는 첫 번째 언어 요소를 검색한 후 다시 패턴에서 입력 문자열의 다음 문자 또는 문자 그룹과 일치하는 다음 언어 요소를 찾습니다. 이 작업은 검색이 성공할 때까지 계속되고, 그렇지 않으면 검색이 실패합니다. 어느 경우에든 정규식 엔진은 입력 문자열에서 한 번에 한 글자씩 검색을 진행합니다.  
  
 다음 예제에서 이에 대해 설명합니다. 정규식 `e{2}\w\b` 는 모든 단어 문자에서 단어 경계까지 "e"가 두 번 나오는 단어를 검색합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking1.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking1.vb#1)]  
  
 이 정규식은 수량자 `{2}`가 있더라도 선형 방식으로 평가됩니다. `{2}` 는 선택적인 수량자가 아니기 때문에 정규식 엔진이 역추적을 수행하지 않습니다. 이 수량자는 정확한 숫자를 지정하며 이전 하위 식이 검색해야 하는 가변 횟수가 아닙니다. 따라서 정규식 엔진은 다음 표에서와 같이 입력 문자열에서 정규식 패턴과 일치하는 항목을 검색하려고 시도합니다.  
  
|작업|패턴 내 위치|문자열 내 위치|결과|  
|---------------|-------------------------|------------------------|------------|  
|1|e|"needing a reed"(인덱스 0)|일치하는 항목이 없습니다.|  
|2|e|"eeding a reed"(인덱스 1)|일치 가능|  
|3|e{2}|"eding a reed"(인덱스 2)|일치 가능|  
|4|\w|"ding a reed"(인덱스 3)|일치 가능|  
|5|\b|"ing a reed"(인덱스 4)|일치 가능 실패|  
|6|e|"eding a reed"(인덱스 2)|일치 가능|  
|7|e{2}|"ding a reed"(인덱스 3)|일치 가능 실패|  
|8|e|"ding a reed"(인덱스 3)|검색이 실패합니다.|  
|9|e|"ing a reed"(인덱스 4)|일치하는 항목이 없습니다.|  
|10|e|"ng a reed"(인덱스 5)|일치하는 항목이 없습니다.|  
|11|e|"g a reed"(인덱스 6)|일치하는 항목이 없습니다.|  
|12|e|" a reed"(인덱스 7)|일치하는 항목이 없습니다.|  
|13|e|"a reed"(인덱스 8)|일치하는 항목이 없습니다.|  
|14|e|" reed"(인덱스 9)|일치하는 항목이 없습니다.|  
|15|e|"reed"(인덱스 10)|일치 없음|  
|16|e|"eed"(인덱스 11)|일치 가능|  
|17|e{2}|"ed"(인덱스 12)|일치 가능|  
|18|\w|"d"(인덱스 13)|일치 가능|  
|19|\b|""(인덱스 14)|일치|  
  
 정규식 엔진에 선택적인 수량자가 없거나 교체 구문이 없는 경우 입력 문자열에서 정규식 패턴과 일치하는 항목을 찾기 위해 필요한 최대 비교 수는 입력 문자열에 있는 문자 수와 거의 동일합니다. 이 경우 정규식 엔진은 이 13자 길이의 문자열에서 가능한 일치 항목을 식별하기 위해 19가지를 비교합니다.  즉, 선택적인 수량자 또는 대체 생성 구문이 없는 경우 정규식 엔진이 선형에 가까운 시간으로 실행됩니다.  
  
 [맨 위로 이동](#top)  
  
<a name="backtracking_with_optional_quantifiers_or_alternation_constructs"></a>   
## <a name="backtracking-with-optional-quantifiers-or-alternation-constructs"></a>선택적인 수량자 또는 교체 구문을 사용한 역추적  
 정규식에 선택적인 수량자 또는 교체 구문이 포함된 경우 입력 문자열에 대한 평가는 더 이상 선형으로 수행되지 않습니다. NFA 엔진에서 패턴 일치는 입력 문자열에 있는 검색할 문자가 아니라 정규식의 언어 요소에 의해 영향을 받습니다. 따라서 정규식 엔진은 선택적인 하위 식 또는 교체 하위 식에 대해 전체 검색을 수행합니다. 하위 식의 다음 언어 요소로 진행할 때 검색이 실패하면 정규식 엔진이 성공한 일치 부분을 버리고 입력 문자열 전체에 대한 정규식 검색을 수행하기 위해 이전에 저장된 상태로 돌아갈 수 있습니다. 일치하는 항목을 찾기 위해 이전에 저장된 상태로 돌아가는 프로세스를 역추적이라고 부릅니다.  
  
 예를 들어 임의의 문자로 시작해서 "es"가 포함된 항목을 검색하는 `.*(es)`라는 정규식 패턴이 있다고 가정해보십시오. 다음 예제에서와 같이 입력 문자열이 "Essential services are provided by regular expressions."인 경우 이 패턴은 "expressions"의 "es"를 포함하여 전체 문자열을 끝까지 검색합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking2.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking2.vb#2)]  
  
 이를 위해 정규식 엔진은 다음과 같은 방식으로 역추적을 사용합니다.  
  
- 전체 입력 문자열에서 `.*` (0개 이상의 임의 문자 검색)를 검색합니다.  
  
- 정규식 패턴의 "e"와 일치하는 항목을 찾습니다. 하지만 입력 문자열에는 검색에 사용할 수 있는 남은 문자가 없습니다.  
  
- 마지막으로 일치한 항목인 "Essential services are provided by regular expressions"로 역추적하고 문장의 끝에 있는 마침표에서 "e"와 일치하는 항목을 찾습니다. 그러면 검색이 실패합니다.  
  
- 계속해서 일시적으로 일치하는 하위 문자열이 "Essential services are provided by regular expr"이 될 때까지 한 번에 한 글자씩 이전에 성공한 일치 항목으로 역추적합니다. 그런 다음 패턴에 있는 "e"와 "expressions"의 두 번째 "e"를 비교하여 일치하는 항목을 찾습니다.  
  
- 패턴에 있는 "s"와 일치한 "e" 문자 다음의 "s"("expressions"의 첫 번째 "s")를 비교합니다. 그러면 검색이 성공합니다.  
  
 역추적을 사용할 경우 길이가 55자인 입력 문자열에서 정규식 패턴과 일치하는 항목을 검색하려면 67번의 비교 작업이 필요합니다. 일반적으로 정규식 엔진에 단일 교체 구문이 포함되었거나 선택적인 단일 수량자가 포함된 경우 패턴을 검색하는 데 필요한 비교 작업 수는 입력 문자열에 있는 문자 수의 두 배 이상입니다.  
  
 [맨 위로 이동](#top)  
  
<a name="backtracking_with_nested_optional_quantifiers"></a>   
## <a name="backtracking-with-nested-optional-quantifiers"></a>선택적인 중첩된 수량자를 사용한 역추적  
 패턴에 교체 구문이 많이 포함되었거나 중첩된 교체 구문이 포함되었거나, 선택적인 중첩된 수량자가 포함된 경우(가장 일반적인 경우) 정규식 패턴과 일치하는 항목을 찾기 위해 필요한 비교 작업 수가 기하급수적으로 증가할 수 있습니다. 예를 들어 정규식 패턴 `^(a+)+$` 는 하나 이상의 "a" 문자가 포함된 전체 문자열을 검색하도록 디자인되었습니다. 예제에는 동일한 길이의 두 입력 문자열이 제공되지만 첫 번째 문자열만 패턴과 일치합니다. <xref:System.Diagnostics.Stopwatch?displayProperty=nameWithType> 클래스는 일치 항목을 검색하는 작업이 수행되는 시간을 확인하는 데 사용됩니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking3.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking3.vb#3)]  
  
 예제의 결과에서와 같이 정규식 엔진은 일치하는 문자열을 식별할 때 걸리는 시간에 비해 입력 문자열이 패턴과 일치하지 않는 것을 확인하는 데 약 두 배의 시간이 걸립니다. 그 이유는 성공하지 못한 검색은 항상 최악의 경우를 나타내기 때문입니다. 정규식 엔진은 일치하는 항목이 없다는 결론을 내리기까지 정규식을 사용하여 데이터에서 가능한 모든 경로를 따라야 하며, 중첩된 괄호가 있으면 데이터에서 발생 가능한 경로 수가 추가로 늘어납니다. 정규식 엔진은 다음을 수행하여 두 번째 문자열이 패턴과 일치하지 않는다는 결론을 내립니다.  
  
- 문자열의 시작 위치에 있는지 확인한 후 `a+`패턴을 사용하여 문자열에서 처음 5개 문자를 검색합니다. 그런 후 문자열에 "a" 문자의 추가 그룹이 없는지 확인합니다. 마지막으로 문자열의 끝인지 테스트합니다. 문자열에 하나의 추가 문자가 남아 있기 때문에 검색이 실패합니다. 이 실패한 검색에는 9번의 비교 작업이 필요합니다. 정규식 엔진은 또한 "a"(이하 매치 1이라고 부름), "aa"(매치 2), "aaa"(매치 3) 및 "aaaa"(매치 4)의 일치 항목에 대한 상태 정보를 저장합니다.  
  
- 정규식 엔진이 이전에 저장된 매치 4로 돌아갑니다. 추가 캡처 그룹에 할당할 수 있도록 "a" 문자가 추가로 하나 더 있는지 확인합니다. 마지막으로 문자열의 끝인지 테스트합니다. 문자열에 하나의 추가 문자가 남아 있기 때문에 검색이 실패합니다. 이 실패한 검색에는 4번의 비교 작업이 필요합니다. 지금까지 총 13번의 비교 작업이 수행되었습니다.  
  
- 정규식 엔진이 이전에 저장된 매치 3으로 돌아갑니다. 추가 캡처 그룹에 할당할 수 있도록 두 개의 추가 "a" 문자가 있는지 확인합니다. 하지만 문자열 끝 테스트가 실패합니다. 그런 다음 매치 3으로 돌아가서 두 개의 추가 캡처 그룹에서 두 개의 추가 "a" 문자를 검색하려고 시도합니다. 그래도 문자열 끝 테스트가 실패합니다. 이렇게 실패한 검색 작업에는 12번의 비교 작업이 필요합니다. 지금까지 총 25번의 비교 작업이 수행되었습니다.  
  
 입력 문자열을 정규식 엔진에서 비교하는 작업은 정규식이 검색 작업의 모든 가능한 조합을 시도하고 일치 항목이 없다는 결론을 내릴 때까지 이러한 방식으로 계속해서 수행됩니다. 중첩된 수량자로 인해 이러한 비교는 O(2<sup>n</sup>) 또는 지수 연산으로 수행되며, 여기서 *n*은 입력 문자열에 있는 문자 수입니다. 즉, 문자 수가 30개인 입력 문자열에서는 최악의 경우 약 1,073,741,824번의 비교 작업이 필요하고, 입력 문자열의 문자 수가 40개이면 약 1,099,511,627,776번의 비교 작업이 필요합니다. 이정도 또는 심지어 더 긴 문자열을 사용하면 정규식 메서드가 정규식 패턴과 일치하지 않는 입력을 처리할 때 완료 시간이 극단적으로 길어질 수 있습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="controlling_backtracking"></a>   
## <a name="controlling-backtracking"></a>역추적 제어  
 역추적을 사용하면 강력하고 유연한 정규식을 만들 수 있습니다. 하지만 이전 단원에 설명한 것처럼 이러한 장점 외에도 성능이 매우 크게 저하될 수 있음에 유의해야 합니다. 과도한 역추적을 방지하려면 <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화하거나 정적 정규식 일치 메서드를 호출할 때 시간 제한 간격을 정의해야 합니다. 이에 대해서는 다음 섹션에서 설명합니다. 그 밖에도, .NET에서는 역추적을 제한하거나 억제하고, 성능 상의 제약이 거의 없거나 전혀 없이 복잡한 정규식을 지원하는 세 가지 정규식 언어 요소인 [역추적하지 않는 하위 식](#Nonbacktracking), [lookbehind 어설션](#Lookbehind) 및 [lookahead 어설션](#Lookahead)을 지원합니다. 각 언어 요소에 대한 자세한 내용은 [Grouping Constructs](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
<a name="Timeout"></a>   
### <a name="defining-a-time-out-interval"></a>시간 제한 간격 정의  
 .NET Framework 4.5부터는 정규식 엔진이 시도를 포기하고 <xref:System.Text.RegularExpressions.RegexMatchTimeoutException> 예외를 throw하기 전에 단일 일치 항목을 검색할 가장 긴 간격을 나타내는 시간 제한 값을 설정할 수 있습니다. <xref:System.TimeSpan> 값을 인스턴스 정규식을 위한 <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=nameWithType> 생성자에 제공하여 시간 제한 간격을 지정합니다. 또한, 각각의 정적 패턴 일치 메서드에 시간 제한 값을 지정할 수 있게 해주는 <xref:System.TimeSpan> 매개 변수의 오버로드가 있습니다. 기본적으로, 시간 제한 간격은 <xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout?displayProperty=nameWithType> 으로 설정되고, 정규식 엔진의 시간이 초과되지 않습니다.  
  
> [!IMPORTANT]
> 정규식이 역추적에 의존하는 경우에는 항상 시간 제한 간격을 설정하는 것이 좋습니다.  
  
 <xref:System.Text.RegularExpressions.RegexMatchTimeoutException> 예외는 정규식 엔진이 지정된 시간 제한 간격 내에 일치 항목을 찾지 못했음을 나타내지만, 예외가 throw된 이유를 나타내지는 않습니다. 과도한 역추적이 원인일 수 있지만, 예외가 throw된 시점의 시스템 부하에서 시간 제한 간격이 너무 낮게 설정되었을 가능성도 있습니다. 예외를 처리할 때 입력 문자열을 포함한 다른 일치 항목을 버리거나 시간 제한 간격을 늘리고 일치 검사 작업을 재시도하는 방법 중에서 선택할 수 있습니다.  
  
 예를 들어, 다음 코드는 <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=nameWithType> 생성자를 호출하여 1초의 시간 제한 값으로 <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화합니다. 줄의 끝에 하나 이상의 "a" 문자가 포함된 하나 이상의 시퀀스와 일치하는 정규식 패턴 `(a+)+$`는 과도한 역추적의 대상이 됩니다. <xref:System.Text.RegularExpressions.RegexMatchTimeoutException> 이 throw되는 경우, 이 예제에서는 시간 제한 값을 최대 간격인 3초까지 늘립니다. 그 후에는 패턴 일치를 찾는 시도를 취소합니다.  
  
 [!code-csharp[System.Text.RegularExpressions.Regex.ctor#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.text.regularexpressions.regex.ctor/cs/ctor1.cs#1)]
 [!code-vb[System.Text.RegularExpressions.Regex.ctor#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.text.regularexpressions.regex.ctor/vb/ctor1.vb#1)]  
  
<a name="Nonbacktracking"></a>   
### <a name="nonbacktracking-subexpression"></a>역추적하지 않는 하위 식  
 `(?>` *subexpression*`)` 언어 요소는 하위 식에서 역추적을 억제합니다. 실패한 검색과 연관된 성능 문제를 방지하는 데 유용합니다.  
  
 다음 예제에서는 역추적을 억제하여 중첩된 수량자를 사용할 때 성능을 향상시키는 방법을 보여 줍니다. 이 예에서는 정규식 엔진이 입력 문자열이 두 개의 정규식과 일치하지 않는지 확인하기 위해 필요한 시간을 측정합니다. 첫 번째 정규식에서는 역추적을 사용하여 하나 이상의 16진수 숫자와 일치하는 하나 이상의 항목이 포함되고 콜론과 하나 이상의 16진수 숫자 그리고 두 개의 콜론이 이어지는 문자열을 검색하려고 시도합니다. 두 번째 정규식은 첫 번째와 동일하지만 역추적이 사용되지 않습니다. 예의 결과에서 보여 지듯이 역추적을 사용하지 않음으로써 얻게 되는 성능 향상 효과가 매우 큽니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking4.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking4.vb#4)]  
  
<a name="Lookbehind"></a>   
### <a name="lookbehind-assertions"></a>lookbehind 어설션  
 .NET에는 입력 문자열에서 이전 문자와 일치하는 두 가지 언어 요소인 `(?<=`*subexpression*`)` 및 `(?<!`*subexpression*`)`이 포함되어 있습니다. 두 언어 요소 모두 너비가 0인 어설션입니다. 즉, 진행 또는 역추적 없이 현재 문자 바로 앞에 있는 문자를 *subexpression*과 일치시킬 수 있는지 여부를 확인합니다.  
  
 `(?<=` *subexpression* `)` 은 긍정 lookbehind 어설션입니다. 즉, 현재 위치 바로 전의 문자가 *subexpression*과 일치해야 합니다. `(?<!`*subexpression*`)` 은 부정 lookbehind 어설션입니다. 즉, 현재 위치 바로 전의 문자가 *subexpression*과 일치하면 안 됩니다. 긍정 및 부정 lookbehind 어설션 모두 *subexpression* 이 이전 하위 식의 하위 집합일 때 가장 유용합니다.  
  
 다음 예제에서는 전자 메일 주소에서 사용자 이름의 유효성을 검사하는 두 개의 동일한 정규식 패턴이 사용됩니다. 첫 번째 패턴은 과도한 역추적으로 인해 성능이 크게 저하됩니다. 두 번째 패턴은 중첩된 수량자를 긍정 lookbehind 어설션으로 바꿔서 첫 번째 정규식을 수정합니다. 이 예의 결과에는 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드의 실행 시간이 표시됩니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking5.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking5.vb#5)]  
  
 첫 번째 정규식 패턴 `^[0-9A-Z]([-.\w]*[0-9A-Z])*@`은(는) 다음 표와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|문자열의 시작 부분에서 검색을 시작합니다.|  
|`[0-9A-Z]`|일치하는 영숫자 문자를 찾습니다. <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드가 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션으로 호출되므로 이 비교는 대/소문자를 구분하지 않습니다.|  
|`[-.\w]*`|하이픈, 마침표 또는 단어 문자가 0개 이상 일치하는 항목을 찾습니다.|  
|`[0-9A-Z]`|일치하는 영숫자 문자를 찾습니다.|  
|`([-.\w]*[0-9A-Z])*`|영숫자 문자로 이어지는 하이픈, 마침표 또는 단어 문자가 0개 이상 조합된 일치하는 항목을 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`@`|"\@" 기호를 찾습니다.|  
  
 두 번째 정규식 패턴 `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@`은 긍정 lookbehind 어설션을 사용합니다. 이 패턴은 다음 표에서와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|문자열의 시작 부분에서 검색을 시작합니다.|  
|`[0-9A-Z]`|일치하는 영숫자 문자를 찾습니다. <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드가 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션으로 호출되므로 이 비교는 대/소문자를 구분하지 않습니다.|  
|`[-.\w]*`|하이픈, 마침표 또는 단어 문자가 0개 이상 포함된 일치하는 항목을 찾습니다.|  
|`(?<=[0-9A-Z])`|마지막으로 일치한 문자를 다시 확인하고 영숫자인 경우 검색을 계속합니다. 영숫자 문자는 마침표, 하이픈 및 모든 단어 문자로 구성되는 집합의 하위 집합입니다.|  
|`@`|"\@" 기호를 찾습니다.|  
  
<a name="Lookahead"></a>   
### <a name="lookahead-assertions"></a>lookahead 어설션  
 .NET에는 입력 문자열에서 다음 문자와 일치하는 두 가지 언어 요소인 `(?=`*subexpression*`)` 및 `(?!`*subexpression*`)`이 포함되어 있습니다. 두 언어 요소 모두 너비가 0인 어설션입니다. 즉, 진행 또는 역추적 없이 현재 문자 바로 뒤에 있는 문자를 *subexpression*과 일치시킬 수 있는지 여부를 확인합니다.  
  
 `(?=` *subexpression* `)` 은 긍정 lookahead 어설션입니다. 즉, 현재 위치 바로 뒤의 문자가 *subexpression*과 일치해야 합니다. `(?!`*subexpression*`)` 은 부정 lookahead 어설션입니다. 즉, 현재 위치 바로 뒤의 문자가 *subexpression*과 일치하면 안 됩니다. 긍정 및 부정 lookahead 어설션 모두 *subexpression* 이 다음 하위 식의 하위 집합인 경우 가장 유용합니다.  
  
 다음 예제에서는 정규화된 형식 이름의 유효성을 검사하는 두 개의 동일한 정규식 패턴이 사용됩니다. 첫 번째 패턴은 과도한 역추적으로 인해 성능이 크게 저하됩니다. 두 번째 패턴은 중첩된 수량자를 긍정 lookahead 어설션으로 바꿔서 첫 번째 정규식을 수정합니다. 이 예의 결과에는 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드의 실행 시간이 표시됩니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.Backtracking#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/cs/backtracking6.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.Backtracking#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.backtracking/vb/backtracking6.vb#6)]  
  
 첫 번째 정규식 패턴 `^(([A-Z]\w*)+\.)*[A-Z]\w*$`은(는) 다음 표와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|문자열의 시작 부분에서 검색을 시작합니다.|  
|`([A-Z]\w*)+\.`|0개 이상의 단어 문자와 마침표가 이어지는 영문자(A-Z)를 찾습니다. <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드가 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션으로 호출되므로 이 비교는 대/소문자를 구분하지 않습니다.|  
|`(([A-Z]\w*)+\.)*`|이전 패턴을 0번 이상 검색합니다.|  
|`[A-Z]\w*`|0개 이상의 단어 문자로 이어지는 영문자를 찾습니다.|  
|`$`|입력 문자열의 끝 부분에서 검색을 종료합니다.|  
  
 두 번째 정규식 패턴 `^((?=[A-Z])\w+\.)*[A-Z]\w*$`에는 긍정 lookahead 어설션이 사용됩니다. 이 패턴은 다음 표에서와 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|문자열의 시작 부분에서 검색을 시작합니다.|  
|`(?=[A-Z])`|첫 번째 문자를 검색하고 영문자(A-Z)인 경우 검색을 계속합니다. <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드가 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 옵션으로 호출되므로 이 비교는 대/소문자를 구분하지 않습니다.|  
|`\w+\.`|마침표로 이어지는 하나 이상의 문자를 검색합니다.|  
|`((?=[A-Z])\w+\.)*`|마침표가 0번 이상 이어지는 하나 이상의 단어 문자의 패턴을 검색합니다. 초기 단어 문자는 영문자여야 합니다.|  
|`[A-Z]\w*`|0개 이상의 단어 문자로 이어지는 영문자를 찾습니다.|  
|`$`|입력 문자열의 끝 부분에서 검색을 종료합니다.|  
  
 [맨 위로 이동](#top)  
  
## <a name="see-also"></a>참고 항목

- [.NET 정규식](../../../docs/standard/base-types/regular-expressions.md)
- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
- [수량자](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)
- [교체 구문](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)
- [Grouping Constructs](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)
