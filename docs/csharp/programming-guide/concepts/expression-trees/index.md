---
title: 식 트리(C#)
ms.date: 07/20/2015
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
ms.openlocfilehash: 7e63bf28f10070daa9624daa67bd5118fa67874d
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926725"
---
# <a name="expression-trees-c"></a>식 트리(C#)
식 트리는 `x < y` 등의 이진 연산이나 메서드 호출과 같이 각 노드가 식인 트리 형식 데이터 구조의 코드를 표시합니다.  
  
 식 트리로 표시되는 코드를 컴파일하고 실행할 수 있습니다. 이렇게 하면 실행 가능한 코드를 동적으로 수정하고, 다양한 데이터베이스에서 LINQ 쿼리를 실행하고, 동적 쿼리를 만들 수 있습니다. LINQ의 식 트리에 대한 자세한 내용은 [방법: 식 트리를 사용하여 동적 쿼리 빌드(C#)](./how-to-use-expression-trees-to-build-dynamic-queries.md)를 참조하세요.  
  
 식 트리는 동적 언어와 .NET Framework 간에 상호 운용성을 제공하고 컴파일러 작성기가 MSIL(Microsoft Intermediate Language) 대신 식 트리를 내보낼 수 있도록 DLR(동적 언어 런타임)에서도 사용됩니다. DLR에 대한 자세한 내용은 [동적 언어 런타임 개요](../../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)를 참조하세요.  
  
 익명 람다 식을 기준으로 C# 또는 Visual Basic 컴파일러가 식 트리를 자동으로 만들도록 할 수도 있고 <xref:System.Linq.Expressions> 네임스페이스를 사용하여 식 트리를 수동으로 만들 수도 있습니다.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>람다 식에서 식 트리 만들기  
 람다 식을 <xref:System.Linq.Expressions.Expression%601> 형식 변수에 할당하면 컴파일러가 해당 람다 식을 나타내는 식 트리를 작성하기 위해 코드를 내보냅니다.  
  
 C# 컴파일러는 람다 식(한 줄 람다)에서만 식 트리를 생성할 수 있으며 문 람다(여러 줄 람다)는 구문 분석할 수 없습니다. C#의 람다 식에 대한 자세한 내용은 [람다 식](../../statements-expressions-operators/lambda-expressions.md)을 참조하세요.  
  
 다음 코드 예제에서는 C# 컴파일러에서 람다 식 `num => num < 5`를 나타내는 식 트리를 만드는 방법을 보여 줍니다.  
  
```csharp  
Expression<Func<int, bool>> lambda = num => num < 5;  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>API를 사용하여 식 트리 만들기  
 API를 사용하여 식 트리를 만들려면 <xref:System.Linq.Expressions.Expression> 클래스를 사용합니다. 이 클래스는 변수나 매개 변수를 나타내는 <xref:System.Linq.Expressions.ParameterExpression> 또는 메서드 호출을 나타내는 <xref:System.Linq.Expressions.MethodCallExpression>과 같이 특정 형식의 식 트리 노드를 만드는 정적 팩터리 메서드를 포함합니다. <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression> 및 기타 식 관련 형식도 <xref:System.Linq.Expressions> 네임스페이스에서 정의됩니다. 이러한 형식은 추상 형식 <xref:System.Linq.Expressions.Expression>에서 파생됩니다.  
  
 다음 코드 예제에서는 API를 사용하여 람다 식 `num => num < 5`를 나타내는 식 트리를 만드는 방법을 보여 줍니다.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Manually build the expression tree for   
// the lambda expression num => num < 5.  
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");  
ConstantExpression five = Expression.Constant(5, typeof(int));  
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);  
Expression<Func<int, bool>> lambda1 =  
    Expression.Lambda<Func<int, bool>>(  
        numLessThanFive,  
        new ParameterExpression[] { numParam });  
```  
  
 .NET Framework 4 이상에서는 식 트리 API가 루프, 조건부 블록, `try-catch` 블록 등의 할당 및 제어 흐름 식도 지원합니다. API를 사용하면 C# 컴파일러를 통해 람다 식에서 작성할 수 있는 것보다 복잡한 식 트리를 만들 수 있습니다. 다음 예제에서는 숫자의 계승을 계산하는 식 트리를 만드는 방법을 보여 줍니다.  
  
```csharp  
// Creating a parameter expression.  
ParameterExpression value = Expression.Parameter(typeof(int), "value");  
  
// Creating an expression to hold a local variable.   
ParameterExpression result = Expression.Parameter(typeof(int), "result");  
  
// Creating a label to jump to from a loop.  
LabelTarget label = Expression.Label(typeof(int));  
  
// Creating a method body.  
BlockExpression block = Expression.Block(  
    // Adding a local variable.  
    new[] { result },  
    // Assigning a constant to a local variable: result = 1  
    Expression.Assign(result, Expression.Constant(1)),  
    // Adding a loop.  
        Expression.Loop(  
    // Adding a conditional block into the loop.  
           Expression.IfThenElse(  
    // Condition: value > 1  
               Expression.GreaterThan(value, Expression.Constant(1)),  
    // If true: result *= value --  
               Expression.MultiplyAssign(result,  
                   Expression.PostDecrementAssign(value)),  
    // If false, exit the loop and go to the label.  
               Expression.Break(label, result)  
           ),  
    // Label to jump to.  
       label  
    )  
);  
  
// Compile and execute an expression tree.  
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);  
  
Console.WriteLine(factorial);  
// Prints 120.  
```

자세한 내용은 [Generating Dynamic Methods with Expression Trees in Visual Studio 2010](https://devblogs.microsoft.com/csharpfaq/generating-dynamic-methods-with-expression-trees-in-visual-studio-2010/)(Visual Studio 2010에서 식 트리를 사용하여 동적 메서드 생성)을 참조하세요. 이 내용은 Visual Studio의 최신 버전에도 적용됩니다.
  
## <a name="parsing-expression-trees"></a>식 트리 구문 분석  
 다음 코드 예제에서는 람다 식 `num => num < 5`를 나타내는 식 트리를 개별 구성 요소로 구성 해제하는 방법을 보여 줍니다.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Create an expression tree.  
Expression<Func<int, bool>> exprTree = num => num < 5;  
  
// Decompose the expression tree.  
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];  
BinaryExpression operation = (BinaryExpression)exprTree.Body;  
ParameterExpression left = (ParameterExpression)operation.Left;  
ConstantExpression right = (ConstantExpression)operation.Right;  
  
Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value);  
  
// This code produces the following output:  
  
// Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>변경 불가능한 식 트리  
 식 트리는 변경할 수 없어야 합니다. 즉, 식 트리를 수정하려면 기존 식 트리를 복사한 다음 트리 내의 노드를 바꾸는 방법으로 새 식 트리를 생성해야 합니다. 식 트리 방문자를 사용하면 기존 식 트리를 트래버스할 수 있습니다. 자세한 내용은 [방법: 식 트리 수정(C#)](./how-to-modify-expression-trees.md)을 참조하세요.  
  
## <a name="compiling-expression-trees"></a>식 트리 컴파일  
 <xref:System.Linq.Expressions.Expression%601> 형식은 식 트리로 표시되는 코드를 실행 가능한 대리자로 컴파일하는 <xref:System.Linq.Expressions.Expression%601.Compile%2A> 메서드를 제공합니다.  
  
 다음 코드 예제에서는 식 트리를 컴파일하고 결과 코드를 실행하는 방법을 보여 줍니다.  
  
```csharp  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 자세한 내용은 [방법: 식 트리 실행(C#)](./how-to-execute-expression-trees.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.Expressions>
- [방법: 식 트리 실행(C#)](./how-to-execute-expression-trees.md)
- [방법: 식 트리 수정(C#)](./how-to-modify-expression-trees.md)
- [람다 식](../../statements-expressions-operators/lambda-expressions.md)
- [동적 언어 런타임 개요](../../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)
- [프로그래밍 개념(C#)](../index.md)
