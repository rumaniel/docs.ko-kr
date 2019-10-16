---
title: 단위 테스트 작성에 대한 모범 사례
description: .NET Core 및 .NET 표준 프로젝트에 대한 코드 품질 및 탄력성을 구동하는 단위 테스트 작성에 대한 모범 사례를 알아봅니다.
author: jpreese
ms.author: wiwagn
ms.date: 07/28/2018
ms.custom: seodec18
ms.openlocfilehash: afd6e7e25573cbb571b225c263b9bcfccfca5647
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926381"
---
# <a name="unit-testing-best-practices-with-net-core-and-net-standard"></a>.NET Core 및.NET 표준을 사용하는 단위 테스트 모범 사례

단위 테스트 작성에는 회귀를 돕고, 문서를 제공하고, 좋은 디자인을 용이하게 하는 등에 다양한 혜택이 있습니다. 그러나 읽기 어렵고 불안정한 단위 테스트는 코드 기반을 파괴할 수 있습니다. 이 문서에서는.NET Core 및 .NET 표준 프로젝트용 단위 테스트 디자인과 관련된 몇 가지 모범 사례를 설명합니다.

이 가이드에서는 단위 테스트를 작성할 때 테스트를 탄력적이고 이해하기 쉽게 유지하기 위한 몇 가지 모범 사례를 알아봅니다.

[John Reese](https://reese.dev), [Roy Osherove](https://osherove.com/)에 대한 특별한 감사

## <a name="why-unit-test"></a>단위 테스트하는 이유는?

### <a name="less-time-performing-functional-tests"></a>기능 테스트 수행 시간 단축
기능 테스트는 비용이 많이 듭니다. 일반적으로 애플리케이션을 열고 사용자(또는 다른 사용자)가 예상되는 동작의 유효성을 검사하기 위해 따라야 하는 일련의 단계 수행이 포함됩니다. 이러한 단계는 항상 테스터에게 알려진 것은 아니며, 이는 테스트를 수행하기 위해 해당 영역에 더 많은 지식을 갖추어야 함을 의미합니다. 테스트 자체는 사소한 변경인 경우에는 몇 초가 걸리거나 큰 변경의 경우에는 몇 분 정도 걸릴 수 있습니다. 마지막으로, 이 프로세스는 시스템에서 수행하는 모든 변경 사항에 대해 반복되어야 합니다.

반면에 단위 테스트는 밀리초가 소요되며, 단추를 눌러 실행할 수 있으며 시스템 전체에 대한 지식이 반드시 필요하지는 않습니다. 테스트 통과 또는 실패 여부는 개인이 아닌 test runner의 몫입니다.

### <a name="protection-against-regression"></a>회귀에 대한 보호
회귀 오류는 애플리케이션이 변경될 때 도입된 결함입니다. 테스터는 새 기능을 테스트할 뿐만 아니라 이전에 구현된 기능이 여전히 예상대로 작동하는지 확인하기 위해 이전에 존재했던 기능도 테스트하는 것이 일반적입니다.

단위 테스트를 사용하면 모든 빌드 후에 또는 코드 줄을 변경한 후에도 전체 테스트 도구 모음을 다시 실행할 수 있습니다. 새 코드가 기존 기능을 중단시키지 않는다는 신뢰를 줍니다.

### <a name="executable-documentation"></a>실행 가능한 설명서
특정 메서드가 무엇을 하는지 또는 특정 입력이 지정된 동작이 어떻게 수행되는지 항상 명확하지는 않을 수 있습니다. 빈 문자열을 전달하면 이 메서드는 어떻게 작동하는가를 자문해 볼 수 있습니다. Null?

이름이 잘 지정된 단위 테스트의 도구 모음이 있는 경우 각 테스트는 지정된 입력에 대해 예상되는 출력을 명확하게 설명할 수 있어야 합니다. 또한 실제로 작동하는지 확인할 수 있어야 합니다.

### <a name="less-coupled-code"></a>적은 결합 코드
코드가 밀접하게 결합되면 단위 테스트하기가 어려울 수 있습니다. 작성 중인 코드에 대한 단위 테스트를 만들지 않으면 결합이 덜 분명해질 수 있습니다.

코드 테스트를 작성하면 자연스럽게 분리됩니다. 그렇지 않으면 테스트하기가 더 어려워지기 때문입니다.

## <a name="characteristics-of-a-good-unit-test"></a>좋은 단위 테스트의 특징

- **Fast**. 완성도 높은 프로젝트에서 수천 개의 단위 테스트를 수행하는 것은 드문 일이 아닙니다. 단위 테스트는 실행하는 데 시간이 거의 걸리지 않습니다. 밀리초.
- **Isolated**. 독립형 단위 테스트는 독립적으로 실행될 수 있으며, 파일 시스템 또는 데이터베이스와 같은 외부 요인에 종속되지 않습니다.
- **반복 가능**. 단위 테스트를 실행하는 것은 해당 결과와 일치해야 합니다. 즉, 실행 사이에 아무 것도 변경하지 않으면 항상 동일한 결과를 반환합니다.
- **자체 검사**. 테스트는 사람의 개입 없이 통과했는지 여부를 자동으로 검색할 수 있어야 합니다.
- **Timely**. 단위 테스트는 테스트 중인 코드에 비해 작성하는 데 불균형적으로 긴 시간이 걸리지 않아야 합니다. 코드를 작성하는 데 비해 많은 시간이 걸리는 코드를 테스트하는 경우 더 많은 테스트가 가능한 디자인을 고려해 보세요.

## <a name="lets-speak-the-same-language"></a>동일한 언어 사용
*mock*이라는 용어는 불행히도 테스트에 대해 이야기할 때 잘못 사용됩니다. 다음은 단위 테스트를 작성할 때 *fakes*의 가장 일반적인 유형을 정의합니다.

*Fake* - fake는 stub 또는 mock 개체를 설명하는 데 사용할 수 있는 일반적인 용어입니다. stub 또는 mock인지 여부는 사용되는 컨텍스트에 따라 달라집니다. 즉, fake는 stub 또는 mock이 될 수 있습니다.

*Mock* - mock 개체는 단위 테스트가 통과되었는지 여부를 결정하는 시스템에서 fake 개체입니다. mock은 어설션될 때까지 Fake로 시작합니다.

*Stub* - stub은 시스템의 기존 종속성(또는 협력자)을 제어할 수 있는 대체품입니다. stub을 사용하여 종속성을 직접 처리하지 않고 코드를 테스트할 수 있습니다. 기본적으로 fake는 stub으로 시작합니다.

다음 코드 조각을 살펴봅니다.

```csharp
var mockOrder = new MockOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

이는 stub이 mock이라고 불리는 예입니다. 이 경우 stub입니다. `Purchase`(테스트 중인 시스템)를 인스턴스화할 수 있는 수단으로 Order를 전달합니다. `MockOrder` 이름도 매우 잘못된 것입니다. 다시 말해서, 순서가 mock이 아니기 때문입니다.

더 나은 방법은

```csharp
var stubOrder = new FakeOrder();
var purchase = new Purchase(stubOrder);

purchase.ValidateOrders();

Assert.True(purchase.CanBeShipped);
```

클래스 이름을 `FakeOrder`로 바꾸면 클래스를 훨씬 더 일반화되게 만들므로 클래스를 mock 또는 stub으로 사용할 수 있습니다. 어느 것이든 테스트 사례에 좋습니다. 위의 예에서는 `FakeOrder`가 stub으로 사용됩니다. assert 중에 `FakeOrder`를 어떤 모양 또는 형태로 사용하지 않습니다. `FakeOrder`는 방금 `Purchase` 클래스에 전달되어 생성자의 요구 사항을 충족했습니다.

Mock으로 사용하려면 다음과 같이 수행하면 됩니다.

```csharp
var mockOrder = new FakeOrder();
var purchase = new Purchase(mockOrder);

purchase.ValidateOrders();

Assert.True(mockOrder.Validated);
```

이 경우 Fake(해당 항목에 대한 어설션)의 속성을 확인 중이므로 위의 코드 조각에서 `mockOrder`는 Mock입니다.

> [!IMPORTANT]
> 이 용어를 올바르게 사용하는 것이 중요합니다. stubs를 "mocks"라고 부른다면 다른 개발자는 의도에 대해 잘못된 가정을 하게 될 것입니다.

mocks와 stubs에 대해 기억해야 할 주요 사항은 mocks는 stubs와 같지만, mock 개체에 대해 어설션하는 반면 stub에 대해서는 어설션하지 않습니다.

## <a name="best-practices"></a>최선의 구현 방법

### <a name="naming-your-tests"></a>테스트 이름 지정
테스트의 이름은 다음 세 부분으로 구성되어야 합니다.

- 테스트할 메서드의 이름입니다.
- 테스트 중인 시나리오입니다.
- 시나리오에서 호출될 때 예상되는 동작입니다.

#### <a name="why"></a>이유

- 이름 지정 표준은 테스트의 의도를 명시적으로 표현하기 때문에 중요합니다.

테스트는 단순히 코드가 작동하는지 확인하는 것 이상이며, 문서도 제공합니다. 단위 테스트 도구 모음을 살펴봄으로써 코드 자체를 조회하지 않고도 코드의 동작을 유추할 수 있습니다. 또한 테스트가 실패하는 경우 기대치를 충족하지 못하는 시나리오를 정확히 확인할 수 있습니다.

#### <a name="bad"></a>Bad:
[!code-csharp[BeforeNaming](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeNaming)]

#### <a name="better"></a>Better:
[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="arranging-your-tests"></a>테스트 정렬
**정렬, 동작, 어설션**은 단위 테스트 시 일반적인 패턴입니다. 이름에서 알 수 있듯이 세 가지 주요 작업으로 구성됩니다.

- 개체를 *정렬*하고 필요에 따라 만들고 설정합니다.
- 개체의 *동작*입니다.
- 특정 항목이 예상대로라고 *assert*합니다.

#### <a name="why"></a>이유

- 테스트할 항목을 *정렬* 및 *assert* 단계에서 명확하게 구분합니다.
- 어설션과 "Act" 코드를 혼합할 기회가 적습니다.

가독성은 테스트를 작성할 때 가장 중요한 측면 중 하나입니다. 테스트 내에서 이러한 작업을 각각 구분하면 코드를 호출하는 데 필요한 종속성, 코드 호출 방법 및 어설션하려는 대상이 명확하게 강조 표시할 수 있습니다. 몇 가지 단계를 결합하여 테스트의 크기를 줄일 수 있지만, 기본적인 목표는 가능한 한 테스트를 최대한으로 읽을 수 있도록 하는 것입니다.

#### <a name="bad"></a>Bad:
[!code-csharp[BeforeArranging](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeArranging)]

#### <a name="better"></a>Better:
[!code-csharp[AfterArranging](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterArranging)]

### <a name="write-minimally-passing-tests"></a>최소한의 테스트 통과 작성
단위 테스트에 사용할 입력은 현재 테스트 중인 동작을 확인하기 위해 가능한 한 가장 간단해야 합니다.

#### <a name="why"></a>이유

- 테스트는 코드베이스의 향후 변화에 대한 복원력이 향상됩니다.
- 구현에 대한 테스트 동작에 근접합니다.

테스트를 통과하는 데 필요한 것보다 많은 정보를 포함하는 테스트는 테스트에 오류가 발생할 가능성이 높으며 테스트의 의도를 덜 명확하게 할 수 있습니다. 테스트를 작성할 때 동작에 집중하려고 합니다. 모델의 추가 속성을 설정하거나 필요하지 않을 때 0이 아닌 값을 사용하면 증명하려고 시도한 것만 손상됩니다.

#### <a name="bad"></a>Bad:
[!code-csharp[BeforeMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMinimallyPassing)]

#### <a name="better"></a>Better:
[!code-csharp[AfterNamingAndMinimallyPassing](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterNamingAndMinimallyPassing)]

### <a name="avoid-magic-strings"></a>매직 문자열 방지
단위 테스트의 이름 지정 변수는(프로덕션 코드의 이름 지정 변수보다 더 중요하지는 않지만) 중요합니다. 단위 테스트에는 매직 문자열이 없어야 합니다.

#### <a name="why"></a>이유

- 값을 특별하게 만드는 요인을 파악하기 위해 테스트의 판독기가 프로덕션 코드를 검사할 필요가 없도록 합니다.
- *성취*하려는 것보다는 *증명*하려는 것을 명시적으로 보여 줍니다.

매직 문자열은 테스트 판독기에 혼동을 일으킬 수 있습니다. 문자열이 일반적이지 않은 경우 매개 변수 또는 반환 값에 대해 특정 값이 선택된 이유가 궁금할 수 있습니다. 이를 통해 테스트에 집중하기보다는 구현 세부 사항을 더 자세히 살펴볼 수 있습니다.

> [!TIP] 
> 테스트를 작성할 때는 가능한 한 많은 의도를 표현하는 것을 목표로 해야 합니다. 매직 문자열의 경우 좋은 방법은 이러한 값을 상수에 할당하는 것입니다.

#### <a name="bad"></a>Bad:
[!code-csharp[BeforeMagicString](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMagicString)]

#### <a name="better"></a>Better:
[!code-csharp[AfterMagicString](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterMagicString)]

### <a name="avoid-logic-in-tests"></a>테스트에서 논리 방지
단위 테스트를 작성할 때 수동 문자열 연결 및 `if`, `while`, `for`, `switch` 등의 논리 조건을 방지합니다.

#### <a name="why"></a>이유

- 테스트 중에 버그가 발생할 가능성이 줄어듭니다.
- 구현 세부 정보보다는 최종 결과에 집중합니다.

테스트 도구 모음에 논리를 도입하면 버그가 발생할 가능성이 크게 증가합니다. 버그를 찾고자 하는 마지막 위치는 테스트 도구 모음 내에 있습니다. 테스트 작동에 높은 수준의 확신이 있어야 합니다. 그렇지 않으면 신뢰할 수 없습니다. 신뢰할 수 없는 테스트는 어떤 가치도 제공하지 않습니다. 테스트가 실패하면 코드에 실제로 잘못된 것이 있어서 무시할 수 없다는 것을 느낄 수 있습니다.

> [!TIP]
> 테스트의 논리가 불가피한 경우 테스트를 두 개 이상의 다른 테스트로 분할하는 것이 좋습니다.

#### <a name="bad"></a>Bad:
[!code-csharp[LogicInTests](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#LogicInTests)]

#### <a name="better"></a>Better:
[!code-csharp[AfterTestLogic](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterTestLogic)]

### <a name="prefer-helper-methods-to-setup-and-teardown"></a>설정 및 해제할 도우미 방법 선호
테스트에 비슷한 개체나 상태가 필요한 경우 Setup 및 Teardown 특성이 있는 경우보다 도우미 메서드를 선호합니다.

#### <a name="why"></a>이유

- 모든 코트가 각 테스트 내에서 볼 수 있기 때문에 테스트를 읽을 때 혼동이 적습니다.
- 지정된 테스트에 대해 너무 많거나 너무 적게 설정될 가능성이 줄어듭니다.
- 테스트 간 원치 않는 종속성을 만드는 테스트 간에 상태를 공유할 가능성이 줄어듭니다.

단위 테스트 프레임워크에서 `Setup`은 단위 테스트 도구 모음 내의 각각의 모든 단위 테스트 전에 호출됩니다. 일부는 이를 유용한 도구로 볼 수 있지만, 일반적으로 테스트를 읽기에는 비대해지고 어렵워집니다. 각 테스트는 일반적으로 테스트를 시작하고 실행하기 위한 요구 사항이 다릅니다. 아쉽게도 `Setup`에서는 각 테스트에 대해 정확히 동일한 요구 사항을 사용해야 합니다.

> [!NOTE] 
> xUnit은 버전 2.x에서 SetUp 및 TearDown을 모두 제거했습니다.

#### <a name="bad"></a>Bad:
[!code-csharp[BeforeSetup](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeSetup)]

```csharp
// more tests...
```

[!code-csharp[BeforeHelperMethod](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeHelperMethod)]

#### <a name="better"></a>Better:
[!code-csharp[AfterHelperMethod](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterHelperMethod)]

```csharp
// more tests...
```

[!code-csharp[AfterSetup](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterSetup)]

### <a name="avoid-multiple-asserts"></a>다중 어설션 방지
테스트를 작성할 때 테스트당 하나의 Assert만 포함하려고 합니다. 하나의 어설션만 사용하는 일반적인 방법은 다음과 같습니다.

- 각 어설션에 대한 별도의 테스트를 만듭니다.
- 매개 변수화된 테스트를 사용합니다.

#### <a name="why"></a>이유

- 하나의 Assert가 실패하면 후속 Assert는 평가되지 않습니다.
- 테스트에 여러 사례를 어설션하지 않도록 합니다.
- 테스트가 실패한 이유에 대한 전체 그림을 제공합니다. 

테스트 사례에 다중 어설션을 도입할 때 모든 어설션이 실행된다는 보장은 없습니다. 대부분의 단위 테스트 프레임워크에서 단위 테스트에 어설션이 실패하면 절차 테스트는 자동으로 실패한 것으로 간주됩니다. 실제로 작동하는 기능이 실패한 것으로 표시되므로 혼란스러울 수 있습니다.

> [!NOTE]
> 이 규칙에 대한 일반적인 예외는 개체에 대해 어설션할 때 발생합니다. 이 경우 일반적으로 각 속성에 대해 다중 어설션을 허용하여 개체가 예상되는 상태에 있는지 확인하는 것이 좋습니다.

#### <a name="bad"></a>Bad:
[!code-csharp[BeforeMultipleAsserts](../../../samples/csharp/unit-testing-best-practices/before/StringCalculatorTests.cs#BeforeMultipleAsserts)]

#### <a name="better"></a>Better:
[!code-csharp[AfterMultipleAsserts](../../../samples/csharp/unit-testing-best-practices/after/StringCalculatorTests.cs#AfterMultipleAsserts)]

### <a name="validate-private-methods-by-unit-testing-public-methods"></a>공용 메서드를 테스트하여 전용 메서드 유효성 검사
대부분의 경우 전용 메서드를 테스트할 필요는 없습니다. 전용 메서드는 구현 세부 정보입니다. 전용 메서드는 절대 분리되어 존재하지 않는다고 생각할 수 있습니다. 특정 시점에서는 구현의 일부로 전용 메서드를 호출하는 공용 연결 메서드가 있을 것입니다. 주의해야 할 것은 사적인 것을 호출하는 공용 메서드의 최종 결과입니다. 

다음 경우를 참조

```csharp
public string ParseLogLine(string input)
{
    var sanitizedInput = TrimInput(input);
    return sanitizedInput;
}

private string TrimInput(string input)
{
    return input.Trim();
}
```

첫 번째 반응은 메서드가 예상대로 작동하는지 확인하려고 하기 때문에 `TrimInput`에 대한 테스트를 작성하는 것일 수 있습니다. 그러나 `ParseLogLine`에서 예상하지 못한 방식으로 `sanitizedInput`을 조작하여 쓸모없는 `TrimInput`에 대한 테스트를 렌더링하는 것은 전적으로 가능합니다. 

실제 테스트는 공용 연결 메서드 `ParseLogLine`에 대해 수행되어야 합니다. 이는 최종적으로 주의를 기울여야 하는 것이기 때문이다. 

```csharp
public void ParseLogLine_ByDefault_ReturnsTrimmedResult()
{
    var parser = new Parser();

    var result = parser.ParseLogLine(" a ");

    Assert.Equals("a", result);
}
```

이 관점에서, 전용 메서드를 표시하는 경우 공용 메서드를 찾아 해당 메서드에 대해 테스트를 작성합니다. 단지 전용 메서드가 예상된 결과를 반환한다고 해서 최종적으로 전용 메서드를 호출하는 시스템이 결과를 올바르게 사용하는 것은 아닙니다.

### <a name="stub-static-references"></a>Stub 정적 참조
단위 테스트의 원칙 중 하나는 테스트 중인 시스템을 완전히 제어해야 한다는 것입니다. 프로덕션 코드에 정적 참조(예: `DateTime.Now`)에 대한 호출을 포함하는 경우 문제가 될 수 있습니다. 다음 코드 참조

```csharp
public int GetDiscountedPrice(int price)
{
    if(DateTime.Now.DayOfWeek == DayOfWeek.Tuesday) 
    {
        return price / 2;
    }
    else 
    {
        return price;
    }
}
```

이 코드를 어떻게 단위 테스트할 수 있나요? 다음과 같은 방법을 시도하는 경우

```csharp
public void GetDiscountedPrice_ByDefault_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(2, actual)
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();

    var actual = priceCalculator.GetDiscountedPrice(2);

    Assert.Equals(1, actual);
}
```

아쉽게도 테스트에 몇 가지 문제점이 있습니다. 

- 테스트 도구 모음을 화요일에 실행하면 두 번째 테스트는 통과하지만 첫 번째 테스트는 실패합니다.
- 테스트 도구 모음을 다른 날에 실행하면 첫 번째 테스트는 통과하지만 두 번째 테스트는 실패합니다.

이러한 문제를 해결하려면 프로덕션 코드에 *이음새*를 도입해야 합니다. 한 가지 방법은 인터페이스에서 제어해야 하는 코드를 래핑하여 프로덕션 코드가 해당 인터페이스에 종속되도록 하는 것입니다.

```csharp
public interface IDateTimeProvider
{
    DayOfWeek DayOfWeek();
}

public int GetDiscountedPrice(int price, IDateTimeProvider dateTimeProvider)
{
    if(dateTimeProvider.DayOfWeek() == DayOfWeek.Tuesday) 
    {
        return price / 2;
    }
    else 
    {
        return price;
    }
}
```

이제 테스트 도구 모음이 됩니다.

```csharp
public void GetDiscountedPrice_ByDefault_ReturnsFullPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Monday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(2, actual);
}

public void GetDiscountedPrice_OnTuesday_ReturnsHalfPrice()
{
    var priceCalculator = new PriceCalculator();
    var dateTimeProviderStub = new Mock<IDateTimeProvider>();
    dateTimeProviderStub.Setup(dtp => dtp.DayOfWeek()).Returns(DayOfWeek.Tuesday);

    var actual = priceCalculator.GetDiscountedPrice(2, dateTimeProviderStub);

    Assert.Equals(1, actual);
}
```

이제 테스트 도구 모음은 `DateTime.Now`에 대한 완전한 제어권을 가지며 메서드를 호출할 때 모든 값을 스텁할 수 있습니다.
