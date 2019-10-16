---
title: ADO.NET에서 Side-by-Side 실행
ms.date: 03/30/2017
ms.assetid: 9f9ba96d-9f89-4f65-bb2f-6860879f4393
ms.openlocfilehash: 0ada258f74338fc7cbc9435fdea8fc896bd2efd6
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782704"
---
# <a name="side-by-side-execution-in-adonet"></a>ADO.NET에서 Side-by-Side 실행
.NET Framework의 side-by-side 실행은 응용 프로그램이 컴파일되는 버전을 사용 하 여 여러 버전의 .NET Framework가 설치 된 컴퓨터에서 응용 프로그램을 실행할 수 있는 기능입니다. Side-by-side 실행을 구성 하는 방법에 대 한 자세한 내용은 side-by-side [실행](../../deployment/side-by-side-execution.md)을 참조 하세요.  
  
 한 버전의 .NET Framework을 사용 하 여 컴파일된 응용 프로그램은 다른 버전의 .NET Framework에서 실행할 수 있습니다. 그러나 설치 된 각 버전의 .NET Framework에 대 한 응용 프로그램 버전을 컴파일하여 개별적으로 실행 하는 것이 좋습니다. 두 경우 모두 응용 프로그램의 이전 버전과의 호환성 또는 이전 버전과의 호환성에 영향을 줄 수 있는 릴리스 간 ADO.NET의 변경 내용을 알고 있어야 합니다.  
  
## <a name="forward-compatibility-and-backward-compatibility"></a>다음 버전 및 이전 버전과의 호환성  
 이후 버전과의 호환성은 응용 프로그램이 이전 버전의 .NET Framework로 컴파일될 수 있지만 이후 버전의 .NET Framework에서는 성공적으로 실행 됨을 의미 합니다. .NET Framework 버전 1.1 용으로 작성 된 ADO.NET 코드는 이후 버전과 호환 됩니다.  
  
 이전 버전과의 호환성은 응용 프로그램이 최신 버전의 .NET Framework에 대해 컴파일되므로 기능 손실 없이 이전 버전의 .NET Framework에서 계속 실행 됨을 의미 합니다. 물론 새 버전의 .NET Framework에 도입 된 기능에 대 한 경우는 아닙니다.  
  
## <a name="the-net-framework-data-provider-for-odbc"></a>.NET Framework Data Provider for ODBC  
 버전 1.1부터 ODBC (<xref:System.Data.Odbc>)에 대 한 .NET Framework Data Provider .NET Framework 일부로 포함 됩니다. ODBC 데이터 공급자는 [데이터 액세스 및 저장소 개발자 센터](https://go.microsoft.com/fwlink/?linkid=4173)에서 웹 다운로드로 .NET Framework 버전 1.0 개발자에 게 제공 됩니다. ODBC 용 다운로드 된 .NET Framework Data Provider에 대 한 네임 스페이스는 **Microsoft. Data. odbc**입니다.  
  
 ODBC 데이터 공급자를 사용 하 여 데이터 원본에 연결 하는 .NET Framework 버전 1.0 용 응용 프로그램을 개발 했 고 .NET Framework 버전 1.1 이상 버전에서 해당 응용 프로그램을 실행 하려는 경우 ODBC dat에 대 한 네임 스페이스를 업데이트 해야 합니다. **데이터**공급자입니다. 그런 다음 최신 버전의 .NET Framework에 대해 다시 컴파일해야 합니다.  
  
 ODBC 데이터 공급자를 사용 하 여 데이터 원본에 연결 하는 .NET Framework 버전 2.0 이상용 응용 프로그램을 개발한 경우 .NET Framework 버전 1.0에서 해당 응용 프로그램을 실행 하려면 ODBC 데이터 공급자를 다운로드 하 여 설치 해야 합니다. .NET Framework 버전 1.0 시스템에서 그런 다음 ODBC 데이터 공급자에 대 한 네임 스페이스를 **Microsoft. data. odbc**로 변경 하 고 .NET Framework 버전 1.0에 대 한 응용 프로그램을 다시 컴파일해야 합니다.  
  
## <a name="the-net-framework-data-provider-for-oracle"></a>.NET Framework Data Provider for Oracle  
 버전 1.1부터 Oracle (<xref:System.Data.OracleClient>)에 대 한 .NET Framework Data Provider .NET Framework 일부로 포함 됩니다. 데이터 공급자는 [데이터 액세스 및 저장소 개발자 센터](https://go.microsoft.com/fwlink/?linkid=4173)에서 웹 다운로드로 .NET Framework 버전 1.0 개발자에 게 제공 됩니다.  
  
 데이터 공급자를 사용 하 여 데이터 원본에 연결 하는 .NET Framework 버전 2.0 이상용 응용 프로그램을 개발 했 고 .NET Framework 버전 1.0에서 해당 응용 프로그램을 실행 하려는 경우 데이터 공급자를 다운로드 하 여에 설치 해야 합니다. T Framework 버전 1.0 시스템입니다.  
  
## <a name="code-access-security"></a>코드 액세스 보안  
 .NET Framework 버전 1.0 (<xref:System.Data.SqlClient>, <xref:System.Data.OleDb>)의 .NET Framework 데이터 공급자는 FullTrust 권한으로 실행 해야 합니다. FullTrust 권한이 없는 영역에서 .NET Framework 버전 1.0의 .NET Framework k 데이터 공급자를 사용 하려고 하면이 발생 <xref:System.Security.SecurityException>합니다.  
  
 그러나 .NET Framework 버전 2.0부터 시작 하 여 부분적으로 신뢰할 수 있는 영역에서 모든 .NET Framework 데이터 공급자를 사용할 수 있습니다. 또한 .NET Framework 버전 1.1의 .NET Framework 데이터 공급자에 새 보안 기능이 추가 되었습니다. 이 기능으로 특정 보안 영역에서 사용할 수 있는 연결 문자열을 제한할 수 있습니다. 뿐만 아니라 특정 보안 영역에 대해 빈 암호 사용을 비활성화할 수도 있습니다. 자세한 내용은 [Code Access Security and ADO.NET](code-access-security.md)을 참조하세요.  
  
 .NET Framework 설치 마다 별도의 보안 .config 파일이 있기 때문에 보안 설정에 호환성 문제가 없습니다. 그러나 응용 프로그램이 .NET Framework 버전 1.1 이상에 포함 된 ADO.NET의 추가 보안 기능에 종속 되는 경우 버전 1.0 시스템에 배포할 수 없습니다.  
  
## <a name="sqlcommand-execution"></a>SqlCommand 실행  
 .NET Framework 버전 1.1부터 데이터 소스에서 명령을 실행 하 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 는 방법이 변경 되었습니다.  
  
 .NET Framework 버전 1.0 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 에서는 **sp_executesql** 저장 프로시저의 컨텍스트에서 모든 명령을 실행 했습니다. 따라서 연결 상태에 영향을 주는 SET NOCOUNT ON과 같은 명령은 현재 명령의 실행에만 적용됩니다. 연결 상태는 연결이 열려 있는 동안 실행되는 모든 후속 명령에 대해 수정되지 않습니다.  
  
 .NET Framework 버전 1.1 이상 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 에서는 명령에 매개 변수가 포함 된 경우에만 **sp_executesql** 저장 프로시저의 컨텍스트에서 명령을 실행 하 여 성능상의 이점을 제공 합니다. 따라서 연결 상태에 영향을 주는 명령이 매개 변수가 없는 명령에 포함된 경우 연결이 열려 있는 동안 실행되는 모든 후속 명령의 연결 상태가 수정됩니다.  
  
 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 호출에서 다음 배치 명령을 실행할 수 있습니다.  
  
```sql
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
```  
  
 .NET Framework 버전 1.1 이상에서는 연결이 열려 있는 동안 실행 되는 모든 후속 명령에 대해 NOCOUNT가 ON으로 유지 됩니다. .NET Framework 버전 1.0에서 NOCOUNT는 현재 명령 실행에 대해서만 설정 됩니다.  
  
 이러한 변경은 두 버전의 .NET Framework에 대 한의 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 동작에 의존 하는 경우 응용 프로그램의 이후 버전과 이전 버전과의 호환성에 모두 영향을 줄 수 있습니다.  
  
 이전 및 이후 버전의 .NET Framework에서 실행 되는 응용 프로그램의 경우 실행 중인 버전과 관계 없이 동작이 동일한 지 확인 하기 위해 코드를 작성할 수 있습니다. 명령을 통해 모든 후속 명령에 대한 연결 상태가 수정되도록 하려면 <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>를 사용하여 명령을 실행하는 것이 좋습니다. 명령을 통해 모든 후속 명령에 대한 연결이 수정되지 않도록 하려면 명령에 연결 상태를 다시 설정하는 명령을 포함하는 것이 좋습니다. 예:  
  
```sql
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
SET NOCOUNT OFF;  
```  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](ado-net-overview.md)
- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
