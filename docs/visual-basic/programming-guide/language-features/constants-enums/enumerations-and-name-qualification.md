---
title: 열거형 및 이름 한정(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], enumerations
- Imports statement [Visual Basic], namespace declarations
- declaring namespaces [Visual Basic], enumerations
- name collisions
- ambiguous names [Visual Basic], enumerations
- enumerations [Visual Basic], name qualification
- names [Visual Basic], avoiding conflicts
- namespaces [Visual Basic], declaring
- naming conflicts, enumerations
- naming conflicts, qualifying names
- declaring enumerations
- references [Visual Basic], enumeration members
- naming conventions [Visual Basic], naming conflicts
- declarations [Visual Basic], namespaces
ms.assetid: 08ba2738-df52-4140-bc55-f57c871c9b73
ms.openlocfilehash: f0a806b040720cf6682f8a72025a0590dd4d91f7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61907441"
---
# <a name="enumerations-and-name-qualification-visual-basic"></a>열거형 및 이름 한정(Visual Basic)
일반적으로 열거형의 멤버를 참조 하는 경우 멤버 이름을 열거형 이름으로 정규화 해야 합니다. 예를 들어, 참조 하는 `Sunday` 소속 프로그램 `Days` 열거형을 다음 구문을 사용:  
  
 [!code-vb[VbEnumsTask#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#18)]  
  
## <a name="using-the-imports-statement"></a>Imports 문을 사용 하 여  
 정규화 된 이름을 추가 하 여 방지할 수는 `Imports` 문을 다음 예제와 같이 코드의 네임 스페이스 선언 섹션:  
  
 [!code-vb[VbEnumsTask#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#22)]  
  
 `Imports` 문에 참조 된 프로젝트 및 어셈블리에서 내 네임 스페이스 이름을 가져옵니다 동일한 문에 표시 되는 모듈 프로젝트입니다. 이 문이 추가 되 면 다음 예제와 같이, 한정자 없이 열거형 멤버를 참조할 수 있습니다.  
  
 [!code-vb[VbEnumsTask#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#24)]  
  
 열거형에 관련 된 상수 집합으로 구성 하 여 다른 컨텍스트에서 이름과 상수를 사용할 수 있습니다. 요일 상수에 대 한 동일한 이름을 사용할 수는 예를 들어 합니다 `Days` 및 `WorkDays` 열거형입니다. 사용 하는 경우는 `Imports` 열거형을 사용 하 여 문을 않도록 주의 해야 참조가 모호해 지지 않도록 합니다. 다음 예제를 참조하세요.  
  
 [!code-vb[VbEnumsTask#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#22)]  
  
 [!code-vb[VbEnumsTask#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#25)]  
  
 가정 `Monday` 둘 다의 구성원은 `Days` 열거형 및 `Workdays` 열거형이이 코드는 컴파일러 오류를 생성 합니다. 각 상수를 참조할 때 참조가 모호해 지지 않도록, 열거를 사용 하 여 상수 이름을 한정 합니다. 다음 코드를 참조 하는 `Saturday` 의 상수를 `Days` 및 `WorkDays` 열거형입니다.  
  
 [!code-vb[VbEnumsTask#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#32)]  
  
## <a name="see-also"></a>참고자료

- [상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)
- [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [방법: Visual Basic에서 열거형 반복](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [방법: 열거형 값과 연결 된 문자열 확인](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [열거형을 사용하는 경우](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [상수 및 리터럴 데이터 형식](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [Enum 문](../../../../visual-basic/language-reference/statements/enum-statement.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
