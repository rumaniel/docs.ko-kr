---
title: 매개 변수와 인수의 차이점(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- parameters [Visual Basic], and arguments
- procedure arguments
- Visual Basic code, procedures
- arguments [Visual Basic], and parameters
- procedure parameters
- parameters [Visual Basic], definition
ms.assetid: c237c056-74f4-4749-9f2c-15864f139a31
ms.openlocfilehash: a69b956c7cffcc2a26916d6fc92f23dd4e2322d7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864249"
---
# <a name="differences-between-parameters-and-arguments-visual-basic"></a>매개 변수와 인수의 차이점(Visual Basic)
대부분의 경우에서 프로시저를 호출한 후 나타나는 상황에 대 한 정보가 있어야 합니다. 반복 또는 공유 작업을 수행 하는 프로시저는 각 호출에 대 한 다른 정보를 사용 합니다. 이 정보는 변수, 상수 및 호출할 때 프로시저에 전달 하는 식으로 구성 됩니다.  
  
 절차로이 정보에 전달 하기 위해 프로시저 정의 *매개 변수*를 호출 코드에서 전달 하 고는 *인수* 해당 매개 변수에. 주차 공간으로 매개 변수 및 인수는 자동차 라고 생각할 수 있습니다. 방금 처럼 다양 한 자동차 수 주차장에 서로 다른 시간에, 호출 코드를 전달할 수 있습니다 다른 인수를 동일한 매개 변수를 프로시저가 호출 될 때마다 합니다.  
  
## <a name="parameters"></a>매개 변수  
 A *매개 변수* 프로시저에는 호출 시 전달할 수 있는 값을 나타냅니다. 해당 매개 변수를 정의 하는 프로시저의 선언입니다.  
  
 정의 하는 경우는 `Function` 또는 `Sub` 지정 프로시저를 *매개 변수 목록* 즉시 프로시저 이름 다음에 괄호로 합니다. 이름, 데이터 형식 및 전달 메커니즘 지정할 각 매개 변수에 대해 ([ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 하거나 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)). 매개 변수가 선택 사항임을 나타낼 수도 있습니다. 즉, 호출 코드에 대 한 값을 전달할 필요가 없습니다.  
  
 각 매개 변수의 이름으로 사용 되는 *지역 변수* 절차에서 합니다. 다른 변수를 사용 하 여 동일한 방식으로 매개 변수 이름을 사용 합니다.  
  
## <a name="arguments"></a>인수  
 *인수* 프로시저를 호출할 때 프로시저 매개 변수에 전달 하는 값을 나타냅니다. 호출 코드는 프로시저를 호출할 때 인수를 제공 합니다.  
  
 호출 하는 경우는 `Function` 또는 `Sub` 포함 하는 절차는 *인수 목록* 즉시 프로시저 이름 다음에 괄호로 합니다. 각 인수 목록의 동일한 위치에서 매개 변수에 해당합니다.  
  
 매개 변수 정의 달리 인수 이름을 갖지 않습니다. 각 인수는 0 이상의 변수, 상수 및 리터럴을 포함할 수 있는 식입니다. 계산된 된 식의 데이터 형식을 해당 매개 변수에 정의 된 데이터 형식과 일치 일반적으로 해야 하 고 어떤 경우이 매개 변수 형식으로 변환할 수 있어야 합니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [Sub 프로시저](./sub-procedures.md)
- [Function 프로시저](./function-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [방법: 프로시저의 매개 변수를 정의 합니다.](./how-to-define-a-parameter-for-a-procedure.md)
- [방법: 프로시저에 인수 전달](./how-to-pass-arguments-to-a-procedure.md)
- [값 또는 참조로 인수 전달](./passing-arguments-by-value-and-by-reference.md)
- [재귀 프로시저](./recursive-procedures.md)
- [프로시저 오버로딩](./procedure-overloading.md)
