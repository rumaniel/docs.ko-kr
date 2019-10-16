---
title: '방법: 열거형 (Visual Basic)를 선언 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], enumerations
- enumerations [Visual Basic], declaring
- declaring enumerations [Visual Basic]
ms.assetid: db4ca1c3-f429-4c81-ae81-29e0157b29fd
ms.openlocfilehash: c74b75adf0f56dd198375cb1ff24656d39ec074c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64610574"
---
# <a name="how-to-declare-enumerations-visual-basic"></a>방법: 열거형 (Visual Basic)를 선언 합니다.
사용 하 여 열거형을 만듭니다는 `Enum` 클래스 또는 모듈을 선언 섹션에서 설명 합니다. 메서드 내에서 열거형을 선언할 수 없습니다. 적절 한 수준의 액세스를 지정 하려면 `Private`, `Protected`를 `Friend`, 또는 `Public`합니다.  
  
 `Enum` 형식에는 이름, 내부 형식 및 필드의 집합을 각각 나타내는 상수입니다. 이름은 유효한 Visual Basic.NET 한정자 여야 합니다. 기본 형식은 정수 형식 중 하나 여야 합니다-`Byte`, `Short`하십시오 `Long` 또는 `Integer`. 기본값은 `Integer`입니다. 열거는 항상 강력한 형식이 지정 되며 정수 숫자 형식으로 서로 바꿔 사용할 수 없습니다.  
  
 열거형 부동 소수점 값을 가질 수 없습니다. 열거형에는 부동 소수점 값을 할당 되 면 `Option Strict On`, 컴파일러 오류가 발생 합니다. 경우 `Option Strict` 됩니다 `Off`, 값을 자동으로 변환 되며는 `Enum` 형식입니다.  
  
 이름에 대 한 정보 및 사용 하는 방법에 대 한 합니다 `Imports` 문을 이름 한정 불필요 참조 [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)합니다.  
  
### <a name="to-declare-an-enumeration"></a>열거형 선언  
  
1. 코드 액세스 수준에 포함 하는 선언을 작성 합니다 `Enum` 키워드 및 다른 선언 각각 다음 예제와 같이 유효한 이름을 `Enum`입니다.  
  
     [!code-vb[VbEnumsTask#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#3)]  
  
2. 열거형의 상수를 정의 합니다. 기본적으로 열거형의 첫 번째 상수를 초기화 `0`, 고 후속 상수 이전 상수 보다 하나 더 큰 값으로 초기화 됩니다. 예를 들어, 다음 열거형 `Days`, 명명 된 상수를 포함 `Sunday` 값을 사용 하 여 `0`, 명명 된 상수 `Monday` 값을 사용 하 여 `1`, 명명 된 상수 `Tuesday` 의값을사용하여`2`등에입니다.  
  
     [!code-vb[VbEnumsTask#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#4)]  
  
3. 대입문을 사용 하 여 열거형에서 상수로 분석 값을 명시적으로 할당할 수 있습니다. 음수를 포함 하 여 모든 정수 값을 할당할 수 있습니다. 예를 들어 상수를 오류 상태를 나타내는 0 보다 작은 값을 사용 하 여 확인할 수 있습니다. 다음 열거형에서 상수 `Invalid` 값을 명시적으로 할당 됩니다 `–1`, 및 상수 `Sunday` 값이 할당 됩니다 `0`합니다. 열거형의 첫 번째 상수 이므로 `Saturday` 또한 값으로 초기화 됩니다 `0`합니다. 값 `Monday` 됩니다 `1` (값 보다 1 더 큽니다 `Sunday`); 값 `Tuesday` 는 `2`등.  
  
     [!code-vb[VbEnumsTask#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#5)]  
  
### <a name="to-declare-an-enumeration-as-an-explicit-type"></a>명시적 형식으로 열거형 선언  
  
- 열거형 형식을 사용 하 여 지정 된 `As` 절을 다음과 같이 합니다.  
  
     [!code-vb[VbEnumsTask#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#6)]  
  
## <a name="see-also"></a>참고자료

- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [방법: Visual Basic에서 열거형 반복](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [방법: 열거형 값과 연결 된 문자열 확인](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [열거형을 사용하는 경우](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [상수 개요](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)
- [상수 및 리터럴 데이터 형식](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [상수 및 열거형](../../../../visual-basic/language-reference/constants-and-enumerations.md)
