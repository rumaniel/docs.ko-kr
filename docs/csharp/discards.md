---
title: 무시 항목 - C# 가이드
description: 할당되지 않은 무시 가능한 변수인 무시 항목에 대한 C#의 지원과 무시 항목을 사용할 수 있는 방법에 관해 설명합니다.
author: rpetrusha
ms.author: ronpet
ms.date: 07/21/2017
ms.openlocfilehash: 761fb69d3bc774975caf63b8aa665f8c19c0430a
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53143607"
---
# <a name="discards---c-guide"></a>무시 항목 - C# 가이드

C# 7.0부터 C#에서는 애플리케이션 코드에서 의도적으로 사용되지 않는 임시 더미 변수인 무시 항목을 지원합니다. 무시 항목은 할당되지 않은 변수에 해당하므로 값을 가지지 않습니다. 무시 항목 변수는 하나만 있고 할당된 스토리지가 아닐 수도 있으므로 무시 항목은 메모리 할당을 줄일 수 있습니다. 코드의 의도를 명확하게 만들므로 코드의 가독성과 유지 관리 편의성을 향상합니다.

변수가 무시 항목임을 지정하려면 변수에 밑줄(`_`)을 이름으로 할당합니다. 예를 들어 다음 메서드 호출은 첫 번째 및 두 번째 값이 무시 항목이고 *영역*이 *GetCityInformation*에서 반환한 해당 세 번째 구성 요소로 설정된 이전에 선언된 변수인 3-튜플을 반환합니다.

```csharp
(_, _, area) = city.GetCityInformation(cityName);
```

C# 7.0에서 무시 항목은 다음 컨텍스트의 할당에서 지원됩니다.

- 튜플 및 개체 [분해](deconstruct.md)
- [is](language-reference/keywords/is.md) 및 [switch](language-reference/keywords/switch.md)를 사용한 패턴 일치
- `out` 매개 변수를 사용한 메서드 호출
- 범위에 `_`이 없는 경우 독립 실행형 `_`

`_`이 유효한 무시 항목인 경우, 해당 값을 검색하거나 할당 작업에서 사용하려고 하면 “‘\_’ 이름이 현재 컨텍스트에 없습니다.”라는 컴파일러 오류 CS0301이 생성됩니다. 이는 `_`에 값이 할당되어 있지 않고 스토리지 위치도 할당되어 있지 않을 수 있기 때문입니다. 실제 변수인 경우에는 이전 예제에서처럼 2개 이상의 값을 무시할 수 없습니다.

## <a name="tuple-and-object-deconstruction"></a>튜플 및 개체 분해

무시 항목은 튜플을 작업할 때 애플리케이션 코드에 튜플 요소 중 일부만 사용하고 일부는 무시하는 경우 특히 유용합니다. 예를 들어, 다음 `QueryCityDataForYears` 메서드는 도시의 이름, 도시의 면적, 연도, 해당 연도의 도시 인구, 두 번째 연도, 해당 두 번째 연도의 도구 인구를 포함하는 6 튜플을 반환합니다. 이 예제는 이러한 두 연도 사이의 인구 변화를 보여 줍니다. 튜플에서 사용 가능한 데이터 중 도시 면적에는 관심이 없고 디자인 타임에 도시 이름과 두 날짜를 알고 있습니다. 따라서 튜플에 저장된 두 가지 인구 값에만 관심이 있고 나머지 값은 무시 항목으로 처리할 수 있습니다.  

[!code-csharp[Tuple-discard](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

무시 항목을 사용한 튜플 분해에 대한 자세한 내용은 [튜플 및 기타 형식 분해](deconstruct.md#deconstructing-tuple-elements-with-discards)를 참조하세요.

클래스, 구조체 또는 인터페이스의 `Deconstruct` 메서드로도 개체에서 특정 데이터 집합을 검색 및 분해할 수 있습니다. 분해된 값의 하위 집합만으로 작업하려는 경우 무시 항목을 사용할 수 있습니다. 다음 예제에서는 `Person` 개체를 4개의 문자열(이름, 성, 도시 및 주)로 분해하지만 성과 주는 무시합니다.

[!code-csharp[Class-discard](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/class-discard1.cs)]

무시 항목을 사용한 사용자 정의 형식 분해에 대한 자세한 내용은 [튜플 및 기타 형식 분해](deconstruct.md#deconstructing-a-user-defined-type-with-discards)를 참조하세요.

## <a name="pattern-matching-with-switch-and-is"></a>`switch` 및 `is`를 사용한 패턴 일치

*무시 패턴*은 [is](language-reference/keywords/is.md) 및 [switch](language-reference/keywords/switch.md) 키워드를 사용한 패턴 일치에서 사용할 수 있습니다. 모든 식은 무시 패턴과 항상 일치됩니다.

다음 예제에서는 [is](language-reference/keywords/is.md) 문을 사용하여 개체가 <xref:System.IFormatProvider> 구현을 제공하고 개체가 `null`인지 테스트하는지를 결정하는 `ProvidesFormatInfo` 메서드를 정의합니다. 또한 무시 패턴을 사용하여 다른 형식의 null이 아닌 개체도 처리합니다.

[!code-csharp[discard-pattern](../../samples/snippets/csharp/programming-guide/discards/discard-pattern2.cs)]

## <a name="calls-to-methods-with-out-parameters"></a>out 매개 변수를 사용한 메서드 호출

`Deconstruct` 메서드를 호출하여 사용자 정의 형식(클래스, 구조체 또는 인터페이스의 인스턴스)를 분해할 때 개별 `out` 인수의 값을 무시할 수 있습니다. 하지만 어느 메서드든 out 매개 변수를 사용하여 호출할 때 `out` 인수의 값을 무시할 수도 있습니다.

다음 예제에서는 [DateTime.TryParse(String, out DateTime)](<xref:System.DateTime.TryParse(System.String,System.DateTime@)>) 메서드를 호출하여 날짜의 문자열 표현이 현재 문화권에 유효한지 확인합니다. 이 예제에서는 날짜 문자열의 유효성 검사에만 관심이 있고 이 문자열의 구문 검사를 통한 날짜 추출에는 관심이 없으므로 메서드의 `out` 인수는 무시 항목입니다.

[!code-csharp[discard-with-out](../../samples/snippets/csharp/programming-guide/discards/discard-out1.cs)]

## <a name="a-standalone-discard"></a>독립 실행형 무시 항목

독립 실행형 무시 항목을 사용하여 무시할 변수를 지정할 수 있습니다. 다음 예제에서는 독립 실행형 무시 항목을 사용하여 비동기 작업에서 반환되는 <xref:System.Threading.Tasks.Task>개체를 무시합니다. 따라서 작업이 완료되려고 할 때 throw되는 예외가 표시되지 않습니다.

[!code-csharp[standalone-discard](../../samples/snippets/csharp/programming-guide/discards/standalone-discard1.cs)]

`_`은 유효한 식별자이기도 합니다. 지원되는 컨텍스트 외부에서 사용하면 `_`은 무시 항목이 아니라 유효한 변수로 처리됩니다. `_`이라는 식별자가 이미 범위 내에 있는 경우 `_`을 독립 실행형 무시 항목으로 사용하면 다음과 같은 결과가 발생할 수 있습니다.

- 범위 내 `_` 변수 값을 실수로 수정하여 의도한 무시 항목의 값 할당. 예:

   [!code-csharp[standalone-discard](../../samples/snippets/csharp/programming-guide/discards/standalone-discard2.cs#1)]

- 형식 안전성 위반으로 인한 컴파일러 오류. 예:

   [!code-csharp[standalone-discard](../../samples/snippets/csharp/programming-guide/discards/standalone-discard2.cs#2)]

- 컴파일러 오류 CS0136, “이름이 ‘\_’인 지역 또는 매개 변수는 이 범위에서 선언될 수 없습니다. 해당 이름이 지역 또는 매개 변수를 정의하기 위해 바깥쪽 지역 범위에서 사용되었습니다.” 예:

   [!code-csharp[standalone-discard](../../samples/snippets/csharp/programming-guide/discards/standalone-discard2.cs#3)]

## <a name="see-also"></a>참고 항목

- [튜플 및 기타 형식 분해](deconstruct.md)
- [`is` 키워드](language-reference/keywords/is.md)
- [`switch` 키워드](language-reference/keywords/switch.md)
