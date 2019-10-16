---
title: Is 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.is
helpviewer_keywords:
- comparison operators [Visual Basic]
- equivalent objects
- TypeOf...Is expression
- Is operator [Visual Basic]
ms.assetid: 8045a6c8-2a83-45b6-ad47-d09a704c656d
ms.openlocfilehash: 0351d224d9bf08a8f3ca74090de7b9c51c2c61bf
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701359"
---
# <a name="is-operator-visual-basic"></a>Is 연산자(Visual Basic)
두 개체 참조 변수를 비교 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
result = object1 Is object2  
```  
  
## <a name="parts"></a>요소  
 `result`  
 필수. 모든 `Boolean` 값입니다.  
  
 `object1`  
 필수. @No__t-0 이름입니다.  
  
 `object2`  
 필수. @No__t-0 이름입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 연산자는 두 개체 참조가 동일한 개체를 참조 하는지 여부를 결정 합니다. 그러나 값 비교를 수행 하지는 않습니다. @No__t-0 및 `object2`이 모두 정확히 동일한 개체 인스턴스를 참조 하는 경우에는 `result`가 `True`입니다. 그렇지 않은 경우-4는-5 @no__t @no__t.  
  
 `Is`은 `TypeOf` 키워드와 함께 사용 하 여 개체 변수가 데이터 형식과 호환 되는지 여부를 테스트 하는 `TypeOf` ... `Is` 식을 만들 수도 있습니다.  
  
> [!NOTE]
> @No__t-0 키워드는 [Select ... Case 문](../../../visual-basic/language-reference/statements/select-case-statement.md).  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Is` 연산자를 사용 하 여 개체 참조 쌍을 비교 합니다. 두 개체가 동일한 지 여부를 나타내는 0 @no__t 값에 결과가 할당 됩니다.  
  
 [!code-vb[VbVbalrOperators#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#27)]  
  
 앞의 예제에서 보여 주는 것 처럼 `Is` 연산자를 사용 하 여 초기 바인딩과 런타임에 바인딩된 개체를 모두 테스트할 수 있습니다.  
  
## <a name="see-also"></a>참조

- [TypeOf 연산자](../../../visual-basic/language-reference/operators/typeof-operator.md)
- [IsNot 연산자](../../../visual-basic/language-reference/operators/isnot-operator.md)
- [Visual Basic의 비교 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [연산자 및 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
