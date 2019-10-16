---
title: Get 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Get
helpviewer_keywords:
- Get statement [Visual Basic], syntax
- Get statement [Visual Basic]
- properties [Visual Basic], read-only
- read-only properties
- Get keyword [Visual Basic]
- property procedures [Visual Basic], Get statements
ms.assetid: 56b05cdc-bd64-4dfd-bb12-824eacec6f94
ms.openlocfilehash: 33fa6811f952d240fb86bbdf59ca83df0afc03ad
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625524"
---
# <a name="get-statement"></a>Get 문
선언 된 `Get` 속성 프로시저는 속성의 값을 검색 하는 데 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ <attributelist> ] [ accessmodifier ] Get()  
    [ statements ]  
End Get  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`attributelist`|선택 사항입니다. 참조 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)합니다.|  
|`accessmodifier`|옵션 중 하나에 `Get` 및 `Set` 이 속성에는 문. 다음 중 하나일 수 있습니다.<br /><br /> -   [보호](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [개인](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.|  
|`statements`|선택 사항입니다. 될 때 실행 되는 하나 이상의 문을 `Get` 속성 프로시저를 호출 합니다.|  
|`End Get`|필수 요소. 정의 종료 합니다 `Get` 속성 프로시저입니다.|  
  
## <a name="remarks"></a>설명  
 모든 속성에 있어야 합니다는 `Get` 속성 프로시저 속성 표시 되어 있지 않으면 `WriteOnly`합니다. `Get` 프로시저는 속성의 현재 값을 반환 하는 데 사용 됩니다.  
  
 Visual Basic로 속성을 자동으로 호출 `Get` 식을 속성의 값을 요청 하는 경우 프로시저입니다.  
  
 속성 선언의 본문에만 속성의 포함 될 수 있습니다 `Get` 하 고 `Set` 프로시저 간의 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md) 및 `End Property` 문. 이러한 프로시저 이외의 저장할 수 없습니다. 특히,이 속성의 현재 값을 저장할 수 없습니다. 다른 속성 프로시저에서 액세스할 수 없으므로 속성 프로시저 중 어디에 저장 하는 경우에 외부 속성을이 값을 저장 해야 합니다. 에 값을 저장 하는 일반적인 방법입니다를 [개인](../../../visual-basic/language-reference/modifiers/private.md) 속성과 동일한 수준에서 선언 된 변수입니다. 정의 해야 합니다는 `Get` 적용 되는 속성 내의 프로시저입니다.  
  
 합니다 `Get` 프로시저는 기본적으로 포함 하는 해당 속성의 액세스 수준을 사용 하지 않는 경우 `accessmodifier` 에 `Get` 문.  
  
## <a name="rules"></a>규칙  
  
- **혼합 된 액세스 수준입니다.** 서로 다른 액세스 수준에 대 한 필요에 따라 지정할 수는 읽기 / 쓰기 속성을 정의 하는 경우는 `Get` 또는 `Set` 절차, 하지만 둘 다. 이 작업을 수행 하는 경우 프로시저 액세스 수준 속성의 액세스 수준 보다 더 제한적 이어야 합니다. 예를 들어, 속성 선언 되 면 `Friend`를 선언할 수 있습니다 합니다 `Get` 프로시저 `Private`, 아닌 `Public`합니다.  
  
     정의 하는 경우는 `ReadOnly` 속성을 `Get` 프로시저 전체 속성을 나타냅니다. 선언할 수 없습니다는 서로 다른 액세스 수준 `Get`이므로 속성에 대 한 두 가지 액세스 수준이 설정 합니다.  
  
- **형식을 반환 합니다.** 합니다 [Property 문](../../../visual-basic/language-reference/statements/property-statement.md) 반환 하는 값의 데이터 형식을 선언할 수 있습니다. `Get` 프로시저는 데이터 형식을 자동으로 반환 합니다. 모든 데이터 형식 또는 열거형, 구조체, 클래스 또는 인터페이스의 이름을 지정할 수 있습니다.  
  
     경우는 `Property` 문을 지정 하지 않습니다 `returntype`, 프로시저에서 반환 `Object`합니다.  
  
## <a name="behavior"></a>동작  
  
- **프로시저에서 반환합니다.** 경우는 `Get` 프로시저가 호출 코드에 반환 되 면 속성 값을 요청 하는 문에서 계속 실행 합니다.  
  
     `Get` 속성 프로시저 중 하나를 사용 하 여 값을 반환할 수는 [Return 문이](../../../visual-basic/language-reference/statements/return-statement.md) 속성 이름에 반환 값을 할당 하 여 합니다. 자세한 내용은 "반환 값"를 참조 하세요 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
     합니다 `Exit Property` 및 `Return` 문은 속성 프로시저를 즉시 종료 합니다. 임의 개수의 `Exit Property` 하 고 `Return` 문을 프로시저에서 아무 곳 이나 나타날 수 있으며 함께 사용할 수 있습니다 `Exit Property` 및 `Return` 문.  
  
- **값을 반환 합니다.** 값을 반환 하는 `Get` 프로시저, 속성 이름에 값을 할당 하거나 포함을 [Return 문이](../../../visual-basic/language-reference/statements/return-statement.md)합니다. 합니다 `Return` 문을 동시에 할당 된 `Get` 프로시저 반환 값 및 절차를 종료 합니다.  
  
     사용 하는 경우 `Exit Property` 속성 이름에 값을 할당 하지 않고는 `Get` 프로시저가 속성의 데이터 형식에 대 한 기본값을 반환 합니다. 자세한 내용은 "반환 값"를 참조 하세요 [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
     다음 예제에서는 두 가지 방법으로 읽기 전용 속성을 보여 줍니다 `quoteForTheDay` 전용 변수에 저장 된 값을 반환할 수 있습니다 `quoteValue`합니다.  
  
     [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]  
  
     [!code-vb[VbVbalrStatements#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#28)]  
  
     [!code-vb[VbVbalrStatements#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#29)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Get` 문을 속성의 값을 반환 합니다.  
  
 [!code-vb[VbVbalrStatements#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>참고자료

- [Set 문](../../../visual-basic/language-reference/statements/set-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [Exit 문](../../../visual-basic/language-reference/statements/exit-statement.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [연습: 클래스 정의](../../../visual-basic/programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)
