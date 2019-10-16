---
title: ID 또는 일련 번호 값 검색
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d6b7f9cb-81be-44e1-bb94-56137954876d
ms.openlocfilehash: 1387dad1f588770384422bf579ed547271b30c0a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794557"
---
# <a name="retrieving-identity-or-autonumber-values"></a>ID 또는 일련 번호 값 검색

관계형 데이터베이스에서 기본 키는 항상 고유한 값이 들어 있는 열 또는 열의 조합입니다. 기본 키 값을 알면 해당 값이 있는 행을 찾을 수 있습니다. SQL Server, Oracle 및 Microsoft Access/Jet 등과 같은 관계형 데이터베이스 엔진은 기본 키로 지정할 수 있는 자동 증분 열의 작성을 지원합니다. 이러한 값은 서버에 의해 행으로 생성되어 테이블에 추가됩니다. 이를 위해서는 SQL Server에서는 열의 identity 속성을 설정하고, Oracle에서는 시퀀스를 만들고, Microsoft Access에서는 AutoNumber 열을 만듭니다.

또한 <xref:System.Data.DataColumn>을 사용하고 <xref:System.Data.DataColumn.AutoIncrement%2A> 속성을 true로 설정하면 자동으로 증분하는 값을 생성할 수도 있습니다. 하지만 여러 클라이언트 애플리케이션이 개별적으로 자동 증분 값을 생성하면 <xref:System.Data.DataTable>의 개별 인스턴스에서 중복되는 값이 생길 수 있습니다. 따라서 서버가 자동 증분 값을 생성하도록 하면 삽입된 각 행에 대해 생성되는 값을 각 사용자가 검색할 수 있도록 할 때 발생할 수 있는 충돌을 방지할 수 있습니다.

`Update`의 `DataAdapter` 메서드 호출 도중 데이터베이스는 데이터를 출력 매개 변수로, 또는 INSERT 문과 동일한 배치에서 실행되는 SELECT 문의 결과 집합 중 첫 번째 반환되는 레코드로 ADO.NET 애플리케이션에 다시 보낼 수 있습니다. ADO.NET에서는 이러한 값을 검색하여 업데이트되는 <xref:System.Data.DataRow>의 해당 열을 업데이트할 수 있습니다.

Microsoft Access Jet 데이터베이스 엔진과 같은 일부 데이터베이스에서는 출력 매개 변수를 지원하지 않으며 하나의 배치에서 여러 문을 처리할 수 없습니다. Jet 데이터베이스 엔진으로 작업하는 경우 `RowUpdated`의 `DataAdapter` 이벤트에 대한 이벤트 처리기에서 별도의 SELECT 명령을 실행하여 삽입된 행에 대해 생성되는 새 AutoNumber 값을 검색할 수 있습니다.

> [!NOTE]
> 자동 증분 값 대신 사용할 수 있는 방법은 <xref:System.Guid.NewGuid%2A> 개체의 <xref:System.Guid> 메서드를 사용하여 새로운 행이 삽입될 때마다 서버로 복사될 수 있는 GUID(Globally Unique Identifier)를 클라이언트 컴퓨터에 생성하는 것입니다. `NewGuid` 메서드는 값이 복제되지 않을 확률이 높은 알고리즘을 사용하여 16바이트 이진 값을 생성합니다. SQL Server 데이터베이스에서 GUID는 SQL Server가 Transact-SQL `uniqueidentifier` 함수를 사용하여 자동으로 생성할 수 있는 `NEWID()` 열에 저장됩니다. GUID를 기본 키로 사용하면 성능에 부정적 영향을 미칠 수 있습니다. SQL Server는 전역적으로 고유 `NEWSEQUENTIALID()` 하지 않을 수 있지만 더 효율적으로 인덱싱할 수 있는 순차적 GUID를 생성 하는 함수에 대 한 지원을 제공 합니다.

## <a name="retrieving-sql-server-identity-column-values"></a>SQL Server ID 열 값 검색

Microsoft SQL Server로 작업하는 경우에는 출력 매개 변수를 사용하는 저장 프로시저를 만들어서 삽입된 행에 대한 ID 값을 반환할 수 있습니다. 다음 테이블에서는 ID 열 값을 검색하는 데 사용할 수 있는 SQL Server의 세 가지 Transact-SQL 함수를 설명합니다.

|함수|Description|
|--------------|-----------------|
|SCOPE_IDENTITY|현재 실행 범위 내의 마지막 ID 값을 반환합니다. SCOPE_IDENTITY는 대부분의 시나리오에 권장됩니다.|
|@@IDENTITY|현재 세션의 모든 테이블에서 생성된 마지막 ID 값을 포함합니다. @@IDENTITY 는 트리거의 영향을 받을 수 있으며, 사용자가 원하는 id 값을 반환 하지 않을 수 있습니다.|
|IDENT_CURRENT|모든 세션 및 모든 범위의 특정 테이블에 대해 생성된 마지막 ID 값을 반환합니다.|

 다음 저장 프로시저는 **Categories** 테이블에 행을 삽입 하 고 output 매개 변수를 사용 하 여 transact-sql SCOPE_IDENTITY () 함수에 의해 생성 된 새 id 값을 반환 하는 방법을 보여 줍니다.

```sql
CREATE PROCEDURE dbo.InsertCategory
  @CategoryName nvarchar(15),
  @Identity int OUT
AS
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)
SET @Identity = SCOPE_IDENTITY()
```

그런 다음 저장 프로시저를 <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> 개체의 <xref:System.Data.SqlClient.SqlDataAdapter>의 소스로 지정할 수 있습니다. <xref:System.Data.SqlClient.SqlCommand.CommandType%2A>의 <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> 속성은 <xref:System.Data.CommandType.StoredProcedure>로 설정해야 합니다. ID 출력은 <xref:System.Data.SqlClient.SqlParameter>이 <xref:System.Data.ParameterDirection>인 <xref:System.Data.ParameterDirection.Output>를 만들어서 검색합니다. `UpdateRowSource.OutputParameters` `UpdateRowSource.Both` <xref:System.Data.SqlClient.SqlCommand.UpdatedRowSource%2A> 가 처리 되 면 삽입 명령의 속성을 또는로 설정한 경우 자동 증가 된 id 값이 반환 되 고 현재 행의 CategoryID 열에 배치 됩니다. `InsertCommand`

삽입 명령이 새 ID 값을 반환하는 INSERT 문과 SELECT 문이 모두 포함된 배치를 실행하는 경우에는 삽입 명령의 `UpdatedRowSource` 속성을 `UpdateRowSource.FirstReturnedRecord`로 설정하여 새 값을 검색할 수 있습니다.

[!code-csharp[DataWorks SqlClient.RetrieveIdentityStoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.RetrieveIdentityStoredProcedure/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.RetrieveIdentityStoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.RetrieveIdentityStoredProcedure/VB/source.vb#1)]

## <a name="merging-new-identity-values"></a>새 ID 값 병합

일반적인 시나리오는 `GetChanges`의 `DataTable` 메서드를 호출하여 변경된 행만 포함된 사본을 만들고 `Update`의 `DataAdapter` 메서드를 호출할 때 새 사본을 사용하는 것입니다. 이 방법은 변경된 행을 업데이트를 수행하는 별도의 구성 요소로 마샬링해야 할 때 특히 유용합니다. 업데이트 후 사본에는 원래 `DataTable`로 다시 병합되어야 하는 새 ID 값이 포함될 수 있습니다. 새 ID 값은 `DataTable`의 원래 값과 다를 가능성이 큽니다. 병합을 수행 하려면 새 id 값을 포함 하 는 새 행을 추가 하는 대신 원래 `DataTable`에서 기존 행을 찾아 업데이트 하기 위해 복사본에서 AutoIncrement 열의 원래 값을 유지 해야 합니다. . 하지만 `Update`는 업데이트된 각 `DataAdapter`에 대해 암시적으로 호출되기 때문에 기본적으로 원래 값은 `AcceptChanges`의 `DataRow` 메서드에 대한 호출 후에 손실됩니다.

`DataColumn` 업데이트 동안 `DataRow`에서 `DataAdapter`의 원래 값을 유지하는 방법에는 두 가지가 있습니다.

- 원래 값을 유지하는 첫 번째 방법은 `AcceptChangesDuringUpdate`의 `DataAdapter` 속성을 `false`로 설정하는 것입니다. 이 설정은 업데이트되는 `DataRow`의 모든 `DataTable`에 영향을 줍니다. 자세한 내용과 코드 예제는 <xref:System.Data.Common.DataAdapter.AcceptChangesDuringUpdate%2A>를 참조하세요.

- 두 번째 방법은 `RowUpdated`의 `DataAdapter` 이벤트 처리기에서 코드를 작성하여 <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A>를 <xref:System.Data.UpdateStatus.SkipCurrentRow>로 설정하는 것입니다. `DataRow`가 업데이트되지만 각 `DataColumn`의 원래 값은 유지됩니다. 이 방법을 사용하면 원하는 행의 원래 값만 유지할 수 있습니다. 예를 들어 <xref:System.Data.Common.RowUpdatedEventArgs.StatementType%2A>을 검사한 다음 <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A>이 <xref:System.Data.UpdateStatus.SkipCurrentRow>인 행의 `StatementType`만 `Insert`로 설정하여 추가된 행의 원래 값은 유지하고 편집 또는 삭제된 행은 원래 값을 유지하지 않도록 코드를 작성할 수 있습니다.

이 방법 중 하나를 사용하여 `DataRow` 업데이트 동안 `DataAdapter`의 원래 값을 유지하는 경우, ADO.NET에서는 각 `DataRow`의 원래 값을 유지하면서 `DataColumn`의 현재 값을 출력 매개 변수 또는 결과 집합의 첫 번째 반환 행을 통해 반환되는 새 값으로 설정하기 위한 일련의 작업을 수행합니다. 먼저 현재 값을 원래 값으로 유지하기 위해 `AcceptChanges`의 `DataRow` 메서드를 호출한 다음 새 값을 할당합니다. 그런 다음 `DataRows` 속성이 <xref:System.Data.DataRow.RowState%2A>로 설정된 <xref:System.Data.DataRowState.Added>의 `RowState` 속성을 <xref:System.Data.DataRowState.Modified>로 설정합니다. 이는 예상하지 않은 동작일 수 있습니다.

업데이트되는 각 <xref:System.Data.DataRow>에 명령 결과가 적용되는 방법은 각 <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A>의 <xref:System.Data.Common.DbCommand> 속성에 따라 결정됩니다. 이 속성은 `UpdateRowSource` 열거형의 값으로 설정됩니다.

다음 테이블에서는 `UpdateRowSource` 열거형 값이 업데이트된 행의 <xref:System.Data.DataRow.RowState%2A> 속성에 영향을 주는 방식을 설명합니다.

|멤버 이름|설명|
|-----------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|`AcceptChanges`가 호출되고 출력 매개 변수 값 또는 반환된 결과 집합 중 첫 번째 행의 값이 업데이트되는 `DataRow`에 추가됩니다. 적용할 값이 없으면 `RowState`는 <xref:System.Data.DataRowState.Unchanged>가 됩니다.|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|행이 반환되면 `AcceptChanges`가 호출되고 행이 `DataTable`의 변경된 행으로 매핑되어 `RowState`가 `Modified`로 설정됩니다. 행이 반환되지 않으면 `AcceptChanges`가 호출되지 않고 `RowState`는 `Added`로 유지됩니다.|
|<xref:System.Data.UpdateRowSource.None>|반환된 매개 변수 또는 행이 무시됩니다. `AcceptChanges`가 호출되지 않고 `RowState`는 `Added`로 유지됩니다.|
|<xref:System.Data.UpdateRowSource.OutputParameters>|`AcceptChanges`가 호출되고 모든 출력 매개 변수가 `DataTable`에서 변경된 행으로 매핑되어 `RowState`가 `Modified`로 설정됩니다. 출력 매개 변수가 없으면 `RowState`는 `Unchanged`가 됩니다.|

### <a name="example"></a>예제

이 예제에서는 `DataTable`에서 변경된 행을 추출하고 <xref:System.Data.SqlClient.SqlDataAdapter>를 사용하여 데이터 소스를 업데이트하고 새 ID 열 값을 검색하는 방법을 보여 줍니다. <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>는 두 개의 Transact-SQL 문을 실행합니다. 첫 번째는 INSERT 문이고, 두 번째는 SCOPE_IDENTITY 함수를 사용하여 ID 값을 검색하는 SELECT 문입니다.

```sql
INSERT INTO dbo.Shippers (CompanyName)
VALUES (@CompanyName);
SELECT ShipperID, CompanyName FROM dbo.Shippers
WHERE ShipperID = SCOPE_IDENTITY();
```

삽입 명령의 `UpdatedRowSource` 속성은 `UpdateRowSource.FirstReturnedRow`로 설정되고 <xref:System.Data.MissingSchemaAction>의 `DataAdapter` 속성은 `MissingSchemaAction.AddWithKey`로 설정됩니다. `DataTable`이 채워지고 코드는 `DataTable`에 새 행을 추가합니다. 그런 다음 변경된 행이 새 `DataTable`로 추출되고, DataTable이 `DataAdapter`로 전달되고 나면 DataAdapter에서 서버를 업데이트합니다.

[!code-csharp[DataWorks SqlClient.MergeIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.MergeIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/VB/source.vb#1)]

`OnRowUpdated` 이벤트 처리기는 <xref:System.Data.Common.RowUpdatedEventArgs.StatementType%2A>의 <xref:System.Data.SqlClient.SqlRowUpdatedEventArgs>을 검사하여 행이 삽입된 행인지 확인합니다. 행이 삽입된 행인 경우에는 <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> 속성이 <xref:System.Data.UpdateStatus.SkipCurrentRow>로 설정됩니다. 행이 업데이트되지만 행의 원래 데이터는 유지됩니다. 프로시저의 본문에서 <xref:System.Data.DataSet.Merge%2A> 메서드가 호출되어 새 ID 값을 원래 `DataTable`로 병합하고, 마지막으로 `AcceptChanges`가 호출됩니다.

[!code-csharp[DataWorks SqlClient.MergeIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/CS/source.cs#2)]
[!code-vb[DataWorks SqlClient.MergeIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.MergeIdentity/VB/source.vb#2)]

## <a name="retrieving-microsoft-access-autonumber-values"></a>Microsoft Access Autonumber 값 검색

이 단원에는 Jet 4.0 데이터베이스에서 `Autonumber` 값을 검색하는 방법을 보여 주는 샘플이 있습니다. Jet 데이터베이스 엔진은 출력 매개 변수를 사용하거나 배치로 여러 개의 문을 실행하는 것을 지원하지 않으므로, 위에 설명한 기술을 사용하여 삽입된 행에 할당된 새 `Autonumber` 값을 반환할 수 없습니다. 그러나 별도의 SELECT @ `RowUpdated` @IDENTITY 문을 실행 하 여 새 `Autonumber` 값을 검색 하는 코드를 이벤트 처리기에 추가할 수 있습니다.

### <a name="example"></a>예제

이 예제에서는 `MissingSchemaAction.AddWithKey`를 사용하여 스키마 정보를 추가하는 대신 먼저 `DataTable`을 올바른 스키마로 구성한 다음 <xref:System.Data.OleDb.OleDbDataAdapter>를 호출하여 `DataTable`을 채웁니다. 이 경우 **CategoryID** 열은 0부터 시작 하 여 삽입 된 각 행에 할당 된 값을 0에서 0으로 <xref:System.Data.DataColumn.AutoIncrement%2A> <xref:System.Data.DataColumn.AutoIncrementStep%2A> , `true`- <xref:System.Data.DataColumn.AutoIncrementSeed%2A> 1로 설정 하 여 감소 하도록 구성 됩니다. 그런 다음 코드에서 두 개의 새 행을 추가하고 `GetChanges`를 사용하여 변경된 행을 `DataTable` 메서드로 전달된 새 `Update`에 추가합니다.

[!code-csharp[DataWorks OleDb.JetAutonumberMerge#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/CS/source.cs#1)]
[!code-vb[DataWorks OleDb.JetAutonumberMerge#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/VB/source.vb#1)]

`RowUpdated` 이벤트 처리기에서는 동일한 열려 있는 <xref:System.Data.OleDb.OleDbConnection>을 `Update`의 `OleDbDataAdapter` 문으로 사용합니다. 또한, 삽입된 행에 대한 `StatementType`의 <xref:System.Data.OleDb.OleDbRowUpdatedEventArgs>을 검사합니다. 삽입 된 각 행에 대해 <xref:System.Data.OleDb.OleDbCommand> 새을 만들어 연결에서 SELECT @@IDENTITY 문을 실행 하 고의 `DataRow` **CategoryID** 열에 `Autonumber` 배치 되는 새 값을 반환 합니다. 그런 다음 `Status`에 대한 숨겨진 호출을 방지하기 위해 `UpdateStatus.SkipCurrentRow` 속성이 `AcceptChanges`로 설정됩니다. 프로시저의 본문에서 `Merge` 메서드가 호출되어 두 `DataTable` 개체를 병합하고, 마지막으로 `AcceptChanges`가 호출됩니다.

[!code-csharp[DataWorks OleDb.JetAutonumberMerge#2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/CS/source.cs#2)]
[!code-vb[DataWorks OleDb.JetAutonumberMerge#2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks OleDb.JetAutonumberMerge/VB/source.vb#2)]

### <a name="retrieving-identity-values"></a>ID 값 검색

열의 값이 고유해야 하는 경우에는 열을 ID로 설정하는 경우가 많습니다. 새 데이터의 ID 값이 필요한 경우도 있습니다. 이 샘플에서는 ID 값을 검색하는 방법을 보여 줍니다.

- 데이터를 삽입하고 ID 값을 반환하는 저장 프로시저를 만듭니다.

- 새 데이터를 삽입하고 결과를 표시하는 명령을 실행합니다.

- <xref:System.Data.SqlClient.SqlDataAdapter>를 사용하여 새 데이터를 삽입하고 결과를 표시합니다.

샘플을 컴파일하고 실행하기 전에 다음 스크립트를 사용하여 샘플 데이터베이스를 만들어야 합니다.

```sql
USE [master]
GO

CREATE DATABASE [MySchool]
GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE procedure [dbo].[CourseExtInfo] @CourseId int
as
select c.CourseID,c.Title,c.Credits,d.Name as DepartmentName
from Course as c left outer join Department as d on c.DepartmentID=d.DepartmentID
where c.CourseID=@CourseId

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
create procedure [dbo].[DepartmentInfo] @DepartmentId int,@CourseCount int output
as
select @CourseCount=Count(c.CourseID)
from course as c
where c.DepartmentID=@DepartmentId

select d.DepartmentID,d.Name,d.Budget,d.StartDate,d.Administrator
from Department as d
where d.DepartmentID=@DepartmentId

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
Create PROCEDURE [dbo].[GetDepartmentsOfSpecifiedYear]
@Year int,@BudgetSum money output
AS
BEGIN
        SELECT @BudgetSum=SUM([Budget])
  FROM [MySchool].[dbo].[Department]
  Where YEAR([StartDate])=@Year

SELECT [DepartmentID]
      ,[Name]
      ,[Budget]
      ,[StartDate]
      ,[Administrator]
  FROM [MySchool].[dbo].[Department]
  Where YEAR([StartDate])=@Year

END
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[GradeOfStudent]
-- Add the parameters for the stored procedure here
@CourseTitle nvarchar(100),@FirstName nvarchar(50),
@LastName nvarchar(50),@Grade decimal(3,2) output
AS
BEGIN
select @Grade=Max(Grade)
from [dbo].[StudentGrade] as s join [dbo].[Course] as c on
s.CourseID=c.CourseID join [dbo].[Person] as p on s.StudentID=p.PersonID
where c.Title=@CourseTitle and p.FirstName=@FirstName
and p.LastName= @LastName
END
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[InsertPerson]
-- Add the parameters for the stored procedure here
@FirstName nvarchar(50),@LastName nvarchar(50),
@PersonID int output
AS
BEGIN
    insert [dbo].[Person](LastName,FirstName) Values(@LastName,@FirstName)

    set @PersonID=SCOPE_IDENTITY()
END
Go

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[Person]([PersonID] [int] IDENTITY(1,1) NOT NULL,
[LastName] [nvarchar](50) NOT NULL,
[FirstName] [nvarchar](50) NOT NULL,
[HireDate] [datetime] NULL,
[EnrollmentDate] [datetime] NULL,
[Picture] [varbinary](max) NULL,
 CONSTRAINT [PK_School.Student] PRIMARY KEY CLUSTERED
(
[PersonID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[StudentGrade]([EnrollmentID] [int] IDENTITY(1,1) NOT NULL,
[CourseID] [nvarchar](10) NOT NULL,
[StudentID] [int] NOT NULL,
[Grade] [decimal](3, 2) NOT NULL,
 CONSTRAINT [PK_StudentGrade] PRIMARY KEY CLUSTERED
(
[EnrollmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
create view [dbo].[EnglishCourse]
as
select c.CourseID,c.Title,c.Credits,c.DepartmentID
from Course as c join Department as d on c.DepartmentID=d.DepartmentID
where d.Name=N'English'

GO
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)
SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF
SET IDENTITY_INSERT [dbo].[Person] ON

INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (1, N'Hu', N'Nan', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (2, N'Norman', N'Laura', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (3, N'Olivotto', N'Nino', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (4, N'Anand', N'Arturo', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (5, N'Jai', N'Damien', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (6, N'Holt', N'Roger', CAST(0x000097F100000000 AS DateTime), NULL)
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (7, N'Martin', N'Randall', CAST(0x00008B1A00000000 AS DateTime), NULL)
SET IDENTITY_INSERT [dbo].[Person] OFF
SET IDENTITY_INSERT [dbo].[StudentGrade] ON

INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (1, N'C1045', 1, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (2, N'C1045', 2, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (3, N'C1045', 3, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (4, N'C1045', 4, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (5, N'C1045', 5, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (6, N'C1061', 1, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (7, N'C1061', 3, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (8, N'C1061', 4, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (9, N'C1061', 5, CAST(1.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (10, N'C2021', 1, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (11, N'C2021', 2, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (12, N'C2021', 4, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (13, N'C2021', 5, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (14, N'C2042', 1, CAST(2.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (15, N'C2042', 2, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (16, N'C2042', 3, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (17, N'C2042', 5, CAST(3.00 AS Decimal(3, 2)))
SET IDENTITY_INSERT [dbo].[StudentGrade] OFF
ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
ALTER TABLE [dbo].[StudentGrade]  WITH CHECK ADD  CONSTRAINT [FK_StudentGrade_Student] FOREIGN KEY([StudentID])
REFERENCES [dbo].[Person] ([PersonID])
GO
ALTER TABLE [dbo].[StudentGrade] CHECK CONSTRAINT [FK_StudentGrade_Student]
GO
```

코드 목록은 다음과 같습니다.

> [!TIP]
> 코드 목록은 Access 데이터베이스 파일 MySchool.mdb를 참조합니다. C# [Code.msdn.microsoft.com](https://code.msdn.microsoft.com/How-to-Retrieve-the-511acece)에서 전체 또는 Visual Basic 샘플 프로젝트의 일부로 myschool를 다운로드할 수 있습니다.

```csharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Data.SqlClient;

class Program {
   static void Main(string[] args) {
      String SqlDbConnectionString = "Data Source=(local);Initial Catalog=MySchool;Integrated Security=True;Asynchronous Processing=true;";

      InsertPerson(SqlDbConnectionString, "Janice", "Galvin");
      Console.WriteLine();

      InsertPersonInAdapter(SqlDbConnectionString, "Peter", "Krebs");
      Console.WriteLine();

      String oledbConnectionString = "Provider=Microsoft.Jet.OLEDB.4.0; Data Source=Database\\MySchool.mdb";
      InsertPersonInJet4Database(oledbConnectionString, "Janice", "Galvin");
      Console.WriteLine();

      Console.WriteLine("Please press any key to exit.....");
      Console.ReadKey();
   }

   // Using stored procedure to insert a new row and retrieve the identity value
   static void InsertPerson(String connectionString, String firstName, String lastName) {
      String commandText = "dbo.InsertPerson";

      using (SqlConnection conn = new SqlConnection(connectionString)) {
         using (SqlCommand cmd = new SqlCommand(commandText, conn)) {
            cmd.CommandType = CommandType.StoredProcedure;

            cmd.Parameters.Add(new SqlParameter("@FirstName", firstName));
            cmd.Parameters.Add(new SqlParameter("@LastName", lastName));
            SqlParameter personId = new SqlParameter("@PersonID", SqlDbType.Int);
            personId.Direction = ParameterDirection.Output;
            cmd.Parameters.Add(personId);

            conn.Open();
            cmd.ExecuteNonQuery();

            Console.WriteLine("Person Id of new person:{0}", personId.Value);
         }
      }
   }

   // Using stored procedure in adapter to insert new rows and update the identity value.
   static void InsertPersonInAdapter(String connectionString, String firstName, String lastName) {
      String commandText = "dbo.InsertPerson";
      using (SqlConnection conn = new SqlConnection(connectionString)) {
         SqlDataAdapter mySchool = new SqlDataAdapter("Select PersonID,FirstName,LastName from [dbo].[Person]", conn);

         mySchool.InsertCommand = new SqlCommand(commandText, conn);
         mySchool.InsertCommand.CommandType = CommandType.StoredProcedure;

         mySchool.InsertCommand.Parameters.Add(
             new SqlParameter("@FirstName", SqlDbType.NVarChar, 50, "FirstName"));
         mySchool.InsertCommand.Parameters.Add(
             new SqlParameter("@LastName", SqlDbType.NVarChar, 50, "LastName"));

         SqlParameter personId = mySchool.InsertCommand.Parameters.Add(new SqlParameter("@PersonID", SqlDbType.Int, 0, "PersonID"));
         personId.Direction = ParameterDirection.Output;

         DataTable persons = new DataTable();
         mySchool.Fill(persons);

         DataRow newPerson = persons.NewRow();
         newPerson["FirstName"] = firstName;
         newPerson["LastName"] = lastName;
         persons.Rows.Add(newPerson);

         mySchool.Update(persons);
         Console.WriteLine("Show all persons:");
         ShowDataTable(persons, 14);
      }
   }

   /// For a Jet 4.0 database, we need use the single statement and event handler to insert new rows and retrieve the identity value.
   static void InsertPersonInJet4Database(String connectionString, String firstName, String lastName) {
      String commandText = "Insert into Person(FirstName,LastName) Values(?,?)";
      using (OleDbConnection conn = new OleDbConnection(connectionString)) {
         OleDbDataAdapter mySchool = new OleDbDataAdapter("Select PersonID,FirstName,LastName from Person", conn);

         // Create Insert Command
         mySchool.InsertCommand = new OleDbCommand(commandText, conn);
         mySchool.InsertCommand.CommandType = CommandType.Text;

         mySchool.InsertCommand.Parameters.Add(new OleDbParameter("@FirstName", OleDbType.VarChar, 50, "FirstName"));
         mySchool.InsertCommand.Parameters.Add(new OleDbParameter("@LastName", OleDbType.VarChar, 50, "LastName"));
         mySchool.InsertCommand.UpdatedRowSource = UpdateRowSource.Both;

         DataTable persons = CreatePersonsTable();

         mySchool.Fill(persons);

         DataRow newPerson = persons.NewRow();
         newPerson["FirstName"] = firstName;
         newPerson["LastName"] = lastName;
         persons.Rows.Add(newPerson);

         DataTable dataChanges = persons.GetChanges();

         mySchool.RowUpdated += OnRowUpdated;

         mySchool.Update(dataChanges);

         Console.WriteLine("Data before merging:");
         ShowDataTable(persons, 14);
         Console.WriteLine();

         persons.Merge(dataChanges);
         persons.AcceptChanges();

         Console.WriteLine("Data after merging");
         ShowDataTable(persons, 14);
      }
   }

   static void OnRowUpdated(object sender, OleDbRowUpdatedEventArgs e) {
      if (e.StatementType == StatementType.Insert) {
         // Retrieve the identity value
         OleDbCommand cmdNewId = new OleDbCommand("Select @@IDENTITY", e.Command.Connection);
         e.Row["PersonID"] = (Int32)cmdNewId.ExecuteScalar();

         // After the status is changed, the original values in the row are preserved. And the
         // Merge method will be called to merge the new identity value into the original DataTable.
         e.Status = UpdateStatus.SkipCurrentRow;
      }
   }

   // Create the Persons table before filling.
   private static DataTable CreatePersonsTable() {
      DataTable persons = new DataTable();

      DataColumn personId = new DataColumn();
      personId.DataType = Type.GetType("System.Int32");
      personId.ColumnName = "PersonID";
      personId.AutoIncrement = true;
      personId.AutoIncrementSeed = 0;
      personId.AutoIncrementStep = -1;
      persons.Columns.Add(personId);

      DataColumn firstName = new DataColumn();
      firstName.DataType = Type.GetType("System.String");
      firstName.ColumnName = "FirstName";
      persons.Columns.Add(firstName);

      DataColumn lastName = new DataColumn();
      lastName.DataType = Type.GetType("System.String");
      lastName.ColumnName = "LastName";
      persons.Columns.Add(lastName);

      DataColumn[] pkey = { personId };
      persons.PrimaryKey = pkey;

      return persons;
   }

   private static void ShowDataTable(DataTable table, Int32 length) {
      foreach (DataColumn col in table.Columns) {
         Console.Write("{0,-" + length + "}", col.ColumnName);
      }
      Console.WriteLine();

      foreach (DataRow row in table.Rows) {
         foreach (DataColumn col in table.Columns) {
            if (col.DataType.Equals(typeof(DateTime)))
               Console.Write("{0,-" + length + ":d}", row[col]);
            else if (col.DataType.Equals(typeof(Decimal)))
               Console.Write("{0,-" + length + ":C}", row[col]);
            else
               Console.Write("{0,-" + length + "}", row[col]);
         }

         Console.WriteLine();
      }
   }
}
```

## <a name="see-also"></a>참고자료

- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [행 상태 및 행 버전](./dataset-datatable-dataview/row-states-and-row-versions.md)
- [AcceptChanges 및 RejectChanges](./dataset-datatable-dataview/acceptchanges-and-rejectchanges.md)
- [데이터 집합 콘텐츠 병합](./dataset-datatable-dataview/merging-dataset-contents.md)
- [DataAdapter로 데이터 원본 업데이트](updating-data-sources-with-dataadapters.md)
- [ADO.NET 개요](ado-net-overview.md)
