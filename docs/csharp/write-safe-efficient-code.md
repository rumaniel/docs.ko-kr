---
title: 안전하고 효율적인 C# 코드 작성
description: 최근 C# 언어의 향상된 기능을 통해 성능이 이전에는 안전하지 않은 코드와 연결되어 있는 안정형 안전 코드를 작성할 수 있습니다.
ms.date: 10/23/2018
ms.custom: mvc
ms.openlocfilehash: 73ad7a84d2ad47f0e0242825d250247ffb39928e
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66832937"
---
# <a name="write-safe-and-efficient-c-code"></a>안전하고 효율적인 C# 코드 작성

C#의 새 기능을 사용하면 향상된 성능으로 안정형의 안전 코드를 작성할 수 있습니다. 이러한 기술을 신중하게 적용한다면 안전하지 않은 코드가 필요한 시나리오는 더 적어집니다. 이러한 기능을 통해 값 형식에 대한 참조를 메서드 인수 및 메서드 반환 값으로 사용하기가 더 쉬워집니다. 안전하게 수행하면 이러한 기술로 값 형식 복사가 최소화됩니다. 값 형식을 사용하면 할당 수 및 가비지 수집 단계를 최소화할 수 있습니다.

이 문서의 샘플 코드 상당수는 C# 7.2에 추가된 기능을 사용합니다. 이러한 기능을 사용하려면 C# 7.2 이상을 사용하도록 프로젝트를 구성해야 합니다. 언어 버전 설정에 대한 자세한 내용은 [언어 버전 구성](language-reference/configure-language-version.md)을 참조하세요.

이 문서에서는 효율적인 리소스 관리를 위한 기술에 중점을 둡니다. 값 형식을 사용할 경우 한 가지 장점은 대개 힙 할당을 할 필요가 없다는 것입니다. 단점은 값으로 복사된다는 점입니다. 이러한 장단점 간에 균형을 잡으려고 하니 많은 양의 데이터에서 작동하는 알고리즘을 최적화하기가 어렵습니다. C# 7.2의 새로운 언어 기능은 값 형식에 대한 참조를 사용하여 안전하고 효율적인 코드를 가능하게 하는 메커니즘을 제공합니다. 이러한 기능을 현명하게 사용하여 할당 및 복사 작업을 최소화하세요. 이 문서에서는 이러한 새로운 기능을 살펴봅니다.

이 문서에서는 다음과 같은 리소스 관리 기술에 중점을 둡니다.

- 형식이 **변경할 수 없음** 상태이며 [`in`](language-reference/keywords/in-parameter-modifier.md) 매개 변수를 사용하는 경우 컴파일러가 복사본을 저장할 수 있음을 나타내도록 [`readonly struct`](language-reference/keywords/readonly.md#readonly-struct-example)를 선언합니다.
- 반환 값이 <xref:System.IntPtr.Size?displayProperty=nameWithType>보다 큰 `struct`이고 스토리지 수명이 값을 반환하는 메서드보다 클 경우 [`ref readonly`](language-reference/keywords/ref.md#reference-return-values) 반환을 사용합니다.
- 성능 상의 이유로 `readonly struct`의 크기가 <xref:System.IntPtr.Size?displayProperty=nameWithType>보다 큰 경우 `in` 매개 변수로 전달해야 합니다.
- 성능에 부정적인 영향을 주거나 모호한 동작으로 이어질 수 있으므로 `readonly` 한정자로 선언되지 않는 한, `struct`를 `in` 매개 변수로 전달해서는 안 됩니다.
- 메모리를 바이트의 시퀀스로 사용하도록[`ref struct`](language-reference/keywords/ref.md#ref-struct-types) 또는 `readonly ref struct`(예: <xref:System.Span%601> 또는 <xref:System.ReadOnlySpan%601>)를 사용합니다.

이러한 기술을 통해 **참조** 및 **값**에 관한 상충적인 두 가지 목표 간에 균형을 유지할 수 있습니다. [참조 형식](programming-guide/types/index.md#reference-types)인 변수는 메모리의 위치에 대한 참조를 유지합니다. [값 형식](programming-guide/types/index.md#value-types)인 변수는 직접 해당 값을 포함합니다. 이러한 차이는 메모리 리소스를 관리하는 데 중요한 차이점을 강조합니다. **값 형식**은 일반적으로 메서드에 전달되거나 메서드에서 반환된 경우 복사됩니다. 이 동작에는 값 형식의 멤버를 호출하는 경우 `this`의 값을 복사하는 동작이 포함됩니다. 복사의 비용은 형식의 크기와 관련이 있습니다. **참조 형식**은 관리형 힙에 할당됩니다. 각 새 개체는 새로 할당해야 하고 이후에 회수되어야 합니다. 이러한 두 작업은 모두 시간이 걸립니다. 참조 형식이 메서드에 인수로 전달되거나 메서드에서 반환되면 참조가 복사됩니다.

이 문서에서는 이러한 권장 사항을 설명하기 위해 3D 요소 구조체의 다음 예제 개념을 사용합니다.

```csharp
public struct Point3D
{
    public double X;
    public double Y;
    public double Z;
}
```

다른 예제에서는 이 개념의 다른 구현을 사용합니다.

## <a name="declare-readonly-structs-for-immutable-value-types"></a>변경할 수 없는 값 형식에 대해 읽기 전용 구조체 선언

`readonly` 한정자를 사용하여 `struct`를 선언하면 변경할 수 없는 형식을 만들려는 의도를 컴파일러에 알립니다. 컴파일러는 다음 규칙을 사용하여 해당 디자인 결정을 적용합니다.

- 모든 필드 멤버는 `readonly`여야 합니다.
- 모든 속성은 자동으로 구현된 속성을 포함하여 읽기 전용이어야 합니다.

이러한 두 규칙으로 `readonly struct`의 멤버가 해당 구조체 상태를 수정하지 않도록 할 수 있습니다. `struct`는 변경할 수 없습니다. `Point3D` 구조체는 다음 예제에 나온 것처럼 변경할 수 없는 구조체로 정의할 수 있습니다.

```csharp
readonly public struct ReadonlyPoint3D
{
    public ReadonlyPoint3D(double x, double y, double z)
    {
        this.X = x;
        this.Y = y;
        this.Z = z;
    }

    public double X { get; }
    public double Y { get; }
    public double Z { get; }
}
```

디자인 의도가 변경할 수 없는 값 형식을 만드는 것이라면 이 권장 사항을 따릅니다. 성능 개선 사항은 추가적인 혜택입니다. `readonly struct`는 디자인 의도를 명확하게 표현합니다.

## <a name="use-ref-readonly-return-statements-for-large-structures-when-possible"></a>가능하면 큰 구조체에 `ref readonly return` 문 사용

반환되는 값이 반환 메서드에 로컬이 아닐 경우 참조로 값을 반환할 수 있습니다. 참조로 반환하는 것은 구조체가 아니라 참조만 복사된다는 것을 의미합니다. 다음 예제에서는 반환되는 값이 로컬 변수이므로 `Origin` 속성은 `ref` 반환을 사용할 수 없습니다.

```csharp
public Point3D Origin => new Point3D(0,0,0);
```

단, 반환된 값이 정적 멤버이므로 다음 속성 정의를 참조로 반환할 수 있습니다.

```csharp
public struct Point3D
{
    private static Point3D origin = new Point3D(0,0,0);

    // Dangerous! returning a mutable reference to internal storage
    public ref Point3D Origin => ref origin;

    // other members removed for space
}
```

호출자가 원점을 수정하지 않도록 하려면 `readonly ref`로 값을 반환해야 합니다.

```csharp
public struct Point3D
{
    private static Point3D origin = new Point3D(0,0,0);

    public static ref readonly Point3D Origin => ref origin;

    // other members removed for space
}
```

`ref readonly`를 반환하면 더 큰 구조체 복사본을 저장하고 내부 데이터 멤버의 불변성을 유지할 수 있습니다.

호출 사이트에서 호출자가 `Origin` 속성을 `readonly ref` 또는 값으로 사용하도록 선택할 수 있습니다.

[!code-csharp[AssignRefReadonly](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#AssignRefReadonly "Assigning a ref readonly")]

이전 코드의 첫 번째 할당에서는 `Origin` 상수의 복사본을 만들고 해당 복사본을 할당합니다. 두 번째 할당에서는 참조를 할당합니다. `readonly` 한정자는 변수 선언의 일부여야 합니다. 참조하는 항목에 대한 참조는 수정할 수 없습니다. 이를 수행하려고 시도하면 컴파일 시간 오류가 발생합니다.

`readonly` 한정자는 `originReference` 선언에 필요합니다.

컴파일러는 호출자가 참조를 수정할 수 없도록 합니다. 값을 직접 할당하려고 하면 컴파일 시간 오류가 발생합니다. 그러나 컴파일러는 멤버 메서드가 구조체의 상태를 수정하는지를 알 수 없습니다.
개체가 수정되지 않도록 하기 위해 컴파일러는 복사본을 만들고 해당 복사본을 사용하여 멤버 참조를 호출합니다. 모든 수정은 해당 방어 복사본에 대한 것입니다.

## <a name="apply-the-in-modifier-to-readonly-struct-parameters-larger-than-systemintptrsize"></a>`in` 한정자를 `System.IntPtr.Size`보다 큰 `readonly struct` 매개 변수에 적용

`in` 키워드는 기존 `ref` 및 `out` 키워드를 보완하여 참조로 인수를 전달합니다. `in` 키워드는 인수를 참조로 전달하도록 지정하지만 호출된 메서드는 값을 수정하지 않습니다.

이 추가는 설계 의도를 표현하기 위한 완벽한 어휘를 제공합니다.
메서드 서명에 다음 한정자 중 어떤 것도 지정하지 않으면 호출된 메서드에 전달될 때 값 형식이 복사됩니다. 이러한 각 한정자는 변수가 참조로 전달되도록 지정하여 복사를 방지합니다. 각 한정자는 각기 다른 의도를 표현합니다.

- `out`: 이 메서드는 이 매개 변수로 사용되는 인수의 값을 설정합니다.
- `ref`: 이 메서드는 이 매개 변수로 사용되는 인수의 값을 설정할 수 있습니다.
- `in`: 이 메서드는 이 매개 변수로 사용되는 인수의 값을 수정하지 않습니다.

참조로 인수를 전달하기 위해 `in` 한정자를 추가하고 불필요한 복사를 방지하기 위해 참조로 인수를 전달할 디자인 의도를 선언합니다. 해당 인수로 사용되는 개체를 수정할 의도가 없습니다.

이 방법은 종종 <xref:System.IntPtr.Size?displayProperty=nameWithType>보다 큰 읽기 전용 값 형식에 대한 성능을 향상시킵니다. 단순 형식(`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool` 및 `enum` 형식)의 경우 모든 잠재적 성능 향상이 최소화됩니다. 사실 <xref:System.IntPtr.Size?displayProperty=nameWithType>보다 작은 형식에 참조로 전달을 사용하면 성능이 저하될 수 있습니다.

다음 코드는 3D 공간에서 두 점 사이의 거리를 계산하는 메서드의 예를 보여 줍니다.

[!code-csharp[InArgument](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#InArgument "Specifying an in argument")]

인수는 각각 세 개의 double을 포함하는 두 개의 구조입니다. double은 8바이트이므로 각 인수는 24바이트입니다. `in` 한정자를 지정하여 머신 아키텍처에 따라 해당 인수에 4바이트 또는 8바이트 참조를 전달합니다. 크기의 차이는 작지만, 애플리케이션이 다양한 값을 사용하여 연속 루프에서 이 메서드를 호출하면 늘어납니다.

`in` 한정자는 `out` 및 `ref`를 다른 방식으로도 보완합니다. `in`, `out` 또는 `ref`가 있는 경우에만 다른 메서드의 오버로드는 만들 수 없습니다. 이러한 새 규칙은 항상 `out` 및 `ref` 매개 변수에 대해 정의된 같은 동작을 확장합니다. `out` 및 `ref` 한정자와 마찬가지로 `in` 한정자가 적용되므로 값 형식이 boxing되지 않습니다.

`in` 한정자는 메서드, 대리자, 람다, 로컬 함수, 인덱서, 연산자 매개 변수를 사용하는 모든 멤버에 적용될 수 있습니다.

`in` 매개 변수의 다른 기능은 `in` 매개 변수에 대한 인수에 리터럴 값 또는 상수를 사용하는 것입니다. 또한 `ref` 또는 `out` 매개 변수와 달리 호출 사이트에서 `in` 한정자를 적용할 필요가 없습니다. 다음 코드는 `CalculateDistance` 메서드를 호출하는 두 가지 예를 보여 줍니다. 첫 번째 예에서는 참조로 전달된 두 개의 로컬 변수를 사용합니다. 두 번째 예는 메서드 호출의 일부로 만들어진 임시 변수를 포함합니다.

[!code-csharp[UseInArgument](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#UseInArgument "Specifying an In argument")]

컴파일러가 `in` 인수의 읽기 전용 특성을 강제 적용하는 여러 가지 방법이 있습니다.  먼저, 호출된 메서드는 `in` 매개 변수에 직접 할당할 수 없습니다. 값이 `struct` 형식일 때 `in` 매개 변수의 모든 필드에 직접 할당할 수 없습니다. 또한 `ref` 또는 `out` 한정자를 사용하여 모든 메서드에 `in` 매개 변수를 전달할 수 없습니다.
이러한 규칙은 필드가 `struct` 형식이고 매개 변수 또한 `struct` 형식인 경우 `in` 매개 변수의 모든 필드에 적용됩니다. 사실 이러한 규칙은 멤버 액세스의 모든 수준에서 형식이 `structs`인 경우 멤버 액세스의 여러 계층에 적용됩니다.
컴파일러는 `in` 인수로 전달된 `struct` 형식과 그 `struct` 멤버가 다른 메서드에 대한 인수로 사용될 경우 읽기 전용 변수가 되도록 합니다.

`in` 매개 변수를 사용하면 복사본 작성 시 발생할 수 있는 잠재적인 성능 비용을 방지할 수 있습니다. 어떠한 메서드 호출의 의미 체계도 변경되지 않습니다. 따라서 호출 사이트에서 `in` 한정자를 지정할 필요가 없습니다. 호출 사이트에서 `in` 한정자를 생략하면 다음과 같은 이유로 인수의 복사본을 만들 수 있음을 컴파일러에 알립니다.

- 암시적 변환은 있지만 인수 유형에서 매개 변수 유형으로의 ID 변환이 아닙니다.
- 인수는 식이지만 알려진 스토리지 변수는 없습니다.
- `in`의 유무의 따라 달라지는 오버로드가 있습니다. 이 경우에는 by 값 오버로드가 더 적합합니다.

이러한 규칙은 읽기 전용 참조 인수를 사용하도록 기존 코드를 업데이트할 때 유용합니다. 호출된 메서드 내에서 by 값 매개 변수를 사용하는 모든 인스턴스 메서드를 호출할 수 있습니다. 이러한 경우 `in` 매개 변수의 복사본이 만들어집니다. 컴파일러가 `in` 매개 변수에 대한 임시 변수를 만들 수 있으므로 사용자는 `in` 매개 변수에 대한 기본값을 지정할 수도 있습니다. 다음 코드에서는 원점(포인트 0,0)을 두 번째 점의 기본값으로 지정합니다.

[!code-csharp[InArgumentDefault](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#InArgumentDefault "Specifying defaults for an in parameter")]

컴파일러가 읽기 전용 인수를 참조로 전달하도록 하려면 다음 코드에 나와 있는 것처럼 호출 사이트의 인수에 `in` 한정자를 지정합니다.

[!code-csharp[UseInArgument](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#ExplicitInArgument "Specifying an In argument")]

이 동작을 통해 성능 향상이 가능한 대규모 코드 베이스에서 시간이 지남에 따라 `in` 매개 변수를 보다 쉽게 채택할 수 있습니다. 먼저 메서드 서명에 `in` 한정자를 추가합니다. 그런 다음, 호출 사이트에 `in` 한정자를 추가하고 `readonly struct` 형식을 생성하여 컴파일러가 더 많은 위치에서 `in` 매개 변수의 방어 복사본을 만들지 않도록 할 수 있습니다.

`in` 매개 변수 지정은 참조 형식 또는 숫자 값과 함께 사용될 수도 있습니다. 그러나 두 경우 모두의 이점은 있다고 하더라도 아주 적습니다.

## <a name="never-use-mutable-structs-as-in-in-argument"></a>`in` 인수와 마찬가지로 변경할 수 있는 구조체 사용 안 함

앞에서 설명한 기술은 반환 참조에 의한 복사 및 참조로 값 전달을 방지하는 방법을 설명합니다. 이러한 기술은 인수 형식이 `readonly struct` 형식으로 선언되는 경우에 가장 적합합니다. 그렇지 않은 경우, 인수의 읽기 전용 특성을 적용하기 위해 많은 상황에서 컴파일러는 **방어 복사본**을 만들어야 합니다. 원점에서 3D 요소의 거리를 계산하는 다음과 같은 예제를 살펴보세요.

[!code-csharp[InArgument](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#InArgument "Specifying an in argument")]

`Point3D` 구조체는 읽기 전용 구조체가 *아닙니다*. 이 메서드의 본문에는 6개의 서로 다른 속성 액세스 호출이 있습니다. 첫 번째 검사에서 이러한 액세스가 안전하다고 생각했을 것입니다. 결국 `get` 접근자는 개체의 상태를 수정하면 안됩니다. 하지만 이를 적용하는 언어 규칙이 없습니다. 일반적인 관습일 뿐입니다. 모든 형식은 내부 상태를 수정한 `get` 접근자를 구현할 수 있습니다. 일부 언어 보장 없이 컴파일러는 모든 멤버를 호출하기 전에 인수의 임시 복사본을 만들어야 합니다. 임시 스토리지가 스택에 만들어지고, 인수 값이 임시 스토리지에 복사되며, 값이 `this` 인수로 각 멤버 액세스에 대한 스택으로 복사됩니다. 다양한 상황에서 이러한 복사는 인수 형식이 `readonly struct`가 아닌 경우 값으로 전달이 읽기 전용 참조로 전달보다 더 빠를 정도로 성능을 저하시킵니다.

대신 거리 계산이 변경할 수 없는 구조체인 `ReadonlyPoint3D`를 사용하는 경우 임시 개체는 필요하지 않습니다.

[!code-csharp[readonlyInArgument](../../samples/csharp/safe-efficient-code/ref-readonly-struct/Program.cs#ReadOnlyInArgument "Specifying a readonly in argument")]

컴파일러가 `readonly struct`의 멤버를 호출할 때 더 효율적인 코드를 생성합니다. 수신기의 복사본 대신 `this` 참조는 항상 멤버 메서드에 대한 참조로 전달된 `in` 매개 변수입니다. 이 최적화는 `readonly struct`를 `in` 인수로 사용하는 경우 복사본을 저장합니다.

null 허용 값 형식은 `in` 인수로 전달할 수 없습니다. <xref:System.Nullable%601> 형식은 읽기 전용 구조체로 선언되지 않습니다. 즉 컴파일러가 매개 변수 선언에서 `in` 수정자를 사용하여 메서드에 전달된 모든 null 허용 값 형식 인수에 대해 방어용 복사본을 생성해야 합니다.

GitHub에 있는 [샘플 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/safe-efficient-code/benchmark)에서 [Benchmark.net](https://www.nuget.org/packages/BenchmarkDotNet/)을 사용하여 성능 차이를 설명하는 예제 프로그램을 확인할 수 있습니다. 값으로 및 참조로 변경할 수 있는 구조체를 전달하는 것과 값으로 및 참조로 변경할 수 없는 구조체를 전달하는 것을 비교합니다. 변경할 수 없는 구조체를 사용하고 참조로 전달하는 것이 가장 빠릅니다.

## <a name="use-ref-struct-types-to-work-with-blocks-or-memory-on-a-single-stack-frame"></a>단일 스택 프레임의 블록 또는 메모리를 작업하기 위해 `ref struct` 형식을 사용합니다.

관련 언어 기능은 단일 스택 프레임에 제한되어야 하는 값 형식을 선언하는 기능입니다. 이 제한을 통해 컴파일러는 몇 가지 최적화를 수행할 수 있습니다. 이 기능의 기본 동기 부여는 <xref:System.Span%601> 및 관련 구조였습니다. <xref:System.Span%601> 유형을 사용하는 새롭고 업데이트된 .NET API를 사용함으로써 이러한 향상된 기능으로부터 성능 향상을 달성할 수 있습니다.

[`stackalloc`](language-reference/operators/stackalloc.md)을 사용하여 만들어진 메모리로 작업할 때나 interop API에서 메모리를 사용할 때도 유사한 요구 사항이 있을 수 있습니다. 해당 요구 사항에 대한 사용자 고유의 `ref struct` 형식을 정의할 수 있습니다.

## <a name="readonly-ref-struct-type"></a>`readonly ref struct` 형식

구조체를 `readonly ref`로 선언하면 `ref struct` 및 `readonly struct` 선언의 이점과 제한이 결합됩니다. 읽기 전용 범위에서 사용된 메모리는 단일 스택 프레임으로 제한되며 읽기 전용 범위에서 사용된 메모리는 수정할 수 없습니다.

## <a name="conclusions"></a>결론

값 형식을 사용하면 할당 작업 수가 최소화됩니다.

- 값 형식에 대한 스토리지는 로컬 변수와 메서드 인수에 스택 할당됩니다.
- 다른 개체의 멤버인 값 형식에 대한 스토리지는 별도 할당이 아니라 해당 개체의 일부로 할당됩니다.
- 값 형식 반환 값에 대한 스토리지는 스택 할당됩니다.

그러한 동일한 상황에서 참조 형식과 대조를 보입니다.

- 참조 형식에 대한 스토리지는 로컬 변수 및 메서드 인수에 힙 할당됩니다. 참조는 스택에 저장됩니다.
- 다른 개체의 멤버인 참조 형식에 대한 스토리지는 별도로 힙에 할당됩니다. 포함하는 개체는 참조를 저장합니다.
- 참조 형식 반환 값에 대한 스토리지는 힙 할당됩니다. 해당 스토리지에 대한 참조는 스택에 저장됩니다.

할당을 최소화하는 작업에는 장단점이 있습니다. `struct`의 크기가 참조의 크기보다 큰 경우 더 많은 메모리를 복사할 수 있습니다. 참조는 일반적으로 64비트 또는 32비트이며 대상 머신 CPU에 따라 달라집니다.

이러한 장단점은 일반적으로 성능에 거의 영향을 주지 않습니다. 그러나 구조체 또는 컬렉션이 더 큰 경우 성능에 미치는 영향은 증가합니다. 연속 루프 및 과다 경로에서는 프로그램에 대한 영향이 더 커질 수 있습니다.

C# 언어에 대한 이러한 향상된 기능은 메모리 할당을 최소화하는 것이 필요한 성능을 달성하는 데 중요한 요인이 되는 성능 중요 알고리즘을 위해 설계되었습니다. 작성하는 코드에서 이러한 기능을 자주 사용하지 않을 수 있습니다. 그러나 이러한 향상된 기능은 .NET 전반에서 채택되었습니다. 점점 더 많은 API에서 이러한 기능을 사용하므로 사용자의 애플리케이션 성능이 개선되는 것을 확인할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [ref 키워드](language-reference/keywords/ref.md)
- [Ref return 및 ref local](programming-guide/classes-and-structs/ref-returns.md)
