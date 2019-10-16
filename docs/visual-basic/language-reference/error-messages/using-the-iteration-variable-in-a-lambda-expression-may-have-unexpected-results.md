---
title: 람다 식에 반복 변수를 사용하면 예기치 않은 결과가 발생할 수 있습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc42324
- bc42324
helpviewer_keywords:
- BC42324
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
ms.openlocfilehash: 3335da503b6fb9c33e44266997cc945214a3a365
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64913069"
---
# <a name="using-the-iteration-variable-in-a-lambda-expression-may-have-unexpected-results"></a>람다 식에 반복 변수를 사용하면 예기치 않은 결과가 발생할 수 있습니다.
람다 식에 반복 변수를 사용 하 여 있을 예기치 않은 결과입니다. 대신 루프 내의 지역 변수를 만들고 반복 변수의 값을 할당 합니다.  
  
 루프 반복 변수를 사용 하 여 루프 내에서 선언 된 람다 식에서이 경고가 표시 됩니다. 예를 들어, 다음 예제에서는 경고를 표시 합니다.  
  
```vb  
For i As Integer = 1 To 10  
    ' The warning is given for the use of i.  
    Dim exampleFunc As Func(Of Integer) = Function() i  
Next  
```  
  
 다음 예제에서는 발생할 수 있는 예기치 않은 결과 보여 줍니다.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            array1(i) = Function() i  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
 합니다 `For` 루프는 각 루프 반복 변수의 값을 반환 람다 식의 배열을 만듭니다 `i`합니다. 람다 식의 평가 하는 경우는 `For Each` 루프를 예상할 수 0, 1, 2, 3 및 4 표시의 연속 값을 보려면 `i` 에 `For` 루프. 최종 값 대신 표시 `i` 다섯 번 표시 됩니다.  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC42324  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 반복 변수의 값을 지역 변수에 할당 및 람다 식에 지역 변수를 사용 합니다.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            Dim j = i  
            array1(i) = Function() j  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
## <a name="see-also"></a>참고자료

- [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
