---
title: '방법: 프로시저 (Visual Basic)에서 값을 반환 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], returning from
- procedures [Visual Basic], returning a value
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
ms.openlocfilehash: 8b53df1634d2b9971bc44c968a17db81cac3924f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61665756"
---
# <a name="how-to-return-a-value-from-a-procedure-visual-basic"></a>방법: 프로시저 (Visual Basic)에서 값을 반환 합니다.
`Function` 프로시저 반환 값 호출 코드를 실행 하 여를 `Return` 문 또는 발생 하는 `Exit Function` 또는 `End Function` 문.  
  
### <a name="to-return-a-value-using-the-return-statement"></a>Return 문을 사용 하 여 값을 반환 하려면  
  
1. 배치는 `Return` 문을 프로시저의 작업이 완료 되는 시점입니다.  
  
2. 수행 합니다 `Return` 호출 코드로 반환 하려는 값을 생성 하는 식으로 키워드입니다.  
  
3. 동일한 프로시저에 `Return` 문을 둘 이상 사용할 수 있습니다.  
  
     다음 `Function` 프로시저 제일 긴 쪽 또는 정삼각형의 빗변을 계산 하 고 호출 코드에 반환 합니다.  
  
     [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]  
  
     다음 예제에서는 일반적인 호출 `hypotenuse`, 반환 된 값을 저장 하는 합니다.  
  
     [!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]  
  
### <a name="to-return-a-value-using-exit-function-or-end-function"></a>Exit 함수 또는 최종 함수를 사용 하 여 값을 반환 하려면  
  
1. 하나 이상의 위치에는 `Function` 프로시저, 프로시저의 이름으로이 값을 할당 합니다.  
  
2. 실행 하는 경우는 `Exit Function` 또는 `End Function` 문, Visual Basic 프로시저의 이름에 가장 최근에 할당 된 값을 반환 합니다.  
  
3. 동일한 프로시저에 `Exit Function` 문을 둘 이상 사용할 수 있으며, `Return` 및 `Exit Function` 문을 혼합할 수도 있습니다.  
  
4. 하나만 사용할 수 있습니다 `End Function` 문에서 `Function` 프로시저입니다.  
  
     자세한 내용 및 예제에 나오는 "반환 값" [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [Sub 프로시저](./sub-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Function 문](../../../../visual-basic/language-reference/statements/function-statement.md)
- [Return 문](../../../../visual-basic/language-reference/statements/return-statement.md)
- [방법: 값을 반환 하는 프로시저 만들기](./how-to-create-a-procedure-that-returns-a-value.md)
- [방법: 값을 반환 하는 프로시저 호출](./how-to-call-a-procedure-that-returns-a-value.md)
