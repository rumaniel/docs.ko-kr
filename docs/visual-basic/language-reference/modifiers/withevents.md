---
title: WithEvents(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.WithEvents
- WithEvents
helpviewer_keywords:
- WithEvents keyword [Visual Basic]
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
ms.openlocfilehash: e8a8fb571fa65228f3a0acec1f902d21eb9bfe04
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268311"
---
# <a name="withevents-visual-basic"></a>WithEvents(Visual Basic)
하나 이상의 선언 된 멤버 변수가 이벤트를 발생 시킬 수 있는 클래스의 인스턴스 참조 하는지를 지정 합니다.  
  
## <a name="remarks"></a>설명  
 변수를 사용 하 여 정의 되 면 `WithEvents`에 메서드를 사용 하 여 변수의 이벤트를 처리 하는 선언적으로 지정할 수 있습니다는 `Handles` 키워드입니다.  
  
 사용할 수 있습니다 `WithEvents` 클래스 또는 모듈 수준 에서만. 즉, 선언 컨텍스트는 `WithEvents` 변수 클래스 또는 모듈 이어야 하며 원본 파일, 네임 스페이스, 구조체 또는 프로시저 일 수 없습니다.  
  
 사용할 수 없습니다 `WithEvents` 구조체 멤버입니다.  
  
 개별 변수만 선언할 수 있습니다-하지 배열-사용 하 여 `WithEvents`입니다.  
  
## <a name="rules"></a>규칙  
  
- **요소 형식입니다.** 선언 해야 `WithEvents` 을 받을 수 있도록 개체 변수를 변수 클래스 인스턴스. 그러나로 선언할 수 없습니다 `Object`합니다. 이벤트를 발생 시킬 수 있는 특정 클래스로 선언 해야 합니다.  
  
 `WithEvents` 한정자는이 컨텍스트에서 사용할 수 있습니다. [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)  
 
## <a name="example"></a>예제

```VB
Dim WithEvents app As Application
```
  
## <a name="see-also"></a>참고자료

- [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)
- [C++ 키워드](../../../visual-basic/language-reference/keywords/index.md)
- [이벤트](../../../visual-basic/programming-guide/language-features/events/index.md)
