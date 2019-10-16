---
title: 코드의 특수 문자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.)
- vb.(
- vb.colon
- vb.!
- vb..
- 'vb.:'
helpviewer_keywords:
- special characters [Visual Basic], in code
- parentheses [Visual Basic], using in code
- colons (:)
- period character in code
- dot operator (.)
- dictionary access operator [Visual Basic]
- concatenation operators [Visual Basic], special characters in code
- concatenation operators [Visual Basic], vs. addition operator
- '! operator'
- separators [Visual Basic], using in code
- operators [Visual Basic], dictionary access
- ': separator character'
- member access operator [Visual Basic]
- addition operator [Visual Basic]
- operators [Visual Basic], member access
- . operator
- exclamation points
- separators
- exclamation point operator (!)
- Visual Basic code, special characters
ms.assetid: 310dce0c-45b5-4e0d-83e9-32df258d2a3e
ms.openlocfilehash: 95bef937912e35cd828bf0090b4cf48ccb3290cc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962469"
---
# <a name="special-characters-in-code-visual-basic"></a>코드의 특수 문자(Visual Basic)
코드에서 특수 문자를 사용 해야 하는 경우가 있습니다. 즉, 영문자 또는 숫자가 아닌 문자를 사용 해야 합니다. Visual Basic 문자 집합의 문장 부호와 특수 문자는 프로그램 텍스트 구성에서 컴파일러 또는 컴파일된 프로그램이 수행 하는 작업을 정의 하는 다양 한 용도로 사용 됩니다. 이러한 특수 문자는 수행할 작업을 지정하지 않습니다.  
  
## <a name="parentheses"></a>괄호  
 `Sub` 또는`Function`와 같은 프로시저를 정의할 때 괄호를 사용 합니다. 모든 프로시저 인수 목록을 괄호로 묶어야 합니다. 또한 괄호를 사용 하 여 변수 또는 인수를 논리 그룹에 추가 합니다. 특히 복잡 한 식에서 연산자 우선 순위의 기본 순서를 재정의 합니다. 다음은 이에 대한 예입니다.  
  
 [!code-vb[VbVbcnConventions#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#11)]  
  
 이전 코드를 실행 하면의 `d` 값이 8.225이 고 `e` 값은 3입니다. 에 대 한 `d` 계산은 `/` `d = b + (c / a)`의 기본 우선 순위를 사용 하며와동일합니다.`+` 계산에서의 괄호는 기본 `e` 우선 순위를 재정의 합니다.  
  
## <a name="separators"></a>Separators  
 구분 기호는 이름에서 제안 하는 것을 의미 합니다. 코드 섹션을 구분 합니다. Visual Basic에서 구분 기호 문자는 콜론 (`:`)입니다. 별도의 줄 대신 한 줄에 여러 문을 포함 하려면 구분 기호를 사용 합니다. 이렇게 하면 공간이 절약 되 고 코드의 가독성이 향상 됩니다. 다음 예에서는 콜론으로 구분 된 세 개의 문을 보여 줍니다.  
  
 [!code-vb[VbVbcnConventions#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#12)]  
  
 자세한 내용은 [방법: 코드](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)에서 문을 중단 하 고 결합 합니다.  
  
 또한 콜론 (`:`) 문자는 문 레이블을 식별 하는 데 사용 됩니다. 자세한 내용은 [방법: 레이블 문](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md).  
  
## <a name="concatenation"></a>연결 연산  
 연산자를 `&` 사용 하 여 *연결*하거나 문자열을 연결 합니다. 숫자 값을 더하는 `+` 연산자와 혼동 하지 마십시오. `+` 연산자를 사용 하 여 숫자 값에 대해 작업할 때 연결 하는 경우 잘못 된 결과를 얻을 수 있습니다. 다음은 이에 대한 예입니다.  
  
 [!code-vb[VbVbcnConventions#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#13)]  
  
 이전 코드를 실행 하면의 `resultA` 값이 21.01이 고 `resultB` 값이 "10.0111"입니다.  
  
## <a name="member-access-operators"></a>멤버 액세스 연산자  
 형식의 멤버에 액세스 하려면 형식 이름과 멤버 이름 사이에 점 (`.`) 또는 느낌표 (`!`) 연산자를 사용 합니다.  
  
### <a name="dot--operator"></a>점 (.) 연산자  
 클래스, `.` 구조체, 인터페이스 또는 열거형에 대해 연산자를 멤버 액세스 연산자로 사용 합니다. 멤버는 필드, 속성, 이벤트 또는 메서드 일 수 있습니다. 다음은 이에 대한 예입니다.  
  
 [!code-vb[VbVbcnConventions#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#14)]  
  
### <a name="exclamation-point--operator"></a>느낌표 (!) 연산자  
 클래스 또는 `!` 인터페이스에 대해서만 연산자를 사전 액세스 연산자로 사용 합니다. 클래스 또는 인터페이스에는 단일 `String` 인수를 허용 하는 기본 속성이 있어야 합니다. `!` 연산자 바로 다음에 오는 식별자는 기본 속성에 문자열로 전달 되는 인수 값이 됩니다. 다음은 이에 대한 예입니다.  
  
 [!code-vb[VbVbcnConventions#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#15)]  
  
 모든의 `MsgBox` 출력 줄에는 값 `32856`이 표시 됩니다. 첫 번째 줄에서는 기존 속성 `index`에 대 한 액세스를 사용 하 고, 두 번째 줄은 클래스 `hasDefault`의 기본 속성인 `index` 팩트를 사용 하며, 세 번째 줄은 클래스에 대 한 사전 액세스를 사용 합니다.  
  
 `!` 연산자의 두 번째 피연산자는 큰따옴표 (`" "`)로 묶여 있지 않은 유효한 Visual Basic 식별자 여야 합니다. 즉, 문자열 리터럴 또는 문자열 변수를 사용할 수 없습니다. 이 `MsgBox` 호출의 마지막 줄을 다음과 같이 변경 하면가 포함 된 문자열 `"X"` 리터럴이어야 하므로 오류가 발생 합니다.  
  
 `"Dictionary access returns " & hD!"X")`  
  
> [!NOTE]
> 기본 컬렉션에 대 한 참조는 명시적 이어야 합니다. 특히 런타임에 바인딩된 변수에는 `!` 연산자를 사용할 수 없습니다.  
  
 문자는 문자 `Single` 형식으로도 사용 됩니다. `!`  
  
## <a name="see-also"></a>참고자료

- [프로그램 구조 및 코드 규칙](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [형식 문자](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
