---
title: Nothing(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Nothing
- vb.Nothing
helpviewer_keywords:
- Nothing keyword [Visual Basic]
- Nothing keyword [Visual Basic], syntax
ms.assetid: 06176e2d-bbf7-4a37-afaa-a86ad21ee99f
ms.openlocfilehash: 12c88db49dc7723fc269195e7d174bfa822c64d3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963754"
---
# <a name="nothing-visual-basic"></a>Nothing(Visual Basic)
모든 데이터 형식의 기본값을 나타냅니다. 참조 형식의 경우 기본값 `null` 은 참조입니다. 값 형식의 경우 기본값은 값 형식이 null을 허용 하는지 여부에 따라 달라 집니다.  
  
> [!NOTE]
> Nullable이 아닌 값 형식의 경우의 `Nothing` Visual Basic는의와 `null` 다릅니다 C#. Visual Basic에서 nullable이 아닌 값 형식의 변수를로 `Nothing`설정 하면 변수가 선언 된 형식에 대 한 기본값으로 설정 됩니다. 에서 C#nullable이 아닌 값 형식의 변수를에 `null`할당 하면 컴파일 타임 오류가 발생 합니다.  
  
## <a name="remarks"></a>설명  
 `Nothing`데이터 형식의 기본값을 나타냅니다. 기본값은 변수가 값 형식 인지 참조 형식 인지에 따라 달라 집니다.  
  
 *값 형식의* 변수에는 해당 값이 직접 포함 됩니다. 값 형식에는 모든 숫자 데이터 형식 `Boolean`, `Char`, `Date`,, 모든 구조 및 모든 열거형이 포함 됩니다. *참조 형식의* 변수는 메모리에 있는 개체의 인스턴스에 대 한 참조를 저장 합니다. 참조 형식에는 클래스, 배열, 대리자 및 문자열이 포함 됩니다. 자세한 내용은 [Value Types and Reference Types](../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)을 참조하세요.  
  
 변수가 값 형식이 면 변수의 동작은 `Nothing` 변수가 nullable 데이터 형식 인지에 따라 달라 집니다. Nullable 값 형식을 나타내려면 형식 이름에 `?` 한정자를 추가 합니다. Nullable `Nothing` 변수에를 할당 하면 값이로 `null`설정 됩니다. 자세한 내용 및 예제는 [Nullable 값 형식](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)을 참조 하세요.  
  
 변수가 null을 허용 하지 않는 값 형식인 경우에 할당 `Nothing` 하면 선언 된 형식에 대 한 기본값으로 설정 됩니다. 해당 형식에 변수 멤버가 포함 되어 있으면 모두 기본값으로 설정 됩니다. 다음 예제에서는 스칼라 형식에 대해이를 보여 줍니다.  
  
 [!code-vb[VbVbalrKeywords#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class2.vb#7)]  
  
 변수가 참조 형식이 면 변수에을 할당 `Nothing` 하 여 변수의 형식에 대 한 `null` 참조로 설정 합니다. `null` 참조로 설정 된 변수가 개체와 연결 되어 있지 않습니다. 다음은 이에 대한 예입니다.  
  
 [!code-vb[VbVbalrKeywords#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class3.vb#8)]  
  
 참조 (또는 nullable 값 형식) 변수가 `null`인지 여부를 확인 하는 경우 또는 `<> Nothing`을 `= Nothing` 사용 하지 마세요. 항상 또는 `Is Nothing` `IsNot Nothing`를 사용 합니다.  
  
 Visual Basic 문자열의 경우 빈 문자열은와 같습니다 `Nothing`. `"" = Nothing` 따라서는 true입니다.  
  
 다음 예에서는 `Is` 및 `IsNot` 연산자를 사용 하는 비교를 보여 줍니다.  
  
 [!code-vb[VbVbalrKeywords#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class4.vb#9)]  
  
 `As` 절을 사용 하지 않고 변수를 선언 하 고로 `Nothing`설정 하는 경우 `Object`변수의 형식은입니다. 예를 들면 `Dim something = Nothing`입니다. 가 on이 고 `Option Strict` `Option Infer` 꺼져 있는 경우이 경우 컴파일 타임 오류가 발생 합니다.  
  
 개체 변수에 할당 `Nothing` 하는 경우에는 더 이상 개체 인스턴스를 참조 하지 않습니다. 변수가 이전에 인스턴스를 참조 한 경우로 `Nothing` 설정 하면 인스턴스 자체가 종료 되지 않습니다. 인스턴스가 종료 되 고 해당 인스턴스와 연결 된 메모리 및 시스템 리소스가 해제 된 후에만 GC (가비지 수집기)에서 활성 참조가 남아 있지 않음을 감지한 후에만 해제 됩니다.  
  
 `Nothing`은 <xref:System.DBNull> (는) 초기화 되지 않은 variant 또는 존재 하지 않는 데이터베이스 열을 나타내는 개체와 다릅니다.  
  
## <a name="see-also"></a>참고자료

- [Dim 문](../../visual-basic/language-reference/statements/dim-statement.md)
- [개체 수명: 개체를 만들고 제거 하는 방법](../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
- [Visual Basic 수명](../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)
- [Is 연산자](../../visual-basic/language-reference/operators/is-operator.md)
- [IsNot 연산자](../../visual-basic/language-reference/operators/isnot-operator.md)
- [Nullable 값 형식](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
