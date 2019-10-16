---
title: 수정 SQL 생성
ms.date: 03/30/2017
ms.assetid: 2188a39d-46ed-4a8b-906a-c9f15e6fefd1
ms.openlocfilehash: 94b6c3c97e8255db2dc4d72bae6c6c12905d9710
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854295"
---
# <a name="modification-sql-generation"></a>수정 SQL 생성

이 단원에서는 SQL:1999 규격 데이터베이스 공급자에 대한 수정 SQL 생성 모듈을 개발하는 방법에 대해 설명합니다. 이 모듈은 수정 명령 트리를 적절한 SQL INSERT, UPDATE 또는 DELETE 문으로 변환하는 작업을 담당합니다.

Select 문의 SQL 생성에 대 한 자세한 내용은 [Sql 생성](sql-generation.md)을 참조 하십시오.

## <a name="overview-of-modification-command-trees"></a>수정 명령 트리 개요

수정 SQL 생성 모듈은 지정된 입력 DbModificationCommandTree를 기반으로 데이터베이스 관련 수정 SQL 문을 생성합니다.

DbModificationCommandTree는 DbCommandTree에서 상속하는 수정 DML 작업(삽입, 업데이트 또는 삭제 작업)의 개체 모델 표현입니다. DbModificationCommandTree의 구현은 다음 세 가지입니다.

- DbInsertCommandTree

- DbUpdateCommandTree

- DbDeleteCommandTree

Entity Framework에서 생성 되는 DbModificationCommandTree 및 해당 구현은 항상 단일 행 작업을 나타냅니다. 이 단원에서는 .NET Framework 버전 3.5에서 이러한 형식과 관련 제약 조건에 대해 설명합니다.

![Diagram](./media/558ba7b3-dd19-48d0-b91e-30a76415bf5f.gif "558ba7b3-dd19-48d0-b91e-30a76415bf5f")

DbModificationCommandTree에는 수정 작업의 대상 집합을 나타내는 Target 속성이 있습니다. Target의 Expression 속성은 입력 집합을 정의하며 항상 DbScanExpression입니다.  DbScanExpression은 대상의 메타 데이터 속성 "정의 쿼리"가 null이 아닌 경우 테이블이 나 뷰 또는 쿼리를 사용 하 여 정의 된 데이터 집합을 나타낼 수 있습니다.

쿼리를 나타내는 DbScanExpression은 모델에서 정의 쿼리를 사용하여 집합이 정의되었지만 해당 수정 작업에 대한 함수가 제공되지 않은 경우 수정 대상으로만 공급자에 연결할 수 있습니다. 공급자가 이러한 시나리오를 지원하지 못할 수도 있습니다. 예를 들어, SqlClient는 이러한 시나리오를 지원하지 않습니다.

DbInsertCommandTree는 명령 트리로 표현된 단일 행 삽입 작업을 나타냅니다.

```csharp
public sealed class DbInsertCommandTree : DbModificationCommandTree {
   public IList<DbModificationClause> SetClauses { get }
   public DbExpression Returning { get }
}
```

DbUpdateCommandTree는 명령 트리로 표현된 단일 행 업데이트 작업을 나타냅니다.

DbDeleteCommandTree는 명령 트리로 표현된 단일 행 삭제 작업을 나타냅니다.

### <a name="restrictions-on-modification-command-tree-properties"></a>수정 명령 트리 속성에 대한 제한 사항

다음 정보와 제한 사항은 수정 명령 트리 속성에 적용됩니다.

#### <a name="returning-in-dbinsertcommandtree-and-dbupdatecommandtree"></a>DbInsertCommandTree 및 DbUpdateCommandTree의 Returning

Returning이 null이 아니면 명령이 판독기를 반환함을 나타내고, 그렇지 않으면 명령이 영향을 받는(삽입 또는 업데이트되는) 행의 수를 나타내는 스칼라 값을 반환해야 합니다.

Returning 값은 삽입되거나 업데이트된 행을 기반으로 반환될 결과의 프로젝션을 지정합니다. 이 값은 행을 나타내는 DbNewInstanceExpression 형식일 수만 있으며 각 인수는 해당 DbModificationCommandTree의 Target에 대한 참조를 나타내는 DbVariableReferenceExpression을 통한 DbPropertyExpression입니다. Returning 속성에서 사용되는 DbPropertyExpressions가 나타내는 속성은 항상 저장소 생성 또는 계산 값입니다. DbInsertCommandTree에서 Returning은 행이 삽입될 테이블의 속성 중 하나 이상이 저장소 생성 또는 계산으로 지정된 경우(ssdl에서 StoreGeneratedPattern.Identity 또는 StoreGeneratedPattern.Computed로 표시됨) null이 아닙니다. DbUpdateCommandTree에서 Returning은 행이 업데이트될 테이블의 속성 중 하나 이상이 저장소 계산으로 지정된 경우(ssdl에서 StoreGeneratedPattern.Computed로 표시됨) null이 아닙니다.

#### <a name="setclauses-in-dbinsertcommandtree-and-dbupdatecommandtree"></a>DbInsertCommandTree 및 DbUpdateCommandTree의 SetClauses

SetClauses는 삽입 또는 업데이트 작업을 정의하는 insert 또는 update set 절의 목록을 지정합니다.

```
The elements of the list are specified as type DbModificationClause, which specifies a single clause in an insert or update modification operation. DbSetClause inherits from DbModificationClause and specifies the clause in a modification operation that sets the value of a property. Beginning in version 3.5 of the .NET Framework, all elements in SetClauses are of type SetClause.
```

Property는 업데이트할 속성을 지정합니다. Property는 항상 해당 DbModificationCommandTree의 Target에 대한 참조를 나타내는 DbVariableReferenceExpression을 통한 DbPropertyExpression입니다.

Value는 속성을 업데이트할 새 값을 지정합니다. Value는 DbConstantExpression 또는 DbNullExpression 형식입니다.

#### <a name="predicate-in-dbupdatecommandtree-and-dbdeletecommandtree"></a>DbUpdateCommandTree 및 DbDeleteCommandTree의 조건자

Predicate는 대상 컬렉션에서 업데이트하거나 삭제할 멤버를 결정하는 데 사용되는 조건자를 지정합니다. Predicate는 DbExpression의 다음 하위 집합으로 작성된 식 트리입니다.

- 오른쪽 자식은 DbPropertyExpression이 아래에 제한 되는 것으로, 왼쪽 자식은 DbConstantExpression로 DbComparisonExpression 종류가 같습니다.

- DbConstantExpression

- 아래 제한 된 DbPropertyExpression을 DbIsNullExpression.

- 해당 DbModificationCommandTree의 Target에 대한 참조를 나타내는 DbVariableReferenceExpression을 통한 DbPropertyExpression

- DbAndExpression

- DbNotExpression

- DbOrExpression

## <a name="modification-sql-generation-in-the-sample-provider"></a>샘플 공급자의 수정 SQL 생성

[Entity Framework 샘플 공급자](https://code.msdn.microsoft.com/windowsdesktop/Entity-Framework-Sample-6a9801d0) 는 Entity Framework를 지 원하는 ADO.NET 데이터 공급자의 구성 요소를 보여 줍니다. 샘플 공급자는 SQL Server 2005 데이터베이스를 대상으로 하며 System.Data.SqlClient ADO.NET 2.0 데이터 공급자 위에 래퍼로 구현됩니다.

샘플 공급자의 수정 SQL 생성 모듈(SQL Generation\DmlSqlGenerator.cs 파일에 있음)은 DbModificationCommandTree를 입력으로 사용하고 단일 수정 SQL 문을 생성합니다. 이 문 뒤에는 DbModificationCommandTree에서 지정된 경우 판독기를 반환하기 위해 SELECT 문이 올 수 있습니다. 생성된 명령의 모양은 대상 SQL Server 데이터베이스의 영향을 받습니다.

### <a name="helper-classes-expressiontranslator"></a>도우미 클래스: ExpressionTranslator

ExpressionTranslator는 DbExpression 형식의 모든 수정 명령 트리 속성에 대해 공통적인 간단한 변환기 역할을 합니다. ExpressionTranslator는 수정 명령 트리의 속성이 제한된 식 형식의 변환만 지원하며 특정 제약 조건을 염두에 두고 작성되었습니다.

아래에서는 특정 식 형식의 방문에 대해 설명합니다(사소한 변환이 포함된 노드는 생략됨).

### <a name="dbcomparisonexpression"></a>DbComparisonExpression

ExpressionTranslator가 preserveMemberValues = true를 사용하여 생성된 경우 오른쪽 상수가 DbNullExpression이 아니라 DbConstantExpression이면 왼쪽 피연산자(DbPropertyExpressions)를 해당 DbConstantExpression과 연결합니다. 이는 영향을 받는 행을 식별하기 위해 반환 SELECT 문이 생성되어야 하는 경우에 사용됩니다.

### <a name="dbconstantexpression"></a>DbConstantExpression

방문된 각 상수에 대해 매개 변수가 만들어집니다.

### <a name="dbpropertyexpression"></a>DbPropertyExpression

DbPropertyExpression의 인스턴스가 항상 입력 테이블을 나타내는 경우 생성에서 별칭을 만들지 않았으면(테이블 변수가 사용되는 업데이트 시나리오에서만 별칭이 발생함) 입력에 대해 별칭을 지정할 필요가 없습니다. 변환에서는 기본적으로 속성 이름을 사용합니다.

## <a name="generating-an-insert-sql-command"></a>INSERT SQL 명령 생성

샘플 공급자에서 지정된 DbInsertCommandTree의 경우 생성된 INSERT 명령은 아래의 두 삽입 템플릿 중 하나를 따릅니다.

첫 번째 템플릿에는 SetClauses 목록의 값에 따라 삽입을 수행하는 명령과 Returning 속성이 null이 아닌 경우 삽입된 행의 Returning 속성에 지정된 속성을 반환하는 SELECT 문이 있습니다. 조건자 요소 "\@ @ROWCOUNT > 0"은 행이 삽입 된 경우 true입니다. Scope_identity ()는 id에 삽입 된 마지막 &#124; id 값을 반환 하기 때문에 조건자 요소 "Keymemberi = keyValueI scope_identity ()"는 keymemberi가 저장소 생성 키인 경우에만 "keymemberi = scope_identity ()" 셰이프를 사용 합니다. 저장소 생성) 열

```sql
-- first insert Template
INSERT <target>   [ (setClauseProperty0, .. setClausePropertyN)]
VALUES (setClauseValue0, .. setClauseValueN) |  DEFAULT VALUES

[SELECT <returning>
 FROM <target>
 WHERE @@ROWCOUNT > 0 AND keyMember0 = keyValue0 AND .. keyMemberI =  keyValueI | scope_identity()  .. AND  keyMemberN = keyValueN]
```

두 번째 템플릿은 기본 키가 저장소 생성 키이지만 정수 형식이 아니라서 scope_identity()와 함께 사용할 수 없는 행의 삽입을 지정하는 경우에 필요합니다. 또한 복합 저장소 생성 키가 있는 경우에도 사용됩니다.

```sql
-- second insert template
DECLARE @generated_keys TABLE [(keyMember0, … keyMemberN)

INSERT <target>   [ (setClauseProperty0, .. setClausePropertyN)]
 OUTPUT inserted.KeyMember0, …, inserted.KeyMemberN INTO @generated_keys
 VALUES (setClauseValue0, .. setClauseValueN) |  DEFAULT VALUES

[SELECT <returning_over_t>
 FROM @generated_keys  AS g
JOIN <target> AS t ON g.KeyMember0 = t.KeyMember0 AND … g.KeyMemberN = t.KeyMemberN
 WHERE @@ROWCOUNT > 0
```

다음은 샘플 공급자에 포함된 모델을 사용하는 예제입니다. 이 예제에서는 DbInsertCommandTree에서 삽입 명령을 생성합니다.

다음 코드에서는 Category를 삽입합니다.

```csharp
using (NorthwindEntities northwindContext = new NorthwindEntities()) {
   Category c = new Category();
   c.CategoryName = "Test Category";
   c.Description = "A new category for testing";
   northwindContext.AddObject("Categories", c);
   northwindContext.SaveChanges();
}
```

이 코드에서는 공급자에 전달되는 다음 명령 트리를 생성합니다.

```
DbInsertCommandTree
|_Parameters
|_Target : 'target'
| |_Scan : dbo.Categories
|_SetClauses
| |_DbSetClause
| | |_Property
| | | |_Var(target).CategoryName
| | |_Value
| |   |_'Test Category'
| |_DbSetClause
| | |_Property
| | | |_Var(target).Description
| | |_Value
| |   |_'A new category for testing'
| |_DbSetClause
|   |_Property
|   | |_Var(target).Picture
|   |_Value
|     |_null
|_Returning
  |_NewInstance : Record['CategoryID'=Edm.Int32]
    |_Column : 'CategoryID'
      |_Var(target).CategoryID
```

샘플 공급자가 생성하는 저장소 명령은 다음 SQL 문입니다.

```sql
insert [dbo].[Categories]([CategoryName], [Description], [Picture])
values (@p0, @p1, null)
select [CategoryID]
from [dbo].[Categories]
where @@ROWCOUNT > 0 and [CategoryID] = scope_identity()
```

## <a name="generating-an-update-sql-command"></a>UPDATE SQL 명령 생성

지정된 DbUpdateCommandTree의 경우 생성된 UPDATE 명령은 다음 템플릿을 기반으로 합니다.

```sql
-- UPDATE Template
UPDATE <target>
SET setClauseProperty0 = setClauseValue0, .. setClausePropertyN = setClauseValueN  | @i = 0
WHERE <predicate>

[SELECT <returning>
 FROM <target>
 WHERE @@ROWCOUNT > 0 AND keyMember0 = keyValue0 AND .. keyMemberI =  keyValueI | scope_identity()  .. AND  keyMemberN = keyValueN]
```

Set 절이 지정 되지 않은 경우에만 set@i 절에 가짜 set 절 ("= 0")이 있습니다. 이는 모든 저장소 계산 열이 다시 계산되도록 하기 위한 것입니다.

Returning 속성이 null이 아닌 경우에만 Returning 속성에 지정된 속성을 반환하기 위해 SELECT 문이 생성됩니다.

다음 예제에서는 샘플 공급자와 함께 포함된 모델을 사용하여 UPDATE 명령을 생성합니다.

다음 사용자 코드에서는 Category를 업데이트합니다.

```csharp
using (NorthwindEntities northwindContext = new NorthwindEntities()) {
   Category c = northwindContext.Categories.Where(i => i.CategoryName == "Test Category").First();
   c.CategoryName = "New test name";
   northwindContext.SaveChanges();
}
```

이 사용자 코드에서는 공급자에 전달되는 다음 명령 트리를 생성합니다.

```
DbUpdateCommandTree
|_Parameters
|_Target : 'target'
| |_Scan : dbo.Categories
|_SetClauses
| |_DbSetClause
|   |_Property
|   | |_Var(target).CategoryName
|   |_Value
|     |_'New test name'
|_Predicate
| |_
|   |_Var(target).CategoryID
|   |_=
|   |_10
|_Returning
```

샘플 공급자는 다음과 같은 저장소 명령을 생성합니다.

```sql
update [dbo].[Categories]
set [CategoryName] = @p0
where ([CategoryID] = @p1)
```

### <a name="generating-a-delete-sql-command"></a>DELETE SQL 명령 생성

지정된 DbDeleteCommandTree의 경우 생성된 DELETE 명령은 다음 템플릿을 기반으로 합니다.

```sql
-- DELETE Template
DELETE <target>
WHERE <predicate>
```

다음 예제에서는 샘플 공급자와 함께 포함된 모델을 사용하여 DELETE 명령을 생성합니다.

다음 사용자 코드에서는 Category를 삭제합니다.

```csharp
using (NorthwindEntities northwindContext = new NorthwindEntities()) {
   Category c = northwindContext.Categories.Where(i => i.CategoryName == "New test name").First();
   northwindContext.DeleteObject(c);
   northwindContext.SaveChanges();
}
```

이 사용자 코드에서는 공급자에 전달되는 다음 명령 트리를 생성합니다.

```
DbDeleteCommandTree
|_Parameters
|_Target : 'target'
| |_Scan : dbo.Categories
|_Predicate
  |_
    |_Var(target).CategoryID
    |_=
    |_10
```

샘플 공급자는 다음과 같은 저장소 명령을 생성합니다.

```sql
delete [dbo].[Categories]
where ([CategoryID] = @p0)
```

## <a name="see-also"></a>참고자료

- [Entity Framework 데이터 공급자 작성](writing-an-ef-data-provider.md)
