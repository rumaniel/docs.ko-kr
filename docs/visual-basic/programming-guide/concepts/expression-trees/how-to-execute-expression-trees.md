---
title: '방법: 식 트리 실행 (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 9dfb5ab3-f48f-417e-975f-f8f6f1cdc18d
ms.openlocfilehash: 135c295070ea591f3b494734f9d236e36b9c3c5d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916497"
---
# <a name="how-to-execute-expression-trees-visual-basic"></a>방법: 식 트리 실행 (Visual Basic)
이 항목에서는 식 트리를 실행하는 방법을 보여 줍니다. 식 트리를 실행할 때 값이 반환될 수 있거나, 메서드 호출 등의 작업만 수행할 수도 있습니다.  
  
 람다 식을 나타내는 식 트리만 실행할 수 있습니다. 람다 식을 나타내는 식 트리는 <xref:System.Linq.Expressions.LambdaExpression> 또는 <xref:System.Linq.Expressions.Expression%601> 형식입니다. 이러한 식 트리를 실행하려면 <xref:System.Linq.Expressions.LambdaExpression.Compile%2A> 메서드를 호출하여 실행 가능한 대리자를 만든 후 대리자를 호출합니다.  
  
> [!NOTE]
> 대리자의 형식을 알 수 없는 경우, 즉 람다 식이 <xref:System.Linq.Expressions.Expression%601> 형식이 아니라 <xref:System.Linq.Expressions.LambdaExpression> 형식인 경우 대리자를 직접 호출하는 대신 대리자의 <xref:System.Delegate.DynamicInvoke%2A> 메서드를 호출해야 합니다.  
  
 식 트리가 람다 식을 나타내지 않는 경우 <xref:System.Linq.Expressions.Expression.Lambda%60%601%28System.Linq.Expressions.Expression%2CSystem.Collections.Generic.IEnumerable%7BSystem.Linq.Expressions.ParameterExpression%7D%29> 메서드를 호출하여 원래 식 트리가 본문으로 포함된 새 람다 식을 만들 수 있습니다. 그런 다음 이 섹션의 앞부분에서 설명한 대로 람다 식을 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 람다 식을 만들고 실행하여 숫자의 거듭제곱을 나타내는 식 트리를 실행하는 방법을 보여 줍니다. 숫자의 거듭제곱을 나타내는 결과가 표시됩니다.  
  
```vb  
' The expression tree to execute.  
Dim be As BinaryExpression = Expression.Power(Expression.Constant(2.0R), Expression.Constant(3.0R))  
  
' Create a lambda expression.  
Dim le As Expression(Of Func(Of Double)) = Expression.Lambda(Of Func(Of Double))(be)  
  
' Compile the lambda expression.  
Dim compiledExpression As Func(Of Double) = le.Compile()  
  
' Execute the lambda expression.  
Dim result As Double = compiledExpression()  
  
' Display the result.  
MsgBox(result)  
  
' This code produces the following output:  
' 8  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- System.Linq.Expressions 네임스페이스를 포함합니다.  
  
## <a name="see-also"></a>참고자료

- [식 트리(Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)
- [방법: 식 트리 수정 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)
