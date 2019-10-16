---
title: '#Const 지시문 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.#Const
- '#vb.Const'
- '#Const'
helpviewer_keywords:
- '#Const directive'
- conditional compilation [Visual Basic], directives
- Const directive (#Const)
- Visual Basic compiler, compiler directives
- constants [Visual Basic], Const directive
- constants [Visual Basic], declaring
- Const statement [Visual Basic], directive (#Const)
- 'declaring constants [Visual Basic], #const directive'
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
ms.openlocfilehash: 9b8d2da2158a8244b4533eb6ef49049949417216
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696848"
---
# <a name="const-directive"></a>#Const 지시문
Visual Basic에 대 한 조건부 컴파일러 상수를 정의 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
#Const constname = expression  
```  
  
## <a name="parts"></a>요소  
 `constname`  
 필수. 정의 되는 상수의 이름입니다.  
  
 `expression`  
 필수. 리터럴, 기타 조건부 컴파일러 상수 또는 `Is`을 제외한 모든 산술 연산자 또는 논리 연산자를 포함 하는 모든 조합입니다.  
  
## <a name="remarks"></a>설명  
 조건부 컴파일러 상수는 항상 표시 되는 파일에 대해 private입니다. @No__t-0 지시어를 사용 하 여 공용 컴파일러 상수를 만들 수 없습니다. 사용자 인터페이스나 `/define` 컴파일러 옵션을 사용 하 여 만들 수 있습니다.  
  
 @No__t-0에서 조건부 컴파일러 상수 및 리터럴만 사용할 수 있습니다. @No__t-0으로 정의 된 표준 상수를 사용 하면 오류가 발생 합니다. 반대로 `#Const` 키워드로 정의 된 상수는 조건부 컴파일에만 사용할 수 있습니다. 상수는 정의 되지 않을 수도 있으며,이 경우 값 `Nothing`이 됩니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 `#Const` 지시문을 사용합니다.  
  
 [!code-vb[VbVbalrConditionalComp#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>참조

- [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
- [#If...Then...#Else 지시문](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [Const 문](../../../visual-basic/language-reference/statements/const-statement.md)
- [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [If...Then...Else 문](../../../visual-basic/language-reference/statements/if-then-else-statement.md)
