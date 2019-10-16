---
title: DLL 호출 규칙이 잘못되었습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID49
ms.assetid: 7c7def45-b0ab-450f-ad3f-4383dfd9aed7
ms.openlocfilehash: f7b0c3a6edbe0b950195306fa66287ff9b209bfe
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61935280"
---
# <a name="bad-dll-calling-convention"></a>DLL 호출 규칙이 잘못되었습니다.
인수는 동적 연결 라이브러리 (DLL)에 전달 된 루틴에서 예상 되 정확히 일치 해야 합니다. 호출 규칙 수, 형식 및 인수 순서를 사용 하 여 처리합니다. 프로그램 루틴을 인수 번호 또는 잘못 된 형식이 전달 되는 DLL에서 호출 하 고 있습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 모든 인수 형식을 호출 하는 루틴의 선언에 지정 된 인수와 일치 하는지 확인 합니다.  
  
2. 동일한 호출 하는 루틴의 선언에 지정 된 인수 개수를 전달 하는 있는지 확인 합니다.  
  
3. DLL 루틴에서 인수 값으로 예상 하는 경우 `ByVal` 루틴의 선언에 해당 인수에 지정 합니다.  
  
## <a name="see-also"></a>참고자료

- [오류 형식](../../../visual-basic/programming-guide/language-features/error-types.md)
- [Call 문](../../../visual-basic/language-reference/statements/call-statement.md)
- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
