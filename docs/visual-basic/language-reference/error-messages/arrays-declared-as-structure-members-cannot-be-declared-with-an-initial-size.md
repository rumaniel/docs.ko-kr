---
title: 구조체 멤버로 선언된 배열은 초기 크기로 선언할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc31043
- bc31043
helpviewer_keywords:
- BC31043
ms.assetid: 5bd90c71-1b78-444b-91e1-4789451ef085
ms.openlocfilehash: 83342b780c0fa7c3a2e0a6797b80ef788117ae92
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250146"
---
# <a name="arrays-declared-as-structure-members-cannot-be-declared-with-an-initial-size"></a>구조체 멤버로 선언된 배열은 초기 크기로 선언할 수 없습니다.

구조체의 배열은 초기 크기로 선언 됩니다. 구조체 요소를 초기화할 수 없으며 배열 크기를 선언 하는 것은 초기화의 한 형태입니다.

**오류 ID:** BC31043

## <a name="example"></a>예제

다음 예제에서는 BC31043를 생성 합니다.

```vb
Structure DemoStruct
    Public demoArray(9) As Integer
End Structure
```

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

1. 구조체의 배열을 동적 (초기 크기 없음)으로 정의 합니다.

2. 특정 크기의 배열이 필요한 경우 코드가 실행 중일 때 [ReDim 문으로](../statements/redim-statement.md) 동적 배열의 크기를 변경할 수 있습니다. 다음 예제는 이러한 과정을 보여 줍니다.
  
    ```vb
    Structure DemoStruct
        Public demoArray() As Integer
    End Structure
    Sub UseStruct()
        Dim struct As DemoStruct  
        ReDim struct.demoArray(9)
        Struct.demoArray(2) = 777
    End Sub  
    ```
  
## <a name="see-also"></a>참조

- [배열](../../programming-guide/language-features/arrays/index.md)
- [방법: 구조 선언](../../programming-guide/language-features/data-types/how-to-declare-a-structure.md)
