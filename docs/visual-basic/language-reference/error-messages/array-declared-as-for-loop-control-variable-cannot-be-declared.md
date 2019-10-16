---
title: For 루프 제어 변수를 통해 선언되는 배열은 초기 크기를 지정하여 선언할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc32039
- bc32039
helpviewer_keywords:
- BC32039
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
ms.openlocfilehash: 9e8bb7b79b5a770c3c92e47d8e7c01c5b83d6061
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701205"
---
# <a name="array-declared-as-for-loop-control-variable-cannot-be-declared-with-an-initial-size"></a>For 루프 제어 변수를 통해 선언되는 배열은 초기 크기를 지정하여 선언할 수 없습니다.
@No__t-0 루프는 배열을 해당 *요소* 반복 변수로 사용 하지만 해당 배열을 초기화 합니다.  
  
 다음 문은이 오류를 생성 하는 방법을 보여 줍니다.  
  
```vb  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 첫 번째 `For Each` 문은 `arrayList`의 요소에 액세스 하는 올바른 방법입니다. 두 번째 `For Each` 문은이 오류를 생성 합니다.  
  
 **오류 ID:** BC32039  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- *요소* 반복 변수의 선언에서 초기화를 제거 합니다.  
  
## <a name="see-also"></a>참조

- [For...Next 문](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [배열](../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [컬렉션](../../../standard/collections/index.md)
