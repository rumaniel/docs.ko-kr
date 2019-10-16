---
title: 함수 식(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Function expression [Visual Basic]
- functions [Visual Basic], function expressions
- lambda expressions [Visual Basic], function expression
ms.assetid: e8a47a45-4b8a-4f45-a623-7653625dffbc
ms.openlocfilehash: 0ab4a77395b478df06f34240212438f3e6e18f6e
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592202"
---
# <a name="function-expression-visual-basic"></a>함수 식(Visual Basic)
함수 람다 식을 정의 하는 매개 변수 및 코드를 선언 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Function ( [ parameterlist ] ) expression  
- or -  
Function ( [ parameterlist ] )  
  [ statements ]  
End Function  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`parameterlist`|(선택 사항) 이 프로시저의 매개 변수를 나타내는 지역 변수 이름 목록입니다. 목록이 비어 있는 경우에도 괄호가 있어야 합니다. [매개 변수 목록](../../../visual-basic/language-reference/statements/parameter-list.md)을 참조 하세요.|  
|`expression`|필수. 단일 식입니다. 식의 형식은 함수의 반환 형식입니다.|  
|`statements`|필수. @No__t-0 문을 사용 하 여 값을 반환 하는 문의 목록입니다. [Return 문](../../../visual-basic/language-reference/statements/return-statement.md)을 참조 하십시오. 반환 되는 값의 형식은 함수의 반환 형식입니다.|  
  
## <a name="remarks"></a>설명  
 *람다 식은* 값을 계산 하 고 반환 하는 이름이 없는 함수입니다. @No__t-0에 대 한 인수를 제외 하 고 대리자 형식을 사용할 수 있는 모든 곳에서 람다 식을 사용할 수 있습니다. 대리자에 대 한 자세한 내용과 대리자에 람다 식을 사용 하는 방법에 대 한 자세한 내용은 [Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md) 및 [완화 된 대리자 변환](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)을 참조 하세요.  
  
## <a name="lambda-expression-syntax"></a>람다 식 구문  
 람다 식의 구문은 표준 함수의 구문과 유사 합니다. 차이점은 다음과 같습니다.  
  
- 람다 식에 이름이 없습니다.  
  
- 람다 식에는 `Overloads` 또는 `Overrides`과 같은 한정자를 사용할 수 없습니다.  
  
- 람다 식은 `As` 절을 사용 하 여 함수의 반환 형식을 지정 하지 않습니다. 대신, 단일 줄 람다 식의 본문이로 계산 되는 값 또는 여러 줄로 된 람다 식의 반환 값에서 형식이 유추 됩니다. 예를 들어 한 줄 람다 식의 본문이-0 @no__t 이면 반환 형식은-1 @no__t 됩니다.  
  
- 한 줄로 된 람다 식의 본문은 문이 아니라 식 이어야 합니다. 본문은 함수 프로시저에 대 한 호출로 구성 될 수 있지만 sub 프로시저에 대 한 호출로 구성 될 수는 없습니다.  
  
- 모든 매개 변수에는 지정 된 데이터 형식이 있어야 합니다. 그렇지 않으면 모두 유추 해야 합니다.  
  
- 선택적 및 Paramarray 매개 변수는 허용 되지 않습니다.  
  
- 제네릭 매개 변수는 허용 되지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 간단한 람다 식을 만드는 두 가지 방법을 보여 줍니다. 첫 번째는 `Dim`을 사용 하 여 함수의 이름을 제공 합니다. 함수를 호출 하려면 매개 변수의 값으로를 보냅니다.  
  
 [!code-vb[VbVbalrLambdas#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#1)]  
  
 [!code-vb[VbVbalrLambdas#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#2)]  
  
## <a name="example"></a>예제  
 또는 함수를 동시에 선언 하 고 실행할 수 있습니다.  
  
 [!code-vb[VbVbalrLambdas#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#3)]  
  
## <a name="example"></a>예제  
 다음은 해당 인수를 증가 하 고 값을 반환 하는 람다 식의 예입니다. 이 예제에서는 함수에 대 한 단일 줄 및 여러 줄 람다 식 구문을 보여 줍니다. 더 많은 예제는 [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)을 참조 하세요.  
  
 [!code-vb[VbVbalrLambdas#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#14)]  
  
## <a name="example"></a>예제  
 람다 식은 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]의 많은 쿼리 연산자의 기반이 되며 메서드 기반 쿼리에서 명시적으로 사용할 수 있습니다. 다음 예에서는 일반적인 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 다음에 쿼리를 메서드 형식으로 변환 하는 방법을 보여 줍니다.  
  
```vb  
Dim londonCusts = From cust In db.Customers  
                       Where cust.City = "London"  
                       Select cust  
  
' This query is compiled to the following code:  
Dim londonCusts = db.Customers.  
                  Where(Function(cust) cust.City = "London").  
                  Select(Function(cust) cust)  
```  
  
 쿼리 메서드에 대 한 자세한 내용은 [쿼리](../../../visual-basic/language-reference/queries/index.md)를 참조 하세요. 표준 쿼리 연산자에 대 한 자세한 내용은 [표준 쿼리 연산자 개요](../../programming-guide/concepts/linq/standard-query-operators-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참조

- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
- [연산자 및 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
- [값 비교](../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)
- [부울 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)
- [If 연산자](../../../visual-basic/language-reference/operators/if-operator.md)
- [완화된 대리자 변환](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
