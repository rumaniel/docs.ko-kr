---
title: "'<membername>'은(는) 상속된 인터페이스 '<interfacename1>' 및 '<interfacename2>'에서 모호합니다."
ms.date: 07/20/2015
f1_keywords:
- vbc30685
- bc30685
helpviewer_keywords:
- BC30685
ms.assetid: 756add7a-23d5-4b4f-a48d-8297d6459c73
ms.openlocfilehash: 06e0d8863c74041f81977b3187fe99a1d05bcd53
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700888"
---
# <a name="membername-is-ambiguous-across-the-inherited-interfaces-interfacename1-and-interfacename2"></a>' \<membername > '은 (는) 상속 된 인터페이스 ' \<interfacename1 > ' 및 ' \<interfacename2 > '에서 모호 합니다.
인터페이스는 여러 인터페이스에서 이름이 같은 멤버를 두 개 이상 상속 합니다.  
  
 **오류 ID:** BC30685  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 사용 하려는 기본 인터페이스로 값을 캐스팅 합니다. 예를 들어:  
  
    ```vb  
    Interface Left  
        Sub MySub()  
    End Interface  
  
    Interface Right  
        Sub MySub()  
    End Interface  
  
    Interface LeftRight  
        Inherits Left, Right  
    End Interface  
  
    Module test  
        Sub Main()  
            Dim x As LeftRight  
            ' x.MySub()  'x is ambiguous.  
            CType(x, Left).MySub() ' Cast to base type.  
            CType(x, Right).MySub() ' Call the other base type.  
        End Sub  
    End Module  
    ```  
  
## <a name="see-also"></a>참조

- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
