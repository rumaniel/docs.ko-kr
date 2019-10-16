---
title: '방법: 식 트리 수정 (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: d1309fff-28bd-4d8e-a2cf-75725999e8f2
ms.openlocfilehash: ac196b56f178659765437a97a25f46c04f8040fa
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054207"
---
# <a name="how-to-modify-expression-trees-visual-basic"></a>방법: 식 트리 수정 (Visual Basic)

이 항목에서는 식 트리를 수정하는 방법을 보여 줍니다. 식 트리는 변경할 수 없으며, 직접 수정할 수 없음을 의미합니다. 식 트리를 변경하려면 기존 식 트리의 복사본을 만들고, 해당 복사본을 만들 때 필요한 사항을 변경해야 합니다. <xref:System.Linq.Expressions.ExpressionVisitor> 클래스를 사용하여 기존 식 트리를 트래버스하고 방문하는 각 노드를 복사할 수 있습니다.

## <a name="to-modify-an-expression-tree"></a>식 트리를 수정하려면

1. **콘솔 응용 프로그램** 프로젝트를 새로 만듭니다.

2. 네임 스페이스에 대 한 파일에 문을추가합니다.`Imports` `System.Linq.Expressions`

3. 프로젝트에 `AndAlsoModifier` 클래스를 추가합니다.

    ```vb
    Public Class AndAlsoModifier
        Inherits ExpressionVisitor

        Public Function Modify(ByVal expr As Expression) As Expression
            Return Visit(expr)
        End Function

        Protected Overrides Function VisitBinary(ByVal b As BinaryExpression) As Expression
            If b.NodeType = ExpressionType.AndAlso Then
                Dim left = Me.Visit(b.Left)
                Dim right = Me.Visit(b.Right)

                ' Make this binary expression an OrElse operation instead
                ' of an AndAlso operation.
                Return Expression.MakeBinary(ExpressionType.OrElse, left, right, _
                                             b.IsLiftedToNull, b.Method)
            End If

            Return MyBase.VisitBinary(b)
        End Function
    End Class
    ```

    이 클래스는 <xref:System.Linq.Expressions.ExpressionVisitor> 클래스를 상속하며, 조건부 `AND` 작업을 나타내는 식을 수정하도록 특수화되었습니다. 해당 작업을 조건부 `AND`에서 조건부 `OR`로 변경합니다. 조건부 `AND` 식은 이진 식으로 표현되기 때문에 이 작업을 위해 클래스는 기본 형식의 <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> 메서드를 재정의합니다. `VisitBinary` 메서드에서 전달된 식이 조건부 `AND` 작업을 나타내는 경우 코드는 조건부 `AND` 연산자 대신 조건부 `OR` 연산자가 포함된 새 식을 생성합니다. `VisitBinary`에 전달된 식이 조건부 `AND` 작업을 나타내지 않는 경우 메서드는 기본 클래스 구현을 따릅니다. 기본 클래스 메서드는 전달된 식 트리와 유사한 노드를 생성하지만 노드의 하위 트리가 방문자에 의해 재귀적으로 생성된 식 트리로 바뀌었습니다.

4. 네임 스페이스에 대 한 파일에 문을추가합니다.`Imports` `System.Linq.Expressions`

5. Module1.vb 파일의 `Main` 메서드에 코드를 추가 하 여 식 트리를 만들고 수정 하는 메서드에 전달 합니다.

    ```vb
    Dim expr As Expression(Of Func(Of String, Boolean)) = _
        Function(name) name.Length > 10 AndAlso name.StartsWith("G")

    Console.WriteLine(expr)

    Dim modifier As New AndAlsoModifier()
    Dim modifiedExpr = modifier.Modify(CType(expr, Expression))

    Console.WriteLine(modifiedExpr)

    ' This code produces the following output:
    ' name => ((name.Length > 10) && name.StartsWith("G"))
    ' name => ((name.Length > 10) || name.StartsWith("G"))
    ```

    코드에서 조건부 `AND` 작업이 포함된 식을 만듭니다. 그런 다음 `AndAlsoModifier` 클래스 인스턴스를 만들고 이 클래스의 `Modify` 메서드에 식을 전달합니다. 원본 및 수정된 식 트리가 둘 다 출력되어 변경 내용을 표시합니다.

6. 애플리케이션을 컴파일하고 실행합니다.

## <a name="see-also"></a>참고자료

- [방법: 식 트리 실행 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)
- [식 트리(Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)
