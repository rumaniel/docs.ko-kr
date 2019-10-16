---
title: 형식 승격(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], scope
- visibility [Visual Basic], declared elements
- Partial keyword [Visual Basic], unexpected results with type promotion
- scope [Visual Basic], declared elements
- scope [Visual Basic], Visual Basic
- type promotion
- declared elements [Visual Basic], visibility
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
ms.openlocfilehash: 02d53770186f7600b190231dc73938ff1589cef6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64610352"
---
# <a name="type-promotion-visual-basic"></a>형식 승격(Visual Basic)
모듈의 프로그래밍 요소를 선언 하면 Visual Basic 모듈을 포함 하는 네임 스페이스에 해당 범위를 승격 합니다. 이 이라고 *형식 승격*합니다.  
  
 다음 예제에서는 모듈의 기본 정 및 해당 모듈의 두 가지 멤버를 보여 줍니다.  
  
 [!code-vb[VbVbalrDeclaredElements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#1)]  
  
 내 `projModule`프로그래밍, 모듈 수준에서 선언 된 요소 수준이 올려진 `projNamespace`합니다. 위의 예에서 `basicEnum` 및 `innerClass` 승격 되 면 있지만 `numberSub` 모듈 수준에서 선언 되지 않았으므로 되지 않습니다.  
  
## <a name="effect-of-type-promotion"></a>형식 승격의 효과  
 형식 승격의 효과 한정 문자열 모듈 이름을 포함할 필요가 없습니다. 다음 예제에서는 앞의 예제에서 절차를 두 번 호출을 만듭니다.  
  
 [!code-vb[VbVbalrDeclaredElements#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#2)]  
  
 앞의 예제에서 첫 번째 호출에서는 완전 한 한정 문자열을 사용 합니다. 그러나이 필요 없는 형식 승격 때문입니다. 두 번째 호출도 액세스 모듈의 멤버를 포함 하지 않고 `projModule` 한정 문자열에 있습니다.  
  
## <a name="defeat-of-type-promotion"></a>형식 승격의 무효화  
 네임 스페이스 모듈 멤버와 동일한 이름 가진 멤버가 이미 있으면 형식 승격이 무효화 됩니다 해당 모듈 멤버에 대 한 합니다. 다음 예제에서는 열거형과 동일한 네임 스페이스 내에 모듈의 기본 정의 보여 줍니다.  
  
 [!code-vb[VbVbalrDeclaredElements#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#3)]  
  
 앞의 예제에서 Visual Basic 클래스를 승격할 수 없습니다 `abc` 에 `thisNameSpace` 네임 스페이스 수준에서 동일한 이름의 열거형 이미 있기 때문입니다. 에 액세스 하려면 `abcSub`, 정규화 문자열을 사용 해야 `thisNamespace.thisModule.abc.abcSub`합니다. 그러나 클래스 `xyz` 는 여전히 승격 액세스할 수 있습니다 `xyzSub` 짧은 한정 문자열을 사용 하 여 `thisNamespace.xyz.xyzSub`입니다.  
  
### <a name="defeat-of-type-promotion-for-partial-types"></a>부분 형식에 대 한 형식 승격의 무효화  
 클래스 또는 모듈 내에서 구조를 사용 하 여 [부분](../../../../visual-basic/language-reference/modifiers/partial.md) 키워드, 형식 승격을 자동으로 통과 해당 클래스 또는 구조체에 대 한 네임 스페이스에 동일한 이름 가진 멤버가 있는지 여부. 모듈의 다른 요소 형식 승격 여전히 가능합니다.  
  
 **결과가 발생 합니다.** 패배 부분 정의의 형식 승격의 예기치 않은 결과 및 컴파일러 오류도 발생할 수 있습니다. 다음 예제에서는 그 중 하나는 모듈 내에서 클래스의 기본 부분 정의 보여 줍니다.  
  
 [!code-vb[VbVbalrDeclaredElements#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#4)]  
  
 앞의 예제에서 개발자의 두 개의 partial 정의 병합 하려면 컴파일러 예상 `sampleClass`합니다. 하지만 컴파일러 내에서 부분 정의 대 한 승격을 고려 하지 않습니다 `sampleModule`합니다. 결과적으로 두 개의 개별 클래스를 컴파일하려고 시도 이라는 `sampleClass` 했지만 다른 한정 경로입니다.  
  
 컴파일러는 정규화된 경로가 동일한 경우에만 부분 정의를 병합합니다.  
  
## <a name="recommendations"></a>권장 사항  
 다음 권장 사항을 바람직한 프로그래밍 관행을 나타냅니다.  
  
- **고유 이름입니다.** 프로그래밍 요소의 이름을 지정 하는 완전히 제어할 경우 때 항상 고유 이름을 사용 하는 것이 좋습니다. 동일한 이름 추가 자격 요구 및 코드를 읽기 어렵게 만들 수 있습니다. 사소한 오류와 예기치 않은 결과가 발생할 수도 있습니다.  
  
- **정규화 합니다.** 모듈과 동일한 네임 스페이스의 다른 요소를 사용 하 여 작업할 때 가장 안전한 방법은 항상 모든 프로그래밍 요소에 대 한 정규화를 사용 하는 것입니다. 형식 승격 모듈 멤버의 수 이며 해당 멤버를 완벽 하 게 적합 하지 않습니다, 경우 실수로 다른 프로그래밍 요소를 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Module 문](../../../../visual-basic/language-reference/statements/module-statement.md)
- [Namespace 문](../../../../visual-basic/language-reference/statements/namespace-statement.md)
- [부분](../../../../visual-basic/language-reference/modifiers/partial.md)
- [Visual Basic의 범위](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
- [방법: 변수의 범위 제어](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)
- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
