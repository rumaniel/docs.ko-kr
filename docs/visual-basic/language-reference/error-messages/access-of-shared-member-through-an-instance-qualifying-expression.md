---
title: 인스턴스를 통한 공유 멤버 액세스입니다. 정규화 식을 계산하지 않습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc42025
- BC42025
helpviewer_keywords:
- BC42025
ms.assetid: db3337e5-c349-42bf-86df-d9c1e00952a5
ms.openlocfilehash: 773a97c301e7cb5bec0234ae466d487ec9716437
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250342"
---
# <a name="access-of-shared-member-through-an-instance-qualifying-expression-will-not-be-evaluated"></a>인스턴스를 통한 공유 멤버 액세스입니다. 정규화 식을 계산하지 않습니다.

클래스 또는 구조체의 인스턴스 변수는 해당 클래스 또는 구조체에 정의 된 `Shared` 변수, 속성, 프로시저 또는 이벤트에 액세스 하는 데 사용 됩니다. 이 경고는 인스턴스 변수를 사용 하 여 상수, 열거형 또는 중첩 된 클래스 또는 구조체와 같은 클래스 또는 구조체의 암시적으로 공유 되는 멤버에 액세스 하는 경우에도 발생할 수 있습니다.

멤버를 공유 하는 목적은 해당 멤버의 복사본을 하나만 만들고 해당 복사본을 선언 된 클래스 또는 구조체의 모든 인스턴스에서 사용할 수 있도록 하는 것입니다. 이는 해당 클래스 또는 구조체의 개별 인스턴스를 포함 하는 변수를 통하지 않고 클래스 또는 구조체의 이름을 통해 `Shared` 멤버에 액세스 하는 것과 일치 합니다.

인스턴스 변수를 통해 `Shared` 멤버에 액세스 하면 멤버가-1 @no__t 된다는 사실을 감안 하 여 코드를 이해 하기가 더 어려워집니다. 또한 이러한 액세스가 공유 멤버의 인스턴스를 반환 하는 `Function` 프로시저와 같이 다른 동작을 수행 하는 식의 일부인 경우 식 및 다른 작업을 수행 하는 다른 모든 작업을 무시 Visual Basic.  
  
자세한 내용 및 예제는 [공유](../modifiers/shared.md)를 참조 하세요.  
  
이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
**오류 ID:** BC42025  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
다음 예제와 같이 `Shared` 멤버를 정의 하는 클래스 또는 구조체의 이름을 사용 하 여 해당 멤버에 액세스 합니다.
  
```vb
Public Class TestClass
    Public Shared Sub SayHello()
        MsgBox("Hello")
    End Sub
End Class
  
Module Program
    Public Sub Main()  
        ' Access a shared method through an instance variable.  
        ' This generates a warning.  
        Dim tc As New TestClass()
        tc.SayHello()
  
        ' Access a shared method by using the class name.  
        ' This does not generate a warning.  
        TestClass.SayHello()
    End Sub  
End Module  
```  
  
> [!NOTE]
> 두 프로그래밍 요소의 이름이 같을 경우 범위의 효과에 대 한 경고를 생성 합니다. 이전 예제에서 `Dim testClass as testClass = Nothing`을 사용 하 여 인스턴스를 선언 하는 경우 컴파일러는 클래스 이름을 통해 메서드 액세스로 `testClass.sayHello()`에 대 한 호출을 처리 하 고 경고가 발생 하지 않습니다.
  
## <a name="see-also"></a>참조

- [공유](../modifiers/shared.md)
- [Visual Basic 범위](../../programming-guide/language-features/declared-elements/scope.md)
