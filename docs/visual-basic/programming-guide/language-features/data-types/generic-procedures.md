---
title: Generic Procedures in Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- generic methods [Visual Basic], type inference
- generics [Visual Basic], type inference
- procedures [Visual Basic], generic
- generic procedures
- type inference, generics
- generic methods [Visual Basic]
- type inference
- generics [Visual Basic], procedures
- generic procedures [Visual Basic], type inference
ms.assetid: 95577b28-137f-4d5c-a149-919c828600e5
ms.openlocfilehash: 4aed16ce9eb59da54156a0cd5f1594819788521b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61906596"
---
# <a name="generic-procedures-in-visual-basic"></a>Generic Procedures in Visual Basic
*제네릭 프로시저*라고도 하는 *제네릭 메서드*, 하나 이상의 형식 매개 변수를 사용 하 여 정의 하는 절차입니다. 따라서 프로시저를 호출할 때마다 데이터 형식 요구 사항에 맞게 코드를 호출 합니다.  
  
 프로시저는 제네릭 클래스 또는 일반 구조체 내에서 정의 되는 것 만으로 제네릭이 아닙니다. 제네릭 되도록 프로시저 걸릴 수 있습니다 일반 매개 변수 외에도 하나 이상의 형식 매개 변수를 수행 해야 합니다. 제네릭이 아닌 프로시저 및 제네릭이 아닌 클래스, 구조체 제네릭 클래스 또는 구조체를 포함 하거나 모듈에서 제네릭 프로시저를 포함할 수 있습니다.  
  
 제네릭 프로시저 하나, 그리고 해당 프로시저 코드가 있을 경우 해당 반환 형식에 기본 매개 변수 목록에서 해당 형식 매개 변수를 사용할 수 있습니다.  
  
## <a name="type-inference"></a>형식 유추  
 제네릭 프로시저가 형식 인수를 전혀 제공 하지 않고 호출할 수 있습니다. 이러한 방식으로 호출을 하는 경우 컴파일러는 프로시저의 형식 인수에 전달 하는 적절 한 데이터 형식을 확인 하려고 합니다. 이 이라고 *형식 유추*합니다. 다음 코드는 호출을 보여 줍니다. 컴파일러 유추 하는 형식 전달 해야 `String` 형식 매개 변수에 `t`합니다.  
  
 [!code-vb[VbVbalrDataTypes#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#15)]  
  
 컴파일러는 호출 컨텍스트에서 형식 인수를 유추할 수 없습니다, 하는 경우 오류를 보고 합니다. 이러한 오류가 발생할 수 있는 배열 차수가 일치 하지 않는 경우 예를 들어, 형식 매개 변수 배열로 일반 매개 변수를 정의 합니다. 다른 차수 (차원 수)의 배열을 제공 제네릭 프로시저를 호출 하는 경우 일치 하지 않는 하면 형식을 유추할 수 없습니다. 다음 코드는 호출을 보여 줍니다. 2 차원 배열은 1 차원 배열을 필요로 하는 프로시저에 전달 되는에 있습니다.  
  
```vb  
Public Sub demoSub(Of t)(ByVal arg() As t)
End Sub

Public Sub callDemoSub()
    Dim twoDimensions(,) As Integer
    demoSub(twoDimensions)
End Sub
```
  
 모든 형식 인수를 생략 해야만 형식 유추를 호출할 수 있습니다. 하나의 형식 인수를 제공 하는 경우 모두 제공 해야 합니다.  
  
 형식 유추가 제네릭 프로시저에만 지원 됩니다. 제네릭 클래스, 구조체, 인터페이스 또는 대리자에서 형식 유추를 호출할 수 없습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 제네릭 정의 `Function` 프로시저 배열에서 특정 요소를 찾으려고 합니다. 하나의 형식 매개 변수를 정의 하 고 매개 변수 목록에 두 개의 매개 변수를 생성 하는 데 사용 합니다.  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbalrDataTypes#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#14)]  
  
### <a name="comments"></a>설명  
 앞의 예제 비교 하는 기능을 요구 `searchValue` 의 각 요소에 대해 `searchArray`합니다. 이 기능을 보장 하기 위해 형식 매개 변수를 제한 `T` 를 구현 하는 <xref:System.IComparable%601> 인터페이스입니다. 코드를 사용 하는 <xref:System.IComparable%601.CompareTo%2A> 메서드 대신 합니다 `=` 연산자에 대 한 형식 인수를 제공 하지 않을 수도 있기 때문에 `T` 지원를 `=` 연산자.  
  
 테스트할 수 있습니다는 `findElement` 다음 코드를 사용 하 여 프로시저입니다.  
  
 [!code-vb[VbVbalrDataTypes#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#13)]  
  
 에 대 한 호출 앞 `MsgBox` "0", "1" 및 "-1"은 각각 표시 합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 제네릭 형식](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [방법: 다른 데이터 형식에 동일한 기능을 제공할 수 있는 클래스 정의](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)
- [방법: 제네릭 클래스 사용](../../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [절차](../../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [프로시저 매개 변수 및 인수](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)
- [형식 목록](../../../../visual-basic/language-reference/statements/type-list.md)
- [매개 변수 목록](../../../../visual-basic/language-reference/statements/parameter-list.md)
