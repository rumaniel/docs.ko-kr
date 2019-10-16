---
title: 스택 공간이 부족합니다(Visual Basic).
ms.date: 07/20/2015
f1_keywords:
- vbrID28
ms.assetid: bfcd792b-ac29-4158-81fc-ea0c13f4ffa2
ms.openlocfilehash: 29dbdf74808fc98bb856483c3fd8e3a09a72113b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61925582"
---
# <a name="out-of-stack-space-visual-basic"></a>스택 공간이 부족합니다(Visual Basic).
스택의는 실행 중인 프로그램의 요구를 사용 하 여 동적으로 메모리 증가 및 축소 하는 작업 영역입니다. 해당 제한은 초과 했습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 프로시저 너무 많이 중첩 되지 않은 확인 합니다.  
  
2. 재귀 프로시저 올바르게 종료 해야 합니다.  
  
3. 로컬 변수 공간이 사용 가능한 것 보다 모듈 수준에서 일부 변수를 선언 해 봅니다. 선언할 수도 있습니다 절차에서는 모든 변수가 정적 앞 합니다 `Property`, `Sub`, 또는 `Function` 키워드를 `Static`입니다. 사용할 수 있습니다는 `Static` 문을 프로시저 내에서 개별 정적 변수를 선언 합니다.  
  
4. 가변 길이 문자열 보다 더 많은 스택 공간을 사용 하는 고정 길이 문자열 가변 길이 문자열로 고정 길이 문자열의 일부를 재정의 합니다. 또한 없는 스택 공간이 요구 되는 모듈 수준에서 문자열을 정의할 수 있습니다.  
  
5. 횟수를 확인 중첩 `DoEvents` 를 사용 하 여 함수 호출을 `Calls` 스택에 활성화 되어 있는 프로시저 보기 대화 상자.  
  
6. "이벤트 cascade" 스택에서 이미 이벤트 프로시저를 호출 하는 이벤트를 트리거하여 발생 하지 있는지 확인 합니다. 종결 되지 않은 재귀 프로시저 호출을 이벤트 캐스케이딩 비슷합니다 이지만 명확 하지 호출 코드에 대 한 명시적 호출 보다는 Visual Basic에서 하므로 합니다. 사용 된 `Calls` 스택에 활성화 되어 있는 프로시저 보기 대화 상자.  
  
## <a name="see-also"></a>참고자료

- [메모리 창](/visualstudio/debugger/memory-windows)
