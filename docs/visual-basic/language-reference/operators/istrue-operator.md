---
title: IsTrue 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.istrue
helpviewer_keywords:
- IsTrue operator [Visual Basic]
- OrElse operator [Visual Basic]
ms.assetid: b6cec0f2-61b1-4331-a7f0-4d07ee3179d6
ms.openlocfilehash: 1152f4b512a85ae183f8fc8d476b69685e2926ef
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966914"
---
# <a name="istrue-operator-visual-basic"></a>IsTrue 연산자(Visual Basic)
식이 인지 여부를 확인 `True`합니다.  
  
 코드에서 명시적 `IsTrue` 으로 호출할 수는 없지만 Visual Basic 컴파일러는이를 사용 하 여 절에서 `OrElse` 코드를 생성할 수 있습니다. 클래스 또는 구조체를 정의한 다음 해당 형식의 변수를 `OrElse` 절에서 사용 하는 경우 해당 클래스 또는 구조체에 대해를 정의 `IsTrue` 해야 합니다.  
  
 컴파일러는 및 `IsFalse` 연산자 `IsTrue` 를 일치 하는 *쌍*으로 간주 합니다. 즉, 이러한 항목 중 하나를 정의 하는 경우 다른 항목을 정의 해야 합니다.  
  
## <a name="compiler-use-of-istrue"></a>IsTrue의 컴파일러 사용  
 클래스 또는 구조체를 정의한 경우 `For` `Else If`, `If`, 또는 `While` 문이나 `When` 절에서 해당 형식의 변수를 사용할 수 있습니다. 이 작업을 수행 하는 경우 컴파일러는 조건을 테스트할 수 있도록 형식을 `Boolean` 값으로 변환 하는 연산자가 필요 합니다. 다음 순서에 따라 적합 한 연산자를 검색 합니다.  
  
1. 클래스 또는 구조체에서로 `Boolean`의 확대 변환 연산자입니다.  
  
2. 클래스 또는 구조체에서로 `Boolean?`의 확대 변환 연산자입니다.  
  
3. 클래스 또는 구조체의 연산자입니다.`IsTrue`  
  
4. 로 `Boolean?` 의 축소 변환은에서로 `Boolean?`의 `Boolean` 변환이 포함 되지 않습니다.  
  
5. 클래스 또는 구조체에서로 `Boolean`의 축소 변환 연산자입니다.  
  
 `Boolean` 또는 연산자로의변환이정의되지않은경우컴파일러는오류를표시합니다.`IsTrue`  
  
> [!NOTE]
> 연산자를 오버 로드할 수 있습니다. 즉, 해당 피연산자의 형식이 해당 클래스 또는 구조체의 형식인 경우 클래스 또는 구조체에서 해당 동작을 다시 정의할 수 있습니다. `IsTrue` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 `IsFalse` 및 `IsTrue` 연산자에 대 한 정의를 포함 하는 구조체의 개요를 정의 합니다.  
  
 [!code-vb[VbVbalrOperators#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>참고자료

- [IsFalse 연산자](../../../visual-basic/language-reference/operators/isfalse-operator.md)
- [방법: 연산자 정의](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [OrElse 연산자](../../../visual-basic/language-reference/operators/orelse-operator.md)
