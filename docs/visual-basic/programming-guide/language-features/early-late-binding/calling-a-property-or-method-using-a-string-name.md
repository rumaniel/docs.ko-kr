---
title: 문자열 이름을 사용하여 속성 또는 메서드 호출(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- passing operators [Visual Basic]
- strings [Visual Basic], passing new operators as
- objects [Visual Basic], setting properties
- setting properties, object properties at run time
- method calls [Visual Basic], strings
- methods [Visual Basic], calling with string names
- calling methods [Visual Basic], string names
- properties [Visual Basic], setting at run time
- CallByName function
ms.assetid: 79a7b8b4-b8c7-4ad8-aca8-12a9a2b32f03
ms.openlocfilehash: 0683047865f520a09b2d2fe196096286b7d78714
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965392"
---
# <a name="calling-a-property-or-method-using-a-string-name-visual-basic"></a>문자열 이름을 사용하여 속성 또는 메서드 호출(Visual Basic)
대부분의 경우 디자인 타임에 개체의 속성 및 메서드를 검색 하 고이를 처리 하는 코드를 작성할 수 있습니다. 그러나 경우에 따라 개체의 속성 및 메서드를 미리 알지 못할 수도 있고, 최종 사용자가 런타임에 속성을 지정 하거나 메서드를 실행할 수 있도록 하는 유연성을 원합니다.  
  
## <a name="callbyname-function"></a>CallByName 함수  
 예를 들어, COM 구성 요소에 연산자를 전달 하 여 사용자가 입력 한 식을 평가 하는 클라이언트 응용 프로그램을 고려해 야 합니다. 새 연산자가 필요한 구성 요소에 새 함수를 지속적으로 추가 한다고 가정 합니다. 표준 개체 액세스 기술을 사용 하는 경우 새 연산자를 사용 하려면 먼저 클라이언트 응용 프로그램을 다시 컴파일하고 다시 배포 해야 합니다. 이를 방지 하기 위해 함수를 `CallByName` 사용 하 여 응용 프로그램을 변경 하지 않고 새 연산자를 문자열로 전달할 수 있습니다.  
  
 함수 `CallByName` 를 사용 하면 문자열을 사용 하 여 런타임에 속성이 나 메서드를 지정할 수 있습니다. `CallByName` 함수의 시그니처는 다음과 같습니다.  
  
 *Result* = `CallByName`(*Object*, *ProcedureName*, *CallType*, *Arguments*())  
  
 첫 번째 인수인 *object*는 동작 하려는 개체의 이름을 사용 합니다. *E* 인수는 호출할 메서드 또는 속성 프로시저의 이름을 포함 하는 문자열을 사용 합니다. *Calltype* 인수는 메서드 (`Microsoft.VisualBasic.CallType.Method`), 속성 읽기 (`Microsoft.VisualBasic.CallType.Get`) 또는 속성 집합 (`Microsoft.VisualBasic.CallType.Set`)을 호출 하는 프로시저의 형식을 나타내는 상수를 사용 합니다. Optional 인 *arguments* 인수는 프로시저에 대 한 인수를 포함 하 `Object` 는 형식의 배열을 사용 합니다.  
  
 현재 솔루션의 `CallByName` 클래스와 함께을 사용할 수 있지만 대부분의 경우 .NET Framework 어셈블리에서 COM 개체 또는 개체에 액세스 하는 데 사용 됩니다.  
  
 다음 코드와 같이 라는 `MathClass` `SquareRoot`새 함수가 있는 라는 클래스가 포함 된 어셈블리에 대 한 참조를 추가 한다고 가정 합니다.  
  
 [!code-vb[VbVbalrOOP#53](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#53)]  
  
 응용 프로그램은 텍스트 상자 컨트롤을 사용 하 여 호출할 메서드와 해당 인수를 제어할 수 있습니다. 예를 들어에서 `TextBox1` 평가할 식이 포함 되어 있고 `TextBox2` 이 함수 이름을 입력 하는 데 사용 되는 경우 `SquareRoot` 다음 코드를 사용 하 여의 `TextBox1`식에서 함수를 호출할 수 있습니다.  
  
 [!code-vb[VbVbalrOOP#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#54)]  
  
 에서 `TextBox1`"64"를 입력 하 고에서 `TextBox2`"SquareRoot"를 입력 한 다음 `CallMath` 프로시저를 호출 하면에 있는 `TextBox1` 숫자의 제곱근이 계산 됩니다. 예제의 코드는 함수를 `SquareRoot` 호출 합니다 .이 함수는 필요한 인수로 계산 되는 식을 포함 하는 문자열을 사용 하 고는 (64의 제곱근)에서 `TextBox1` "8"을 반환 합니다. 물론, 사용자가에 `TextBox2`잘못 된 문자열을 입력 하는 경우, 문자열에 메서드 대신 속성 이름이 포함 된 경우 또는 메서드에 추가 필수 인수가 있는 경우 런타임 오류가 발생 합니다. 를 사용 `CallByName` 하 여 이러한 오류 또는 다른 오류를 예상할 때 강력한 오류 처리 코드를 추가 해야 합니다.  
  
> [!NOTE]
> 함수는 `CallByName` 경우에 따라 유용 하 게 사용 되지만,를 사용 하면 프로시저를 호출 하는 데를 `CallByName` 사용 하는 것이 런타임에 바인딩된 호출 보다 약간 느리기 때문에 성능이 저하 될 수 있습니다. 루프 내부와 같이 반복적으로 호출 되는 함수를 호출 하는 경우 성능에 `CallByName` 심각한 영향을 미칠 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Interaction.CallByName%2A>
- [개체 형식 확인](../../../../visual-basic/programming-guide/language-features/early-late-binding/determining-object-type.md)
