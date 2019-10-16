---
title: '방법: 두 개체가 동일한 (Visual Basic) 여부를 확인합니다'
ms.date: 07/20/2015
helpviewer_keywords:
- testing [Visual Basic], objects
- objects [Visual Basic], comparing
- object variables [Visual Basic], determining identity
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
ms.openlocfilehash: aae053ae0473ed6ced0f28da3d5e5afc0be629df
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769085"
---
# <a name="how-to-determine-whether-two-objects-are-identical-visual-basic"></a>방법: 두 개체가 동일한 (Visual Basic) 여부를 확인합니다
Visual basic의 경우 두 변수가 메모리에서 동일한 클래스 인스턴스를 가리키는 두 개의 변수 참조의 포인터가 동일한 경우, 즉, 동일한 간주 됩니다. 예를 들어, Windows Forms 응용 프로그램에서는 하려는 비교를 확인 하는지 여부를 현재 인스턴스 (`Me`) 동일 특정 인스턴스를 같은 `Form2`합니다.  
  
 Visual Basic에서는 포인터를 비교할 두 연산자를 제공 합니다. [Is 연산자](../../../../visual-basic/language-reference/operators/is-operator.md) 반환 `True` 개체가 동일 하면 하며 [IsNot 연산자](../../../../visual-basic/language-reference/operators/isnot-operator.md) 반환 `True` 하지 않은 경우.  
  
## <a name="determining-if-two-objects-are-identical"></a>두 개체가 동일한 지 확인 합니다.  
  
#### <a name="to-determine-if-two-objects-are-identical"></a>두 개체가 동일한 지 확인 하려면  
  
1. 설정 된 `Boolean` 두 개체를 테스트할 식입니다.  
  
2. 테스트 식에서 사용 된 `Is` 피연산자로 두 개체를 사용 하 여 연산자입니다.  
  
     `Is` 반환 `True` 개체 동일한 클래스 인스턴스를 가리키는 경우.  
  
## <a name="determining-if-two-objects-are-not-identical"></a>두 개체가 동일 하지 않은지 확인 합니다.  
 두 개체가 같지 및 결합 하기에 비효율적인 수 하는 경우 작업을 수행 하려는 경우에 따라 `Not` 하 고 `Is`예를 들어 `If Not obj1 Is obj2`합니다. 이런 경우에서 사용할 수는 `IsNot` 연산자입니다.  
  
#### <a name="to-determine-if-two-objects-are-not-identical"></a>두 개체가 동일한 지 확인 하려면  
  
1. 설정 된 `Boolean` 두 개체를 테스트할 식입니다.  
  
2. 테스트 식에서 사용 된 `IsNot` 피연산자로 두 개체를 사용 하 여 연산자입니다.  
  
     `IsNot` 반환 `True` 경우 개체는 동일한 클래스 인스턴스를 가리키지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 쌍을 테스트 `Object` 변수를 같은 클래스 인스턴스를 가리키는지 확인 합니다.  
  
 [!code-vb[VbVbalrKeywords#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class7.vb#14)]  
  
 앞의 예제에는 다음과 같은 출력이 표시 됩니다.  
  
 `objA different from objB? True`  
  
 `objA identical to objC? True`  
  
## <a name="see-also"></a>참고자료

- [Object 데이터 형식](../../../../visual-basic/language-reference/data-types/object-data-type.md)
- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [개체 변수 값](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)
- [Is 연산자](../../../../visual-basic/language-reference/operators/is-operator.md)
- [IsNot 연산자](../../../../visual-basic/language-reference/operators/isnot-operator.md)
- [방법: 두 개체가 관련이 있는지 여부를 결정 합니다.](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)
- [Me, My, MyBase 및 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
