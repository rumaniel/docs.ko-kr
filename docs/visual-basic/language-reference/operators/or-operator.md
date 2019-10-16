---
title: Or 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Or
helpviewer_keywords:
- Or operator [Visual Basic]
- operators [Visual Basic], bitwise
- inclusive Or operator [Visual Basic]
- bitwise operators [Visual Basic], OR operator
- Or keyword [Visual Basic]
- operators [Visual Basic], inclusive or
- operators [Visual Basic], disjunction
- bitwise comparison [Visual Basic]
- logical disjunction
- disjunction operator [Visual Basic]
ms.assetid: 41ed6905-bf3d-468a-9e3b-03c10d461891
ms.openlocfilehash: 03decb4ad32e8ff2c03e3b64a272bce779282973
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701229"
---
# <a name="or-operator-visual-basic"></a>Or 연산자(Visual Basic)
두 개의 `Boolean` 식에 논리 분리를 수행 하거나 두 숫자 식에 비트 분리를 수행 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
result = expression1 Or expression2  
```  
  
## <a name="parts"></a>요소  
 `result`  
 필수. 모든 `Boolean` 또는 숫자 식입니다. @No__t 0 비교의 경우-1 @no__t 두 @no__t 값의 포함 논리 분리입니다. 비트 연산의 경우 `result`은 두 숫자 비트 패턴의 포함 비트 논리합을 나타내는 숫자 값입니다.  
  
 `expression1`  
 필수. 모든 `Boolean` 또는 숫자 식입니다.  
  
 `expression2`  
 필수. 모든 `Boolean` 또는 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0을 비교 하는 경우 `expression1`과 `expression2`가 모두 `False` 인 경우에만-1 @no__t `False`가 됩니다. 다음 표에서는 `result`이 결정 되는 방법을 보여 줍니다.  
  
|경우 `expression1` 됩니다|및 `expression2` 됩니다|값 `result`은입니다.|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
> @No__t-0 비교에서 `Or` 연산자는 항상 프로시저 호출을 포함 하는 두 식을 모두 계산 합니다. [OrElse 연산자](../../../visual-basic/language-reference/operators/orelse-operator.md) 는 *단락*을 수행 합니다. 즉, `expression1`가 `True` 이면 `expression2`가 계산 되지 않습니다.  
  
 비트 연산의 경우 `Or` 연산자는 두 숫자 식에서 동일 하 게 배치 된 비트의 비트 비교를 수행 하 고 다음 표에 따라 `result`의 해당 비트를 설정 합니다.  
  
|@No__t 비트의 경우-0은입니다.|및 비트 `expression2`은입니다.|비트 `result`은입니다.|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|1|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
> 논리 및 비트 연산자는 다른 산술 및 관계형 연산자 보다 낮은 우선 순위를 가지 므로 정확한 실행을 위해 모든 비트 연산을 괄호로 묶어야 합니다.  
  
## <a name="data-types"></a>데이터 형식  
 피연산자가 하나의 `Boolean` 식과 하나의 숫자 식으로 구성 된 경우 Visual Basic `Boolean` 식을 숫자 값으로 변환 하 고 (@no__t-@no__t 2의 경우-1) 비트 연산을 수행 합니다.  
  
 @No__t-0 비교의 경우 결과의 데이터 형식은-1 @no__t 됩니다. 비트 비교의 경우 결과 데이터 형식은 `expression1` 및 `expression2`의 데이터 형식에 적합 한 숫자 형식입니다. [연산자 결과의 데이터 형식](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)에서 "관계형 및 비트 비교" 표를 참조 하세요.  
  
## <a name="overloading"></a>오버로딩  
 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `Or` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Or` 연산자를 사용 하 여 두 식에 대 한 포함 논리 분리를 수행 합니다. 결과는 두 식 중 하나 `True` 인지 여부를 나타내는 0 @no__t 값입니다.  
  
 [!code-vb[VbVbalrOperators#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#35)]  
  
 앞의 예제에서는 `True`, `True` 및 `False`의 결과를 각각 생성 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Or` 연산자를 사용 하 여 두 숫자 식의 개별 비트에 대 한 포괄적 논리합 연산을 수행 합니다. 피연산자의 해당 비트 중 하나가 1로 설정 된 경우 결과 패턴의 비트가 설정 됩니다.  
  
 [!code-vb[VbVbalrOperators#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#36)]  
  
 앞의 예제에서는 각각 10, 14 및 14의 결과를 생성 합니다.  
  
## <a name="see-also"></a>참조

- [논리/비트 연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [OrElse 연산자](../../../visual-basic/language-reference/operators/orelse-operator.md)
- [Visual Basic 논리 및 비트 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
