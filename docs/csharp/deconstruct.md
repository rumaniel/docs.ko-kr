---
title: 튜플 및 기타 형식 분해
description: 튜플 및 기타 형식을 분해하는 방법을 알아봅니다.
author: rpetrusha
ms.author: ronpet
ms.date: 07/18/2016
ms.assetid: 0b0c4b0f-4a47-4f66-9b8e-f5c63b195960
ms.openlocfilehash: 5d37f9567570666c280be437aa0472a620a16c63
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68400398"
---
# <a name="deconstructing-tuples-and-other-types"></a>튜플 및 기타 형식 분해

튜플은 메서드 호출에서 여러 값을 검색할 수 있는 간단한 방법을 제공합니다. 하지만 튜플을 검색한 후 튜플의 개별 요소를 처리해야 합니다. 다음 예제와 같이 요소별로 이 작업을 수행하면 번거롭습니다. `QueryCityData` 메서드는 3 튜플을 반환하며 각 튜플 요소가 별도의 작업에서 변수에 할당됩니다.

[!code-csharp[WithoutDeconstruction](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-tuple1.cs)]

개체에서 여러 필드 및 속성 값을 검색하는 작업도 똑같이 번거로울 수 있습니다. 멤버별로 변수에 필드 또는 속성 값을 할당해야 하기 때문입니다.

C# 7.0부터는 한 번의 *분해* 작업으로 튜플에서 여러 요소를 검색하거나 개체에서 여러 필드, 속성 및 계산 값을 검색할 수 있습니다. 튜플을 분해할 때는 튜플 요소를 개별 변수에 할당하고, 개체를 분해할 때는 선택한 값을 개별 변수에 할당합니다.

## <a name="deconstructing-a-tuple"></a>튜플 분해

C#에서는 튜플 분해를 기본적으로 지원하므로 한 작업에서 튜플의 모든 항목을 패키지 해제할 수 있습니다. 튜플을 분해하는 일반 구문은 정의하는 구문과 유사합니다. 즉, 대입문 왼쪽에서 각 요소가 할당되는 변수를 괄호로 묶습니다. 예를 들어 다음 문은 4 튜플의 요소를 네 개의 개별 변수에 할당합니다.

```csharp
var (name, address, city, zip) = contact.GetAddressInfo();
```

다음과 같은 세 가지 방법으로 튜플을 분해합니다.

- 괄호 안에 각 필드의 형식을 명시적으로 선언할 수 있습니다. 다음 예제에서는 이 방법을 사용하여 `QueryCityData` 메서드에서 반환된 3 튜플을 분해합니다.

    [!code-csharp[Deconstruction-Explicit](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-tuple2.cs#1)]

- C#에서 각 변수의 형식을 유추하도록 `var` 키워드를 사용할 수 있습니다. `var` 키워드는 괄호 밖에 놓습니다. 다음 예제에서는 `QueryCityData` 메서드에서 반환된 3 튜플을 분해할 때 형식 유추를 사용합니다.

    [!code-csharp[Deconstruction-Infer](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-tuple3.cs#1)]

    괄호 안에 일부 또는 모든 변수 선언에 `var` 키워드를 개별적으로 사용할 수도 있습니다.

    [!code-csharp[Deconstruction-Infer-Some](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-tuple4.cs#1)]

    이 방법은 번거로우므로 사용하지 않는 것이 좋습니다.

- 마지막으로, 튜플을 이미 선언된 변수로 분해할 수 있습니다.

    [!code-csharp[Deconstruction-Declared](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-tuple5.cs#1)]

튜플에 있는 모든 필드의 형식이 같은 경우에도 괄호 밖에 특정 형식을 지정할 수 없습니다. 이 경우 컴파일러 오류 CS8136, “Deconstruction 'var (...)' 양식에서는 'var'에 특정 형식을 사용할 수 없습니다.”가 생성됩니다.

튜플의 각 요소도 변수에 할당해야 합니다. 생략하는 요소가 있으면 컴파일러에서 CS8132 오류, “‘x’ 요소의 튜플을 ‘y’ 변수로 분해할 수 없습니다.”가 생성됩니다.

분해의 왼쪽에 있는 기존 변수에 할당 및 선언을 혼합할 수 없습니다. 컴파일러가 “분해는 왼쪽에 선언과 식을 혼합할 수 없습니다”라는 오류 CS8184를 생성합니다. 구성원이 새로 선언된 변수 및 기존 변수를 포함할 경우.

## <a name="deconstructing-tuple-elements-with-discards"></a>무시 항목을 사용한 튜플 요소 분해

튜플을 분해할 때 일부 요소 값에만 관심이 있는 경우가 종종 있습니다. C# 7.0부터는 C#에서 지원하는 *무시 항목* 즉, 무시하도록 선택한 값을 갖는 쓰기 전용 변수를 활용할 수 있습니다. 무시 항목은 할당에서 밑줄 문자(“\_”)로 지정됩니다. 원하는 수의 값을 모두 하나의 무시 항목 `_`로 표시하여 무시할 수 있습니다.

다음 예제에서는 무시 항목과 함께 튜플을 사용하는 방법을 보여 줍니다. `QueryCityDataForYears` 메서드는 도시의 이름, 도시의 면적, 연도, 해당 연도의 도시 인구, 두 번째 연도, 해당 두 번째 연도의 도구 인구를 포함하는 6 튜플을 반환합니다. 이 예제는 이러한 두 연도 사이의 인구 변화를 보여 줍니다. 튜플에서 사용 가능한 데이터 중 도시 면적에는 관심이 없고 디자인 타임에 도시 이름과 두 날짜를 알고 있습니다. 따라서 튜플에 저장된 두 가지 인구 값에만 관심이 있고 나머지 값은 무시 항목으로 처리할 수 있습니다.  

[!code-csharp[Tuple-discard](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

## <a name="deconstructing-user-defined-types"></a>사용자 정의 형식 분해

C#은 튜플이 아닌 형식의 분해에 대해 기본 제공 지원을 제공하지 않습니다. 그러나 클래스, 구조체 또는 인터페이스의 만든 이는 하나 이상의 `Deconstruct` 메서드를 구현하여 형식의 인스턴스를 분해하도록 허용할 수 있습니다. 이 메서드는 void를 반환하며 분해할 각 값은 메서드 시그니처에서 [out](language-reference/keywords/out-parameter-modifier.md) 매개 변수로 표시됩니다. 예를 들어 다음 `Person` 클래스의 `Deconstruct` 메서드는 이름, 중간 이름 및 성을 반환합니다.

[!code-csharp[Class-deconstruct](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-class1.cs#1)]

그러면 다음과 같은 할당을 사용하여 `p`라는 `Person` 클래스의 인스턴스를 분해할 수 있습니다.

[!code-csharp[Class-deconstruct](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-class1.cs#2)]

다음 예제에서는 `Deconstruct` 메서드를 오버로드하여 `Person` 개체의 속성을 다양한 조합으로 반환합니다. 개별 오버로드는 다음을 반환합니다.

- 이름 및 성
- 이름, 성 및 중간 이름
- 이름, 성, 도시 이름 및 주 이름

[!code-csharp[Class-deconstruct](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-class2.cs)]

`Deconstruct` 메서드를 오버로드하여 개체에서 일반적으로 추출되는 데이터 그룹을 반영하려면 먼저 고유하고 명확한 시그니처를 사용하여 `Deconstruct` 메서드를 신중하게 정의해야 합니다. 여러 `Deconstruct` 메서드의 `out` 매개 변수 수가 동일하거나 `out` 매개 변수 수와 형식은 동일하지만 순서가 다른 경우 혼동이 생길 수 있습니다.

다음 예제의 오버로드된 `Deconstruct` 메서드에서는 가능한 혼동 원인 중 하나를 보여 줍니다. 첫 번째 오버로드는 `Person` 개체의 이름, 중간 이름, 성 및 나이를 해당 순서로 반환합니다. 두 번째 오버로드는 연간 소득과 함께 이름 정보만 반환하지만 이름, 중간 이름 및 성의 순서가 다릅니다. 따라서 `Person` 인스턴스를 분해할 때 인수 순서를 혼동하기 쉽습니다.

[!code-csharp[Deconstruct-ambiguity](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-ambiguous.cs)]

## <a name="deconstructing-a-user-defined-type-with-discards"></a>무시 항목을 사용한 사용자 정의 형식 분해

[튜플](#deconstructing-tuple-elements-with-discards)에서와 마찬가지로 무시 항목을 사용하여 `Deconstruct` 메서드에서 반환된 항목 중 선택한 항목을 무시할 수 있습니다. 각 무시 항목은 “\_”이라는 변수로 정의하며 단일 분해 작업에 여러 무시 항목을 포함할 수 있습니다.

다음 예제에서는 `Person` 개체를 4개의 문자열(이름, 성, 도시 및 주)로 분해하지만 성과 주는 무시합니다.

[!code-csharp[Class-discard](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/class-discard1.cs#1)]

## <a name="deconstructing-a-user-defined-type-with-an-extension-method"></a>확장 메서드를 사용한 사용자 정의 형식 분해

클래스, 구조체 또는 인터페이스의 만든 이가 아니더라도 하나 이상의 `Deconstruct` [확장 메서드](programming-guide/classes-and-structs/extension-methods.md) 구현을 통해 해당 형식의 개체를 분해하여 관심 있는 값을 반환할 수 있습니다.

다음 예제에서는 <xref:System.Reflection.PropertyInfo?displayProperty=nameWithType> 클래스에 대한 두 개의 `Deconstruct` 확장 메서드를 정의합니다. 첫 번째 메서드는 속성의 형식, 정적 속성인지 인스턴스 속성인지 여부, 읽기 전용인지 여부, 인덱싱되었는지 여부 등 속성의 특성을 나타내는 값 집합을 반환합니다. 두 번째 메서드는 속성의 접근성을 나타냅니다. get 및 set 접근자의 접근성이 다를 수 있으므로 부울 값은 속성에 별도의 get 및 set 접근자가 있는지 여부와 있는 경우 접근성이 동일한지 여부를 나타냅니다. 접근자가 하나만 있거나 get 및 set 접근자 모두 접근성이 동일한 경우 `access` 변수는 속성 전체의 접근성을 나타냅니다. 그러지 않으면 get 및 set 접근자의 접근성이 `getAccess` 및 `setAccess` 변수로 표시됩니다.

[!code-csharp[Extension-deconstruct](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/deconstruct-extension1.cs)]

## <a name="see-also"></a>참고 항목

- [삭제](discards.md)
- [튜플](tuples.md)
