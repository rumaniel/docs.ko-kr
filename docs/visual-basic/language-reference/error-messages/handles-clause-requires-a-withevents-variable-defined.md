---
title: Handles 절에는 포함하는 형식 또는 해당 형식의 기본 형식 중 하나에 정의된 WithEvents 변수가 필요합니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30506
- bc30506
helpviewer_keywords:
- BC30506
ms.assetid: 5b66f6a8-f050-4e03-a57f-a64e85f80cb5
ms.openlocfilehash: 04c94d3d32660d1a186a9bb377c49a53e1451be6
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512741"
---
# <a name="handles-clause-requires-a-withevents-variable-defined-in-the-containing-type-or-one-of-its-base-types"></a>Handles 절에는 포함하는 형식 또는 해당 형식의 기본 형식 중 하나에 정의된 WithEvents 변수가 필요합니다.
절에 변수를 `WithEvents` 제공 하지 않았습니다. `Handles` 프로시저 `Handles` 선언 끝에 있는 키워드를 `WithEvents` 사용 하면 키워드를 사용 하 여 선언 된 개체 변수에 의해 발생 된 이벤트를 처리할 수 있습니다.
  
 **오류 ID:** BC30506

## <a name="to-correct-this-error"></a>이 오류를 해결하려면
  
- 필요한 `WithEvents` 변수를 제공 합니다.
  
## <a name="example"></a>예제

다음 예제에서는 [WithEvents](../modifiers/withevents.md) 키워드가 <xref:System.Timers.Timer?displayProperty=nameWithType> 인스턴스의 정의에 사용 `BC30506` 되지 않기 때문에 Visual Basic는 컴파일러 오류를 생성 합니다.

```vb
Imports System.Timers

Module Module1
    Private _timer1 As New Timer() With {.Interval = 1000, .Enabled = True}
    
    Sub Main()
        Console.WriteLine("Press any key to start the timer...")
        Console.ReadKey()
        _timer1.Start()
        Console.ReadKey()
    End Sub

    Private Sub Timer1_Tick(sender As Object, args As EventArgs) Handles _timer1.Elapsed
        Console.WriteLine("Press any key to terminate...")
    End Sub
End Module
```

다음 예제는 `WithEvents` 키워드를 사용 하 `_timer1` 여 변수를 정의 하기 때문에 성공적으로 컴파일됩니다.

```vb
Imports System.Timers

Module Module1
    Private WithEvents _timer1 As New Timer() With {.Interval = 1000}

    Sub Main()
        Console.WriteLine("Press any key to start the timer...")
        Console.ReadKey()
        _timer1.Start()
        Console.ReadKey()
    End Sub

    Private Sub Timer1_Tick(sender As Object, args As EventArgs) Handles _timer1.Elapsed
        Console.WriteLine("Press any key to terminate...")
    End Sub

End Module
```

## <a name="see-also"></a>참고자료

- [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)
