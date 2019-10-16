---
title: 식 트리 실행
description: 식 트리를 실행 가능한 중간 언어(IL) 명령으로 변환하여 실행하는 방법을 알아봅니다.
ms.date: 06/20/2016
ms.assetid: 109e0ac5-2a9c-48b4-ac68-9b6219cdbccf
ms.openlocfilehash: f6dca5a3965924e8eb6e1c04fe7ffc3c78c7df93
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57201848"
---
# <a name="executing-expression-trees"></a>식 트리 실행

[이전 -- 식 트리를 지원하는 프레임워크 형식](expression-classes.md)

*식 트리*는 일부 코드를 나타내는 데이터 구조입니다.
컴파일되고 실행 가능한 코드가 아닙니다. 식 트리로 표시되는 .NET 코드를 실행하려면 실행 가능한 IL 명령으로 변환해야 합니다.

## <a name="lambda-expressions-to-functions"></a>람다 식을 함수로 변환

모든 LambdaExpression 또는 LambdaExpression에서 파생된 모든 형식을 실행 가능한 IL로 변환할 수 있습니다. 다른 식 형식은 코드로 직접 변환할 수 없습니다. 실제로 이 제한은 거의 효과가 없습니다. 람다 식은 실행 가능한 IL(중간 언어)로 변환하여 실행하려는 식의 유일한 형식입니다. `ConstantExpression`을 직접 실행하는 것의 의미를 생각해 보세요. 유용한 의미가 있나요? `LambdaExpression`이거나 `LambdaExpression`에서 파생된 형식인 모든 식 트리는 IL로 변환할 수 있습니다.
식 형식 `Expression<TDelegate>` 는 .NET Core 라이브러리에서 유일하게 구체적인 예제입니다. 이 형식은 모든 대리자 형식에 매핑되는 식을 나타내는 데 사용됩니다. 이 형식은 대리자 형식에 매핑되므로 .NET에서 식을 검사하고 람다 식의 시그니처와 일치하는 적절한 대리자에 대해 IL을 생성할 수 있습니다. 

대부분의 경우 식과 해당 대리자 간에 간단한 매핑이 만들어집니다. 예를 들어 `Expression<Func<int>>`로 표시되는 식 트리는 `Func<int>` 형식의 대리자로 변환됩니다. 반환 형식 및 인수 목록을 사용하는 람다 식의 경우 람다 식으로 표시된 실행 코드의 대상 형식인 대리자 형식이 있습니다.

`LambdaExpression` 형식에는 식 트리를 실행 코드로 변환하는 데 사용되는 `Compile` 및 `CompileToMethod` 멤버가 포함됩니다. `Compile` 메서드는 대리자를 만듭니다. `CompileToMethod` 메서드는 식 트리의 컴파일된 출력을 나타내는 IL로 `MethodBuilder` 개체를 업데이트합니다. `CompileToMethod`는 .NET Core가 아니라 전체 데스크톱 프레임워크에서 사용할 수 있습니다.

필요에 따라 생성된 대리자 개체에 대한 기호 디버깅 정보를 수신하는 `DebugInfoGenerator`를 제공할 수도 있습니다. 그러면 식 트리를 대리자 개체로 변환하고 생성된 대리자에 대한 전체 디버깅 정보를 받을 수 있습니다.

다음 코드를 사용하여 식을 대리자로 변환합니다.

```csharp
Expression<Func<int>> add = () => 1 + 2;
var func = add.Compile(); // Create Delegate
var answer = func(); // Invoke Delegate
Console.WriteLine(answer);
```

대리자 형식은 식 형식을 기반으로 합니다. 강력한 형식의 방식으로 대리자 개체를 사용하려면 반환 형식 및 인수 목록을 알고 있어야 합니다. `LambdaExpression.Compile()` 메서드는 `Delegate` 형식을 반환합니다. 컴파일 시간 도구에서 인수 목록 또는 반환 형식을 확인할 수 있도록 하려면 올바른 대리자 형식으로 캐스팅해야 합니다.

## <a name="execution-and-lifetimes"></a>실행 및 수명

`LambdaExpression.Compile()`을 호출할 때 만든 대리자를 호출하여 코드를 실행합니다. 위의 `add.Compile()`이 대리자를 반환하는 위치에서 이를 확인할 수 있습니다. 해당 대리자를 호출하고 `func()`를 호출하면 코드가 실행됩니다.

이 대리자는 식 트리의 코드를 나타냅니다. 해당 대리자에 대한 핸들을 유지하고 나중에 호출할 수 있습니다. 식 트리가 나타내는 코드를 실행할 때마다 식 트리를 컴파일할 필요는 없습니다. 식 트리는 변경할 수 없으며 나중에 동일한 식 트리를 컴파일하면 동일한 코드를 실행하는 대리자가 만들어집니다.

필요 없는 컴파일 호출을 방지하여 성능을 향상시키려면 보다 정교한 캐싱 메커니즘을 만들려고 해야 합니다. 임의의 식 트리 두 개를 비교하여 동일한 알고리즘을 나타내는지 확인하는 경우에도 실행하는 데 시간이 오래 걸릴 수 있습니다. `LambdaExpression.Compile()`의 추가 호출을 방지하여 절약한 계산 시간이 동일한 실행 코드에서 서로 다른 두 식 트리 결과를 확인하는 코드 실행 시간을 초과할 수 있습니다.

## <a name="caveats"></a>주의 사항

람다 식을 대리자로 컴파일하고 해당 대리자를 호출하는 것은 식 트리로 수행할 수 있는 가장 간단한 작업 중 하나입니다. 그러나 이 간단한 작업에서도 주의해야 할 사항이 있습니다. 

람다 식은 식에서 참조되는 모든 지역 변수에 대해 클로저를 만듭니다. 대리자의 일부가 되는 모든 변수는 `Compile`을 호출하는 위치 및 결과 대리자를 실행할 때 사용할 수 있도록 보장해야 합니다.

일반적으로 컴파일러는 이렇게 되도록 합니다. 그러나 식이 `IDisposable`을 구현하는 변수에 액세스하는 경우 코드는 식 트리에서 보유한 개체를 삭제할 수 있습니다.

예를 들어 다음 코드는 `int`가 `IDisposable`을 구현하지 않기 때문에 제대로 작동합니다.

```csharp
private static Func<int, int> CreateBoundFunc()
{
    var constant = 5; // constant is captured by the expression tree
    Expression<Func<int, int>> expression = (b) => constant + b;
    var rVal = expression.Compile();
    return rVal;
}
```

대리자가 지역 변수 `constant`에 대한 참조를 캡처했습니다.
해당 변수는 나중에 `CreateBoundFunc`에서 반환한 함수가 실행될 때 언제든지 액세스할 수 있습니다.

그러나 `IDisposable`을 구현하는 다음(다소 인위적임) 클래스를 살펴보세요.

```csharp
public class Resource : IDisposable
{
    private bool isDisposed = false;
    public int Argument
    {
        get
        {
            if (!isDisposed)
                return 5;
            else throw new ObjectDisposedException("Resource");
        }
    }

    public void Dispose()
    {
        isDisposed = true;
    }
}
```

아래와 같이 식에서 사용하는 경우 `Resource.Argument` 속성에서 참조하는 코드를 실행하면 `ObjectDisposedException`이 표시됩니다.

```csharp
private static Func<int, int> CreateBoundResource()
{
    using (var constant = new Resource()) // constant is captured by the expression tree
    {
        Expression<Func<int, int>> expression = (b) => constant.Argument + b;
        var rVal = expression.Compile();
        return rVal;
    }
}
```

이 메서드에서 반환된 대리자는 `constant`를 통해 닫히고 삭제되었습니다. 이 대리자는 `using` 문에서 선언되었기 때문에 삭제되었습니다. 

이제 이 메서드에서 반환된 대리자를 실행하면 실행 시점에 `ObjectDisposedException`이 throw됩니다.

컴파일 시간 구문을 나타내는 런타임 오류가 발생하면 이상하게 보일 수 있지만 식 트리를 사용하면 이런 환경이 시작됩니다.

이 문제에는 많은 순열이 있으므로 이 문제를 방지하는 일반적인 지침을 제공하기가 어렵습니다. 식을 정의하는 경우 지역 변수에 액세스할 때 주의해야 하며 공용 API에서 반환할 수 있는 식 트리를 만드는 경우 현재 개체(`this`로 표시됨)의 상태에 액세스할 때도 주의해야 합니다.

식의 코드는 다른 어셈블리의 메서드나 속성을 참조할 수 있습니다. 해당 어셈블리는 식을 정의할 때, 식을 컴파일할 때 및 결과 대리자를 호출할 때 액세스할 수 있어야 합니다. 어셈블리가 없는 경우 `ReferencedAssemblyNotFoundException`이 발생하게 됩니다.

## <a name="summary"></a>요약

람다 식을 나타내는 식 트리를 컴파일하면 실행할 수 있는 대리자를 만들 수 있습니다. 그러면 식 트리로 표시되는 코드를 실행하는 메커니즘이 제공됩니다.

식 트리는 생성되는 특정 구문에 대해 실행되는 코드를 나타냅니다. 코드를 컴파일하고 실행하는 환경이 식을 만드는 환경과 일치하는 경우 모든 작업이 예상대로 작동합니다. 그렇지 않을 경우 오류를 예측할 수 있으며 식 트리를 사용하여 코드를 처음 테스트할 때 catch됩니다.

[다음 -- 식 해석](expression-trees-interpreting.md)
