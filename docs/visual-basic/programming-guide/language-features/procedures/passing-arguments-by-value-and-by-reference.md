---
title: 값 및 참조로 인수 전달(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- ByRef keyword [Visual Basic], passing arguments by reference
- Visual Basic code, procedures
- passing arguments [Visual Basic], by value or by reference
- ByVal keyword [Visual Basic], passing arguments by value
- arguments [Visual Basic], passing by value or by reference
- argument passing [Visual Basic], by value or by reference
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
ms.openlocfilehash: eb2260c6547d4f1cd7d9c23445ac38ac600e3535
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638862"
---
# <a name="passing-arguments-by-value-and-by-reference-visual-basic"></a>값 및 참조로 인수 전달(Visual Basic)
Visual Basic의 프로시저에 인수를 전달할 수 있습니다 *값별로* 하거나 *참조별*합니다. 이 *전달 메커니즘*, 프로시저가 호출 코드에서 인수를 기본 프로그래밍 요소를 수정할 수 있는지 여부를 결정 합니다. 프로시저 선언을 지정 하 여 각 매개 변수의 전달 메커니즘을 결정 합니다 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 하거나 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 키워드입니다.  
  
## <a name="distinctions"></a>차이점  
 프로시저에 인수로 전달할 경우 서로 상호 작용 하는 몇 가지 다른 차이점 고려해 야 합니다.  
  
- 기본 프로그래밍 요소를 수정할 수 있는지 여부  
  
- 인수 자체를 수정할 수 있는지 여부  
  
- 값별 또는 참조별 인수가 전달 되 고 있는지 여부  
  
- 값 형식 또는 참조 형식 인수 데이터 형식 인지  
  
 자세한 내용은 참조 하세요. [수정할 간의 차이점 및 수정할 수 없는 인수](./differences-between-modifiable-and-nonmodifiable-arguments.md) 하 고 [차이 간의 값과 By Reference 인수를 전달](./differences-between-passing-an-argument-by-value-and-by-reference.md)합니다.  
  
## <a name="choice-of-passing-mechanism"></a>전달 메커니즘의 선택  
 각 인수에 대해 신중 하 게 전달 메커니즘을 선택 해야 합니다.  
  
- **보호**합니다. 두 전달 메커니즘 중 하나를 선택할 가장 중요 한 조건을 변경 하려면 변수를 호출 됩니다. 인수를 전달 하는 장점은 `ByRef` 프로시저 해당 인수를 통해 호출 코드에 값을 반환할 수 있다는입니다. 인수를 전달 하는 장점은 `ByVal` 프로시저에 의해 변경 되는 변수를 보호 하는 합니다.  
  
- **성능**합니다. 전달 메커니즘 코드의 성능에 영향을 줄 수 있습니다, 있지만 차이 일반적으로 중요 하지 않습니다. 이 한 가지 예외는 전달 되는 값 형식 `ByVal`합니다. 이 경우 Visual Basic 인수의 전체 데이터 콘텐츠를 복사합니다. 따라서 구조체와 같은 큰 값 형식의 경우이 더 효율적일 수 있습니다 전달 `ByRef`합니다.  
  
     참조 형식에 대 한 데이터에 대 한 포인터만 복사 (4 바이트 32 비트 플랫폼에서는 64 비트 플랫폼에서 8 바이트)입니다. 따라서 형식의 인수를 전달할 수 있습니다 `String` 또는 `Object` 성능 영향을 주지 않고 값으로.  
  
## <a name="determination-of-the-passing-mechanism"></a>전달 메커니즘 확인  
 프로시저 선언 각 매개 변수의 전달 메커니즘을 지정합니다. 호출 코드를 재정의할 수 없습니다는 `ByVal` 메커니즘입니다.  
  
 매개 변수를 사용 하 여 선언 되 면 `ByRef`, 코드를 호출 하는 메커니즘을 강제로 실행할 수 있습니다 `ByVal` 호출에서 괄호 안에 인수 이름을 포함 하 여 합니다. 자세한 내용은 [방법: 값으로 전달 될 인수가](./how-to-force-an-argument-to-be-passed-by-value.md)합니다.  
  
 Visual Basic의 기본값인 값으로 인수 전달 합니다.  
  
## <a name="when-to-pass-an-argument-by-value"></a>값으로 인수를 전달 하는 경우  
  
- 호출 코드 요소가 인수의 기반이 되는 요소를 수정할 수 없는 경우 해당 매개 변수를 선언 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)합니다. 코드 없이 수정할 수 없는 요소의 값을 변경할 수 있습니다.  
  
- 기본 요소는 수정할 수 있지만 해당 값을 변경할 수 하는 절차를 원하지 않는 경우 매개 변수를 선언 `ByVal`합니다. 호출 코드에만 값으로 전달 수정할 수 있는 요소의 값을 변경할 수 있습니다.  
  
## <a name="when-to-pass-an-argument-by-reference"></a>참조로 인수를 전달 하는 경우  
  
- 프로시저에 호출 코드의 내부 요소를 변경 해야 하는 경우 해당 매개 변수를 선언 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)합니다.  
  
- 호출 코드에서 기본 요소를 변경 하는 절차에 따라 올바른 코드를 실행 하는 경우 매개 변수를 선언 `ByRef`합니다. 값으로 전달 하는 경우 또는 호출 코드에서 재정의 하는 경우는 `ByRef` 인수를 괄호로 묶어 전달 메커니즘 프로시저 호출에 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 값으로 인수를 전달 하는 경우 및 참조로 전달 하는 경우를 보여 줍니다. 프로시저 `Calculate` 둘 다 포함 된 `ByVal` 및 `ByRef` 매개 변수입니다. 이자율을 지정 `rate`, 및 금액 합계 `debt`, 프로시저의 작업에 대 한 새 값을 계산 하는 것 `debt` 이자의 원래 값에 적용 한 결과인 `debt`. 때문에 `debt` 되는 `ByRef` 매개 변수를 새 합계에 해당 하는 호출 코드에서 인수 값에 반영 됩니다 `debt`합니다. 매개 변수 `rate` 되는 `ByVal` 매개 변수 때문에 `Calculate` 해당 값을 변경 하지 않아야 합니다.  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbcnProcedures#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class2.vb#74)]  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [방법: 프로시저 인수의 값 변경](./how-to-change-the-value-of-a-procedure-argument.md)
- [방법: 값 변경에 대해 프로시저 인수 보호](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [방법: 인수가 값으로 전달 되도록 설정](./how-to-force-an-argument-to-be-passed-by-value.md)
- [위치 및 이름으로 인수 전달](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
