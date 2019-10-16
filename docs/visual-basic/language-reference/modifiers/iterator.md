---
title: 반복기(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Iterator
helpviewer_keywords:
- Iterator keyword [Visual Basic]
ms.assetid: 69cb0b04-ac87-49d0-bcfe-810c0d60daff
ms.openlocfilehash: 4f42cf864e836c53cff5e7d620f4bdfa43c4c7ec
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661278"
---
# <a name="iterator-visual-basic"></a>반복기(Visual Basic)
지정 된 함수 또는 `Get` 접근자가 반복기입니다.  
  
## <a name="remarks"></a>설명  
 *반복기* 컬렉션 사용자 지정 반복을 수행 합니다. 반복기를 사용 하는 [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) 문을 한 번에 하나씩 컬렉션의 각 요소를 반환 합니다. 경우는 `Yield` 문에 도달 하면, 코드의 현재 위치가 유지 됩니다. 다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.  
  
 함수 또는 반복기를 구현할 수 있습니다는 `Get` 속성 정의의 접근자입니다. 합니다 `Iterator` 반복기 함수 선언에 표시 되는 한정자 또는 `Get` 접근자입니다.  
  
 사용 하 여 클라이언트 코드에서 반복기를 호출 하는 [각각에 대 한 중... 다음 문을](../../../visual-basic/language-reference/statements/for-each-next-statement.md)합니다.  
  
 반복기 함수의 반환 형식 또는 `Get` 접근자 수 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>합니다 <xref:System.Collections.IEnumerator>, 또는 <xref:System.Collections.Generic.IEnumerator%601>합니다.  
  
 반복기를 사용할 수 없습니다 `ByRef` 매개 변수입니다.  
  
 반복기는 이벤트, 인스턴스 생성자, 정적 생성자 또는 정적 소멸자에서 발생할 수 없습니다.  
  
 반복기는 익명 함수를 수 있습니다. 자세한 내용은 [반복기](../../programming-guide/concepts/iterators.md)를 참조하세요.  
  
## <a name="usage"></a>사용  
 `Iterator` 한정자는 다음 컨텍스트에서 사용할 수 있습니다.  
  
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## <a name="example"></a>예제  
 다음 예제에서는 반복기 함수를 보여 줍니다. 반복기 함수에는 `Yield` 문 내에 있는 [에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-next-statement.md) 루프입니다. 각 반복 합니다 [각각에 대 한](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 문의 본문 `Main` 대 한 호출이 생성를 `Power` 반복기 함수입니다. 반복기 함수를 호출할 때마다 다음에 `Yield` 루프를 반복하는 도중에 `For…Next` 문이 실행됩니다.  
  
 [!code-vb[VbVbalrStatements#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#98)]  
  
## <a name="example"></a>예제  
 다음 예제는 반복기인 `Get` 접근자에 대해 설명합니다. `Iterator` 속성 선언에서 한정자가 있습니다.  
  
 [!code-vb[VbVbalrStatements#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#99)]  
  
 추가 예제를 보려면 [반복기](../../programming-guide/concepts/iterators.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.CompilerServices.IteratorStateMachineAttribute>
- [반복기](../../programming-guide/concepts/iterators.md)
- [Yield 문](../../../visual-basic/language-reference/statements/yield-statement.md)
