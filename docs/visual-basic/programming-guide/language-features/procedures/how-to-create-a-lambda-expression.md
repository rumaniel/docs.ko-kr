---
title: '방법: 람다 식 (Visual Basic) 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
ms.assetid: 3279bd5c-80f7-410a-a7ba-f7085ed36aa5
ms.openlocfilehash: fc2b7ed2004b842116d051b393f00506428def61
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61665938"
---
# <a name="how-to-create-a-lambda-expression-visual-basic"></a>방법: 람다 식 (Visual Basic) 만들기
A *람다 식* 은 함수 또는 서브루틴에 이름이 없습니다입니다. 람다 식은 대리자 형식이 유효한 모든 곳에서 사용할 수 있습니다.  
  
### <a name="to-create-a-single-line-lambda-expression-function"></a>한 줄 람다 식 함수를 만들려면  
  
1. 대리자 형식을 사용할 수 있는 모든 상황에서 키워드를 입력 `Function`다음 예제와 같이:  
  
     `Dim add1 =`  `Function`  
  
2. 괄호로 직후 `Function`, 함수의 매개 변수를 입력 합니다. 뒤에 이름을 지정 하지 않으면 확인 `Function`합니다.  
  
     `Dim add1 = Function`  `(num As Integer)`  
  
3. 매개 변수 목록 다음 함수의 본문으로 단일 식을 입력 합니다. 식이 계산 되는 값에는 함수가 반환한 값이입니다. 사용 하지 않는 것을 `As` 반환 형식을 지정 하는 절.  
  
     [!code-vb[VbVbalrLambdas#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#1)]  
  
     정수 인수에 전달 하 람다 식을 호출 합니다.  
  
     [!code-vb[VbVbalrLambdas#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#2)]  
  
4. 또는 동일한 결과 다음 예제에서 수행 됩니다.  
  
     [!code-vb[VbVbalrLambdas#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#3)]  
  
### <a name="to-create-a-single-line-lambda-expression-subroutine"></a>한 줄 람다 식 서브루틴을 만들려면  
  
1. 대리자 형식을 사용할 수 있는 모든 상황에서 키워드를 입력 `Sub`다음 예제에서와 같이 합니다.  
  
     `Dim add1 =`  `Sub`  
  
2. 괄호로 직후 `Sub`, 서브루틴의 매개 변수를 입력 합니다. 뒤에 이름을 지정 하지 않으면 확인 `Sub`합니다.  
  
     `Dim add1 = Sub`  `(msg As String)`  
  
3. 매개 변수 목록에 다음 서브루틴의 본문으로 단일 문을 입력 합니다.  
  
     [!code-vb[VbVbalrLambdas#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#17)]  
  
     문자열 인수를 전달 하 람다 식을 호출 합니다.  
  
     [!code-vb[VbVbalrLambdas#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#18)]  
  
### <a name="to-create-a-multiline-lambda-expression-function"></a>여러 줄 람다 식 함수를 만들려면  
  
1. 대리자 형식을 사용할 수 있는 모든 상황에서 키워드를 입력 `Function`다음 예제에서와 같이 합니다.  
  
     `Dim add1 =`  `Function`  
  
2. 괄호로 직후 `Function`, 함수의 매개 변수를 입력 합니다. 뒤에 이름을 지정 하지 않으면 확인 `Function`합니다.  
  
     `Dim add1 = Function`  `(index As Integer)`  
  
3. Enter 키를 누릅니다. `End Function` 문을 자동으로 추가 됩니다.  
  
4. 함수의 본문 내에서 식을 만들고 값을 반환 하려면 다음 코드를 추가 합니다. 사용 하지 않는 것을 `As` 반환 형식을 지정 하는 절.  
  
     [!code-vb[VbVbalrLambdas#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#19)]  
  
     정수 인수에 전달 하 람다 식을 호출 합니다.  
  
     [!code-vb[VbVbalrLambdas#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#20)]  
  
### <a name="to-create-a-multiline-lambda-expression-subroutine"></a>여러 줄 람다 식 서브루틴을 만들려면  
  
1. 대리자 형식을 사용할 수 있는 모든 상황에서 키워드를 입력 `Sub`다음 예제에서와 같이:  
  
     `Dim add1 =`  `Sub`  
  
2. 괄호로 직후 `Sub`, 서브루틴의 매개 변수를 입력 합니다. 뒤에 이름을 지정 하지 않으면 확인 `Sub`합니다.  
  
     `Dim add1 = Sub`  `(msg As String)`  
  
3. Enter 키를 누릅니다. `End Sub` 문을 자동으로 추가 됩니다.  
  
4. 함수의 본문 내에서 서브루틴 호출 될 때 실행한 다음 코드를 추가 합니다.  
  
     [!code-vb[VbVbalrLambdas#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#21)]  
  
     문자열 인수를 전달 하 람다 식을 호출 합니다.  
  
     [!code-vb[VbVbalrLambdas#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#22)]  
  
## <a name="example"></a>예제  
 람다 식의 일반적인 용도 형식의 매개 변수에 대해 인수로 전달 될 수 있는 함수를 정의 하는 `Delegate`합니다. 다음 예제에서는 <xref:System.Diagnostics.Process.GetProcesses%2A> 로컬 컴퓨터에서 실행 중인 프로세스의 배열을 반환 합니다. <xref:System.Linq.Enumerable.Where%2A> 메서드를 <xref:System.Linq.Enumerable> 클래스에 필요한를 `Boolean` 인수로 대리자입니다. 예제에서 람다 식은 해당 용도로 사용 됩니다. 반환 `True` 에서 선택 됩니다 및 각 프로세스에 대해 스레드 한 개만 있는 `filteredList`합니다.  
  
 [!code-vb[VbVbalrLambdas#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class4.vb#10)]  
  
 앞의 예제는 작성 된 다음 코드와 동일 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 구문:  
  
 [!code-vb[VbVbalrLambdas#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class5.vb#11)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Linq.Enumerable>
- [람다 식](./lambda-expressions.md)
- [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub 문](../../../../visual-basic/language-reference/statements/sub-statement.md)
- [대리자](../../../../visual-basic/programming-guide/language-features/delegates/index.md)
- [방법: 프로시저에 Visual Basic에서 다른 프로시저 전달](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)
- [Delegate 문](../../../../visual-basic/language-reference/statements/delegate-statement.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
