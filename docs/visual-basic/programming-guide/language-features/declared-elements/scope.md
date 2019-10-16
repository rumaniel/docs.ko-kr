---
title: Visual Basic의 범위
ms.date: 07/20/2015
helpviewer_keywords:
- module scope [Visual Basic]
- scope [Visual Basic], levels
- module level
- procedures [Visual Basic], scope
- declared elements [Visual Basic], scope
- namespaces [Visual Basic], scope
- scope [Visual Basic], declared elements
- scope [Visual Basic], about scope
- levels of scope [Visual Basic]
- block scope [Visual Basic]
- scope [Visual Basic], Visual Basic
- procedure scope [Visual Basic]
ms.assetid: 208106fe-79c9-4eec-93c6-55f08548895f
ms.openlocfilehash: 7f7e32d6ac838e250c260987d3d5c375f8697c45
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512859"
---
# <a name="scope-in-visual-basic"></a>Visual Basic의 범위

선언 된 요소의 *범위* 는 이름을 한정 하거나 [Imports 문 (.net 네임 스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)을 통해 사용할 수 있도록 하는 것을 제외 하 고이를 참조할 수 있는 모든 코드 집합입니다. 요소는 다음 수준 중 하나에서 범위를 가질 수 있습니다.

|Level|설명|
|-----------|-----------------|
|블록 범위|선언 된 코드 블록 내 에서만 사용할 수 있습니다.|
|프로시저 범위|선언 된 프로시저 내의 모든 코드에서 사용할 수 있습니다.|
|모듈 범위|선언 된 모듈, 클래스 또는 구조체 내의 모든 코드에서 사용할 수 있습니다.|
|네임 스페이스 범위|선언 된 네임 스페이스의 모든 코드에서 사용할 수 있습니다.|

이러한 범위의 범위는 가장 좁은 (블록)에서 가장 넓은 (네임 스페이스)로 진행 됩니다. 여기서 가장 작은 *범위* 는 한정자 없이 요소를 참조할 수 있는 가장 작은 코드 집합을 의미 합니다. 자세한 내용은이 페이지의 "범위 수준"을 참조 하세요.

## <a name="specifying-scope-and-defining-variables"></a>범위 지정 및 변수 정의

요소를 선언할 때 요소의 범위를 지정 합니다. 범위는 다음 요인에 따라 달라질 수 있습니다.

- 요소를 선언 하는 영역 (블록, 프로시저, 모듈, 클래스 또는 구조체)

- 요소의 선언이 포함 된 네임 스페이스입니다.

- 요소에 대해 선언 하는 액세스 수준입니다.

이름은 같지만 범위가 다른 변수를 정의할 때 주의 해야 합니다. 이렇게 하면 예기치 않은 결과가 발생할 수 있기 때문입니다. 자세한 내용은 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)을 참조하세요.

## <a name="levels-of-scope"></a>범위 수준

프로그래밍 요소는 선언 하는 지역 전체에서 사용할 수 있습니다. 동일한 지역의 모든 코드는 이름을 한정 하지 않고 요소를 참조할 수 있습니다.

### <a name="block-scope"></a>블록 범위

블록은 다음과 같은 시작 및 종료 선언 문 내에 포함 된 문의 집합입니다.

- `Do` 및 `Loop`

- `For`[`Each`] 및`Next`

- `If` 및 `End If`

- `Select` 및 `End Select`

- `SyncLock` 및 `End SyncLock`

- `Try` 및 `End Try`

- `While` 및 `End While`

- `With` 및 `End With`

블록 내에서 변수를 선언 하는 경우 해당 블록 내 에서만 사용할 수 있습니다. 다음 예제에서 `cube` 정수 변수의 범위는와 `End If`사이의 `If` 블록 이며 실행이 블록 밖으로 전달 되는 경우를 `cube` 더 이상 참조할 수 없습니다.

```vb
If n < 1291 Then
    Dim cube As Integer
    cube = n ^ 3
End If
```

> [!NOTE]
> 변수의 범위가 블록으로 제한 되는 경우에도 여전히 전체 프로시저의 수명입니다. 프로시저를 실행 하는 동안 블록을 두 번 이상 입력 하는 경우 각 블록 변수는 이전 값을 유지 합니다. 이러한 경우 예기치 않은 결과를 방지 하기 위해 블록의 시작 부분에서 블록 변수를 초기화 하는 것이 좋습니다.

### <a name="procedure-scope"></a>프로시저 범위

프로시저 내에서 선언 된 요소는 해당 프로시저 외부에서 사용할 수 없습니다. 선언을 포함 하는 프로시저만이 프로시저를 사용할 수 있습니다. 이 수준의 변수는 *지역 변수*라고도 합니다. [Static](../../../../visual-basic/language-reference/modifiers/static.md) 키워드를 사용 하거나 사용 하지 않고 [Dim 문으로](../../../../visual-basic/language-reference/statements/dim-statement.md)선언 합니다.

프로시저 및 블록 범위는 밀접 하 게 관련 되어 있습니다. 프로시저 내에서 변수를 선언 하 고 해당 프로시저 내의 블록 외부에서 변수를 선언 하는 경우 해당 변수는 블록 범위가 있는 것으로 간주할 수 있습니다. 여기서 블록은 전체 프로시저입니다.

> [!NOTE]
> `Static` 변수가 있는 경우에도 모든 로컬 요소는 해당 요소가 표시 되는 프로시저에 전용입니다. 프로시저 내에서 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 키워드를 사용 하 여 요소를 선언할 수 없습니다.

### <a name="module-scope"></a>모듈 범위

편의를 위해 모듈, 클래스 및 구조에는 단일 용어 *모듈 수준이* 동일 하 게 적용 됩니다. 선언 문을 프로시저 또는 블록 외부에 배치 하 고 모듈, 클래스 또는 구조체 내에 배치 하 여이 수준에서 요소를 선언할 수 있습니다.

모듈 수준에서 선언을 만들면 선택 하는 액세스 수준에 따라 범위가 결정 됩니다. 모듈, 클래스 또는 구조가 포함 된 네임 스페이스도 범위에 영향을 줍니다.

[Private](../../../../visual-basic/language-reference/modifiers/private.md) 액세스 수준을 선언 하는 요소는 해당 모듈의 모든 프로시저에서 사용할 수 있지만 다른 모듈의 코드에는 사용할 수 없습니다. 액세스 수준 키워드를 사용 하지 않는 `Private` 경우 모듈 수준의 문은기본적으로로설정됩니다.`Dim` 그러나 `Private` `Dim` 문에 키워드를 사용 하 여 범위 및 액세스 수준을 보다 명확 하 게 만들 수 있습니다.

다음 예에서는 모듈에 정의 된 모든 프로시저가 문자열 변수 `strMsg`를 참조할 수 있습니다. 두 번째 프로시저가 호출 되 면 대화 상자에 문자열 변수의 `strMsg` 내용이 표시 됩니다.

```vb
' Put the following declaration at module level (not in any procedure).
Private strMsg As String
' Put the following Sub procedure in the same module.
Sub initializePrivateVariable()
    strMsg = "This variable cannot be used outside this module."
End Sub
' Put the following Sub procedure in the same module.
Sub usePrivateVariable()
    MsgBox(strMsg)
End Sub
```

### <a name="namespace-scope"></a>네임 스페이스 범위

[Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 또는 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 키워드를 사용 하 여 모듈 수준에서 요소를 선언 하는 경우 요소가 선언 되는 네임 스페이스 전체의 모든 프로시저에서 해당 요소를 사용할 수 있게 됩니다. 앞의 예제를 다음과 같이 변경 하 여 문자열 변수 `strMsg` 를 선언 네임 스페이스의 모든 위치에서 코드로 참조할 수 있습니다.

```vb
' Include this declaration at module level (not inside any procedure).
Public strMsg As String
```

네임 스페이스 범위에는 중첩 된 네임 스페이스가 포함 됩니다. 네임 스페이스 내에서 사용할 수 있는 요소는 해당 네임 스페이스 내에 중첩 된 모든 네임 스페이스 내 에서도 사용할 수 있습니다.

프로젝트에 [네임 스페이스 문이](../../../../visual-basic/language-reference/statements/namespace-statement.md)포함 되어 있지 않으면 프로젝트의 모든 항목이 동일한 네임 스페이스에 있습니다. 이 경우 네임 스페이스 범위를 프로젝트 범위로 간주할 수 있습니다. `Public`모듈, 클래스 또는 구조체의 요소는 해당 프로젝트를 참조 하는 모든 프로젝트 에서도 사용할 수 있습니다.

## <a name="choice-of-scope"></a>범위 선택

변수를 선언 하는 경우 범위를 선택할 때 다음 사항에 유의 해야 합니다.

### <a name="advantages-of-local-variables"></a>지역 변수의 장점

지역 변수는 다음과 같은 이유로 모든 종류의 임시 계산에 적합 합니다.

- **이름 충돌 방지.** 지역 변수 이름은 충돌을 받을 수 없습니다. 예를 들어 라는 `intTemp`변수를 포함 하는 여러 다른 프로시저를 만들 수 있습니다. 각 `intTemp` 프로시저는 지역 변수로 선언 되므로 각 프로시저는 자체 버전의 `intTemp`만 인식 합니다. 다른 프로시저의 변수에 영향을 주지 `intTemp` `intTemp` 않고 한 프로시저에서 로컬의 값을 변경할 수 있습니다.

- **메모리 소비** 지역 변수는 프로시저를 실행 하는 동안에만 메모리를 사용 합니다. 이 프로시저는 호출 코드로 반환 될 때 해당 메모리를 해제 합니다. 반면 [공유](../../../../visual-basic/language-reference/modifiers/shared.md) 및 [정적](../../../../visual-basic/language-reference/modifiers/static.md) 변수는 응용 프로그램 실행이 중지 될 때까지 메모리 리소스를 사용 하므로 필요한 경우에만 사용 합니다. 인스턴스 *변수* 는 인스턴스가 계속 존재 하는 동안 메모리를 사용 하며,이로 인해 지역 변수 보다 효율성이 낮지만 또는 `Shared` `Static` 변수 보다 효율성이 높아집니다.

### <a name="minimizing-scope"></a>범위 최소화

일반적으로 변수 또는 상수를 선언 하는 경우 범위를 최대한 좁게 만드는 것이 좋습니다 (블록 범위는 가장 좁은). 이렇게 하면 메모리를 절약 하 고 잘못 된 변수를 잘못 참조 하는 코드의 가능성을 최소화 합니다. 마찬가지로 프로시저 호출 사이에 값을 유지 해야 하는 경우에만 변수를 [정적](../../../../visual-basic/language-reference/modifiers/static.md) 으로 선언 해야 합니다.

## <a name="see-also"></a>참고자료

- [선언 요소의 특징](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [방법: 변수의 범위 제어](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)
- [Visual Basic 수명](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)
- [Visual Basic의 액세스 수준](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
