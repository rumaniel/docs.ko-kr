---
title: "'AddressOf' 피연산자에는 괄호 없이 메서드 이름을 사용해야 합니다."
ms.date: 07/20/2015
f1_keywords:
- vbc30577
- bc30577
helpviewer_keywords:
- BC30577
ms.assetid: c2c55640-5c61-4e66-97a4-4322020c6001
ms.openlocfilehash: b8c67c2390df91c6a4af66e020365544e6bf369b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61751633"
---
# <a name="addressof-operand-must-be-the-name-of-a-method-without-parentheses"></a>'AddressOf' 피연산자에는 괄호 없이 메서드 이름을 사용해야 합니다.
`AddressOf` 연산자는 특정 프로시저를 참조하는 프로시저 대리자 인스턴스를 만듭니다. 구문은 다음과 같습니다.  
  
 `AddressOf` `procedurename`  
  
 인수 다음에 괄호를 삽입 `AddressOf`에 불필요 합니다.  
  
 **오류 ID:** BC30577  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 인수 다음에 괄호를 제거 `AddressOf`합니다.  
  
2. 인수는 메서드 이름 인지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [AddressOf 연산자](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [대리자](../../../visual-basic/programming-guide/language-features/delegates/index.md)
