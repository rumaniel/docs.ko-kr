---
title: '방법: 두 개체가 동일한 (Visual Basic) 인지 여부를 테스트합니다'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], reference
- Is operator [Visual Basic], comparing objects
- reference variables [Visual Basic]
- variables [Visual Basic], referring to same object
- objects [Visual Basic], variables referring to same
- Visual Basic code, operators
ms.assetid: f760e828-8704-4256-bc2d-c22a4c93b524
ms.openlocfilehash: 6301228d786fe55e8851b6207dd84819671656f4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649674"
---
# <a name="how-to-test-whether-two-objects-are-the-same-visual-basic"></a>방법: 두 개체가 동일한 (Visual Basic) 인지 여부를 테스트합니다
두 변수 개체를 참조 하는 경우 사용할 수 있습니다 합니다 `Is` 또는 `IsNot` 연산자 또는 둘 다에서 동일한 인스턴스를 참조 하는지 확인 합니다.  
  
### <a name="to-test-whether-two-objects-are-the-same"></a>두 개체가 같은지 여부를 테스트 하려면  
  
- 사용 된 [Is 연산자](../../../../visual-basic/language-reference/operators/is-operator.md) 또는 [IsNot 연산자](../../../../visual-basic/language-reference/operators/isnot-operator.md) 피연산자로 두 변수를 사용 하 여 합니다.  
  
     [!code-vb[VbVbalrOperators#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#69)]  
  
 두 개체가 같은 인스턴스를 참조 하는 여부에 따라 특정 작업을 수행 하려는 경우. 앞의 예제에서는 컨트롤 비교 `c` 폼에 있는 활성 컨트롤에 대해 `f`합니다. 활성 컨트롤이 없는 경우 없는 경우 하나 하지 않은 동일한 컨트롤 인스턴스로 `c`, 그런 다음 `If` 추가적인 처리 없이 문은 실패 하 고 프로시저에서 반환 합니다.  
  
 사용할지 `Is` 또는 `IsNot` 할 개인 편의 관련 됩니다. 하나는 지정된 된 식에서 다른 보다 읽기 쉬울 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
