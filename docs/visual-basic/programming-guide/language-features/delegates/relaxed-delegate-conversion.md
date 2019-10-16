---
title: 완화된 대리자 변환(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- relaxed delegate conversion [Visual Basic]
- delegates [Visual Basic], relaxed conversion
- conversions [Visual Basic], relaxed delegate
ms.assetid: 64f371d0-5416-4f65-b23b-adcbf556e81c
ms.openlocfilehash: ac1246764d26d694d10b817b9195b13169d6d9be
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651261"
---
# <a name="relaxed-delegate-conversion-visual-basic"></a>완화된 대리자 변환(Visual Basic)
완화 된 대리자 변환을 사용 하면 해당 시그니처가 동일 하지 않은 경우에 대리자 또는 처리기에 sub 및 함수를 할당할 수 있습니다. 따라서 대리자를 바인딩할 메서드 호출을 이미 허용 바인딩을 사용 하 여 일치 됩니다.  
  
## <a name="parameters-and-return-type"></a>매개 변수 및 반환 형식  
 낮은 수준의 변환을 서명이 완전히 일치 하는 대신 다음 조건이 충족 되어야 필요한 경우 `Option Strict` 로 설정 된 `On`:  
  
- 할당 된 함수의 해당 매개 변수의 데이터 형식으로 각 대리자 매개 변수의 데이터 형식에서 확대 변환이 있어야 하거나 `Sub`합니다. 다음 예제에서는 대리자 `Del1` 하나의 매개 변수가 `Integer`합니다. 매개 변수 `m` 할당 된 람다 식에서 확대 변환이 없는 데이터 형식이 있어야 `Integer`와 같은 `Long` 또는 `Double`합니다.  
  
     [!code-vb[VbVbalrRelaxedDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#1)]  
  
     [!code-vb[VbVbalrRelaxedDelegates#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#2)]  
  
     축소 변환은 경우에만 허용 됩니다 `Option Strict` 로 설정 된 `Off`합니다.  
  
     [!code-vb[VbVbalrRelaxedDelegates#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#8)]  
  
- 할당 된 함수의 반환 형식에서 반대 방향으로의 확대 변환이 있어야 합니다. 또는 `Sub` 대리자의 반환 형식입니다. 다음 예제에서 각 할당 된 람다 식의 본문으로 확대 되는 데이터 형식으로 계산 되어야 `Integer` 의 반환 형식인 `del1` 는 `Integer`합니다.  
  
     [!code-vb[VbVbalrRelaxedDelegates#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#3)]  
  
 하는 경우 `Option Strict` 로 설정 된 `Off`는 양쪽 방향에서 제거 되었습니다 제한 확대 합니다.  
  
 [!code-vb[VbVbalrRelaxedDelegates#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#4)]  
  
## <a name="omitting-parameter-specifications"></a>매개 변수 사양 생략  
 완화 된 대리자는 할당 된 메서드의 매개 변수 사양을 완전히 생략할 수 있습니다.  
  
 [!code-vb[VbVbalrRelaxedDelegates#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#5)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#6)]  
  
 참고 일부 매개 변수를 지정 및 다른 사용자를 생략할 수 없습니다.  
  
 [!code-vb[VbVbalrRelaxedDelegates#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#15)]  
  
 매개 변수를 생략할 수 있는 몇 가지 복잡 한 매개 변수 관련 된 이벤트 처리기를 정의 하는 경우에 유용 합니다. 일부 이벤트 처리기에 대 한 인수를 사용 하지 않습니다. 대신, 처리기는 이벤트가 등록 되 고 인수를 무시 하는 컨트롤의 상태를 직접 액세스 합니다. 완화 된 대리자를 사용 하면 모호성이 없는 이러한 선언에서 인수를 생략할 수 있습니다. 다음 예제에서는 완벽 하 게 지정된 된 메서드 `OnClick` 다시 작성할 수 있습니다 `RelaxedOnClick`합니다.  
  
```vb  
Sub OnClick(ByVal sender As Object, ByVal e As EventArgs) Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
  
Sub RelaxedOnClick() Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
```  
  
## <a name="addressof-examples"></a>AddressOf 예제  
 람다 식은 형식 관계를 쉽게 확인할 수 있도록 이전 예제에서 사용 됩니다. 그러나 동일한 relaxation을 사용 하는 대리자 할당 허용 되 `AddressOf`, `Handles`, 또는 `AddHandler`합니다.  
  
 다음 예제에서는 함수 `f1`, `f2`를 `f3`, 및 `f4` 모두에 할당할 수 있습니다 `Del1`합니다.  
  
 [!code-vb[VbVbalrRelaxedDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#7)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#9)]  
  
 다음 예제는 경우에만 유효 `Option Strict` 로 설정 된 `Off`합니다.  
  
 [!code-vb[VbVbalrRelaxedDelegates#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#14)]  
  
## <a name="dropping-function-returns"></a>함수 반환 값 삭제  
 완화 된 대리자 변환을 사용 하면 함수를 할당 하는 `Sub` 대리자를 효과적으로 함수의 반환 값을 무시 합니다. 그러나 할당할 수 없습니다를 `Sub` 함수 대리자입니다. 다음 예제에서는 함수의 주소로 `doubler` 에 할당 됩니다 `Sub` 대리자 `Del3`합니다.  
  
 [!code-vb[VbVbalrRelaxedDelegates#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#10)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#11)]  
  
## <a name="see-also"></a>참고자료

- [람다 식](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
- [확대 변환과 축소 변환](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [대리자](../../../../visual-basic/programming-guide/language-features/delegates/index.md)
- [방법: 프로시저에 Visual Basic에서 다른 프로시저 전달](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
