---
title: 실행 방식에 따라 표준 쿼리 연산자 분류 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 7f55b0be-9f6e-44f8-865c-6afbea50cc54
ms.openlocfilehash: e89c58707b4980b208395cce67434a6e5efa5d22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939263"
---
# <a name="classification-of-standard-query-operators-by-manner-of-execution-visual-basic"></a>실행 방식에 따라 표준 쿼리 연산자 분류 (Visual Basic)
표준 쿼리 연산자 메서드의 LINQ to Objects 구현은 즉시 실행 또는 지연된 실행의 두 가지 기본 방식 중 하나로 실행됩니다. 지연된 실행을 사용하는 쿼리 연산자는 스트리밍 및 비스트리밍의 두 가지 범주로 추가로 구분할 수 있습니다. 여러 쿼리 연산자가 어떻게 실행되는지 알고 있으면 제공된 쿼리에서 얻을 결과를 이해하는 데 도움이 될 수 있습니다. 데이터 소스가 변경되거나 다른 쿼리 위에 쿼리를 빌드할 경우 특히 도움이 됩니다. 이 항목에서는 실행 방식에 따라 표준 쿼리 연산자를 분류합니다.  
  
## <a name="manners-of-execution"></a>실행 방식  
  
### <a name="immediate"></a>즉시  
 즉시 실행은 코드의 쿼리가 선언되는 지점에서 데이터 소스를 읽고 작업이 수행됨을 의미합니다. 하나의 비열거형 결과를 반환하는 모든 표준 쿼리 연산자는 즉시 실행됩니다.  
  
### <a name="deferred"></a>연기됨  
 지연된 실행은 코드의 쿼리가 선언되는 지점에서 작업이 수행되지 않음을 의미합니다. 예를 들어 `For Each` 문을 사용하여 쿼리 변수가 열거될 경우에만 작업이 수행됩니다. 즉, 쿼리 실행 결과는 쿼리가 정의될 때가 아니라 쿼리가 실행될 때 데이터 소스의 내용에 따라 달라집니다. 쿼리 변수가 여러 번 열거될 경우 매번 결과가 다를 수 있습니다. 반환 형식이 <xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Linq.IOrderedEnumerable%601>인 표준 쿼리 연산자는 대부분 지연 방식으로 실행됩니다.  
  
 지연된 실행을 사용하는 쿼리 연산자는 스트리밍 및 비스트리밍으로 추가로 분류할 수 있습니다.  
  
#### <a name="streaming"></a>스트리밍  
 스트리밍 연산자는 요소를 생성하기 전에 모든 소스 데이터를 읽을 필요가 없습니다. 실행 시 스트리밍 연산자는 소스 요소를 읽을 때 각 소스 요소에 대해 작업을 수행하고 해당하는 경우 요소를 생성합니다. 스트리밍 연산자는 결과 요소가 생성될 때까지 소스 요소를 계속 읽습니다. 즉, 두 개 이상의 소스 요소를 읽어 하나의 결과 요소를 생성할 수 있습니다.  
  
#### <a name="non-streaming"></a>비스트리밍  
 비스트리밍 연산자는 결과 요소를 생성하기 전에 모든 소스 데이터를 읽어야 합니다. 정렬 또는 그룹화 등의 작업은 이 범주로 분류됩니다. 실행 시 비스트리밍 쿼리 연산자는 모든 소스 데이터를 읽고, 데이터 구조에 넣고, 작업을 수행하고, 결과 요소를 생성합니다.  
  
## <a name="classification-table"></a>분류 표  
 다음 표에서는 실행 방법에 따라 각 표준 쿼리 연산자 메서드를 분류합니다.  
  
> [!NOTE]
> 한 연산자가 두 개의 열에 표시되어 있으면 두 개의 입력 시퀀스가 작업에 포함되고 각 시퀀스는 다르게 계산됩니다. 이러한 경우에 지연된 스트리밍 방식으로 계산되는 것은 항상 매개 변수 목록의 첫 번째 시퀀스입니다.  
  
|표준 쿼리 연산자|반환 형식|즉시 실행|지연된 스트리밍 실행|지연된 비스트리밍 실행|  
|-----------------------------|-----------------|-------------------------|----------------------------------|---------------------------------------|  
|<xref:System.Linq.Enumerable.Aggregate%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.All%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Any%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.AsEnumerable%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Average%2A>|단일 숫자 값|X|||  
|<xref:System.Linq.Enumerable.Cast%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Concat%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Contains%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Count%2A>|<xref:System.Int32>|X|||  
|<xref:System.Linq.Enumerable.DefaultIfEmpty%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Distinct%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.ElementAt%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.ElementAtOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.Empty%2A>|<xref:System.Collections.Generic.IEnumerable%601>|X|||  
|<xref:System.Linq.Enumerable.Except%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.First%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.FirstOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.GroupBy%2A>|<xref:System.Collections.Generic.IEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.GroupJoin%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
<xref:System.Linq.Enumerable.Intersect%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.Join%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.Last%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.LastOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.LongCount%2A>|<xref:System.Int64>|X|||  
|<xref:System.Linq.Enumerable.Max%2A>|단일 숫자 값, TSource 또는 TResult|X|||  
|<xref:System.Linq.Enumerable.Min%2A>|단일 숫자 값, TSource 또는 TResult|X|||  
|<xref:System.Linq.Enumerable.OfType%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.OrderBy%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.OrderByDescending%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.Range%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Repeat%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Reverse%2A>|<xref:System.Collections.Generic.IEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.Select%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SelectMany%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SequenceEqual%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Single%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.SingleOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.Skip%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SkipWhile%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Sum%2A>|단일 숫자 값|X|||  
|<xref:System.Linq.Enumerable.Take%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
<xref:System.Linq.Enumerable.TakeWhile%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.ThenBy%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.ThenByDescending%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.ToArray%2A>|TSource 배열|X|||  
|<xref:System.Linq.Enumerable.ToDictionary%2A>|<xref:System.Collections.Generic.Dictionary%602>|X|||  
|<xref:System.Linq.Enumerable.ToList%2A>|<xref:System.Collections.Generic.IList%601>|X|||  
|<xref:System.Linq.Enumerable.ToLookup%2A>|<xref:System.Linq.ILookup%602>|X|||  
|<xref:System.Linq.Enumerable.Union%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Where%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
  
## <a name="see-also"></a>참고자료

- <xref:System.Linq.Enumerable>
- [표준 쿼리 연산자 개요(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [표준 쿼리 연산자 (Visual Basic)에 대 한 쿼리 식 구문](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)
- [LINQ to Objects(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
