---
title: System.Delegate 및 `delegate` 키워드
description: .NET Framework에서 대리자를 지원하는 클래스와 해당 클래스가 ‘delegate’ 키워드에 매핑되는 방법을 설명합니다.
ms.date: 06/20/2016
ms.assetid: f3742fda-13c2-4283-8966-9e21c2674393
ms.openlocfilehash: 4cf2b113fc9e2c6621f648af7ecb272a42b1f056
ms.sourcegitcommit: 7156c0b9e4ce4ce5ecf48ce3d925403b638b680c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58465778"
---
# <a name="systemdelegate-and-the-delegate-keyword"></a>System.Delegate 및 `delegate` 키워드

[이전](delegates-overview.md)

이 문서에서는 .NET Core Framework에서 대리자를 지원하는 클래스와 해당 클래스가 `delegate` 키워드에 매핑되는 방법을 설명합니다.

## <a name="defining-delegate-types"></a>대리자 형식 정의

먼저 'delegate' 키워드를 살펴보겠습니다. 대리자 작업을 수행할 때 기본적으로 이 키워드를 사용하기 때문입니다. `delegate` 키워드를 사용할 때 컴파일러가 생성하는 코드는 <xref:System.Delegate> 및 <xref:System.MulticastDelegate> 클래스의 멤버를 호출하는 메서드 호출에 매핑됩니다. 

메서드 시그니처를 정의하는 것과 비슷한 구문을 사용하여 대리자 형식을 정의합니다. `delegate` 키워드를 정의에 추가하면 됩니다.

계속해서 List.Sort() 메서드를 예제로 사용합니다. 첫 번째 단계는 비교 대리자에 대한 형식을 만드는 것입니다.

```csharp
// From the .NET Core library

// Define the delegate type:
public delegate int Comparison<in T>(T left, T right);
```

컴파일러에서는 사용된 시그니처와 일치하는 `System.Delegate`에서 파생된 클래스를 생성합니다(이 경우 정수를 반환하고 두 개의 인수가 포함된 메서드). 해당 대리자의 형식은 `Comparison`입니다. `Comparison` 대리자 형식은 제네릭 형식입니다. 제네릭에 대한 자세한 내용은 [여기](generics.md)를 참조하세요.

구문이 변수를 선언하는 것처럼 보일 수 있지만 실제로는 *형식*을 선언합니다. 클래스 내부, 직접 네임스페이스 내부 또는 전역 네임스페이스에 대리자 형식을 정의할 수 있습니다.

> [!NOTE]
> 전역 네임스페이스에 직접 대리자 형식(또는 기타 형식)을 선언하는 것은 권장하지 않습니다. 

이 클래스의 클라이언트가 인스턴스의 호출 목록에서 메서드를 추가 및 제거할 수 있도록 컴파일러에서는 이 새로운 형식에 대한 추가 및 제거 처리기를 생성합니다. 컴파일러는 추가되거나 제거되는 메서드의 시그니처가 메서드를 선언할 대 사용된 시그니처와 일치하도록 지정합니다. 

## <a name="declaring-instances-of-delegates"></a>대리자의 인스턴스 선언

대리자를 정의한 후 해당 형식의 인스턴스를 만들 수 있습니다.
C#의 모든 변수처럼 네임스페이스에서 직접 또는 전역 네임스페이스에서 대리자 인스턴스를 선언할 수 없습니다.

```csharp
// inside a class definition:

// Declare an instance of that type:
public Comparison<T> comparator;
```

변수 형식은 앞에서 정의한 대리자 형식인 `Comparison<T>`입니다. 변수 이름은 `comparator`입니다.
 
 위의 코드 조각에서는 클래스 내부에 멤버 변수를 선언했습니다. 메서드에 대한 인수 또는 지역 변수인 대리자 변수를 선언할 수도 있습니다.

## <a name="invoking-delegates"></a>대리자 호출

대리자를 호출하여 대리자 호출 목록에 있는 메서드를 호출합니다. `Sort()` 메서드 내부에서 코드는 비교 메서드를 호출하여 개체를 배치할 순서를 결정합니다.

```csharp
int result = comparator(left, right);
```

위 줄에서 코드는 대리자에 연결된 메서드를 *호출*합니다.
변수를 메서드 이름으로 처리하고 일반 메서드 호출 구문을 사용하여 변수를 호출합니다.

해당 코드 줄은 안전하지 않은 가정을 생성합니다. 대상이 대리자에 추가되었다는 보장이 없습니다. 대상이 연결되지 않은 경우 위 줄은 `NullReferenceException`을 throw합니다. 이 문제를 해결하는 데 사용된 관용구는 간단한 null 검사보다 더 복잡하고 이 [시리즈](delegates-patterns.md)의 뒷부분에서 설명합니다.

## <a name="assigning-adding-and-removing-invocation-targets"></a>호출 대상 할당, 추가 및 제거

이 방법으로 대리자 형식을 정의하고 대리자 인스턴스를 선언 및 호출합니다.

`List.Sort()` 메서드를 사용하려는 개발자는 시그니처가 대리자 형식 정의와 일치하는 메서드를 정의하고 정렬 메서드에서 사용된 대리자에 할당해야 합니다. 이 할당으로 해당 대리자 개체의 호출 목록에 메서드를 추가합니다.

길이별로 문자열 목록을 정렬한다고 가정합니다. 비교 함수는 다음과 같을 수 있습니다.

```csharp
private static int CompareLength(string left, string right) =>
    left.Length.CompareTo(right.Length);
```

메서드는 private 메서드로 선언됩니다. 괜찮습니다. 이 메서드를 public 인터페이스에 포함하지 않으려고 할 수 있습니다. 대리자에 연결될 경우 비교 메서드로 계속 사용할 수 있습니다. 호출 코드에서는 이 메서드를 대리자 개체의 대상 목록에 연결하고 해당 대리자를 통해 메서드에 액세스할 수 있습니다.

해당 메서드를 `List.Sort()` 메서드에 전달하여 관계를 만듭니다.

```csharp
phrases.Sort(CompareLength);
```

메서드 이름은 괄호 없이 사용됩니다. 메서드를 인수로 사용하면 메서드 참조를 대리자 호출 대상으로 사용될 수 있는 참조로 변환하고 해당 메서드를 호출 대상으로 연결하도록 컴파일러에 알립니다.

`Comparison<string>` 형식의 변수를 선언하고 할당을 수행하여 명시적 상태일 수도 있습니다.

```csharp
Comparison<string> comparer = CompareLength;
phrases.Sort(comparer);
```

대리자 대상으로 사용되는 메서드가 작은 메서드인 경우에는 일반적으로 [람다 식](./programming-guide/statements-expressions-operators/lambda-expressions.md) 구문을 사용하여 할당을 수행합니다.

```csharp
Comparison<string> comparer = (left, right) => left.Length.CompareTo(right.Length);
phrases.Sort(comparer);
```

대리자 대상에 람다 식을 사용하는 방법은 [이후 섹션](delegates-patterns.md)에서 자세히 설명합니다.

Sort() 예제에서는 일반적으로 단일 대상 메서드를 대리자에 연결합니다. 그러나 대리자 개체는 여러 대상 메서드가 대리자 개체에 연결되어 있는 호출 목록을 지원합니다.

## <a name="delegate-and-multicastdelegate-classes"></a>Delegate 및 MulticastDelegate 클래스

위에 설명된 언어 지원은 일반적으로 대리자를 사용할 때 필요한 기능과 지원을 제공합니다. 이러한 기능은 .NET Core Framework의 두 가지 클래스 <xref:System.Delegate> 및 <xref:System.MulticastDelegate>를 기반으로 빌드됩니다.

`System.Delegate` 클래스와 단일 직접 하위 클래스 `System.MulticastDelegate`는 대리자를 만들고, 메서드를 대리자 대상으로 등록하고, 대리자 대상으로 등록된 모든 메서드를 호출하기 위한 프레임워크 지원을 제공합니다. 

흥미롭게도 `System.Delegate` 및 `System.MulticastDelegate` 클래스는 자체가 대리자 형식이 아닙니다. 모든 특정 대리자 형식에 대한 기초를 제공합니다. 동일한 언어 디자인 프로세스에서는 `Delegate` 또는 `MulticastDelegate`에서 파생되는 클래스를 선언할 수 없도록 요구했습니다. C# 언어 규칙은 이러한 선언을 금지합니다.
 
대신에 C# 컴파일러는 C# 언어 키워드를 사용하여 대리자 형식을 선언할 경우 `MulticastDelegate`에서 파생된 클래스의 인스턴스를 만듭니다.

이 디자인은 C# 및 .NET의 첫 번째 릴리스를 기반으로 합니다. 디자인 팀의 한 가지 목적은 언어에서 대리자를 사용할 때 형식 안전성을 적용하는지 확인하는 것이었습니다. 이는 대리자가 인수의 올바른 형식 및 개수를 사용하여 호출되는지 확인함을 의미합니다. 또한 컴파일 시간에 반환 형식이 제대로 표시되었는지 확인함을 의미합니다. 대리자는 이전에 제네릭이었던 1.0 .NET 릴리스의 일부였습니다.

이 형식 안전성을 적용하는 가장 좋은 방법은 컴파일러에서 사용되는 메서드 시그니처를 표현한 구체적인 대리자 클래스를 만드는 것이었습니다.

파생 클래스를 만들 수 없더라도 이러한 클래스에서 정의된 메서드를 사용하게 됩니다. 대리자 관련 작업을 수행할 때 사용할 가장 일반적인 메서드를 살펴보겠습니다.

기억해야 하는 가장 중요한 첫 번째 사실은 사용하는 모든 대리자는 `MulticastDelegate`에서 파생된다는 것입니다. 멀티캐스트 대리자는 대리자를 통해 호출할 경우 두 개 이상의 메서드 대상이 호출될 수 있음을 의미합니다. 원래 디자인에서는 하나의 대상 메서드만 연결 및 호출할 수 대리자와 여러 대상 메서드를 연결 및 호출할 수 있는 대리자를 구분하도록 고려했습니다. 이 구분은 원래 고려한 것보다 실제로 그다지 유용하지 않았습니다. 두 가지 클래스가 이미 만들어졌고 초기 공식 릴리스 이후 프레임워크에 포함되었습니다.

대리자와 함께 가장 많이 사용할 메서드는 `Invoke()` 및 `BeginInvoke()` / `EndInvoke()`입니다. `Invoke()`는 특정 대리자 인스턴스에 연결된 모든 메서드를 호출합니다. 위에서 확인한 대로, 일반적으로 대리자 변수에서 메서드 호출 스택을 사용하여 대리자를 호출합니다. [이 시리즈의 뒷부분](delegates-patterns.md)에서 살펴보겠지만 이러한 메서드에서 직접 사용되는 패턴이 있습니다.

이제 언어 구문 및 대리자 지원 클래스를 확인했으므로 강력한 형식의 대리자를 사용하고, 만들고, 호출하는 방법을 살펴보겠습니다.

[다음](delegates-strongly-typed.md)
