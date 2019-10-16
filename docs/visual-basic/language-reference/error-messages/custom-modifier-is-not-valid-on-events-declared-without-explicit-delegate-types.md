---
title: 명시적 대리자 형식 없이 선언된 이벤트에는 'Custom' 한정자를 사용할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc31122
- bc31122
helpviewer_keywords:
- BC31122
ms.assetid: 6911f0d1-641a-473b-906d-8ee5681194be
ms.openlocfilehash: 169cb49cc5abc76b7c52785392d0083b81a99450
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61803885"
---
# <a name="custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types"></a>명시적 대리자 형식 없이 선언된 이벤트에는 'Custom' 한정자를 사용할 수 없습니다.
사용자 지정이 아닌 경우와 달리를 `Custom Event` 선언에 필요는 `As` 절과 이벤트에 대 한 대리자 형식을 명시적으로 지정 하는 이벤트 이름입니다.  
  
 비-사용자 지정 이벤트 수 사용 하 여 정의 `As` 절 및 명시적 대리자 형식 또는 매개 변수를 사용 하 여 목록 바로 이벤트 이름 다음에 있습니다.  
  
 **오류 ID:** BC31122  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 사용자 지정 이벤트와 동일한 매개 변수 목록 사용 하 여 대리자를 정의 합니다.  
  
     예를 들어 경우는 `Custom Event` 정의한 `Custom Event Test(ByVal sender As Object, ByVal i As Integer)`, 해당 대리자는 다음 것을 합니다.  
  
     [!code-vb[VbVbalrEventError#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#18)]  
  
2. 대체 매개 변수 목록을 사용 하 여 사용자 지정 이벤트는 `As` 절 대리자 형식을 지정 합니다.  
  
     예를 사용 하 여 계속 `Custom Event` 선언을 다음과 같이 다시 작성할 수는 있습니다.  
  
     [!code-vb[VbVbalrEventError#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#19)]  
  
## <a name="example"></a>예제  
 이 예제에서는 선언 된 `Custom Event` 필요한 지정 `As` 대리자 형식으로는 절.  
  
 [!code-vb[VbVbalrEventError#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#2)]  
  
## <a name="see-also"></a>참고자료

- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)
- [Delegate 문](../../../visual-basic/language-reference/statements/delegate-statement.md)
- [이벤트](../../../visual-basic/programming-guide/language-features/events/index.md)
