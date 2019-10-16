---
title: '방법: (Visual Basic) 값을 반환 하는 프로시저 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedures [Visual Basic], returning a value
ms.assetid: 8ee19f95-a9ef-4033-963b-d224dca207c4
ms.openlocfilehash: 115c1df4bd49d5848d72c4cbd0242a49a12740c7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61863729"
---
# <a name="how-to-create-a-procedure-that-returns-a-value-visual-basic"></a>방법: (Visual Basic) 값을 반환 하는 프로시저 만들기
사용할를 `Function` 프로시저를 호출 하는 코드에 값을 반환 합니다.  
  
### <a name="to-create-a-procedure-that-returns-a-value"></a>값을 반환 하는 프로시저를 만들려면  
  
1. 다른 프로시저 밖에 서 사용 하 여는 `Function` 문 뒤에 `End Function` 문입니다.  
  
2. 에 `Function` 문을 따릅니다는 `Function` 키워드 이름 절차 및 다음 매개 변수 목록 괄호를 사용 하 여.  
  
3. 괄호 다음에 `As` 절 반환된 된 값의 데이터 형식을 지정 합니다.  
  
4. 간의 프로시저의 코드 문을 배치 합니다 `Function` 및 `End Function` 문입니다.  
  
5. 사용 된 `Return` 호출 코드에 값을 반환 하는 문입니다.  
  
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
- [방법: 프로시저에서 값을 반환 합니다.](./how-to-return-a-value-from-a-procedure.md)
- [방법: 값을 반환 하는 프로시저 호출](./how-to-call-a-procedure-that-returns-a-value.md)
