---
title: LINQ to Entities에서 쿼리
ms.date: 03/30/2017
ms.assetid: c015a609-29eb-4e95-abb1-2ca721c6e2ad
ms.openlocfilehash: 561fa3217a80a8437b7c4d175d5a1156096ac241
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249567"
---
# <a name="queries-in-linq-to-entities"></a>LINQ to Entities에서 쿼리
쿼리는 데이터 소스에서 데이터를 검색하는 식입니다. 관계형 데이터베이스에는 SQL이 사용되고 XML에는 XQuery가 사용되는 것과 같이 쿼리는 일반적으로 특수화된 쿼리 언어로 표현됩니다. 따라서 개발자는 쿼리하는 데이터 소스나 데이터 형식에 따라 새로운 쿼리 언어를 배워야 했습니다. LINQ(Language-Integrated Query)는 다양한 데이터 소스 및 형식에 사용할 수 있는 간단하고 일관된 모델을 제공합니다. LINQ 쿼리에서는 항상 프로그래밍 개체가 사용됩니다.  
  
 LINQ 쿼리 작업은 데이터 소스 가져오기, 쿼리 만들기 및 쿼리 실행으로 구성됩니다.  
  
 <xref:System.Collections.Generic.IEnumerable%601> 제네릭 인터페이스 또는 <xref:System.Linq.IQueryable%601> 제네릭 인터페이스를 구현하는 데이터 소스는 LINQ를 통해 쿼리할 수 있습니다. <xref:System.Data.Objects.ObjectQuery%601> 제네릭<xref:System.Linq.IQueryable%601> 인터페이스를 구현 하는 제네릭 클래스의 인스턴스는 LINQ to Entities 쿼리의 데이터 원본 역할을 합니다. <xref:System.Data.Objects.ObjectQuery%601> 제네릭 클래스는 0개 이상의 형식화된 개체로 구성된 컬렉션을 반환하는 쿼리를 나타냅니다. C# 키워드`var` (Dim in Visual Basic)를 사용 하 여 컴파일러가 엔터티 형식을 유추 하도록 할 수도 있습니다.  
  
 쿼리에는 데이터 소스에서 검색하려는 정보를 정확히 지정해야 합니다. 또한 정보를 반환하기 전에 정보에 대한 정렬, 그룹화 및 구체화하는 방법을 쿼리에 지정할 수 있습니다. LINQ에서 쿼리는 변수에 저장됩니다. 값 시퀀스를 반환하는 쿼리의 경우에는 쿼리 변수 자체가 쿼리 가능한 형식이어야 합니다. 이 쿼리 변수는 어떠한 작업을 수행하거나 데이터를 반환하지 않고 쿼리 정보를 저장하기만 합니다. 쿼리를 만든 후에는 해당 쿼리를 실행하여 데이터를 검색해야 합니다.  
  
## <a name="query-syntax"></a>쿼리 구문  
 LINQ to Entities 쿼리는 쿼리 식 구문과 메서드 기반 쿼리 구문이라는 두 가지 구문으로 작성할 수 있습니다. 쿼리 식 구문은 C# 3.0과 Visual Basic 9.0에 새로 도입된 것으로서 Transact-SQL 또는 XQuery와 유사한 선언적 구문으로 작성된 일련의 절로 구성되어 있습니다. 그러나 .NET Framework CLR (공용 언어 런타임)에서는 쿼리 식 구문 자체를 읽을 수 없습니다. 따라서 컴파일 타임에 쿼리 식은 CLR에서 인식할 수 있는 메서드 호출로 변환됩니다. 이러한 메서드를 *표준 쿼리 연산자*라고 합니다. 개발자는 쿼리 구문을 사용하는 대신 메서드 구문을 사용하여 표준 쿼리 연산자를 직접 호출할 수도 있습니다. 자세한 내용은 [LINQ의 쿼리 구문 및 메서드 구문](../../../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)을 참조하세요.  
  
### <a name="query-expression-syntax"></a>쿼리 식 구문  
 쿼리 식은 선언적 쿼리 구문입니다. 이 구문을 사용하면 개발자는 Transact-SQL과 비슷한 높은 수준의 언어로 쿼리를 작성할 수 있습니다. 쿼리 식 구문을 사용하면 최소한의 코드로 데이터 소스에 대해 복잡한 필터링, 정렬 및 그룹화 작업을 수행할 수 있습니다. 자세한 내용은 [기본 쿼리 작업 (Visual Basic)을](../../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md). 쿼리 식 구문을 사용하는 방법을 보여 주는 예제는 다음 항목을 참조하세요.  
  
- [쿼리 식 구문 예제: Projection](query-expression-syntax-examples-projection.md)  
  
- [쿼리 식 구문 예제: 필터링](query-expression-syntax-examples-filtering.md)  
  
- [쿼리 식 구문 예제: 주](query-expression-syntax-examples-ordering.md)  
  
- [쿼리 식 구문 예제: 집계 연산자](query-expression-syntax-examples-aggregate-operators.md)  
  
- [쿼리 식 구문 예제: 파티션은](query-expression-syntax-examples-partitioning.md)  
  
- [쿼리 식 구문 예제: 조인 연산자](query-expression-syntax-examples-join-operators.md)  
  
- [쿼리 식 구문 예제: 요소 연산자](query-expression-syntax-examples-element-operators.md)  
  
- [쿼리 식 구문 예제: 묶어서](query-expression-syntax-examples-grouping.md)  
  
- [쿼리 식 구문 예제: 관계 탐색](query-expression-syntax-examples-navigating-relationships.md)  
  
### <a name="method-based-query-syntax"></a>메서드 기반 쿼리 구문  
 LINQ to Entities 쿼리를 작성 하는 또 다른 방법은 메서드 기반 쿼리를 사용 하는 것입니다. 메서드 기반 쿼리 구문은 람다 식을 매개 변수로 전달하는 LINQ 연산자 메서드에 대한 직접 메서드 호출의 시퀀스입니다. 자세한 내용은 [람다 식](../../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)을 참조하세요. 메서드 기반 구문을 사용하는 방법을 보여 주는 예제는 다음 항목을 참조하세요.  
  
- [메서드 기반 쿼리 구문 예제: Projection](method-based-query-syntax-examples-projection.md)  
  
- [메서드 기반 쿼리 구문 예제: 필터링](method-based-query-syntax-examples-filtering.md)  
  
- [메서드 기반 쿼리 구문 예제: 주](method-based-query-syntax-examples-ordering.md)  
  
- [메서드 기반 쿼리 구문 예제: 집계 연산자](method-based-query-syntax-examples-aggregate-operators.md)  
  
- [메서드 기반 쿼리 구문 예제: 파티션은](method-based-query-syntax-examples-partitioning.md)  
  
- [메서드 기반 쿼리 구문 예제: 변환할](method-based-query-syntax-examples-conversion.md)  
  
- [메서드 기반 쿼리 구문 예제: 조인 연산자](method-based-query-syntax-examples-join-operators.md)  
  
- [메서드 기반 쿼리 구문 예제: 요소 연산자](method-based-query-syntax-examples-element-operators.md)  
  
- [메서드 기반 쿼리 구문 예제: 묶어서](method-based-query-syntax-examples-grouping.md)  
  
- [메서드 기반 쿼리 구문 예제: 관계 탐색](method-based-query-syntax-examples-navigating-relationships.md)  
  
## <a name="see-also"></a>참고자료

- [LINQ to Entities](linq-to-entities.md)
- [C#에서 LINQ 시작](../../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)
- [Visual Basic에서 LINQ 시작](../../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [Entity Framework 병합 옵션 및 컴파일된 쿼리](https://go.microsoft.com/fwlink/?LinkId=199591)
