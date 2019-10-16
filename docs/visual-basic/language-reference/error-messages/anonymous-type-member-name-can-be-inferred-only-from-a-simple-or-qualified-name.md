---
title: 익명 형식 멤버 이름은 인수가 없는 단순한 이름 또는 정규화된 이름에서만 유추할 수 있습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc36556
- bc36556
helpviewer_keywords:
- BC36556
ms.assetid: e3ba1f33-3a71-4f03-9b04-ed5ec17de17c
ms.openlocfilehash: 38f669fe183ac79ebed6e5a122bc70aedc9bb753
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701220"
---
# <a name="anonymous-type-member-name-can-be-inferred-only-from-a-simple-or-qualified-name-with-no-arguments"></a>익명 형식 멤버 이름은 인수가 없는 단순한 이름 또는 정규화된 이름에서만 유추할 수 있습니다.
복합 식에서 무명 형식 멤버 이름을 유추할 수 없습니다.  
  
```vb  
Dim numbers() As Integer = {1, 2, 3, 4, 5}  
' Not valid.  
' Dim instanceName1 = New With {numbers(3)}  
```  
  
 익명 형식이 멤버 이름 및 형식을 유추할 수 있는 소스에 대 한 자세한 내용은 [How to: 익명 형식 선언에서 속성 이름 및 형식을 유추 @ no__t-0.  
  
 **오류 ID:** BC36556  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 다음 코드와 같이 멤버 이름에 식을 할당 합니다.  
  
    ```vb  
    Dim instanceName2 = New With {.number = numbers(3)}  
    ```  
  
## <a name="see-also"></a>참조

- [익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [방법: 익명 형식 선언에서 속성 이름 및 형식 유추 @ no__t-0
