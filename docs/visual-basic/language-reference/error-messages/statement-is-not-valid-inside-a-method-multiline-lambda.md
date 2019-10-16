---
title: 문은은 메서드 / 여러 줄 람다 내부 올바르지 않습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30024
- bc30024
helpviewer_keywords:
- BC30024
ms.assetid: 758e7a8f-429b-42c1-9a78-778e5b480e04
ms.openlocfilehash: 9e6c8ddd7851aee6d9fa1928a6854f7337b867b0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593222"
---
# <a name="statement-is-not-valid-inside-a-methodmultiline-lambda"></a>메서드 내부에는 문을 사용할 수 없습니다./multiline lambda
문 내에서 올바르지 않습니다.는 `Sub`, `Function`, 속성 `Get`, 또는 속성 `Set` 프로시저입니다. 일부 문이 모듈 또는 클래스 수준에서 배치할 수 있습니다. 다른 사용자와 같은 `Option Strict`, 네임 스페이스 수준 이어야 하며 다른 모든 선언 앞에 야 합니다.  
  
 **오류 ID:** BC30024  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 문을 프로시저에서 제거 합니다.  
  
## <a name="see-also"></a>참고자료

- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Get 문](../../../visual-basic/language-reference/statements/get-statement.md)
- [Set 문](../../../visual-basic/language-reference/statements/set-statement.md)
