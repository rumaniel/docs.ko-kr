---
title: <type1>'<typename>'은 '<interfacename>' 인터페이스에 대한 '<membername>'을 구현해야 합니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30154
- bc30154
helpviewer_keywords:
- BC30154
ms.assetid: 259afdfa-3608-4760-adcb-88ec0da5020d
ms.openlocfilehash: a824b66eaad964049ced5cae5eb2cc370d00ba7f
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696888"
---
# <a name="type1typename-must-implement-membername-for-interface-interfacename"></a>\<type1 > ' \<typename > '은 (는) ' \<interfacename > ' 인터페이스에 대해 ' \<membername > '를 구현 해야 합니다.
' \<typename > '은 (는) ' \<interfacename > ' 인터페이스에 대해 ' \<membername > '을 구현 해야 합니다. 구현 속성에 일치 하는 ' ReadOnly '/' WriteOnly ' 지정 자가 있어야 합니다.  
  
 클래스 또는 구조체는 인터페이스를 구현 하지만 인터페이스에 의해 정의 된 프로시저, 속성 또는 이벤트를 구현 하지는 않습니다. 인터페이스의 모든 멤버를 구현 해야 합니다.  
  
 **오류 ID:** BC30154  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 인터페이스에 정의 된 것과 동일한 이름 및 서명을 사용 하 여 멤버를 선언 합니다. 적어도 `End Function`, `End Sub` 또는 `End Property` 문을 포함 해야 합니다.  
  
2. @No__t-1, `Sub`, `Property` 또는 @no__t 문의 끝에 `Implements` 절을 추가 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
    ```vb  
    Public Event ItHappened() Implements IBaseInterface.ItHappened  
    ```  
  
3. 속성을 구현할 때 `ReadOnly` 또는 `WriteOnly`이 인터페이스 정의에서와 동일한 방식으로 사용 되는지 확인 합니다.  
  
4. 속성을 구현 하는 경우 `Get` 및 `Set` 프로시저를 적절 하 게 선언 합니다.  
  
## <a name="see-also"></a>참조

- [Implements 문](../../../visual-basic/language-reference/statements/implements-statement.md)
- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
