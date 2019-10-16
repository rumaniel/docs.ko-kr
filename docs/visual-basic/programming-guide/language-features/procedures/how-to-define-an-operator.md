---
title: '방법: 연산자 (Visual Basic)를 정의 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- operators [Visual Basic], defining
- procedures [Visual Basic], operator
- Visual Basic code, operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- operator procedures [Visual Basic], about operator procedures
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: d4b0e253-092a-4e6e-9fe2-01f562140a29
ms.openlocfilehash: 14aa25de78eb357f8474d3828aa45e48e7a4f9c7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61863847"
---
# <a name="how-to-define-an-operator-visual-basic"></a>방법: 연산자 (Visual Basic)를 정의 합니다.
클래스 또는 구조체를 정의한 경우에 표준 연산자의 동작을 정의할 수 있습니다 (같은 `*`, `<>`, 또는 `And`) 클래스 또는 구조체 형식의 하나 또는 두 피연산자 모두가 하는 경우.  
  
 클래스 또는 구조체에서 연산자 프로시저도 표준 연산자를 정의 합니다. 모든 연산자 프로시저 여야 `Public` `Shared`합니다.  
  
 클래스 또는 구조체에서 연산자를 정의 라고도 *오버 로드* 연산자입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 정의 된 `+` 구조에 대 한 연산자 호출 `height`합니다. 구조는 feet 및 인치 단위로 측정 된 높이 사용 합니다. 하나의 *인치* 2.54 센티미터 이며 하나 *foot* 12 인치입니다. 생성자는 정규화 된 값 (인치 < 12.0)을 위해 다음을 수행 합니다. *모듈로* 산술 12입니다. `+` 연산자 생성자를 사용 하 여 정규화 된 값을 생성 합니다.  
  
 [!code-vb[VbVbcnProcedures#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#25)]  
  
 구조를 테스트할 수 있습니다 `height` 다음 코드를 사용 합니다.  
  
 [!code-vb[VbVbcnProcedures#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#26)]  

## <a name="see-also"></a>참고자료

- [연산자 프로시저](./operator-procedures.md)
- [방법: 변환 연산자를 정의 합니다.](./how-to-define-a-conversion-operator.md)
- [방법: 연산자 프로시저 호출](./how-to-call-an-operator-procedure.md)
- [방법: 연산자를 정의 하는 클래스를 사용 합니다.](./how-to-use-a-class-that-defines-operators.md)
- [Operator 문](../../../../visual-basic/language-reference/statements/operator-statement.md)
- [Structure 문](../../../../visual-basic/language-reference/statements/structure-statement.md)
- [방법: 구조 선언](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)
- [Mod 연산자](../../../../visual-basic/language-reference/operators/mod-operator.md)
