---
title: 프로시저 매개 변수 및 인수(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], argument lists
- values [Visual Basic], passing to procedures
- arguments [Visual Basic], passing
- procedures [Visual Basic], parameters
- Visual Basic code, argument lists
- Visual Basic code, procedures
- parameters [Visual Basic], Visual Basic procedures
- parameters [Visual Basic], lists
- arguments [Visual Basic], Visual Basic procedures
- arguments [Visual Basic], procedures
- parameter lists [Visual Basic]
- Visual Basic code, parameter lists
- argument lists [Visual Basic]
- procedures [Visual Basic], parameter lists
ms.assetid: ff275aff-aa13-40df-bd4c-63486db8c1e9
ms.openlocfilehash: 08bb05f681d5f795bc448ddc62976d7675696023
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638844"
---
# <a name="procedure-parameters-and-arguments-visual-basic"></a>프로시저 매개 변수 및 인수(Visual Basic)
대부분의 경우 프로시저를 호출한 후 나타나는 상황에 대 한 일부 정보를 해야 합니다. 반복 또는 공유 작업을 수행 하는 프로시저는 각 호출에 대 한 다른 정보를 사용 합니다. 이 정보는 변수, 상수 및 호출할 때 프로시저에 전달 하는 식으로 구성 됩니다.  
  
 A *매개 변수* 프로시저에는 호출할 때 제공 하는 값을 나타냅니다. 해당 매개 변수를 정의 하는 프로시저의 선언입니다.  
  
 매개 변수가 없는, 매개 변수 하나 또는 둘 이상 있는 프로시저를 정의할 수 있습니다. 매개 변수를 지정 하는 프로시저 정의의 일부로 호출 되는 *매개 변수 목록*합니다.  
  
 *인수* 프로시저를 호출할 때 프로시저 매개 변수에 제공한 값을 나타냅니다. 호출 코드는 프로시저를 호출할 때 인수를 제공 합니다. 인수를 지정 하는 프로시저 호출의 일부 라고 합니다 *인수 목록*합니다.  
  
 다음 그림에서는 프로시저를 호출 하는 코드를 보여 줍니다. `safeSquareRoot` 서로 다른 두 위치에서. 변수 값을 전달 하는 첫 번째 호출 `x` (4.0) 매개 변수에 `number`, 및 반환 값은 `root` (2.0) 변수에 할당 된 `y`합니다. 두 번째 호출은 전달에 리터럴 값 9.0 `number`, (3.0) 반환 값을 변수에 할당 합니다 `z`.  
  
 ![매개 변수에 인수를 전달 보여 주는 다이어그램](./media/procedure-parameters-and-arguments/pass-argument-parameter.gif)  
  
 자세한 내용은 [매개 변수 간의 차이점 및 인수](./differences-between-parameters-and-arguments.md)합니다.  
  
## <a name="parameter-data-type"></a>매개 변수 데이터 형식  
 매개 변수의 데이터 형식을 사용 하 여 정의한는 `As` 선언 절. 예를 들어, 다음 함수는 문자열 및 정수를 허용합니다.  
  
 [!code-vb[VbVbcnProcedures#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#32)]  
  
 형식 검사 스위치 하는 경우 ([Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md))은 `Off,` 는 `As` 절은 선택 사항 제외 하 고 하나의 매개 변수를 사용 하는 경우 모든 매개 변수 사용 해야 합니다. 형식 검사가 `On`, `As` 절이 모든 프로시저 매개 변수에 필요 합니다.  
  
 호출 코드에서는 해당 매개 변수를와 다른 데이터 형식과 같은 인수를 제공할 경우 `Byte` 에 `String` 매개 변수를 다음 중 하나를 수행 해야 합니다.  
  
- 인수만 지정 매개 변수 데이터 형식으로 변환할 데이터 형식  
  
- 설정 `Option Strict Off` 암시적 축소 변환을; 수 있도록 또는  
  
- 변환 키워드를 사용 하 여 데이터 형식을 명시적으로 변환 합니다.  
  
### <a name="type-parameters"></a>형식 매개 변수  
 A *제네릭 프로시저* 하나 이상의 정의 *형식 매개 변수* 일반 매개 변수 외에도 합니다. 제네릭 프로시저를 호출 데이터 형식 요구 사항을 각각의 개별 호출은 조정할 수 있도록 프로시저를 호출할 때마다 다른 데이터 형식을 전달 하도록 허용 합니다. [Generic Procedures in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [Sub 프로시저](./sub-procedures.md)
- [Function 프로시저](./function-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [방법: 프로시저의 매개 변수를 정의 합니다.](./how-to-define-a-parameter-for-a-procedure.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [프로시저 오버로딩](./procedure-overloading.md)
- [Visual Basic의 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
