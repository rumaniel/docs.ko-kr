---
title: C#의 LINQ(Language-Integrated Query)
description: C#의 LINQ(Language-Integrated Query) 소개
ms.date: 11/30/2016
ms.assetid: 007cc736-f5cf-4919-b99b-0c00ab2814ce
ms.openlocfilehash: fe408210b30b5f6118dc66b4c8f7057fb6654881
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66482985"
---
# <a name="language-integrated-query-linq"></a>LINQ(Language-Integrated Query)

LINQ(Language-Integrated Query)는 C# 언어에 직접 쿼리 기능을 통합하는 방식을 기반으로 하는 기술 집합 이름입니다. 일반적으로 데이터에 대한 쿼리는 컴파일 시간의 형식 검사나 IntelliSense 지원 없이 간단한 문자열로 표현됩니다. 또한 데이터 원본의 각 유형에 대해 다른 쿼리 언어를 배워야 합니다. SQL 데이터베이스, XML 문서, 다양한 웹 서비스 등. LINQ를 사용할 경우 쿼리는 클래스, 메서드, 이벤트와 같은 고급 언어 구문이 됩니다.

쿼리를 작성하는 개발자의 경우 LINQ에서 가장 눈에 잘 띄는 "언어 통합" 부분은 쿼리 식입니다. 쿼리 식은 선언적 *쿼리 구문*으로 작성됩니다. 쿼리 구문을 사용하면 최소한의 코드로 데이터 소스에 대해 필터링, 정렬 및 그룹화 작업을 수행할 수 있습니다. 동일한 기본 쿼리 식 패턴을 사용하여 SQL 데이터베이스, ADO .NET 데이터 세트, XML 문서 및 스트림, .NET 컬렉션에서 데이터를 쿼리하고 변환할 수 있습니다.

다음 예제에서는 전체 쿼리 작업을 보여 줍니다. 전체 작업에는 데이터 소스 만들기, 쿼리 식 정의 및 `foreach` 문의 쿼리 실행이 포함됩니다.

[!code-csharp[csProgGuideLINQ#11](~/samples/snippets/csharp/concepts/linq/index_1.cs)]

## <a name="query-expression-overview"></a>쿼리 식 개요

- 쿼리 식은 LINQ 사용 데이터 소스에서 데이터를 쿼리하고 변환하는 데 사용할 수 있습니다. 예를 들어 단일 쿼리로 SQL 데이터베이스에서 데이터를 검색하고 XML 스트림을 출력으로 생성할 수 있습니다.

- 쿼리 식은 익숙한 C# 언어 구문을 많이 사용하기 때문에 쉽게 마스터할 수 있습니다.

- 대부분의 경우 컴파일러가 형식을 유추할 수 있기 때문에 명시적으로 형식을 제공할 필요는 없지만 쿼리 식의 변수는 모두 강력한 형식을 갖습니다. 자세한 내용은 [LINQ 쿼리 작업의 형식 관계](../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)를 참조하세요.

- 쿼리는 쿼리 변수를 반복할 때까지(예: `foreach` 문) 실행되지 않습니다. 자세한 내용은 [LINQ 쿼리 소개](../programming-guide/concepts/linq/introduction-to-linq-queries.md)를 참조하세요.

- 컴파일 타임에 쿼리 식은 C# 사양에 명시된 규칙에 따라 표준 쿼리 연산자 메서드 호출으로 변환됩니다. 쿼리 구문을 사용하여 표현할 수 있는 모든 쿼리는 메서드 구문으로도 표현할 수 있습니다. 그러나 대부분의 경우 쿼리 구문이 더 읽기 쉽고 간결합니다. 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/expressions.md#query-expressions) 및 [표준 쿼리 연산자 개요](../programming-guide/concepts/linq/standard-query-operators-overview.md)를 참조하세요.

- 일반적으로 LINQ 쿼리를 작성하는 경우 가능하면 쿼리 구문을 사용하고 필요한 경우 메서드 구문을 사용하는 것이 좋습니다. 두 개의 다른 폼 간에 의미 체계 또는 성능상의 차이는 없습니다. 쿼리 식이 메서드 구문으로 작성된 동급의 식보다 읽기 쉬운 경우가 많습니다.

- <xref:System.Linq.Enumerable.Count%2A> 또는 <xref:System.Linq.Enumerable.Max%2A>와 같은 일부 쿼리 작업은 해당하는 쿼리 식 절이 없으므로 메서드 호출로 표현해야 합니다. 메서드 구문을 다양한 방법으로 쿼리 구문에 조합할 수 있습니다. 자세한 내용은 [쿼리 구문과 메서드 구문 비교](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)를 참조하세요.

- 쿼리 식은 쿼리가 적용되는 형식에 따라 식 트리 또는 대리자로 컴파일될 수 있습니다. <xref:System.Collections.Generic.IEnumerable%601> 쿼리는 대리자로 컴파일됩니다. <xref:System.Linq.IQueryable> 및 <xref:System.Linq.IQueryable%601> 쿼리는 식 트리로 컴파일됩니다. 자세한 내용은 [식 트리](../expression-trees.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

LINQ에 대한 자세한 내용을 알아보려면 [쿼리 식 기본 사항](query-expression-basics.md)에서 몇 가지 기본 개념을 익힌 후 관심 있는 LINQ 기술에 대한 설명서를 읽어보세요.

- XML 문서: [LINQ to XML](../programming-guide/concepts/linq/linq-to-xml-overview.md)

- ADO.NET Entity Framework: [LINQ to Entities](../../framework/data/adonet/ef/language-reference/linq-to-entities.md)

- .NET 컬렉션, 파일, 문자열 등: [LINQ to Objects](../programming-guide/concepts/linq/linq-to-objects.md)

LINQ를 보다 깊이 있게 이해하려면 [C#의 LINQ](linq-in-csharp.md)를 참조하세요.

C#에서 LINQ를 사용하려면 자습서 [LINQ 작업](../tutorials/working-with-linq.md)을 참조하세요.
