---
title: 익명 형식 정의(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- anonymous types [Visual Basic], type definition
ms.assetid: 7a8a0ddc-55ba-4d67-869e-87a84d938bac
ms.openlocfilehash: 5f6486965d9e44524420975523e10ded32a135b7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755219"
---
# <a name="anonymous-type-definition-visual-basic"></a>익명 형식 정의(Visual Basic)

무명 형식의 인스턴스 선언에 대 한 응답, 컴파일러는 형식에 대해 지정된 된 속성을 포함 하는 새 클래스 정을 만듭니다.

## <a name="compiler-generated-code"></a>컴파일러에서 생성 된 코드

다음 정의 대 한 `product`, 컴파일러는 속성을 포함 하는 새 클래스 정의 만듭니다 `Name`를 `Price`, 및 `OnHand`합니다.

[!code-vb[VbVbalrAnonymousTypes#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#25)]

클래스 정의 다음과 유사한 속성 정의 포함합니다. 이 없는 `Set` 키 속성에 대 한 메서드. 키 속성의 값은 읽기 전용입니다.

```vb
Public Class $Anonymous1
    Private _name As String
    Private _price As Double
    Private _onHand As Integer
     Public ReadOnly Property Name() As String
        Get
            Return _name
        End Get
    End Property

    Public ReadOnly Property Price() As Double
        Get
            Return _price
        End Get
    End Property

    Public Property OnHand() As Integer
        Get
            Return _onHand
        End Get
        Set(ByVal Value As Integer)
            _onHand = Value
        End Set
    End Property

End Class
```

또한 익명 형식 정의 매개 변수가 없는 생성자를 포함 합니다. 생성자 매개 변수를 필요로 하는 허용 되지 않습니다.

무명 형식 선언에 하나 이상의 키 속성이 포함 된 경우 형식 정의에서 상속 된 세 가지 멤버를 재정의 하는 <xref:System.Object>: <xref:System.Object.Equals%2A>하십시오 <xref:System.Object.GetHashCode%2A>, 및 <xref:System.Object.ToString%2A>합니다. 키 속성이 없는 선언 하는 경우에 <xref:System.Object.ToString%2A> 재정의 됩니다. 재정의 다음 기능을 제공 합니다.

- `Equals` 반환 `True` 두 익명 형식 인스턴스는 동일한 인스턴스 또는 다음 조건을 충족 하는 경우:

  - 동일한 수의 속성을 갖습니다.

  - 동일한 순서로 동일한 이름 가진 속성이 선언 되 고 유추 된 형식입니다. 이름 비교는 대/소문자 구분 하지 않습니다.

  - 키 속성은 하나 이상의 속성 및 `Key` 키워드 동일한 속성에 적용 됩니다.

  - 키 속성의 각 해당 쌍의 비교 반환 `True`합니다.

    다음 예제에서 예를 들어 `Equals` 반환 `True` 동안만 `employee01` 및 `employee08`합니다. 새 인스턴스를 일치 하지 않습니다 이유를 지정 하는 각 줄 앞의 주석이 `employee01`합니다.

    [!code-vb[VbVbalrAnonymousTypes#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#24)]

- `GetHashcode` 적절 하 게 고유 GetHashCode 알고리즘을 제공합니다. 알고리즘의 해시 코드를 계산 합니다. 키 속성만 사용 합니다.

- `ToString` 다음 예제에서와 같이 연결 된 속성 값의 문자열을 반환 합니다. 키 및 키가 아닌 속성을 모두 포함 됩니다.

  [!code-vb[VbVbalrAnonymousTypes#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#29)]

익명 형식의 명시적으로 명명 된 속성은 이러한 생성 된 메서드와 충돌 하지 않습니다. 즉, 사용할 수 없습니다 `.Equals`, `.GetHashCode`, 또는 `.ToString` 속성 이름을 지정 합니다.

하나 이상 포함 하는 익명 형식 정의 키 속성이 구현 합니다 <xref:System.IEquatable%601?displayProperty=nameWithType> 인터페이스를 여기서 `T` 무명 형식의 형식입니다.

> [!NOTE]
> 무명 형식 선언 동일한 어셈블리에서 발생 하는, 해당 속성에 동일한 이름을 가진 및 유추 된 형식, 동일한 순서로 속성이 선언 되 고 동일한 속성이 키 속성으로 표시 된 경우에 같은 익명 형식을 만듭니다.

## <a name="see-also"></a>참고자료

- [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [방법: 무명 형식 선언에서 속성 이름 및 형식 유추](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
