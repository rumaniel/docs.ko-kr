---
title: '>>= 연산자(Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.>>=
helpviewer_keywords:
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- operator >>= [Visual Basic]
- compound assignment statements [Visual Basic]
- '>>= operator [Visual Basic]'
ms.assetid: 2bcd9abb-7a8c-4229-b75d-8816ff1dc700
ms.openlocfilehash: 08d4e251a96ca387a709319e752351db6825d9e8
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701352"
---
# <a name="-operator-visual-basic"></a>> > = 연산자 (Visual Basic)
변수 또는 속성 값에서 산술 오른쪽 시프트를 수행 하 고 결과를 다시 변수 또는 속성에 할당 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
variableorproperty >>= amount  
```  
  
## <a name="parts"></a>요소  
 `variableorproperty`  
 필수. 정수 계열 형식의 변수 또는 속성 (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `ULong`).  
  
 `amount`  
 필수. @No__t-0으로 확대 되는 데이터 형식의 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자의 좌 변에 있는 요소는 간단한 스칼라 변수, 속성 또는 배열의 요소일 수 있습니다. 변수 또는 속성은 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)일 수 없습니다.  
  
 @No__t-0 연산자는 먼저 변수나 속성의 값에 대 한 산술 오른쪽 시프트를 수행 합니다. 그런 다음 연산자는 해당 작업의 결과를 변수 또는 속성에 다시 할당 합니다.  
  
 산술 시프트는 순환 하지 않습니다. 즉, 결과의 한쪽 끝에서 이동 하는 비트가 다른 쪽 끝에서는 다시 계산 되지 않습니다. 산술 오른쪽 시프트에서 가장 오른쪽 비트 위치를 넘어 이동 하는 비트는 무시 되 고 맨 왼쪽 비트는 왼쪽의 비워진 비트 위치로 전파 됩니다. 즉, `variableorproperty`에 음수 값이 있으면 비워진 위치가 1로 설정 됩니다. @No__t-0이 양수 이거나 해당 데이터 형식이 부호 없는 형식이 면 비워진 위치가 0으로 설정 됩니다.  
  
## <a name="overloading"></a>오버로딩  
 [> > 연산자](../../../visual-basic/language-reference/operators/right-shift-operator.md) 를 *오버 로드할*수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식이 면 클래스 또는 구조체에서 해당 동작을 다시 정의할 수 있습니다. @No__t-0 연산자를 오버 로드 하면 `>>=` 연산자의 동작에 영향을 줍니다. 코드에서-1 @no__t 오버 로드 하는 클래스 또는 구조체에 `>>=`을 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `>>=` 연산자를 사용 하 여 `Integer` 변수의 비트 패턴을 지정 된 크기 만큼 오른쪽으로 이동 하 고 결과를 변수에 할당 합니다.  
  
 [!code-vb[VbVbalrOperators#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>참조

- [>> 연산자](../../../visual-basic/language-reference/operators/right-shift-operator.md)
- [할당 연산자](../../../visual-basic/language-reference/operators/assignment-operators.md)
- [비트 시프트 연산자](../../../visual-basic/language-reference/operators/bit-shift-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
