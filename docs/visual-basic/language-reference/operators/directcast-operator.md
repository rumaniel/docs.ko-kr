---
title: DirectCast 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.directCast
- directCast
helpviewer_keywords:
- DirectCast keyword [Visual Basic]
ms.assetid: 63e5a1d0-4d9e-4732-bf8f-e90c0c8784b8
ms.openlocfilehash: 628ce4f06b91d0f514f71dea3aad8ea0fee6dccf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778549"
---
# <a name="directcast-operator-visual-basic"></a>DirectCast 연산자(Visual Basic)
상속 또는 구현에 따라 형식 변환 작업을 소개 합니다.  
  
## <a name="remarks"></a>설명  
 `DirectCast` 향상 된 성능을 어느 정도 제공할 수 있도록 변환에 대 한 런타임 도우미 루틴 Visual Basic을 사용 하지 않습니다 `CType` 데이터 형식에서 변환할 때 `Object`합니다.  
  
 사용할 합니다 `DirectCast` 키워드를 사용 하는 방법은 비슷합니다는 [CType Function](../../../visual-basic/language-reference/functions/ctype-function.md) 및 [TryCast 연산자](../../../visual-basic/language-reference/operators/trycast-operator.md) 키워드. 첫 번째 인수와 두 번째 인수로 변환 하는 형식으로 식을 제공 합니다. `DirectCast` 두 인수의 데이터 형식 간의 상속 또는 구현 관계를 필요합니다. 즉, 한 형식에서 상속 하거나 다른 구현 해야 합니다.  
  
## <a name="errors-and-failures"></a>오류 및 실패  
 `DirectCast` 상속 또는 구현 관계 없는 있는지 검색 하는 경우 컴파일러 오류를 생성 합니다. 하지만 컴파일러 오류가 없다고 성공적인 변환을 보장 하지 않습니다. 원하는 변환에 축소 하는 경우에 런타임에 실패할 수 있습니다. 이 경우 런타임에서 throw는 <xref:System.InvalidCastException> 오류입니다.  
  
## <a name="conversion-keywords"></a>변환 키워드  
 형식 변환 키워드의 비교는 다음과 같습니다.  
  
|키워드|데이터 형식|인수가 관계|런타임 오류|  
|---|---|---|---|  
|[CType 함수](../../../visual-basic/language-reference/functions/ctype-function.md)|모든 데이터 형식|두 데이터 형식 간에 확대 또는 축소 변환을 정의 해야 합니다.|Throw <xref:System.InvalidCastException>|  
|`DirectCast`|모든 데이터 형식|형식에서 상속 하거나 다른 형식을 구현 해야 합니다.|Throw <xref:System.InvalidCastException>|  
|[TryCast 연산자](../../../visual-basic/language-reference/operators/trycast-operator.md)|참조 형식에만|형식에서 상속 하거나 다른 형식을 구현 해야 합니다.|반환 [Nothing](../../../visual-basic/language-reference/nothing.md)|  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 사용 `DirectCast`, 런타임에 하나는 실패 하는 성공 합니다.  
  
 [!code-vb[VbVbalrKeywords#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#1)]  
  
 런타임 형식의 이전 예제의 `q` 는 `Double`합니다. `CType` 때문에 성공 `Double` 변환할 수 `Integer`입니다. 그러나 첫 번째 `DirectCast` 런타임 유형의 때문에 런타임에 실패 `Double` 사용 하 여 상속 관계가 없는 `Integer`한 변환이 존재 하는 경우에 합니다. 두 번째 `DirectCast` 형식에서 변환 되기 때문에 성공 <xref:System.Windows.Forms.Form> 입력할 <xref:System.Windows.Forms.Control>, 올 <xref:System.Windows.Forms.Form> 상속 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Convert.ChangeType%2A?displayProperty=nameWithType>
- [확대 변환과 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
