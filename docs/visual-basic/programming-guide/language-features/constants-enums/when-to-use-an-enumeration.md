---
title: 열거형을 사용하는 경우(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
ms.assetid: e6e47b5b-3ed9-452d-a481-9c3fed88519a
ms.openlocfilehash: a43c55d4ad6a895957b53ae18c3641c5383a24ce
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64585070"
---
# <a name="when-to-use-an-enumeration-visual-basic"></a>열거형을 사용하는 경우(Visual Basic)
열거형에는 관련 된 상수 집합을 사용 하는 간편한 방법은 제공 합니다. 열거형, 또는 `Enum`, 기호화 된 이름 값의 집합입니다. 열거형 데이터 형식으로 처리 됩니다 하 고 변수 및 속성과 함께 사용할 상수 집합을 사용할 수 있습니다.  
  
## <a name="when-to-use-an-enumeration"></a>열거형을 사용하는 경우  
 프로시저에서 변수 집합을 제한, 열거형을 사용 하는 것이 좋습니다. 열거형은 의미 있는 이름을 사용 하는 경우에 특히 보다 명확 하 고 좀 더 읽기 쉬운 코드를 확인 합니다.  
  
 열거형을 사용 하는 이점은 다음과 같습니다.  
  
- 숫자를 잘못 입력 하 여 발생 한 오류를 줄입니다.  
  
- 에서는 값을 나중에 변경 하기가 쉽습니다.  
  
- 에서는 코드는 오류 쉬워지므로 발생할 가능성이 줄어듭니다 즉를 쉽게 읽을 수 있습니다.  
  
- 이후 버전과 호환성을 확인합니다. 열거형을 사용 하 여 코드는 멤버 이름에 해당 하는 값을 나중에 변경 되 면 실패할 가능성이 적습니다.  
  
## <a name="naming-enumerations"></a>열거형 이름 지정  
 열거형 멤버에 대 한 명명 규칙을 사용 합니다. Visual Basic에서 열거형 멤버 이름을 발견, 다른 참조 된 형식 라이브러리에는 동일한 이름을 포함 하는 경우 예외가 throw 될 수 있습니다. 응용 프로그램 또는 구성 요소에서 값을 식별 하는 고유한 접두사를 사용 합니다.  
  
 열거형의 멤버를 참조 하는 경우 있습니다 해야 열거형 이름으로 멤버 이름을 한 정하는 그렇지 않으면 사용 된 `Imports` 문입니다. 자세한 내용은 [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)합니다.  
  
## <a name="predefined-enumerations"></a>미리 정의 된 열거형  
 Visual Basic과 같은 다양 한 미리 정의 된 열거를 제공 합니다 `FirstDayOfWeek` 고 `MsgBoxResult`, 코드를 용이 하 게 합니다. 이러한 목록은 참조 하세요. [상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [방법: Visual Basic에서 열거형 반복](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [방법: 열거형 값과 연결 된 문자열 확인](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [Enum 문](../../../../visual-basic/language-reference/statements/enum-statement.md)
- [상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)
