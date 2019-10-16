---
title: Widening(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.widening
helpviewer_keywords:
- conversions [Visual Basic], type
- type conversion [Visual Basic]
- conversions [Visual Basic], data type
- Widening keyword [Visual Basic]
- data type conversion [Visual Basic]
ms.assetid: 646ae263-94d3-40a2-b0cc-64f619292f56
ms.openlocfilehash: d7d43d4f5f931881d5c8b663c719fe7f92559799
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778666"
---
# <a name="widening-visual-basic"></a>Widening(Visual Basic)
나타내는 변환 연산자 (`CType`) 클래스 또는 구조체를 원래 클래스 또는 구조체의 모든 가능한 값을 보유할 수 있는 형식으로 변환 합니다.  
  
## <a name="converting-with-the-widening-keyword"></a>확대 키워드를 사용 하 여 변환  
 변환 절차 지정 해야 합니다 `Public Shared` 외에 `Widening`합니다.  
  
 확대 변환 런타임에 항상 실패 하 고 데이터가 손실 되지 마십시오. 예로 `Single` 하 `Double`, `Char` 에 `String`, 파생 형식과 해당 기본 형식에 합니다. 이 마지막은 확대 변환 파생된 형식은 기본 형식의 모든 멤버를 포함 되어 있으므로 기본 형식의 인스턴스.  
  
 사용 하는 코드를 사용할 필요가 없습니다 `CType` 확대 변환에 대 한 경우에 `Option Strict` 는 `On`합니다.  
  
 `Widening` 키워드는이 컨텍스트에서 사용할 수 있습니다.  
  
 [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 예를 들어 확대 변환과 축소 변환 연산자의 정의 참조 [방법: 변환 연산자 정의](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)
- [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)
- [확대 변환과 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [방법: 연산자 정의](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [CType 함수](../../../visual-basic/language-reference/functions/ctype-function.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [방법: 변환 연산자를 정의 합니다.](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
