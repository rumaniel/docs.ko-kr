---
title: ^= 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.^=
helpviewer_keywords:
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- ^= operator [Visual Basic]
- compound assignment statements [Visual Basic]
ms.assetid: 397da132-2d96-4a85-a7bc-f7c730a608c9
ms.openlocfilehash: 382e0b27c2dbf27e5acccf29f1b8d2b002cb6664
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592230"
---
# <a name="-operator-visual-basic"></a>^= 연산자(Visual Basic)
변수나 속성의 값을 식의 거듭제곱으로 올리고 결과를 다시 변수 또는 속성에 할당 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
variableorproperty ^= expression  
```  
  
## <a name="parts"></a>요소  
 `variableorproperty`  
 필수. 임의의 숫자 변수 또는 속성입니다.  
  
 `expression`  
 필수. 임의의 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자의 좌 변에 있는 요소는 간단한 스칼라 변수, 속성 또는 배열의 요소일 수 있습니다. 변수 또는 속성은 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)일 수 없습니다.  
  
 @No__t-0 연산자는 먼저 연산자의 왼쪽에 있는 변수 또는 속성의 값을 연산자의 오른쪽에 있는 식의 값의 거듭제곱으로 발생 시킵니다. 그런 다음 연산자는 해당 작업의 결과를 변수 또는 속성에 다시 할당 합니다.  
  
 Visual Basic는 [Double 데이터 형식](../../../visual-basic/language-reference/data-types/double-data-type.md)에서 항상 지 각 연산을 수행 합니다. 다른 형식의 피연산자는 `Double`으로 변환 되며 결과는 항상 `Double`입니다.  
  
 @No__t-0의 값은 소수 자릿수, 음수 또는 둘 다 일 수 있습니다.  
  
## <a name="overloading"></a>오버로딩  
 [^ 연산자](../../../visual-basic/language-reference/operators/exponentiation-operator.md) 는 *오버 로드*될 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 재정의할 수 있습니다. @No__t-0 연산자를 오버 로드 하면 `^=` 연산자의 동작에 영향을 줍니다. 코드에서-1 @no__t 오버 로드 하는 클래스 또는 구조체에 `^=`을 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `^=` 연산자를 사용 하 여 한 `Integer` 변수의 값을 두 번째 변수의 거듭제곱으로 올리고 결과를 첫 번째 변수에 할당 합니다.  
  
 [!code-vb[VbVbalrOperators#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>참조

- [^ 연산자](../../../visual-basic/language-reference/operators/exponentiation-operator.md)
- [할당 연산자](../../../visual-basic/language-reference/operators/assignment-operators.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
