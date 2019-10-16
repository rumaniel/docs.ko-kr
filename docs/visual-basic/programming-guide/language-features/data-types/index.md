---
title: Visual Basic의 데이터 형식
ms.date: 07/20/2015
helpviewer_keywords:
- data types [Visual Basic], declaring
- typing
- data types [Visual Basic]
- Visual Basic code, data types
- data types [Visual Basic], improving speed with
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
ms.openlocfilehash: 192ced1da400372f877cb54aaa29d60fcd0bbcad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62008269"
---
# <a name="data-types-in-visual-basic"></a>Visual Basic의 데이터 형식
프로그래밍 요소의 *데이터 형식*은 사용할 수 있는 데이터의 종류 및 데이터를 저장하는 방식을 의미합니다. 데이터 형식은 컴퓨터 메모리에 저장할 수 있거나 식의 계산에 사용되는 모든 값에 적용됩니다. 모든 변수, 리터럴, 상수, 열거형, 속성, 프로시저 매개 변수, 프로시저 인수 및 프로시저 반환 값은 데이터 형식을 가집니다.  
  
## <a name="declared-data-types"></a>선언된 데이터 형식  
 선언문을 사용하여 프로그래밍 요소를 정의하고 `As` 절을 사용하여 데이터 형식을 지정합니다. 다음 표에서는 다양한 요소를 선언하기 위해 사용하는 문을 보여 줍니다.  
  
|프로그래밍 요소|데이터 형식 선언|  
|-------------------------|---------------------------|  
|변수|[Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)에서 지정합니다.<br /><br /> `Dim`  `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`  `billsPaid As Decimal = 0`|  
|Literal|리터럴 형식 문자에 지정합니다. [형식 문자](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)에서 "리터럴 형식 문자"를 참조하세요.<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|상수|[Const 문](../../../../visual-basic/language-reference/statements/const-statement.md)에서 지정합니다.<br /><br /> `Const`  `modulus As Single = 4.17825F`|  
|열거형|[Enum 문](../../../../visual-basic/language-reference/statements/enum-statement.md)에서 지정합니다.<br /><br /> `Public`   `Enum`   `colors`|  
|속성|[Property 문](../../../../visual-basic/language-reference/statements/property-statement.md)에서 지정합니다.<br /><br /> `Property`  `region() As String`|  
|프로시저 매개 변수|[Sub 문](../../../../visual-basic/language-reference/statements/sub-statement.md), [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md) 또는 [Operator 문](../../../../visual-basic/language-reference/statements/operator-statement.md)에서 지정합니다.<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|프로시저 인수|호출 코드에서 지정합니다. 각 인수는 이미 선언된 프로그래밍 요소이거나 선언된 요소를 포함하는 식입니다.<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|프로시저 반환 값|[Function 문](../../../../visual-basic/language-reference/statements/function-statement.md) 또는 [Operator 문](../../../../visual-basic/language-reference/statements/operator-statement.md)에서 지정합니다.<br /><br /> `Function convert(ByVal b As Byte)`  `As String`|  
  
 Visual Basic 데이터 형식 목록은 [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [형식 문자](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
- [기본 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)
- [복합 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)
- [Visual Basic의 제네릭 형식](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [Visual Basic의 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [구조체](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [튜플](tuples.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [데이터 형식의 효율적 사용](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
