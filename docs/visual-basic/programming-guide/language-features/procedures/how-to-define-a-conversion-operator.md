---
title: '방법: 변환 연산자 (Visual Basic)를 정의 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- operators [Visual Basic], defining
- procedures [Visual Basic], operator
- operators [Visual Basic], overloading
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: 54203dfa-c24b-463f-9942-d5153e89e762
ms.openlocfilehash: cf7bfdd09c7f3429f9c730a7aec34b24af3f2e9f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61863716"
---
# <a name="how-to-define-a-conversion-operator-visual-basic"></a>방법: 변환 연산자 (Visual Basic)를 정의 합니다.
클래스 또는 구조체를 정의한 경우 해당 클래스 또는 구조체 형식 및 다른 데이터 형식 간의 형식 변환 연산자를 정의할 수 있습니다 (같은 `Integer`, `Double`, 또는 `String`).  
  
 형식 변환으로 정의 [CType Function](../../../../visual-basic/language-reference/functions/ctype-function.md) 클래스 또는 구조체 내에서 프로시저입니다. 모든 변환 프로시저 여야 `Public Shared`를 각각 지정 해야 합니다 [Widening](../../../../visual-basic/language-reference/modifiers/widening.md) 또는 [Narrowing](../../../../visual-basic/language-reference/modifiers/narrowing.md)합니다.  
  
 클래스 또는 구조체에서 연산자를 정의 라고도 *오버 로드* 연산자입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 라는 구조 간의 변환 연산자를 정의 `digit` 및 `Byte`합니다.  
  
 [!code-vb[VbVbcnProcedures#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#27)]  
  
 구조를 테스트할 수 있습니다 `digit` 다음 코드를 사용 합니다.  
  
 [!code-vb[VbVbcnProcedures#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>참고자료

- [연산자 프로시저](./operator-procedures.md)
- [방법: 연산자 정의](./how-to-define-an-operator.md)
- [방법: 연산자 프로시저 호출](./how-to-call-an-operator-procedure.md)
- [방법: 연산자를 정의 하는 클래스를 사용 합니다.](./how-to-use-a-class-that-defines-operators.md)
- [Operator 문](../../../../visual-basic/language-reference/statements/operator-statement.md)
- [Structure 문](../../../../visual-basic/language-reference/statements/structure-statement.md)
- [방법: 구조 선언](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)
- [암시적 변환과 명시적 변환](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [확대 변환과 축소 변환](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
