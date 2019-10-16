---
title: DbConnection, DbCommand 및 DbException
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 58aab611-7e6f-4749-b983-28ab7ae87dbe
ms.openlocfilehash: 09526f111adeecb817ce4c4e587ca3713e0d8cde
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785195"
---
# <a name="dbconnection-dbcommand-and-dbexception"></a>DbConnection, DbCommand 및 DbException
<xref:System.Data.Common.DbProviderFactory>와 <xref:System.Data.Common.DbConnection>을 만든 다음 명령과 데이터 판독기를 사용하여 데이터 소스에서 데이터를 검색할 수 있습니다.  
  
## <a name="retrieving-data-example"></a>데이터 검색 예제  
 다음 예제에서는 `DbConnection` 개체를 인수로 사용합니다. <xref:System.Data.Common.DbCommand>를 SQL SELECT 문으로 설정하여 Categories 테이블에서 데이터를 선택하기 위해 <xref:System.Data.Common.DbCommand.CommandText%2A>를 만듭니다. 이 코드에서는 Categories 테이블이 데이터 소스에 있다고 가정합니다. 연결이 열리고 <xref:System.Data.Common.DbDataReader>를 통해 데이터가 검색됩니다.  
  
 [!code-csharp[DataWorks DbProviderFactories.DbCommandData#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommandData/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbCommandData#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommandData/VB/source.vb#1)]  
  
## <a name="executing-a-command-example"></a>명령 실행 예제  
 다음 예제에서는 `DbConnection` 개체를 인수로 사용합니다. `DbConnection`이 유효하면 연결이 열리고 <xref:System.Data.Common.DbCommand>가 만들어져 실행됩니다. <xref:System.Data.Common.DbCommand.CommandText%2A>는 Northwind 데이터베이스의 Categories 테이블에 대해 삽입 작업을 수행하는 SQL INSERT 문으로 설정됩니다. 이 코드에서는 Northwind 데이터베이스가 데이터 소스에 있고 INSERT 문에 사용된 SQL 구문이 지정된 공급자에 대해 유효하다고 가정합니다. 데이터 소스에서 발생하는 오류는 <xref:System.Data.Common.DbException> 코드 블록에서 처리되고 다른 모든 예외는 <xref:System.Exception> 블록에서 처리됩니다.  
  
 [!code-csharp[DataWorks DbProviderFactories.DbCommand#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommand/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbCommand#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommand/VB/source.vb#1)]  
  
## <a name="handling-data-errors-with-dbexception"></a>DbException을 사용하여 데이터 오류 처리  
 <xref:System.Data.Common.DbException> 클래스는 데이터 소스와 관련하여 throw되는 모든 예외에 대한 기본 클래스입니다. 예외 처리 코드에서 이 클래스를 사용하면 특정 예외 클래스를 참조하지 않고도 다양한 공급자에 의해 throw되는 예외를 처리할 수 있습니다. 다음 코드 조각에서는 <xref:System.Data.Common.DbException>에 <xref:System.Exception.GetType%2A>, <xref:System.Exception.Source%2A>, <xref:System.Runtime.InteropServices.ExternalException.ErrorCode%2A> 및 <xref:System.Exception.Message%2A> 속성을 사용하여 데이터 소스에서 반환한 오류 정보를 표시하는 방법을 보여 줍니다. 오류 형식, 공급자 이름을 나타내는 소스, 오류 코드, 오류와 관련된 메시지 등이 출력에 표시됩니다.  
  
```vb  
Try  
    ' Do work here.  
Catch ex As DbException  
    ' Display information about the exception.  
    Console.WriteLine("GetType: {0}", ex.GetType())  
    Console.WriteLine("Source: {0}", ex.Source)  
    Console.WriteLine("ErrorCode: {0}", ex.ErrorCode)  
    Console.WriteLine("Message: {0}", ex.Message)  
Finally  
    ' Perform cleanup here.  
End Try  
```  
  
```csharp  
try  
{  
    // Do work here.  
}  
catch (DbException ex)  
{  
    // Display information about the exception.  
    Console.WriteLine("GetType: {0}", ex.GetType());  
    Console.WriteLine("Source: {0}", ex.Source);  
    Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);  
    Console.WriteLine("Message: {0}", ex.Message);  
}  
finally  
{  
    // Perform cleanup here.  
}  
```  
  
## <a name="see-also"></a>참고자료

- [DbProviderFactory](dbproviderfactories.md)
- [DbProviderFactory 가져오기](obtaining-a-dbproviderfactory.md)
- [DbDataAdapter로 데이터 수정](modifying-data-with-a-dbdataadapter.md)
- [ADO.NET 개요](ado-net-overview.md)
