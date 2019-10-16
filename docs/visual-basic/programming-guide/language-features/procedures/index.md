---
title: Visual Basic의 프로시저
ms.date: 04/28/2017
helpviewer_keywords:
- procedures [Visual Basic], structured code
- Visual Basic code, procedures
- procedures [Visual Basic], types of
- structured code [Visual Basic], procedures
- procedures
ms.assetid: 9effbcf0-80a0-4d1a-98f4-2c6920592766
ms.openlocfilehash: 4b6dfe30268aef7dc61f130c2775e2cc0d1503e8
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64635624"
---
# <a name="procedures-in-visual-basic"></a>Visual Basic의 프로시저
A *프로시저* 선언문으로 묶은 Visual Basic 문 블록입니다 (`Function`, `Sub`, `Operator`, `Get`, `Set`) 일치 하는 `End` 선언 합니다. Visual Basic의 모든 실행 문은 프로시저 내에 있어야 합니다.  
  
## <a name="calling-a-procedure"></a>프로시저 호출  
 코드에서 다른 위치에 있는 프로시저를 호출합니다. 이것을 *프로시저 호출*이라고 합니다. 프로시저는 실행이 완료되면 자신을 호출한 코드(*호출 코드*라고 함)로 컨트롤을 반환합니다. 호출 코드란 프로시저를 이름으로 지정하고 프로시저에 컨트롤을 전달하는 문 또는 문 내부의 식입니다.  
  
## <a name="returning-from-a-procedure"></a>프로시저에서 반환  
 프로시저는 실행이 완료되면 호출 코드로 컨트롤을 반환합니다. 이를 위해 [Return 문](../../../../visual-basic/language-reference/statements/return-statement.md), 프로시저에 대한 적절한 [Exit 문](../../../../visual-basic/language-reference/statements/exit-statement.md) 또는 프로시저의 [End \<Keyword> 문](../../../../visual-basic/language-reference/statements/end-keyword-statement.md)을 사용할 수 있습니다. 그러면 컨트롤이 호출 코드에서 프로시저 호출 지점 이후로 전달됩니다.  
  
- `Return` 문과 함께 컨트롤이 즉시 호출 코드로 반환됩니다. `Return` 문 이후의 문은 실행되지 않습니다. 동일한 프로시저에 `Return` 문을 둘 이상 사용할 수 있습니다.  
  
- `Exit Sub` 또는 `Exit Function` 문과 함께 컨트롤이 즉시 호출 코드로 반환됩니다. `Exit` 문 이후의 문은 실행되지 않습니다. 동일한 프로시저에 `Exit` 문을 둘 이상 사용할 수 있으며, `Return` 및 `Exit` 문을 혼합할 수도 있습니다.  
  
- `Return` 또는 `Exit` 문이 없는 경우 프로시저는 프로시저 본문의 마지막 문 이후에 `End Sub`나 `End Function`, `End Get`, 또는 `End Set` 문으로 마무리됩니다. `End` 문은 컨트롤을 호출 코드에 즉시 반환합니다. 프로시저에 `End` 문을 하나만 사용할 수 있습니다.  
  
## <a name="parameters-and-arguments"></a>매개 변수 및 인수  
 대부분의 경우 프로시저는 사용자가 호출할 때마다 다른 데이터에서 작동해야 합니다. 프로시저 호출의 일부로 이 정보를 프로시저에 전달할 수 있습니다. 프로시저는 0개 이상의 *매개 변수*를 정의하며, 각 매개 변수는 사용자가 전달할 것으로 예상하는 값을 나타냅니다. 프로시저 정의의 각 매개 변수에 해당하는 것이 프로시저 호출의 *인수*입니다. 인수는 지정된 프로시저 호출에서 해당 매개 변수에 전달하는 값을 나타냅니다.  
  
## <a name="types-of-procedures"></a>프로시저 유형  
 Visual Basic에서는 여러 유형의 프로시저를 사용합니다.  
  
- [Sub 프로시저](./sub-procedures.md)는 작업을 수행하지만 호출 코드에 값을 반환하지 않습니다.  
  
- 이벤트 처리 프로시저는 사용자 작업에 의해 발생하거나 프로그램에서 발생하는 이벤트에 대한 응답으로 실행되는 `Sub` 프로시저입니다.  
  
- [Function 프로시저](./function-procedures.md)는 호출 코드에 값을 반환합니다. 반환하기 전에 다른 작업을 수행할 수 있습니다.

    C#으로 작성된 일부 함수는 *참조 반환 값*을 반환합니다. 함수 호출자는 반환 값을 수정할 수 있으며, 이 수정은 호출된 개체의 상태에 반영됩니다. Visual Basic 2017부터 Visual Basic 코드는 참조 반환 값을 사용할 수는 있지만, 값을 참조로 반환할 수는 없습니다. 자세한 내용은 [참조 반환 값](ref-return-values.md)을 참조하세요.
  
- [Property 프로시저](./property-procedures.md)는 개체 및 모듈에 대한 속성 값을 반환하고 할당합니다.  
  
- [Operator 프로시저](./operator-procedures.md)는 피연산자 중 하나 또는 둘 모두가 새로 정의된 클래스 또는 구조일 때 표준 연산자의 동작을 정의합니다.  
  
- 호출 코드가 호출할 때마다 특정 데이터 유형을 전달할 수 있도록, [Visual Basic의 제네릭 프로시저](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)는 일반 매개 변수 외에도 하나 이상의 *형식 매개 변수*를 정의합니다.  
  
## <a name="procedures-and-structured-code"></a>프로시저 및 구조적 코드  
 애플리케이션의 각 실행 코드 줄은 `Main`, `calculate` 또는 `Button1_Click` 등의 프로시저 내부에 있어야 합니다. 큰 프로시저를 더 작은 프로시저로 세분화하면 애플리케이션을 더 쉽게 읽을 수 있습니다.  
  
 프로시저는 자주 사용되는 계산, 텍스트와 컨트롤 조작, 데이터베이스 작업 등의 반복 또는 공유 작업을 수행하는 데 유용합니다. 코드의 여러 위치에서 프로시저를 호출할 수 있으므로 프로시저를 애플리케이션의 빌딩 블록으로 사용할 수 있습니다.  
  
 프로시저로 코드의 구조를 만들면 다음과 같은 이점이 있습니다.  
  
- 프로시저를 사용하여 프로그램을 개별 논리 단위로 나눌 수 있습니다. 프로시저 없이 전체 프로그램을 디버그하는 것보다는 개별 단위를 디버그하는 것이 더 수월합니다.  
  
- 한 프로그램에서 사용하기 위해 프로시저를 개발한 후, 거의 또는 전혀 수정하지 않고 종종 다른 프로그램에서 사용할 수 있습니다. 이를 통해 코드 중복을 방지할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [방법: 프로시저 만들기](./how-to-create-a-procedure.md)
- [Sub 프로시저](./sub-procedures.md)
- [Function 프로시저](./function-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [재귀 프로시저](./recursive-procedures.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [Generic Procedures in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)
- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
