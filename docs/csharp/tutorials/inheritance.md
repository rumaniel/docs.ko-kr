---
title: C#의 상속
description: C# 라이브러리 및 애플리케이션에서 상속 사용 방법 알아보기
author: rpetrusha
ms.author: ronpet
ms.date: 07/05/2018
ms.assetid: aeb68c74-0ea0-406f-9fbe-2ce02d47ef31
ms.openlocfilehash: 41377cb47836624160a5b402e0a85270b68eba4f
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70850992"
---
# <a name="inheritance-in-c-and-net"></a>C# 및 .NET의 상속

이 자습서에서는 C#의 상속에 대해 소개합니다. 상속은 특정 기능(데이터 및 동작)을 제공하는 기본 클래스를 정의하고 해당 기능을 상속하거나 재정의하는 파생 클래스를 정의할 수 있는 개체 지향 프로그래밍 언어의 기능입니다.

## <a name="prerequisites"></a>전제 조건

이 자습서에서는 .NET Core SDK를 설치했다고 가정합니다. 다운로드하려면 [.NET Core 다운로드](https://dotnet.microsoft.com/download) 페이지를 방문하세요. 코드 편집기도 필요합니다. 원하는 어떤 코드 편집기도 사용 가능하지만 이 자습서에서는 [Visual Studio Code](https://code.visualstudio.com)를 사용합니다.

## <a name="running-the-examples"></a>예제 실행

이 자습서의 예제를 만들고 실행하기 위해 명령줄에서 [dotnet](../../core/tools/dotnet.md) 유틸리티를 사용합니다. 각 예제에 대해 다음 단계를 수행합니다.

1. 이 예제를 저장할 디렉터리를 만듭니다.
1. 명령 프롬프트에 [dotnet new console](../../core/tools/dotnet-new.md)을 입력하여 새로운 .NET Core 프로젝트를 만듭니다.
1. 예제의 코드를 복사한 후 코드 편집기에 붙여 넣습니다.
1. 명령줄에서 [dotnet restore](../../core/tools/dotnet-restore.md) 명령을 입력하여 프로젝트의 종속성을 로드하거나 복원합니다.

  [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

1. [dotnet run](../../core/tools/dotnet-run.md) 명령을 입력하여 예제를 컴파일하고 실행합니다.

## <a name="background-what-is-inheritance"></a>배경: 상속이란?

*상속*은 개체 지향 프로그래밍의 기본적인 특성 중 하나입니다. 부모 클래스의 동작을 다시 사용(상속), 확장 또는 수정하는 자식 클래스를 정의할 수 있습니다. 멤버가 상속되는 클래스를 *기본 클래스*라고 합니다. 기본 클래스의 멤버를 상속하는 클래스를 *파생 클래스*라고 합니다.

C# 및 .NET은 *단일 상속*만 지원합니다. 즉, 하나의 클래스가 단일 클래스에서만 상속할 수 있습니다. 그러나 상속은 전이적이므로 형식 집합에 대해 상속 계층을 정의할 수 있습니다. 즉, 형식 `D`는 형식 `C`에서 상속할 수 있으며, 이 형식은 `B` 형식에서 상속하고, 이 형식은 기본 클래스 형식 `A`에서 상속합니다. 상속은 전이적이므로 형식 `A`의 멤버를 형식 `D`에서 사용할 수 있습니다.

기본 클래스의 모든 멤버가 파생 클래스에서 상속되는 것은 아닙니다. 다음 멤버는 상속되지 않습니다.

- [정적 생성자](../programming-guide/classes-and-structs/static-constructors.md): 클래스의 정적 데이터를 초기화합니다.

- [인스턴스 생성자](../programming-guide/classes-and-structs/constructors.md): 클래스의 새 인스턴스를 만들기 위해 호출합니다. 각 클래스는 자체 생성자를 정의해야 합니다.

- [종료자](../programming-guide/classes-and-structs/destructors.md): 클래스의 인스턴스를 삭제하기 위해 런타임의 가비지 수집기에 의해 호출됩니다.

기본 클래스의 다른 모든 멤버는 파생 클래스에서 상속되지만 표시 가능 여부는 해당 액세스 가능성에 따라 달라집니다. 멤버의 액세스 가능성은 다음과 같이 파생 클래스의 표시 여부에 영향을 미칩니다.

- [개인](../language-reference/keywords/private.md) 멤버는 기본 클래스에 중첩된 파생 클래스에서만 표시됩니다. 그렇지 않으면 파생 클래스에서 표시되지 않습니다. 다음 예제에서 `A.B`는 `A`에서 파생되는 중첩 클래스이고 `C`는 `A`에서 파생됩니다. 개인 `A.value` 필드는 A.B에 표시됩니다. 그러나 `C.GetValue` 메서드에서 주석을 제거하고 예제를 컴파일하려고 하면 컴파일러 오류 CS0122: "보호 수준 때문에 'A.value'에 액세스할 수 없습니다."가 표시됩니다.

  [!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/private.cs#1)]

- [Protected](../language-reference/keywords/protected.md) 멤버는 파생 클래스에서만 표시됩니다.

- [Internal](../language-reference/keywords/internal.md) 멤버는 기본 클래스와 동일한 어셈블리에 있는 파생 클래스에서만 표시됩니다. 기본 클래스와는 다른 어셈블리에 있는 파생 클래스에서는 표시되지 않습니다.

- [Public](../language-reference/keywords/public.md) 멤버는 파생 클래스에서 표시되고 파생 클래스의 공용 인터페이스에 속합니다. 상속된 public 멤버는 파생 클래스에서 정의된 것처럼 호출할 수 있습니다. 다음 예제에서 클래스 `A`는 `Method1`이라는 메서드를 정의하고 클래스 `B`는 클래스 `A`에서 상속합니다. 그런 다음 이 예제에서는 마치 `B`에 대한 인스턴스 메서드인 것처럼 `Method1`을 호출합니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/basics.cs#1)]

파생 클래스는 대체 구현을 제공하여 상속된 멤버를 *재정의*할 수도 있습니다. 멤버를 재정의하기 위해서는 기본 클래스의 멤버가 [virtual](../language-reference/keywords/virtual.md) 키워드로 표시되어야 합니다. 기본적으로 기본 클래스 멤버는 `virtual`로 표시되지 않으며 재정의할 수 없습니다. 다음 예제와 같이 비가상 멤버를 재정의하려고 하면 컴파일러 오류 CS0506: "\<member>는 virtual, abstract 또는 override로 표시되지 않으므로 상속된 멤버 \<member>를 재정의할 수 없습니다.”가 표시됩니다.

```csharp
public class A
{
    public void Method1()
    {
        // Do something.
    }
}

public class B : A
{
    public override void Method1() // Generates CS0506.
    {
        // Do something else.
    }
}
```

일부 경우에 파생 클래스는 기본 클래스 구현을 *반드시* 재정의해야 합니다. [abstract](../language-reference/keywords/abstract.md) 키워드로 표시된 기본 클래스 멤버의 경우 파생 클래스에서 재정의해야 합니다. 다음 예제를 컴파일하려고 하면 클래스 `B`가 `A.Method1`에 대한 구현을 제공하지 않으므로 컴파일러 오류 CS0534, “&lt;class&gt;는 상속된 추상 멤버 &lt;member&gt;를 구현하지 않습니다.”가 표시됩니다.

```csharp
public abstract class A
{
    public abstract void Method1();
}

public class B : A // Generates CS0534.
{
    public void Method3()
    {
        // Do something.
    }
}
```

상속은 클래스 및 인터페이스에만 적용됩니다. 다른 형식 범주(구조체, 대리자 및 열거형)은 상속을 지원하지 않습니다. 이러한 규칙 때문에 다음 예제와 같은 코드를 컴파일하려고 하면 컴파일러 오류 CS0527이 발생합니다. "인터페이스 목록에 있는 'ValueType' 형식이 인터페이스가 아닙니다." 이 오류 메시지는 구조체가 구현하는 인터페이스를 정의할 수 있지만 상속은 지원되지 않음을 나타냅니다.

```csharp
using System;

public struct ValueStructure : ValueType // Generates CS0527.
{
}
```

## <a name="implicit-inheritance"></a>암시적 상속

단일 상속을 통해 상속할 수 있는 형식을 제외하고, .NET 형식 시스템의 모든 형식은 <xref:System.Object> 또는 여기에서 파생된 형식에서 암시적으로 상속합니다. <xref:System.Object>의 공통 기능은 모든 형식에서 사용할 수 있습니다.

암시적 상속의 의미를 살펴보기 위해 빈 클래스 정의에 해당하는 새 클래스 `SimpleClass`를 정의해 보겠습니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/simpleclass.cs#1)]

그런 다음, 리플렉션(형식의 메타데이터를 검사하여 해당 형식에 대한 정보를 가져올 수 있음)을 사용하여 `SimpleClass` 형식에 속한 멤버의 목록을 가져올 수 있습니다. `SimpleClass` 클래스에 어떤 멤버도 정의되지 않은 경우에도 예제의 출력에는 실제로 9개의 멤버가 있는 것으로 나타납니다. 이러한 멤버 중 하나는 C# 컴파일러에서 `SimpleClass` 형식에 대해 자동으로 제공하는 매개 변수가 없는(또는 기본) 생성자입니다. 나머지 8개 멤버는 .NET 형식 시스템의 모든 클래스 및 인터페이스가 마지막에 암시적으로 상속하는 형식인 <xref:System.Object>의 멤버입니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/simpleclass.cs#2)]

<xref:System.Object> 클래스에서 암시적으로 상속되므로 다음 메서드를 `SimpleClass` 클래스에서 사용할 수 있습니다.

- 공용 `ToString` 메서드: `SimpleClass` 개체를 해당 문자열 표현으로 변환하고 정규화된 형식 이름을 반환합니다. 이 경우 `ToString` 메서드는 문자열 "SimpleClass"를 반환합니다.

- 두 개체가 같은지를 테스트하는 세 가지 메서드: 공용 인스턴스 `Equals(Object)` 메서드, 공용 정적 `Equals(Object, Object)` 메서드, 공용 정적 `ReferenceEquals(Object, Object)` 메서드. 기본적으로 이러한 메서드는 참조 같음을 테스트합니다. 즉, 두 개체 변수가 같으려면 같은 개체를 참조해야 합니다.

- 공용 `GetHashCode` 메서드: 형식의 인스턴스가 해시된 컬렉션에 사용될 수 있도록 하는 값을 계산합니다.

- 공용 `GetType` 메서드: `SimpleClass` 형식을 나타내는 <xref:System.Type> 개체를 반환합니다.

- 보호된 <xref:System.Object.Finalize%2A> 메서드: 개체의 메모리를 가비지 수집기에 의해 회수되기 전에 관리되지 않는 리소스를 해제하도록 설계되었습니다.

- 보호된 <xref:System.Object.MemberwiseClone%2A> 메서드: 현재 개체의 단순 복제를 만듭니다.

암시적 상속으로 인해 `SimpleClass` 개체에서 상속된 모든 멤버를 실제로 `SimpleClass` 클래스에 정의된 멤버인 것처럼 호출할 수 있습니다. 예를 들어 다음 예제에서는 `SimpleClass` 가 <xref:System.Object> 에서 상속하는 `SimpleClass.ToString` 메서드를 호출합니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/simpleclass2.cs#1)]

다음 표에는 C#으로 만들 수 있는 형식 및 이러한 형식이 암시적으로 상속하는 형식 범주가 나와 있습니다. 각 기본 형식은 암시적으로 파생된 형식에 대한 상속을 통해 다른 멤버 집합을 사용할 수 있게 합니다.

| 형식 범주 | 다음에서 암시적으로 상속                                                      |
| ------------- | ----------------------------------------------------------------------------- |
| 클래스         | <xref:System.Object>                                                          |
| struct        | <xref:System.ValueType>, <xref:System.Object>                                 |
| enum          | <xref:System.Enum>, <xref:System.ValueType>, <xref:System.Object>             |
| 대리자(delegate)      | <xref:System.MulticastDelegate>, <xref:System.Delegate>, <xref:System.Object> |

## <a name="inheritance-and-an-is-a-relationship"></a>상속 및 "~이다(is a)" 관계

일반적으로 상속은 기본 클래스와 하나 이상의 파생 클래스 간 "~이다(is a)" 관계를 나타내는 데 사용됩니다. 여기서 파생 클래스는 기본 클래스의 특수화된 버전입니다. 즉, 파생 클래스는 기본 클래스의 한 종류입니다. 예를 들어 `Publication` 클래스는 임의 종류의 출판물을 나타내고 `Book` 및 `Magazine` 클래스는 특정 유형의 출판물을 나타냅니다.

> [!NOTE]
> 클래스 또는 구조체는 하나 이상의 인터페이스를 구현할 수 있습니다. 인터페이스 구현은 종종 단일 상속을 위한 해결 방법 또는 구조체에 상속을 사용하는 방법으로 제공되지만, 인터페이스 및 해당 구현 형식 사이에서 상속과는 다른 관계(“~할 수 있다(can do)” 관계)를 나타내는 데 사용됩니다. 인터페이스는 해당 인터페이스를 구현 형식에서 사용 가능하게 만드는 기능 일부(예: 같은지 테스트하는 기능, 개체를 비교하거나 정렬하는 기능 또는 문화권별 구문 분석 및 서식 지정을 지원하는 기능)를 정의합니다.

"~이다(is a)"는 형식과 해당 형식의 특정 인스턴스화 사이의 관계를 나타내기도 합니다. 다음 예제에서 `Automobile`은 세 가지 고유한 읽기 전용 속성, 즉 자동차의 제조업체인 `Make`, 자동차의 종류인 `Model`, 제조 연도인 `Year`를 갖는 클래스입니다. 또한 `Automobile` 클래스에는 해당 인수가 속성 값에 할당된 생성자가 있으며, <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드를 재정의하여 `Automobile` 클래스가 아닌 `Automobile` 인스턴스를 고유하게 식별하는 문자열을 생성합니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/is-a.cs#1)]

이 경우 특정 자동차 제조업체 및 모델을 나타내기 위해 상속을 사용하지 않아야 합니다. 예를 들어 Packard Motor Car Company에서 제조한 자동차임을 나타내기 위해 `Packard` 형식을 정의할 필요가 없습니다. 대신, 다음 예제와 같이 해당 클래스 생성자에 적절한 값을 사용하여 `Automobile` 개체를 만들어 이러한 속성을 나타낼 수 있습니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/is-a.cs#2)]

상속을 기준으로 하는 ~이다(is a) 관계는 기본 클래스와 기본 클래스에 추가 멤버를 더하거나 기본 클래스에 없는 추가 기능을 필요로 하는 파생 클래스에 가장 잘 적용됩니다.

## <a name="designing-the-base-class-and-derived-classes"></a>기본 클래스 및 파생 클래스 디자인

기본 클래스와 해당 파생 클래스를 디자인하는 프로세스를 살펴보겠습니다. 이 섹션에서는 책, 잡지, 신문, 저널, 기사 등과 같은 모든 종류의 출판물을 나타내는 `Publication` 기본 클래스를 정의합니다. 또한 `Publication` 클래스에서 파생되는 `Book` 클래스도 정의합니다. `Magazine`, `Journal`, `Newspaper` 및 `Article`과 같은 다른 파생 클래스를 정의하도록 예제를 쉽게 확장할 수 있습니다.

### <a name="the-base-publication-class"></a>기본 게시 클래스

`Publication` 클래스를 디자인할 때 결정해야 하는 몇 가지 디자인은 다음과 같습니다.

- 기본 `Publication` 클래스에 포함할 멤버, `Publication` 멤버에서 메서드 구현을 제공하는지 여부 또는 `Publication`이 해당 파생 클래스에 대한 템플릿으로 사용되는 추상 기본 클래스인지 여부

  이 경우 `Publication` 클래스는 메서드 구현을 제공합니다. [추상 기본 클래스 및 파생 클래스 디자인](#abstract) 섹션에는 추상 기본 클래스를 사용하여 파생 클래스가 재정의해야 하는 메서드를 정의하는 예제가 포함되어 있습니다. 파생 클래스는 파생 형식에 적합한 모든 구현을 자유롭게 제공할 수 있습니다.

  코드를 다시 사용하는 기능(즉, 여러 파생 클래스가 기본 클래스 메서드의 선언 및 구현을 공유하며 재정의할 필요가 없음)은 비추상 기본 클래스의 장점입니다. 따라서 일부 또는 대부분의 특수화된 `Publication` 형식에서 해당 코드를 공유할 가능성이 높은 경우 `Publication`에 멤버를 추가해야 합니다. 기본 클래스 구현을 효율적으로 제공하지 못하면 기본 클래스에서 단일 구현이 아니라 파생 클래스에서 거의 동일한 멤버 구현을 제공해야 합니다. 여러 위치에서 중복된 코드를 유지해야 하면 버그가 발생하기 쉬워집니다.

  코드 재사용을 최대화하고 논리적이고 직관적인 상속 계층 구조를 만들려면 모두 또는 대부분의 출판물에 공통되는 데이터 및 기능만 `Publication` 클래스에 포함해야 합니다. 그러면 파생 클래스는 나타내는 특정 종류를 출판물에 고유한 멤버를 구현합니다.

- 클래스 계층 구조 확장 범위. 단순히 하나의 기본 클래스와 하나 이상의 파생 클래스가 아닌 세 개 이상의 클래스로 구성된 계층 구조를 개발하려고 하나요? 예를 들어 `Publication`은 `Magazine`, `Journal` 및 `Newspaper`의 기본 클래스인 `Periodical`의 기본 클래스일 수 있습니다.

  예제에서는 `Publication` 클래스와 `Book` 파생 클래스가 각각 하나씩 구성된 작은 계층 구조를 사용합니다. 이 예제는 쉽게 확장하여 `Publication`에서 파생되는 많은 수의 추가 클래스(예: `Magazine` 및 `Article`)를 만들 수 있습니다.

- 기본 클래스의 인스턴스화가 타당한지 여부. 타당하지 않은 경우 [abstract](../language-reference/keywords/abstract.md) 키워드를 클래스에 적용해야 합니다. 그렇지 않으면 해당 클래스 생성자를 호출하여 `Publication` 클래스를 인스턴스화할 수 있습니다. 클래스 생성자에 대한 직접 호출에 의해 `abstract` 키워드로 표시된 클래스를 인스턴스화하려고 하면 C# 컴파일러는 오류 CS0144, "추상 클래스 또는 인터페이스의 인스턴스를 만들 수 없습니다."를 생성합니다. 리플렉션을 사용하여 클래스를 인스턴스화하려고 하면 리플렉션 메서드가 <xref:System.MemberAccessException> 을 throw합니다.

  기본적으로 기본 클래스는 해당 클래스 생성자를 호출하여 인스턴스화할 수 있습니다. 클래스 생성자를 명시적으로 정의할 필요는 없습니다. 생성자가 기본 클래스의 소스 코드에 없는 경우 C# 컴파일러는 기본(매개 변수 없는) 생성자를 자동으로 제공합니다.

  예를 들어 `Publication` 클래스를 인스턴스화할 수 없도록 [abstract](../language-reference/keywords/abstract.md)로 표시합니다.  `abstract` 메서드가 없는 `abstract` 클래스는 이 클래스가 몇 가지 구체적인 클래스(예: `Book`, `Journal`) 간에 공유되는 추상 개념을 나타낸다는 것을 나타냅니다.

- 파생 클래스에서 특정 멤버의 기본 클래스 구현을 상속해야 하는지 여부, 파생 클래스에 기본 클래스 구현을 재정의할 수 있는 옵션이 있는지 여부 또는 파생 클래스에서 구현을 제공해야 하는지 여부. [abstract](../language-reference/keywords/abstract.md) 키워드를 사용하여 파생 클래스에서 구현을 제공하도록 적용합니다. [virtual](../language-reference/keywords/virtual.md) 키워드를 사용하여 파생 클래스에서 기본 클래스 메서드를 재정의할 수 있도록 허용합니다. 기본적으로 기본 클래스에 정의된 메서드는 재정의 가능하지 *않습니다*.

 `Publication` 클래스에는 `abstract` 메서드가 없지만 클래스 자체는 `abstract`입니다.

- 파생 클래스가 상속 계층 구조의 최종 클래스를 나타내고 자체적으로 추가 파생 클래스에 대한 기본 클래스로 사용될 수 없는지 여부. 기본적으로 모든 클래스는 기본 클래스로 사용될 수 있습니다. [sealed](../language-reference/keywords/sealed.md) 키워드를 적용하여 클래스가 추가 클래스에 대한 기본 클래스로 사용될 수 없음을 나타낼 수 있습니다. 봉인된 클래스로부터 파생하려고 하면 컴파일러 오류 CS0509 "봉인된 형식 \<typeName>에서 파생될 수 없습니다."를 생성했습니다.

  예를 들어 파생 클래스를 `sealed`로 표시합니다.

다음 예제에서는 `Publication` 클래스에 대한 소스 코드와 `Publication.PublicationType` 속성이 반환하는 `PublicationType` 열거형을 보여 줍니다. <xref:System.Object>에서 상속하는 멤버 외에 `Publication` 클래스는 다음과 같은 고유한 멤버 및 멤버 재정의를 정의합니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/base-and-derived.cs#1)]

- 생성자

  `Publication` 클래스는 `abstract`이므로 다음 예제와 같은 코드에서 직접 인스턴스화할 수 없습니다.

  ```csharp
  var publication = new Publication("Tiddlywinks for Experts", "Fun and Games",
                                    PublicationType.Book);
  ```

  그러나 `Book` 클래스에 대한 소스 코드가 나타내는 것처럼 해당 인스턴스 생성자를 파생 클래스 생성자에서 직접 호출할 수 있습니다.

- 출판물과 관련된 두 가지 속성

  `Title`은 `Publication` 생성자를 호출하여 해당 값이 제공되는 읽기 전용 <xref:System.String> 속성입니다.

  `Pages`는 출판물에 포함된 총 페이지 수를 나타내는 읽기/쓰기 <xref:System.Int32> 속성입니다. 값은 `totalPages`라는 private 필드에 저장됩니다. 값은 양수여야 하며 양수가 아니면 <xref:System.ArgumentOutOfRangeException> 이 throw됩니다.

- 출판사 관련 멤버

  두 개의 읽기 전용 속성 `Publisher` 및 `Type`입니다. 해당 값은 원래 `Publication` 클래스 생성자를 호출하여 제공됩니다.

- 출판 관련 멤버

  두 가지 메서드 `Publish` 및 `GetPublicationDate`가 출판일을 설정하고 반환합니다. `Publish` 메서드는 호출될 때 private `published` 플래그를 `true`로 설정하고 전달된 날짜를 private `datePublished` 필드에 대한 인수로 할당합니다. `GetPublicationDate` 메서드는 `published` 플래그가 `false`이면 문자열 "NYP"를 반환하고, `true`이면 `datePublished` 필드 값을 반환합니다.

- 저작권 관련 멤버

  `Copyright` 메서드는 저작권 소유자의 이름과 저작권 연도를 인수로 사용한 후 `CopyrightName` 및 `CopyrightDate` 속성에 할당합니다.

- `ToString` 메서드 재정의

  형식이 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드를 재정의하지 않으면 한 인스턴스를 다른 인스턴스와 구분하는 데 별로 도움이 되지 않는 형식의 정규화된 이름을 반환합니다. `Publication` 클래스는 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 을 재정의하여 `Title` 속성의 값을 반환합니다.

다음 그림에서는 기본 `Publication` 클래스와 암시적으로 상속된 해당 <xref:System.Object> 클래스 간의 관계를 보여 줍니다.

![Object 및 Publication 클래스](media/publication-class.jpg)

### <a name="the-book-class"></a>`Book` 클래스

`Book` 클래스는 책을 특수한 출판문 형식으로 나타냅니다. 다음 예제에서는 `Book` 클래스에 대한 소스 코드를 보여 줍니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/base-and-derived.cs#2)]

`Publication`에서 상속하는 멤버 외에 `Book` 클래스는 다음과 같은 고유한 멤버 및 멤버 재정의를 정의합니다.

- 2개의 생성자

  두 `Book` 생성자는 3가지 공용 매개 변수를 공유합니다. 두 *title* 및 *publisher*는 `Publication` 생성자의 매개 변수에 해당합니다. 세 번째는 변경할 수 없는 공용 `Author` 속성에 저장되는 *author*입니다. 한 생성자에는 `ISBN` auto 속성에 저장되는 *isbn* 매개 변수가 포함됩니다.

  첫 번째 생성자는 [this](../language-reference/keywords/this.md) 키워드를 사용하여 다른 생성자를 호출합니다. 생성자 연결(chaining)은 생성자를 정의하는 일반적인 패턴입니다. 가장 많은 수의 매개 변수를 사용하여 생성자를 호출하면 더 적은 수의 매개 변수를 사용하는 생성자가 기본값을 제공합니다.

  두 번째 생성자는 [base](../language-reference/keywords/base.md) 키워드를 사용하여 기본 클래스 생성자에 제목 및 출판사 이름을 전달합니다. 소스 코드에서 기본 클래스 생성자를 명시적으로 호출하지 않으면 C# 컴파일러는 기본 클래스의 기본 생성자 또는 매개 변수 없는 생성자에 대한 호출을 자동으로 제공합니다.

- 읽기 전용 `ISBN` 속성: 고유한 10 또는 13자리 숫자인 `Book` 개체의 국제 표준 도서 번호를 반환합니다. ISBN은 `Book` 생성자 중 하나에 인수로 제공됩니다. ISBN은 컴파일러에서 자동 생성되는 private 지원 필드에 저장됩니다.

- 읽기 전용 `Author` 속성. 저자 이름은 두 `Book` 생성자의 인수로 제공되고 속성에 저장됩니다.

- 두 개의 읽기 전용 가격 관련 속성 `Price` 및 `Currency`. 해당 값은 `SetPrice` 메서드 호출에 인수로 제공됩니다. `Currency` 속성은 세 자리 ISO 통화 기호입니다(예: 미국 달러의 경우 USD). ISO 통화 기호는 <xref:System.Globalization.RegionInfo.ISOCurrencySymbol%2A> 속성에서 검색할 수 있습니다. 이러한 두 속성은 모두 외부적으로 읽기 전용이지만 둘 다 `Book` 클래스의 코드로 설정할 수 있습니다.

- `SetPrice` 메서드는 `Price` 및 `Currency` 속성의 값을 설정합니다. 이러한 값은 동일한 해당 속성으로 반환됩니다.

- `ToString` 메서드(`Publication`에서 상속), <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> 및 <xref:System.Object.GetHashCode%2A> 메서드(<xref:System.Object>에서 상속)에 대해 재정의합니다.

  재정의되지 않으면 <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> 메서드는 참조 같음 여부를 테스트합니다. 즉, 두 개체 변수는 같은 개체를 참조하는 경우 동일한 것으로 간주됩니다. 반면에 `Book` 클래스에서 두 개의 `Book` 개체에 동일한 ISBN이 있는 경우 이 두 개체는 동일해야 합니다.

  <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> 메서드를 재정의할 경우 런타임이 효율적인 검색을 위해 해시된 컬렉션에 항목을 저장하는 데 사용하는 값을 반환하는 <xref:System.Object.GetHashCode%2A> 메서드도 재정의해야 합니다. 해시 코드는 같음 테스트와 일치하는 값을 반환해야 합니다. 두 `Book` 개체의 ISBN 속성이 같으면 `true`를 반환하도록 <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>를 재정의했으므로 `ISBN` 속성에서 반환된 문자열의 <xref:System.String.GetHashCode%2A> 메서드를 호출하여 계산된 해시 코드를 반환합니다.

다음 그림에서는 `Book` 클래스와 해당 기본 클래스인 `Publication` 클래스 간 관계를 보여 줍니다.

![Publication 및 Book 클래스](media/book-class.jpg)

이제 다음 예제와 같이 `Book` 개체를 인스턴스화하고, 고유 멤버 및 상속된 멤버를 모두 호출하고, `Publication` 형식 또는 `Book` 형식의 매개 변수가 필요한 메서드에 인수로 전달할 수 있습니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/use-publication.cs#1)]

## <a name="designing-abstract-base-classes-and-their-derived-classes"></a>추상 기본 클래스 및 파생 클래스 디자인
<a name="abstract"></a>

앞의 예제에서는 파생 클래스에서 코드를 공유할 수 있도록 여러 메서드 구현을 제공하는 기본 클래스를 정의했습니다. 그러나 대부분의 경우 기본 클래스는 구현을 제공할 것으로 예상되지 않습니다. 대신, 기본 클래스는 *추상 메서드*를 선언하는 *추상 클래스*이며, 각 파생 클래스에서 구현해야 하는 멤버를 정의하는 템플릿으로 사용됩니다. 일반적으로 추상 기본 클래스에서 각 파생 형식의 구현은 해당 형식에 고유합니다. 클래스에서 출판물에 공통된 기능의 구현을 제공했지만, `Publication` 개체를 인스턴스화하는 것은 의미가 없으므로 클래스를 abstract 키워드로 표시했습니다.

예를 들어 닫힌 2차원 기하 도형 각각에 2개의 속성, 즉 도형의 내부 크기를 나타내는 area 속성과 도형 가장자리의 거리를 나타내는 perimeter 속성이 포함되어 있습니다. 그러나 이러한 속성이 계산되는 방식은 전적으로 도형에 따라 결정됩니다. 예를 들어 원의 둘레(또는 원주)를 계산하는 공식은 삼각형의 둘레를 계산하는 공식과 다릅니다. `Shape` 클래스는 `abstract` 메서드가 있는 `abstract` 클래스입니다. 이는 파생 클래스에서 동일한 기능을 공유한다고 나타내지만, 이러한 파생 클래스는 해당 기능을 다르게 구현합니다.

다음 예제에서는 두 속성 `Area` 및 `Perimeter`를 정의하는 `Shape`라는 추상 기본 클래스를 정의합니다. 클래스를 [abstract](../language-reference/keywords/abstract.md) 키워드로 표시하는 것 외에도, 각 인스턴스 멤버도 [abstract](../language-reference/keywords/abstract.md) 키워드로 표시됩니다. 이 경우 `Shape` 도 정규화된 이름은 아닌 형식의 이름을 반환하도록 <xref:System.Object.ToString%2A?displayProperty=nameWithType> 메서드를 재정의합니다. 아울러 두 정적 멤버 `GetArea` 및 `GetPerimeter`를 정의합니다. 이러한 정적 멤버는 호출자가 파생 클래스 인스턴스의 면적 및 둘레를 쉽게 검색할 수 있도록 합니다. 파생 클래스의 인스턴스를 이러한 메서드 중 하나에 전달하면 런타임에서 파생 클래스의 메서드 재정의를 호출합니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/shape.cs#1)]

그러면 `Shape`에서 특정 도형을 나타내는 일부 클래스를 파생시킬 수 있습니다. 다음 예제에서는 3개의 클래스인 `Triangle`, `Rectangle` 및 `Circle`을 정의합니다. 각각은 해당 특정 도형에 고유한 수식을 사용하여 면적 및 둘레를 컴퓨팅합니다. 일부 파생 클래스는 나타내는 도형마다 고유한 `Rectangle.Diagonal` 및 `Circle.Diameter`와 같은 속성도 정의합니다.

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/shape.cs#2)]

다음 예제에서는 `Shape`에서 파생된 개체를 사용합니다. 또한 `Shape`에서 파생된 개체의 배열을 인스턴스화하고 반환 `Shape` 속성 값을 래핑하는 `Shape` 클래스의 정적 메서드를 호출합니다. 런타임에서는 파생 형식의 재정의된 속성에서 값을 검색합니다. 또한 이 예제에서는 배열의 각 `Shape` 개체를 해상 파생 형식으로 캐스팅하고, 캐스팅이 성공하면 `Shape`의 해당 특정 하위 클래스 속성을 검색합니다. 

[!code-csharp[Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/shape.cs#3)]

## <a name="see-also"></a>참고 항목

- [클래스 및 개체](../tour-of-csharp/classes-and-objects.md)
- [상속(C# 프로그래밍 가이드)](../programming-guide/classes-and-structs/inheritance.md)
