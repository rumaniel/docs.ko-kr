---
title: Oracle 시퀀스
ms.date: 03/30/2017
ms.assetid: 27cd371d-8252-414d-b5b2-5d31fa44b585
ms.openlocfilehash: 772aeda94215ccc8e1eff0e1145ed0399791197d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794591"
---
# <a name="oracle-sequences"></a>Oracle 시퀀스
.NET Framework Data Provider for Oracle은 삽입을 수행한 후 <xref:System.Data.OracleClient.OracleDataAdapter>를 사용하여 서버에서 생성한 Oracle 시퀀스 키 값을 검색하는 작업을 지원합니다.  
  
 SQL Server와 Oracle은 기본 키로 지정할 수 있는 자동 증분 열의 생성을 지원합니다. 이러한 값은 서버에 의해 행으로 생성되어 테이블에 추가됩니다. 이를 위해서는 SQL Server에서는 열의 Identity 속성을 설정하고, Oracle에서는 시퀀스를 만듭니다. SQL Server의 자동 증분 열과 Oracle의 시퀀스의 차이점은 다음과 같습니다.  
  
- SQL Server에서 열을 자동 증분 열로 표시하면 새 행을 삽입할 때 SQL Server에서 자동으로 열에 대해 새 값을 생성합니다.  
  
- Oracle에서는 테이블의 열에 대해 새 값을 생성하기 위해 시퀀스를 만들지만 시퀀스와 테이블 또는 열은 서로 독립적입니다. Oracle 시퀀스는 테이블이나 저장 프로시저와 같은 개체입니다.  
  
 Oracle 데이터베이스에 시퀀스를 만들 때 시퀀스 시작 값과 값 간의 증분 값을 정의할 수 있습니다. 새 행을 제출하기 전에 시퀀스에서 새 값을 쿼리할 수도 있습니다. 즉, 데이터베이스에 새 행을 삽입하기 전에 코드에서 새 행의 키 값을 인식할 수 있습니다.  
  
 SQL Server 및 ADO.NET를 사용 하 여 자동 증분 열을 만드는 방법에 대 한 자세한 내용은 [id 또는 일련 번호 값 검색](retrieving-identity-or-autonumber-values.md) 및 [AutoIncrement 열 만들기](./dataset-datatable-dataview/creating-autoincrement-columns.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 C# 예제에서는 Oracle 데이터베이스에서 새 시퀀스 값을 검색하는 방법을 보여 줍니다. 이 예제는 새 행을 제출하는 데 사용된 INSERT INTO 쿼리의 시퀀스를 참조한 후 Oracle10g에 소개된 RETURNING 절을 사용하여 생성된 시퀀스 값을 반환합니다. 이 예제에서는 "자리 표시자" 기본 키 값을 생성하는 ADO.NET의 자동 증분 기능을 사용하여 일련의 보류된 새 행을 <xref:System.Data.DataTable>에 추가합니다. ADO.NET이 새 행에 대해 생성한 증분 값은 "자리 표시자"일 뿐입니다. 즉, 데이터베이스에서는 ADO.NET이 생성한 값과는 다른 값을 생성할 수도 있습니다.  
  
 이 예제에서는 보류된 삽입을 데이터베이스에 제출하기 전에 행 내용을 표시합니다. 그런 다음 이 코드에서는 새 <xref:System.Data.OracleClient.OracleDataAdapter> 개체를 만들고 이 개체의 <xref:System.Data.OracleClient.OracleDataAdapter.InsertCommand%2A> 및 <xref:System.Data.OracleClient.OracleDataAdapter.UpdateBatchSize%2A> 속성을 설정합니다. 또한 이 예제에서는 출력 매개 변수를 사용하여 서버에서 생성한 값을 반환하는 논리를 제공합니다. 그런 다음 업데이트를 실행하여 보류된 행을 제출하고 <xref:System.Data.DataTable>의 내용을 표시합니다.  
  
```csharp  
public void OracleSequence(String connectionString)  
{  
   String insertString =   
      "INSERT INTO SequenceTest_Table (ID, OtherColumn)" +  
      "VALUES (SequenceTest_Sequence.NEXTVAL, :OtherColumn)" +  
      "RETURNING ID INTO :ID";  
  
   using (OracleConnection conn = new OracleConnection(connectionString))  
   {  
      //Open a connection.  
      conn.Open();  
      OracleCommand cmd = conn.CreateCommand();  
  
      // Prepare the database.  
      cmd.CommandText = "DROP SEQUENCE SequenceTest_Sequence";  
      try { cmd.ExecuteNonQuery(); } catch { }  
  
      cmd.CommandText = "DROP TABLE SequenceTest_Table";  
      try { cmd.ExecuteNonQuery(); } catch { }  
  
      cmd.CommandText = "CREATE TABLE SequenceTest_Table " +  
                     "(ID int PRIMARY KEY, OtherColumn varchar(255))";  
      cmd.ExecuteNonQuery();  
  
      cmd.CommandText = "CREATE SEQUENCE SequenceTest_Sequence " +  
                        "START WITH 100 INCREMENT BY 5";  
      cmd.ExecuteNonQuery();  
  
      DataTable testTable = new DataTable();  
      DataColumn column = testTable.Columns.Add("ID", typeof(int));  
      column.AutoIncrement = true;  
      column.AutoIncrementSeed = -1;  
      column.AutoIncrementStep = -1;  
      testTable.PrimaryKey = new DataColumn[] { column };  
      testTable.Columns.Add("OtherColumn", typeof(string));  
      for (int rowCounter = 1; rowCounter <= 15; rowCounter++)  
      {  
         testTable.Rows.Add(null, "Row #" + rowCounter.ToString());  
      }  
  
      Console.WriteLine("Before Update => ");  
      foreach (DataRow row in testTable.Rows)  
      {  
         Console.WriteLine("   {0} - {1}", row["ID"], row["OtherColumn"]);  
      }  
      Console.WriteLine();  
  
      cmd.CommandText =   
        "SELECT ID, OtherColumn FROM SequenceTest_Table";  
      OracleDataAdapter da = new OracleDataAdapter(cmd);  
      da.InsertCommand = new OracleCommand(insertString, conn);  
      da.InsertCommand.Parameters.Add(":ID", OracleType.Int32, 0, "ID");  
      da.InsertCommand.Parameters[0].Direction = ParameterDirection.Output;  
      da.InsertCommand.Parameters.Add(":OtherColumn", OracleType.VarChar, 255, "OtherColumn");  
      da.InsertCommand.UpdatedRowSource = UpdateRowSource.OutputParameters;  
      da.UpdateBatchSize = 10;  
  
      da.Update(testTable);  
  
      Console.WriteLine("After Update => ");  
      foreach (DataRow row in testTable.Rows)  
      {  
         Console.WriteLine("   {0} - {1}", row["ID"], row["OtherColumn"]);  
      }  
      // Close the connection.  
      conn.Close();  
   }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [Oracle 및 ADO.NET](oracle-and-adonet.md)
- [ADO.NET 개요](ado-net-overview.md)
