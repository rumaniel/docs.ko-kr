---
title: Narrowing(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.narrowing
helpviewer_keywords:
- conversions [Visual Basic], type
- type conversion [Visual Basic]
- conversions [Visual Basic], data type
- Narrowing keyword [Visual Basic]
- data type conversion [Visual Basic]
ms.assetid: a207ee91-aca4-4771-b4e2-713f029bf2bb
ms.openlocfilehash: eb5f021371291483b8eb2a13727a9fda94540638
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61920642"
---
# <a name="narrowing-visual-basic"></a>Narrowing(Visual Basic)
나타내는 변환 연산자 (`CType`) 클래스 또는 구조체를 원래 클래스 또는 구조체의 가능한 값의 일부를 저장 하지 못할 수 있는 형식으로 변환 합니다.  
  
## <a name="converting-with-the-narrowing-keyword"></a>축소 키워드를 사용 하 여 변환  
 변환 절차 지정 해야 합니다 `Public Shared` 외에 `Narrowing`합니다.  
  
 축소 변환 수행 항상 런타임에 성공 및 실패 하거나 하 데이터 손실이 발생할 합니다. 예로 `Long` 하 `Integer`, `String` 를 `Date`, 및 파생된 형식에 기본 형식입니다. 기본 형식을 파생 된 유형의 모든 멤버를 포함 하지 않을 수 파생 형식의 인스턴스를 따라서 이기 때문에 마지막으로이 변환이 축소 합니다.  
  
 경우 `Option Strict` 은 `On`를 사용 하는 코드를 사용 해야 합니다 `CType` 모든 축소 변환에 대 한 합니다.  
  
 `Narrowing` 키워드는이 컨텍스트에서 사용할 수 있습니다.  
  
 [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
## <a name="see-also"></a>참고자료

- [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)
- [확장](../../../visual-basic/language-reference/modifiers/widening.md)
- [확대 변환과 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [방법: 연산자 정의](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [CType 함수](../../../visual-basic/language-reference/functions/ctype-function.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
