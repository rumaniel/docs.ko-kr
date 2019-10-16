---
title: 클래스의 명시적 인스턴스가 없는 공유 메서드 또는 공유 멤버 이니셜라이저에서는 클래스의 인스턴스 멤버를 참조할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30369
- bc30369
helpviewer_keywords:
- Shared
- BC30369
ms.assetid: 39d9466b-c1f3-4406-91a5-3d6c52d23a3d
ms.openlocfilehash: 9b388685299469d5865d57b698e3a66de912fa84
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250200"
---
# <a name="cannot-refer-to-an-instance-member-of-a-class-from-within-a-shared-method-or-shared-member-initializer-without-an-explicit-instance-of-the-class"></a>클래스의 명시적 인스턴스가 없는 공유 메서드 또는 공유 멤버 이니셜라이저에서는 클래스의 인스턴스 멤버를 참조할 수 없습니다.

공유 프로시저 내에서 클래스의 공유 되지 않은 멤버를 참조 하려고 했습니다. 다음 예제에서는 이러한 상황을 보여 줍니다.
  
```vb  
Class Sample
    Public x as Integer  
    Public Shared Sub SetX()
        x = 10  
    End Sub  
End Class  
```  
  
 위의 예제에서 할당 문은-0 @no__t이 오류 메시지를 생성 합니다. 공유 프로시저가 인스턴스 변수에 액세스 하려고 하기 때문입니다.  
  
 변수 `x`은 [Shared](../modifiers/shared.md)로 선언 되지 않았으므로 인스턴스 멤버입니다. @No__t-0 클래스의 각 인스턴스에는-1 @no__t 고유한 개별 변수가 포함 되어 있습니다. 한 인스턴스가 `x` 값을 설정 하거나 변경 하는 경우 다른 인스턴스에서 `x`의 값에 영향을 주지 않습니다.
  
 그러나-0 @no__t 프로시저는 `Sample` 클래스의 모든 인스턴스 사이에 `Shared`입니다. 즉, 클래스의 인스턴스 중 하나에 연결 되어 있지 않고 개별 인스턴스와 독립적으로 작동 합니다. 이 인스턴스에는 특정 인스턴스에 대 한 연결이 없기 때문에 `setX`은 인스턴스 변수에 액세스할 수 없습니다. @No__t-0 변수 에서만 작동 해야 합니다. @No__t-0이 공유 변수의 값을 설정 하거나 변경 하는 경우 클래스의 모든 인스턴스에서 새 값을 사용할 수 있습니다.
  
 **오류 ID:** BC30369
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면
  
1. 멤버가 클래스의 모든 인스턴스 간에 공유 되도록 할지 아니면 각 인스턴스에 대해 개별 항목을 유지할지 결정 합니다.

2. 멤버의 단일 복사본을 모든 인스턴스 간에 공유 하려면 `Shared` 키워드를 멤버 선언에 추가 합니다. 프로시저 선언에서 `Shared` 키워드를 유지 합니다.

3. 각 인스턴스에서 멤버의 개별 복사본을 갖도록 하려면 멤버 선언에 대해 `Shared`을 지정 하지 마십시오. 프로시저 선언에서 `Shared` 키워드를 제거 합니다.
  
## <a name="see-also"></a>참조

- [공유](../modifiers/shared.md)
