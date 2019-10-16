---
title: 중첩된 함수에 '<delegatename>' 대리자와 호환되는 시그니처가 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc36532
- bc36532
helpviewer_keywords:
- BC36532
ms.assetid: 493f292c-d81e-40ef-8b47-61f020571829
ms.openlocfilehash: 912962e2ab39c4811294ccc225814b230100e12a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592004"
---
# <a name="nested-function-does-not-have-a-signature-that-is-compatible-with-delegate-delegatename"></a>중첩 된 함수에서 대리자와 호환 되는 서명 되지 않은 '\<delegatename >'
람다 식에 호환 되지 않는 서명이 대리자에 할당 되었습니다. 예를 들어, 다음 코드를 대리자 `Del` 은 두 개의 정수 매개 변수입니다.  
  
```vb  
Delegate Function Del(ByVal p As Integer, ByVal q As Integer) As Integer  
```  
  
 하나의 인수를 사용 하 여 람다 식 형식으로 선언 된 경우 오류는 발생 `Del`:  
  
```vb  
' Neither of these is valid.   
' Dim lambda1 As Del = Function(n As Integer) n + 1  
' Dim lambda2 As Del = Function(n) n + 1  
```  
  
 **오류 ID:** BC36532  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 서명을 호환 되도록 할당 된 람다 식 또는 대리자 정의 조정 합니다.  
  
## <a name="see-also"></a>참고자료

- [완화된 대리자 변환](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
