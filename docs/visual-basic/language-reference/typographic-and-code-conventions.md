---
title: 글꼴 표시 및 코드 규칙(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions [Visual Basic], Visual Basic
- best practices [Visual Basic], coding conventions
- conventions [Visual Basic], Visual Basic coding
- typographic conventions [Visual Basic]
- document conventions [Visual Basic]
- conventions [Visual Basic], documentation
- Visual Basic code, conventions
ms.assetid: 1916cd81-ea9d-4faa-81f7-4a0d864b60f4
ms.openlocfilehash: 3255dff8268cd5500a1244716f37bf30f5b43cfb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61698605"
---
# <a name="typographic-and-code-conventions-visual-basic"></a>글꼴 표시 및 코드 규칙(Visual Basic)
Visual Basic 설명서에는 다음 글꼴 표시 및 코드 규칙에 사용합니다.  
  
## <a name="typographic-conventions"></a>글꼴 표시 규칙  
  
|예제|설명|  
|-------------|-----------------|  
|`Sub`, `If`, `ChDir`, `Print`, `True`, `Debug`|언어별 키워드 및 런타임 멤버 첫 문자가 대문자 있고이 예제와 같이 서식이 지정 됩니다.|  
|**SmallProject**, **ButtonCollection**|단어 및 구를 입력 하 라는 메시지가 표시 되는이 예제와 같이 서식이 지정 됩니다.|  
|[Module 문](../../visual-basic/language-reference/statements/module-statement.md)|클릭 하 여 다른 도움말 페이지로 이동할 수 있습니다 링크에는이 예와 같이 서식이 지정 됩니다.|  
|*object*, *variableName*, `argumentList`|사용자가 제공한 정보에 대 한 자리 표시자에는이 예제와 같이 서식이 지정 됩니다.|  
|[ Shadows ], [ *expressionList* ]|구문에서 선택적 항목이 대괄호로 묶입니다.|  
|{ `Public` &#124; `Friend` &#124; `Private` }|구문에서 두 개 이상 항목 중 하나를 선택 해야 하는 경우는 중괄호로 묶인 항목과 세로 막대로 구분 합니다.<br /><br /> 항목 하나를 한 개만 선택 해야 합니다.|  
|[ `Protected` &#124; `Friend` ]|구문에서 간에 두 개 이상의 항목을 선택 하는 옵션을 사용 하는 경우는 대괄호로 항목과 세로 막대로 구분 합니다.<br /><br /> 항목의 조합이 나 항목이 없으면 선택할 수 있습니다.|  
|[{ `ByVal` &#124; `ByRef` }]|구문에서 둘 이상의 항목을 선택할 수 있지만 항목을 완전히 생략할 수도 있습니다 항목은 대괄호로 중괄호로 묶은 및 세로 막대로 구분 합니다.|  
|*memberName*1, *memberName*2, *memberName*3|예제에 표시 된 대로 아래 첨자, 여러 인스턴스는 같은 자리 표시자 구분 됩니다.|  
|*memberName1*<br /><br /> ...<br /><br /> *memberNameN*|줄임표 (...)는 구문에서 불특정 개수의 줄임표 앞에 즉시 종류의 항목을 나타내는 데 사용 됩니다.<br /><br /> 코드에서 줄임표는 명확한 설명을 위해 생략 하는 코드를 의미 합니다.|  
|ESC 키를 입력|키 이름 및 바로 가기 키 시퀀스가 모두 대문자로 표시 합니다.|  
|ALT + F1|더하기 기호 (+) 키 이름 사이 표시 되 면 다른를 누른 채 하나의 키를 누른 해야 있습니다. 예를 들어, ALT + F1은 F1 키를 누르거나 ALT 키를 누른을 의미 합니다.|  
  
## <a name="code-conventions"></a>코드 규칙  
  
|예제|설명|  
|-------------|-----------------|  
|`sampleString = "Hello, world!"`|코드 샘플을 고정 폭 글꼴에 나타나고이 예제와 같이 서식이 지정 됩니다.|  
|값을 설정 하는 이전 문을 `sampleString` 에 "Hello, world!"|이 예제에 표시 된 대로 설명 텍스트의 코드 요소에 고정 폭 글꼴을에 나타납니다.|  
|`' This is a comment.`<br /><br /> `REM This is also a comment.`|코드 주석 아포스트로피 (') 또는 REM 키워드에서 도입 되었습니다.|  
|`sampleVar = "This is an " _`<br /><br /> `& "example" _`<br /><br /> `& " of how to continue code."`|밑줄 (_) 줄의 끝에 공백을 문에 다음 줄에서 계속 됨을 나타냅니다.|  
  
## <a name="see-also"></a>참고자료

- [Visual Basic 언어 참조](../../visual-basic/language-reference/index.md)
- [C++ 키워드](../../visual-basic/language-reference/keywords/index.md)
- [Visual Basic 런타임 라이브러리 멤버](../../visual-basic/language-reference/runtime-library-members.md)
- [Visual Basic 명명 규칙](../../visual-basic/programming-guide/program-structure/naming-conventions.md)
- [방법: 코드에서 문 분리 및 결합](../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
- [코드 주석](../../visual-basic/programming-guide/program-structure/comments-in-code.md)
