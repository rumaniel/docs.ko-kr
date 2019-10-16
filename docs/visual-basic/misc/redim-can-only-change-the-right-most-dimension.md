---
title: "'ReDim'으로는 맨 오른쪽 차원만 변경할 수 있습니다."
ms.date: 07/20/2015
f1_keywords:
- vbrArray_TypeMismatch
ms.assetid: d53cf41b-7a7a-466c-a29a-920d99698fa9
ms.openlocfilehash: f38bcb99b682ace497859b67fe3bb829bbc80c4d
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69664414"
---
# <a name="redim-can-only-change-the-right-most-dimension"></a>'ReDim'으로는 맨 오른쪽 차원만 변경할 수 있습니다.
`ReDim` 문에서 `Preserve` 키워드를 사용하여 마지막 차원이 아닌 배열의 차원을 변경하려고 했습니다. `Preserve`를 사용하는 경우 배열의 마지막 차원만 크기를 조정할 수 있습니다. 다른 모든 차원의 경우 기존 배열과 동일한 크기를 지정해야 합니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- `Preserve` 키워드를 제거합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 배열](../programming-guide/language-features/arrays/index.md)
- [Visual Basic의 배열 차원](../programming-guide/language-features/arrays/array-dimensions.md)
- [ReDim 문](../../visual-basic/language-reference/statements/redim-statement.md)
- [Dim 문](../../visual-basic/language-reference/statements/dim-statement.md)
