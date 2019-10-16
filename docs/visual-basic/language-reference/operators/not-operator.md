---
title: Not 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Not
helpviewer_keywords:
- Boolean expressions, negating
- operators [Visual Basic], bitwise
- negation operator [Visual Basic]
- inverse bit values in variables [Visual Basic]
- bitwise operators [Visual Basic], NOT operator
- bitwise comparison [Visual Basic]
- Not operator [Visual Basic]
- logical negation
- operators [Visual Basic], negation
ms.assetid: 8f2ea83c-d2ed-480a-a474-3042a1cad9b5
ms.openlocfilehash: 5ebc5f9dbf674a9a6560bd96b3e8c9edcae08a81
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701084"
---
# <a name="not-operator-visual-basic"></a>Not 연산자(Visual Basic)
@No__t-0 식에 논리 부정을 수행 하거나 숫자 식에 비트 부정을 수행 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
result = Not expression  
```  
  
## <a name="parts"></a>요소  
 `result`  
 필수. 모든 `Boolean` 또는 숫자 식입니다.  
  
 `expression`  
 필수. 모든 `Boolean` 또는 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 식의 경우 다음 표에서 `result`이 결정 되는 방법을 보여 줍니다.  
  
|경우 `expression` 됩니다|값 `result`은입니다.|  
|------------------------|------------------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 숫자 식에서 `Not` 연산자는 숫자 식의 비트 값을 반전 하 고 다음 표에 따라 `result`의 해당 비트를 설정 합니다.  
  
|@No__t 비트의 경우-0은입니다.|비트 `result`은입니다.|  
|-------------------------------|----------------------------|  
|1|0|  
|0|1|  
  
> [!NOTE]
> 논리 및 비트 연산자는 다른 산술 및 관계형 연산자 보다 낮은 우선 순위를 가지 므로 정확한 실행을 위해 모든 비트 연산을 괄호로 묶어야 합니다.  
  
## <a name="data-types"></a>데이터 형식  
 부울 부정의 경우 결과의 데이터 형식은 `Boolean`입니다. 비트 부정의 경우 결과 데이터 형식은 `expression`과 동일 합니다. 그러나 expression이 `Decimal` 이면 @no__t 결과는-1입니다.  
  
## <a name="overloading"></a>오버로딩  
 @No__t-0 연산자는 *오버 로드*될 수 있습니다. 즉, 클래스 또는 구조체의 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 재정의할 수 있습니다. 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Not` 연산자를 사용 하 여 `Boolean` 식에 논리 부정을 수행 합니다. 결과는 식의 값을 반대로 나타내는 @no__t 값입니다.  
  
 [!code-vb[VbVbalrOperators#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#33)]  
  
 앞의 예제에서는 각각 `False` 및 `True`의 결과를 생성 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Not` 연산자를 사용 하 여 숫자 식의 개별 비트에 대 한 논리 부정을 수행 합니다. 결과 패턴의 비트는 부호 비트를 포함 하 여 피연산자 패턴에서 해당 비트의 역방향으로 설정 됩니다.  
  
 [!code-vb[VbVbalrOperators#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#34)]  
  
 앞의 예제에서는 – 11, – 9 및 – 7의 결과를 각각 생성 합니다.  
  
## <a name="see-also"></a>참조

- [논리/비트 연산자 (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic 논리 및 비트 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
