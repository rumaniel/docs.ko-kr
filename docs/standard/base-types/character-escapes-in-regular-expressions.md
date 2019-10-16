---
title: .NET 정규식의 문자 이스케이프
description: .NET 정규식에서 특수 문자 및 이스케이프된 문자에 대해 알아봅니다.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- unescaped characters
- replacement patterns
- characters, escapes
- regular expressions, character escapes
- escape characters
- .NET Framework regular expressions, character escapes
- constructs, character escapes
ms.assetid: f49cc9cc-db7d-4058-8b8a-422bc08b29b0
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 248d434f7aad56d84d952fa27cf49f3d370f4a1c
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "69934825"
---
# <a name="character-escapes-in-regular-expressions"></a>정규식의 문자 이스케이프
정규식의 백슬래시(\\)는 다음 중 하나를 나타냅니다.  
  
- 다음 섹션의 표에 나와 있는 대로 뒤에 나오는 문자는 특수 문자입니다. 예를 들어 `\b`는 단어 경계에서 정규식 일치가 시작되어야 함을 나타내는 앵커이고, `\t`는 탭을 나타내고, `\x020`은 공백을 나타냅니다.  
  
- 이스케이프되지 않은 언어 구문으로 해석되는 문자는 문자 그대로 해석되어야 합니다. 예를 들어 중괄호(`{`)는 수량자 정의를 시작하지만 중괄호 뒤에 백슬래시가 있으면(`\{`) 정규식 엔진이 중괄호와 일치해야 함을 나타냅니다. 마찬가지로 단일 백슬래시는 이스케이프된 언어 구문의 시작을 표시하지만, 이중 백슬래시(`\\`)는 정규식 엔진이 백슬래시와 일치해야 함을 나타냅니다.  
  
> [!NOTE]
> 문자 이스케이프는 정규식 패턴에서는 인식되지만 대체 패턴에서 인식되지 않습니다.  
  
## <a name="character-escapes-in-net"></a>.NET의 문자 이스케이프  
 다음 표에서는 .NET의 정규식에서 지원하는 문자 이스케이프를 보여 줍니다.  
  
|문자 또는 시퀀스|설명|  
|---------------------------|-----------------|  
|다음을 제외한 모든 문자입니다.<br /><br /> 을 선택합니다. $ ^ { [ ( &#124; ) * + ? \ |**문자 또는 시퀀스** 열에 나열된 문자 이외의 문자는 정규식에서 특별한 의미를 가지지 않습니다. 문자 그대로 해석됩니다.<br /><br /> **문자 또는 시퀀스** 열에 포함된 문자는 특수 정규식 언어 요소입니다. 정규식에서 이들 문자를 찾으려면 문자를 이스케이프하거나 [긍정 문자 그룹](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)에 포함해야 합니다. 예를 들어 정규식 `\$\d+` 또는 `[$]\d+`는 "$1200"을 찾습니다.|  
|`\a`|벨 문자인 `\u0007`을 찾습니다.|  
|`\b`|`[`*character_group*`]` 문자 클래스에서 백스페이스 문자인 `\u0008`을 찾습니다.  [문자 클래스](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)를 참조하세요. 문자 클래스 이외에 `\b`는 단어 경계와 일치하는 앵커입니다. [앵커](../../../docs/standard/base-types/anchors-in-regular-expressions.md)를 참조하세요.|  
|`\t`|탭 문자인 `\u0009`를 찾습니다.|  
|`\r`|캐리지 리턴 문자인 `\u000D`를 찾습니다. `\r`은 줄 바꿈 문자인 `\n`과 다릅니다.|  
|`\v`|세로 탭 문자인 `\u000B`를 찾습니다.|  
|`\f`|용지 공급 문자인 `\u000C`를 찾습니다.|  
|`\n`|줄 바꿈 문자인 `\u000A`를 찾습니다.|  
|`\e`|이스케이프 문자인 `\u001B`를 찾습니다.|  
|`\` *nnn*|ASCII 문자를 찾습니다. 여기서 *nnn*은 8진수 문자 코드를 나타내는 두 자리 또는 세 자리 숫자로 구성됩니다. 예를 들어 `\040`은 공백 문자를 나타냅니다. 이 생성자가 한 개의 숫자만 포함하거나(예: `\2`) 캡처링 그룹의 수와 일치하는 경우에는 역참조로 해석됩니다. [역참조 구문](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md)을 참조하세요.|  
|`\x` *nn*|ASCII 문자를 찾습니다. 여기서 *nn*은 두 자리 16진수 문자 코드입니다.|  
|`\c` *X*|ASCII 제어 문자를 찾습니다. 여기서 X는 제어 문자를 나타내는 문자입니다. 예를 들어, `\cC`는 CTRL-C입니다.|  
|`\u` *nnnn*|단위 값이 *nnnn* 16진수인 UTF-16 코드 단위를 찾습니다. **참고:**  유니코드를 지정하는 데 사용되는 Perl 5 문자 이스케이프는 .NET에서 지원되지 않습니다. Perl 5 문자 이스케이프는 `\x{` *####* `…}` 형식입니다. 여기서 *####* `…`는 일련의 16진수입니다. 대신에 `\u`*nnnn*을 사용합니다.|  
|`\`|이스케이프된 문자로 인식되지 않는 문자가 뒤에 나올 경우 이 문자를 찾습니다. 예를 들어 `\*`는 별표(*)와 일치하고 `\x2A`와 같습니다.|  
  
## <a name="an-example"></a>예제  
 다음 예제에서는 정규식에서 문자 이스케이프를 사용하는 방법을 보여 줍니다. 세계 최대 도시의 이름과 2009년 인구가 포함된 문자열을 구문 분석합니다. 각 도시 이름과 해당 인구는 탭(`\t`) 또는 세로 막대(&#124; 또는 `\u007c`)로 구분됩니다. 개별 도시 및 해당 인구는 캐리지 리턴 및 줄 바꿈으로 서로 구분됩니다.  
  
 [!code-csharp[RegularExpressions.Language.Escapes#1](../../../samples/snippets/csharp/VS_Snippets_CLR/regularexpressions.language.escapes/cs/escape1.cs#1)]
 [!code-vb[RegularExpressions.Language.Escapes#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/regularexpressions.language.escapes/vb/escape1.vb#1)]  
  
 정규식 `\G(.+)[\t|\u007c](.+)\r?\n` 는 다음 테이블과 같이 해석됩니다.  
  
|무늬|설명|  
|-------------|-----------------|  
|`\G`|마지막 일치가 종료되면 일치를 시작합니다.|  
|`(.+)`|임의 문자를 한 번 이상 찾습니다. 이 그룹은 첫 번째 캡처링 그룹입니다.|  
|`[\t\u007c]`|탭 문자(`\t`) 또는 세로 막대(&#124;)를 찾습니다.|  
|`(.+)`|임의 문자를 한 번 이상 찾습니다. 이 그룹은 두 번째 캡처링 그룹입니다.|  
|`\r?\n`|캐리지 리턴, 줄 바꿈이 차례로 나타나는 발생 0개 또는 1개를 찾습니다.|  
  
## <a name="see-also"></a>참고 항목

- [정규식 언어 - 빠른 참조](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
