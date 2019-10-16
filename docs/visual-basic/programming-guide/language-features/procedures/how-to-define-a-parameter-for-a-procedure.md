---
title: '방법: 프로시저 (Visual Basic)에 대 한 매개 변수를 정의 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- procedure parameters [Visual Basic], defining data types for
- procedures [Visual Basic], parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters [Visual Basic], defining
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
ms.openlocfilehash: bf57d4dbd7e8596396fb2e9099d5984759d6e90d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665375"
---
# <a name="how-to-define-a-parameter-for-a-procedure-visual-basic"></a>방법: 프로시저 (Visual Basic)에 대 한 매개 변수를 정의 합니다.
A *매개 변수* 호출 코드를 호출할 때 프로시저에 값을 전달할 수 있습니다. 동일한 방식으로 변수를 선언 하면 해당 이름 및 데이터 형식을 지정 하는 프로시저에 대 한 각 매개 변수를 선언 합니다. 전달 메커니즘을 지정할 수도 있습니다 및 선택적 매개 변수 인지 합니다.  
  
 자세한 내용은 [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)합니다.  
  
### <a name="to-define-a-procedure-parameter"></a>프로시저 매개 변수를 정의 하려면  
  
1. 프로시저 선언에서 매개 변수 이름이 다른 매개 변수에서 쉼표로 구분 되는 프로시저의 매개 변수 목록에 추가 합니다.  
  
2. 매개 변수의 데이터 형식을 결정 합니다.  
  
3. 매개 변수 이름 뒤에 `As` 절 데이터 형식을 지정 합니다.  
  
4. 매개 변수에 대해 원하는 전달 메커니즘을 결정 합니다. 일반적으로 호출 코드에서 해당 값을 변경할 수 하는 절차를 하려는 경우가 아니면 값으로 매개 변수를 전달 합니다.  
  
5. 매개 변수 이름 앞에 야 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 하거나 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 전달 메커니즘을 지정 합니다. 자세한 내용은 [차이점 간의 값과 By Reference 인수를 전달](./differences-between-passing-an-argument-by-value-and-by-reference.md)합니다.  
  
6. 매개 변수가 선택적 이면 전달 메커니즘을 앞에 야 [선택 사항](../../../../visual-basic/language-reference/modifiers/optional.md) 등호를 사용 하 여 매개 변수 데이터 형식에 따라 (`=`) 및 기본 값입니다.  
  
     개요를 정의 하는 다음 예제는 `Sub` 세 개의 매개 변수를 사용 하 여 프로시저입니다. 처음 두 개는 필수 되며 세 번째 옵션입니다. 매개 변수 선언 매개 변수 목록에 쉼표로 구분 됩니다.  
  
     [!code-vb[VbVbcnProcedures#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#33)]  
  
     첫 번째 매개 변수가 허용을 `customer` 개체 및 `updateCustomer` 전달 되는 변수를 직접 업데이트할 수 있습니다 `c` 인수가 전달 되기 때문에 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)합니다. 프로시저 전달 되므로 마지막 두 인수의 값을 변경할 수 없습니다 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)합니다.  
  
     호출 코드에 대 한 값을 제공 하지 않는 경우는 `level` 매개 변수를 Visual Basic 설정의 기본값은 0입니다.  
  
     형식 검사 스위치 하는 경우 ([Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md))은 `Off`는 `As` 매개 변수를 정의 하는 경우이 절은 선택 사항입니다. 그러나 하나의 매개 변수를 사용 하는 경우는 `As` 절을 모두 사용 해야 합니다. 형식 검사 스위치 이면 `On`, `As` 절은 모든 매개 변수 정의에 필요 합니다.  
  
     모든 프로그래밍 요소에 대 한 데이터 형식을 지정 하는 이라고 *강력한 형식화*합니다. 설정한 경우 `Option Strict On`, Visual Basic 강력한 형식 지정을 적용 합니다. 이 것이 좋습니다 다음과 같은 이유로:  
  
    - 프로그램 변수 및 매개 변수에 대 한 IntelliSense 지원도를 수 있습니다. 이렇게 하면 코드에서 입력할 때 해당 속성 및 기타 멤버를 볼 수 있습니다.  
  
    - 컴파일러를에 형식 검사를 수행할 수 있습니다. 이렇게 하면 런타임에 오버플로 같은 오류로 인해 실패할 수 있는 문을 catch 합니다. 또한 지원 하지 않는 개체에 메서드 호출을 catch 합니다.  
  
    - 코드의 더 빠른 실행에서 발생합니다. 그 이유 중 하나는 프로그래밍 요소에 대 한 데이터 형식을 지정 하지 않으면, Visual Basic 컴파일러를 할당 하는 `Object` 형식입니다. 컴파일된 코드 사이 변환 해야 할 수 `Object` 및 다른 데이터 형식을 사용 하면 성능이 저하 됩니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [Sub 프로시저](./sub-procedures.md)
- [Function 프로시저](./function-procedures.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [재귀 프로시저](./recursive-procedures.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [개체 지향 프로그래밍(Visual Basic)](../../concepts/object-oriented-programming.md)
