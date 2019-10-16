---
title: '방법: (Visual Basic) 값으로 전달 될 인수가 설정'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures [Visual Basic], calling
- arguments [Visual Basic], in parentheses
- procedure arguments [Visual Basic], in parentheses
- arguments [Visual Basic], changing value
ms.assetid: 77b4f2d2-1055-4c2f-a521-874d1db86946
ms.openlocfilehash: 540271c414ac295c419533a4622657d60d123796
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665390"
---
# <a name="how-to-force-an-argument-to-be-passed-by-value-visual-basic"></a>방법: (Visual Basic) 값으로 전달 될 인수가 설정
프로시저 선언 전달 메커니즘을 결정 합니다. 매개 변수 선언 되 면 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), Visual Basic는 해당 인수가 참조로 전달 하려면 필요 합니다. 이렇게 하면 인수의 기반이 되는 호출 코드에서 프로그래밍 요소의 값을 변경 하는 절차입니다. 이러한 변경에 대 한 내부 요소를 보호 하려는 경우 재정의할 수 있습니다는 `ByRef` 인수 이름을 괄호로 묶어 전달 메커니즘 프로시저에서 호출 합니다. 이 괄호는 호출의 인수 목록을 묶는 괄호는 별개입니다.  
  
 호출 코드를 재정의할 수 없습니다는 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 메커니즘입니다.  
  
### <a name="to-force-an-argument-to-be-passed-by-value"></a>인수가 값으로 전달 되도록 설정 하려면  
  
- 해당 매개 변수가 선언 된 경우 `ByVal` 절차에서는 않아도 모든 추가 단계를 수행 합니다. Visual Basic은 이미 인수를 값별로 전달 하려면 필요 합니다.  
  
- 해당 매개 변수가 선언 된 경우 `ByRef` 절차에서는 프로시저 호출에서 괄호 안에 인수를 묶습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 재정의 `ByRef` 매개 변수를 선언 합니다. 인하도록 강제 하는 호출에서 `ByVal`를 중첩 괄호 유의 합니다.  
  
 [!code-vb[VbVbcnProcedures#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#39)]  
  
 [!code-vb[VbVbcnProcedures#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#40)]  
  
 때 `str` 인수 목록에 추가 괄호로 묶인 합니다 `setNewString` 프로시저가 호출 코드에서 해당 값을 변경할 수 없습니다 및 `MsgBox` "바꿀 수 없습니다 byval로 전달 하는 경우"를 표시 합니다. 때 `str` 묶여 있지 않은 추가 괄호 안의 프로시저를 변경할 수 및 `MsgBox` "inString 인수에 대 한 새 값입니다."를 표시 합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 참조로 변수를 전달 하는 경우 사용 해야는 `ByRef` 키워드가이 메커니즘을 지정 합니다.  
  
 Visual Basic의 기본값인 값으로 인수 전달 합니다. 그러나는 것이 좋은 프로그래밍 방법 중 하나를 포함 하는 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 또는 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 키워드 선언 된 모든 매개 변수를 사용 합니다. 이렇게 하면 코드를 쉽게 읽을 수 있습니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 프로시저 매개 변수를 선언 하는 경우 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)를 올바르게 실행 되는 코드의 호출 코드의 내부 요소를 변경할 수 있는지에 따라 달라질 수 있습니다. 호출 코드에서 인수를 괄호로 묶어이 호출 하는 메커니즘을 재정의 하거나 수정할 수 없는 인수를 전달 하는 경우 프로시저는 내부 요소를 변경할 수 없습니다. 이 호출 코드에서 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 호출 코드에서 인수를 기본 값을 변경 하는 절차를 허용할 위험할은 항상 있습니다. 원하는이 값이 변경 되 고 사용 하기 전에 유효성을 검사할 준비가 되어 있는지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [수정할 수 있는 인수와 수정할 수 없는 인수 사이의 차이점](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [인수를 값으로 전달할 때와 참조로 전달할 때의 차이점](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [방법: 프로시저 인수의 값 변경](./how-to-change-the-value-of-a-procedure-argument.md)
- [방법: 값 변경에 대해 프로시저 인수 보호](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [위치 및 이름으로 인수 전달](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
