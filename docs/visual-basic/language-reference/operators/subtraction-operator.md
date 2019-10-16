---
title: '- 연산자 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.Negate
- vb.-
helpviewer_keywords:
- operator [Visual Basic]
- operators [Visual Basic], subtraction
- operators [Visual Basic], difference
- negation operator [Visual Basic]
- operators [Visual Basic], arithmetic
- subtraction operator [Visual Basic], syntax
- arithmetic operators [Visual Basic], subtraction
- difference operator [Visual Basic]
- math operators [Visual Basic]
- operators [Visual Basic], negation
- minus operator [Visual Basic]
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
ms.openlocfilehash: 5f6b6b67e2999d380cfca078a43162b3e1db2206
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701297"
---
# <a name="--operator-visual-basic"></a>- 연산자(Visual Basic)
두 숫자 식의 차이를 반환 하거나 숫자 식의 음수 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
expression1 – expression2
```
  
로 구분하거나 여러

```vb  
–expression1  
```  
  
## <a name="parts"></a>요소  
 `expression1`  
 필수 요소. 임의의 숫자 식입니다.  
  
 `expression2`  
 @No__t-0 연산자가 음수 값을 계산 하는 경우에만 필요 합니다. 임의의 숫자 식입니다.  
  
## <a name="result"></a>결과  
 결과는 `expression1`과 `expression2` 사이의 차이가 며-2 @no__t의 부정 값입니다.  
  
 결과 데이터 형식은 및 `expression1` `expression2`의 데이터 형식에 적합 한 숫자 형식입니다. [연산자 결과의 데이터 형식](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)에서 "정수 산술 연산" 표를 참조 하세요.  
  
## <a name="supported-types"></a>지원 형식  
 모든 숫자 형식. 여기에는 부호 없는 및 부동 소수점 형식 및 `Decimal`가 포함 됩니다.  
  
## <a name="remarks"></a>설명  
 이전에 표시 된 구문에 표시 된 첫 번째 사용에서 `–` 연산자는 두 숫자 식의 차이에 대 한 *이진* 산술 빼기 연산자입니다.  
  
 앞에 표시 된 구문에 표시 된 두 번째 사용에서 `–` 연산자는 식의 음수 값에 대 한 *단항* 부정 연산자입니다. 이러한 의미에서 부정은 `expression1`의 부호를 반대로 하 여 `expression1`이 음수 이면 결과가 양수인 것으로 구성 됩니다.  
  
 두 식이 모두 [Nothing](../../../visual-basic/language-reference/nothing.md)으로 계산 되는 경우 `–` 연산자는이 값을 0으로 처리 합니다.  
  
> [!NOTE]
> 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `–` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `–` 연산자를 사용 하 여 두 숫자 간의 차이를 계산 하 고 반환한 다음 숫자를 부정 합니다.  
  
 [!code-vb[VbVbalrOperators#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#10)]  
  
 이러한 문을 실행 한 후 `binaryResult`에 124.45이 포함 되 고 `unaryResult`에 – 334.90이 포함 됩니다.  
  
## <a name="see-also"></a>참조

- [-= 연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic의 산술 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
