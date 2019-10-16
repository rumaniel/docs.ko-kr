---
title: 로컬 함수 및 람다 식
description: 로컬 함수가 람다 식보다 더 적합한 선택일 수 있는 이유를 알아봅니다.
ms.date: 06/27/2016
ms.assetid: 368d1752-3659-489a-97b4-f15d87e49ae3
ms.openlocfilehash: 7577950314f8c57fba635db8b2bcd69e8d427dc3
ms.sourcegitcommit: 438919211260bb415fc8f96ca3eabc33cf2d681d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2019
ms.locfileid: "59611447"
---
# <a name="local-functions-compared-to-lambda-expressions"></a>로컬 함수 및 람다 식 비교

얼핏 보기에 [로컬 함수](programming-guide/classes-and-structs/local-functions.md)와 [람다 식](./programming-guide/statements-expressions-operators/lambda-expressions.md)은 매우 유사합니다. 대부분의 경우 람다 식과 로컬 함수 사용 간 선택은 스타일 및 개인 기본 설정의 문제입니다. 그러나 하나 또는 다른 것을 사용할 수 있는 것에 알고 있어야 하는 실제 차이점이 있습니다.

계승 알고리즘의 로컬 함수 및 람다 식 구현 간의 차이점을 살펴보겠습니다. 먼저 로컬 함수를 사용하는 버전은 다음과 같습니다.

[!code-csharp[LocalFunctionFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#37_LocalFunctionFactorial "Recursive factorial using local function")]

람다 식을 사용하는 버전과 해당 구현을 비교해 보세요.

[!code-csharp[26_LambdaFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#38_LambdaFactorial "Recursive factorial using lambda expressions")]

로컬 함수에는 이름이 있습니다. 람다 식은 `Func` 또는 `Action` 형식인 변수에 할당된 무명 메서드입니다. 로컬 함수를 선언하는 경우 인수 형식 및 반환 형식은 함수 선언의 일부입니다. 람다 식 본문에 포함되는 대신 인수 형식 및 반환 형식은 람다 식의 변수 형식 선언의 일부입니다. 이러한 두 가지 차이점은 코드를 더 명확하게 할 수 있습니다.

로컬 함수는 람다 식보다 한정된 할당에 대한 다양한 규칙을 갖고 있습니다. 로컬 함수 선언은 범위에 있는 모든 코드 위치에서 참조될 수 있습니다. 람다 식을 액세스하려면 대리자 변수에 할당해야 합니다(또는 람다 식을 참조하는 대리자를 통해 호출). 람다 식을 사용하는 버전은 람다 식 `nthFactorial`을 정의하기 전에 선언하고 초기화해야 합니다. 이렇게 하지 않으면 `nthFactorial`을 할당하기 전에 참조하여 컴파일 시간 오류가 발생합니다.
이러한 차이점은 로컬 함수를 사용하여 재귀 알고리즘을 쉽게 만들 수 있음을 의미합니다. 자신을 호출하는 로컬 함수를 선언하고 정의할 수 있습니다. 람다 식을 동일한 람다 식을 참조하는 본문에 다시 할당하려면 선언하고, 기본 값을 할당해야 합니다.

한정된 할당 규칙은 로컬 함수 또는 람다 식에서 캡처되는 변수에도 영향을 줍니다. 로컬 함수와 람다 식 규칙 모두는 로컬 함수 또는 람다 식이 대리자로 변환되는 시점에 캡처된 변수를 한정적으로 할당해야 합니다. 차이점은 선언될 때 람다 식이 대리자로 변환된다는 점입니다. 로컬 함수는 대리자로 사용되는 경우에만 대리자로 변환됩니다. 로컬 함수를 선언하고 메서드처럼 호출하여 참조하는 경우 대리자로 변환되지 않습니다. 해당 규칙을 통해 포함된 범위 내의 모든 편리한 위치에서 로컬 함수를 선언할 수 있습니다. 모든 return 문 뒤의 부모 메서드 끝에 로컬 함수를 선언하는 것은 일반적입니다.

세 번째, 컴파일러는 로컬 함수가 포함된 범위에서 캡처된 변수를 한정적으로 할당할 수 있도록 하는 정적 분석을 수행할 수 있습니다. 다음 예제를 고려해 보세요.

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

컴파일러는 `LocalFunction`에서 호출될 때 `y`를 한정적으로 할당하는지 확인할 수 있습니다. `LocalFunction`은 `return` 문 전에 호출되므로 `y`는 `return` 문에서 한정적으로 할당됩니다.

예제 분석을 활성화하는 분석은 네 번째 차이점을 활성화합니다.
해당 용도에 따라 로컬 함수는 람다 식에 항상 필요한 힙 할당을 피할 수 있습니다. 로컬 함수가 대리자로 변환되지 않고 로컬 함수에 의해 캡처된 변수가 대리자로 변환된 다른 람다 식 또는 로컬 함수에 의해 캡처되지 않는 경우 컴파일러는 힙 할당을 피할 수 있습니다. 

다음 비동기 예제를 살펴보세요.

[!code-csharp[TaskLambdaExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#36_TaskLambdaExample "Task returning method with lambda expression")]

이 람다 식의 클로저에는 `address`, `index` 및 `name` 변수가 포함됩니다. 로컬 함수의 경우 클로저를 구현하는 개체는 `struct` 형식일 수 있습니다. 해당 구조체 형식은 로컬 함수에 참조로 전달됩니다. 구현에서 이러한 차이점은 할당에 저장됩니다.

람다 식에 필요한 인스턴스화는 추가 메모리 할당을 의미하며, 시간이 중요한 코드 경로에서 성능에 영향을 줄 수 있습니다.
로컬 함수는 이러한 오버헤드를 유발하지 않습니다. 위의 예제에서 로컬 함수 버전은 람다 식 버전보다 할당 수가 2개 더 적습니다.

> [!NOTE]
> 이 메서드에 해당하는 로컬 함수는 클로저에 클래스도 사용합니다. 로컬 함수의 클로저가 `class` 또는 `struct`로 구현되는지 여부는 구현 세부 정보입니다. 로컬 함수는 `struct`를 사용할 수 있는 반면, 람다는 항상 `class`를 사용합니다.

[!code-csharp[TaskLocalFunctionExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#TaskExample "Task returning method with local function")]

이 샘플에서 설명하지 않은 한 가지 최종 장점은 `yield return` 구문을 사용해서 로컬 함수를 반복기로 구현하여 값 시퀀스를 생성할 수 있다는 것입니다. `yield return` 문은 람다 식에 허용되지 않습니다.

로컬 함수는 람다 식과 중복되는 것처럼 보일 수도 있지만, 실제로 다른 용도로 다르게 사용됩니다.
로컬 함수는 다른 메서드의 컨텍스트에서만 호출되는 함수를 작성하려는 경우에 더 효율적입니다.
