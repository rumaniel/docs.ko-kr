---
title: SQL-CLR 형식 불일치
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0a90c33f-7ed7-4501-ad5f-6224c5da8e9b
ms.openlocfilehash: 27708f4bb8e191156f578132602570bc4a6337b0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781205"
---
# <a name="sql-clr-type-mismatches"></a>SQL-CLR 형식 불일치

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 개체 모델과 SQL Server 간의 변환을 대부분 자동화합니다. 하지만 정확한 변환이 불가능한 경우도 있습니다. CLR (공용 언어 런타임) 형식과 SQL Server 데이터베이스 형식 간의 이러한 키 불일치는 다음 섹션에 요약 되어 있습니다. 특정 형식 매핑과 함수 변환에 대 한 자세한 내용은 [SQL CLR 형식 매핑](sql-clr-type-mapping.md) 및 [데이터 형식 및 함수](data-types-and-functions.md)에서 찾을 수 있습니다.

## <a name="data-types"></a>데이터 형식

CLR과 SQL Server 간의 변환은 쿼리가 데이터베이스로 전송될 때와 쿼리 결과가 개체 모델로 반환될 때 수행됩니다. 예를 들어 다음 Transact-SQL 쿼리에는 두 번의 값 변환이 필요합니다.

```sql
Select DateOfBirth From Customer Where CustomerId = @id
```

SQL Server에서 쿼리를 실행하기 전에 Transact-SQL 매개 변수 값을 지정해야 합니다. 이 예제에서는 먼저 `id` 매개 변수 값을 CLR의 <xref:System.Int32?displayProperty=nameWithType> 형식에서 SQL Server의 `INT` 형식으로 변환하여 데이터베이스에서 값을 인식할 수 있도록 해야 합니다. 그런 다음 결과를 검색하기 위해 SQL Server의 `DateOfBirth` 열을 SQL Server의 `DATETIME` 형식에서 개체 모델에 사용할 수 있는 CLR의 <xref:System.DateTime?displayProperty=nameWithType> 형식으로 변환해야 합니다. 이 예제에서 CLR 개체 모델의 형식과 SQL Server 데이터베이스의 형식은 자연적으로 매핑됩니다. 그러나 이러한 방식으로 매핑되지 않는 경우도 있습니다.

### <a name="missing-counterparts"></a>대응 항목 누락

다음과 같은 형식에는 대응되는 항목이 없습니다.

- CLR <xref:System> 네임스페이스의 불일치

  - **부호 없는 정수**입니다. 일반적으로 이 형식은 오버플로를 방지하기 위해 크기가 더 큰 부호 있는 대응 항목에 매핑됩니다. 리터럴은 값에 따라 크기가 같거나 더 작은 부호 있는 숫자로 변환할 수 있습니다.

  - **부울**. 이 형식은 1비트 또는 더 큰 숫자나 문자열로 매핑될 수 있습니다. 리터럴은 동일한 값으로 계산되는 식(예: SQL의 `1=1`과 CLS의 `True`)에 매핑할 수 있습니다.

  - **TimeSpan**. 이 형식은 두 `DateTime` 값의 차이를 나타내며 SQL Server의 `timestamp`에 대응되지 않습니다. 일부 경우에는 CLR의 <xref:System.TimeSpan?displayProperty=nameWithType>이 SQL Server의 `TIME` 형식에 매핑될 수 있습니다. SQL Server의 `TIME` 형식은 24시간 미만의 양수 값을 나타낼 때만 사용되지만 CLR의 <xref:System.TimeSpan>은 나타낼 수 있는 범위가 넓습니다.

  > [!NOTE]
  > 의 <xref:System.Data.SqlTypes> SQL Server 관련 .NET Framework 형식은이 비교에 포함 되지 않습니다.

- SQL Server의 불일치

  - **고정 길이 문자 형식**입니다. Transact-sql은 유니코드와 비유니코드 범주를 구분 하 고 각 범주에는 세 가지 고유 형식 (고정 `nchar`길이 `varchar` / `char`, 가변 길이 `nvarchar` /및)이 있습니다. 크기 `ntext` /를 늘립니다. `text` 고정 길이 문자 형식은 문자를 검색하기 위해 CLR의 <xref:System.Char?displayProperty=nameWithType> 형식에 매핑될 수 있지만 실제 변환 및 동작은 동일한 형식과 일치하지 않습니다.

  - **비트**. `bit` 도메인에는 `Nullable<Boolean>`과 동일한 수의 값이 있지만 형식이 서로 다릅니다. `Bit`는 `0` 대신 `1` 값을`true`사용 하 고 부울 식에 해당 하는로 사용할 수 없습니다. / `false`

  - **타임 스탬프**. CLR의 <xref:System.TimeSpan?displayProperty=nameWithType> 형식과 달리 SQL Server의 `TIMESTAMP` 형식은 각 업데이트에 고유하고 <xref:System.DateTime> 값 간의 차이를 기반으로 하지 않는 데이터베이스에서 생성된 8바이트 숫자를 나타냅니다.

  - **Money** 및 **SmallMoney**. 이 형식은 <xref:System.Decimal>에 매핑될 수 있지만 기본적으로 다른 형식이며 서버 기반 함수와 변환에서 다른 형식으로 취급됩니다.

### <a name="multiple-mappings"></a>다중 매핑

여러 SQL Server 데이터 형식을 하나 이상의 CLR 데이터 형식에 매핑할 수 있습니다. 또한 여러 CLR 형식을 하나 이상의 SQL Server 형식에 매핑할 수도 있습니다. LINQ to SQL에서 매핑을 지원하지만 그렇다고 해서 CLR 및 SQL Server 간에 매핑되는 두 형식의 정밀도, 범위 및 의미 체계가 완벽하게 일치하는 것은 아닙니다. 일부 매핑에는 이러한 차원의 일부 또는 전체에 있어 차이가 있을 수 있습니다. 이러한 잠재적인 차이점에 대 한 자세한 내용은 [SQL-CLR 형식 매핑의](sql-clr-type-mapping.md)다양 한 매핑 가능성에 대해 확인할 수 있습니다.

### <a name="user-defined-types"></a>사용자 정의 형식

사용자 정의 CLR 형식은 형식 시스템의 차이를 좁히는 역할을 합니다. 하지만 형식 버전 관리 측면에서 흥미로운 문제를 발생시킵니다. 클라이언트의 버전 변경이 데이터베이스 서버에 저장된 형식 변경과 일치하지 않을 수 있습니다. 이러한 변경으로 인해 형식 의미 체계가 일치하지 않을 수 있는 다른 형식 불일치가 발생하고 버전 차이가 표시될 수 있습니다. 상속 계층이 연속 버전에서 리팩터링되므로 추가 복잡한 문제가 발생합니다.

## <a name="expression-semantics"></a>식 의미 체계

CLR과 데이터베이스 형식 간의 pairwise 불일치 외에도 식은 불일치에 복잡성을 더합니다. 연산자 의미 체계, 함수 의미 체계, 암시적 형식 변환 및 우선 순위 규칙의 불일치를 고려해야 합니다.

다음 하위 단원에서는 비슷해 보이는 식의 불일치를 보여 줍니다. 의미 체계가 지정된 CLR 식과 동등한 SQL 식을 생성할 수도 있습니다. 그러나 비슷해 보이는 식의 의미 체계 차이가 CLR 사용자에게 드러나는지 여부 및 의미 체계를 동등하게 하기 위해 필요한 변경이 의도된 동작인지 여부는 명확하지 않습니다. 이는 값 집합에 대해 식을 계산하는 경우에 특히 중요한 문제입니다. 차이의 표시 여부는 데이터에 따라 달라질 수 있으며 코딩과 디버깅 중에 식별하기 어려울 수 있습니다.

### <a name="null-semantics"></a>Null 의미 체계

SQL 식은 부울 식에 대해 세 개의 값이 지정되는 논리를 제공합니다. 결과는 true, false 또는 null일 수 있습니다. 반면 CLR은 null 값과 관련된 비교에 대해 두 개의 값이 있는 부울 결과를 지정합니다. 다음 코드를 살펴보세요.

[!code-csharp[DLinqMismatch#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#2)]
[!code-vb[DLinqMismatch#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#2)]

```sql
-- Assume col1 and col2 are integer columns with null values.
-- Assume that ANSI null behavior has not been explicitly
--  turned off.
Select …
From …
Where col1 = col2
-- Evaluates to null, not true and the corresponding row is not
--   selected.
-- To obtain matching behavior (i -> col1, j -> col2) change
--   the query to the following:
Select …
From …
Where
    col1 = col2
or (col1 is null and col2 is null)
-- (Visual Basic 'Nothing'.)
```

두 개의 값이 지정되는 결과에 대한 가정에서도 유사한 문제가 발생합니다.

[!code-csharp[DLinqMismatch#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#3)]
[!code-vb[DLinqMismatch#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#3)]

```sql
-- Assume col1 and col2 are nullable columns.
-- Assume that ANSI null behavior has not been explicitly
--   turned off.
Select …
From …
Where
    col1 = col2
or col1 != col2
-- Visual Basic: col1 <> col2.

-- Excludes the case where the boolean expression evaluates
--   to null. Therefore the where clause does not always
--   evaluate to true.
```

앞의 경우에서 SQL을 생성할 때 동등한 동작을 얻을 수는 있지만 변환이 사용자 의도를 정확하게 반영하지 못할 수 있습니다.

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]는 SQL에 C# `null` 대 한 `nothing` 비교 의미 체계를 적용 하거나 Visual Basic 하지 않습니다. 비교 연산자는 구문상 동등한 SQL 항목으로 변환됩니다. 의미 체계는 서버 또는 연결 설정에 정의된 SQL 의미 체계를 반영합니다. 설정을 변경하여 의미 체계를 변경할 수 있지만 기본 SQL Server 설정에서는 두 개의 null 값이 같지 않은 것으로 고려됩니다. 하지만 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 쿼리 변환에서 서버 설정을 고려하지 않습니다.

리터럴 `null`(`nothing`)을 사용한 비교는 해당 SQL 버전(`is null` 또는 `is not null`)으로 변환됩니다.

데이터 정렬의 `null`(`nothing`) 값은 SQL Server에서 정의됩니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 데이터 정렬을 변경하지 않습니다.

### <a name="type-conversion-and-promotion"></a>형식 변환 및 확장

SQL은 식에서 다양한 암시적 변환을 지원합니다. C#의 유사한 식에는 명시적 캐스트가 필요합니다. 예를 들면 다음과 같습니다.

- 명시적 캐스트 없이 SQL에서 `Nvarchar` 및 `DateTime` 형식을 비교할 수 있습니다. C#에는 명시적 변환이 필요합니다.

- `Decimal`은 암시적으로 SQL의 `DateTime`으로 변환됩니다. C#은 암시적 변환을 허용하지 않습니다.

마찬가지로 내부 형식 집합이 다르기 때문에 Transact-SQL의 형식 우선 순위는 C#의 형식 우선 순위와 다릅니다. 실제로 우선 순위 목록 간에는 분명한 하위 집합/상위 집합 관계가 없습니다. 예를 들어 `nvarchar`를 `varchar`와 비교하면 암시적으로 `varchar` 식이 `nvarchar`로 변환됩니다. CLR은 동등한 확장 기능을 제공하지 않습니다.

단순한 경우에는 이러한 차이로 인해 해당 SQL 식에 대한 중복 캐스트가 있는 CLR 식이 발생합니다. 보다 중요한 점은 SQL 식의 중간 결과가 암시적으로 C#에 정확한 대응 항목이 없는 형식으로 확장되거나 그 반대의 경우가 발생할 수 있다는 것입니다. 전체적으로 이러한 식의 테스트, 디버깅 및 유효성 검사는 사용자에게 상당한 부담이 됩니다.

### <a name="collation"></a>데이터 정렬

Transact-SQL은 문자열 형식에 대한 주석으로 명시적 데이터 정렬을 지원합니다. 이러한 데이터 정렬에 따라 특정 비교의 유효성이 결정됩니다. 예를 들어 명시적 데이터 정렬이 다른 두 열을 비교하면 오류가 발생합니다. 훨씬 단순한 CTS 문자열 형식을 사용하면 이러한 오류가 발생하지 않습니다. 다음 예제를 참조하세요.

```sql
create table T2 (
    Col1 nvarchar(10),
    Col2      nvarchar(10) collate Latin_general_ci_as
)
```

[!code-csharp[DLinqMismatch#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#4)]
[!code-vb[DLinqMismatch#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#4)]

```sql
Select …
From …
Where Col1 = Col2
-- Error, collation conflict.
```

실제로 데이터 정렬 하위 절은 대체할 수 없는 *제한 된 형식을* 만듭니다.

마찬가지로 형식 시스템에서 정렬 순서가 크게 다를 수 있습니다. 이러한 차이는 결과 정렬에 영향을 줍니다. <xref:System.Guid>는 모든 16바이트에서 사전순으로 정렬되는 반면(`IComparable()`), T-SQL은 node(10-15), clock-seq(8-9), time-high(6-7), time-mid(4-5), time-low(0-3)의 순서로 GUID를 비교합니다. 이러한 순서는 NT에서 생성된 GUID가 8진수 순서를 가지고 있을 때 SQL 7.0에서 정해졌습니다. 이 접근 방식을 사용하면 동일한 노드 클러스터에서 생성된 GUID가 타임스탬프에 따라 순서대로 표시됩니다. 이 접근 방식은 인덱스 작성에도 유용합니다. 임의의 IO 대신 삽입이 추가가 됩니다. 개인 정보 보호를 위해 나중에 Windows에서 순서가 스크램블되었지만 SQL에서 호환성을 유지해야 합니다. 해결 방법은 <xref:System.Data.SqlTypes.SqlGuid> <xref:System.Guid>대신를 사용 하는 것입니다.

### <a name="operator-and-function-differences"></a>연산자 및 함수 차이

기본적으로 비교 가능한 연산자와 함수에도 의미 체계상 미묘한 차이가 있습니다. 예를 들면 다음과 같습니다.

- C#은 논리 연산자 `&&` 및 `||`에 대한 연산자의 사전순에 따라 단락 의미 체계를 지정합니다. 반면 SQL은 세트 기반 쿼리를 대상으로 하므로 최적화 프로그램에서 보다 자유롭게 실행 순서를 결정할 수 있습니다. 몇 가지 함축된 의미에는 다음이 포함됩니다.

  - 의미상 동일 하 게 변환 하려면`CASE` "... `WHEN` … `THEN`"SQL에서 구문을 사용 하 여 피연산자 실행 순서를 다시 정렬 하지 않습니다.

  - 연산자에 대 한 `AND` 느슨한 변환은 C# 식이 첫 번째 피연산자의 계산 결과에 따라 두 번째 피연산자를 계산 하는 데 / `OR` 사용 되는 경우 예기치 않은 오류를 일으킬 수 있습니다.

- `Round()`함수는 .NET Framework 및 T-sql에 서로 다른 의미를 갖습니다.

- 문자열의 시작 인덱스가 CLR에서는 0이지만 SQL에서는 1입니다. 따라서 인덱스가 있는 모든 함수에 인덱스 변환이 필요합니다.

- CLR은 부동 소수점 실수에 대해 모듈러스(‘%’) 연산자를 지원하지만 SQL은 그렇지 않습니다.

- `Like` 연산자는 암시적 변환을 기반으로 효과적으로 자동 오버로드를 수행합니다. `Like` 연산자는 문자열 형식에 적용되도록 정의되지만 숫자 형식이나 `DateTime` 형식에서 암시적으로 변환하면 문자열이 아닌 이러한 형식도 `Like`에 사용할 수 있습니다. CTS에는 비교 가능한 암시적 변환이 없습니다. 따라서 추가 오버로드가 필요합니다.

    > [!NOTE]
    > 이 `Like` 연산자 동작은 C#에만 적용됩니다. Visual Basic `Like` 키워드는 변경되지 않습니다.

- 오버플로는 항상 SQL에서 확인 되지만 래핑을 방지 하기 위해 (Visual Basic C# 아닌)에 명시적으로 지정 되어야 합니다. C1+C2가 C3에 저장되는 경우 정수 열 C1, C2 및 C3이 지정됩니다(Update T Set C3 = C1 + C2).

    ```sql
    create table T3 (
        Col1      integer,
        Col2      integer
    )
    insert into T3 (col1, col2) values (2147483647, 5)
    -- Valid values: max integer value and 5.
    select * from T3 where col1 + col2 < 0
    -- Produces arithmetic overflow error.
    ```

[!code-csharp[DLinqMismatch#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#5)]
[!code-vb[DLinqMismatch#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#5)]

- SQL은 .NET Framework 은행원의 반올림을 사용 하는 동안 대칭 산술 연산을 수행 합니다. 자세한 내용은 기술 자료 문서 196652를 참조하세요.

- 기본적으로 일반 로캘의 경우 SQL에서 문자열 비교는 대/소문자를 구분하지 않습니다. Visual Basic 및 C#에서는 대/소문자를 구분합니다. 예 `s == "Food"` 를 들어 (`s = "Food"` Visual Basic) `s == "Food"` 는가 인 `food`경우 `s` 다른 결과를 생성할 수 있습니다.

    ```sql
    -- Assume default US-English locale (case insensitive).
    create table T4 (
        Col1      nvarchar (256)
    )
    insert into T4 values (‘Food’)
    insert into T4 values (‘FOOD’)
    select * from T4 where Col1 = ‘food’
    -- Both the rows are returned because of case-insensitive matching.
    ```

[!code-csharp[DLinqMismatch#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#6)]
[!code-vb[DLinqMismatch#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#6)]

- SQL의 고정 길이 문자 형식 인수에 적용된 연산자/함수는 CLR의 <xref:System.String?displayProperty=nameWithType>에 적용된 동일한 연산자/함수와 의미 체계가 완전히 다릅니다. 이 문제를 형식에 대한 단원에서 설명한 대응 항목 누락 문제의 확장으로 간주할 수도 있습니다.

    ```sql
    create table T4 (
        Col1      nchar(4)
    )
    Insert into T5(Col1) values ('21');
    Insert into T5(Col1) values ('1021');
    Select * from T5 where Col1 like '%1'
    -- Only the second row with Col1 = '1021' is returned.
    -- Not the first row!
    ```

     [!code-csharp[DLinqMismatch#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#7)]
     [!code-vb[DLinqMismatch#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#7)]

     문자열 연결에서도 유사한 문제가 발생합니다.

    ```sql
    create table T6 (
        Col1      nchar(4)
        Col2       nchar(4)
    )
    Insert into T6 values ('a', 'b');
    Select Col1+Col2 from T6
    -- Returns concatenation of padded strings "a   b   " and not "ab".
    ```

요약하면 CLR 식에 대해 회선 변환이 필요할 수도 있고 SQL 기능을 노출하기 위해 추가 연산자/함수가 필요할 수도 있습니다.

### <a name="type-casting"></a>형식 캐스팅

C#과 SQL에서 사용자는 명시적 형식 캐스트(`Cast` 및 `Convert`)를 사용하여 식의 기본 의미 체계를 재정의할 수 있습니다. 그러나 형식 시스템 경계를 넘어 이 기능을 노출하면 문제가 발생합니다. 원하는 의미 체계를 제공하는 SQL 캐스트를 해당 C# 캐스트로 쉽게 변환할 수 없습니다. 또한 형식 불일치, 대응 항목 누락 및 다른 형식 우선 순위 계층 때문에 C# 캐스트를 동등한 SQL 캐스트로 직접 변환할 수 없습니다. 형식 시스템 불일치 노출과 중요한 식 기능 손실을 절충해야 합니다.

경우에 따라 식의 유효성 검사를 위한 형식 캐스팅은 도메인에 필요하지 않지만 기본값이 아닌 매핑이 식에 올바로 적용되도록 하는 데 형식 캐스팅이 필요할 수도 있습니다.

```sql
-- Example from "Non-default Mapping" section extended
create table T5 (
    Col1      nvarchar(10),
    Col2      nvarchar(10)
)
Insert into T5(col1, col2) values (‘3’, ‘2’);
```

[!code-csharp[DLinqMismatch#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#8)]
[!code-vb[DLinqMismatch#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#8)]

```sql
Select *
From T5
Where Col1 + Col2 > 4
-- "Col1 + Col2" expr evaluates to '32'
```

## <a name="performance-issues"></a>성능 문제

일부 SQL Server의 경우 clr 형식 차이로 인해 CLR과 SQL Server 형식 시스템 사이를 교차 하는 경우 성능이 저하 될 수 있습니다. 성능에 영향을 주는 시나리오에는 다음과 같은 것이 있습니다.

- 논리 AND/OR 연산자의 강제 계산 순서

- 조건자 계산 순서를 적용하는 SQL을 생성하면 SQL 최적화 프로그램의 기능이 제한됩니다.

- CLR 컴파일러에서 정의되었든 개체-관계 쿼리 구현에서 정의되었든 관계없이 형식 변환은 인덱스 사용을 줄일 수 있습니다.

     예를 들면 다음과 같습니다.

    ```sql
    -- Table DDL
    create table T5 (
        Col1      varchar(100)
    )
    ```

     [!code-csharp[DLinqMismatch#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#9)]
     [!code-vb[DLinqMismatch#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#9)]

     식 `(s = SOME_STRING_CONSTANT)`의 변환을 살펴보세요.

    ```sql
    -- Corresponding part of SQL where clause
    Where …
    Col1 = SOME_STRING_CONSTANT
    -- This expression is of the form <varchar> = <nvarchar>.
    -- Hence SQL introduces a conversion from varchar to nvarchar,
    --   resulting in
    Where …
    Convert(nvarchar(100), Col1) = SOME_STRING_CONSTANT
    -- Cannot use the index for column Col1 for some implementations.
    ```

의미 체계의 차이 외에 SQL Server 및 CLR 형식 시스템을 거치는 동안 성능에 미치는 영향도 고려해야 합니다. 큰 데이터 집합의 경우 이러한 성능 문제에 따라 응용 프로그램의 배포 가능 여부가 결정될 수 있습니다.

## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
