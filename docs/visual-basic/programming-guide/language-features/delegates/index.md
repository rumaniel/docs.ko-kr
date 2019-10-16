---
title: 대리자(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [Visual Basic]
- Visual Basic code, delegates
ms.assetid: 410b60dc-5e60-4ec0-bfae-426755a2ee28
ms.openlocfilehash: b3f333f1714a66a8ff462000385af92cf343a19e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62050599"
---
# <a name="delegates-visual-basic"></a>대리자(Visual Basic)

대리자는 메서드를 참조하는 개체입니다. 다른 프로그래밍 언어에서 사용되는 함수 포인터와 비슷하기 때문에 *형식 안전 함수 포인터*라고도 합니다. 함수 포인터와 달리 Visual Basic 대리자는 클래스를 기반으로 하는 참조 형식 <xref:System.Delegate?displayProperty=nameWithType>합니다. 대리자는 공유 메서드(클래스의 특정 인스턴스 없이 호출할 수 있는 메서드) 및 인스턴스 메서드를 둘 다 참조할 수 있습니다.

## <a name="delegates-and-events"></a>대리자 및 이벤트

대리자는 호출 프로시저와 호출되는 프로시저 간에 중개자가 필요한 경우에 유용합니다. 예를 들어 다양한 상황에서 다른 이벤트 처리기를 호출하도록 하는 이벤트를 발생시키는 개체를 원할 수 있습니다. 그러나 이벤트를 발생시키는 개체는 특정 이벤트를 처리할 이벤트 처리기가 어느 것인지를 미리 알 수 없습니다. Visual Basic 사용 하면 이벤트를 사용 하 여 동적으로 연결할 이벤트 처리기 대리자를 사용 하는 경우 만들어를 `AddHandler` 문입니다. 런타임 시 대리자는 적절한 이벤트 처리기로 호출을 전달합니다.

사용자가 직접 대리자를 만들 수 있지만 대부분의 경우에서 Visual Basic 대리자를 만들고 세부 정보를 처리 합니다. 예를 들어 `Event` 문은 `<EventName>EventHandler`라는 대리자 클래스를 `Event` 문을 포함하고 이벤트와 시그니처가 같은 클래스의 중첩 클래스로 암시적으로 정의합니다. `AddressOf` 문은 특정 프로시저를 참조하는 대리자의 인스턴스를 암시적으로 만듭니다. 다음 두 코드 줄은 동일한 의미를 갖습니다. 첫 번째 줄에서는 `Button1_Click` 메서드에 대한 참조가 인수로 전달된 `EventHandler`의 인스턴스를 명시적으로 만듭니다. 두 번째 줄은 동일한 작업을 좀 더 편리하게 수행합니다.

[!code-vb[VbVbalrDelegates#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#6)]

컴파일러가 어디에서든지 상황에 따라 대리자의 형식을 결정할 수 있도록 대리자를 만드는 간단한 방법을 사용할 수 있습니다.

## <a name="declaring-events-that-use-an-existing-delegate-type"></a>기존 대리자 형식을 사용하는 이벤트 선언

일부 경우에 기존 대리자 형식을 내부 대리자로 사용하도록 이벤트를 선언하려고 할 수 있습니다. 다음 구문에 해당 방법이 나와 있습니다.

[!code-vb[VbVbalrDelegates#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#7)]

동일한 처리기로 여러 이벤트 라우팅하려는 경우에 유용합니다.

## <a name="delegate-variables-and-parameters"></a>대리자 변수 및 매개 변수

빈 스레드 또는 런타임에 다른 버전의 함수를 호출해야 하는 프로시저 등, 이벤트와 관련되지 않은 다른 작업에 대리자를 사용할 수 있습니다.

예를 들어 자동차 이름에 목록 상자를 포함하는 광고 애플리케이션을 분류한다고 가정합니다. 광고는 일반적으로 자동차 제조업체에 해당하는 제목별로 정렬됩니다. 일부 자동차의 제조업체 앞에 자동차 연식이 포함되어 있을 때 문제가 발생할 수 있습니다. 문제는 목록 상자의 기본 제공 정렬 기능이 문자 코드를 기준으로만 정렬된다는 것입니다. 즉, 모든 광고는 날짜 순서로 배치된 다음 제조업체 순서로 정렬됩니다.

이 문제를 해결하려면 대부분의 목록 상자에 대해 표준 사전순 정렬을 사용하지만 자동차 광고의 경우는 런타임에 사용자 지정 정렬 프로시저로 전환할 수 있는 정렬 프로시저를 클래스에 만들 수 있습니다. 이렇게 하려면 대리자를 사용하여 런타임에 정렬 클래스에 사용자 지정 정렬 프로시저를 전달합니다.

## <a name="addressof-and-lambda-expressions"></a>AddressOf 및 람다 식

각 대리자 클래스는 개체 메서드의 사양이 전달되는 생성자를 정의합니다. 대리자 생성자에 대한 인수는 메서드 또는 람다 식에 대한 참조여야 합니다.

메서드에 대한 참조를 지정하려면 다음 구문을 사용합니다.

`AddressOf` [`expression`.]`methodName`

`expression`의 컴파일 타임 형식은 해당 시그니처가 대리자 클래스의 시그니처와 일치하는 지정된 이름의 메서드를 포함하는 클래스 또는 인터페이스의 이름이어야 합니다. `methodName`은 공유 메서드이거나 인스턴스 메서드일 수 있습니다. `methodName`은 클래스의 기본 메서드에 대해 대리자를 만들더라도 선택 사항이 아닙니다.

람다 식을 지정하려면 다음 구문을 사용합니다.

`Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`

다음 예제에서는 대리자에 대한 참조를 지정하는 데 사용되는 `AddressOf` 및 람다 식을 둘 다 보여 줍니다.

[!code-vb[VbVbalrDelegates#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class2.vb#15)]

함수의 시그니처는 대리자 형식의 시그니처와 일치해야 합니다. 람다 식에 대한 자세한 내용은 [람다 식](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)을 참조하세요. 대리자에 대한 람다 식 및 `AddressOf` 대입의 추가 예제를 보려면 [완화된 대리자 변환](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)을 참조하세요.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[방법: 대리자 메서드 호출](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)|메서드를 대리자를 연결하고 대리자를 통해 해당 메서드를 호출하는 방법을 보여 주는 예제를 제공합니다.|
|[방법: 프로시저에 Visual Basic에서 다른 프로시저 전달](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)|대리자를 사용하여 한 프로시저를 다른 프로시저에 전달하는 방법을 보여 줍니다.|
|[완화된 대리자 변환](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)|시그니처가 동일하지 않더라도 sub 및 함수를 대리자 또는 처리기에 할당하는 방법을 설명합니다.|
|[이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)|Visual Basic의 이벤트에 대해 간략하게 설명합니다.|
