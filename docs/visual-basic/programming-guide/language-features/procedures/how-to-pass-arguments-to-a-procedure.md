---
title: '방법: (Visual Basic) 프로시저에 인수 전달'
ms.date: 07/20/2015
helpviewer_keywords:
- arguments [Visual Basic], passing to procedures
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], calling
- argument passing [Visual Basic], procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
ms.openlocfilehash: 012ad8e6229958575030ee820a3b0b79cc50facc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61863443"
---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a>방법: (Visual Basic) 프로시저에 인수 전달
프로시저를 호출 하는 경우에 인수 목록 괄호로 묶어 프로시저 이름을 뒤에 있습니다. 프로시저에 정의 하는 모든 필수 매개 변수에 해당 하는 인수를 제공 하 고 인수를 선택적으로 제공할 수는 `Optional` 매개 변수입니다. 지정 하지 않으면 경우는 `Optional` 호출에서 매개 변수를 후속 인수를 제공 하는 경우 인수 목록에서 해당 위치를 표시 하려면 쉼표를 포함 해야 합니다.  
  
 와 같은 데이터 형식의 인수는 해당 매개 변수를 다른 전달 하려는 경우 `Byte` 하 `String`, 형식 검사 스위치를 설정할 수 있습니다 ([Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md))를 `Off`입니다. 경우 `Option Strict` 는 `On`, 하나를 사용 해야 변환이 나 명시적 변환 키워드를 확대 합니다. 자세한 내용은 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) 하 고 [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)합니다.  
  
 자세한 내용은 [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)합니다.  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a>프로시저에 하나 이상의 인수를 전달 하려면  
  
1. 호출 문에서 괄호를 사용 하 여 프로시저 이름 뒤에.  
  
2. 괄호 안에 인수 목록에 배치 합니다. 프로시저에 정의 필요한 각 매개 변수에 대 한 인수를 포함 하 고 쉼표를 사용 하 여 인수를 구분 합니다.  
  
3. 각 인수는 해당 매개 변수의 데이터 형식 변환할 프로시저 형식으로 계산 되는 유효한 식 정의 해야 합니다.  
  
4. 매개 변수가 정의 되어 있으면 [선택 사항](../../../../visual-basic/language-reference/modifiers/optional.md), 인수 목록에 포함 하거나 생략할 수 있습니다. 를 생략 하면 프로시저 매개 변수에 대해 정의 된 기본값을 사용 합니다.  
  
5. 에 대 한 인수를 생략 하면는 `Optional` 매개 변수 및 매개 변수 목록 뒤에 다른 매개 변수가 있는, 인수 목록에 추가 쉼표는 생략 된 인수의 위치를 표시할 수 있습니다.  
  
     다음 예제에서는 Visual Basic <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 함수입니다.  
  
     [!code-vb[VbVbcnProcedures#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#34)]  
  
     앞의 예제에 표시 될 메시지 문자열은 필요한 첫 번째 인수를 제공 합니다. 메시지 상자에 표시할 단추를 지정 하는 선택적 두 번째 매개 변수에 대 한 인수를 생략 합니다. 호출에 값을 제공 하지 않는 있으므로 `MsgBox` 기본값을 사용 하 여 `MsgBoxStyle.OKOnly`만 표시는 **확인** 단추.  
  
     인수 목록에 있는 두 번째 쉼표는 생략 된 두 번째 인수의 위치를 표시 하 고 마지막 문자열의 선택적 세 번째 매개 변수에 전달 됩니다 `MsgBox`, 제목 표시줄에 표시할 텍스트는 합니다.  
  
## <a name="see-also"></a>참고자료

- [Sub 프로시저](./sub-procedures.md)
- [Function 프로시저](./function-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [방법: 프로시저의 매개 변수를 정의 합니다.](./how-to-define-a-parameter-for-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [재귀 프로시저](./recursive-procedures.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [개체 지향 프로그래밍(Visual Basic)](../../concepts/object-oriented-programming.md)
