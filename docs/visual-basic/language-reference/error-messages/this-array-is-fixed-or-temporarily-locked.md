---
title: 이 배열은 고정되었거나 임시로 잠겨 있습니다(Visual Basic).
ms.date: 07/20/2015
f1_keywords:
- vbrID10
ms.assetid: de6713a6-51d7-4edb-8515-d5fb544e2091
ms.openlocfilehash: c7b5372b6046e25aad87131ba141cb71c580e12c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625939"
---
# <a name="this-array-is-fixed-or-temporarily-locked-visual-basic"></a>이 배열은 고정되었거나 임시로 잠겨 있습니다(Visual Basic).
이 오류는 다음과 같은 가능한 원인을:  
  
- 사용 하 여 `ReDim` 고정 크기 배열 요소의 수를 변경 합니다.  
  
- 하나의 요소가 전달 인수로 프로시저에는 모듈 수준 동적 배열 차원을 다시 지정 하려고 합니다. 배열 방지 하기 위해 잠겨 요소를 전달 하면 프로시저 내의 참조 매개 변수에 대 한 메모리 할당을 취소 합니다.  
  
- 값을 할당 하려고를 `Variant` 배열을 포함 하는 변수 하지만 `Variant` 현재 잠겨 있습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 원래 배열을 사용 하 여 선언 하 여 고정 되지 않고 동적으로 만들 `ReDim` (경우 배열의 선언 된 프로시저 내에서) 또는 (배열 모듈 수준에서 선언 됩니다 경우 요소의 수를 지정 하지 않고 선언 하 여.  
  
2. 실제로 프로시저 모듈에서 모두 표시 되므로 요소를 전달 해야 하는지 여부를 결정 합니다.  
  
3. 잠그고 어떤 결정을 `Variant` 해제 합니다.  
  
## <a name="see-also"></a>참고자료

- [배열(C++)](../../../visual-basic/programming-guide/language-features/arrays/index.md)
