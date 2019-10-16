---
title: Function 프로시저(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Function procedures
- return values [Visual Basic], function procedures
- Visual Basic code, procedures
- procedures [Visual Basic], calling
- procedures [Visual Basic], Function procedures
- syntax [Visual Basic], function procedures
ms.assetid: 1b9f632c-553b-4cb6-920a-ded117ead8c0
ms.openlocfilehash: 4fd24369380e5f8ccf8de939c36ba72a12dc872e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649611"
---
# <a name="function-procedures-visual-basic"></a>Function 프로시저(Visual Basic)
A `Function` 절차는 일련의 Visual Basic 문으로 둘러싸인 합니다 `Function` 및 `End Function` 문. `Function` 프로시저는 작업을 수행한 다음 호출 코드에 제어를 반환 합니다. 제어를 반환 하기 호출 코드에도 값을 반환 합니다.  
  
 후 첫 번째 실행 가능 문을 사용 하 여 프로시저를 호출할 문이 실행 될 때마다 시작 합니다 `Function` 문과 첫 번째 끝 `End Function`, `Exit Function`, 또는 `Return` 문을 발견 했습니다.  
  
 정의할 수 있습니다는 `Function` 모듈, 클래스 또는 구조체에는 프로시저입니다. `Public` 어디에서 나 호출할 수 있습니다 즉 기본적으로 모듈, 클래스 또는 구조체 정의 액세스 권한이 있는 응용 프로그램에서 합니다.  
  
 `Function` 프로시저 호출 코드에서 전달 되는 식, 상수, 변수 등의 인수를 사용할 수 있습니다.  
  
## <a name="declaration-syntax"></a>선언 구문  
 선언 구문이 `Function` 절차는 다음과 같습니다.  
  
```vb  
[Modifiers] Function FunctionName [(ParameterList)] As ReturnType  
    [Statements]  
End Function  
```  
  
 합니다 *한정자* 액세스 수준 및 오버 로드, 재정의 공유 및 숨기기에 대 한 정보를 지정할 수 있습니다. 자세한 내용은 [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
 수행한 동일한 방식으로 각 매개 변수를 선언할 [Sub 프로시저](./sub-procedures.md)합니다.  
  
### <a name="data-type"></a>데이터 형식  
 모든 `Function` 프로시저는 데이터 형식에 각 변수와 마찬가지로 않습니다. 이 데이터 형식을 지정 하 여는 `As` 절을 `Function` 문 및 해당 함수 호출 코드로 반환 값의 데이터 형식을 결정 합니다. 다음 샘플 선언에서는이 보여 줍니다.  
  
```vb  
Function yesterday() As Date  
End Function  
  
Function findSqrt(ByVal radicand As Single) As Single  
End Function  
```  
  
 자세한 내용은 "파트"를 참조 하세요 [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
## <a name="returning-values"></a>반환 값  
 값을 `Function` 프로시저에서 전송 하는 호출 코드에 다시 반환 값 이라고 합니다. 프로시저는 두 가지 방법 중 하나에서이 값을 반환합니다.  
  
- 사용 된 `Return` 반환 값 및 반환을 지정 하는 문을 호출 프로그램에 즉시 제어 합니다. 다음은 이에 대한 예입니다.  
  
```vb  
Function FunctionName [(ParameterList)] As ReturnType  
    ' The following statement immediately transfers control back  
    ' to the calling code and returns the value of Expression.  
    Return Expression  
End Function  
```  
  
- 프로시저의 하나 이상의 문에서 함수 이름에 값을 할당합니다. 될 때까지 호출 프로그램에 제어를 반환 하지 않습니다는 `Exit Function` 또는 `End Function` 문이 실행 됩니다. 다음은 이에 대한 예입니다.  
  
```vb  
Function FunctionName [(ParameterList)] As ReturnType  
    ' The following statement does not transfer control back to the calling code.  
    FunctionName = Expression  
    ' When control returns to the calling code, Expression is the return value.  
End Function  
```  
  
 함수 이름에 반환 값을 할당 하는 장점은 만날 때까지 제어 프로시저에서 반환 하지 않는 프로그램 `Exit Function` 또는 `End Function` 문. 이 임시 값을 할당 하 고 필요한 경우 나중에 조정 수 있습니다.  
  
 값을 반환 하는 방법에 대 한 자세한 내용은 참조 하세요. [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)합니다. 배열을 반환 하는 방법에 대 한 내용은 [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)합니다.  
  
## <a name="calling-syntax"></a>호출 구문  
 호출 하는 `Function` 프로시저 이름과 인수 중 하나에 식 또는 대입문의 오른쪽을 포함 하 여 합니다. 선택적 인수가 아닌 모든 인수에 대 한 값을 제공 해야 하 고 인수 목록을 괄호로 묶어야 합니다. 인수 없이 제공 되는 경우에 필요에 따라 괄호를 생략할 수 있습니다.  
  
 에 대 한 호출에 대 한 구문을 `Function` 절차는 다음과 같습니다.  
  
 *lvalue*  `=`  *functionname* `[(` *argumentlist* `)]`  
  
 `If ((` *functionname* `[(` *argumentlist* `)] / 3) <=`  *expression* `) Then`  
  
 호출 하는 경우는 `Function` 프로시저 필요가 없습니다 해당 반환 값을 사용 합니다. 그렇지 않으면 함수는 모든 작업이 수행 되었는지, 되지만 반환 값은 무시 됩니다. <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 이 방식 이라고 합니다.  
  
### <a name="illustration-of-declaration-and-call"></a>선언 및 호출의 그림  
 다음 `Function` 프로시저 제일 긴 쪽 또는 다른 두 가지 측면에 대 한 값이 지정 된 오른쪽 삼각형의 빗변을 계산 합니다.  
  
 [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]  
  
 다음 예제에서는 일반적인 호출 `hypotenuse`합니다.  
  
 [!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [Sub 프로시저](./sub-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)
- [방법: 값을 반환 하는 프로시저 만들기](./how-to-create-a-procedure-that-returns-a-value.md)
- [방법: 프로시저에서 값을 반환 합니다.](./how-to-return-a-value-from-a-procedure.md)
- [방법: 값을 반환 하는 프로시저 호출](./how-to-call-a-procedure-that-returns-a-value.md)
