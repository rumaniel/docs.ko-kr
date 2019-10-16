---
title: 식 트리를 지원하는 프레임워크 형식
description: 식 트리를 지원하는 프레임워크 형식, 식 트리 만들기, 식 트리 API 작업을 위한 기술에 대해 알아봅니다.
ms.date: 06/20/2016
ms.assetid: e9c85021-0d36-48af-91b7-aaaa66f22654
ms.openlocfilehash: d11a13000019faf2ab5c35d41d48fa199e901d1c
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70925964"
---
# <a name="framework-types-supporting-expression-trees"></a>식 트리를 지원하는 프레임워크 형식

[이전 -- 식 트리 설명](expression-trees-explained.md)

.NET Core 프레임워크에는 식 트리에서 작동하는 클래스 목록이 많습니다.
전체 목록은 <xref:System.Linq.Expressions>에서 확인할 수 있습니다.
전체 목록을 실행하는 대신 프레임워크 클래스가 어떻게 디자인되었는지 살펴보겠습니다.

언어 디자인에서 식이란 값을 계산하고 반환하는 코드의 본문입니다. 식은 매우 간단할 수 있습니다. 상수 식 `1`은 상수 값 1을 반환합니다. 식은 더 복잡할 수 있습니다. `(-B + Math.Sqrt(B*B - 4 * A * C)) / (2 * A)` 식은 2차 방정식의 근을 반환합니다(방정식에 솔루션이 있는 경우).  

## <a name="it-all-starts-with-systemlinqexpression"></a>모두 System.Linq.Expression으로 시작

식 트리 사용의 복잡성 중 하나는 많은 종류의 식이 프로그램의 여러 위치에서 유효하다는 점입니다. 대입 식을 살펴보세요. 대입 식의 오른쪽은 상수 값, 변수, 메서드 호출 식 등이 될 수 있습니다. 해당 언어 유연성은 식 트리를 트래버스할 때 트리 노드의 모든 위치에서 여러 가지 다른 식 형식이 표시될 수 있음을 의미합니다. 따라서 기본 식 형식으로 작업하는 것이 가장 간단합니다. 그러나 더 많은 것을 알아야 하는 경우가 있습니다.
기본 식 클래스에는 `NodeType` 속성이 이러한 용도로 포함되어 있으며,
가능한 식 형식의 열거형인 `ExpressionType`을 반환합니다.
노드의 형식을 알고 있다면 해당 형식으로 캐스트할 수 있으며 식 노드의 형식을 알고 있으면 특정 작업을 수행할 수 있습니다. 특정 노드 유형을 검색한 다음 이러한 식의 특정 속성을 사용할 수 있습니다.

예를 들어 다음 코드는 변수 액세스 식에서 변수의 이름을 인쇄합니다. 노드 유형을 확인하고 변수 액세스 식에 캐스트한 다음 특정 식 형식의 속성을 확인하는 방법을 따랐습니다.

```csharp
Expression<Func<int, int>> addFive = (num) => num + 5;

if (addFive.NodeType == ExpressionType.Lambda)
{
    var lambdaExp = (LambdaExpression)addFive;

    var parameter = lambdaExp.Parameters.First();

    Console.WriteLine(parameter.Name);
    Console.WriteLine(parameter.Type);
}
```

## <a name="creating-expression-trees"></a>식 트리 만들기

`System.Linq.Expression` 클래스에는 식을 만드는 많은 정적 메서드도 포함 되어 있습니다. 이러한 메서드는 자식에 대해 제공된 인수를 사용하여 식 노드를 만듭니다. 이러한 방식으로 리프 노드에서 위로 식을 작성합니다. 예를 들어 다음 코드는 더하기 식을 작성합니다.

```csharp
// Addition is an add expression for "1 + 2"
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var addition = Expression.Add(one, two);
```

이 간단한 예제를 통해 식 트리를 만들고 사용하는 데 많은 형식이 관련됨을 확인할 수 있습니다. 이러한 복잡성은 C# 언어에서 제공하는 풍부한 어휘의 기능을 제공하는 데 필요합니다.

## <a name="navigating-the-apis"></a>API 탐색
C# 언어의 거의 모든 구문 요소에 매핑되는 식 노드 유형이 있습니다. 각 형식에는 해당 언어 요소 형식에 대한 특정 메서드가 있습니다. 한 번에 기억해야 할 사항이 많습니다. 다음은 모든 사항을 기억하는 대신 식 트리로 작업할 때 사용할 수 있는 기술입니다.

1. `ExpressionType` 열거형의 멤버를 확인하여 검색할 수 있는 노드를 결정합니다. 실제로 식 트리를 트래버스하고 이해하려는 경우에 도움이 됩니다.
2. `Expression` 클래스의 정적 멤버를 확인하여 식을 작성합니다. 이러한 메서드는 자식 노드 집합에서 모든 식 형식을 작성할 수 있습니다.
3. `ExpressionVisitor` 클래스를 확인하여 수정된 식 트리를 작성합니다.

세 영역을 각각 확인하면 더 자세히 알아볼 수 있습니다. 이러한 세 단계 중 한 단계로 시작하면 반드시 필요한 항목을 확인할 수 있습니다.
 
 [다음 -- 식 트리 실행](expression-trees-execution.md)
