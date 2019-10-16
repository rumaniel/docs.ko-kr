---
title: Yield 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Yield
helpviewer_keywords:
- iterators, Yield statement [Visual Basic]
- iterators [Visual Basic]
- Yield statement [Visual Basic]
ms.assetid: f33126c5-d7c4-43e2-8e36-4ae3f0703d97
ms.openlocfilehash: 645b8c4908095bc8d38c47836658325c9b47a569
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615058"
---
# <a name="yield-statement-visual-basic"></a>Yield 문(Visual Basic)
컬렉션의 다음 요소를 보냅니다는 `For Each...Next` 문입니다.  
  
## <a name="syntax"></a>구문  
  
```  
Yield expression  
```  
  
## <a name="parameters"></a>매개 변수  
  
|용어|정의|  
|---|---|  
|`expression`|필수 요소. 반복기 함수 형식을 암시적으로 변환할 수 있는 식 또는 `Get` 포함 하는 접근자를 `Yield` 문입니다.|  
  
## <a name="remarks"></a>설명  
 `Yield` 문을 한 번에 컬렉션의 요소를 하나를 반환 합니다. 합니다 `Yield` 문이 반복기 함수에 포함 되는지 또는 `Get` 접근자 컬렉션에 대해 사용자 지정 반복을 수행 합니다.  
  
 사용 하 여 반복기 함수를 사용 하는 [각각에 대 한 중... 다음 문을](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 또는 LINQ 쿼리입니다. 각 반복은 `For Each` 루프 반복기 함수를 호출 합니다. 경우는 `Yield` 문에 반복기 함수에 도달할 때 `expression` 반환 되 고 코드의 현재 위치가 유지 됩니다. 다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.  
  
 형식에서 암시적 변환이 있어야 합니다. `expression` 에 `Yield` 문은 반복기의 반환 형식입니다.  
  
 사용할 수는 `Exit Function` 또는 `Return` 반복을 끝내는 문입니다.  
  
 "Yield"는 예약어 이며에서 사용 하는 경우에 특별 한 의미가 있는 `Iterator` 함수 또는 `Get` 접근자입니다.  
  
 반복기 함수에 대 한 자세한 내용은 및 `Get` 접근자를 참조 하세요 [반복기](../../programming-guide/concepts/iterators.md)합니다.  
  
## <a name="iterator-functions-and-get-accessors"></a>반복기 함수 및 Get 접근자  
 반복기 함수 선언 또는 `Get` 접근자에는 다음 요구 사항을 충족 해야 합니다.  
  
- 여기에 포함 해야 합니다는 [반복기](../../../visual-basic/language-reference/modifiers/iterator.md) 한정자입니다.  
  
- 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, 또는 <xref:System.Collections.Generic.IEnumerator%601>여야 합니다.  
  
- 모든 것이 없습니다 `ByRef` 매개 변수입니다.  
  
 반복기 함수를 이벤트, 인스턴스 생성자, 정적 생성자 또는 정적 소멸자에서 발생할 수 없습니다.  
  
 반복기 함수를 익명 함수를 수 있습니다. 자세한 내용은 [반복기](../../programming-guide/concepts/iterators.md)를 참조하세요.  
  
## <a name="exception-handling"></a>예외 처리  
 `Yield` 문 내에 있을 수는 `Try` 블록을 [시도 하는 중... Catch 하는 중... Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)합니다. A `Try` 있는 블록을 `Yield` 문의 `Catch` 블록을 가질 수 있습니다를 `Finally` 블록.  
  
 A `Yield` 문 내에 있을 수 없습니다.을 `Catch` 블록 또는 `Finally` 블록입니다.  
  
 경우는 `For Each` 본문 (반복기 함수) 외부에서 예외를 throw를 `Catch` 반복기 함수에는 블록이 실행 되지 않습니다 하지만 `Finally` 반복기 함수에는 블록이 실행 됩니다. `Catch` 블록은 반복기 함수 내에서 반복기 함수 내에서 발생 하는 예외만 catch 합니다.  
  
## <a name="technical-implementation"></a>기술 구현  
 다음 반환 코드를 `IEnumerable (Of String)` 반복기 함수에서 다음의 요소를 반복 하 고는 `IEnumerable (Of String)`합니다.  
  
```vb  
Dim elements As IEnumerable(Of String) = MyIteratorFunction()  
    …  
For Each element As String In elements  
Next  
```  
  
 에 대 한 호출 `MyIteratorFunction` 함수의 본문을 실행 하지 않습니다. 대신에 `IEnumerable(Of String)` 변수에 `elements`을 반환합니다.  
  
 `For Each` 루프 반복에서 <xref:System.Collections.IEnumerator.MoveNext%2A>에 대한 `elements` 메서드가 호출됩니다. 이 호출은 다음 `MyIteratorFunction` 문에 도달할 때까지 `Yield` 본문을 실행합니다. `Yield` 문 뿐만 아니라 값을 결정 하는 식을 반환 합니다.는 `element` 루프 본문에서 사용에 대 한 변수 뿐만 아니라 합니다 <xref:System.Collections.Generic.IEnumerator%601.Current%2A> 요소의 속성은 `IEnumerable (Of String)`.  
  
 이후에 `For Each` 루프가 반복될 때마다 중지되었던 위치에서 반복기 본문 실행이 계속되고 `Yield` 문에 도달하면 다시 중지됩니다. 합니다 `For Each` 루프를 완료 하는 경우 끝 반복기 함수 또는 `Return` 또는 `Exit Function` 문에 도달 하면 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에는 `Yield` 문 내에 있는 [에 대 한 중... 다음](../../../visual-basic/language-reference/statements/for-next-statement.md) 루프입니다. 각 반복 합니다 [각각에 대 한](../../../visual-basic/language-reference/statements/for-each-next-statement.md) 문의 본문 `Main` 대 한 호출이 생성를 `Power` 반복기 함수입니다. 반복기 함수를 호출할 때마다 다음에 `Yield` 루프를 반복하는 도중에 `For…Next` 문이 실행됩니다.  
  
 반복기 메서드의 반환 형식은 <xref:System.Collections.Generic.IEnumerable%601>, 반복기 인터페이스 형식이 있습니다. 반복기 메서드가 호출되면 숫자의 거듭제곱이 들어 있는 열거형 개체를 반환합니다.  
  
 [!code-vb[VbVbalrStatements#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#98)]  
  
## <a name="example"></a>예제  
 다음 예제는 반복기인 `Get` 접근자에 대해 설명합니다. 속성 선언에 포함 된 `Iterator` 한정자입니다.  
  
 [!code-vb[VbVbalrStatements#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#99)]  
  
 추가 예제를 보려면 [반복기](../../programming-guide/concepts/iterators.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [문(C++)](../../../visual-basic/language-reference/statements/index.md)
