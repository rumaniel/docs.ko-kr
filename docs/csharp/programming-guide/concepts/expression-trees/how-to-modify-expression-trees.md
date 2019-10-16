---
title: '방법: 식 트리 수정(C#)'
ms.date: 07/20/2015
ms.assetid: 9b0cd8c2-457e-4833-9e36-31e79545f442
ms.openlocfilehash: 7875cf1ccca8866cc87ebec80701ad77ad2bea2d
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595064"
---
# <a name="how-to-modify-expression-trees-c"></a>방법: 식 트리 수정(C#)
이 항목에서는 식 트리를 수정하는 방법을 보여 줍니다. 식 트리는 변경할 수 없으며, 직접 수정할 수 없음을 의미합니다. 식 트리를 변경하려면 기존 식 트리의 복사본을 만들고, 해당 복사본을 만들 때 필요한 사항을 변경해야 합니다. <xref:System.Linq.Expressions.ExpressionVisitor> 클래스를 사용하여 기존 식 트리를 트래버스하고 방문하는 각 노드를 복사할 수 있습니다.  
  
### <a name="to-modify-an-expression-tree"></a>식 트리를 수정하려면  
  
1. **콘솔 애플리케이션** 프로젝트를 새로 만듭니다.  
  
2. `System.Linq.Expressions` 네임스페이스에 대한 `using` 지시문을 파일에 추가합니다.  
  
3. 프로젝트에 `AndAlsoModifier` 클래스를 추가합니다.  
  
    ```csharp  
    public class AndAlsoModifier : ExpressionVisitor  
    {  
        public Expression Modify(Expression expression)  
        {  
            return Visit(expression);  
        }  
  
        protected override Expression VisitBinary(BinaryExpression b)  
        {  
            if (b.NodeType == ExpressionType.AndAlso)  
            {  
                Expression left = this.Visit(b.Left);  
                Expression right = this.Visit(b.Right);  
  
                // Make this binary expression an OrElse operation instead of an AndAlso operation.  
                return Expression.MakeBinary(ExpressionType.OrElse, left, right, b.IsLiftedToNull, b.Method);  
            }  
  
            return base.VisitBinary(b);  
        }  
    }  
    ```  
  
     이 클래스는 <xref:System.Linq.Expressions.ExpressionVisitor> 클래스를 상속하며, 조건부 `AND` 작업을 나타내는 식을 수정하도록 특수화되었습니다. 해당 작업을 조건부 `AND`에서 조건부 `OR`로 변경합니다. 조건부 `AND` 식은 이진 식으로 표현되기 때문에 이 작업을 위해 클래스는 기본 형식의 <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> 메서드를 재정의합니다. `VisitBinary` 메서드에서 전달된 식이 조건부 `AND` 작업을 나타내는 경우 코드는 조건부 `AND` 연산자 대신 조건부 `OR` 연산자가 포함된 새 식을 생성합니다. `VisitBinary`에 전달된 식이 조건부 `AND` 작업을 나타내지 않는 경우 메서드는 기본 클래스 구현을 따릅니다. 기본 클래스 메서드는 전달된 식 트리와 유사한 노드를 생성하지만 노드의 하위 트리가 방문자에 의해 재귀적으로 생성된 식 트리로 바뀌었습니다.  
  
4. `System.Linq.Expressions` 네임스페이스에 대한 `using` 지시문을 파일에 추가합니다.  
  
5. Program.cs 파일의 `Main` 메서드에 코드를 추가하여 식 트리를 만들고 이 식 트리를 수정할 메서드에 전달합니다.  
  
    ```csharp  
    Expression<Func<string, bool>> expr = name => name.Length > 10 && name.StartsWith("G");  
    Console.WriteLine(expr);  
  
    AndAlsoModifier treeModifier = new AndAlsoModifier();  
    Expression modifiedExpr = treeModifier.Modify((Expression) expr);  
  
    Console.WriteLine(modifiedExpr);  
  
    /*  This code produces the following output:  
  
        name => ((name.Length > 10) && name.StartsWith("G"))  
        name => ((name.Length > 10) || name.StartsWith("G"))  
    */  
    ```  
  
     코드에서 조건부 `AND` 작업이 포함된 식을 만듭니다. 그런 다음 `AndAlsoModifier` 클래스 인스턴스를 만들고 이 클래스의 `Modify` 메서드에 식을 전달합니다. 원본 및 수정된 식 트리가 둘 다 출력되어 변경 내용을 표시합니다.  
  
6. 애플리케이션을 컴파일하고 실행합니다.  
  
## <a name="see-also"></a>참고 항목

- [방법: 식 트리 실행(C#)](./how-to-execute-expression-trees.md)
- [식 트리(C#)](./index.md)
