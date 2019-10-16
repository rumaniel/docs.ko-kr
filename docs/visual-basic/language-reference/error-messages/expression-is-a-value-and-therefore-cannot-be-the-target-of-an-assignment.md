---
title: 식이 값이므로 할당 대상일 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- bc30068
- vbc30068
helpviewer_keywords:
- BC30068
ms.assetid: d65141e1-f31e-4ac5-a3b8-0b2e02a71ebf
ms.openlocfilehash: d5aae4d30abbf9ed2af260412352a5e0452e0dcc
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68513032"
---
# <a name="expression-is-a-value-and-therefore-cannot-be-the-target-of-an-assignment"></a>식이 값이므로 할당 대상일 수 없습니다.

문에서 식에 값을 할당 하려고 합니다. 런타임에 쓰기 가능한 변수, 속성 또는 배열 요소에만 값을 할당할 수 있습니다. 다음 예에서는이 오류가 발생할 수 있는 방법을 보여 줍니다.

```vb
Dim yesterday As Integer
ReadOnly maximum As Integer = 45
yesterday + 1 = DatePart(DateInterval.Day, Now)
' The preceding line is an ERROR because of an expression on the left.
maximum = 50
' The preceding line is an ERROR because maximum is declared ReadOnly.
```

속성과 배열 요소에도 유사한 예제가 적용 될 수 있습니다.

**간접 액세스.** 값 형식을 통해 간접적으로 액세스 하는 경우에도이 오류가 발생할 수 있습니다. 를 통해 <xref:System.Drawing.Point> <xref:System.Windows.Forms.Control.Location%2A>간접적으로 액세스 하 여의 값을 설정 하려고 시도 하는 다음 코드 예제를 고려 합니다.

```vb
' Assume this code runs inside Form1.
Dim exitButton As New System.Windows.Forms.Button()
exitButton.Text = "Exit this form"
exitButton.Location.X = 140
' The preceding line is an ERROR because of no storage for Location.
```

이전 예제의 마지막 문은 <xref:System.Drawing.Point> <xref:System.Windows.Forms.Control.Location%2A> 속성이 반환 하는 구조에 대 한 임시 할당만 만들기 때문에 실패 합니다. 구조체는 값 형식이 며 문이 실행 된 후에는 임시 구조가 유지 되지 않습니다. 에 대 <xref:System.Windows.Forms.Control.Location%2A>한 변수를 선언 하 고 사용 하 여 문제를 해결 하면 <xref:System.Drawing.Point> 구조에 대 한 보다 영구적인 할당을 만들 수 있습니다. 다음 예제에서는 이전 예제의 마지막 문을 바꿀 수 있는 코드를 보여 줍니다.

```vb
Dim exitLocation as New System.Drawing.Point(140, exitButton.Location.Y)
exitButton.Location = exitLocation
```

**오류 ID:** BC30068

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

- 문이 식에 값을 할당 하는 경우 식을 쓰기 가능한 단일 변수, 속성 또는 배열 요소로 바꿉니다.

- 문에서 값 형식 (일반적으로 구조체)을 통해 간접적으로 액세스 하는 경우 값 형식을 저장할 변수를 만듭니다.

- 적절 한 구조 (또는 다른 값 형식)를 변수에 할당 합니다.

- 변수를 사용 하 여 속성에 액세스 하 고 값을 할당 합니다.

## <a name="see-also"></a>참고자료

- [연산자 및 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
- [프로시저 문제 해결](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)
