---
title: .NET Framework 정규식
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pattern-matching with regular expressions, about pattern-matching
- substrings
- searching with regular expressions, about regular expressions
- pattern-matching with regular expressions
- searching with regular expressions
- parsing text with regular expressions
- regular expressions [.NET Framework], about regular expressions
- regular expressions [.NET Framework]
- .NET Framework regular expressions, about
- characters [.NET Framework], regular expressions
- parsing text with regular expressions, overview
- .NET Framework regular expressions
- strings [.NET Framework], regular expressions
ms.assetid: 521b3f6d-f869-42e1-93e5-158c54a6895d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 89b527d4febb677512b3cdcf7cd47344d182ae26
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736859"
---
# <a name="net-regular-expressions"></a>.NET 정규식
정규식은 텍스트를 처리하는 강력하고 유연하며 효율적인 방법을 제공합니다. 정규식의 광범위한 패턴 일치 표기법을 사용하여 많은 양의 텍스트를 신속하게 구문 분석함으로써 특정 문자 패턴을 찾고, 텍스트의 유효성을 검사하여 해당 텍스트가 미리 정의된 패턴(예: 전자 메일 주소)과 일치하는지 확인하며, 텍스트 부분 문자열을 추출, 편집, 바꾸기 또는 삭제하고, 추출된 문자열을 컬렉션에 추가하여 보고서를 생성할 수 있습니다. 문자열을 처리하거나 텍스트의 큰 블록을 구문 분석하는 많은 애플리케이션의 경우 정규식은 필수적인 도구입니다.  
  
## <a name="how-regular-expressions-work"></a>정규식의 작동 방식  
 정규식을 사용하여 텍스트를 처리하는 중심에는 .NET에서 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 개체로 표현되는 정규식 엔진이 있습니다. 정규식을 사용하여 텍스트를 처리하려면 최소한 정규식 엔진이 다음과 같은 두 가지 정보 항목과 함께 제공되어야 합니다.  
  
- 텍스트에서 식별할 정규식 패턴  
  
     .NET에서 정규식 패턴은 특수 구문 또는 언어로 정의되며 Perl 5 정규식과 호환되고 오른쪽에서 왼쪽으로 일치와 같은 몇 가지 기능을 더 추가합니다. 자세한 내용은 [정규식 언어 - 빠른 참조](regular-expression-language-quick-reference.md)를 참조하세요.  
  
- 정규식 패턴에 대해 구문 분석할 텍스트  
  
 <xref:System.Text.RegularExpressions.Regex> 클래스의 메서드를 사용하여 다음과 같은 작업을 수행할 수 있습니다.  
  
- <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드를 호출하여 입력 텍스트에서 정규식 패턴이 발생하는지를 확인합니다. <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> 메서드를 사용하여 텍스트의 유효성을 검사하는 예제는 [방법: 문자열이 올바른 이메일 형식인지 확인](how-to-verify-that-strings-are-in-valid-email-format.md)을 참조하세요.  
  
- <xref:System.Text.RegularExpressions.Regex.Match%2A?displayProperty=nameWithType> 또는 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드를 호출하여 정규식 패턴과 일치하는 텍스트를 하나 또는 모두 검색합니다. 전자 메서드는 일치하는 텍스트에 대한 정보를 제공하는 <xref:System.Text.RegularExpressions.Match?displayProperty=nameWithType> 개체를 반환합니다. 후자는 구문 분석된 텍스트에서 찾은 각 일치 항목에 대한 하나의 <xref:System.Text.RegularExpressions.MatchCollection> 개체를 포함하는 <xref:System.Text.RegularExpressions.Match?displayProperty=nameWithType> 개체를 반환합니다.  
  
- <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 메서드를 호출하여 정규식 패턴과 일치하는 텍스트를 바꿉니다. <xref:System.Text.RegularExpressions.Regex.Replace%2A> 메서드를 사용하여 날짜 형식을 변경하고 문자열에서 잘못된 문자를 제거하는 예제는 [방법: 문자열에서 유효하지 않은 문자 제거](how-to-strip-invalid-characters-from-a-string.md) 및 [예제: 날짜 형식 변경](regular-expression-example-changing-date-formats.md)을 참조하세요.  
  
 정규식 개체 모델의 개요는 [정규식 개체 모델](the-regular-expression-object-model.md)을 참조하세요.  
  
 정규식 언어에 대한 자세한 내용은 [정규식 언어 - 빠른 참조](regular-expression-language-quick-reference.md)를 참조하거나, 다음 브로슈어 중 하나를 다운로드하여 인쇄하세요.  
  
 [Word(.docx) 형식의 빠른 참조](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)  
 [PDF(.pdf) 형식의 빠른 참조](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)  
  
## <a name="regular-expression-examples"></a>정규식 예제  
 <xref:System.String> 클래스에는 큰 문자열에서 리터럴 문자열을 찾을 때 사용할 수 있는 다양한 문자열 검색 및 바꾸기 메서드가 포함되어 있습니다. 정규식은 다음 예제에서 보여 주는 것처럼 큰 문자열에서 여러 부분 문자열 중 하나를 찾거나 문자열에서 패턴을 식별할 때 가장 유용합니다.  
  
### <a name="example-1-replacing-substrings"></a>예제 1: 부분 문자열 바꾸기  
 메일 그룹에 경우에 따라 호칭(Mr., Mrs., Miss 또는 Ms.)이 이름 및 성과 함께 포함되어 있는 이름이 들어 있다고 가정합니다. 메일 그룹에서 봉투 레이블을 생성할 때 호칭을 포함하지 않으려는 경우 다음 예제에서 보여 주는 것처럼 정규식을 사용하여 호칭을 제거할 수 있습니다.  
  
 [!code-csharp[Conceptual.Regex#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex/cs/example1.cs#2)]
 [!code-vb[Conceptual.Regex#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex/vb/example1.vb#2)]  
  
 정규식 패턴 `(Mr\.? |Mrs\.? |Miss |Ms\.? )`는 모든 "Mr", "Mr.", "Mrs", "Mrs.", "Miss", "Ms" 또는 "Ms."가 발생하는 것과 일치합니다. <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> 메서드에 대한 호출은 일치하는 문자열을 <xref:System.String.Empty?displayProperty=nameWithType>로 바꿉니다. 즉, 원래 문자열에서 일치하는 문자열을 제거합니다.  
  
### <a name="example-2-identifying-duplicated-words"></a>예제 2: 중복된 단어 식별  
 실수로 단어를 중복하는 것은 작성자가 흔히 하는 실수입니다. 다음 예제에서 보여 주는 것처럼 정규식을 사용하여 중복된 단어를 식별할 수 있습니다.  
  
 [!code-csharp[Conceptual.Regex#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex/cs/example2.cs#3)]
 [!code-vb[Conceptual.Regex#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex/vb/example2.vb#3)]  
  
 정규식 패턴 `\b(\w+?)\s\1\b`는 다음과 같이 해석될 수 있습니다.  
  
|||  
|-|-|  
|`\b`|단어 경계를 시작합니다.|  
|(\w+?)|하나 이상의 단어 문자(가능한 한 적은 문자)를 찾습니다. 이러한 단어 문자는 함께 `\1`이라고 할 수 있는 그룹을 형성합니다.|  
|`\s`|공백 문자를 찾습니다.|  
|`\1`|`\1`이라는 그룹과 같은 부분 문자열을 찾습니다.|  
|`\b`|단어 경계를 찾습니다.|  
  
 <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=nameWithType> 메서드가 정규식 옵션이 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType>로 설정된 상태로 호출됩니다. 따라서 찾기 작업은 대/소문자를 구분하지 않으며, 이 예제에서는 부분 문자열 "This this"를 중복으로 식별합니다.  
  
 입력 문자열에 부분 문자열 "this? This"가 포함되어 있습니다. 그러나 문장 부호가 중간에 있어 이는 중복으로 식별되지 않습니다.  
  
### <a name="example-3-dynamically-building-a-culture-sensitive-regular-expression"></a>예제 3: 동적으로 문화권 구분 정규식 작성  
 다음 예제에서는 정규식이 .NET의 전역화 기능에서 제공하는 유연성과 결합되었을 때의 성능을 설명합니다. 이 예제에서는 <xref:System.Globalization.NumberFormatInfo> 개체를 사용하여 시스템의 현재 문화권의 통화 값 형식을 확인합니다. 그런 다음 해당 정보를 사용하여 텍스트에서 통화 값을 추출하는 정규식을 동적으로 구성합니다. 각 일치 항목에 대해 숫자 문자열만 포함된 하위 그룹을 추출하여 <xref:System.Decimal> 값으로 변환하고 누계를 계산합니다.  
  
 [!code-csharp[Conceptual.Regex#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex/cs/example.cs#1)]
 [!code-vb[Conceptual.Regex#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex/vb/example.vb#1)]  
  
 현재 문화권이 영어 - 미국(en-US)인 컴퓨터에서 이 예제를 실행할 경우 정규식 `\$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)`가 동적으로 작성됩니다. 이 정규식 패턴은 다음과 같이 해석될 수 있습니다.  
  
|||  
|-|-|  
|`\$`|입력 문자열에서 단일 달러 기호(`$`)를 찾습니다. 정규식 패턴 문자열에는 백슬래시가 포함되어 달러 기호가 정규식 앵커로 해석되는 것이 아니라 리터럴로 해석될 것임을 나타냅니다. (`$` 기호 단독으로는 정규식 엔진이 문자열의 끝 부분에서 찾기를 시작하려고 해야 한다는 사실을 나타냅니다.) 현재 문화권의 통화 기호가 정규식 기호로 잘못 해석되지 않도록 하기 위해 이 예제에서는 <xref:System.Text.RegularExpressions.Regex.Escape%2A?displayProperty=nameWithType> 메서드를 호출하여 문자를 이스케이프합니다.|  
|`\s*`|0개 이상의 공백 문자를 찾습니다.|  
|`[-+]?`|0개 이상의 더하기 기호 또는 빼기 기호를 찾습니다.|  
|`([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)`|이 식을 둘러싼 바깥쪽 괄호는 이 식을 캡처링 그룹 또는 하위 식으로 정의합니다. 일치 항목을 찾은 경우 일치하는 문자열의 이 부분에 대한 정보는 <xref:System.Text.RegularExpressions.Group> 속성에서 반환하는 <xref:System.Text.RegularExpressions.GroupCollection> 개체의 두 번째 <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=nameWithType> 개체에서 검색할 수 있습니다. (컬렉션의 첫 번째 요소는 전체 일치를 나타냅니다.)|  
|`[0-9]{0,3}`|10진수 0-9를 0~3개 찾습니다.|  
|`(,[0-9]{3})*`|그룹 구분 기호 하나 다음에 세 개의 10진수가 있는 0개 이상의 일치 항목을 찾습니다.|  
|`\.`|단일 소수 구분 기호를 찾습니다.|  
|`[0-9]+`|하나 이상의 10진수를 찾습니다.|  
|`(\.[0-9]+)?`|소수 구분 기호 다음에 하나 이상의 10진수가 있는 0개 이상의 일치 항목을 찾습니다.|  
  
 입력 문자열에서 이러한 각 하위 패턴을 찾은 경우 찾기가 성공하고 일치 항목에 대한 정보가 포함된 <xref:System.Text.RegularExpressions.Match> 개체가 <xref:System.Text.RegularExpressions.MatchCollection> 개체에 추가됩니다.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[정규식 언어 - 빠른 참조](regular-expression-language-quick-reference.md)|정규식을 정의하는 데 사용할 수 있는 문자, 연산자 및 생성자 집합에 대한 정보를 제공합니다.|  
|[정규식 개체 모델](the-regular-expression-object-model.md)|정규식 클래스를 사용하는 방법을 보여 주는 코드 예제 및 정보를 제공합니다.|  
|[정규식 동작 정보](details-of-regular-expression-behavior.md)|.NET 정규식의 기능 및 동작에 대한 정보를 제공합니다.|  
|[정규식 예제](regular-expression-examples.md)|정규식의 일반적인 사용을 보여 주는 코드 예제를 제공합니다.|  
  
## <a name="reference"></a>참조  
 <xref:System.Text.RegularExpressions?displayProperty=nameWithType>  
 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>  
 [정규식 - 빠른 참조(Word 형식으로 다운로드)](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)  
 [정규식 - 빠른 참조(PDF 형식으로 다운로드)](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)
