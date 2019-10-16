---
title: 명령 실행
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.openlocfilehash: f749ea37e1655f006e4de26e7cb279b778fe4faf
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795114"
---
# <a name="executing-a-command"></a>명령 실행
.NET Framework에 포함된 각 .NET Framework 데이터 공급자에는 <xref:System.Data.Common.DbCommand>에서 상속되는 고유 명령 개체가 있습니다. .NET Framework Data Provider for OLE DB에는 <xref:System.Data.OleDb.OleDbCommand> 개체가 있고, .NET Framework Data Provider for SQL Server에는 <xref:System.Data.SqlClient.SqlCommand> 개체가 있으며, .NET Framework Data Provider for ODBC와 .NET Framework Data Provider for Oracle에는 각각 <xref:System.Data.Odbc.OdbcCommand> 개체와 <xref:System.Data.OracleClient.OracleCommand> 개체가 있습니다. 이러한 각 개체는 명령의 유형 및 원하는 반환 값을 기준으로 명령 실행을 위한 메서드를 노출합니다. 다음 표에는 이러한 명령 및 해당 반환 값이 나와 있습니다.  
  
|명령|반환 값|  
|-------------|------------------|  
|`ExecuteReader`|`DataReader` 개체를 반환합니다.|  
|`ExecuteScalar`|단일 스칼라 값을 반환합니다.|  
|`ExecuteNonQuery`|어떠한 행도 반환하지 않는 명령을 실행합니다.|  
|`ExecuteXMLReader`|<xref:System.Xml.XmlReader>를 반환합니다. `SqlCommand` 개체에만 사용할 수 있습니다.|  
  
 강력한 형식의 각 명령 개체는 명령 문자열의 해석 방법을 지정하는 <xref:System.Data.CommandType> 열거형도 지원합니다. 다음 표에는 CommandType의 각 열거형이 나와 있습니다.  
  
|CommandType|Description|  
|-----------------|-----------------|  
|`Text`|데이터 소스에 실행할 문을 정의하는 SQL 명령입니다.|  
|`StoredProcedure`|저장 프로시저의 이름입니다. 호출하는 `Parameters` 메서드에 관계없이 명령의 `Execute` 속성을 사용하면 입력 및 출력 매개 변수와 반환 값에 액세스할 수 있습니다. `ExecuteReader`를 사용하는 경우 `DataReader`가 닫히기 전에는 반환 값과 출력 매개 변수에 액세스할 수 없습니다.|  
|`TableDirect`|테이블의 이름입니다.|  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 <xref:System.Data.SqlClient.SqlCommand> 개체를 만든 다음 해당 속성을 설정하여 저장 프로시저를 실행하는 방법을 보여 줍니다. 저장 프로시저에 대한 입력 매개 변수를 지정하는 데는 <xref:System.Data.SqlClient.SqlParameter> 개체를 사용합니다. <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 메서드를 사용하여 명령을 실행하고 <xref:System.Data.SqlClient.SqlDataReader>의 출력을 콘솔 창에 표시합니다.  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
### <a name="troubleshooting-commands"></a>명령 문제 해결  
 .NET Framework Data Provider for SQL Server는 실패한 명령 실행과 관련된 간헐적인 문제를 감지할 수 있도록 성능 카운터를 추가합니다. 자세한 내용은 [성능 카운터](performance-counters.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [명령 및 매개 변수](commands-and-parameters.md)
- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [ADO.NET 개요](ado-net-overview.md)
