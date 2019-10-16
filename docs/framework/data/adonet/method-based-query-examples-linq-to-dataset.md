---
title: 메서드 기반 쿼리 예제(LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: d340775c-7f39-4087-a290-5cbec6cfa68e
ms.openlocfilehash: 3cda55457df4157f1b0d2cdef1f857cfe6540c66
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783739"
---
# <a name="method-based-query-examples-linq-to-dataset"></a>메서드 기반 쿼리 예제(LINQ to DataSet)
이 섹션에서는 표준 쿼리 연산자를 사용 하는 메서드 기반 쿼리 구문에 LINQ to DataSet 프로그래밍 예제를 제공 합니다. 이러한 <xref:System.Data.DataSet> 예제에서 사용 되는은 [데이터 집합](loading-data-into-a-dataset.md)에 `FillDataSet` 데이터를 로드 하는 데 지정 된 메서드를 사용 하 여 채워집니다. 자세한 내용은 [표준 쿼리 연산자 개요 (C#)](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md) 또는 [표준 쿼리 연산자 개요 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [프로젝션](method-based-query-syntax-examples-projection.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.Select%2A> 및 <xref:System.Linq.Enumerable.SelectMany%2A> 메서드를 사용하여 <xref:System.Data.DataSet>을 쿼리하는 방법을 보여 줍니다.  
  
 [분할](method-based-query-syntax-examples-partitioning-linq.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.Skip%2A> 및 <xref:System.Linq.Enumerable.Take%2A> 메서드를 사용하여 <xref:System.Data.DataSet>을 쿼리하고 결과를 분할하는 방법을 보여 줍니다.  
  
 [정렬](method-based-query-syntax-examples-ordering-linq-to-dataset.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.OrderByDescending%2A>, <xref:System.Linq.Enumerable.Reverse%2A> 및 <xref:System.Linq.Enumerable.ThenByDescending%2A> 메서드를 사용하여 <xref:System.Data.DataSet>을 쿼리하고 결과를 정렬하는 방법을 보여 줍니다.  
  
 [집합 연산자](method-based-query-syntax-examples-set-operators.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Except%2A>, <xref:System.Linq.Enumerable.Intersect%2A> 및 <xref:System.Linq.Enumerable.Union%2A> 연산자를 사용하여 데이터 행 집합에 대해 값 기반 비교 연산을 수행하는 방법을 보여 줍니다.  
  
 [변환 연산자](method-based-query-syntax-examples-conversion-operators.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.ToArray%2A>, <xref:System.Linq.Enumerable.ToDictionary%2A> 및 <xref:System.Linq.Enumerable.ToList%2A> 메서드를 사용하여 쿼리 식을 즉시 실행하는 방법을 보여 줍니다.  
  
 [요소 연산자](method-based-query-syntax-examples-element-operators.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.First%2A> 및 <xref:System.Linq.Enumerable.ElementAt%2A> 메서드를 사용하여 <xref:System.Data.DataRow>에서 <xref:System.Data.DataSet> 요소를 가져오는 방법을 보여 줍니다.  
  
 [집계 연산자](method-based-query-syntax-examples-aggregate-operators.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.Max%2A>, <xref:System.Linq.Enumerable.Min%2A> 및 <xref:System.Linq.Enumerable.Sum%2A> 메서드를 사용하여 <xref:System.Data.DataSet>을 쿼리하고 데이터를 집계하는 방법을 보여 줍니다.  
  
 [Join](method-based-query-syntax-examples-join-linq-to-dataset.md)  
 이 항목의 예제에서는 <xref:System.Linq.Enumerable.GroupJoin%2A> 및 <xref:System.Linq.Enumerable.Join%2A> 메서드를 사용하여 <xref:System.Data.DataSet>을 쿼리하는 방법을 보여 줍니다.  
  
## <a name="see-also"></a>참고자료

- [쿼리 식 예제](query-expression-examples-linq-to-dataset.md)
- [DataSet별 연산자 예제](dataset-specific-operator-examples-linq-to-dataset.md)
- [LINQ to DataSet 예제](linq-to-dataset-examples.md)
