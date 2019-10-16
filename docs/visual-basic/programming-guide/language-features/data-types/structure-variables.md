---
title: 구조체 변수(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- structures [Visual Basic], variables
- structures [Visual Basic], structure variables
- variables [Visual Basic], structure variables
- structure variables [Visual Basic]
ms.assetid: 156872f8-aabc-4454-8e2d-f2253c3c13c9
ms.openlocfilehash: a86a60def9ac1b8140194ecb6f5e784c62a0e101
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630961"
---
# <a name="structure-variables-visual-basic"></a>구조체 변수(Visual Basic)

구조를 만든 후에는 프로시저 수준 및 모듈 수준 변수를 해당 형식으로 선언할 수 있습니다. 예를 들어 컴퓨터 시스템에 대 한 정보를 기록 하는 구조를 만들 수 있습니다. 다음은 이에 대한 예입니다.

```vb
Public Structure systemInfo
    Public cPU As String
    Public memory As Long
    Public purchaseDate As Date
End Structure
```

이제 해당 형식의 변수를 선언할 수 있습니다. 다음 선언에서는이를 보여 줍니다.

```vb
Dim mySystem, yourSystem As systemInfo
```

> [!NOTE]
> 클래스 및 모듈에서 [Dim 문을](../../../../visual-basic/language-reference/statements/dim-statement.md) 사용 하 여 선언 된 구조체는 기본적으로 공용 액세스를 사용 합니다. 구조체를 private로 설정 하려면 [private](../../../../visual-basic/language-reference/modifiers/private.md) 키워드를 사용 하 여 구조체를 선언 해야 합니다.

## <a name="access-to-structure-values"></a>구조 값에 대 한 액세스

구조체 변수의 요소에서 값을 할당 하 고 검색 하려면를 사용할 때와 동일한 구문을 사용 하 여 개체에 대 한 속성을 설정 하 고 가져옵니다. 구조체 변수 이름과 요소 이름 사이에`.`멤버 액세스 연산자 ()를 추가 합니다. 다음 예제에서는 이전에 형식 `systemInfo`으로 선언 된 변수의 요소에 액세스 합니다.

```vb
mySystem.cPU = "486"
Dim tooOld As Boolean
If yourSystem.purchaseDate < #1/1/1992# Then tooOld = True
```

## <a name="assigning-structure-variables"></a>구조 변수 할당

둘 다 동일한 구조 유형인 경우 하나의 변수를 다른 변수에 할당할 수도 있습니다. 이렇게 하면 한 구조체의 모든 요소가 다른 구조체의 해당 요소에 복사 됩니다. 다음 선언에서는이를 보여 줍니다.

```vb
yourSystem = mySystem
```

구조체 요소가 `String`, `Object`또는 배열과 같은 참조 형식이 면 데이터에 대 한 포인터가 복사 됩니다. 이전 예제에서가 개체 변수 `systemInfo` 를 포함 한 경우 앞의 예제는에서 `mySystem` 로 `yourSystem`포인터를 복사 했 고 한 구조를 통해 개체의 데이터 변경 내용이 액세스 될 때 적용 됩니다. 다른 구조를 통해.

## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [기본 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)
- [복합 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [구조체](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [방법: 구조 선언](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)
- [구조체 및 기타 프로그래밍 요소](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)
- [구조체와 클래스](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)
- [Structure 문](../../../../visual-basic/language-reference/statements/structure-statement.md)
