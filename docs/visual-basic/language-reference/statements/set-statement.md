---
title: Set 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Set
helpviewer_keywords:
- property procedures [Visual Basic], Set statements
- Set statement [Visual Basic]
- Set statement [Visual Basic], syntax
- write-only properties
- properties [Visual Basic], write-only
ms.assetid: 9ecc27b4-df84-420d-9075-db25455fb3cd
ms.openlocfilehash: fb51dfbae4d9c4ef205e67ac15c5027e62a9a938
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64663191"
---
# <a name="set-statement-visual-basic"></a>Set 문(Visual Basic)
선언 된 `Set` 속성 프로시저 속성에 값을 할당 하는 데 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ <attributelist> ] [ accessmodifier ] Set (ByVal value [ As datatype ])  
    [ statements ]  
End Set  
```  
  
## <a name="parts"></a>요소  
 `attributelist`  
 선택 사항입니다. 참조 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)합니다.  
  
 `accessmodifier`  
 옵션 중 하나에 `Get` 및 `Set` 이 속성에는 문. 다음 중 하나일 수 있습니다.  
  
- [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)  
  
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
- [전용](../../../visual-basic/language-reference/modifiers/private.md)  
  
- `Protected Friend`  
  
 [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.  
  
 `value`  
 필수 요소. 속성에 대 한 새 값을 포함 하는 매개 변수입니다.  
  
 `datatype`  
 필요한 경우 `Option Strict` 는 `On`합니다. 데이터 형식의 `value` 매개 변수입니다. 속성의 데이터 형식으로 지정한 데이터 형식과 같아야 여기서이 `Set` 정보가 선언 됩니다.  
  
 `statements`  
 선택 사항입니다. 될 때 실행 되는 하나 이상의 문을 `Set` 속성 프로시저를 호출 합니다.  
  
 `End Set`  
 필수 요소. 정의 종료 합니다 `Set` 속성 프로시저입니다.  
  
## <a name="remarks"></a>설명  
 모든 속성에 있어야 합니다는 `Set` 속성 프로시저 속성 표시 되어 있지 않으면 `ReadOnly`합니다. `Set` 방법을 사용 하는 속성의 값을 설정 합니다.  
  
 Visual Basic로 속성을 자동으로 호출 `Set` 프로시저 대입문 속성에 저장할 수 있는 값을 제공 합니다.  
  
 Visual Basic에 매개 변수를 전달 합니다 `Set` 속성을 할당 하는 동안 프로시저입니다. 매개 변수를 제공 하지 않는 경우 `Set`, 라는 암시적 매개 변수를 사용 하는 통합된 개발 환경 (IDE) `value`합니다. 매개 변수 속성에 할당할 값을 보유 합니다. 일반적으로 개인 로컬 변수에이 값을 저장 하 고 반환할 때마다는 `Get` 프로시저를 호출 합니다.  
  
 속성 선언의 본문에만 속성의 포함 될 수 있습니다 `Get` 하 고 `Set` 프로시저 간의 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md) 및 `End Property` 문. 이러한 프로시저 이외의 저장할 수 없습니다. 특히,이 속성의 현재 값을 저장할 수 없습니다. 다른 속성 프로시저에서 액세스할 수 없으므로 속성 프로시저 중 어디에 저장 하는 경우에 외부 속성을이 값을 저장 해야 합니다. 에 값을 저장 하는 일반적인 방법입니다를 [개인](../../../visual-basic/language-reference/modifiers/private.md) 속성과 동일한 수준에서 선언 된 변수입니다. 정의 해야 합니다는 `Set` 적용 되는 속성 내의 프로시저입니다.  
  
 합니다 `Set` 프로시저는 기본적으로 포함 하는 해당 속성의 액세스 수준을 사용 하지 않는 경우 `accessmodifier` 에 `Set` 문.  
  
## <a name="rules"></a>규칙  
  
- **혼합 된 액세스 수준입니다.** 서로 다른 액세스 수준에 대 한 필요에 따라 지정할 수는 읽기 / 쓰기 속성을 정의 하는 경우는 `Get` 또는 `Set` 절차, 하지만 둘 다. 이 작업을 수행 하는 경우 프로시저 액세스 수준 속성의 액세스 수준 보다 더 제한적 이어야 합니다. 예를 들어, 속성 선언 되 면 `Friend`를 선언할 수 있습니다 합니다 `Set` 프로시저 `Private`, 아닌 `Public`합니다.  
  
     정의 하는 경우는 `WriteOnly` 속성을 `Set` 프로시저 전체 속성을 나타냅니다. 선언할 수 없습니다는 서로 다른 액세스 수준 `Set`이므로 속성에 대 한 두 가지 액세스 수준이 설정 합니다.  
  
## <a name="behavior"></a>동작  
  
- **속성 프로시저에서 반환합니다.** 경우는 `Set` 프로시저가 호출 코드에 반환 되 면 저장 될 값을 제공 하는 문을 계속 실행 합니다.  
  
     `Set` 속성 프로시저 중 하나를 사용 하 여 반환할 수 있습니다 합니다 [Return 문이](../../../visual-basic/language-reference/statements/return-statement.md) 또는 [Exit 문을](../../../visual-basic/language-reference/statements/exit-statement.md)합니다.  
  
     합니다 `Exit Property` 및 `Return` 문은 속성 프로시저를 즉시 종료 합니다. 임의 개수의 `Exit Property` 하 고 `Return` 문을 프로시저에서 아무 곳 이나 나타날 수 있으며 함께 사용할 수 있습니다 `Exit Property` 및 `Return` 문.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Set` 속성의 값을 설정 하는 문입니다.  
  
 [!code-vb[VbVbalrStatements#55](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#55)]  
  
## <a name="see-also"></a>참고자료

- [Get 문](../../../visual-basic/language-reference/statements/get-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [속성 프로시저](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)
