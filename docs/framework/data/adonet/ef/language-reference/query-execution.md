---
title: 쿼리 실행
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c0e6cf23-63ac-47dd-bfe9-d5bdca826fac
ms.openlocfilehash: fcf0d3eed95d36f7764ca048da62b589779d8d47
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249544"
---
# <a name="query-execution"></a>쿼리 실행
LINQ 쿼리가 사용자에 의해 작성되고 나면 명령 트리로 변환됩니다. 명령 트리란 Entity Framework에 호환되는 쿼리 표현입니다. 변환된 명령 트리는 데이터 소스에 대해 실행됩니다. 쿼리 실행 시 모든 쿼리 식, 다시 말해서 쿼리의 모든 구성 요소가 계산되며 여기에는 결과 구체화에서 사용되는 식도 포함됩니다.  
  
 쿼리 식이 실행되는 시점은 다양할 수 있습니다. LINQ 쿼리는 쿼리 변수가 만들어질 때 실행되는 것이 아니라 쿼리 변수가 반복될 때마다 실행됩니다. 이를 *지연 된 실행*이라고 합니다. 쿼리를 즉시 실행할 수도 있습니다. 이 방법은 쿼리 결과를 캐시하는 데 유용합니다. 쿼리 즉시 실행에 대해서는 이 항목 뒷부분에서 설명합니다.  
  
 LINQ to Entities 쿼리를 실행하면 쿼리의 일부 식은 서버에서 실행되고 일부 식은 클라이언트에서 로컬로 실행될 수 있습니다. 식에 대한 클라이언트 쪽 계산은 쿼리가 서버에서 실행되기 전에 수행됩니다. 식이 클라이언트에서 계산되면 계산 결과로 쿼리의 식이 대체된 다음 서버에서 쿼리가 실행됩니다. 쿼리가 데이터 소스에서 실행되므로 데이터 소스 구성이 클라이언트에 지정된 동작을 재정의합니다. 예를 들어, null 값 처리 및 숫자의 전체 자릿수는 서버 설정에 따라 달라집니다. 서버에서 쿼리를 실행하는 중에 throw되는 모든 예외는 클라이언트에 직접 전달됩니다.  
 
> [!TIP]
> 연산자의 실행 동작을 신속 하 게 식별할 수 있도록 하는 테이블 형식의 쿼리 연산자에 대 한 편리한 요약은 [실행 방식에 따라 표준 쿼리 연산자 분류 (C#)](../../../../../csharp/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)를 참조 하세요.

## <a name="deferred-query-execution"></a>지연된 쿼리 실행  
 값 시퀀스를 반환하는 쿼리의 경우 쿼리 변수 자체에는 쿼리 결과가 저장되지 않고 쿼리 명령만 저장됩니다. 쿼리 실행은 `foreach` 또는 `For Each` 루프에서 쿼리 변수가 반복될 때까지 지연됩니다. 이를 지연 된 *실행*이라고 합니다. 즉, 쿼리를 생성 한 후 쿼리가 실행 됩니다. 즉, 원하는 때에 언제라도 쿼리를 실행할 수 있습니다. 예를 들어, 이 기능은 다른 애플리케이션에서 업데이트되는 데이터베이스가 있을 때 유용합니다. 사용자의 애플리케이션에서 최신 정보를 검색하는 쿼리를 만든 다음 쿼리를 반복적으로 실행하여 업데이트된 정보를 항상 반환할 수 있습니다.  
  
 지연된 실행은 여러 쿼리를 결합하거나 하나의 쿼리를 확장 가능하게 합니다. 확장된 쿼리는 새 작업을 포함할 수 있도록 수정되며, 실행 결과에 변경 사항이 반영됩니다. 다음 예제의 첫 번째 쿼리에서는 모든 제품을 반환합니다. 두 번째 쿼리에서는 `Where`를 사용하여 첫 번째 쿼리를 확장하고 크기가 "L"인 모든 제품을 반환합니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#Composing1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#composing1)]
 [!code-vb[DP L2E Conceptual Examples#Composing1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#composing1)]  
  
 쿼리를 실행한 이후의 모든 쿼리에서는 메모리 내 LINQ 연산자를 사용합니다. `foreach` 또는 `For Each` 문을 사용하거나 LINQ 변환 연산자를 호출하는 방법으로 쿼리 변수를 반복하면 즉시 실행됩니다. 이러한 변환 연산자에는 <xref:System.Linq.Enumerable.ToList%2A>, <xref:System.Linq.Enumerable.ToArray%2A>, <xref:System.Linq.Enumerable.ToLookup%2A> 및 <xref:System.Linq.Enumerable.ToDictionary%2A>가 있습니다.  
  
## <a name="immediate-query-execution"></a>즉시 쿼리 실행  
 값 시퀀스를 반환하는 쿼리의 지연된 실행과는 달리, singleton 값을 반환하는 쿼리는 즉시 실행됩니다. singleton 쿼리의 예로는 <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.First%2A> 및 <xref:System.Linq.Enumerable.Max%2A>가 있습니다. singleton 결과를 계산하려면 쿼리에서 시퀀스를 생성해야 하므로 이러한 쿼리는 즉시 실행됩니다. 즉시 실행을 강제할 수도 있습니다. 이 기능은 쿼리 결과를 캐시하려는 경우에 유용합니다. singleton 값을 생성하지 않는 쿼리를 즉시 실행하려면 쿼리나 쿼리 변수에 대해 <xref:System.Linq.Enumerable.ToList%2A> 메서드, <xref:System.Linq.Enumerable.ToDictionary%2A> 메서드 또는 <xref:System.Linq.Enumerable.ToArray%2A> 메서드를 호출하면 됩니다. 다음 예제에서는 <xref:System.Linq.Enumerable.ToArray%2A> 메서드로 시퀀스를 즉시 계산하여 배열에 넣습니다.  
  
 [!code-csharp[DP L2E Examples#ToArray](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#toarray)]
 [!code-vb[DP L2E Examples#ToArray](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#toarray)]  
  
 쿼리 식 바로 다음에 `foreach` 또는 `For Each` 루프를 배치하는 방법으로 강제 실행할 수도 있습니다. 하지만 <xref:System.Linq.Enumerable.ToList%2A> 또는 <xref:System.Linq.Enumerable.ToArray%2A>를 호출하면 모든 데이터를 단일 컬렉션 개체에 캐시하게 됩니다.  
  
## <a name="store-execution"></a>저장소 실행  
 일반적으로 LINQ to Entities의 식은 서버에서 계산되며, 식의 동작은 CLR(공용 언어 런타임) 의미 체계가 아니라 데이터 소소의 의미 체계를 따릅니다. 하지만 식을 클라이언트에서 실행하는 경우 등에서는 예외가 있습니다. 이런 경우 서버와 클라이언트의 시간대가 다르면 예기치 않은 결과가 나올 수 있습니다.  
  
 쿼리의 일부 식은 클라이언트에서 실행될 수 있습니다. 일반적으로 쿼리 실행은 대부분 서버에서 발생합니다. 데이터 소스에 매핑된 쿼리 요소에 대해 실행되는 메서드와 별도로 로컬에서 실행 가능한 쿼리 식이 종종 있습니다. 쿼리 식을 로컬에서 실행하면 쿼리 실행 또는 결과 생성에 사용할 수 있는 값이 반환됩니다.  
  
 클로저의 값, 하위 식, 하위 쿼리 바인딩 및 개체를 쿼리 결과로 구체화하는 작업 등 특정 작업은 항상 클라이언트에서 실행됩니다. 이렇게 하면 실행 과정에서 매개 변수 값과 같은 요소가 업데이트될 수 없습니다. 익명 형식이 인라인으로 데이터 소스에 생성될 수 있지만 그럴 것이라고 가정하지 않는 것이 좋습니다. 데이터 소스에서 인라인 그룹화를 생성할 수도 있지만 모든 인스턴스에서 그럴 것이라고 가정하면 안 됩니다. 일반적으로 서버에서 생성되는 항목에 대해 어떤 가정도 하지 않는 것이 좋습니다.  
  
 이 단원에서는 코드가 클라이언트에서 로컬로 실행되는 시나리오에 대해 설명합니다. 로컬로 실행 되는 식 형식에 대 한 자세한 내용은 [LINQ to Entities 쿼리의 식](expressions-in-linq-to-entities-queries.md)을 참조 하세요.  
  
### <a name="literals-and-parameters"></a>리터럴 및 매개 변수  
 다음 예제의 `orderID` 변수와 같은 지역 변수는 클라이언트에서 계산됩니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#LiteralParameter1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#literalparameter1)]
 [!code-vb[DP L2E Conceptual Examples#LiteralParameter1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#literalparameter1)]  
  
 메서드 매개 변수 또한 클라이언트에서 계산됩니다. 다음에서 `orderID` 메서드에 전달된 `MethodParameterExample` 매개 변수를 예제로 들 수 있습니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#MethodParameterExample](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#methodparameterexample)]
 [!code-vb[DP L2E Conceptual Examples#MethodParameterExample](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#methodparameterexample)]  
  
### <a name="casting-literals-on-the-client"></a>클라이언트에서 리터럴 캐스팅  
 `null`에서 CLR 형식으로의 캐스팅이 클라이언트에서 실행됩니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#NullCastToString](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#nullcasttostring)]
 [!code-vb[DP L2E Conceptual Examples#NullCastToString](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#nullcasttostring)]  
  
 특정 형식(예: null을 허용하는 <xref:System.Decimal>)으로의 캐스팅이 클라이언트에서 실행됩니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#CastToNullable](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#casttonullable)]
 [!code-vb[DP L2E Conceptual Examples#CastToNullable](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#casttonullable)]  
  
### <a name="constructors-for-literals"></a>리터럴의 생성자  
 개념적 모델 형식으로 매핑 가능한 새로운 CLR 형식이 클라이언트에서 실행됩니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#ConstructorForLiteral](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#constructorforliteral)]
 [!code-vb[DP L2E Conceptual Examples#ConstructorForLiteral](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#constructorforliteral)]  
  
 새 배열 또한 클라이언트에서 실행됩니다.  
  
## <a name="store-exceptions"></a>저장소 예외  
 쿼리 실행 과정에서 발생하는 저장소 오류는 클라이언트에 전달되며 매핑이나 처리가 이루어지지 않습니다.  
  
## <a name="store-configuration"></a>저장소 구성  
 쿼리가 저장소에 대해 실행되면 저장소 구성이 모든 클라이언트 동작을 재정의하며 모든 연산과 식에 대해 저장소 의미 체계가 표현됩니다. 이로 인해 null 비교, GUID 정렬, 명확하지 않은 데이터 형식(예: 부동 소수점 형식 또는 <xref:System.DateTime>) 연산의 정밀도와 정확도, 문자열 작업 등의 영역에서 CLR 실행과 저장소 실행의 동작이 서로 다를 수 있습니다. 쿼리 결과를 검토할 때는 이 점을 염두에 두어야 합니다.  
  
 예를 들어 다음은 CLR과 SQL Server 사이의 몇 가지 동작 차이점입니다.  
  
- SQL Server의 GUID 정렬은 CLR에서와 다릅니다.  
  
- SQL Server에서 Decimal 형식을 처리할 때 결과 전체 자릿수도 다를 수 있습니다. 이것은 SQL Server Decimal 형식의 고정 전체 자릿수 요구 사항 때문입니다. 예를 들어, <xref:System.Decimal> 값 0.0, 0.0, 1.0의 평균은 클라이언트 메모리에서 0.3333333333333333333333333333이지만 저장소에서는 SQL Server의 Decimal 형식에 대한 기본 전체 자릿수에 따라 0.333333입니다.  
  
- 일부 문자열 비교 연산도 SQL Server와 CLR에서 다르게 처리됩니다. 문자열 비교 동작은 서버의 정렬 설정에 따라 달라집니다.  
  
- LINQ to Entities 쿼리에 포함된 함수 또는 메서드 호출은 Entity Framework의 정식 함수에 매핑된 후 Transact-SQL로 변환되어 SQL Server 데이터베이스에서 실행됩니다. 이런 매핑된 함수의 동작이 기본 클래스 라이브러리에 구현된 것과 다른 경우가 있습니다. 예를 들어, 빈 문자열을 매개 변수로 하여 <xref:System.String.Contains%2A>, <xref:System.String.StartsWith%2A> 및 <xref:System.String.EndsWith%2A> 메서드를 호출하면 CLR에서 실행했을 때는 `true`가, SQL Server에서 실행했을 때는 `false`가 반환됩니다. <xref:System.String.EndsWith%2A> 메서드 역시 다른 결과를 반환할 수 있으며, 이는 SQL Server에서는 후행 공백만 다르면 두 문자열을 동일한 것으로 간주하는 데 비하여 CLR에서는 동일하지 않은 것으로 간주하기 때문입니다. 다음 예제에서 이를 확인할 수 있습니다.  
  
 [!code-csharp[DP L2E Conceptual Examples#CanonicalFuncVsCLRBaseType](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#canonicalfuncvsclrbasetype)]
 [!code-vb[DP L2E Conceptual Examples#CanonicalFuncVsCLRBaseType](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#canonicalfuncvsclrbasetype)]
