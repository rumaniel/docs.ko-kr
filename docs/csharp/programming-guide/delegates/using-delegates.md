---
title: 대리자 사용 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [C#], how to use
ms.assetid: 99a2fc27-a32e-4a34-921c-e65497520eec
ms.openlocfilehash: f7ee014150a01fe0010048101576f2fece360146
ms.sourcegitcommit: 10db6551ea3c971470cf5d2cc21ba1cbcefe5c55
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72031871"
---
# <a name="using-delegates-c-programming-guide"></a>대리자 사용(C# 프로그래밍 가이드)

[대리자](../../language-reference/keywords/delegate.md)는 C 및 C++의 함수 포인터처럼 메서드를 안전하게 캡슐화하는 형식입니다. 함수 포인터와는 달리 대리자는 개체 지향적이고 형식이 안전하며 보안이 유지됩니다. 대리자의 형식은 대리자의 이름으로 정의됩니다. 다음 예제에서는 [string](../../language-reference/keywords/string.md)을 인수로 사용하고 [void](../../language-reference/keywords/void.md)를 반환하는 메서드를 캡슐화할 수 있는 `Del` 대리자를 선언합니다.

[!code-csharp[csProgGuideDelegates#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#21)]

대리자 개체는 일반적으로 대리자가 래핑할 메서드의 이름을 제공하거나 [익명 함수](../statements-expressions-operators/anonymous-functions.md)를 사용하여 생성합니다. 대리자를 인스턴스화하고 나면 대리자에 대한 메서드 호출이 대리자에 의해 해당 메서드로 전달됩니다. 호출자가 대리자에게 전달한 매개 변수가 메서드로 전달되며 메서드의 반환 값(있는 경우)이 대리자에 의해 호출자로 반환됩니다. 이 과정을 대리자 호출이라고 합니다. 인스턴스화된 대리자는 래핑된 메서드 자체인 것처럼 호출할 수 있습니다. 예:

[!code-csharp[csProgGuideDelegates#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#22)]  

[!code-csharp[csProgGuideDelegates#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#23)]

대리자 형식은 .NET Framework의 <xref:System.Delegate> 클래스에서 파생되며, [봉인](../../language-reference/keywords/sealed.md)되어 있으므로 <xref:System.Delegate>에서는 파생될 수 없으며 해당 클래스에서 사용자 지정 클래스를 파생할 수도 없습니다. 인스턴스화된 대리자는 개체이므로 매개 변수로 전달하거나 속성에 할당할 수 있습니다. 따라서 메서드가 대리자를 매개 변수로 허용하고 나중에 대리자를 호출할 수 있습니다. 비동기 콜백이라는 이러한 방식은 긴 프로세스 완료 시 호출자에게 알림을 제공하는 일반적인 방법입니다. 이러한 방식으로 대리자를 사용하면 대리자를 사용하는 코드가 사용 중인 메서드의 구현을 확인하지 않아도 됩니다. 이 기능은 캡슐화 인터페이스에서 제공하는 기능과 비슷합니다.

콜백은 사용자 지정 비교 메서드를 정의하고 해당 대리자를 정렬 메서드로 전달할 때도 일반적으로 사용됩니다. 이 경우 호출자의 코드를 정렬 알고리즘의 일부분으로 포함할 수 있습니다. 다음 예제 메서드는 `Del` 형식을 매개 변수로 사용합니다.

[!code-csharp[csProgGuideDelegates#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#24)]

위에서 작성된 대리자를 해당 메서드로 전달할 수 있습니다.

[!code-csharp[csProgGuideDelegates#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#25)]

그러면 콘솔에 다음 출력이 표시됩니다.

```console
The number is: 3
```

대리자를 추상화로 사용하는 경우 `MethodWithCallback`이 콘솔을 직접 호출할 필요가 없으며 콘솔을 호출하기 위해 이 메서드를 지정하지 않아도 됩니다. `MethodWithCallback`은 단순히 문자열을 준비하여 다른 메서드로 전달할 뿐입니다. 위임된 메서드는 매개 변수를 필요한 수만큼 사용할 수 있으므로 이러한 방식은 특히 유용합니다.

인스턴스 메서드를 래핑하기 위한 대리자를 생성할 때 해당 대리자는 인스턴스와 메서드를 모두 참조합니다. 대리자는 래핑 대상 메서드 이외의 인스턴스 형식은 알 수 없으므로 해당 개체에 대리자 서명과 일치하는 메서드가 있으면 모든 개체 형식을 참조할 수 있습니다. 정적 메서드를 래핑하기 위해 생성하는 대리자는 메서드만 참조합니다. 다음의 선언을 살펴보세요.

[!code-csharp[csProgGuideDelegates#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#26)]

이제는 위에 나와 있는 정적 `DelegateMethod`와 함께 3개 메서드를 `Del` 인스턴스로 래핑할 수 있습니다.

대리자는 호출 시 둘 이상의 메서드를 호출할 수 있습니다. 이러한 호출을 멀티캐스트라고 합니다. 대리자의 메서드 목록(호출 목록)에 메서드를 더 추가하려는 경우 더하기 또는 더하기 대입 연산자('+' 또는 '+=')를 사용하여 대리자만 두 개 더 추가하면 됩니다. 예:

[!code-csharp[csProgGuideDelegates#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#27)]

이 시점에서 `allMethodsDelegate`의 호출 목록에는 `Method1`, `Method2`, `DelegateMethod`의 3개 메서드가 포함되어 있습니다. 원래 대리자 3개(`d1`, `d2`, `d3`)는 그대로 유지됩니다. `allMethodsDelegate`를 호출하면 3개 메서드가 모두 순서대로 호출됩니다. 대리자가 참조 매개 변수를 사용하는 경우 참조는 각 3개 메서드에 순서대로 전달되며 메서드 하나의 변경 내용은 다음 메서드에도 표시됩니다. 메서드 중 하나라도 메서드 내에서 catch되지 않은 예외를 throw하면 해당 예외가 대리자의 호출자에게 해당 예외가 전달되며 호출 목록의 후속 메서드는 호출되지 않습니다. 반환 값 및/또는 out 매개 변수를 포함하는 대리자는 마지막으로 호출한 메서드의 반환 값과 매개 변수를 반환합니다. 호출 목록에서 메서드를 제거하려면 [빼기 또는 빼기 대입 연산자](../../language-reference/operators/subtraction-operator.md)(`-` 또는 `-=`)를 사용합니다. 예:

[!code-csharp[csProgGuideDelegates#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#28)]

대리자 형식은 `System.Delegate`에서 파생되므로 해당 클래스로 정의되는 메서드와 속성을 대리자에서 호출할 수 있습니다. 예를 들어 대리자의 호출 목록에 있는 메서드 수를 확인하려는 경우 다음과 같이 코드를 작성하면 됩니다.

[!code-csharp[csProgGuideDelegates#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#29)]

호출 목록에 메서드가 둘 이상 포함된 대리자는 <xref:System.MulticastDelegate>의 하위 클래스인 `System.Delegate`에서 파생됩니다. 두 클래스가 모두 `GetInvocationList`를 지원하므로 위의 코드는 두 경우에 모두 사용 가능합니다.

멀티캐스트 대리자는 이벤트 처리에서 광범위하게 사용됩니다. 이벤트 소스 개체는 해당 이벤트를 받도록 등록된 받는 사람 개체에 이벤트 알림을 보냅니다. 이벤트를 등록하기 위해 받는 사람은 이벤트를 처리하도록 설계된 메서드를 만든 다음 해당 메서드의 대리자를 만들어 이벤트 소스로 전달합니다. 소스는 이벤트 발생 시 대리자를 호출합니다. 그러면 대리자가 받는 사람에 대해 이벤트 처리 메서드를 호출하여 이벤트 데이터를 전달합니다. 지정된 이벤트의 대리자 형식은 이벤트 소스에 의해 정의됩니다. 자세한 내용은 [이벤트](../events/index.md)를 참조하세요.

컴파일 시간에 할당된 서로 다른 형식의 두 대리자를 비교하면 컴파일 오류가 발생합니다. 대리자 인스턴스가 정적 `System.Delegate` 형식이면 비교는 허용되지만 런타임에서 false가 반환됩니다. 예:

[!code-csharp[csProgGuideDelegates#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#30)]

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [대리자](./index.md)
- [대리자의 가변성 사용](../concepts/covariance-contravariance/using-variance-in-delegates.md)
- [대리자의 가변성](../concepts/covariance-contravariance/variance-in-delegates.md)
- [Func 및 Action 제네릭 대리자에 가변성 사용](../concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
- [이벤트](../events/index.md)
