---
title: Regular Expression 개체 모델
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, backreferences
- Regex class
- Match class
- pattern-matching with regular expressions, backreferences
- .NET Framework regular expressions, classes
- CaptureCollection class
- Group class
- characters [.NET Framework], backreferences
- substrings
- .NET Framework regular expressions, backreferences
- searching with regular expressions, classes
- backreferences
- Capture class
- repeating groups of characters
- MatchCollection class
- parsing text with regular expressions, backreferences
- regular expressions [.NET Framework]
- characters [.NET Framework], regular expressions
- classes [.NET Framework], regular expression
- regular expressions [.NET Framework], classes
- characters [.NET Framework], metacharacters
- metacharacters, regular expression classes
- metacharacters, backreferences
- parsing text with regular expressions, classes
- regular expressions [.NET Framework], backreferences
- strings [.NET Framework], regular expressions
- pattern-matching with regular expressions, classes
- GroupCollection class
ms.assetid: 49a21470-64ca-4b5a-a889-8e24e3c0af7e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ea31dc154d5df2b0058af4c04035d096d5e850c3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64664669"
---
# <a name="the-regular-expression-object-model"></a>Regular Expression 개체 모델
<a name="introduction"></a> 이 항목에서는 .NET 정규식 작업을 수행하는 데 사용되는 개체 모델을 설명합니다. 여기에는 다음 단원이 포함되어 있습니다.  
  
- [정규식 엔진](#Engine)  
  
- [MatchCollection 및 Match 개체](#Match_and_MCollection)  
  
- [그룹 컬렉션](#GroupCollection)  
  
- [캡처된 그룹](#the_captured_group)  
  
- [캡처 컬렉션](#CaptureCollection)  
  
- [개별 캡처](#the_individual_capture)  
  
<a name="Engine"></a>   
## <a name="the-regular-expression-engine"></a>정규식 엔진  
 .NET의 정규식 엔진은 <xref:System.Text.RegularExpressions.Regex> 클래스로 표현됩니다. 정규식 엔진은 정규식을 구문 분석 및 컴파일하고, 정규식 패턴을 입력 문자열과 일치시키는 작업 수행을 담당합니다. 이 엔진은 .NET 정규식 개체 모델의 중심 구성 요소입니다.  
  
 정규식 엔진은 다음과 같은 두 가지 방법 중 하나로 사용할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.Regex> 클래스의 정적 메서드를 호출합니다. 메서드 매개 변수에는 입력 문자열과 정규식 패턴이 포함됩니다. 정규식 엔진은 정적 메서드 호출에 사용되는 정규식을 캐시하므로 동일한 정규식을 사용하는 정적 정규식 메서드에 대한 반복 호출은 상대적으로 좋은 성능을 제공합니다.  
  
- 정규식을 클래스 생성자에 전달하여 <xref:System.Text.RegularExpressions.Regex> 개체를 인스턴스화합니다. 이 경우 <xref:System.Text.RegularExpressions.Regex> 개체는 변경 불가능하며(읽기 전용), 단일 정규식과 강력하게 결합된 정규식 엔진을 나타냅니다. <xref:System.Text.RegularExpressions.Regex> 인스턴스에 사용되는 정규식은 캐시되지 않으므로 동일한 정규식으로 <xref:System.Text.RegularExpressions.Regex> 개체를 여러 번 인스턴스화해서는 안 됩니다.  
  
 <xref:System.Text.RegularExpressions.Regex> 클래스의 메서드를 호출하여 다음과 같은 작업을 수행할 수 있습니다.  
  
- 문자열이 정규식 패턴과 일치하는지 확인합니다.  
  
- 단일 일치 항목 또는 첫 번째 일치 항목을 추출합니다.  
  
- 모든 일치 항목을 추출합니다.  
  
- 일치하는 부분 문자열을 바꿉니다.  
  
- 단일 문자열을 문자열 배열로 분할합니다.  
  
 이러한 작업은 다음 섹션에 설명되어 있습니다.  
  
### <a name="matching-a-regular-expression-pattern"></a>정규식 패턴 일치  
 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드는 문자열이 패턴과 일치할 경우 `true`를 반환하고, 그렇지 않을 경우 `false`를 반환합니다. <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> 메서드는 일반적으로 문자열 입력의 유효성을 검사하는 데 사용됩니다. 예를 들어, 다음 코드는 문자열이 미국의 유효한 사회 보장 번호와 일치하도록 합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/validate1.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/validate1.vb#1)]  
  
 정규식 패턴 `^\d{3}-\d{2}-\d{4}$` 는 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|입력 문자열의 시작 부분을 찾습니다.|  
|`\d{3}`|세 개의 10진수를 찾습니다.|  
|`-`|하이픈을 찾습니다.|  
|`\d{2}`|두 개의 10진수를 찾습니다.|  
|`-`|하이픈을 찾습니다.|  
|`\d{4}`|네 개의 10진수를 찾습니다.|  
|`$`|입력 문자열의 끝 부분을 찾습니다.|  
  
### <a name="extracting-a-single-match-or-the-first-match"></a>단일 일치 항목 또는 첫 번째 일치 항목 추출  
 <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> 메서드는 정규식 패턴과 일치하는 첫 번째 부분 문자열에 대한 정보가 포함된 <xref:System.Text.RegularExpressions.Match> 개체를 반환합니다. `Match.Success` 속성이 일치 항목을 찾았음을 나타내는 `true`를 반환하는 경우 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 메서드를 호출하여 후속 일치 항목에 대한 정보를 검색할 수 있습니다. 이러한 메서드 호출은 `Match.Success` 속성이 `false`를 반환할 때까지 계속될 수 있습니다. 예를 들어, 다음 코드에서는 <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType> 메서드를 사용하여 문자열에서 첫 번째 중복된 단어를 찾습니다. 그런 다음 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 메서드를 호출하여 추가 중복된 단어를 찾습니다. 이 예제에서는 현재 찾기가 성공했는지와 `Match.Success` 메서드에 대한 호출이 뒤따라야 하는지를 확인하기 위해 메서드를 호출한 후마다 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 속성을 검토합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match1.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match1.vb#2)]  
  
 정규식 패턴 `\b(\w+)\W+(\1)\b` 는 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`(\w+)`|하나 이상의 단어 문자를 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`\W+`|하나 이상의 단어가 아닌 문자를 찾습니다.|  
|`(\1)`|캡처된 첫 번째 문자열을 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
### <a name="extracting-all-matches"></a>모든 일치 항목 추출  
 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드는 정규식 엔진이 입력 문자열에서 찾은 모든 일치 항목에 대한 정보가 포함된 <xref:System.Text.RegularExpressions.MatchCollection> 개체를 반환합니다. 예를 들어, 이전 예제를 <xref:System.Text.RegularExpressions.Regex.Matches%2A> 및 <xref:System.Text.RegularExpressions.Regex.Match%2A> 메서드 대신 <xref:System.Text.RegularExpressions.Match.NextMatch%2A> 메서드를 호출하도록 다시 작성할 수 있습니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/matches1.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/matches1.vb#3)]  
  
### <a name="replacing-a-matched-substring"></a>일치하는 부분 문자열 바꾸기  
 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 메서드는 정규식 패턴과 일치하는 각 부분 문자열을 지정된 문자열 또는 정규식 패턴으로 바꾸고, 바뀐 내용이 포함된 전체 입력 문자열을 반환합니다. 예를 들어, 다음 코드는 문자열에서 10진수 앞에 미국 통화 기호를 추가합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/replace1.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/replace1.vb#4)]  
  
 정규식 패턴 `\b\d+\.\d{2}\b` 는 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`\d+`|하나 이상의 10진수 숫자가 일치하는지 확인합니다.|  
|`\.`|마침표를 찾습니다.|  
|`\d{2}`|두 개의 10진수를 찾습니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 바꾸기 패턴 `$$$&`는 다음 테이블과 같이 해석됩니다.  
  
|무늬|바꾸기 문자열|  
|-------------|------------------------|  
|`$$`|달러 기호($) 문자|  
|`$&`|일치하는 전제 부분 문자열|  
  
### <a name="splitting-a-single-string-into-an-array-of-strings"></a>단일 문자열을 문자열 배열로 분할  
 <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> 메서드는 정규식 일치에 의해 정의된 위치에서 입력 문자열을 분할합니다. 예를 들어, 다음 코드는 번호 매기기 목록의 항목을 문자열 배열에 배치합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/split1.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/split1.vb#5)]  
  
 정규식 패턴 `\b\d{1,2}\.\s` 는 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`\d{1,2}`|한 개 또는 두 개의 10진수를 찾습니다.|  
|`\.`|마침표를 찾습니다.|  
|`\s`|공백 문자를 찾습니다.|  
  
<a name="Match_and_MCollection"></a>   
## <a name="the-matchcollection-and-match-objects"></a>MatchCollection 및 Match 개체  
 정규식 메서드가 정규식 개체 모델의 일부인 두 개체 <xref:System.Text.RegularExpressions.MatchCollection> 개체 및 <xref:System.Text.RegularExpressions.Match> 개체를 반환합니다.  
  
<a name="the_match_collection"></a>   
### <a name="the-match-collection"></a>일치 컬렉션  
 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드는 정규식 엔진이 입력 문자열에서 찾은 모든 일치 항목(입력 문자열에서 나타나는 순서대로)을 나타내는 <xref:System.Text.RegularExpressions.MatchCollection> 개체가 포함된 <xref:System.Text.RegularExpressions.Match> 개체를 반환합니다. 일치 항목이 없는 경우 이 메서드는 멤버 없이 <xref:System.Text.RegularExpressions.MatchCollection> 개체를 반환합니다. <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> 속성을 사용하여 인덱스(0에서 <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> 속성 값보다 1 작은 값까지)별로 컬렉션의 개별 멤버에 액세스할 수 있습니다. <xref:System.Text.RegularExpressions.MatchCollection.Item%2A>은 컬렉션의 인덱서(C#의 경우) 및 기본 속성(Visual Basic의 경우)입니다.  
  
 기본적으로 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드에 대한 호출에서는 지연 평가를 사용하여 <xref:System.Text.RegularExpressions.MatchCollection> 개체를 채웁니다. 완전히 채워진 컬렉션이 필요한 속성(예: <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> 및 <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> 속성)에 액세스할 경우 성능이 저하될 수 있습니다. 따라서 <xref:System.Collections.IEnumerator> 메서드에서 반환하는 <xref:System.Text.RegularExpressions.MatchCollection.GetEnumerator%2A?displayProperty=nameWithType> 개체를 사용하여 컬렉션에 액세스하는 것이 좋습니다. 개별 언어는 컬렉션의 <xref:System.Collections.IEnumerator> 인터페이스를 래핑하는 생성자(예: Visual Basic의 경우 `For Each` 및 C#의 경우 `foreach`)를 제공합니다.  
  
 다음 예제에서는 <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%29?displayProperty=nameWithType> 메서드를 사용하여, 입력 문자열에서 찾은 모든 일치 항목으로 <xref:System.Text.RegularExpressions.MatchCollection> 개체를 채웁니다. 이 예제에서는 컬렉션을 열거하고 문자열 배열에 일치 항목을 복사하며 정수 배열에 문자 위치를 기록합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/matchcollection1.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/matchcollection1.vb#6)]  
  
<a name="the_match"></a>   
### <a name="the-match"></a>일치  
 <xref:System.Text.RegularExpressions.Match> 클래스는 단일 정규식 일치의 결과를 나타냅니다. 다음과 같은 두 가지 방법으로 <xref:System.Text.RegularExpressions.Match> 개체에 액세스할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.MatchCollection> 메서드에서 반환하는 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 개체에서 해당 개체를 검색합니다. 개별 <xref:System.Text.RegularExpressions.Match> 개체를 검색하려면 `foreach`(C#의 경우) 또는 `For Each`...`Next`(Visual Basic의 경우) 생성자를 사용하여 컬렉션을 반복하거나, <xref:System.Text.RegularExpressions.MatchCollection.Item%2A?displayProperty=nameWithType> 속성을 사용하여 인덱스 또는 이름으로 특정 <xref:System.Text.RegularExpressions.Match> 개체를 검색합니다. 또한 인덱스(0에서 컬렉션의 개체 수보다 1 작은 값까지)로 컬렉션을 반복하여 컬렉션에서 개별 <xref:System.Text.RegularExpressions.Match> 개체를 검색할 수 있습니다. 그러나 이 메서드는 <xref:System.Text.RegularExpressions.MatchCollection.Count%2A?displayProperty=nameWithType> 속성에 액세스하므로 지연 평가를 사용하지 않습니다.  
  
     다음 예제에서는 <xref:System.Text.RegularExpressions.Match> 또는 <xref:System.Text.RegularExpressions.MatchCollection>...`foreach` 생성자를 사용하여 컬렉션을 반복함으로써 `For Each` 개체에서 개별 `Next` 개체를 검색합니다. 정규식은 단순히 입력 문자열에서 문자열 "abc"를 찾습니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match2.vb#7)]  
  
- 문자열 또는 문자열 일부에서 첫 번째 일치 항목을 나타내는 <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> 개체를 반환하는 <xref:System.Text.RegularExpressions.Match> 메서드를 호출합니다. `Match.Success` 속성 값을 검색하여 일치 항목을 찾았는지를 확인할 수 있습니다. 후속 일치 항목을 나타내는 <xref:System.Text.RegularExpressions.Match> 개체를 검색하려면 반환된 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 개체의 `Success` 속성이 <xref:System.Text.RegularExpressions.Match>일 때까지 `false` 메서드를 반복적으로 호출합니다.  
  
     다음 예제에서는 <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=nameWithType> 및 <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 메서드를 사용하여 입력 문자열에서 문자열 "abc"를 찾습니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/match3.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/match3.vb#8)]  
  
 <xref:System.Text.RegularExpressions.Match> 클래스의 두 속성은 컬렉션 개체를 반환합니다.  
  
- <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 속성은 정규식 패턴에서 캡처링 그룹과 일치하는 부분 문자열에 대한 정보가 포함된 <xref:System.Text.RegularExpressions.GroupCollection> 개체를 반환합니다.  
  
- `Match.Captures` 속성은 사용이 제한된 <xref:System.Text.RegularExpressions.CaptureCollection> 개체를 반환합니다. 컬렉션은 <xref:System.Text.RegularExpressions.Match> 속성이 `Success`인 `false` 개체에 대해서는 채워지지 않습니다. 그렇지 않은 경우 이 컬렉션은 <xref:System.Text.RegularExpressions.Capture> 개체와 동일한 정보를 가진 단일 <xref:System.Text.RegularExpressions.Match> 개체를 포함합니다.  
  
 이러한 개체에 대한 자세한 내용은 이 항목 뒷부분의 [그룹 컬렉션](#GroupCollection) 및 [캡처 컬렉션](#CaptureCollection) 섹션을 참조하세요.  
  
 <xref:System.Text.RegularExpressions.Match> 클래스의 두 추가 속성은 일치 항목에 대한 정보를 제공합니다. `Match.Value` 속성은 입력 문자열에서 정규식 패턴과 일치하는 부분 문자열을 반환합니다. `Match.Index` 속성은 입력 문자열에서 일치하는 문자열의 0부터 시작하는 시작 위치를 반환합니다.  
  
 또한 <xref:System.Text.RegularExpressions.Match> 클래스에는 두 개의 패턴 일치 메서드가 포함되어 있습니다.  
  
- <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=nameWithType> 메서드는 현재 <xref:System.Text.RegularExpressions.Match> 개체가 나타내는 일치 항목 뒤에서 일치 항목을 찾아 해당 일치 항목을 나타내는 <xref:System.Text.RegularExpressions.Match> 개체를 반환합니다.  
  
- <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 메서드는 일치하는 문자열에 대해 지정된 바꾸기 작업을 수행하고 결과를 반환합니다.  
  
 다음 예제에서는 <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> 메서드를 사용하여, 두 소수 자릿수를 포함하는 모든 숫자 앞에 $ 기호와 공백 하나를 추가합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/result1.cs#9)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/result1.vb#9)]  
  
 정규식 패턴 `\b\d+(,\d{3})*\.\d{2}\b` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`\d+`|하나 이상의 10진수 숫자가 일치하는지 확인합니다.|  
|`(,\d{3})*`|쉼표 하나 다음에 세 개의 10진수가 있는 0개 이상의 일치 항목을 찾습니다.|  
|`\.`|소수점 문자를 찾습니다.|  
|`\d{2}`|두 개의 10진수를 찾습니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 바꾸기 패턴 `$$ $&`는 일치하는 부분 문자열이 달러 기호($)(`$$` 패턴), 공백 하나 및 일치 항목 값(`$&` 패턴)으로 바뀌어야 함을 나타냅니다.  
  
 [맨 위로 이동](#introduction)  
  
<a name="GroupCollection"></a>   
## <a name="the-group-collection"></a>그룹 컬렉션  
 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 속성은 단일 일치 항목에서 캡처된 그룹을 나타내는 <xref:System.Text.RegularExpressions.GroupCollection> 개체가 포함된 <xref:System.Text.RegularExpressions.Group> 개체를 반환합니다. 컬렉션의 첫 번째 <xref:System.Text.RegularExpressions.Group> 개체(인덱스 0에 있음)는 전체 일치를 나타냅니다. 뒤에 나오는 각 개체는 단일 캡처링 그룹의 결과를 나타냅니다.  
  
 <xref:System.Text.RegularExpressions.Group> 속성을 사용하여 컬렉션에서 개별 <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=nameWithType> 개체를 검색할 수 있습니다. 명명되지 않은 그룹은 컬렉션에서 위치로 검색하고, 명명된 그룹은 이름 또는 위치로 검색할 수 있습니다. 명명되지 않은 캡처는 컬렉션에서 맨 앞에 나타나고, 정규식 패턴에서 나타나는 순서대로 왼쪽에서 오른쪽으로 인덱싱됩니다. 명명된 캡처는 명명되지 않은 캡처 다음에, 정규식 패턴에서 나타나는 순서대로 왼쪽에서 오른쪽으로 인덱싱됩니다. 특정 정규식 일치 메서드에 대해 반환된 컬렉션에서 사용 가능한 번호가 매겨진 그룹을 확인하려면 인스턴스 <xref:System.Text.RegularExpressions.Regex.GetGroupNumbers%2A?displayProperty=nameWithType> 메서드를 호출하면 됩니다. 컬렉션에서 사용 가능한 명명된 그룹을 확인하려면 인스턴스 <xref:System.Text.RegularExpressions.Regex.GetGroupNames%2A?displayProperty=nameWithType> 메서드를 호출하면 됩니다. 두 메서드는 모두 정규식으로 찾은 일치 항목을 분석하는 범용 루틴에서 특히 유용합니다.  
  
 <xref:System.Text.RegularExpressions.GroupCollection.Item%2A?displayProperty=nameWithType> 속성은 컬렉션의 인덱스(C#의 경우) 및 컬렉션 개체의 기본 속성(Visual Basic의 경우)입니다. 즉, 개별 <xref:System.Text.RegularExpressions.Group> 개체를 다음과 같이 인덱스로(또는 명명된 그룹의 경우 이름으로) 액세스할 수 있습니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/groupsyntax1.cs#13)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/groupsyntax1.vb#13)]  
  
 다음 예제에서는 그룹화 구문을 사용하여 날짜의 월, 일 및 연도를 캡처하는 정규식을 정의합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/groupcollection1.cs#10)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/groupcollection1.vb#10)]  
  
 정규식 패턴 `\b(\w+)\s(\d{1,2}),\s(\d{4})\b` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\b`|단어 경계에서 일치 항목 찾기를 시작합니다.|  
|`(\w+)`|하나 이상의 단어 문자를 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`\s`|공백 문자를 찾습니다.|  
|`(\d{1,2})`|한 개 또는 두 개의 10진수를 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|  
|`,`|쉼표 하나를 찾습니다.|  
|`\s`|공백 문자를 찾습니다.|  
|`(\d{4})`|네 개의 10진수를 찾습니다. 이 그룹은 세 번째 캡처링 그룹입니다.|  
|`\b`|단어 경계에서 일치 항목 찾기를 끝냅니다.|  
  
 [맨 위로 이동](#introduction)  
  
<a name="the_captured_group"></a>   
## <a name="the-captured-group"></a>캡처된 그룹  
 <xref:System.Text.RegularExpressions.Group> 클래스는 단일 캡처링 그룹의 결과를 나타냅니다. 정규식에 정의된 캡처링 그룹을 나타내는 그룹 개체는 <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> 속성에서 반환하는 <xref:System.Text.RegularExpressions.GroupCollection> 개체의 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 속성에서 반환합니다. <xref:System.Text.RegularExpressions.GroupCollection.Item%2A> 속성은 <xref:System.Text.RegularExpressions.Group> 클래스의 인덱스(C#의 경우) 및 기본 속성(Visual Basic의 경우)입니다. 또한 `foreach` 또는 `For Each` 구문을 사용하여 컬렉션을 반복함으로써 개별 멤버를 검색할 수 있습니다. 예제는 이전 섹션을 참조하세요.  
  
 다음 예제에서는 중첩된 그룹화 구문을 사용하여 부분 문자열을 그룹으로 캡처합니다. 정규식 패턴 `(a(b))c`는 문자열 "abc"와 일치합니다. 이 패턴은 부분 문자열 "ab"를 첫 번째 캡처링 그룹에 할당하고 부분 문자열 "b"를 두 번째 캡처링 그룹에 할당합니다.  
  
 [!code-csharp[RegularExpressions.Classes#6](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#6)]
 [!code-vb[RegularExpressions.Classes#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#6)]  
  
 다음 예제에서는 명명된 그룹화 구문을 사용하여 문자열에서 정규식을 콜론(:)에서 분할하는 "DATANAME:VALUE" 형식의 데이터가 포함된 부분 문자열을 캡처합니다.  
  
 [!code-csharp[RegularExpressions.Classes#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#8)]
 [!code-vb[RegularExpressions.Classes#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#8)]  
  
 정규식 패턴 `^(?<name>\w+):(?<value>\w+)` 는 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|입력 문자열의 시작 부분에서 일치 항목 찾기를 시작합니다.|  
|`(?<name>\w+)`|하나 이상의 단어 문자를 찾습니다. 캡처링 그룹은 이름은 `name`입니다.|  
|`:`|콜론 하나를 찾습니다.|  
|`(?<value>\w+)`|하나 이상의 단어 문자를 찾습니다. 캡처링 그룹은 이름은 `value`입니다.|  
  
 <xref:System.Text.RegularExpressions.Group> 클래스의 속성은 캡처된 그룹에 대한 정보를 제공합니다. `Group.Value` 속성은 캡처된 부분 문자열을 포함하고, `Group.Index` 속성은 입력 텍스트에서 캡처된 그룹의 시작 위치를 나타내며, `Group.Length` 속성은 캡처된 텍스트의 길이를 포함하고, `Group.Success` 속성은 부분 문자열이 캡처링 그룹에 의해 정의된 패턴과 일치하는지를 나타냅니다.  
  
 그룹에 수량자를 적용하면(자세한 내용은 [수량자](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md) 참조) 캡처링 그룹별로 한 캡처의 관계가 다음과 같은 두 가지 방법으로 수정됩니다.  
  
- 그룹에 `*` 또는 `*?` 수량자(0개 이상의 일치 항목을 지정함)가 적용된 경우 캡처링 그룹은 입력 문자열에 일치 항목이 없을 수도 있습니다. 캡처된 텍스트가 없는 경우 <xref:System.Text.RegularExpressions.Group> 개체의 속성은 다음 테이블과 같이 설정됩니다.  
  
    |그룹 속성|값|  
    |--------------------|-----------|  
    |`Success`|`false`|  
    |`Value`|<xref:System.String.Empty?displayProperty=nameWithType>|  
    |`Length`|0|  
  
     다음 예제에서 이에 대해 설명합니다. 정규식 패턴 `aaa(bbb)*ccc`에서 첫 번째 캡처링 그룹(부분 문자열 "bbb")은 0번 이상 일치할 수 있습니다. 입력 문자열 "aaaccc"가 패턴과 일치하므로 캡처링 그룹은 일치 항목이 없습니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/nocapture1.cs#11)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/nocapture1.vb#11)]  
  
- 수량자는 캡처링 그룹에 의해 정의된 패턴과 여러 번 일치할 수 있습니다. 이 경우 `Value` 개체의 `Length` 및 <xref:System.Text.RegularExpressions.Group> 속성은 캡처된 마지막 부분 문자열에 대한 정보만 포함합니다. 예를 들어, 다음 정규식은 마침표로 끝나는 단일 문장과 일치합니다. 두 개의 그룹화 구문을 사용합니다. 첫 번째 그룹화 구문은 개별 단어를 공백 문자와 함께 캡처하고, 두 번째 그룹화 구문은 개별 단어를 캡처합니다. 예제의 출력이 보여 주는 것처럼, 정규식이 전체 문장을 캡처하는 데 성공하더라도 두 번째 캡처링 그룹은 마지막 단어만 캡처합니다.  
  
     [!code-csharp[Conceptual.RegularExpressions.ObjectModel#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/lastcapture1.cs#12)]
     [!code-vb[Conceptual.RegularExpressions.ObjectModel#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/lastcapture1.vb#12)]  
  
 [맨 위로 이동](#introduction)  
  
<a name="CaptureCollection"></a>   
## <a name="the-capture-collection"></a>캡처 컬렉션  
 <xref:System.Text.RegularExpressions.Group> 개체는 마지막 캡처에 대한 정보만 포함합니다. 그러나 캡처링 그룹에 의해 만들어진 캡처의 전체 집합은 <xref:System.Text.RegularExpressions.CaptureCollection> 속성에서 반환하는 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 개체에서 계속 제공합니다. 컬렉션의 각 멤버는 해당 캡처링 그룹에 의해 만들어진 캡처를 캡처된 순서(및 따라서 캡처된 문자열이 입력 문자열에서 왼쪽에서 오른쪽으로 검색된 순서)대로 나타내는 <xref:System.Text.RegularExpressions.Capture> 개체입니다. 다음과 같은 두 가지 방법 중 하나로 컬력션에서 개별 <xref:System.Text.RegularExpressions.Capture> 개체를 검색할 수 있습니다.  
  
- `foreach`(C#의 경우) 또는 `For Each`(Visual Basic의 경우)와 같은 생성자를 사용하여 컬렉션을 반복합니다.  
  
- <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A?displayProperty=nameWithType> 속성을 사용하여 인덱스로 특정 개체를 검색합니다. <xref:System.Text.RegularExpressions.CaptureCollection.Item%2A> 속성은 <xref:System.Text.RegularExpressions.CaptureCollection> 개체의 기본 속성(Visual Basic의 경우) 또는 인덱서(C#의 경우)입니다.  
  
 캡처링 그룹에 수량자가 적용되지 않은 경우 <xref:System.Text.RegularExpressions.CaptureCollection> 개체는 별로 관심이 없는 단일 <xref:System.Text.RegularExpressions.Capture> 개체를 포함하는데, 해당 <xref:System.Text.RegularExpressions.Group> 개체와 동일한 일치 항목에 대한 정보를 제공하기 때문입니다. 캡처링 그룹에 수량자가 적용된 경우 <xref:System.Text.RegularExpressions.CaptureCollection> 개체는 캡처링 그룹에 의해 만들어진 모든 캡처를 포함하고, 컬렉션의 마지막 멤버는 <xref:System.Text.RegularExpressions.Group> 개체와 동일한 캡처를 나타냅니다.  
  
 예를 들어, 정규식 패턴 `((a(b))c)+`(여기서 + 수량자는 하나 이상의 일치 항목을 지정함)를 사용하여 문자열 "abcabcabc"에서 일치 항목을 캡처하는 경우 각 <xref:System.Text.RegularExpressions.CaptureCollection> 개체의 <xref:System.Text.RegularExpressions.Group> 개체는 세 개의 멤버를 포함합니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/capturecollection1.cs#14)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/capturecollection1.vb#14)]  
  
 다음 예제에서는 정규식 `(Abc)+`를 사용하여 문자열 "XYZAbcAbcAbcXYZAbcAb"에서 문자열 "Abc"의 하나 이상의 연속 발생을 찾습니다. 이 예제에서는 <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=nameWithType> 속성을 사용하여, 캡처된 부분 문자열의 여러 그룹을 반환하는 방법을 보여 줍니다.  
  
 [!code-csharp[RegularExpressions.Classes#5](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Classes/cs/Example.cs#5)]
 [!code-vb[RegularExpressions.Classes#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Classes/vb/Example.vb#5)]  
  
 [맨 위로 이동](#introduction)  
  
<a name="the_individual_capture"></a>   
## <a name="the-individual-capture"></a>개별 캡처  
 <xref:System.Text.RegularExpressions.Capture> 클래스는 단일 하위 식 캡처의 결과를 포함합니다. <xref:System.Text.RegularExpressions.Capture.Value%2A?displayProperty=nameWithType> 속성은 일치하는 텍스트를 포함하고, <xref:System.Text.RegularExpressions.Capture.Index%2A?displayProperty=nameWithType> 속성은 입력 문자열에서 일치하는 하위 문장열이 시작하는 위치(0부터 시작함)를 나타냅니다.  
  
 다음 예제에서는 선택된 도시의 온도에 대한 입력 문자열을 구문 분석합니다. 도시와 해당 온도를 구분하는 데 쉼표(",")가 사용되었으며, 각 도시의 데이터를 구분하는 데 세미콜론(";")이 사용되었습니다. 전체 입력 문자열은 단일 일치 항목을 나타냅니다. 문자열을 구문 분석하는 데 사용되는 정규식 패턴 `((\w+(\s\w+)*),(\d+);)+`에서 도시 이름은 두 번째 캡처링 그룹에 할당되었고, 온도는 네 번째 캡처링 그룹에 할당되었습니다.  
  
 [!code-csharp[Conceptual.RegularExpressions.ObjectModel#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/cs/capture1.cs#16)]
 [!code-vb[Conceptual.RegularExpressions.ObjectModel#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.objectmodel/vb/capture1.vb#16)]  
  
 정규식은 다음 테이블과 같이 정의됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\w+`|하나 이상의 단어 문자를 찾습니다.|  
|`(\s\w+)*`|공백 문자 다음에 하나 이상의 단어 문자가 있는 0개 이상의 일치 항목을 찾습니다. 이 패턴에서는 여러 단어로 된 도시 이름을 찾습니다. 이 그룹은 세 번째 캡처링 그룹입니다.|  
|`(\w+(\s\w+)*)`|하나 이상의 단어 문자 다음에 0개 이상의 공백 문자 및 하나 이상의 단어 문자가 있는 일치 항목을 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|  
|`,`|쉼표 하나를 찾습니다.|  
|`(\d+)`|하나 이상의 숫자를 찾습니다. 이 그룹은 네 번째 캡처링 그룹입니다.|  
|`;`|세미콜론을 하나 찾습니다.|  
|`((\w+(\s\w+)*),(\d+);)+`|단어 하나 다음에 추가 단어가 있고 그 다음에 쉼표 하나, 하나 이상의 숫자 및 세미콜론 하나가 한 번 이상 나타나는 패턴을 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Text.RegularExpressions>
- [.NET 정규식](../../../docs/standard/base-types/regular-expressions.md)
- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
