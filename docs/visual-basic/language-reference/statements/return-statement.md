---
title: Return 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Return
helpviewer_keywords:
- Return statement [Visual Basic], syntax
- control flow [Visual Basic], returning control to expressions
- Return statement [Visual Basic]
- expressions [Visual Basic], returning control to
ms.assetid: ac86e7f0-5a67-42c3-9834-0e0381efa3ec
ms.openlocfilehash: af49ea95d7f9d01072190ac3ccf6ba2f1041347e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957667"
---
# <a name="return-statement-visual-basic"></a>Return 문(Visual Basic)
`Function` ,`Sub`, ,`Set`또는 프로시저`Operator` 를 호출한 코드로 제어를 반환 합니다. `Get`  
  
## <a name="syntax"></a>구문  
  
```  
Return  
-or-  
Return expression  
```  
  
## <a name="part"></a>부분  
 `expression`  
 `Function` ,`Get`또는 프로시저`Operator` 에 필요 합니다. 호출 코드에 반환 될 값을 나타내는 식입니다.  
  
## <a name="remarks"></a>설명  
 `Sub` 또는 프로시저에서`Return` 문은 `Exit Sub` 또는`expression` 문과 같으며 제공`Exit Property` 되지 않아야 합니다. `Set`  
  
 `Function`, 또는프로시저`Operator` 에서 문은를 포함`expression`해야 하며`expression` , 프로시저의 반환 형식으로 변환할 수 있는 데이터 형식으로 계산 되어야 합니다. `Return` `Get` 또는 프로시저에서 프로시저 이름에 식을 할당 하 여 반환 값으로 사용 하 고 `Exit Function` 또는 `Exit Property` 문을 실행 하는 방법도 있습니다. `Get` `Function` 프로시저에서를 사용 `Return expression`해야 합니다. `Operator`  
  
 동일한 프로시저에 적절 한 `Return` 수의 문을 포함할 수 있습니다.  
  
> [!NOTE]
> `Finally` 블록의 코드는 `Try` 또는 `Return` `Return` 블록의 문이 발견 된 후에 실행 되며 해당 문이 실행 되기 전에 실행 됩니다. `Catch` `Return` 문은 블록`Finally` 에 포함 될 수 없습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Return` 문을 여러 번 사용 하 여 프로시저에서 다른 작업을 수행할 필요가 없을 때 호출 코드로 돌아갑니다.  
  
 [!code-vb[VbVbalrStatements#53](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#53)]  
  
## <a name="see-also"></a>참고자료

- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Get 문](../../../visual-basic/language-reference/statements/get-statement.md)
- [Set 문](../../../visual-basic/language-reference/statements/set-statement.md)
- [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [Exit 문](../../../visual-basic/language-reference/statements/exit-statement.md)
- [Try...Catch...Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
