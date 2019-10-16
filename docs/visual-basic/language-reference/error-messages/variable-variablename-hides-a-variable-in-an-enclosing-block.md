---
title: "'<variablename>' 변수는 바깥쪽 블록에 있는 변수를 숨깁니다."
ms.date: 07/20/2015
f1_keywords:
- vbc30616
- bc30616
helpviewer_keywords:
- BC30616
ms.assetid: e7658ebc-da45-451b-a409-a0f8915f0beb
ms.openlocfilehash: 4312abef83728f432e2f6a492e5acad3450719b1
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592057"
---
# <a name="variable-variablename-hides-a-variable-in-an-enclosing-block"></a>' @No__t-0variablename > ' 변수는 바깥쪽 블록의 변수를 숨깁니다.
블록에 포함 된 변수는 다른 지역 변수와 동일한 이름을 갖습니다.  
  
 **오류 ID:** BC30616  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 다른 지역 변수와 동일 하지 않도록 포함 된 블록의 변수 이름을 바꿉니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
    ```vb  
    Dim a, b, x As Integer  
    If a = b Then  
       Dim y As Integer = 20 ' Uniquely named block variable.  
    End If  
    ```  
  
- 이 오류의 일반적인 원인은 이벤트 처리기 내에서 `Catch e As Exception`을 사용 하는 것입니다. 이 경우 `Catch` 블록 변수의 이름을 `e`가 아니라-1 @no__t 합니다.  
  
- 이 오류의 또 다른 일반적인 소스는 별도 `Catch` 블록의 `Try` 블록 내에 선언 된 지역 변수에 액세스 하려고 시도 하는 것입니다. 이를 해결 하려면 `Try...Catch...Finally` 구조 외부에서 변수를 선언 합니다.  
  
## <a name="see-also"></a>참조

- [Try...Catch...Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
- [변수 선언](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
