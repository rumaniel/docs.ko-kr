---
title: 속성
description: 유효성 검사, 계산된 값, 지연 평가, 속성 변경 알림 기능을 포함하는 C# 속성에 대해 알아봅니다.
ms.date: 04/25/2018
ms.openlocfilehash: 6638ae74516d7546882c8a380eed9b03ff3d18e9
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69587414"
---
# <a name="properties"></a>속성

속성은 C#의 주요 구성 요소입니다. 언어는 개발자가 디자인 의도를 정확하게 표현하는 코드를 작성할 수 있는 구문을 정의합니다.

속성은 액세스 시 필드처럼 동작합니다.
그러나 필드와 달리 속성은 속성에 액세스하거나 할당할 때 실행되는 문을 정의하는 접근자로 구현됩니다.

## <a name="property-syntax"></a>속성 구문

속성 구문은 필드에 대한 자연 확장입니다. 필드는 스토리지 위치를 정의합니다.

[!code-csharp[Person class with public fields](../../samples/snippets/csharp/properties/Person.cs#1)]

속성 정의에는 해당 속성의 값을 검색하고 할당하는 `get` 및 `set` 접근자에 대한 선언이 포함됩니다.

[!code-csharp[Person class with public properties](../../samples/snippets/csharp/properties/Person.cs#2)]

위에 표시된 구문은 *자동 속성* 구문입니다. 컴파일러는 속성을 백업하는 필드의 스토리지 위치를 생성합니다. 또한 컴파일러는 `get` 및 `set` 접근자의 본문을 구현합니다.

때로는 해당 형식의 기본값이 아닌 값으로 속성을 초기화해야 합니다.  이 작업을 위해 C#에서는 닫는 중괄호 뒤에 속성의 값을 설정합니다. `FirstName` 속성의 초기 값을 `null` 대신 빈 문자열로 설정할 수도 있습니다. 아래와 같이 지정하면 됩니다.

[!code-csharp[Person class with properties and initializer](../../samples/snippets/csharp/properties/Person.cs#3)]

이 아티클의 뒷부분에서 살펴보겠지만 특정 초기화는 읽기 전용 속성에 가장 유용합니다.

아래 표시된 대로 스토리지를 직접 정의할 수도 있습니다.

[!code-csharp[Person class with properties and backing field](../../samples/snippets/csharp/properties/Person.cs#4)]

속성 구현이 단일 식인 경우 getter 또는 setter에 대해 *식 본문 멤버*를 사용할 수 있습니다.

[!code-csharp[Person class with properties and expression bodied getters and setters](../../samples/snippets/csharp/properties/Person.cs#5)]

이 아티클 전체에서 해당하는 경우 이 간소화된 구문이 사용됩니다.

위에 표시된 속성 정의는 읽기/쓰기 속성입니다. set 접근자에서 `value` 키워드를 확인합니다. `set` 접근자에는 항상 `value`라는 단일 매개 변수가 있습니다. `get` 접근자는 속성 형식(이 예제에서는 `string`)으로 변환할 수 있는 값을 반환해야 합니다.

이것이 기본 구문입니다. 다양한 디자인 구문을 지원하는 여러 가지 변환이 있습니다. 각 변환에 대한 구문 옵션을 살펴보고 알아봅니다.

## <a name="scenarios"></a>시나리오

위의 예제에서는 가장 간단한 속성 정의 사례 중 하나인 유효성 검사 없는 읽기/쓰기 속성을 보여 주었습니다. `get` 및 `set` 접근자에서 원하는 코드를 작성하여 다양한 시나리오를 만들 수 있습니다.

### <a name="validation"></a>유효성 검사

`set` 접근자에서 코드를 작성하여 속성으로 표현된 값이 항상 유효한지 확인합니다. 예를 들어 이름을 비워 두거나 공백일 수 없다는 `Person` 클래스에 대한 규칙이 있다고 가정합니다. 다음과 같이 작성할 수 있습니다.

[!code-csharp[Validating property setters](../../samples/snippets/csharp/properties/Person.cs#6)]

속성 setter 유효성 검사의 일부인 `throw` 식을 사용하여 앞의 예제를 간소화할 수 있습니다.

[!code-csharp[Validating property setters](../../samples/snippets/csharp/properties/Person.cs#7)]

위의 예제에서는 첫 번째 이름을 비워 두거나 공백일 수 없다는 규칙을 적용합니다. 개발자가 작성하는 경우

```csharp
hero.FirstName = "";
```

해당 할당으로 인해 `ArgumentException`이 throw됩니다. 속성 set 접근자의 반환 형식이 void여야 하므로 예외를 throw하여 set 접근자에서 오류를 보고합니다.

이 동일한 구문을 시나리오에서 필요한 항목으로 확장할 수 있습니다. 서로 다른 속성 간의 관계를 확인하거나 모든 외부 조건에 대해 유효성을 검사할 수 있습니다. 유효한 모든 C# 문을 속성 접근자에서 사용할 수 있습니다.

### <a name="read-only"></a>읽기 전용

이 시점까지 살펴본 모든 속성 정의는 공용 접근자를 사용한 읽기/쓰기 속성입니다. 속성에 유효한 유일한 액세스 가능성은 아닙니다.
읽기 전용 속성을 만들거나 set 및 get 접근자에 대해 다른 액세스 가능성을 제공할 수 있습니다. `Person` 클래스가 해당 클래스의 다른 메서드에서만 `FirstName` 속성의 값을 변경할 수 있도록 한다고 가정합니다. set 접근자에 `public` 대신 `private` 액세스 가능성을 제공할 수 있습니다.

[!code-csharp[Using a private setter for a publicly readonly property](../../samples/snippets/csharp/properties/Person.cs#8)]

이제 `FirstName` 속성을 모든 코드에서 액세스할 수 있지만 `Person` 클래스의 다른 코드에서만 할당할 수 있습니다.

set 또는 get 접근자에 제한적인 액세스 한정자를 추가할 수 있습니다. 개별 접근자에 설정하는 액세스 한정자는 속성 정의의 액세스 한정자보다 더 제한적이어야 합니다. 위 내용은 `FirstName` 속성이 `public`이지만 set 접근자가 `private`이므로 유효합니다. `public` 접근자를 사용하여 `private` 속성을 선언할 수 없습니다. 속성 선언을 `protected`, `internal`, `protected internal` 또는 `private`로 선언할 수도 있습니다.

`get` 접근자에 더 제한적인 한정자를 설정하는 것도 가능합니다. 예를 들어 `public` 속성이 있지만 `get` 접근자를 `private`로 제한할 수 있습니다. 이 시나리오는 실제로 거의 수행되지 않습니다.

생성자 또는 속성 이니셜라이저에서만 설정할 수 있도록 속성 수정을 제한할 수도 있습니다. 다음과 같이 `Person` 클래스를 수정할 수 있습니다.

[!code-csharp[A readonly auto implemented property](../../samples/snippets/csharp/properties/Person.cs#9)]

이 기능은 읽기 전용 속성으로 노출되는 컬렉션을 초기화하는 데 주로 사용됩니다.

```csharp
public class Measurements
{
    public ICollection<DataPoint> points { get; } = new List<DataPoint>();
}
```

### <a name="computed-properties"></a>계산된 속성

속성은 멤버 필드의 값을 반환할 필요가 없습니다. 계산된 값을 반환하는 속성을 만들 수 있습니다. `Person` 개체를 확장하여 이름과 성을 연결해서 계산된 전체 이름을 반환하겠습니다.

[!code-csharp[A computed property](../../samples/snippets/csharp/properties/Person.cs#10)]

위 예에서는 [문자열 보간](./language-reference/tokens/interpolated.md) 기능을 사용하여 전체 이름에 대한 서식이 지정된 문자열을 만듭니다.

계산된 `FullName` 속성을 만드는 보다 간결한 방법을 제공하는 *식 본문 멤버*를 사용할 수도 있습니다.

[!code-csharp[A computed property using an expression bodied member](../../samples/snippets/csharp/properties/Person.cs#11)]

*식 본문 멤버*는 *람다 식* 구문을 사용하여 단일 식이 포함된 메서드를 정의합니다. 여기서 해당 식은 person 개체의 전체 이름을 반환합니다.

### <a name="cached-evaluated-properties"></a>캐시된 평가 속성

계산된 속성의 개념과 스토리지를 혼합하고 *캐시된 평가 속성*을 만들 수 있습니다.  예를 들어 처음 액세스할 때만 문자열 형식이 지정되도록 `FullName` 속성을 업데이트할 수 있습니다.

[!code-csharp[Caching the value of a computed property](../../samples/snippets/csharp/properties/Person.cs#12)]

하지만 위의 코드에는 버그가 포함되어 있습니다. 코드가 `FirstName` 또는 `LastName` 속성의 값을 업데이트하는 경우 이전에 평가한 `fullName` 필드는 유효하지 않습니다. `fullName` 필드가 다시 평가되도록 `FirstName` 및 `LastName` 속성의 `set` 접근자를 수정합니다.

[!code-csharp[Invalidating the cache correctly](../../samples/snippets/csharp/properties/Person.cs#13)]

이 최종 버전은 필요한 경우에만 `FullName` 속성을 평가합니다.
이전에 계산한 버전이 유효한 경우 해당 버전이 사용됩니다. 다른 상태 변경으로 인해 이전에 계산한 버전이 무효화된 경우 다시 계산됩니다. 이 클래스를 사용하는 개발자는 구현 세부 정보를 알 필요가 없습니다. 이러한 내부 변경 내용은 Person 개체의 사용에 영향을 주지 않습니다. 이것이 속성을 사용하여 개체의 데이터 멤버를 노출하는 주요 이유입니다.

### <a name="attaching-attributes-to-auto-implemented-properties"></a>자동 구현 속성에 특성 연결

C# 7.3부터 필드 특성은 자동 구현된 속성의 컴파일러에서 생성된 지원 필드에 연결될 수 있습니다. 예를 들어 고유한 정수 `Id` 속성을 추가하는 `Person` 클래스에 대한 수정 버전을 사용합니다.
자동 구현 속성을 사용하여 `Id` 속성을 작성하지만 디자인은 `Id` 속성을 유지하기 위해 호출하지 않습니다. <xref:System.NonSerializedAttribute>는 속성이 아니라 필드에만 연결할 수 있습니다. 다음 예제와 같이 특성에 `field:` 지정자를 사용하여 `Id` 속성의 지원 필드에 <xref:System.NonSerializedAttribute>를 연결할 수 있습니다.

[!code-csharp[Attaching attributes to a backing field](../../samples/snippets/csharp/properties/Person.cs#14)]

이 기술은 자동 구현 속성의 지원 필드에 연결하는 모든 특성에서 작동합니다.

### <a name="implementing-inotifypropertychanged"></a>INotifyPropertyChanged 구현

속성 접근자에서 코드를 작성해야 하는 최종 시나리오는 값이 변경되었다고 데이터 바인딩 클라이언트에 알리는 데 사용되는 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 지원하는 것입니다. 속성의 값이 변경되면 개체가 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged?displayProperty=nameWithType> 이벤트를 발생시켜 변경되었음을 나타냅니다. 데이터 바인딩 라이브러리가 해당 변경 내용에 따라 차례로 표시 요소를 업데이트합니다. 아래 코드는 이 person 클래스의 `FirstName` 속성에 대해 `INotifyPropertyChanged`를 구현하는 방법을 보여 줍니다.

[!code-csharp[invalidating the cache correctly](../../samples/snippets/csharp/properties/Person.cs#15)]

`?.` 연산자를 *null 조건부 연산자*라고 합니다. 연산자의 오른쪽을 평가하기 전에 null 참조를 확인합니다. 최종 결과로, `PropertyChanged` 이벤트에 대한 구독자가 없는 경우 이벤트를 발생시키는 코드가 실행되지 않습니다. 해당 경우 이 확인을 수행하지 않으면 `NullReferenceException`이 throw됩니다. 자세한 내용은 [`events`](events-overview.md)를 참조하세요. 또한 이 예제에서는 새 `nameof` 연산자를 사용하여 속성 이름 기호에서 해당 텍스트 표현으로 변환합니다.
`nameof`를 사용하면 속성 이름을 잘못 입력하는 오류를 줄일 수 있습니다.

<xref:System.ComponentModel.INotifyPropertyChanged>를 구현하는 작업은 필요한 시나리오를 지원하기 위해 접근자의 코드를 작성할 수 있는 경우의 예제입니다.

## <a name="summing-up"></a>요약

속성은 클래스 또는 개체에 있는 스마트 필드의 한 형태입니다. 개체 외부에서는 개체의 필드와 유사하게 나타납니다. 그러나 C# 기능의 전체 팔레트를 사용하여 속성을 구현할 수 있습니다.
유효성 검사, 다른 액세스 가능성, 지연 평가 또는 시나리오에 필요한 모든 요구 사항을 제공할 수 있습니다.
