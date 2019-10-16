---
title: "'#ElseIf'는 짝이 되는 '#If' 또는 '#ElseIf' 뒤에 와야 합니다."
ms.date: 07/20/2015
f1_keywords:
- vbc30014
- bc30014
helpviewer_keywords:
- BC30014
ms.assetid: 5215585e-2efa-485a-9efe-9833a1cc83a0
ms.openlocfilehash: 4832fb80cfbe42c7a1303e0de69f36784711c05a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61803365"
---
# <a name="elseif-must-be-preceded-by-a-matching-if-or-elseif"></a>'#ElseIf'는 짝이 되는 '#If' 또는 '#ElseIf' 뒤에 와야 합니다.
`#ElseIf` 는 조건부 컴파일 지시문입니다. `#ElseIf` 일치 하는 절을 야 `#If` 또는 `#ElseIf` 절.  
  
 **오류 ID:** BC30014  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 확인 앞 `#If` 또는 `#ElseIf` 이에서 분리 없습니다 `#ElseIf` 간섭 조건부 컴파일 블록 또는 잘못 배치 된 `#End If`합니다.  
  
2. 경우는 `#ElseIf` 앞에 `#Else` 지시문을 제거 하거나를 `#Else` 로 변경 하거나는 `#ElseIf`합니다.  
  
3. 다른 모든 항목의 순서가 올바른 경우 `#If` 지시문을 조건부 컴파일 블록의 시작 부분에 추가합니다.  
  
## <a name="see-also"></a>참고자료

- [#If...Then...#Else 지시문](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
