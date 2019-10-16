---
title: 사용자 정의 상수(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic], circular references
- Const statement [Visual Basic], user-defined constants
- user-defined constants [Visual Basic]
- scope [Visual Basic], constants
- constants [Visual Basic], user-defined
- circular references between constants [Visual Basic]
ms.assetid: a1206d5c-c45e-4ac2-970a-4a0be6a05fdd
ms.openlocfilehash: 5d4fe5d1b9048f4a8ae22a84e14456318ca38f0f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645855"
---
# <a name="user-defined-constants-visual-basic"></a>사용자 정의 상수(Visual Basic)
상수는 숫자 또는 변경 되지 않는 문자열의 발생 하는 의미 있는 이름입니다. 상수는 애플리케이션 실행 중 변함없이 유지되는 값을 저장합니다. 컨트롤 또는 구성 요소를 사용 하 여 작업에 의해 정의 된 상수를 사용할 수 있습니다 하거나 직접 만들 수 있습니다. 사용자가 직접 만든 상수 상수 라고 *사용자 정의*합니다.  
  
 상수를 선언 하는 `Const` 변수 이름을 만들 경우 동일한 지침을 사용 하 여 문입니다. 하는 경우 `Option Strict` 는 `On`, 상수 형식을 명시적으로 선언 해야 합니다.  
  
## <a name="const-statement-usage"></a>Const 문 사용  
 `Const` 문 수 수치를 나타내거나 날짜/시간 값:  
  
 [!code-vb[VbEnumsTask#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#10)]  
  
 정의할 수도 있습니다 `String` 상수:  
  
 [!code-vb[VbEnumsTask#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#13)]  
  
 등호의 오른쪽에 있는 식 ( `=` )는 종종 숫자 또는 리터럴 문자열 이지만 (하지만 해당 식은 함수 호출을 포함할 수 없습니다) 숫자 또는 문자열에서 발생 하는 식일 수 있습니다. 이전에 정의 된 상수를 기준으로 상수를 정의할 수도 있습니다.  
  
 [!code-vb[VbEnumsTask#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#15)]  
  
## <a name="scope-of-user-defined-constants"></a>사용자 정의 상수 범위  
 `Const` 문의 범위는 같은 위치에 선언 된 변수의 것과 동일 합니다. 다음 방법 중 하나에서 범위를 지정할 수 있습니다.  
  
- 프로시저 내에 존재 하는 상수를 만들려면 해당 절차 내에서 선언 합니다.  
  
- 모듈 외부 코드 아니라 클래스 내의 모든 프로시저에 사용할 수 있는 상수를 만들려면 클래스의 선언 섹션에서 선언 합니다.  
  
- 어셈블리의 외부 클라이언트가 아니라 어셈블리의 모든 멤버에 사용할 수 있는 상수를 만들려면 사용 하 여 선언 된 `Friend` 클래스의 선언 섹션에는 키워드입니다.  
  
- 응용 프로그램 전체에서 사용할 수 있는 상수를 만들려면 사용 하 여 선언 된 `Public` 선언에서 키워드 섹션 클래스입니다.  
  
 자세한 내용은 [방법: 상수 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)합니다.  
  
### <a name="avoiding-circular-references"></a>순환 참조 방지  
 다른 상수를 기준으로 상수를 정의할 수 있습니다, 되므로 실수로 만들 수는 *주기*, 또는 두 개 이상의 상수 간의 순환 참조를 합니다. 주기를 두 개 이상의 공용 상수를 각각 다음 예제와 같이 다른 측면에서 정의 된 경우 발생 합니다.  
  
 [!code-vb[VbEnumsTask#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#16)]  
[!code-vb[VbEnumsTask#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#17)]  
  
 주기가 발생 하는 경우 Visual Basic 컴파일러 오류를 생성 합니다.  
  
## <a name="see-also"></a>참고자료

- [Const 문](../../../../visual-basic/language-reference/statements/const-statement.md)
- [상수 및 리터럴 데이터 형식](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [상수 및 열거형](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)
- [상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)
- [열거형 개요](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
- [상수 개요](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)
- [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
