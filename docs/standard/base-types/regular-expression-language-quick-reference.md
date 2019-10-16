---
title: 정규식 언어 - 빠른 참조
ms.date: 03/30/2017
ms.technology: dotnet-standard
f1_keywords:
- VS.RegularExpressionBuilder
helpviewer_keywords:
- regex cheat sheet
- parsing text with regular expressions, language elements
- searching with regular expressions, language elements
- pattern-matching with regular expressions, language elements
- regular expressions, language elements
- regular expressions [.NET Framework]
- cheat sheet
- .NET Framework regular expressions, language elements
ms.assetid: 930653a6-95d2-4697-9d5a-52d11bb6fd4c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 053df7eeba10938f1d1d749e856f64d179d471d4
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "64664671"
---
# <a name="regular-expression-language---quick-reference"></a>정규식 언어 - 빠른 참조
 정규식은 정규식 엔진이 입력 텍스트에서 찾으려고 하는 패턴입니다. 패턴은 하나 이상의 문자 리터럴, 연산자 또는 구문으로 구성됩니다.  간략하게 살펴보려면 [.NET 정규식](../../../docs/standard/base-types/regular-expressions.md)을 참조하세요.  
  
 이 빠른 참조의 각 단원에서는 정규식을 정의하는 데 사용할 수 있는 특정 범주의 문자, 연산자 및 구문을 보여줍니다.  
  
 또한 쉽게 참조할 수 있도록 다운로드 및 인쇄할 수 있는 다음과 같은 두 가지 형식으로 이 정보를 제공했습니다.  
  
 [Word(.docx) 형식으로 다운로드](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)  
 [PDF(.pdf) 형식으로 다운로드](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)  
  
## <a name="character-escapes"></a>문자 이스케이프  
 정규식의 백슬래시 문자(\\)는 뒤에 오는 문자가 다음 표에 나와 있는 것과 같은 특수 문자이거나 리터럴로 해석되어야 함을 나타냅니다. 자세한 내용은 [문자 이스케이프](../../../docs/standard/base-types/character-escapes-in-regular-expressions.md)를 참조하세요.  
  
|이스케이프된 문자|설명|무늬|일치 항목|  
|-----------------------|-----------------|-------------|-------------|  
|`\a`|벨 문자인 \u0007을 찾습니다.|`\a`|`"Error!" + '\u0007'`의 `"\u0007"`|  
|`\b`|문자 클래스에서 백스페이스 문자인 \u0008을 찾습니다.|`[\b]{3,}`|`"\b\b\b\b"`의 `"\b\b\b\b"`|  
|`\t`|탭 문자인 \u0009를 찾습니다.|`(\w+)\t`|`"item1\titem2\t"`의 `"item1\t"`, `"item2\t"`|  
|`\r`|캐리지 리턴 문자인 \u000D를 찾습니다. (`\r`은 줄 바꿈 문자인 `\n`과 다릅니다.)|`\r\n(\w+)`|`"\r\nThese are\ntwo lines."`의 `"\r\nThese"`|  
|`\v`|세로 탭 문자인 \u000B를 찾습니다.|`[\v]{2,}`|`"\v\v\v"`의 `"\v\v\v"`|  
|`\f`|용지 공급 문자인 \u000C를 찾습니다.|`[\f]{2,}`|`"\f\f\f"`의 `"\f\f\f"`|  
|`\n`|줄 바꿈 문자인 \u000A를 찾습니다.|`\r\n(\w+)`|`"\r\nThese are\ntwo lines."`의 `"\r\nThese"`|  
|`\e`|이스케이프 문자인 \u001B를 찾습니다.|`\e`|`"\x001B"`의 `"\x001B"`|  
|`\` *nnn*|8진수 표현을 사용하여 문자를 지정합니다. (*nnn*은 두 자리 또는 세 자리로 구성됩니다.)|`\w\040\w`|`"a bc d"`의 `"a b"`, `"c d"`|  
|`\x` *nn*|16진수 표현을 사용하여 문자를 지정합니다. (*nn*은 정확히 두 자리로 구성됩니다.)|`\w\x20\w`|`"a bc d"`의 `"a b"`, `"c d"`|  
|`\c` *X*<br /><br /> `\c` *x*|*X* 또는 *x*로 지정한 ASCII 제어 문자를 찾습니다. 여기서 *X* 또는 *x*는 제어 문자를 나타내는 문자입니다.|`\cC`|`"\x0003"`의 `"\x0003"`(Ctrl-C)|  
|`\u` *nnnn*|16진수 표현(정확히 네 자리로 구성되는 *nnnn*)을 사용하여 유니코드 문자를 찾습니다.|`\w\u0020\w`|`"a bc d"`의 `"a b"`, `"c d"`|  
|`\`|이 표나 이 항목의 다른 표에 있는 이스케이프된 문자로 인식되지 않는 문자가 뒤에 나올 경우 이 문자를 찾습니다. 예를 들어, `\*`는 `\x2A`와 같고 `\.`는 `\x2E`와 같습니다. 이를 통해 정규식 엔진이 언어 요소(예: \* 또는 ?)와 `\*` 또는 `\?`로 표현되는 문자 리터럴을 구분할 수 있습니다.|`\d+[\+-x\*]\d+`|`"(2+2) * 3*9"`의 `"2+2"` 및 `"3*9"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="character-classes"></a>문자 클래스  
 문자 클래스는 문자 집합 중 하나를 찾습니다. 문자 클래스에는 다음 표에 나와 있는 언어 요소가 포함됩니다. 자세한 내용은 [문자 클래스](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)를 참조하세요.  
  
|문자 클래스|설명|무늬|일치 항목|  
|---------------------|-----------------|-------------|-------------|  
|`[` *character_group* `]`|*character_group*에서 단일 문자를 찾습니다. 기본적으로 일치 항목 찾기에서는 대/소문자를 구분합니다.|`[ae]`|`"gray"`의 `"a"`<br /><br /> `"lane"`의 `"a"`, `"e"`|  
|`[^` *character_group* `]`|부정: *character_group*에 없는 모든 단일 문자를 찾습니다. 기본적으로 *character_group*의 문자는 대/소문자를 구분합니다.|`[^aei]`|`"reign"`의 `"r"`, `"g"`, `"n"`|  
|`[` *first* `-` *last* `]`|문자 범위: *first*에서 *last* 사이에 있는 모든 단일 문자를 찾습니다.|`[A-Z]`|`"AB123"`의 `"A"`, `"B"`|  
|`.`|와일드카드: \n 이외의 모든 단일 문자를 찾습니다.<br /><br /> 리터럴 마침표 문자(. 또는 `\u002E`)를 찾으려면 마침표 문자 앞에 이스케이프 문자를 추가해야 합니다(`\.`).|`a.e`|`"nave"`의 `"ave"`<br /><br /> `"water"`의 `"ate"`|  
|`\p{` *name* `}`|유니코드 일반 범주나 *name*으로 지정된 명명된 블록에 있는 모든 단일 문자를 찾습니다.|`\p{Lu}`<br /><br /> `\p{IsCyrillic}`|`"City Lights"`의 `"C"`, `"L"`<br /><br /> `"ДЖem"`의 `"Д"`, `"Ж"`|  
|`\P{` *name* `}`|유니코드 일반 범주나 *name*으로 지정된 명명된 블록에 없는 모든 단일 문자를 찾습니다.|`\P{Lu}`<br /><br /> `\P{IsCyrillic}`|`"City"`의 `"i"`, `"t"`, `"y"`<br /><br /> `"ДЖem"`의 `"e"`, `"m"`|  
|`\w`|단어 문자를 찾습니다.|`\w`|`"ID A1.3"`의 `"I"`, `"D"`, `"A"`, `"1"`, `"3"`|  
|`\W`|비단어 문자를 찾습니다.|`\W`|`"ID A1.3"`의 `" "`, `"."`|  
|`\s`|공백 문자를 나타냅니다.|`\w\s`|`"ID A1.3"`의 `"D "`|  
|`\S`|공백 문자가 아닌 문자를 찾습니다.|`\s\S`|`"int __ctr"`의 `" _"`|  
|`\d`|10진수를 찾습니다.|`\d`|`"4 = IV"`의 `"4"`|  
|`\D`|10진수 이외의 모든 문자를 찾습니다.|`\D`|`"4 = IV"`의 `" "`, `"="`, `" "`, `"I"`, `"V"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="anchors"></a>앵커  
 앵커 또는 너비가 0인 원자적 어설션은 문자열에서 일치 항목의 현재 위치에 따라 일치의 성공 또는 실패 여부를 결정하지만 엔진에서 문자열을 따라 가거나 문자를 소비하도록 하지는 않습니다. 다음 표에 나와 있는 메타문자는 앵커입니다. 자세한 내용은 [앵커](../../../docs/standard/base-types/anchors-in-regular-expressions.md)를 참조하세요.  
  
|어설션|설명|무늬|일치 항목|  
|---------------|-----------------|-------------|-------------|  
|`^`|기본적으로 일치 항목은 문자열의 시작 부분에서 시작되어야 합니다. 다중 선에서는 줄의 시작 부분에서 시작되어야 합니다.|`^\d{3}`|`"901-333-"`의 `"901"`|  
|`$`|기본적으로 일치 항목은 문자열의 끝부분 또는 문자열의 끝부분 `\n` 앞에서 발생해야 합니다. 다중 선에서는 줄의 끝부분 또는 줄의 끝 `\n` 앞에서 발생해야 합니다.|`-\d{3}$`|`"-901-333"`의 `"-333"`|  
|`\A`|일치 항목이 문자열의 시작 부분에 있어야 합니다.|`\A\d{3}`|`"901-333-"`의 `"901"`|  
|`\Z`|일치 항목이 문자열의 끝이나 문자열의 끝에 있는 `\n` 앞에 있어야 합니다.|`-\d{3}\Z`|`"-901-333"`의 `"-333"`|  
|`\z`|일치 항목이 문자열의 끝에 있어야 합니다.|`-\d{3}\z`|`"-901-333"`의 `"-333"`|  
|`\G`|일치 항목이 이전 일치 항목 찾기가 끝난 지점에 있어야 합니다.|`\G\(\d\)`|`"(1)(3)(5)[7](9)"`의 `"(1)"`, `"(3)"`, `"(5)"`|  
|`\b`|일치 항목이 `\w`(영숫자) 문자와 `\W`(영숫자가 아닌 문자) 문자 사이의 경계에 있어야 합니다.|`\b\w+\s\w+\b`|`"them theme them them"`의 `"them theme"`, `"them them"`|  
|`\B`|일치 항목이 `\b` 경계에 있어야 합니다.|`\Bend\w*\b`|`"end sends endure lender"`의 `"ends"`, `"ender"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="grouping-constructs"></a>그룹화 구문  
 그룹화 구문은 정규식의 하위 식을 나타내며 대개 입력 문자열의 부분 문자열을 캡처합니다. 그룹화 구문에는 다음 표에 나와 있는 언어 요소가 포함됩니다. 자세한 내용은 [그룹화 구문](grouping-constructs-in-regular-expressions.md)을 참조하세요.  
  
|그룹화 구문|설명|무늬|일치 항목|  
|------------------------|-----------------|-------------|-------------|  
|`(` *subexpression* `)`|일치하는 하위 식을 캡처하고 서수(1부터 시작)를 할당합니다.|`(\w)\1`|`"deep"`의 `"ee"`|  
|`(?<` *name* `>` *subexpression* `)`|일치하는 하위 식을 명령된 그룹에 캡처합니다.|`(?<double>\w)\k<double>`|`"deep"`의 `"ee"`|  
|`(?<` *이름1* `-` *이름2* `>` *subexpression* `)`|균형 조정 그룹 정의를 정의합니다. 자세한 내용은 [그룹화 구문](grouping-constructs-in-regular-expressions.md)의 "균형 조정 그룹 정의" 섹션을 참조하세요.|`(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$`|`"3+2^((1-3)*(3-1))"`의 `"((1-3)*(3-1))"`|  
|`(?:` *subexpression* `)`|비캡처 그룹을 정의합니다.|`Write(?:Line)?`|`"Console.WriteLine()"`의 `"WriteLine"`<br /><br /> `"Console.Write(value)"`의 `"Write"`|  
|`(?imnsx-imnsx:` *subexpression* `)`|*subexpression* 내에서 지정된 옵션을 적용하거나 사용하지 않도록 설정합니다. 자세한 내용은 [정규식 옵션](regular-expression-options.md)을 참조하세요.|`A\d{2}(?i:\w+)\b`|`"A12xl A12XL a12xl"`의 `"A12xl"`, `"A12XL"`|  
|`(?=` *subexpression* `)`|너비가 0인 긍정 우측 어설션입니다.|`\w+(?=\.)`|`"He is. The dog ran. The sun is out."`의 `"is"`, `"ran"` 및 `"out"`|  
|`(?!` *subexpression* `)`|너비가 0인 부정 우측 어설션입니다.|`\b(?!un)\w+\b`|`"unsure sure unity used"`의 `"sure"`, `"used"`|  
|`(?<=` *subexpression* `)`|너비가 0인 긍정 좌측 어설션입니다.|`(?<=19)\d{2}\b`|`"1851 1999 1950 1905 2003"`의 `"99"`, `"50"`, `"05"`|  
|`(?<!` *subexpression* `)`|너비가 0인 부정 좌측 어설션입니다.|`(?<!19)\d{2}\b`|`"1851 1999 1950 1905 2003"`의 `"51"`, `"03"`|  
|`(?>` *subexpression* `)`|역추적하지 않는(또는 "greedy") 하위 식입니다.|`[13579](?>A+B+)`|`"1ABB 3ABBC 5AB 5AC"`의 `"1ABB"`, `"3ABB"` 및 `"5AB"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="quantifiers"></a>수량자  
 수량자는 이전 요소(문자, 그룹 또는 문자 클래스)의 인스턴스가 입력 문자열에 몇 개 있어야 일치 항목으로 간주되는지를 지정합니다. 수량자에는 다음 표에 나와 있는 언어 요소가 포함됩니다. 자세한 내용은 [수량자](quantifiers-in-regular-expressions.md)를 참조하세요.  
  
|수량자|설명|무늬|일치 항목|  
|----------------|-----------------|-------------|-------------|  
|`*`|이전 요소를 0개 이상 찾습니다.|`\d*\.\d`|`".0"`, `"19.9"`, `"219.9"`|  
|`+`|이전 요소를 1개 이상 찾습니다.|`"be+"`|`"been"`의 `"bee"`, `"bent"`의 `"be"`|  
|`?`|이전 요소를 0개 또는 1개 찾습니다.|`"rai?n"`|`"ran"`, `"rain"`|  
|`{` *n* `}`|이전 요소를 정확히 *n* 회 찾습니다.|`",\d{3}"`|`"1,043.6"`의 `",043"`, `"9,876,543,210"`의 `",876"`, `",543"` 및 `",210"`|  
|`{` *n* `,}`|이전 요소를 최소한 *n* 회 찾습니다.|`"\d{2,}"`|`"166"`, `"29"`, `"1930"`|  
|`{` *n* `,` *m* `}`|이전 요소를 *n* 회 이상, *m* 회 이하로 찾습니다.|`"\d{3,5}"`|`"166"`, `"17668"`<br /><br /> `"193024"`의 `"19302"`|  
|`*?`|이전 요소를 0개 이상 가능한 한 적은 개수로 찾습니다.|`\d*?\.\d`|`".0"`, `"19.9"`, `"219.9"`|  
|`+?`|이전 요소를 1개 이상 가능한 한 적은 개수로 찾습니다.|`"be+?"`|`"been"`의 `"be"`, `"bent"`의 `"be"`|  
|`??`|이전 요소를 가능한 한 적은 개수로 0개 또는 1개 찾습니다.|`"rai??n"`|`"ran"`, `"rain"`|  
|`{` *n* `}?`|이전 요소를 정확히 *n* 회 찾습니다.|`",\d{3}?"`|`"1,043.6"`의 `",043"`, `"9,876,543,210"`의 `",876"`, `",543"` 및 `",210"`|  
|`{` *n* `,}?`|이전 요소를 최소한 *n* 회 이상 가능한 한 적은 개수로 찾습니다.|`"\d{2,}?"`|`"166"`, `"29"`, `"1930"`|  
|`{` *n* `,` *m* `}?`|이전 요소를 *n* 회에서 *m* 회 사이에서 찾으며, 가능한 한 적은 개수로 찾습니다.|`"\d{3,5}?"`|`"166"`, `"17668"`<br /><br /> `"193024"`의 `"193"`, `"024"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="backreference-constructs"></a>역참조 구문  
 역참조를 사용하면 이전에 찾은 하위 식을 이후에 동일한 정규식에서 식별할 수 있습니다. 다음 표에서는 .NET의 정규식에서 지원하는 역참조 구문을 보여줍니다. 자세한 내용은 [역참조 구문](backreference-constructs-in-regular-expressions.md)을 참조하세요.  
  
|역참조 구문|설명|무늬|일치 항목|  
|-----------------------------|-----------------|-------------|-------------|  
|`\` *number*|역참조입니다. 번호가 매겨진 하위 식의 값을 찾습니다.|`(\w)\1`|`"seek"`의 `"ee"`|  
|`\k<` *name* `>`|명명된 역참조입니다. 명명된 식의 값을 찾습니다.|`(?<char>\w)\k<char>`|`"seek"`의 `"ee"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="alternation-constructs"></a>교체 구문  
 교체 구문은 일치를 허용하도록 정규식을 수정합니다. 이러한 구문에는 다음 표에 나와 있는 언어 요소가 포함됩니다. 자세한 내용은 [교체 구문](alternation-constructs-in-regular-expressions.md)을 참조하세요.  
  
|교체 구문|설명|무늬|일치 항목|  
|---------------------------|-----------------|-------------|-------------|  
|<code>&#124;</code>|세로 막대(<code>&#124;</code>)로 구분된 한 가지 요소와 일치합니다.|<code>th(e&#124;is&#124;at)</code>|`"this is the day."`의 `"the"`, `"this"`|  
|`(?(` *expression* `)` *yes* <code>&#124;</code> *no* `)`|*expression* 으로 지정한 정규식 패턴이 일치하면 *yes*와 일치합니다. 그렇지 않으면 선택 사항 *no* 부분과 일치합니다. *expression*은 너비가 0인 어설션으로 해석됩니다.|<code>(?(A)A\d{2}\b&#124;\b\d{3}\b)</code>|`"A10 C103 910"`의 `"A10"`, `"910"`|  
|`(?(` *name* `)` *yes* <code>&#124;</code> *no* `)`|명명되거나 번호가 매겨진 캡처링 그룹인 *name*에 일치하는 항목이 있으면 *yes*와 일치합니다. 그렇지 않으면 선택 사항 *no*와 일치합니다.|<code>(?&lt;quoted&gt;&quot;)?(?(quoted).+?&quot;&#124;\S+\s)</code>|`"Dogs.jpg \"Yiska playing.jpg\""`의 `"Dogs.jpg "`, `"\"Yiska playing.jpg\""`|  
  
 [맨 위로 이동](#top)  
  
## <a name="substitutions"></a>대체  
 대체는 바꾸기 패턴에서 지원하는 정규식 언어 요소입니다. 자세한 내용은 [대체](substitutions-in-regular-expressions.md)를 참조하세요. 다음 표에 나와 있는 메타문자는 너비가 0인 원자성 어설션입니다.  
  
|문자|설명|무늬|바꾸기 패턴|입력 문자열|결과 문자열|  
|---------------|-----------------|-------------|-------------------------|------------------|-------------------|  
|`$` *number*|그룹 *number*와 일치하는 부분 문자열을 대체합니다.|`\b(\w+)(\s)(\w+)\b`|`$3$2$1`|`"one two"`|`"two one"`|  
|`${` *name* `}`|명명된 그룹 *name*과 일치하는 부분 문자열을 대체합니다.|`\b(?<word1>\w+)(\s)(?<word2>\w+)\b`|`${word2} ${word1}`|`"one two"`|`"two one"`|  
|`$$`|"$" 리터럴을 대체합니다.|`\b(\d+)\s?USD`|`$$$1`|`"103 USD"`|`"$103"`|  
|`$&`|일치하는 전체 문자열의 복사본을 대체합니다.|`\$?\d*\.?\d+`|`**$&**`|`"$1.30"`|`"**$1.30**"`|  
|``$` ``|일치하는 문자열 앞에 있는 입력 문자열의 모든 텍스트를 대체합니다.|`B+`|``$` ``|`"AABBCC"`|`"AAAACC"`|  
|`$'`|일치하는 문자열 뒤에 있는 입력 문자열의 모든 텍스트를 대체합니다.|`B+`|`$'`|`"AABBCC"`|`"AACCCC"`|  
|`$+`|캡처된 마지막 그룹을 대체합니다.|`B+(C+)`|`$+`|`"AABBCCDD"`|`"AACCDD"`|  
|`$_`|전체 입력 문자열을 대체합니다.|`B+`|`$_`|`"AABBCC"`|`"AAAABBCCCC"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="regular-expression-options"></a>정규식 옵션  
 정규식 엔진이 정규식 패턴을 해석하는 방법을 제어하는 옵션을 지정할 수 있습니다. 옵션의 대부분은 인라인(정규식 패턴)에서 또는 1개 이상의 <xref:System.Text.RegularExpressions.RegexOptions> 상수로 지정될 수 있습니다. 이 빠른 참조는 인라인 옵션만 나열합니다. 인라인 및 <xref:System.Text.RegularExpressions.RegexOptions> 옵션에 대한 자세한 내용은 [Regular Expression Options](regular-expression-options.md)를 참조하세요.  
  
 인라인 옵션을 두 가지 방법으로 지정할 수 있습니다.  
  
- [기타 구문](miscellaneous-constructs-in-regular-expressions.md) `(?imnsx-imnsx)`을 사용하여 옵션이나 옵션 집합 앞에 빼기 기호(-)를 추가해 해당 옵션을 해제할 수 있습니다. 예를 들어 `(?i-mn)`은 대/소문자를 구분하지 않는 일치 조건(`i`)을 설정하고 여러 줄 모드(`m`)를 해제하고 명명되지 않은 그룹 캡처(`n`)를 해제합니다. 이 옵션은 옵션이 정의되는 지점부터 정규식 패턴에 적용되고, 패턴 끝 또는 다른 구문이 옵션을 되돌리는 지점까지 유효합니다.  
  
- [그룹화 구문](grouping-constructs-in-regular-expressions.md)`(?imnsx-imnsx:`*subexpression*`)`을 사용하여 지정된 그룹에 대해서만 옵션을 정의할 수 있습니다.  
  
 .NET 정규식 엔진은 다음 인라인 옵션을 지원합니다.  
  
|옵션|설명|무늬|일치 항목|  
|------------|-----------------|-------------|-------------|  
|`i`|대/소문자를 구분하지 않는 일치를 사용합니다.|`\b(?i)a(?-i)a\w+\b`|`"aardvark AAAuto aaaAuto Adam breakfast"`의 `"aardvark"`, `"aaaAuto"`|  
|`m`|여러 줄 모드를 사용합니다. `^` 및 `$`는 각 줄의 시작 및 끝과 일치합니다(문자열의 시작 및 끝이 아님).|예제를 보려면 [정규식 옵션](regular-expression-options.md)에서 "여러 줄 모드" 섹션을 참조하세요.||  
|`n`|명명되지 않은 그룹을 캡처하지 않습니다.|예를 들어 [정규식 옵션](regular-expression-options.md)에서 "명시적 캡처만 해당" 섹션을 참조하세요.||  
|`s`|한 줄 모드를 사용합니다.|예제를 보려면 [정규식 옵션](regular-expression-options.md)에서 "한 줄 모드" 섹션을 참조하세요.||  
|`x`|정규식 패턴에서 이스케이프되지 않은 공백은 무시합니다.|`\b(?x) \d+ \s \w+`|`"1 aardvark 2 cats IV centurions"`의 `"1 aardvark"`, `"2 cats"`|  
  
 [맨 위로 이동](#top)  
  
## <a name="miscellaneous-constructs"></a>기타 구문  
 기타 구문은 정규식 패턴을 수정하거나 정규식 패턴에 대한 정보를 제공합니다. 다음 표에서는 .NET에서 지원하는 기타 구문을 보여줍니다. 자세한 내용은 [기타 구문](miscellaneous-constructs-in-regular-expressions.md)을 참조하세요.  
  
|구문|정의|예제|  
|---------------|----------------|-------------|  
|`(?imnsx-imnsx)`|패턴 중간에 대/소문자 구분하지 않음과 같은 옵션을 설정하거나 해제합니다. 자세한 내용은 [정규식 옵션](regular-expression-options.md)을 참조하세요.|`\bA(?i)b\w+\b`는 `"ABA Able Act"`의 `"ABA"`, `"Able"`과 일치합니다.|  
|`(?#` *주석* `)`|인라인 주석입니다. 주석이 첫 번째 닫는 괄호 문자에서 끝납니다.|`\bA(?#Matches words starting with A)\w+\b`|  
|`#` [줄의 끝]|X-모드 주석입니다. 주석이 이스케이프되지 않은 `#`에서 시작하여 줄 끝까지 이어집니다.|`(?x)\bA\w+\b#Matches words starting with A`|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Text.RegularExpressions?displayProperty=nameWithType>
- <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>
- [정규식](regular-expressions.md)
- [정규식 클래스](the-regular-expression-object-model.md)
- [정규식 예제](regular-expression-examples.md)
- [정규식 - 빠른 참조(Word 형식으로 다운로드)](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
- [정규식 - 빠른 참조(PDF 형식으로 다운로드)](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)
