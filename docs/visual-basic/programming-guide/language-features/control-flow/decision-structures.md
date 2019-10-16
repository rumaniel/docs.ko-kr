---
title: 판단 구조(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- statements [Visual Basic], control flow
- If statement [Visual Basic], decision structures
- If statement [Visual Basic], If...Then...Else
- control flow [Visual Basic], decision structures
- decision structures [Visual Basic]
- conditional statements [Visual Basic], decision structures
ms.assetid: 2e2e0895-4483-442a-b17c-26aead751ec2
ms.openlocfilehash: f0df649c4be50e9cadd51258c89137b68b4ffe22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963194"
---
# <a name="decision-structures-visual-basic"></a>판단 구조(Visual Basic)
Visual Basic를 사용 하면 조건을 테스트 하 고 해당 테스트의 결과에 따라 다른 작업을 수행할 수 있습니다. 조건에 대해 true 또는 false, 식의 다양 한 값 또는 일련의 문을 실행할 때 생성 되는 다양 한 예외에 대해 테스트할 수 있습니다.  
  
 다음 그림은 조건이 true 인지 false 인지에 따라 조건이 true 인지 테스트 하 고 다른 작업을 수행 하는 의사 결정 구조를 보여 줍니다.  
  
 ![... 인 경우의 순서도 그런 다음 ... Else 생성.](./media/decision-structures/if-then-else-construction.gif)  
  
## <a name="ifthenelse-construction"></a>... 그런 다음 ... Else 생성  
 `If...Then...Else`구문을 사용 하면 하나 이상의 조건을 테스트 하 고 각 조건에 따라 하나 이상의 문을 실행할 수 있습니다. 조건을 테스트 하 고 다음과 같은 방법으로 작업을 수행할 수 있습니다.  
  
- 조건이 인 경우 하나 이상의 문을 실행 합니다.`True`  
  
- 조건이 인 경우 하나 이상의 문을 실행 합니다.`False`  
  
- 조건이 이면 다른 문을 실행 `True` 하 고, 그렇지 않은 경우 다른 문을 실행 합니다.`False`  
  
- 이전 조건이 인 경우 추가 조건 테스트`False`  
  
 이러한 모든 가능성을 제공 하는 컨트롤 구조는 다음과 같은 경우입니다. [ 그런 다음 ... Else 문](../../../../visual-basic/language-reference/statements/if-then-else-statement.md). 하나의 테스트와 한 개의 문이 실행 되는 경우 한 줄 버전을 사용할 수 있습니다. 더 복잡 한 조건 및 동작 집합이 있는 경우 여러 줄 버전을 사용할 수 있습니다.  
  
## <a name="selectcase-construction"></a>...를 선택 합니다. 사례 생성  
 이 `Select...Case` 구문을 사용 하면 식을 한 번 계산 하 고 가능한 다른 값에 따라 다른 문 집합을 실행할 수 있습니다. 자세한 내용은 Select ...를 참조 하세요. [ Case 문](../../../../visual-basic/language-reference/statements/select-case-statement.md).  
  
## <a name="trycatchfinally-construction"></a>Try ... Catch ... Finally 생성  
 `Try...Catch...Finally`구문을 사용 하 여 문 중 하나에서 예외가 발생 하는 경우 제어를 유지 하는 환경에서 문 집합을 실행할 수 있습니다. 다른 예외에 대해 다른 작업을 수행할 수 있습니다. 필요에 관계 없이 전체 `Try...Catch...Finally` 생성을 끝내기 전에 실행 되는 코드 블록을 선택적으로 지정할 수 있습니다. 자세한 내용은 [Try...Catch...Finally 문](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)을 참조하세요.  
  
> [!NOTE]
> 많은 컨트롤 구조에서 키워드를 클릭 하면 구조에 있는 모든 키워드가 강조 표시 됩니다. `If` 예를 들어, `If...Then...Else` 생성을 클릭 하면 생성에서, `ElseIf` `Then`,, `If` `Else`및 `End If` 의 모든 인스턴스가 강조 표시 됩니다. 다음 또는 이전 강조 표시 된 키워드로 이동 하려면 CTRL + SHIFT + 아래쪽 화살표 또는 CTRL + SHIFT + 위쪽 화살표를 누릅니다.  
  
## <a name="see-also"></a>참고자료

- [제어 흐름](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)
- [루프 구조](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)
- [기타 제어 구조](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)
- [중첩 제어 구조](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [If 연산자](../../../../visual-basic/language-reference/operators/if-operator.md)
