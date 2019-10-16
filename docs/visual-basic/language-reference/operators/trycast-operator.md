---
title: TryCast 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.trycast
- trycast
helpviewer_keywords:
- TryCast keyword [Visual Basic]
ms.assetid: d1ef5d47-fef4-491e-b014-1d910628f65c
ms.openlocfilehash: c0eea4565d5040bb00743fc7864ac15b0fccdea9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013467"
---
# <a name="trycast-operator-visual-basic"></a>TryCast 연산자(Visual Basic)
예외를 throw 하지 않는 형식 변환 작업을 소개 합니다.  
  
## <a name="remarks"></a>설명  
 변환에 실패 하면 `CType` 하 고 `DirectCast` 둘 다 throw는 <xref:System.InvalidCastException> 오류입니다. 이 응용 프로그램의 성능을 저하 수 있습니다. `TryCast` 반환 [아무](../../../visual-basic/language-reference/nothing.md)가능한 예외를 처리 하는 대신 테스트 하기만 하면에 대 한 결과가 반환된 되도록 `Nothing`합니다.  
  
 사용할 합니다 `TryCast` 키워드를 동일한 방식 합니다 [CType Function](../../../visual-basic/language-reference/functions/ctype-function.md) 및 [DirectCast 연산자](../../../visual-basic/language-reference/operators/directcast-operator.md) 키워드. 첫 번째 인수와 두 번째 인수로 변환 하는 형식으로 식을 제공 합니다. `TryCast` 클래스 및 인터페이스와 같은 참조 형식에만 작동합니다. 두 형식 간의 상속 또는 구현 관계를 해야합니다. 즉, 한 형식에서 상속 하거나 다른 구현 해야 합니다.  
  
## <a name="errors-and-failures"></a>오류 및 실패  
 `TryCast` 상속 또는 구현 관계 없는 있는지 검색 하는 경우 컴파일러 오류를 생성 합니다. 하지만 컴파일러 오류가 없다고 성공적인 변환을 보장 하지 않습니다. 원하는 변환에 축소 하는 경우에 런타임에 실패할 수 있습니다. 이 경우 `TryCast` 반환 [Nothing](../../../visual-basic/language-reference/nothing.md)합니다.  
  
## <a name="conversion-keywords"></a>변환 키워드  
 형식 변환 키워드의 비교는 다음과 같습니다.  
  
|키워드|데이터 형식|인수가 관계|런타임 오류|  
|---|---|---|---|  
|[CType 함수](../../../visual-basic/language-reference/functions/ctype-function.md)|모든 데이터 형식|두 데이터 형식 간에 확대 또는 축소 변환을 정의 해야 합니다.|Throw <xref:System.InvalidCastException>|  
|[DirectCast 연산자](../../../visual-basic/language-reference/operators/directcast-operator.md)|모든 데이터 형식|형식에서 상속 하거나 다른 형식을 구현 해야 합니다.|Throw <xref:System.InvalidCastException>|  
|`TryCast`|참조 형식에만|형식에서 상속 하거나 다른 형식을 구현 해야 합니다.|반환 [Nothing](../../../visual-basic/language-reference/nothing.md)|  
  
## <a name="example"></a>예제  
 다음 예제에서는 `TryCast`을 사용하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrKeywords#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>참고자료

- [확대 변환과 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
