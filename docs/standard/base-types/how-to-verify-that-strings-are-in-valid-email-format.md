---
title: '방법: 문자열이 올바른 전자 메일 형식인지 확인'
ms.date: 08/10/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, examples
- user input, examples
- Regex.IsMatch method
- regular expressions [.NET Framework], examples
- examples [Visual Basic], strings
- IsValidEmail
- validation, email strings
- input, checking
- strings [.NET Framework], examples [Visual Basic]
- email [.NET Framework], validating
- IsMatch method
ms.assetid: 7536af08-4e86-4953-98a1-a8298623df92
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1fe0ead93d1ff2b7867a52d80cf812e2850ea7b3
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836299"
---
# <a name="how-to-verify-that-strings-are-in-valid-email-format"></a>방법: 문자열이 올바른 전자 메일 형식인지 확인
다음 예제에서는 정규식을 사용하여 문자열이 올바른 전자 메일 형식인지 확인합니다.  

## <a name="example"></a>예  
 이 예제에서는 문자열에 올바른 전자 메일 주소가 포함되어 있으면 `IsValidEmail` 를 반환하고, 그렇지 않으면 `true` 를 반환하지만 다른 작업을 수행하지 않는 `false` 메서드를 정의합니다.  
  
 전자 메일 주소가 올바른지 확인하기 위해 `IsValidEmail` 메서드는 <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.MatchEvaluator%29?displayProperty=nameWithType> 정규식 패턴으로 `(@)(.+)$` 메서드를 호출하여 전자 메일 주소에서 도메인 이름을 분리합니다. 세 번째 매개 변수는 일치하는 텍스트를 처리하고 대체하는 메서드를 나타내는 <xref:System.Text.RegularExpressions.MatchEvaluator> 대리자입니다. 정규식 패턴은 다음과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`(@)`|@ 문자를 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`(.+)`|하나 이상의 문자를 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|  
|`$`|문자열의 끝 부분에서 일치 항목 찾기를 끝냅니다.|  
  
 @ 문자와 함께 도메인 이름이 `DomainMapper` 메서드로 전달됩니다. 이 메서드는 <xref:System.Globalization.IdnMapping> 클래스를 사용하여 US-ASCII 문자 범위 외부에 있는 유니코드 문자를 Punycode로 변환합니다. 이 메서드는 `invalid` 메서드가 도메인 이름에서 잘못된 문자를 발견하는 경우 `True` 플래그를 <xref:System.Globalization.IdnMapping.GetAscii%2A?displayProperty=nameWithType>로 설정합니다. 메서드는 앞에 @ 기호가 있는 Punycode 도메인 이름을 `IsValidEmail` 메서드에 반환합니다.  
  
 그러면 `IsValidEmail` 메서드는 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=nameWithType> 메서드를 호출하여 주소가 정규식 패턴을 따르는지 확인합니다.  
  
 `IsValidEmail` 메서드는 전자 메일 주소의 유효성을 검사하기 위해 인증을 수행하는 것이 아닙니다. 단지 형식이 전자 메일 주소에 올바른지 여부만 확인합니다. 또한 `IsValidEmail` 메서드는 최상위 도메인 이름이 조회 작업 시 요구되는 [IANA 루트 영역 데이터베이스](https://www.iana.org/domains/root/db)에 나열된 올바른 도메인 이름인지 확인하지 않습니다. 대신, 정규식은 최상위 도메인 이름이 2~24개의 ASCII 문자(첫 번째 문자와 마지막 문자는 영숫자이고, 나머지 문자는 영숫자이거나 하이픈(-)임)로 구성되었는지만 확인합니다.  
  
 [!code-csharp[RegularExpressions.Examples.Email#7](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Email/cs/example4.cs#7)]
 [!code-vb[RegularExpressions.Examples.Email#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Email/vb/example4.vb#7)]  
  
 이 예제에서 정규식 패턴 ``^(?(")(".+?(?<!\\)"@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`{}|~\w])*)(?<=[0-9a-z])@))(?([)([(\d{1,3}.){3}\d{1,3}])|(([0-9a-z][-0-9a-z]*[0-9a-z]*.)+[a-z0-9][-a-z0-9]{0,22}[a-z0-9]))$``는 다음 테이블과 같이 해석됩니다. 정규식은 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> 플래그를 사용하여 컴파일됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`^`|문자열의 시작 부분에서 일치 항목 찾기를 시작합니다.|  
|`(?(")`|첫 번째 문자가 따옴표인지 확인합니다. `(?(")` 는 대체 구문의 시작 부분입니다.|  
|`(?("")("".+?(?<!\\)""@)`|첫 번째 문자가 따옴표인 경우 시작 따옴표 뒤에 임의의 문자가 1개 이상 나오고 그 뒤에 끝 따옴표가 나오는 일치 항목을 찾습니다. 끝 따옴표는 앞에 백슬래시 문자(\\)가 없어야 합니다. `(?<!` 는 너비가 0인 부정 lookbehind 어설션의 시작 부분입니다. 문자열은 @ 기호로 끝나야 합니다.|  
|<code>&#124;(([0-9a-z]</code>|첫 번째 문자가 따옴표가 아니면 a-z 또는 A-Z(비교는 대/소문자를 구분하지 않음)의 영문자 또는 0-9의 숫자를 찾습니다.|  
|`(\.(?!\.))`|다음 문자가 마침표이면 일치하게 됩니다. 마침표가 아니면 왼쪽에서 오른쪽으로 다음 문자를 검색하여 일치 항목을 계속 찾습니다. `(?!\.)` 는 메일 주소의 로컬 부분에 마침표 두 개가 연속으로 나타나지 않도록 하며 너비가 0인 부정 lookahead 어설션입니다.|  
|<code>&#124;[-!#\$%&'\*\+/=\?\^\`{}\&#124;~\w]</code>|다음 문자가 마침표가 아니면 단어 문자 또는 -!#$%'*+=?^\`{}&#124;~ 중 하나를 찾습니다.|  
|<code>((\.(?!\.))&#124;[-!#\$%'\*\+/=\?\^\`{}\&#124;~\w])*</code>|교체 패턴(마침표가 아닌 문자 또는 여러 문자 중 하나 앞에 마침표가 있는 패턴)을 0번 이상 찾습니다.|  
|`@`|@ 문자를 찾습니다.|  
|`(?<=[0-9a-z])`|@ 문자 앞의 문자가 영문자(A-Z, a-z) 또는 숫자(0-9)인 경우 일치 항목 찾기를 계속합니다. `(?<=[0-9a-z])` 구문은 너비가 0인 긍정 lookbehind 어설션을 정의합니다.|  
|`(?(\[)`|@ 뒤의 문자가 여는 대괄호인지 확인합니다.|  
|`(\[(\d{1,3}\.){3}\d{1,3}\])`|여는 대괄호이면 IP 주소(1자리에서 3자리까지의 숫자로 이루어진 4개의 집합이며 각 집합은 마침표로 구분됨)와 닫는 대괄호 앞에 있는 여는 대괄호를 찾습니다.|  
|<code>&#124;(([0-9a-z][-0-9a-z]*[0-9a-z]*\.)+</code>|@ 뒤의 문자가 여는 대괄호가 아니면 영숫자(A-Z, a-z 또는 0-9) 1개, 하이픈 0개 이상, 영숫자(A-Z, a-z 또는 0-9) 0개 또는 1개와 마침표 1개로 구성된 패턴과 일치하는 항목을 찾습니다. 이 패턴은 한 번 이상 반복될 수 있으며, 뒤에 최상위 도메인 이름이 있어야 합니다.|  
|`[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))`|최상위 도메인 이름은 영숫자(a-z, A-Z 및 0-9)로 시작하고 끝나야 하며, 영숫자이거나 하이픈인 0~22개의 ASCII 문자를 포함할 수도 있습니다.|  
|`$`|문자열의 끝 부분에서 일치 항목 찾기를 끝냅니다.|  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 `IsValidEmail` 및 `DomainMapper` 메서드는 정규식 유틸리티 메서드의 라이브러리에 포함되거나 응용 프로그램 클래스에서 전용 정적 또는 인스턴스 메서드로 포함될 수 있습니다.  
  
 이러한 메서드를 정규식 라이브러리에 포함하려면 코드를 복사한 다음 Visual Studio 클래스 라이브러리 프로젝트에 붙여 넣거나 텍스트 파일에 붙여 넣은 후에 다음과 같은 명령을 사용하여 명령줄에서 컴파일합니다. 여기서는 소스 코드 파일의 이름이 RegexUtilities.cs 또는 RegexUtilities.vb라고 가정합니다.  
  
```csharp  
csc /t:library RegexUtilities.cs  
```  
  
```vb  
vbc /t:library RegexUtilities.vb  
```  
  
 또한 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> 메서드를 사용하여 정규식 라이브러리에 이 정규식을 포함시킬 수 있습니다.  
  
 정규식 라이브러리에 사용될 경우 다음과 같은 코드를 사용하여 호출할 수 있습니다.  
  
 [!code-csharp[RegularExpressions.Examples.Email#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Email/cs/example4.cs#8)]
 [!code-vb[RegularExpressions.Examples.Email#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Email/vb/example4.vb#8)]  
  
 메일 유효성 검사 정규식을 포함하는 클래스 라이브러리 RegexUtilities.dll을 만들었다고 가정할 때 다음 방법 중 하나로 이 예제를 컴파일할 수 있습니다.  
  
-   Visual Studio에서 콘솔 응용 프로그램을 만들고 프로젝트에 RegexUtilities.dll에 대한 참조를 추가합니다.  
  
-   명령줄에서 소스 코드를 복사한 다음 텍스트 파일에 붙여넣고 다음과 같은 명령을 사용하여 컴파일합니다. 이때 소스 코드 파일의 이름이 Example.cs 또는 Example.vb라고 가정합니다.  
  
    ```csharp  
    csc Example.cs /r:RegexUtilities.dll  
    ```  
  
    ```vb  
    vbc Example.vb /r:RegexUtilities.dll  
    ```  
  
## <a name="see-also"></a>참고 항목

- [.NET Framework 정규식](../../../docs/standard/base-types/regular-expressions.md)
