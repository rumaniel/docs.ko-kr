---
title: 표준 쿼리 연산자 개요 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 302bd39e-2ec1-495b-94bf-37d370d6f05f
ms.openlocfilehash: 9bfdf2163be52d9016a800d65006bbc4fbf560a3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61908143"
---
# <a name="standard-query-operators-overview-visual-basic"></a>표준 쿼리 연산자 개요 (Visual Basic)
*표준 쿼리 연산자*는 LINQ 패턴을 형성하는 메서드입니다. 이 메서드 중 대부분은 시퀀스에서 작동합니다. 여기서 시퀀스란 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스 또는 <xref:System.Linq.IQueryable%601> 인터페이스를 구현하는 형식의 개체입니다. 표준 쿼리 연산자는 필터링, 프로젝션, 집계, 정렬 등을 포함하여 쿼리 기능을 제공합니다.  
  
 <xref:System.Collections.Generic.IEnumerable%601> 형식의 개체에 대해 작동하는 연산자와 <xref:System.Linq.IQueryable%601> 형식의 개체에 대해 작동하는 연산자 등 두 가지 LINQ 표준 쿼리 연산자 집합이 있습니다. 각 집합을 구성하는 메서드는 각각 <xref:System.Linq.Enumerable> 및 <xref:System.Linq.Queryable> 클래스의 정적 멤버입니다. 작동하는 형식의 *확장 메서드*로 정의됩니다. 즉, 정적 메서드 구문 또는 인스턴스 메서드 구문을 사용하여 호출할 수 있습니다.  
  
 또한 여러 표준 쿼리 연산자 메서드는 <xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Linq.IQueryable%601>을 기반으로 하는 형식이 아닌 다른 형식에서 작동합니다. <xref:System.Linq.Enumerable> 형식은 <xref:System.Collections.IEnumerable> 형식의 개체에서 작동하는 이러한 두 메서드를 정의합니다. 두 메서드 <xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> 및 <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29>을 사용하면 LINQ 패턴에서 매개 변수가 없는 컬렉션이나 제네릭이 아닌 컬렉션을 쿼리할 수 있습니다. 이 작업을 위해 강력한 형식의 개체 컬렉션을 만듭니다. <xref:System.Linq.Queryable> 클래스는 <xref:System.Linq.Queryable> 형식의 개체에서 작동하는 두 개의 유사한 메서드 <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> 및 <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>을 정의합니다.  
  
 표준 쿼리 연산자는 단일 값 또는 값 시퀀스를 반환하는지에 따라 실행 타이밍이 다릅니다. singleton 값(예: <xref:System.Linq.Enumerable.Average%2A> 및 <xref:System.Linq.Enumerable.Sum%2A>)을 반환하는 이러한 메서드는 즉시 실행됩니다. 시퀀스를 반환하는 메서드는 쿼리 실행을 지연하고 열거 가능한 개체를 반환합니다.  
  
 메모리 내 컬렉션에 대해 작동하는 메서드, 즉 <xref:System.Collections.Generic.IEnumerable%601>을 확장하는 메서드의 경우 반환된 열거 가능한 개체는 메서드에 전달된 인수를 캡처합니다. 해당 개체를 열거하는 경우 쿼리 연산자의 논리가 사용되며 쿼리 결과가 반환됩니다.  
  
 반면, <xref:System.Linq.IQueryable%601>을 확장하는 메서드는 쿼리 동작을 구현하지 않고 수행할 쿼리를 나타내는 식 트리를 빌드합니다. 쿼리 처리는 소스 <xref:System.Linq.IQueryable%601> 개체에 의해 처리됩니다.  
  
 한 쿼리에서 쿼리 메서드 호출을 연결하여 쿼리가 임의로 복잡해질 수 있습니다.  
  
 다음 코드 예제에서는 표준 쿼리 연산자를 사용하여 시퀀스에 대한 정보를 가져올 수 있는 방법을 보여 줍니다.  
  
```vb  
Dim sentence = "the quick brown fox jumps over the lazy dog"  
' Split the string into individual words to create a collection.  
Dim words = sentence.Split(" "c)  
  
Dim query = From word In words   
            Group word.ToUpper() By word.Length Into gr = Group   
            Order By Length _  
            Select Length, GroupedWords = gr  
  
Dim output As New System.Text.StringBuilder  
For Each obj In query  
    output.AppendLine(String.Format("Words of length {0}:", obj.Length))  
    For Each word As String In obj.GroupedWords  
        output.AppendLine(word)  
    Next  
Next  
  
'Display the output  
MsgBox(output.ToString())  
  
' This code example produces the following output:  
'  
' Words of length 3:  
' THE  
' FOX  
' THE  
' DOG  
' Words of length 4:  
' OVER  
' LAZY  
' Words of length 5:  
' QUICK  
' BROWN  
' JUMPS   
```  
  
## <a name="query-expression-syntax"></a>쿼리 식 구문  
 자주 사용되는 표준 쿼리 연산자 중 일부에는 *쿼리* *식*의 일부로 호출할 수 있는 전용 C# 및 Visual Basic 언어 키워드 구문이 있습니다. 표준 쿼리 연산자가 전용 키워드와 해당 구문에 대 한 자세한 내용은 참조 하세요. [표준 쿼리 연산자 (Visual Basic)에 대 한 쿼리 식 구문](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)합니다.  
  
## <a name="extending-the-standard-query-operators"></a>표준 쿼리 연산자 확장  
 대상 도메인 또는 기술에 적합한 도메인 특정 메서드를 만들어 표준 쿼리 연산자 집합을 강화할 수 있습니다. 또한 원격 평가, 쿼리 변환, 최적화 등의 추가 서비스를 제공하는 고유한 구현으로 표준 쿼리 연산자를 바꿀 수도 있습니다. 예제는 <xref:System.Linq.Enumerable.AsEnumerable%2A>을 참조하세요.  
  
## <a name="related-sections"></a>관련 단원  
 다음 링크는 기능에 따라 다양한 표준 쿼리 연산자에 대한 추가 정보를 제공하는 항목으로 이동합니다.  
  
 [데이터 정렬](../../../../visual-basic/programming-guide/concepts/linq/sorting-data.md)  
  
 [집합 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/set-operations.md)  
  
 [데이터 필터링 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/filtering-data.md)  
  
 [수량자 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md)  
  
 [프로젝션 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projection-operations.md)  
  
 [데이터 분할 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/partitioning-data.md)  
  
 [조인 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/join-operations.md)  
  
 [데이터 그룹화 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/grouping-data.md)  
  
 [생성 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/generation-operations.md)  
  
 [같음 연산 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/equality-operations.md)  
  
 [요소 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/element-operations.md)  
  
 [데이터 형식 변환 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)  
  
 [연결 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/concatenation-operations.md)  
  
 [집계 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)  
  
## <a name="see-also"></a>참고자료

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [LINQ 소개(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-linq.md)
- [표준 쿼리 연산자 (Visual Basic)에 대 한 쿼리 식 구문](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)
- [실행 (Visual Basic) 방식에 따라 표준 쿼리 연산자 분류](../../../../visual-basic/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)
- [확장명 메서드](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
