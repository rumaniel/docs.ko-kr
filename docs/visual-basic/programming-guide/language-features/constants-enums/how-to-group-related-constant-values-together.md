---
title: '방법: 그룹 관련된 상수 값 그룹화 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic], constants
- constants [Visual Basic], grouping together
ms.assetid: 09d61da5-c940-4126-a79f-ba93c36653dc
ms.openlocfilehash: a4f74e48cfdd5c0bc0f745d0f32eb39442f5bd83
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61906765"
---
# <a name="how-to-group-related-constant-values-together-visual-basic"></a>방법: 그룹 관련된 상수 값 그룹화 (Visual Basic)
열거형은 가장 좋은 방법은 관련된 상수를 그룹화 합니다. 사용 하 여 열거형을 만듭니다는 `Enum` 클래스 또는 모듈의 선언 섹션에서 문입니다. 자세한 내용은 [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)합니다.  
  
### <a name="to-group-related-constant-values"></a>그룹에 관련 상수 값  
  
1. 코드 액세스 수준에 포함 하는 선언을 작성 합니다 `Enum` 키워드 및 유효한 이름이입니다. 이 예제에서는 합니다 `Private` 열거형 `temperatureValues`합니다.  
  
     [!code-vb[VbEnumsTask#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#21)]  
  
2. 열거형의 상수를 정의 합니다. 이 예제에서는 합니다 `Public` 열거형 `temperatureValues` 값을 할당 합니다.  
  
     [!code-vb[VbEnumsTask#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [열거형을 사용하는 경우](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [상수 개요](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)
- [상수 및 리터럴 데이터 형식](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)
