---
title: LINQ 쿼리 소개(C#)
ms.date: 07/20/2015
helpviewer_keywords:
- deferred execution [LINQ]
- LINQ, queries
- LINQ, deferred execution
- queries [LINQ], about LINQ queries
ms.assetid: 37895c02-268c-41d5-be39-f7d936fa88a8
ms.openlocfilehash: 6188af0ffea699899212e4bcf20b7c19f68858b4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924342"
---
# <a name="introduction-to-linq-queries-c"></a>LINQ 쿼리 소개(C#)
*쿼리*는 데이터 소스에서 데이터를 검색하는 식입니다. 쿼리는 일반적으로 특수화된 쿼리 언어로 표현됩니다. 관계형 데이터베이스에는 SQL이 사용되고 XML에는 XQuery가 사용되는 것처럼 시간에 따라 다양한 형식의 데이터 소스에 대해 서로 다른 언어가 개발되었습니다. 따라서 개발자는 지원해야 하는 데이터 소스의 형식이나 데이터 형식에 따라 새로운 쿼리 언어를 배워야 했습니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]는 다양한 데이터 소스 및 형식에 사용할 수 있는 일관된 모델을 제공함으로써 이러한 상황을 간단하게 합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리에서는 항상 개체를 사용하고 있습니다. XML 문서, SQL 데이터베이스, ADO.NET 데이터 세트, .NET 컬렉션 및 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자를 사용할 수 있는 다른 모든 형식에서 데이터를 쿼리하고 변환하는 데 동일한 기본 코딩 패턴을 사용합니다.  
  
## <a name="three-parts-of-a-query-operation"></a>쿼리 작업의 세 부분  
 모든 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 작업은 다음과 같은 세 가지 고유한 작업으로 구성됩니다.  
  
1. 데이터 소스 가져오기.  
  
2. 쿼리 만들기.  
  
3. 쿼리 실행.  
  
 다음 예제에서는 쿼리 작업의 세 부분이 소스 코드로 표현되는 방식을 보여 줍니다. 예제에서는 편의상 정수 배열을 데이터 소스로 사용하지만 다른 데이터 소스에도 동일한 개념이 적용됩니다. 이 예제는 이 항목의 나머지 부분 전체에서 참조됩니다.  
  
 [!code-csharp[CsLINQGettingStarted#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#1)]  
  
 다음 그림에서는 전체 쿼리 작업을 보여 줍니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에서는 쿼리 실행이 쿼리 자체와 구분됩니다. 즉, 쿼리 변수를 만드는 것만으로 데이터가 검색되지는 않습니다.  
  
 ![전체 LINQ 쿼리 작업의 다이어그램](./media/introduction-to-linq-queries/linq-query-complete-operation.png)  
  
## <a name="the-data-source"></a>데이터 소스  
 이전 예제에서는 데이터 소스가 배열이기 때문에 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 암시적으로 지원합니다. 즉, [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]로 쿼리할 수 있다는 의미입니다. 쿼리가 `foreach` 문에서 실행되고, `foreach`는 <xref:System.Collections.IEnumerable> 또는 <xref:System.Collections.Generic.IEnumerable%601>이 필요합니다. <xref:System.Collections.Generic.IEnumerable%601> 또는 제네릭 <xref:System.Linq.IQueryable%601> 같은 파생된 인터페이스를 지원하는 형식을 *쿼리 가능 형식*이라고 합니다.  
  
 쿼리 가능 형식은 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 데이터 소스로 사용하기 위해 수정하거나 특별하게 처리할 필요가 없습니다. 소스 데이터가 쿼리 가능 형식으로 메모리에 나타나지 않을 경우 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자는 그렇게 나타내야 합니다. 예를 들어 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]는 XML 문서를 쿼리 가능 <xref:System.Xml.Linq.XElement> 형식으로 로드합니다.  
  
 [!code-csharp[CsLINQGettingStarted#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#2)]  
  
 먼저 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]을 사용하여 디자인 타임에 수동으로 또는 Visual Studio에서 [Visual Studio의 LINQ to SQL 도구](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)를 사용하여 개체 관계형 매핑을 만듭니다. 개체에 대해 쿼리를 작성하면 런타임에 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]에서 데이터베이스와의 통신을 처리합니다. 다음 예에서 `Customers`는 데이터베이스의 특정 테이블을 나타내며, <xref:System.Linq.IQueryable%601> 쿼리 결과 형식은 <xref:System.Collections.Generic.IEnumerable%601>에서 파생됩니다.  
  
```csharp  
Northwnd db = new Northwnd(@"c:\northwnd.mdf");  
  
// Query for customers in London.  
IQueryable<Customer> custQuery =  
    from cust in db.Customers  
    where cust.City == "London"  
    select cust;  
```  
  
 특정 형식의 데이터 소스를 만드는 방법에 대한 자세한 내용은 다양한 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자에 대한 설명서를 참조하세요. 그러나 기본 규칙은 아주 간단합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 데이터 소스는 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스 또는 이 인터페이스에서 상속된 인터페이스를 지원하는 모든 개체입니다.  
  
> [!NOTE]
> 제네릭이 아닌 <xref:System.Collections.IEnumerable> 인터페이스를 지원하는 <xref:System.Collections.ArrayList> 같은 형식은 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 데이터 소스로도 사용됩니다. 자세한 내용은 [방법: LINQ를 사용하여 ArrayList 쿼리(C#)](./how-to-query-an-arraylist-with-linq.md)를 참조하세요.  
  
## <a name="query"></a> 쿼리  
 쿼리는 데이터 소스 또는 소스에서 검색할 정보를 지정합니다. 필요한 경우 쿼리는 정보를 반환하기 전에 해당 정보를 정렬, 그룹화 및 구체화하는 방법도 지정합니다. 쿼리는 쿼리 변수에 저장되고 쿼리 식으로 초기화됩니다. 쿼리를 쉽게 작성할 수 있도록 C#에서는 새로운 쿼리 구문이 도입되었습니다.  
  
 이전 예제의 쿼리는 정수 배열에서 모든 짝수를 반환합니다. 쿼리 식에는 `from`, `where` 및 `select`의 세 가지 절이 포함됩니다. SQL에 익숙한 경우 절의 순서가 SQL의 순서와 반대임을 알고 있을 것입니다. `from` 절은 데이터 소스를 지정하고 `where` 절은 필터를 적용하며 `select` 절은 반환되는 요소의 형식을 지정합니다. 이러한 쿼리 절 및 다른 쿼리 절은 [LINQ 쿼리 식](../../linq-query-expressions/index.md) 섹션에서 자세히 설명합니다. 여기에서 중요한 점은 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에서 쿼리 변수 자체는 아무 작업도 수행하지 않고 데이터를 반환하지 않는다는 것입니다. 나중에 쿼리가 실행될 때 결과를 생성하는 데 필요한 정보를 저장합니다. 백그라운드에서 쿼리를 생성하는 방법에 대한 자세한 내용은 [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)를 참조하세요.  
  
> [!NOTE]
> 쿼리는 메서드 구문을 사용하여 표현할 수도 있습니다. 자세한 내용은 [LINQ의 쿼리 구문 및 메서드 구문](./query-syntax-and-method-syntax-in-linq.md)을 참조하세요.  
  
## <a name="query-execution"></a>쿼리 실행  
  
### <a name="deferred-execution"></a>지연된 실행  
 앞에서 설명한 대로 쿼리 변수 자체는 쿼리 명령을 저장할 뿐입니다. 실제 쿼리 실행은 `foreach` 문에서 쿼리 변수가 반복될 때까지 지연됩니다. 이 개념을 *지연된 실행*이라고 하며 다음 예제에서 보여 줍니다.  
  
 [!code-csharp[csLinqGettingStarted#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#4)]  
  
 `foreach` 문은 쿼리 결과가 검색되는 위치이기도 합니다. 예를 들어 이전 쿼리에서 반복 변수 `num`은 반환된 시퀀스에서 각 값을 한 번에 하나씩 저장합니다.  
  
 쿼리 변수 자체는 쿼리 결과를 저장하지 않으므로 원하는 만큼 자주 실행할 수 있습니다. 예를 들어 별도의 애플리케이션에서 지속적으로 업데이트되는 데이터베이스가 있을 수 있습니다. 이 애플리케이션에서 최근 데이터를 검색하는 쿼리를 작성하고 이를 일정 간격을 두고 반복적으로 실행하여 매번 다른 결과를 검색할 수 있습니다.  
  
### <a name="forcing-immediate-execution"></a>즉시 실행 강제 적용  
 소스 요소 범위에 대해 집계 함수를 수행하는 쿼리는 먼저 해당 요소를 반복해야 합니다. 이러한 쿼리의 예로 `Count`, `Max`, `Average` 및 `First`가 있습니다. 이러한 쿼리는 쿼리 자체에서 결과를 반환하려면 `foreach`를 사용해야 하기 때문에 명시적 `foreach` 문 없이 실행됩니다. 또한 이러한 유형의 쿼리는 `IEnumerable` 컬렉션이 아니라 단일 값을 반환합니다. 다음 쿼리는 소스 배열에서 짝수의 개수를 반환합니다.  
  
 [!code-csharp[csLinqGettingStarted#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#5)]  
  
 모든 쿼리를 즉시 실행하고 그 결과를 캐시하기 위해 <xref:System.Linq.Enumerable.ToList%2A> 또는 <xref:System.Linq.Enumerable.ToArray%2A> 메서드를 호출할 수 있습니다.  
  
 [!code-csharp[csLinqGettingStarted#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#6)]  
  
 또한 `foreach` 루프를 쿼리 식 바로 다음에 배치하여 강제로 실행할 수 있습니다. 그러나 `ToList` 또는 `ToArray`를 호출하여 단일 컬렉션 개체에서 모든 데이터를 캐시할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [C#에서 LINQ 시작](./getting-started-with-linq.md)
- [연습: C#에서 쿼리 작성](./walkthrough-writing-queries-linq.md)
- [LINQ 쿼리 식](../../linq-query-expressions/index.md)
- [foreach, in](../../../language-reference/keywords/foreach-in.md)
- [쿼리 키워드(LINQ)](../../../language-reference/keywords/query-keywords.md)
