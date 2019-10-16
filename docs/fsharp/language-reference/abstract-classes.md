---
title: 추상 클래스
description: 일부 또는 F# 모든 멤버를 구현 하지 않고 다양 한 개체 형식 집합의 공통 기능을 나타내는 추상 클래스에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: d7fc87178cff7c5c824992c97198b49f87025f00
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71082956"
---
# <a name="abstract-classes"></a>추상 클래스

*추상 클래스* 는 파생 클래스에서 구현을 제공할 수 있도록 일부 또는 모든 멤버를 구현 하지 않은 상태로 유지 하는 클래스입니다.

## <a name="syntax"></a>구문

```fsharp
// Abstract class syntax.
[<AbstractClass>]
type [ accessibility-modifier ] abstract-class-name =
[ inherit base-class-or-interface-name ]
[ abstract-member-declarations-and-member-definitions ]

// Abstract member syntax.
abstract member member-name : type-signature
```

## <a name="remarks"></a>설명

개체 지향 프로그래밍에서 추상 클래스는 계층의 기본 클래스로 사용 되며 다양 한 개체 형식 집합의 공통 기능을 나타냅니다. 이름 "abstract"가 암시 하는 것 처럼, 추상 클래스는 문제 도메인의 구체적 엔터티와 직접 일치 하지 않는 경우가 많습니다. 그러나 이러한 항목은 공통 된 다양 한 구체적인 엔터티를 나타냅니다.

추상 클래스에는 `AbstractClass` 특성이 있어야 합니다. 구현 및 구현 되지 않은 멤버가 있을 수 있습니다. 클래스에 적용 될 때 *추상* 이라는 용어를 사용 하는 것은 다른 .net 언어의 경우와 동일 합니다. 그러나 메서드 (및 속성)에 적용할 때 *추상* 이라는 용어를 사용 하는 것은 다른 .net 언어 F# 에서 사용 하는 것과 약간 다릅니다. 에서 F#메서드가 `abstract` 키워드로 표시 되 면이는 멤버에 *가상 디스패치 슬롯*이라는 항목이 해당 형식에 대 한 가상 함수 내부 테이블에 있음을 나타냅니다. 즉, `virtual` 키워드가 F# 언어로 사용 되지 않지만 메서드는 가상입니다. 키워드 `abstract` 는 메서드가 구현 되었는지 여부에 관계 없이 가상 메서드에 사용 됩니다. 가상 디스패치 슬롯의 선언은 해당 디스패치 슬롯에 대 한 메서드의 정의와 별개입니다. F# 따라서 다른 .net 언어의 가상 메서드 선언 및 정의에 해당 하는 것은 `default` 키워드 또는 `override` 키워드를 사용 하 여 추상 메서드 선언과 개별 정의의 조합입니다. 자세한 내용 및 예제는 [메서드](./members/methods.md)를 참조 하세요.

클래스는 선언 되었지만 정의 되지 않은 추상 메서드가 있는 경우에만 추상으로 간주 됩니다. 따라서 추상 메서드를 포함 하는 클래스는 추상 클래스가 아닐 수도 있습니다. 클래스에 정의 되지 않은 추상 메서드가 없으면 **AbstractClass** 특성을 사용 하지 마십시오.

이전 구문에서 *액세스 가능성 한정자* 는, `public` `private` 또는 `internal`일 수 있습니다. 자세한 내용은 [액세스 제어](access-control.md)를 참조하세요.

다른 형식과 마찬가지로 추상 클래스에는 기본 클래스와 하나 이상의 기본 인터페이스가 있을 수 있습니다. 각 기본 클래스 또는 인터페이스는 `inherit` 키워드와 함께 별도의 줄에 표시 됩니다.

추상 클래스의 형식 정의에는 완전히 정의 된 멤버가 포함 될 수 있지만 추상 멤버가 포함 될 수도 있습니다. 추상 멤버의 구문은 앞의 구문에서 별도로 표시 됩니다. 이 구문에서 멤버의 *형식 시그니처* 는 변환 및 튜플 된 매개 변수에 적절 한 토큰 및/또는 `->` `*` 토큰으로 구분 된 매개 변수 형식 및 반환 형식을 포함 하는 목록입니다. 추상 멤버 형식 시그니처의 구문은 서명 파일에서 사용 되 고 Visual Studio Code 편집기에서 IntelliSense에 의해 표시 되는 구문과 동일 합니다.

다음 코드에서는 두 개의 비추상 파생 클래스인 Square 및 Circle을 포함 하는 추상 클래스 셰이프를 보여 줍니다. 예제에서는 추상 클래스, 메서드 및 속성을 사용 하는 방법을 보여 줍니다. 예제에서 추상 클래스 도형은 구체적 엔터티 원과 사각형의 공통 요소를 나타냅니다. 모든 모양의 일반 기능 (2 차원 좌표계에서)은 Shape 클래스 (표의 위치, 회전 각도 및 영역 및 둘레 속성)로 요약 됩니다. 이를 재정의할 수 있습니다. 단, 위치를 제외 하 고 개별 셰이프를 변경할 수 없는 동작입니다.

순환 클래스에서와 같이 회전 메서드를 재정의할 수 있습니다 .이는 대칭으로 인해 회전 고정입니다. 따라서 Circle 클래스에서 회전 메서드는 아무 작업도 수행 하지 않는 메서드로 대체 됩니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2901.fs)]

**출력:**

```console
Perimeter of square with side length 10.000000 is 40.000000
Circumference of circle with radius 5.000000 is 31.415927
Area of Square: 100.000000
Area of Circle: 78.539816
```

## <a name="see-also"></a>참고자료

- [클래스](classes.md)
- [멤버](./members/index.md)
- [메서드](./members/methods.md)
- [Properties](./members/Properties.md)
