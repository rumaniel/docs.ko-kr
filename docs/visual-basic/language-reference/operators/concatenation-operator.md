---
title: '&amp; 연산자 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.&
helpviewer_keywords:
- And (&) operator
- ampersand operator (&)
- '& operator'
- concatenation operators [Visual Basic], syntax
- strings [Visual Basic], concatenating
ms.assetid: fefc3d00-cbf1-475c-8c5e-6fb213b3f85a
ms.openlocfilehash: aaa7c1b9ab7f6c920180d97b55c3bdeb23f00e02
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592240"
---
# <a name="amp-operator-visual-basic"></a>&amp; 연산자 (Visual Basic)
두 식의 문자열 연결을 생성 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
result = expression1 & expression2  
```  
  
## <a name="parts"></a>요소  
 `result`  
 필수. @No__t-0 또는 `Object` 변수  
  
 `expression1`  
 필수. @No__t-0으로 확대 되는 데이터 형식의 식입니다.  
  
 `expression2`  
 필수. @No__t-0으로 확대 되는 데이터 형식의 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 또는 `expression2`의 데이터 형식이 `String`가 아니지만 `String`으로 확대 된 경우 `String`로 변환 됩니다. 데이터 형식 중 하나가 `String`으로 확장 되지 않는 경우 컴파일러에서 오류를 생성 합니다.  
  
 @No__t-0의 데이터 형식은-1 @no__t. 하나 또는 두 식이 모두 [Nothing](../../../visual-basic/language-reference/nothing.md) 으로 평가 되거나 @no__t 값이-1 인 경우 값이 "" 인 문자열로 처리 됩니다.  
  
> [!NOTE]
> 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `&` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
> [!NOTE]
> 앰퍼샌드 (&) 문자를 사용 하 여 변수를 `Long` 형식으로 식별할 수도 있습니다. 자세한 내용은 [형식 문자](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)를 참조 하십시오.  
  
## <a name="example"></a>예제  
 이 예에서는 `&` 연산자를 사용 하 여 문자열 연결을 강제 적용 합니다. 결과는 두 문자열 피연산자의 연결을 나타내는 문자열 값입니다.  
  
 [!code-vb[VbVbalrOperators#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#2)]  
  
## <a name="see-also"></a>참조

- [&= 연산자](../../../visual-basic/language-reference/operators/and-assignment-operator.md)
- [연결 연산자](../../../visual-basic/language-reference/operators/concatenation-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic의 연결 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)
