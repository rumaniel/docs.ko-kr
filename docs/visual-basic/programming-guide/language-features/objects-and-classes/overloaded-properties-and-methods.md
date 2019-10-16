---
title: 오버 로드 된 속성 및 메서드 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- properties [Visual Basic], overloading
- methods [Visual Basic], overloading
- shadowing
- names [Visual Basic], multiple procedures with same
- procedures [Visual Basic], multiples with same name
- classes [Visual Basic], properties
- classes [Visual Basic], methods
- method overloading
- Overloads keyword [Visual Basic], overloaded members
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
ms.openlocfilehash: 8d7341370d9770d2e57f786ac7c68277e66a9bbd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61864873"
---
# <a name="overloaded-properties-and-methods-visual-basic"></a>오버 로드 된 속성 및 메서드 (Visual Basic)

오버 로드 둘 이상의 프로시저, 인스턴스 생성자 또는 속성 이름은 같지만 다른 형식의 인수를 사용 하 여 클래스에서 생성 됩니다.

## <a name="overloading-usage"></a>오버 로드 사용

오버 로드 개체 모델에 다른 데이터 형식에서 작동 하는 프로시저에 대해 동일한 이름을 사용 하도록 요구할 때 특히 유용 합니다. 예를 들어, 여러 다른 데이터 형식을 표시할 수 있는 클래스를 가지기 `Display` 는 다음과 같은 절차:

[!code-vb[VbVbalrOOP#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#64)]

오버 로드를 허용 하지 않고 다음과 같이 동일한 작업을 수행 하는 경우에 각 프로시저에 대 한 고유한 이름을 만들기 위해 해야 확인 메시지가 나타납니다.

[!code-vb[VbVbalrOOP#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#65)]

오버 로드 쉽게 사용할 수 있는 데이터 형식의 선택할을 제공 하기 때문에 속성 또는 메서드를 사용 합니다. 예를 들어 오버 로드 된 `Display` 설명 이전에 메서드 코드의 다음 줄 중 하나를 사용 하 여:

[!code-vb[VbVbalrOOP#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#66)]

Visual Basic 런타임에 지정할 매개 변수의 데이터 형식을 기반으로 올바른 프로시저를 호출 합니다.

## <a name="overloading-rules"></a>오버 로드 규칙

 두 개 이상의 속성 또는 동일한 이름 가진 메서드를 추가 하 여 클래스에 대 한 오버 로드 된 멤버를 만듭니다. 오버 로드 된 파생된 멤버를 제외 하 고 각 오버 로드 된 멤버는 다른 매개 변수 목록이 있어야 합니다. 및 속성 또는 프로시저를 오버 로드할 때 다음 항목을 별도 기능으로 사용할 수 없습니다.

- 한정자와 같은 `ByVal` 또는 `ByRef`, 멤버 또는 멤버의 매개 변수를 적용 하는 합니다.

- 매개 변수 이름

- 프로시저의 반환 형식

합니다 `Overloads` 오버 로드를 허용 하는 경우 키워드는 선택 사항 이지만 멤버를 사용 하는 경우 오버 로드는 `Overloads` 키워드 다음 다른 모든 오버 로드 된 멤버 이름이 같은이 키워드를 지정 해야이 합니다.

파생된 클래스에서 멤버를 동일한 매개 변수 및 매개 변수 형식으로 알려진 프로세스를 사용 하 여 상속 된 멤버를 오버 로드할 수 있습니다 *이름 및 시그니처 별로 섀도잉*합니다. 경우는 `Overloads` 이름 및 시그니처 별로 숨김에 멤버의 파생된 클래스의 구현을 사용할 기본 클래스에서 구현 하는 대신 및 해당 멤버에 대 한 다른 모든 오버 로드의 인스턴스를 사용할 때 키워드를 사용 합니다 파생된 클래스입니다.

경우는 `Overloads` 은 동일한 매개 변수 및 매개 변수 형식이 아닌 멤버와 상속된 된 멤버를 오버 로드할 때 키워드를 생략 하면 다음는 오버 로딩 이라고 *이름별 섀도잉*합니다. 멤버의 상속 된 구현을 대체 이름으로 섀도잉 고 다른 모든 오버 로드 관련 계승자와 파생된 클래스의 인스턴스를 사용할 수 없습니다.

합니다 `Overloads` 및 `Shadows` 한정자 동일한 속성 또는 메서드 함께 사용할 수 없습니다.

### <a name="example"></a>예제

다음 예제 중 하나를 허용 하는 오버 로드 된 메서드를 만듭니다는 `String` 또는 `Decimal` 달러 금액 및 반환 판매세가 포함 된 문자열 표현입니다.

#### <a name="to-use-this-example-to-create-an-overloaded-method"></a>오버 로드 된 메서드를 만들려면이 예제를 사용 하려면

1. 새 프로젝트를 열고 라는 클래스를 추가 `TaxClass`합니다.

2. `TaxClass` 클래스에 다음 코드를 추가합니다.

    [!code-vb[VbVbalrOOP#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#67)]

3. 다음 절차를 폼에 추가 합니다.

    [!code-vb[VbVbalrOOP#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#68)]

4. 호출 프로그램과 폼에 단추를 추가 합니다 `ShowTax` 프로시저는 `Button1_Click` 단추의 이벤트.

5. 프로젝트를 실행 하 고 오버 로드 된 테스트 폼에서 단추를 클릭 `ShowTax` 프로시저입니다.

런타임 시 컴파일러에 사용 되는 매개 변수와 일치 하는 적절 한 오버 로드 된 함수를 선택 합니다. 오버 로드 된 메서드를 사용 하 여 먼저 호출 단추를 클릭 하면는 `Price` 매개 변수는 문자열 및 메시지를 "가격 is a String입니다. 세금은 $5.12"표시 됩니다. `TaxAmount` 사용 하 여 호출 되는 `Decimal` 값 두 번째 시간 및 메시지, "가격은 10 진수입니다. 세금은 $5.12"표시 됩니다.

## <a name="see-also"></a>참고자료

- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [Visual Basic의 숨김 기능](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
- [Sub 문](../../../../visual-basic/language-reference/statements/sub-statement.md)
- [상속 기본 사항](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
- [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)
- [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)
- [오버로드](../../../../visual-basic/language-reference/modifiers/overloads.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
