---
title: LINQ to Entities
ms.date: 03/30/2017
ms.assetid: 641f9b68-9046-47a1-abb0-1c8eaeda0e2d
ms.openlocfilehash: bc568cb9dff170062651c908471a36cd17eac980
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854372"
---
# <a name="linq-to-entities"></a>LINQ to Entities
LINQ to Entities에서는 개발자가 Visual Basic 또는 Visual C#을 사용하여 Entity Framework 개념적 모델에 대한 쿼리를 작성할 수 있도록 해 주는 LINQ(Language-Integrated Query) 지원을 제공합니다. Entity Framework에 대한 쿼리는 개체 컨텍스트에 대해 실행되는 명령 트리 쿼리로 표현됩니다. LINQ to Entities는 LINQ(Language-Integrated Query) 쿼리를 명령 트리 쿼리로 변환하여 Entity Framework에 대해 실행한 다음 Entity Framework와 LINQ에서 모두 사용할 수 있는 개체를 반환합니다. 다음은 LINQ to Entities 쿼리를 만들고 실행하는 프로세스입니다.  
  
1. <xref:System.Data.Objects.ObjectQuery%601>에서 <xref:System.Data.Objects.ObjectContext> 인스턴스를 생성합니다.  
  
2. <xref:System.Data.Objects.ObjectQuery%601> 인스턴스를 사용하여 LINQ to Entities 쿼리를 C# 또는 Visual Basic으로 작성합니다.  
  
3. LINQ 표준 쿼리 연산자 및 식을 명령 트리로 변환합니다.  
  
4. 명령 트리 표현에서 데이터 소스에 대해 쿼리를 실행합니다. 실행 중에 데이터 소스에서 throw되는 모든 예외는 클라이언트에게 직접 전달됩니다.  
  
5. 쿼리 결과를 다시 클라이언트에 반환합니다.  
  
## <a name="constructing-an-objectquery-instance"></a>ObjectQuery 인스턴스 생성  
 <xref:System.Data.Objects.ObjectQuery%601> 제네릭 클래스는 0개 이상의 형식화된 엔터티로 구성된 컬렉션을 반환하는 쿼리를 나타냅니다. 개체 쿼리는 수동으로 생성되는 대신 일반적으로 기존 개체 컨텍스트에서 생성되며 항상 해당 개체 컨텍스트에 속합니다. 이 컨텍스트는 쿼리를 작성하고 실행하는 데 필요한 연결 및 메타데이터 정보를 제공합니다. <xref:System.Data.Objects.ObjectQuery%601> 제네릭 클래스는 LINQ 쿼리를 증분 빌드할 수 있는 작성기 메서드를 가지고 있는 <xref:System.Linq.IQueryable%601> 제네릭 인터페이스를 구현합니다. C# `var` 키워드(Visual Basic에서는 로컬 형식 유추가 가능한 경우 `Dim`)를 사용하여 컴파일러에서 엔터티 형식을 유추하도록 할 수도 있습니다.  
  
## <a name="composing-the-queries"></a>쿼리 작성  
 <xref:System.Data.Objects.ObjectQuery%601> 제네릭 인터페이스를 구현하는 <xref:System.Linq.IQueryable%601> 제네릭 클래스의 인스턴스는 LINQ to Entities 쿼리의 데이터 소스 역할을 합니다. 쿼리에는 데이터 소스에서 검색하려는 정보를 정확히 지정해야 합니다. 또한 정보를 반환하기 전에 정보에 대한 정렬, 그룹화 및 구체화하는 방법을 쿼리에 지정할 수 있습니다. LINQ에서 쿼리는 변수에 저장됩니다. 이 쿼리 변수는 어떠한 작업을 수행하거나 데이터를 반환하지 않고 쿼리 정보를 저장하기만 합니다. 쿼리를 만든 후에는 해당 쿼리를 실행하여 데이터를 검색해야 합니다.  
  
 LINQ to Entities 쿼리는 쿼리 식 구문과 메서드 기반 쿼리 구문이라는 두 가지 구문으로 작성할 수 있습니다. 쿼리 식 구문과 메서드 기반 쿼리 구문은 C# 3.0과 Visual Basic 9.0의 새로운 기능입니다.  
  
 자세한 내용은 [LINQ to Entities의 쿼리](queries-in-linq-to-entities.md)를 참조 하세요.  
  
## <a name="query-conversion"></a>쿼리 변환  
 LINQ to Entities 쿼리를 Entity Framework에 대해 실행하려면 LINQ 쿼리를 Entity Framework에 대해 실행할 수 있는 명령 트리 표현으로 변환해야 합니다.  
  
 LINQ to Entities 쿼리는 LINQ 표준 쿼리 연산자 (예: <xref:System.Linq.Queryable.Select%2A>, <xref:System.Linq.Queryable.Where%2A>및 <xref:System.Linq.Queryable.GroupBy%2A>)와 식 (x > 10, Contact. LastName 등)으로 구성 됩니다. LINQ 연산자는 클래스로 정의되지 않으며 클래스에 있는 메서드입니다. LINQ에서 식은 <xref:System.Linq.Expressions> 네임스페이스 내의 형식에 허용되는 모든 항목을 포함할 수 있습니다. 확대하면 람다 함수로 표현할 수 있는 모든 항목을 포함할 수 있습니다. LINQ의 식은 <xref:System.Data.Objects.ObjectQuery%601>에서 지원되고 정의에 따라 데이터베이스에서 허용되는 연산으로 제한된 Entity Framework에서 허용되는 식의 상위 집합입니다.  
  
 Entity Framework에서는 연산자와 식이 모두 단일 형식 계층 구조로 표현된 다음 명령 트리에 배치됩니다. 명령 트리는 Entity Framework에서 쿼리를 실행하는 데 사용됩니다. LINQ 쿼리를 명령 트리로 표현할 수 없는 경우에는 쿼리를 변환할 때 예외가 throw됩니다. LINQ to Entities 쿼리를 변환하는 데는 표준 쿼리 연산자 변환과 식 변환이라는 두 가지 하위 변환이 수반됩니다.  
  
 많은 LINQ 표준 쿼리 연산자가 LINQ to Entities에서 올바르게 변환되지 않습니다. 이러한 연산자를 사용하면 쿼리를 변환할 때 예외가 발생합니다. 지원 되는 LINQ to Entities 연산자 목록은 [지원 되거나 지원 되지 않는 LINQ 메서드 (LINQ to Entities)](supported-and-unsupported-linq-methods-linq-to-entities.md)를 참조 하세요.  
  
 LINQ to Entities에서 표준 쿼리 연산자를 사용 하는 방법에 대 한 자세한 내용은 [LINQ to Entities 쿼리의 표준 쿼리 연산자](standard-query-operators-in-linq-to-entities-queries.md)를 참조 하세요.  
  
 일반적으로 LINQ to Entities의 식은 서버에서 계산되므로 식의 동작은 CLR 의미 체계를 따르지 않습니다. 자세한 내용은 [LINQ to Entities 쿼리의 식](expressions-in-linq-to-entities-queries.md)을 참조 하세요.  
  
 CLR 메서드 호출이 데이터 소스의 정식 함수에 매핑되는 방법에 대 한 자세한 내용은 [Clr method To 정식 함수 매핑](clr-method-to-canonical-function-mapping.md)을 참조 하세요.  
  
 LINQ to Entities 쿼리 내에서 정식, 데이터베이스 및 사용자 지정 함수를 호출 하는 방법에 대 한 자세한 내용은 [LINQ to Entities 쿼리에서 함수 호출](calling-functions-in-linq-to-entities-queries.md)을 참조 하세요.  
  
## <a name="query-execution"></a>쿼리 실행  
 사용자가 만든 LINQ 쿼리는 Entity Framework와 호환되는 표현(명령 트리 형태)으로 변환된 다음 데이터 소스에 대해 실행됩니다. 쿼리 실행 시 모든 쿼리 식(또는 쿼리의 구성 요소)은 클라이언트나 서버에서 계산됩니다. 이러한 식에는 결과 구체화나 엔터티 프로젝션에 사용되는 식이 포함됩니다. 자세한 내용은 [쿼리 실행](query-execution.md)을 참조 하세요. 쿼리를 한 번 컴파일한 다음 다른 매개 변수를 사용 하 여 여러 번 실행 하 여 성능을 향상 시키는 방법에 대 한 자세한 내용은 [컴파일된 쿼리 (LINQ to Entities)](compiled-queries-linq-to-entities.md)를 참조 하세요.  
  
## <a name="materialization"></a>구체화  
 구체화는 쿼리 결과를 CLR 형식으로 클라이언트에게 다시 반환하는 프로세스입니다. LINQ to Entities에서는 쿼리 결과 데이터 레코드가 반환되지 않으며 사용자나 Entity Framework에 의해 정의되었거나 컴파일러에 의해 생성된(익명 형식) 기본 CLR 형식이 항상 사용됩니다. 모든 개체 구체화는 Entity Framework에 의해 수행됩니다. Entity Framework와 CLR 간의 매핑 실패로 인해 오류가 발생하면 개체 구체화 동안 예외가 throw됩니다.  
  
 쿼리 결과는 대개 다음 중 하나로 반환됩니다.  
  
- 개념적 모델에 정의된 복합 형식의 프로젝션 또는 0개 이상의 형식화된 엔터티 개체가 포함된 컬렉션  
  
- Entity Framework에서 지 원하는 CLR 형식입니다.  
  
- 인라인 컬렉션  
  
- 익명 형식  
  
 자세한 내용은 [쿼리 결과](query-results.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [LINQ to Entities에서 쿼리](queries-in-linq-to-entities.md)  
  
 [LINQ to Entities 쿼리의 식](expressions-in-linq-to-entities-queries.md)  
  
 [LINQ to Entities 쿼리에서 함수 호출](calling-functions-in-linq-to-entities-queries.md)  
  
 [컴파일된 쿼리(LINQ to Entities)](compiled-queries-linq-to-entities.md)  
  
 [쿼리 실행](query-execution.md)  
  
 [쿼리 결과](query-results.md)  
  
 [LINQ to Entities 쿼리에서 표준 쿼리 연산자](standard-query-operators-in-linq-to-entities-queries.md)  
  
 [정식 함수 매핑에 대한 CLR 메서드](clr-method-to-canonical-function-mapping.md)  
  
 [지원 및 미지원 LINQ 메서드 (LINQ to Entities)](supported-and-unsupported-linq-methods-linq-to-entities.md)  
  
 [LINQ to Entities에서 알려진 문제 및 고려 사항](known-issues-and-considerations-in-linq-to-entities.md)  
  
## <a name="see-also"></a>참고자료

- [LINQ to Entities에서 알려진 문제 및 고려 사항](known-issues-and-considerations-in-linq-to-entities.md)
- [LINQ(Language-Integrated Query) - C#](../../../../../csharp/programming-guide/concepts/linq/index.md)
- [LINQ(Language-Integrated Query) - Visual Basic](../../../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ 및 ADO.NET](../../linq-and-ado-net.md)
- [ADO.NET Entity Framework](../index.md)
