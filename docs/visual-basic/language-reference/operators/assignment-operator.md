---
title: = 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Assign
- vb.=
helpviewer_keywords:
- = operator [Visual Basic]
- = assignment statements [Visual Basic]
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
ms.openlocfilehash: ca4c519dd80c07f54dc1c3dfe70daf6948446363
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591836"
---
# <a name="-operator-visual-basic"></a>= 연산자(Visual Basic)
변수 또는 속성에 값을 할당 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
variableorproperty = value  
```  
  
## <a name="parts"></a>요소  
 `variableorproperty`  
 쓰기 가능한 변수 또는 모든 속성입니다.  
  
 `value`  
 모든 리터럴, 상수 또는 식입니다.  
  
## <a name="remarks"></a>설명  
 등호 (`=`)의 왼쪽에 있는 요소는 간단한 스칼라 변수, 속성 또는 배열의 요소일 수 있습니다. 변수 또는 속성은 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)일 수 없습니다. @No__t-0 연산자는 오른쪽의 값을 왼쪽에 있는 변수나 속성에 할당 합니다.  
  
> [!NOTE]
> @No__t-0 연산자는 비교 연산자로도 사용 됩니다. 자세한 내용은 [비교 연산자](../../../visual-basic/language-reference/operators/comparison-operators.md)를 참조 하세요.  
  
## <a name="overloading"></a>오버로딩  
 @No__t-0 연산자는 할당 연산자가 아닌 관계형 비교 연산자로만 오버 로드 될 수 있습니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 대입 연산자를 보여 줍니다. 오른쪽의 값이 왼쪽의 변수에 할당 됩니다.  
  
 [!code-vb[VbVbalrOperators#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>참조

- [&= 연산자](../../../visual-basic/language-reference/operators/and-assignment-operator.md)
- [*= 연산자](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)
- [+= 연산자](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)
- [-= 연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)
- [/= 연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)
- [\\= 연산자](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)
- [^= 연산자](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
- [비교 연산자](../../../visual-basic/language-reference/operators/comparison-operators.md)
- [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)
- [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
