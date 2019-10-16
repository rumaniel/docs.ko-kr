---
title: 표준 쿼리 연산자 변환
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a60c30fa-1e68-45fe-b984-f6abb9ede40e
ms.openlocfilehash: af22b6a895fef8037eb5c069ffb7cb23d1333531
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833675"
---
# <a name="standard-query-operator-translation"></a>표준 쿼리 연산자 변환

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 표준 쿼리 연산자를 SQL 명령으로 변환합니다. 데이터베이스의 쿼리 프로세서는 SQL 변환의 실행 의미를 결정 합니다.

표준 쿼리 연산자는 *시퀀스*에 대해 정의 됩니다. 시퀀스는 *순서가 지정* 되며 시퀀스의 각 요소에 대 한 참조 id를 사용 합니다. 자세한 내용은 [표준 쿼리 연산자 개요 (C#)](../../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md) 또는 [표준 쿼리 연산자 개요 (Visual Basic)](../../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)를 참조 하세요.

SQL은 정렬 되지 않은 *값 집합*을 주로 처리 합니다. 순서 지정은 일반적으로 명시적으로 지정되는 후처리 작업으로 쿼리의 중간 결과가 아닌 최종 결과에 적용됩니다. ID는 값으로 정의됩니다. 이러한 이유로 SQL 쿼리는 *집합*대신 다중 집합 (*백*)를 처리 하는 것을 인식 합니다.

다음 단락에서는 표준 쿼리 연산자와 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 SQL 서버 공급자에 대한 해당 SQL 변환 사이의 차이점에 대해 설명합니다.

## <a name="operator-support"></a>연산자 지원

### <a name="concat"></a>Concat

<xref:System.Linq.Enumerable.Concat%2A> 메서드는 수신자 순서와 인수 순서가 동일한 순서 있는 다중 집합에 대해 정의됩니다. <xref:System.Linq.Enumerable.Concat%2A>는 공통 순서 이전에 다중 집합에 대해 `UNION ALL`로 작동합니다.

최종 단계는 결과가 생성되기 전에 SQL에서 순서를 지정하는 단계입니다. <xref:System.Linq.Enumerable.Concat%2A>에서는 해당 인수의 순서를 유지하지 않습니다. 순서가 적절하게 지정되게 하려면 <xref:System.Linq.Enumerable.Concat%2A>에 대한 결과의 순서를 명시적으로 지정해야 합니다.

### <a name="intersect-except-union"></a>Intersect, Except, Union

<xref:System.Linq.Enumerable.Intersect%2A> 및 <xref:System.Linq.Enumerable.Except%2A> 메서드는 집합에 대해서만 잘 정의되어 있습니다. 다중 집합에 대한 의미 체계는 정의되어 있지 않습니다.

<xref:System.Linq.Enumerable.Union%2A> 메서드는 다중 집합에 대해 순서 없는 다중 집합의 연결로 정의됩니다(사실상 SQL UNION ALL 절의 결과와 같음).

### <a name="take-skip"></a>Take, Skip

<xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A> 메서드는 *정렬 된 집합*에 대해서만 잘 정의 됩니다. 순서 없는 집합이나 다중 집합에 대한 의미 체계는 정의되어 있지 않습니다.

> [!NOTE]
> <xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>에는 SQL Server 2000에 대한 쿼리에서 사용할 경우 몇 가지 제한이 따릅니다. 자세한 내용은 [문제 해결](troubleshooting.md)에서 "SQL Server 2000의 Skip 및 Take 예외" 항목을 참조 하세요.

SQL의 순서 지정에 대한 제한 사항 때문에 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 이러한 메서드의 인수에 대한 순서 지정 작업을 메서드의 결과로 이동하려고 합니다. 예를 들어 다음 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 쿼리를 살펴보세요.

[!code-csharp[DLinqSQOTranslation#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#1)]
[!code-vb[DLinqSQOTranslation#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#1)]

이 코드에 대해 생성된 SQL은 다음과 같이 순서 지정 작업을 맨 뒤로 옮깁니다.

```sql
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],
FROM [Customers] AS [t0]
WHERE (NOT (EXISTS(
    SELECT NULL AS [EMPTY]
    FROM (
        SELECT TOP 1 [t1].[CustomerID]
        FROM [Customers] AS [t1]
        WHERE [t1].[City] = @p0
        ORDER BY [t1].[CustomerID]
        ) AS [t2]
    WHERE [t0].[CustomerID] = [t2].[CustomerID]
    ))) AND ([t0].[City] = @p1)
ORDER BY [t0].[CustomerID]
```

<xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>을 연결할 때 지정한 모든 순서가 일치해야 함을 알 수 있습니다. 그렇지 않으면 결과가 정의되지 않습니다.

<xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>은 모두 표준 쿼리 연산자 사양을 기반으로 하는 음수가 아닌 정수 계열 상수 인수에 대해 잘 정의되어 있습니다.

### <a name="operators-with-no-translation"></a>변환이 없는 연산자

다음 메서드는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 변환되지 않습니다. 가장 일반적인 이유는 순서 없는 다중 집합과 시퀀스 간의 차이 때문입니다.

|연산자|이유|
|---------------|---------------|
|<xref:System.Linq.Enumerable.TakeWhile%2A>, <xref:System.Linq.Enumerable.SkipWhile%2A>|SQL 쿼리는 다중 집합에 대해서는 작동하지만 시퀀스에 대해서는 작동하지 않습니다. `ORDER BY`는 결과에 적용되는 마지막 절이어야 합니다. 따라서 이러한 두 메서드에 대한 일반 용도 변환이 없습니다.|
|<xref:System.Linq.Enumerable.Reverse%2A>|순서 있는 집합에 대해 이 메서드의 변환이 가능하지만 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 현재 변환되지 않습니다.|
|<xref:System.Linq.Enumerable.Last%2A>, <xref:System.Linq.Enumerable.LastOrDefault%2A>|순서 있는 집합에 대해 이러한 메서드의 변환이 가능하지만 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 현재 변환되지 않습니다.|
|<xref:System.Linq.Enumerable.ElementAt%2A>, <xref:System.Linq.Enumerable.ElementAtOrDefault%2A>|SQL 쿼리는 다중 집합에 대해서는 작동하지만 인덱싱 가능한 시퀀스에 대해서는 작동하지 않습니다.|
|<xref:System.Linq.Enumerable.DefaultIfEmpty%2A>(기본 인수로 오버로드)|일반적으로 임의의 튜플에 대해 기본값을 지정할 수 없습니다. 일부 경우 외부 조인을 통해 튜플에 null 값을 지정할 수는 있습니다.|

## <a name="expression-translation"></a>식 변환

### <a name="null-semantics"></a>Null 의미 체계

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 null 비교 의미 체계를 SQL에 적용하지 않습니다. 비교 연산자는 구문상 동등한 SQL 항목으로 변환됩니다. 이러한 이유로 의미 체계에는 서버 또는 연결 설정에 정의 된 SQL 의미 체계가 반영 됩니다. 예를 들어 두 개의 null 값은 기본 SQL Server 설정에서 동일 하지 않은 것으로 간주 되지만, 설정을 변경 하 여 의미 체계를 변경할 수 있습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 쿼리를 변환할 때 서버 설정을 고려하지 않습니다.

리터럴 null을 사용한 비교는 해당 SQL 버전(`is null` 또는 `is not null`)으로 변환됩니다.

데이터 정렬의 `null` 값은 SQL Server에서 정의됩니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 데이터 정렬을 변경하지 않습니다.

### <a name="aggregates"></a>집계

표준 쿼리 연산자의 집계 메서드 <xref:System.Linq.Enumerable.Sum%2A>은 빈 시퀀스 또는 null만 들어 있는 시퀀스를 0으로 계산합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 SQL의 의미 체계는 변경되지 않은 상태로 유지되고 <xref:System.Linq.Enumerable.Sum%2A>은 빈 시퀀스 또는 null만 들어 있는 시퀀스를 0이 아닌 `null`로 계산합니다.

중간 결과에 대한 SQL 제한은 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 집계에 적용됩니다. 32비트 정수 수량의 <xref:System.Linq.Enumerable.Sum%2A>은 64비트 결과를 사용하여 계산되지 않습니다. 표준 쿼리 연산자 구현이 메모리 내의 해당 시퀀스에 대해 오버플로를 발생시키지 않는 경우에도 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 <xref:System.Linq.Enumerable.Sum%2A> 변환에 대해 오버플로가 발생할 수 있습니다.

마찬가지로 정수 값의 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 대한 <xref:System.Linq.Enumerable.Average%2A> 변환은 `integer`이 아닌 `double`로 계산됩니다.

### <a name="entity-arguments"></a>엔터티 인수

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 엔터티 형식을 <xref:System.Linq.Enumerable.GroupBy%2A> 및 <xref:System.Linq.Enumerable.OrderBy%2A> 메서드에서 사용할 수 있습니다. 이러한 연산자 변환에서 형식 인수를 사용하는 것은 해당 형식의 모든 멤버를 지정하는 것과 동일합니다. 예를 들어 다음 코드는 동일합니다.

[!code-csharp[DLinqSQOTranslation#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#2)]
[!code-vb[DLinqSQOTranslation#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#2)]

### <a name="equatable--comparable-arguments"></a>같을 수 있는/비교 가능한 인수

인수의 같음은 다음과 같은 메서드의 구현에서 필요합니다.

- <xref:System.Linq.Enumerable.Contains%2A>

- <xref:System.Linq.Enumerable.Skip%2A>

- <xref:System.Linq.Enumerable.Union%2A>

- <xref:System.Linq.Enumerable.Intersect%2A>

- <xref:System.Linq.Enumerable.Except%2A>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 *플랫* 인수에 대 한 같음 및 비교를 지원 하지만 시퀀스를 포함 하거나 포함 하는 인수에 대해서는 지원 하지 않습니다. 단순 인수는 SQL 행에 매핑될 수 있는 형식입니다. 시퀀스를 포함하지 않는 것으로 정적으로 확인할 수 있는 하나 이상의 엔터티 형식에 대한 프로젝션은 단순 인수인 것으로 간주됩니다.

다음은 플랫 인수의 예입니다.

[!code-csharp[DLinqSQOTranslation#3](~/samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#3)]
[!code-vb[DLinqSQOTranslation#3](~/samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#3)]

다음은 플랫 (계층)이 아닌 인수의 예입니다.

[!code-csharp[DLinqSQOTranslation#4](~/samples/snippets/csharp/VS_Snippets_Data/DLinqSQOTranslation/cs/Program.cs#4)]
[!code-vb[DLinqSQOTranslation#4](~/samples/snippets/visualbasic/VS_Snippets_Data/DLinqSQOTranslation/vb/Module1.vb#4)]

### <a name="visual-basic-function-translation"></a>Visual Basic 함수 변환

Visual Basic 컴파일러에서 사용하는 다음과 같은 도우미 함수는 해당하는 SQL 연산자 및 함수로 변환됩니다.

- `CompareString`

- `DateTime.Compare`

- `Decimal.Compare`

- `IIf (in Microsoft.VisualBasic.Interaction)`

변환 메서드는 다음과 같습니다.

|||||
|-|-|-|-|
|ToBoolean|ToSByte|ToByte|ToChar|
|ToCharArrayRankOne|ToDate|ToDecimal|ToDouble|
|ToInteger|ToUInteger|ToLong|ToULong|
|ToShort|ToUShort|ToSingle|ToString|

## <a name="inheritance-support"></a>상속 지원

### <a name="inheritance-mapping-restrictions"></a>상속 매핑 제한

자세한 내용은 [방법: 매핑 상속 계층 @ no__t-0.

### <a name="inheritance-in-queries"></a>쿼리의 상속

C# 캐스트는 프로젝션에서만 지원됩니다. 다른 위치에 사용된 캐스트는 변환되지 않고 무시됩니다. SQL 함수 이름을 제외하고는 SQL에서는 사실상 CLR <xref:System.Convert>와 동일한 기능만 수행합니다. 즉, SQL에서는 한 형식의 값을 다른 형식으로 변환할 수 있습니다. 다른 형식과 동일한 비트를 재해석하는 개념이 없으므로 CLR 캐스트와 동일한 기능이 없습니다. 이 때문에 C# 캐스트는 로컬에서만 작동하며 원격으로 작동하지 않습니다.

`is` 및 `as` 연산자와 `GetType` 메서드는 `Select` 연산자뿐 아니라 다른 쿼리 연산자에서도 사용할 수 있습니다.

## <a name="sql-server-2008-support"></a>SQL Server 2008 지원

.NET Framework 3.5 SP1부터 LINQ to SQL에서는 SQL Server 2008에 새로 도입된 날짜 및 시간 형식에 대한 매핑이 지원됩니다. 그러나 이러한 새로운 형식에 매핑된 값에 대한 연산을 수행할 때는 LINQ to SQL 쿼리 연산자에 대해 몇 가지 제한 사항이 적용됩니다.

### <a name="unsupported-query-operators"></a>지원되지 않는 쿼리 연산자

다음 쿼리 연산자는 `DATETIME2`, `DATE`, `TIME` 및 `DATETIMEOFFSET` 등의 새로운 SQL Server 날짜 및 시간 형식에 매핑된 값에서는 지원되지 않습니다.

- `Aggregate`

- `Average`

- `LastOrDefault`

- `OfType`

- `Sum`

이러한 SQL Server 날짜 및 시간 형식에 매핑하는 방법에 대 한 자세한 내용은 [SQL-CLR 형식 매핑](sql-clr-type-mapping.md)을 참조 하세요.

## <a name="sql-server-2005-support"></a>SQL Server 2005 지원

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 다음과 같은 SQL Server 2005 기능을 지원하지 않습니다.

- SQL CLR용으로 작성된 저장 프로시저

- 사용자 정의 형식

- XML 쿼리 기능

## <a name="sql-server-2000-support"></a>SQL Server 2000 지원

다음 SQL Server 2000 제한 (Microsoft SQL Server 2005에 비해)은 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 지원에 영향을 줍니다.

### <a name="cross-apply-and-outer-apply-operators"></a>Cross Apply 및 Outer Apply 연산자

이러한 연산자는 SQL Server 2000에서 사용할 수 없습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 일련의 다시 쓰기를 시도하여 해당 연산자를 적절한 조인으로 바꿉니다.

`Cross Apply` 및 `Outer Apply`는 관계 탐색을 위해 생성됩니다. 이러한 다시 쓰기가 가능한 쿼리 집합은 잘 정의되어 있지 않습니다. 이러한 이유로 SQL Server 2000에 대해 지원 되는 최소 쿼리 집합은 관계 탐색과 관련이 없는 집합입니다.

### <a name="text--ntext"></a>text/ntext

Microsoft SQL Server 2005에서 지원 되는 `varchar(max)` @ no__t-4 @ no__t-5에 대 한 특정 쿼리 작업에서 데이터 형식 `text` @ no__t-1 @ no__t을 사용할 수 없습니다.

이 제한에 대한 해결 방법은 없습니다. 특히 `Distinct()` 또는 `text` 열에 매핑된 멤버가 들어 있는 결과에서는 `ntext`를 사용할 수 없습니다.

### <a name="behavior-triggered-by-nested-queries"></a>중첩된 쿼리에 의해 트리거되는 동작

SQL Server 2000 (SP4) 바인더에는 중첩 된 쿼리에 의해 트리거되는 몇 가지 고유한 특징이 있습니다. 이러한 고유한 특징이를 트리거하는 SQL 쿼리 집합은 잘 정의 되어 있지 않습니다. 따라서 SQL Server 예외를 일으킬 수 있는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 쿼리 집합을 정의할 수 없습니다.

### <a name="skip-and-take-operators"></a>Skip 및 Take 연산자

<xref:System.Linq.Enumerable.Take%2A> 및 <xref:System.Linq.Enumerable.Skip%2A>에는 SQL Server 2000에 대한 쿼리에서 사용할 경우 몇 가지 제한이 따릅니다. 자세한 내용은 [문제 해결](troubleshooting.md)에서 "SQL Server 2000의 Skip 및 Take 예외" 항목을 참조 하세요.

## <a name="object-materialization"></a>개체 구체화

구체화에서는 하나 이상의 SQL 쿼리에서 반환한 행을 사용하여 CLR 개체를 만듭니다.

- 다음 호출은 구체화의 일부로 *로컬에서 실행* 됩니다.

  - 생성자

  - 프로젝션의 `ToString` 메서드

  - 프로젝션의 형식 캐스트

- @No__t-0 메서드 다음에 오는 메서드는 *로컬로 실행*됩니다. 이 메서드는 즉시 실행되지 않습니다.

- `struct`를 쿼리 결과의 반환 형식이나 결과 형식의 멤버로 사용할 수 있습니다. 엔터티는 클래스여야 합니다. 익명 형식은 클래스 인스턴스로 구체화되지만 명명된 구조체(비엔터티)는 프로젝션에서 사용할 수 있습니다.

- 쿼리 결과에 대한 반환 형식의 멤버는 <xref:System.Linq.IQueryable%601> 형식일 수 있습니다. 이 멤버는 로컬 컬렉션으로 구체화됩니다.

- 다음 메서드는 메서드가 적용 되는 시퀀스의 *즉시 구체화* 를 발생 시킵니다.

  - <xref:System.Linq.Enumerable.ToList%2A>

  - <xref:System.Linq.Enumerable.ToDictionary%2A>

  - <xref:System.Linq.Enumerable.ToArray%2A>

## <a name="see-also"></a>참조

- [참조](reference.md)
- [시퀀스에서 요소 반환 또는 건너뛰기](return-or-skip-elements-in-a-sequence.md)
- [두 시퀀스 연결](concatenate-two-sequences.md)
- [두 시퀀스 간의 차집합 반환](return-the-set-difference-between-two-sequences.md)
- [두 시퀀스의 교집합 반환](return-the-set-intersection-of-two-sequences.md)
- [두 시퀀스의 합집합 반환](return-the-set-union-of-two-sequences.md)
