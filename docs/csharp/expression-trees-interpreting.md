---
title: 식 해석
description: 식 트리의 구조를 검사하는 코드를 작성하는 방법을 알아봅니다.
ms.date: 06/20/2016
ms.assetid: adf73dde-1e52-4df3-9929-2e0670e28e16
ms.openlocfilehash: c9d80ca234e298df2f2e7ce48fbf92cb817fc8a7
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70925682"
---
# <a name="interpreting-expressions"></a>식 해석

[이전 -- 식 실행](expression-trees-execution.md)

이제 *식 트리*의 구조를 검사하는 몇 가지 코드를 작성해 보겠습니다. 식 트리의 모든 노드는 `Expression`에서 파생되는 클래스의 개체입니다.

해당 디자인은 식 트리의 모든 노드 방문을 비교적 간단한 재귀 작업으로 만듭니다. 일반적인 전략은 루트 노드에서 시작하고 노드의 종류를 확인하는 것입니다.

노드 형식에 자식이 있는 경우 자식을 재귀적으로 방문합니다. 각 자식 노드에서 루트 노드에 사용된 프로세스를 반복합니다. 즉, 형식을 확인하고 형식에 자식이 있는 경우 각 자식을 방문합니다.

## <a name="examining-an-expression-with-no-children"></a>자식이 없는 식 검사
먼저 매우 간단한 식 트리의 각 노드를 방문해 보겠습니다.
다음은 상수 식을 만든 다음 해당 속성을 검사하는 코드입니다.

```csharp
var constant = Expression.Constant(24, typeof(int));

Console.WriteLine($"This is a/an {constant.NodeType} expression type");
Console.WriteLine($"The type of the constant value is {constant.Type}");
Console.WriteLine($"The value of the constant value is {constant.Value}");
```

다음과 같이 출력됩니다.

```output
This is an Constant expression type
The type of the constant value is System.Int32
The value of the constant value is 24
```

이제 이 식을 검색하고 식에 대해 몇 가지 중요한 속성을 작성하는 코드를 작성해 보겠습니다. 해당 코드는 다음과 같습니다.

## <a name="examining-a-simple-addition-expression"></a>간단한 더하기 식 검사

이 섹션의 소개 부분에 있는 더하기 샘플로 시작해 보겠습니다.

```csharp
Expression<Func<int>> sum = () => 1 + 2;
```

> `var`을 사용하여 이 식 트리를 선언하지 않습니다. 왜냐하면 할당의 오른쪽이 암시적으로 형식화되어 있기 때문에 그렇게 할 수 없습니다. 이 사항을 좀더 자세히 이해하려면 [여기](implicitly-typed-lambda-expressions.md)를 읽어보세요.

루트 노드는 `LambdaExpression`입니다. `=>` 연산자의 오른쪽에서 흥미로운 코드를 가져오려면 `LambdaExpression`의 자식 중 하나를 찾아야 합니다. 이 섹션에서는 모든 식을 사용하여 찾습니다. 부모 노드는 `LambdaExpression`의 반환 형식을 찾는 데 도움이 됩니다.

이 식의 각 노드를 검사하려면 많은 노드를 재귀적으로 방문해야 합니다. 다음은 간단한 첫 번째 구현입니다.

```csharp
Expression<Func<int, int, int>> addition = (a, b) => a + b;

Console.WriteLine($"This expression is a {addition.NodeType} expression type");
Console.WriteLine($"The name of the lambda is {((addition.Name == null) ? "<null>" : addition.Name)}");
Console.WriteLine($"The return type is {addition.ReturnType.ToString()}");
Console.WriteLine($"The expression has {addition.Parameters.Count} arguments. They are:");
foreach(var argumentExpression in addition.Parameters)
{
    Console.WriteLine($"\tParameter Type: {argumentExpression.Type.ToString()}, Name: {argumentExpression.Name}");
}

var additionBody = (BinaryExpression)addition.Body;
Console.WriteLine($"The body is a {additionBody.NodeType} expression");
Console.WriteLine($"The left side is a {additionBody.Left.NodeType} expression");
var left = (ParameterExpression)additionBody.Left;
Console.WriteLine($"\tParameter Type: {left.Type.ToString()}, Name: {left.Name}");
Console.WriteLine($"The right side is a {additionBody.Right.NodeType} expression");
var right= (ParameterExpression)additionBody.Right;
Console.WriteLine($"\tParameter Type: {right.Type.ToString()}, Name: {right.Name}");
```

이 샘플은 다음과 같이 출력됩니다.

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 arguments. They are:
        Parameter Type: System.Int32, Name: a
        Parameter Type: System.Int32, Name: b
The body is a/an Add expression
The left side is a Parameter expression
        Parameter Type: System.Int32, Name: a
The right side is a Parameter expression
        Parameter Type: System.Int32, Name: b
```

위의 코드 샘플에서 많은 반복을 확인할 수 있습니다.
이러한 반복을 정리하고 보다 일반적인 용도의 식 노드 방문자를 빌드해 보겠습니다. 그러려면 재귀 알고리즘을 작성해야 합니다. 모든 노드는 자식이 있는 형식일 수 있습니다.
자식이 있는 모든 노드에서는 해당 자식을 방문하여 해당 노드의 종류를 확인해야 합니다. 다음은 재귀를 활용하여 더하기 연산을 방문하는 정리된 버전입니다.

```csharp
// Base Visitor class:
public abstract class Visitor
{
    private readonly Expression node;

    protected Visitor(Expression node)
    {
        this.node = node;
    }

    public abstract void Visit(string prefix);

    public ExpressionType NodeType => this.node.NodeType;
    public static Visitor CreateFromExpression(Expression node)
    {
        switch(node.NodeType)
        {
            case ExpressionType.Constant:
                return new ConstantVisitor((ConstantExpression)node);
            case ExpressionType.Lambda:
                return new LambdaVisitor((LambdaExpression)node);
            case ExpressionType.Parameter:
                return new ParameterVisitor((ParameterExpression)node);
            case ExpressionType.Add:
                return new BinaryVisitor((BinaryExpression)node);
            default:
                Console.Error.WriteLine($"Node not processed yet: {node.NodeType}");
                return default(Visitor);
        }
    }
}

// Lambda Visitor
public class LambdaVisitor : Visitor
{
    private readonly LambdaExpression node;
    public LambdaVisitor(LambdaExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression type");
        Console.WriteLine($"{prefix}The name of the lambda is {((node.Name == null) ? "<null>" : node.Name)}");
        Console.WriteLine($"{prefix}The return type is {node.ReturnType.ToString()}");
        Console.WriteLine($"{prefix}The expression has {node.Parameters.Count} argument(s). They are:");
        // Visit each parameter:
        foreach (var argumentExpression in node.Parameters)
        {
            var argumentVisitor = Visitor.CreateFromExpression(argumentExpression);
            argumentVisitor.Visit(prefix + "\t");
        }
        Console.WriteLine($"{prefix}The expression body is:");
        // Visit the body:
        var bodyVisitor = Visitor.CreateFromExpression(node.Body);
        bodyVisitor.Visit(prefix + "\t");
    }
}

// Binary Expression Visitor:
public class BinaryVisitor : Visitor
{
    private readonly BinaryExpression node;
    public BinaryVisitor(BinaryExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This binary expression is a {NodeType} expression");
        var left = Visitor.CreateFromExpression(node.Left);
        Console.WriteLine($"{prefix}The Left argument is:");
        left.Visit(prefix + "\t");
        var right = Visitor.CreateFromExpression(node.Right);
        Console.WriteLine($"{prefix}The Right argument is:");
        right.Visit(prefix + "\t");
    }
}

// Parameter visitor:
public class ParameterVisitor : Visitor
{
    private readonly ParameterExpression node;
    public ParameterVisitor(ParameterExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This is an {NodeType} expression type");
        Console.WriteLine($"{prefix}Type: {node.Type.ToString()}, Name: {node.Name}, ByRef: {node.IsByRef}");
    }
}

// Constant visitor:
public class ConstantVisitor : Visitor
{
    private readonly ConstantExpression node;
    public ConstantVisitor(ConstantExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This is an {NodeType} expression type");
        Console.WriteLine($"{prefix}The type of the constant value is {node.Type}");
        Console.WriteLine($"{prefix}The value of the constant value is {node.Value}");
    }
}
```

이 알고리즘은 임의의 `LambdaExpression`을 방문할 수 있는 알고리즘의 기반입니다. 많은 허점이 있습니다. 즉, 만들어진 코드는 가능한 식 트리 노드 집합의 매우 작은 샘플만 찾습니다. 그러나 생성되는 항목에서 많은 부분을 익힐 수 있습니다. `Visitor.CreateFromExpression` 메서드의 기본 사례에서는 새 노드 형식이 나타나면 오류 콘솔에 메시지를 출력합니다. 이런 방식으로 새로운 식 형식을 추가합니다.

위에 표시된 더하기 식에서 이 방문자를 실행하면 다음과 같이 출력됩니다.

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
        This is an Parameter expression type
        Type: System.Int32, Name: b, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This is an Parameter expression type
                Type: System.Int32, Name: a, ByRef: False
        The Right argument is:
                This is an Parameter expression type
                Type: System.Int32, Name: b, ByRef: False
```

보다 일반적인 방문자 구현을 구축했으므로 훨씬 더 다양한 형식을 식을 방문하여 처리할 수 있습니다.

## <a name="examining-an-addition-expression-with-many-levels"></a>많은 수준으로 더하기 식 검사

더 복잡한 예제를 시도해 보겠지만 노드 형식은 여전히 더하기로만 제한합니다.

```csharp
Expression<Func<int>> sum = () => 1 + 2 + 3 + 4;
```

방문자 알고리즘에서 실행하기 전에 사고 연습을 통해 출력되는 사항을 파악합니다. `+` 연산자는 *이진 연산자*임을 기억하세요. 이 연산자에는 왼쪽과 오른쪽 피연산자를 나타내는 두 개의 자식이 있어야 합니다. 여러 가지 방법으로 올바른 트리를 생성할 수 있습니다.

```csharp
Expression<Func<int>> sum1 = () => 1 + (2 + (3 + 4));
Expression<Func<int>> sum2 = () => ((1 + 2) + 3) + 4;

Expression<Func<int>> sum3 = () => (1 + 2) + (3 + 4);
Expression<Func<int>> sum4 = () => 1 + ((2 + 3) + 4);
Expression<Func<int>> sum5 = () => (1 + (2 + 3)) + 4;
```

가장 유망한 해답을 강조하기 위해 두 가지 가능한 해답으로 분리된 것을 볼 수 있습니다. 첫 번째는 *오른쪽 결합성* 식을 나타내고, 두 번째는 *왼쪽 결합형* 식을 나타냅니다.
이러한 두 형식의 장점은 형식이 임의 개수의 더하기 식으로 확장된다는 점입니다. 

방문자를 통해 이 식을 실행하면 이 출력을 통해 간단한 더하기 식이 *왼쪽 결합성*이 있음을 확인할 수 있습니다. 

이 샘플을 실행하고 전체 식 트리를 보기 위해 소스 식 트리에서 한 가지를 변경해야 했습니다. 식 트리에 모든 상수가 포함되어 있으면 결과 트리에는 상수 값 `10`만 포함됩니다. 컴파일러는 모든 더하기를 수행하고 가장 간단한 형태로 식을 줄입니다. 식에서 하나의 변수를 추가하기만 하면 원래 트리를 확인하는 데 충분합니다.

```csharp
Expression<Func<int, int>> sum = (a) => 1 + a + 3 + 4;
```

이 합계에 대한 방문자를 만들고 방문자를 실행하면 다음 출력이 표시됩니다.

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 1 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This binary expression is a Add expression
                        The Left argument is:
                                This is an Constant expression type
                                The type of the constant value is System.Int32
                                The value of the constant value is 1
                        The Right argument is:
                                This is an Parameter expression type
                                Type: System.Int32, Name: a, ByRef: False
                The Right argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 3
        The Right argument is:
                This is an Constant expression type
                The type of the constant value is System.Int32
                The value of the constant value is 4
```

방문자 코드를 통해 다른 샘플을 실행하고 해당 코드가 나타내는 트리를 확인할 수도 있습니다. 다음은 컴파일러가 상수를 계산할 수 없도록 하는 추가 매개 변수가 있는 위의 `sum3` 식에 대한 예제입니다.

```csharp
Expression<Func<int, int, int>> sum3 = (a, b) => (1 + a) + (3 + b);
```

방문자의 출력은 다음과 같습니다.

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
        This is an Parameter expression type
        Type: System.Int32, Name: b, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 1
                The Right argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: a, ByRef: False
        The Right argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 3
                The Right argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: b, ByRef: False
```

괄호는 출력의 일부가 아닙니다. 식 트리에는 입력 식의 괄호를 나타내는 노드가 없습니다. 식 트리의 구조에는 우선 순위를 전달하는 데 필요한 모든 정보가 포함됩니다.

## <a name="extending-from-this-sample"></a>이 샘플에서 확장

이 샘플은 가장 기본적인 식 트리만 처리합니다. 이 섹션에서 살펴본 코드는 상수 정수와 이진 `+` 연산자만 처리합니다. 최종 샘플로 방문자를 업데이트하여 더 복잡한 식을 처리해 보겠습니다. 다음 코드에 대해 작동하도록 만들어 보겠습니다.

```csharp
Expression<Func<int, int>> factorial = (n) =>
    n == 0 ? 
    1 : 
    Enumerable.Range(1, n).Aggregate((product, factor) => product * factor);
```

이 코드는 수학 *계승* 함수에 가능한 한 가지 구현을 나타냅니다. 이 코드를 작성한 방법에서는 식에 람다 식을 할당하여 식 트리를 작성할 때의 두 가지 제한을 강조합니다. 첫째, 문 람다는 허용되지 않습니다. 즉, 루프, 블록, if/else 문 및 C#에서 일반적인 다른 제어 구조를 사용할 수 없습니다. 식 사용으로 제한됩니다. 둘째, 같은 식을 재귀적으로 호출할 수 없습니다.
이미 대리자인 경우에는 가능하지만 식 트리 형식으로는 호출할 수 없습니다. [식 트리 작성](expression-trees-building.md)에 대한 섹션에서는 이러한 제한 사항을 해결하는 기술을 알아봅니다.

이 식에서는 다음과 같은 형식의 노드가 모두 나타납니다.

1. 같음(이진 식)
2. 곱하기(이진 식)
3. 조건식(? : 식)
4. 메서드 호출 식(`Range()` 및 `Aggregate()` 호출)

방문자 알고리즘을 수정하는 한 가지 방법은 해당 알고리즘을 계속 실행하고 `default` 절에 도달할 때마다 노드 형식을 기록하는 것입니다. 몇 번 반복하면 각각의 잠재적 노드를 확인하게 됩니다. 그러면 다 끝났습니다. 결과는 다음과 같이 나타납니다.

```csharp
public static Visitor CreateFromExpression(Expression node)
{
    switch(node.NodeType)
    {
        case ExpressionType.Constant:
            return new ConstantVisitor((ConstantExpression)node);
        case ExpressionType.Lambda:
            return new LambdaVisitor((LambdaExpression)node);
        case ExpressionType.Parameter:
            return new ParameterVisitor((ParameterExpression)node);
        case ExpressionType.Add:
        case ExpressionType.Equal:
        case ExpressionType.Multiply:
            return new BinaryVisitor((BinaryExpression)node);
        case ExpressionType.Conditional:
            return new ConditionalVisitor((ConditionalExpression)node);
        case ExpressionType.Call:
            return new MethodCallVisitor((MethodCallExpression)node);
        default:
            Console.Error.WriteLine($"Node not processed yet: {node.NodeType}");
            return default(Visitor);
    }
}
```

ConditionalVisitor 및 MethodCallVisitor는 해당 두 노드를 처리합니다.

```csharp
public class ConditionalVisitor : Visitor
{
    private readonly ConditionalExpression node;
    public ConditionalVisitor(ConditionalExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression");
        var testVisitor = Visitor.CreateFromExpression(node.Test);
        Console.WriteLine($"{prefix}The Test for this expression is:");
        testVisitor.Visit(prefix + "\t");
        var trueVisitor = Visitor.CreateFromExpression(node.IfTrue);
        Console.WriteLine($"{prefix}The True clause for this expression is:");
        trueVisitor.Visit(prefix + "\t");
        var falseVisitor = Visitor.CreateFromExpression(node.IfFalse);
        Console.WriteLine($"{prefix}The False clause for this expression is:");
        falseVisitor.Visit(prefix + "\t");
    }
}

public class MethodCallVisitor : Visitor
{
    private readonly MethodCallExpression node;
    public MethodCallVisitor(MethodCallExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression");
        if (node.Object == null)
            Console.WriteLine($"{prefix}This is a static method call");
        else
        {
            Console.WriteLine($"{prefix}The receiver (this) is:");
            var receiverVisitor = Visitor.CreateFromExpression(node.Object);
            receiverVisitor.Visit(prefix + "\t");
        }

        var methodInfo = node.Method;
        Console.WriteLine($"{prefix}The method name is {methodInfo.DeclaringType}.{methodInfo.Name}");
        // There is more here, like generic arguments, and so on.
        Console.WriteLine($"{prefix}The Arguments are:");
        foreach(var arg in node.Arguments)
        {
            var argVisitor = Visitor.CreateFromExpression(arg);
            argVisitor.Visit(prefix + "\t");
        }
    }
}
```

식 트리에 대한 출력은 다음과 같습니다.

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 1 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: n, ByRef: False
The expression body is:
        This expression is a Conditional expression
        The Test for this expression is:
                This binary expression is a Equal expression
                The Left argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: n, ByRef: False
                The Right argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 0
        The True clause for this expression is:
                This is an Constant expression type
                The type of the constant value is System.Int32
                The value of the constant value is 1
        The False clause for this expression is:
                This expression is a Call expression
                This is a static method call
                The method name is System.Linq.Enumerable.Aggregate
                The Arguments are:
                        This expression is a Call expression
                        This is a static method call
                        The method name is System.Linq.Enumerable.Range
                        The Arguments are:
                                This is an Constant expression type
                                The type of the constant value is System.Int32
                                The value of the constant value is 1
                                This is an Parameter expression type
                                Type: System.Int32, Name: n, ByRef: False
                        This expression is a Lambda expression type
                        The name of the lambda is <null>
                        The return type is System.Int32
                        The expression has 2 arguments. They are:
                                This is an Parameter expression type
                                Type: System.Int32, Name: product, ByRef: False
                                This is an Parameter expression type
                                Type: System.Int32, Name: factor, ByRef: False
                        The expression body is:
                                This binary expression is a Multiply expression
                                The Left argument is:
                                        This is an Parameter expression type
                                        Type: System.Int32, Name: product, ByRef: False
                                The Right argument is:
                                        This is an Parameter expression type
                                        Type: System.Int32, Name: factor, ByRef: False
```

## <a name="extending-the-sample-library"></a>샘플 라이브러리 확장

이 섹션의 샘플은 식 트리의 노드를 방문하여 검사하는 핵심 기술을 보여 줍니다. 식 트리의 노드를 방문하고 액세스하는 핵심 작업에 집중하기 위해 필요할 수 있는 많은 작업에 주석을 달았습니다. 

첫째, 방문자는 정수인 상수만 처리합니다. 상수 값은 다른 모든 숫자 형식이 될 수 있으며 C# 언어는 해당 형식 간의 변환 및 승격을 지원합니다. 이 코드의 보다 강력한 버전은 이러한 모든 기능을 미러링합니다.

마지막 예제도 가능한 노드 형식의 하위 집합을 인식합니다.
이 예제가 실패하도록 하는 많은 식을 제공할 수도 있습니다.
전체 구현은 <xref:System.Linq.Expressions.ExpressionVisitor>라는 이름으로 .NET Standard에 포함되며 가능한 노드 형식을 모두 처리할 수 있습니다.

마지막으로 이 문서에서 사용된 라이브러리는 데모 및 학습용으로 작성되었으며, 최적화되지 않았습니다. 사용된 구조를 매우 명확하게 하고 노드를 방문하여 포함된 항목을 분석하는 데 사용된 기술을 강조하기 위해 작성되었습니다. 프로덕션 구현에서는 지금까지보다 성능에 더 많은 주의를 기울입니다.

이러한 제한 사항에도 불구하고 식 트리를 읽고 이해하는 알고리즘 작성을 완료해야 합니다.

[다음 -- 식 작성](expression-trees-building.md)
