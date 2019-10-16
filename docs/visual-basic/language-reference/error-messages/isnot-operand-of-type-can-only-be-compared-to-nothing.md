---
title: "'typename'이(가) nullable 형식이므로 'typename' 형식의 'IsNot' 피연산자는 'Nothing'과(와)만 비교할 수 있습니다."
ms.date: 07/20/2015
f1_keywords:
- bc32128
- vbc32128
helpviewer_keywords:
- BC32128
ms.assetid: 1155b23a-ad75-4bab-b9da-73f35c767a36
ms.openlocfilehash: f19b8cd5f80ba9fd6d1f5a9162b04ee409e24e28
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921136"
---
# <a name="isnot-operand-of-type-typename-can-only-be-compared-to-nothing-because-typename-is-a-nullable-type"></a>'typename'이(가) nullable 형식이므로 'typename' 형식의 'IsNot' 피연산자는 'Nothing'과(와)만 비교할 수 있습니다.
Nullable로 선언 된 변수를 식으로 비교 된 이외의 `Nothing` 를 사용 하 여 `IsNot` 연산자입니다.  
  
 **오류 ID:** BC32128  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. `Nothing` 연산자를 사용하여 nullable 형식을 `IsNot` 이외의 식과 비교하려면 다음 예제와 같이 nullable 형식에서 `GetType` 메서드를 호출하고 그 결과를 식과 비교합니다.  
  
```vb  
Dim number? As Integer = 5  
  
If number IsNot Nothing Then  
  If number.GetType() IsNot Type.GetType("System.Int32") Then   
  
  End If  
End If  
```  
  
## <a name="see-also"></a>참고자료

- [Nullable 값 형식](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
- [IsNot 연산자](../../../visual-basic/language-reference/operators/isnot-operator.md)
