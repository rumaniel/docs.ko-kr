---
title: With' 문 내부에서만 '.' 또는 '!'로 시작할 수 있습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30157
- bc30157
helpviewer_keywords:
- BC30157
ms.assetid: 70daaee1-14f9-45b7-9f30-53794310b95e
ms.openlocfilehash: 15390fb506fe9bca10f6917f5b26451a5569bece
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61921123"
---
# <a name="leading--or--can-only-appear-inside-a-with-statement"></a>With' 문 내부에서만 '.' 또는 '!'로 시작할 수 있습니다.
내부는 마침표 (.) 또는 느낌표 (!)을 `With` 블록 왼쪽 식을 없이 발생 합니다. 멤버 액세스 (`.`) 및 사전 멤버 액세스 (`!`) 멤버가 포함 된 요소를 지정 하는 식이 필요 합니다. 이 값은 왼쪽 접근자의 또는의 대상으로 즉시 표시 되어야 합니다는 `With` 멤버 액세스를 포함 하는 블록입니다.  
  
 **오류 ID:** BC30157  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 확인 된 `With` 블록 형식이 잘못 되었습니다.  
  
2. 없는 경우 없는 `With` 차단, 멤버를 포함 하는 정의 된 요소가 계산 되는 접근자의 왼쪽에 식을 추가 합니다.  
  
## <a name="see-also"></a>참고자료

- [코드의 특수 문자](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)
- [With...End With 문](../../../visual-basic/language-reference/statements/with-end-with-statement.md)
