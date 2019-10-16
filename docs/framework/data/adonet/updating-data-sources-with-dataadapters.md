---
title: DataAdapter로 데이터 원본 업데이트
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
ms.openlocfilehash: 4a6e22352a309f9d624c6922abc531cb31a5baf1
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736694"
---
# <a name="updating-data-sources-with-dataadapters"></a>DataAdapter로 데이터 원본 업데이트

`Update`의 <xref:System.Data.Common.DataAdapter> 메서드를 호출하면 <xref:System.Data.DataSet>의 변경 내용이 데이터 소스에 다시 적용됩니다. `Update` 메서드는 `Fill` 메서드와 마찬가지로 `DataSet`의 인스턴스, 선택적 <xref:System.Data.DataTable> 개체 또는 `DataTable` 이름을 인수로 사용합니다. `DataSet` 인스턴스는 변경 내용을 포함하는 `DataSet`이며 `DataTable`은 변경 내용을 검색할 테이블을 식별합니다. `DataTable`을 지정하지 않으면 `DataTable`의 첫 번째 `DataSet`이 사용됩니다.

`Update` 메서드를 호출하면 `DataAdapter`가 변경 내용을 분석하여 INSERT, UPDATE, DELETE 등의 적절한 명령을 실행합니다. `DataAdapter`에 대한 변경 사항이 발견되면 <xref:System.Data.DataRow>는 <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 또는 <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A>를 사용하여 변경 내용을 처리합니다. 이로써 가능한 경우 디자인 타임에 저장 프로시저를 사용하여 명령 구문을 지정함으로써 ADO.NET 애플리케이션의 성능을 최대화할 수 있습니다. `Update`를 호출하기 전에 명령을 명시적으로 설정해야 합니다. `Update`를 호출했는데 삭제된 행에 대한 `DeleteCommand`가 없는 경우와 같이 특정 업데이트에 사용할 적절한 명령이 없으면 예외가 throw됩니다.

> [!NOTE]
> SQL Server 저장 프로시저를 통해 `DataAdapter`로 데이터를 편집하거나 삭제하는 경우에는 저장 프로시저 정의에 SET NOCOUNT ON을 사용하면 안 됩니다. SET NOCOUNT ON을 사용하는 경우 반환되는 행 개수가 0이 되어 `DataAdapter`가 이를 동시성 충돌로 인식합니다. 그 결과 <xref:System.Data.DBConcurrencyException>이 throw됩니다.

명령 매개 변수를 사용하여 `DataSet`의 수정된 각 행에 대해 SQL 문이나 저장 프로시저의 입력 및 출력 값을 지정할 수 있습니다. 자세한 내용은 [DataAdapter 매개 변수](dataadapter-parameters.md)합니다.

> [!NOTE]
> <xref:System.Data.DataTable>에서의 행 삭제 및 제거의 차이점을 이해하는 것이 중요합니다. `Remove` 또는 `RemoveAt` 메서드를 호출하면 행이 즉시 제거됩니다. 그런 다음 `DataTable`에 `DataSet` 또는 `DataAdapter`을 전달하고 `Update`를 호출하면 백 엔드 데이터 소스에 있는 해당 행은 아무런 영향을 받지 않습니다. `Delete` 메서드를 사용하면 행이 `DataTable`에 그대로 남아 있고 삭제 표시됩니다. 그런 다음 `DataTable`에 `DataSet` 또는 `DataAdapter`을 전달하고 `Update`를 호출하면 백 엔드 데이터 소스의 해당 행이 삭제됩니다.

`DataTable`이 단일 데이터베이스 테이블에 매핑되거나 단일 데이터베이스 테이블에서 생성된 경우에는 <xref:System.Data.Common.DbCommandBuilder> 개체를 사용하여 `DeleteCommand`의 `InsertCommand`, `UpdateCommand` 및 `DataAdapter` 개체를 자동으로 생성할 수 있습니다. 자세한 내용은 [commandbuilder를 사용 하를 사용 하 여 명령 생성](generating-commands-with-commandbuilders.md)합니다.

## <a name="using-updatedrowsource-to-map-values-to-a-dataset"></a>UpdatedRowSource를 사용하여 DataSet에 값 매핑

`DataTable` 개체의 `DataAdapter` 속성을 사용하면 <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A>의 Update 메서드를 호출한 이후 데이터 소스에서 반환된 값이 <xref:System.Data.Common.DbCommand>에 다시 매핑되는 방법을 제어할 수 있습니다. `UpdatedRowSource` 속성을 <xref:System.Data.UpdateRowSource> 열거형 값 중 하나로 설정하면 `DataAdapter` 명령에서 반환하는 출력 매개 변수를 무시할지 아니면 `DataSet`의 변경된 행에 적용할지 제어할 수 있습니다. 반환되는 첫 번째 행이 있는 경우 이를 `DataTable`의 변경된 행에 적용할지 여부도 지정할 수 있습니다.

다음 표에서는 `UpdateRowSource` 열거형의 여러 값과 각 값이 `DataAdapter`에 사용하는 명령의 동작에 미치는 영향에 대해 설명합니다.

|UpdatedRowSource 열거형|설명|
|----------------------------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|출력 매개 변수 및 반환된 결과 집합의 첫 번째 행 모두 `DataSet`의 변경된 행에 매핑할 수 있습니다.|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|반환된 결과 집합의 첫 번째 행 데이터만 `DataSet`의 변경된 행에 매핑할 수 있습니다.|
|<xref:System.Data.UpdateRowSource.None>|출력 매개 변수 또는 반환된 결과 집합의 행이 모두 무시됩니다.|
|<xref:System.Data.UpdateRowSource.OutputParameters>|출력 매개 변수만 `DataSet`의 변경된 행에 매핑할 수 있습니다.|

`Update` 메서드는 변경 내용을 데이터 소스에 다시 적용하지만 사용자가 `DataSet`을 마지막으로 채운 이후에 다른 클라이언트에서 데이터 소스의 데이터를 수정했을 수도 있습니다. 현재 데이터로 `DataSet`을 새로 고치려면 `DataAdapter` 및 `Fill` 메서드를 사용합니다. 그러면 새 행이 테이블에 추가되고 업데이트된 정보가 기존 행에 통합됩니다. `Fill` 메서드는 `DataSet`에 있는 행과 `SelectCommand`에서 반환된 행의 기본 키 값을 검사하여 새 행을 추가할지 또는 기존 행을 업데이트할지 결정합니다. `Fill`가 반환한 결과 행의 기본 키 값과 일치하는 `DataSet` 행의 기본 키 값이 발견되면 `SelectCommand` 메서드는 기존 행을 `SelectCommand`가 반환한 행의 정보로 업데이트하고 기존 행의 <xref:System.Data.DataRow.RowState%2A>를 `Unchanged`로 설정합니다 `SelectCommand`가 반환한 행의 기본 키 값이 `DataSet` 행의 기본 키 값과 일치하지 않으면 `Fill` 메서드는 `RowState`가 `Unchanged`인 새 행을 추가합니다.

> [!NOTE]
> `SelectCommand`가 OUTER JOIN의 결과를 반환하면 `DataAdapter`는 결과 `PrimaryKey`에 대해 `DataTable` 값을 설정하지 않습니다. 행 중복 문제를 해결하려면 `PrimaryKey`를 직접 정의해야 합니다. 자세한 내용은 [기본 키 정의](./dataset-datatable-dataview/defining-primary-keys.md)합니다.

`Update` 메서드를 호출할 때 발생할 수 있는 예외를 처리 하려면 `RowUpdated` 이벤트를 사용 하 여 발생 하는 행 업데이트 오류에 대응 하거나 ( [DataAdapter 이벤트 처리](handling-dataadapter-events.md)참조) 또는을 이전으로 `DataAdapter.ContinueUpdateOnError` `true` 설정할 수 있습니다. 을 `Update`호출 하 고 업데이트가 완료 되 면 특정 행의 `RowError` 속성에 저장 된 오류 정보에 응답 합니다 ( [행 오류 정보](./dataset-datatable-dataview/row-error-information.md)참조).

> [!NOTE]
> `AcceptChanges` ,`DataTable`또는 에서를`Original` 호출 하면의 모든 값`DataRow`이에 대 한 `DataRow`값으로 덮어쓰여집니다. `Current` `DataSet` `DataRow` 행을 고유하게 식별하는 필드 값을 수정한 경우 `AcceptChanges`를 호출하면 `Original` 값이 데이터 소스의 값과 더 이상 일치하지 않습니다. `AcceptChanges`는 `DataAdapter`의 Update 메서드를 호출하는 동안 각 행에 대해 자동으로 호출됩니다. 먼저 `AcceptChangesDuringUpdate`의 `DataAdapter` 속성을 false로 설정하거나 `RowUpdated` 이벤트에 대한 이벤트 처리기를 만들고 <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A>를 <xref:System.Data.UpdateStatus.SkipCurrentRow>로 설정하면 Update 메서드를 호출할 때 원래 값을 보존할 수 있습니다. 자세한 내용은 [데이터 집합 콘텐츠 병합](./dataset-datatable-dataview/merging-dataset-contents.md) 및 [DataAdapter 이벤트 처리](handling-dataadapter-events.md)를 참조 하세요.

## <a name="example"></a>예제

다음 예제에서는 `UpdateCommand` `DataAdapter` 의를 명시적으로 설정 하 고 해당 `Update` 메서드를 호출 하 여 수정 된 행에 대 한 업데이트를 수행 하는 방법을 보여 줍니다. UPDATE 문의 WHERE 절에 지정된 매개 변수는 `Original`의 `SourceColumn` 값을 사용하도록 설정되어 있습니다. `Current` 값이 수정되어 데이터 소스에 있는 값과 일치하지 않을 수 있기 때문에 이 설정은 매우 중요합니다. `Original` 값은 데이터 소스에서 `DataTable`을 채우는 데 사용한 값입니다.

[!code-csharp[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/VB/source.vb#1)]

## <a name="autoincrement-columns"></a>AutoIncrement 열

데이터 소스의 테이블에 자동 증분 열이 있으면 저장 프로시저의 출력 매개 변수로 자동 증분 값을 반환하여 테이블의 열에 매핑하거나, 저장 프로시저 또는 SQL 문에서 반환된 결과 집합의 첫 번째 행에 있는 자동 증분 값을 반환하거나, `DataSet`의 `RowUpdated` 이벤트를 통해 추가적인 SELECT 문을 실행하여 `DataAdapter`의 열을 채울 수 있습니다. 자세한 내용 및 예제를 참조 하세요 [Retrieving Identity or Autonumber 값](retrieving-identity-or-autonumber-values.md)합니다.

## <a name="ordering-of-inserts-updates-and-deletes"></a>삽입, 업데이트 및 삭제 순서

대부분의 경우에는 `DataSet`을 통해 변경된 내용이 데이터 소스에 전송되는 순서가 매우 중요합니다. 예를 들어 기존 행의 기본 키 값을 업데이트하고 새 기본 키 값이 외래 키로 지정된 새 행을 추가하는 경우에는 삽입하기 전에 업데이트를 처리해야 합니다.

`Select`의 `DataTable` 메서드를 사용하여 특정 `DataRow`의 행만 참조하는 `RowState` 배열을 반환할 수 있습니다. 그런 다음 반환된 `DataRow` 배열을 `Update`의 `DataAdapter` 메서드에 전달하여 수정된 행을 처리할 수 있습니다. 업데이트될 행의 하위 집합을 지정하여 삽입, 업데이트 및 삭제가 처리되는 순서를 제어할 수 있습니다.

## <a name="example"></a>예제

예를 들어, 다음 코드에서는 테이블의 삭제된 행이 먼저 처리되고 업데이트된 행과 삽입된 행이 차례로 처리되도록 합니다.

```vb
Dim table As DataTable = dataSet.Tables("Customers")

' First process deletes.
dataSet.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.Deleted))

' Next process updates.
adapter.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.ModifiedCurrent))

' Finally, process inserts.
adapter.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.Added))
```

```csharp
DataTable table = dataSet.Tables["Customers"];

// First process deletes.
adapter.Update(table.Select(null, null, DataViewRowState.Deleted));

// Next process updates.
adapter.Update(table.Select(null, null,
  DataViewRowState.ModifiedCurrent));

// Finally, process inserts.
adapter.Update(table.Select(null, null, DataViewRowState.Added));
```

## <a name="use-a-dataadapter-to-retrieve-and-update-data"></a>DataAdapter를 사용하여 데이터 검색 및 업데이트

DataAdapter를 사용하여 데이터를 검색하고 업데이트할 수 있습니다.

- 이 샘플에서는 DataAdapter.AcceptChangesDuringFill을 사용하여 데이터베이스의 데이터를 복제합니다. 이 속성이 false로 설정되어 있으면 테이블을 채울 때 AcceptChanges가 호출되지 않으며 새로 추가된 행은 삽입된 행으로 처리됩니다. 따라서 이 샘플에서는 이러한 행을 사용하여 새 행을 데이터베이스에 삽입합니다.

- 이 샘플에서는 DataAdapter.TableMappings를 사용하여 소스 테이블과 DataTable 간의 매핑을 정의합니다.

- 이 샘플에서는 DataAdapter.FillLoadOption을 사용하여 어댑터가 DbDataReader에서 DataTable을 채우는 방법을 결정합니다. DataTable을 만드는 경우 이 속성을 LoadOption.Upsert 또는 LoadOption.PreserveChanges로 설정하여 현재 버전이나 원래 버전에 데이터베이스의 데이터를 쓸 수만 있습니다.

- 또한 이 샘플에서는 DbDataAdapter.UpdateBatchSize를 사용하여 배치 작업을 수행하는 방법으로 테이블을 업데이트합니다.

샘플을 컴파일 및 실행하기 전에 다음과 같이 샘플 데이터베이스를 만들어야 합니다.

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

ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
```

이 코드 샘플을 사용 하 여 C# 및 Visual Basic 프로젝트에서 찾을 수 있습니다 [개발자 코드 샘플](https://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=How%20to%20use%20DataAdapter%20to%20retrieve%20and%20update%20data&f%5B1%5D)합니다.

```csharp
using System;
using System.Data;
using System.Data.Common;
using System.Data.SqlClient;
using System.Linq;
using CSDataAdapterOperations.Properties;

namespace CSDataAdapterOperations.Properties {
   internal sealed partial class Settings : global::System.Configuration.ApplicationSettingsBase {

      private static Settings defaultInstance = ((Settings)(global::System.Configuration.ApplicationSettingsBase.Synchronized(new Settings())));

      public static Settings Default {
         get {
            return defaultInstance;
         }
      }

      [global::System.Configuration.ApplicationScopedSettingAttribute()]
      [global::System.Configuration.DefaultSettingValueAttribute("Data Source=(local);Initial Catalog=MySchool;Integrated Security=True")]
      public string MySchoolConnectionString {
         get {
            return ((string)(this["MySchoolConnectionString"]));
         }
      }
   }
}

class Program {
   static void Main(string[] args) {
      Settings settings = new Settings();

      // Copy the data from the database.  Get the table Department and Course from the database.
      String selectString = @"SELECT [DepartmentID],[Name],[Budget],[StartDate],[Administrator]
                                     FROM [MySchool].[dbo].[Department];

                                   SELECT [CourseID],@Year as [Year],Max([Title]) as [Title],
                                   Max([Credits]) as [Credits],Max([DepartmentID]) as [DepartmentID]
                                   FROM [MySchool].[dbo].[Course]
                                   Group by [CourseID]";

      DataSet mySchool = new DataSet();

      SqlCommand selectCommand = new SqlCommand(selectString);
      SqlParameter parameter = selectCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2);
      parameter.Value = new Random(DateTime.Now.Millisecond).Next(9999);

      // Use DataTableMapping to map the source tables and the destination tables.
      DataTableMapping[] tableMappings = {new DataTableMapping("Table", "Department"), new DataTableMapping("Table1", "Course")};
      CopyData(mySchool, settings.MySchoolConnectionString, selectCommand, tableMappings);

      Console.WriteLine("The following tables are from the database.");
      foreach (DataTable table in mySchool.Tables) {
         Console.WriteLine(table.TableName);
         ShowDataTable(table);
      }

      // Roll back the changes
      DataTable department = mySchool.Tables["Department"];
      DataTable course = mySchool.Tables["Course"];

      department.Rows[0]["Name"] = "New" + department.Rows[0][1];
      course.Rows[0]["Title"] = "New" + course.Rows[0]["Title"];
      course.Rows[0]["Credits"] = 10;

      Console.WriteLine("After we changed the tables:");
      foreach (DataTable table in mySchool.Tables) {
         Console.WriteLine(table.TableName);
         ShowDataTable(table);
      }

      department.RejectChanges();
      Console.WriteLine("After use the RejectChanges method in Department table to roll back the changes:");
      ShowDataTable(department);

      DataColumn[] primaryColumns = { course.Columns["CourseID"] };
      DataColumn[] resetColumns = { course.Columns["Title"] };
      ResetCourse(course, settings.MySchoolConnectionString, primaryColumns, resetColumns);
      Console.WriteLine("After use the ResetCourse method in Course table to roll back the changes:");
      ShowDataTable(course);

      // Batch update the table.
      String insertString = @"Insert into [MySchool].[dbo].[Course]([CourseID],[Year],[Title],
                                   [Credits],[DepartmentID])
             values (@CourseID,@Year,@Title,@Credits,@DepartmentID)";
      SqlCommand insertCommand = new SqlCommand(insertString);
      insertCommand.Parameters.Add("@CourseID", SqlDbType.NVarChar, 10, "CourseID");
      insertCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2, "Year");
      insertCommand.Parameters.Add("@Title", SqlDbType.NVarChar, 100, "Title");
      insertCommand.Parameters.Add("@Credits", SqlDbType.Int, 4, "Credits");
      insertCommand.Parameters.Add("@DepartmentID", SqlDbType.Int, 4, "DepartmentID");

      const Int32 batchSize = 10;
      BatchInsertUpdate(course, settings.MySchoolConnectionString, insertCommand, batchSize);
   }

   private static void CopyData(DataSet dataSet, String connectionString, SqlCommand selectCommand, DataTableMapping[] tableMappings) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         selectCommand.Connection = connection;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {adapter.TableMappings.AddRange(tableMappings);
            // If set the AcceptChangesDuringFill as the false, AcceptChanges will not be called on a
            // DataRow after it is added to the DataTable during any of the Fill operations.
            adapter.AcceptChangesDuringFill = false;

            adapter.Fill(dataSet);
         }
      }
   }

   // Roll back only one column or several columns data of the Course table by call ResetDataTable method.
   private static void ResetCourse(DataTable table, String connectionString,
       DataColumn[] primaryColumns, DataColumn[] resetColumns) {
      table.PrimaryKey = primaryColumns;

      // Build the query string
      String primaryCols = String.Join(",", primaryColumns.Select(col => col.ColumnName));
      String resetCols = String.Join(",", resetColumns.Select(col => $"Max({col.ColumnName}) as {col.ColumnName}"));

      String selectString = $"Select {primaryCols},{resetCols} from Course Group by {primaryCols}");

      SqlCommand selectCommand = new SqlCommand(selectString);

      ResetDataTable(table, connectionString, selectCommand);
   }

   // RejectChanges will roll back all changes made to the table since it was loaded, or the last time AcceptChanges
   // was called. When you copy from the database, you can lose all the data after calling RejectChanges
   // The ResetDataTable method rolls back one or more columns of data.
   private static void ResetDataTable(DataTable table, String connectionString,
       SqlCommand selectCommand) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         selectCommand.Connection = connection;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {
            // The incoming values for this row will be written to the current version of each
            // column. The original version of each column's data will not be changed.
            adapter.FillLoadOption = LoadOption.Upsert;

            adapter.Fill(table);
         }
      }
   }

   private static void BatchInsertUpdate(DataTable table, String connectionString,
       SqlCommand insertCommand, Int32 batchSize) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         insertCommand.Connection = connection;
         // When setting UpdateBatchSize to a value other than 1, all the commands
         // associated with the SqlDataAdapter have to have their UpdatedRowSource
         // property set to None or OutputParameters. An exception is thrown otherwise.
         insertCommand.UpdatedRowSource = UpdateRowSource.None;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter()) {
            adapter.InsertCommand = insertCommand;
            // Gets or sets the number of rows that are processed in each round-trip to the server.
            // Setting it to 1 disables batch updates, as rows are sent one at a time.
            adapter.UpdateBatchSize = batchSize;

            adapter.Update(table);

            Console.WriteLine("Successfully to update the table.");
         }
      }
   }

   private static void ShowDataTable(DataTable table) {
      foreach (DataColumn col in table.Columns) {
         Console.Write("{0,-14}", col.ColumnName);
      }
      Console.WriteLine("{0,-14}", "RowState");

      foreach (DataRow row in table.Rows) {
         foreach (DataColumn col in table.Columns) {
            if (col.DataType.Equals(typeof(DateTime)))
               Console.Write("{0,-14:d}", row[col]);
            else if (col.DataType.Equals(typeof(Decimal)))
               Console.Write("{0,-14:C}", row[col]);
            else
               Console.Write("{0,-14}", row[col]);
         }
         Console.WriteLine("{0,-14}", row.RowState);
      }
   }
}
```

## <a name="see-also"></a>참조

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [행 상태 및 행 버전](./dataset-datatable-dataview/row-states-and-row-versions.md)
- [AcceptChanges 및 RejectChanges](./dataset-datatable-dataview/acceptchanges-and-rejectchanges.md)
- [데이터 세트 콘텐츠 병합](./dataset-datatable-dataview/merging-dataset-contents.md)
- [ID 또는 일련 번호 값 검색](retrieving-identity-or-autonumber-values.md)
- [ADO.NET 개요](ado-net-overview.md)
