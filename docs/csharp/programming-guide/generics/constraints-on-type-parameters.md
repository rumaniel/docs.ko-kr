---
title: 형식 매개 변수에 대한 제약 조건 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 04/12/2018
helpviewer_keywords:
- generics [C#], type constraints
- type constraints [C#]
- type parameters [C#], constraints
- unbound type parameter [C#]
ms.openlocfilehash: 5c36639d76a6fbd4e36f39486369a55a56a6e3ea
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396285"
---
# <a name="constraints-on-type-parameters-c-programming-guide"></a>형식 매개 변수에 대한 제약 조건(C# 프로그래밍 가이드)

제약 조건은 형식 인수에서 갖추고 있어야 하는 기능을 컴파일러에 알립니다. 제약 조건이 없으면 형식 인수가 어떤 형식이든 될 수 있습니다. 컴파일러는 모든 .NET 형식의 궁극적인 기본 클래스인 <xref:System.Object?displayProperty=nameWithType>의 멤버만 가정할 수 있습니다. 자세한 내용은 [제약 조건을 사용하는 이유](#why-use-constraints)를 참조하세요. 클라이언트 코드에서 제약 조건에 의해 허용되지 않는 형식을 사용하여 클래스를 인스턴스화하려고 하면 컴파일 시간 오류가 발생합니다. 제약 조건은 `where` 상황별 키워드를 사용하여 지정됩니다. 다음 표에는 7가지 형식의 제약 조건이 나와 있습니다.

|제약 조건|설명|
|----------------|-----------------|
|`where T : struct`|형식 인수는 값 형식이어야 합니다. <xref:System.Nullable%601>를 제외한 임의의 값 형식을 지정할 수 있습니다. nullable 값 형식에 대한 자세한 내용은 [Nullable 값 형식](../nullable-types/index.md)을 참조하세요.|
|`where T : class`|형식 인수는 참조 형식이어야 합니다. 이 제약 조건은 모든 클래스, 인터페이스, 대리자 또는 배열 형식에도 적용됩니다.|
|`where T : notnull`|형식 인수는 nullable이 아닌 형식이어야 합니다. 인수는 C# 8.0 이상의 nullable이 아닌 참조 형식이거나 nullable이 아닌 값 형식일 수 있습니다. 이 제약 조건은 모든 클래스, 인터페이스, 대리자 또는 배열 형식에도 적용됩니다.|
|`where T : unmanaged`|형식 인수는 [비관리형 형식](../../language-reference/builtin-types/unmanaged-types.md)이어야 합니다.|
|`where T : new()`|형식 인수에 매개 변수가 없는 public 생성자가 있어야 합니다. 다른 제약 조건과 함께 사용할 경우 `new()` 제약 조건을 마지막에 지정해야 합니다.|
|`where T :` *\<기본 클래스 이름>*|형식 인수가 지정된 기본 클래스이거나 지정된 기본 클래스에서 파생되어야 합니다.|
|`where T :` *\<인터페이스 이름>*|형식 인수가 지정된 인터페이스이거나 지정된 인터페이스를 구현해야 합니다. 여러 인터페이스 제약 조건을 지정할 수 있습니다. 제약 인터페이스가 제네릭일 수도 있습니다.|
|`where T : U`|T에 대해 제공되는 형식 인수는 U에 대해 제공되는 인수이거나 이 인수에서 파생되어야 합니다.|

일부 제약 조건은 상호 배타적입니다. 모든 값 형식에는 매개 변수가 없는 액세스 가능 생성자가 있어야 합니다. `struct` 제약 조건은 `new()` 제약 조건을 의미하고, `new()` 제약 조건은 `struct` 제약 조건과 결합할 수 없습니다. `unmanaged` 제약 조건은 `struct` 제약 조건을 의미합니다. `unmanaged` 제약 조건은 `struct` 또는 `new()` 제약 조건과 결합할 수 없습니다.

## <a name="why-use-constraints"></a>제약 조건을 사용하는 이유

형식 매개 변수 제약을 통해 허용되는 작업 및 메서드 호출 수를 제약 형식 및 해당 상속 계층 구조의 모든 형식에서 지원하는 작업 및 메서드 호출로 늘립니다. 제네릭 클래스 또는 메서드를 디자인할 때 제네릭 멤버에서 단순 할당 이외의 작업을 대해 수행하거나 <xref:System.Object?displayProperty=nameWithType>에서 지원하지 않는 메서드를 호출하는 경우 형식 매개 변수에 제약 조건을 적용해야 합니다. 예를 들어 기본 클래스 제약 조건은 이 형식의 개체나 이 형식에서 파생된 개체만 형식 인수로 사용된다고 컴파일러에 알립니다. 컴파일러에 이 보장이 있으면 해당 형식의 메서드가 제네릭 클래스에서 호출되도록 허용할 수 있습니다. 다음 코드 예제에서는 기본 클래스 제약 조건을 적용하여 `GenericList<T>` 클래스([제네릭 소개](introduction-to-generics.md)에 있음)에 추가할 수 있는 기능을 보여 줍니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#9)]

이 제약 조건을 통해 제네릭 클래스에서 `Employee.Name` 속성을 사용할 수 있습니다. 제약 조건은 `T` 형식의 모든 항목을 `Employee` 개체 또는 `Employee`에서 상속하는 개체 중 하나로 보장하도록 지정합니다.

동일한 형식 매개 변수에 여러 개의 제약 조건을 적용할 수 있으며, 제약 조건 자체가 다음과 같이 제네릭 형식일 수 있습니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#10)]

`where T : class` 제약 조건을 적용하는 경우 `==` 및 `!=` 연산자는 참조 ID만 테스트하고 값이 같은지 테스트하지 않으므로 형식 매개 변수에 사용하지 않도록 합니다. 이러한 연산자가 인수로 사용되는 형식에서 오버로드되는 경우에도 이 동작이 발생합니다. 다음 코드는 이 내용을 보여 줍니다. <xref:System.String> 클래스가 `==` 연산자를 오버로드하지만 출력이 false입니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#11)]

컴파일러에서 컴파일 시간에 `T`가 참조 형식이고 모든 참조 형식에 유효한 기본 연산자를 사용해야 한다는 것만 인식합니다. 값 일치 여부를 테스트해야 하는 경우에도 `where T : IEquatable<T>` 또는 `where T : IComparable<T>` 제약 조건을 적용하고 제네릭 클래스를 생성하는 데 사용할 모든 클래스에서 인터페이스를 구현하는 것이 좋습니다.

## <a name="constraining-multiple-parameters"></a>여러 매개 변수 제한

다음 예제와 같이 여러 매개 변수에 제약 조건을 적용하고, 단일 매개 변수에 여러 제약 조건을 적용할 수 있습니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#12)]

## <a name="unbounded-type-parameters"></a>바인딩되지 않은 형식 매개 변수

 공용 클래스 `SampleClass<T>{}`의 T와 같이 제약 조건이 없는 형식 매개 변수를 바인딩되지 않은 형식 매개 변수라고 합니다. 바인딩되지 않은 형식 매개 변수에는 다음 규칙이 있습니다.

- `!=` 및 `==` 연산자는 구체적인 형식 인수가 이러한 연산자를 지원한다는 보장이 없기 때문에 사용할 수 없습니다.
- `System.Object`로/에서 변환하거나 임의의 인터페이스 형식으로 명시적으로 변환할 수 있습니다.
- [null](../../language-reference/keywords/null.md)과 비교할 수 있습니다. 바인딩되지 않은 매개 변수를 `null`과 비교하는 경우 형식 인수가 값 형식이면 비교에서 항상 false를 반환합니다.

## <a name="type-parameters-as-constraints"></a>제약 조건으로 형식 매개 변수 사용

다음 예제와 같이 고유한 형식 매개 변수가 있는 멤버 함수가 해당 매개 변수를 포함 형식의 형식 매개 변수로 제약해야 하는 경우 제네릭 형식 매개 변수를 제약 조건으로 사용하면 유용합니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#13)]

앞의 예제에서 `T`는 `Add` 메서드 컨텍스트에서는 형식 제약 조건이고, `List` 클래스 컨텍스트에서는 바인딩되지 않은 형식 매개 변수입니다.

제네릭 클래스 정의에서 형식 매개 변수를 제약 조건으로 사용할 수도 있습니다. 형식 매개 변수는 다른 형식 매개 변수와 함께 꺾쇠괄호 안에 선언해야 합니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#14)]

컴파일러에서 형식 매개 변수가 `System.Object`에서 파생된다는 점을 제외하고는 형식 매개 변수에 대해 아무 것도 가정할 수 없기 때문에, 제네릭 클래스에서 형식 매개 변수를 제약 조건으로 사용하는 경우는 제한됩니다. 두 형식 매개 변수 사이의 상속 관계를 적용하려는 시나리오에서 제네릭 클래스에 형식 매개 변수를 제약 조건으로 사용합니다.

## <a name="notnull-constraint"></a>NotNull 제약 조건

C# 8.0부터는 `notnull` 제약 조건을 사용하여 형식 인수가 nullable이 아닌 값 형식 또는 nullable이 아닌 참조 형식이어야 함을 지정할 수 있습니다. `notnull` 제약 조건은 `nullable enable` 컨텍스트에서만 사용할 수 있습니다. nullable 형식을 감지하지 않는 컨텍스트에서 `notnull` 제약 조건을 추가하는 경우 컴파일러가 경고를 생성합니다. 

다른 제약 조건과 달리 형식 인수가 `notnull` 제약 조건을 위반하면 컴파일러는 해당 코드가 `nullable enable` 컨텍스트에서 컴파일될 때 경고를 생성합니다. 코드가 nullable 형식을 감지하지 않는 컨텍스트에서 컴파일된 경우에는 컴파일러가 경고나 오류를 생성하지 않습니다.

## <a name="unmanaged-constraint"></a>관리되지 않는 제약 조건

C# 7.3부터 `unmanaged` 제약 조건을 사용하여 형식 매개 변수가 [관리되지 않는 형식](../../language-reference/builtin-types/unmanaged-types.md)이어야 한다고 지정할 수 있습니다. `unmanaged` 제약 조건을 사용하면 다음 예제와 같이 메모리 블록으로 조작할 수 있는 형식을 사용하도록 재사용 가능한 루틴을 작성할 수 있습니다.

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#15)]

앞의 메서드는 기본 제공 형식으로 알려지지 않은 형식에서 `sizeof` 연산자를 사용하므로 `unsafe` 컨텍스트에서 컴파일해야 합니다. `unmanaged` 제약 조건이 없으면 `sizeof` 연산자를 사용할 수 없습니다.

## <a name="delegate-constraints"></a>대리자 제약 조건

C# 7.3부터 <xref:System.Delegate?displayProperty=nameWithType> 또는 <xref:System.MulticastDelegate?displayProperty=nameWithType>를 기본 클래스 제약 조건으로 사용할 수도 있습니다. CLR에서는 항상 이 제약 조건을 허용했지만, C# 언어에서는 이 제약 조건을 허용하지 않았습니다. `System.Delegate` 제약 조건을 사용하면 형식이 안전한 방식으로 대리자에서 작동하는 코드를 작성할 수 있습니다. 다음 코드는 두 대리자가 동일한 형식인 경우 이를 결합하는 확장 메서드를 정의합니다.

[!code-csharp[using the delegate constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#16)]

위의 메서드를 사용하여 동일한 형식의 대리자를 결합할 수 있습니다.

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#17)]

마지막 줄의 주석 처리를 제거하면 컴파일되지 않습니다. `first` 및 `test`는 모두 대리자 형식이지만 서로 다른 대리자 형식입니다.

## <a name="enum-constraints"></a>열거형 제약 조건

C# 7.3부터 <xref:System.Enum?displayProperty=nameWithType> 형식을 기본 클래스 제약 조건으로 지정할 수도 있습니다. CLR에서는 항상 이 제약 조건을 허용했지만, C# 언어에서는 이 제약 조건을 허용하지 않았습니다. `System.Enum`을 사용하는 제네릭은 `System.Enum`의 정적 메서드를 사용하여 결과를 캐시하기 위해 형식이 안전한 프로그래밍을 제공합니다. 다음 샘플에서는 열거형 형식에 유효한 값을 모두 찾은 다음, 해당 값을 문자열 표현에 매핑하는 사전을 작성합니다.

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#18)]

사용된 메서드는 성능에 영향을 주는 리플렉션을 사용합니다. 리플렉션이 필요한 호출을 반복하는 대신, 이 메서드를 호출하여 캐시되고 다시 사용되는 컬렉션을 작성할 수 있습니다.

다음 샘플과 같이 이 메서드는 열거형을 만들고 해당 값과 이름의 사전을 작성하는 데 사용할 수 있습니다.

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#19)]

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#20)]

## <a name="see-also"></a>참고 항목

- <xref:System.Collections.Generic>
- [C# 프로그래밍 가이드](../index.md)
- [제네릭 소개](./index.md)
- [제네릭 클래스](./generic-classes.md)
- [new 제약 조건](../../language-reference/keywords/new-constraint.md)
