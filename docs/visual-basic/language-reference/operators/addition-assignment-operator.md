---
title: += 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.+=
helpviewer_keywords:
- += operator [Visual Basic]
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- += operator [Visual Basic], appending strings
- compound assignment statements [Visual Basic]
ms.assetid: d3e959f4-85d4-4e47-87c4-77b62335a5b3
ms.openlocfilehash: 249a19abfb08677c01ac4cc484d049a7ed1a983c
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591641"
---
# <a name="-operator-visual-basic"></a>+= 연산자(Visual Basic)
숫자 식의 값을 숫자 변수나 속성의 값에 추가 하 고 결과를 변수 또는 속성에 할당 합니다. 를 사용 하 여 `String` 식을 `String` 변수 또는 속성에 연결 하 고 결과를 변수 또는 속성에 할당할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
variableorproperty += expression  
```  
  
## <a name="parts"></a>요소  
 `variableorproperty`  
 필수. 임의의 숫자 또는 @no__t 0 변수 또는 속성입니다.  
  
 `expression`  
 필수. 임의의 숫자 또는 `String` 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자의 좌 변에 있는 요소는 간단한 스칼라 변수, 속성 또는 배열의 요소일 수 있습니다. 변수 또는 속성은 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)일 수 없습니다.  
  
 @No__t-0 연산자는 오른쪽의 값을 왼쪽에 있는 변수나 속성에 추가 하 고 결과를 왼쪽에 있는 변수나 속성에 할당 합니다. @No__t-0 연산자를 사용 하 여 오른쪽의 `String` 식을 왼쪽에 있는 `String` 변수 또는 속성에 연결 하 고 결과를 왼쪽에 있는 변수나 속성에 할당할 수도 있습니다.  
  
> [!NOTE]
> @No__t-0 연산자를 사용 하는 경우 더하기 또는 문자열 연결의 발생 여부를 확인 하지 못할 수 있습니다. 모호성을 제거 하 고 자체 문서화 코드를 제공 하려면 연결에 `&=` 연산자를 사용 합니다.  
  
 이 할당 연산자는 컴파일 환경에서 엄격한 의미 체계를 적용 하는 경우 암시적으로 확대를 수행 하지만 축소 변환을 수행 하지 않습니다. 이러한 변환에 대 한 자세한 내용은 [확대 및 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)을 참조 하세요. Strict 및 관대 한 의미 체계에 대 한 자세한 내용은 [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)을 참조 하세요.  
  
 관대 한 의미 체계가 허용 되는 경우 `+=` 연산자는 `+` 연산자에 의해 수행 되는 것과 같은 다양 한 문자열 및 숫자 변환을 암시적으로 수행 합니다. 이러한 변환에 대 한 자세한 내용은 [+ 연산자](../../../visual-basic/language-reference/operators/addition-operator.md)를 참조 하세요.  
  
## <a name="overloading"></a>오버로딩  
 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `+` @No__t-0 연산자를 오버 로드 하면 `+=` 연산자의 동작에 영향을 줍니다. 코드에서-1 @no__t 오버 로드 하는 클래스 또는 구조체에 `+=`을 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `+=` 연산자를 사용 하 여 한 변수의 값을 다른 변수의 값과 결합 합니다. 첫 번째 부분은 숫자 변수와 함께 `+=`을 사용 하 여 한 값을 다른 값에 추가 합니다. 두 번째 부분에서는 `String` 변수와 `+=`을 사용 하 여 한 값을 다른 값과 연결 합니다. 두 경우 모두 결과는 첫 번째 변수에 할당 됩니다.  
  
 [!code-vb[VbVbalrOperators#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#7)]  
  
 [!code-vb[VbVbalrOperators#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#8)]  
  
 @No__t-0은 이제 13 이며 `str1`의 값이 이제 "103"입니다.  
  
## <a name="see-also"></a>참조

- [+ 연산자](../../../visual-basic/language-reference/operators/addition-operator.md)
- [할당 연산자](../../../visual-basic/language-reference/operators/assignment-operators.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [연결 연산자](../../../visual-basic/language-reference/operators/concatenation-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
