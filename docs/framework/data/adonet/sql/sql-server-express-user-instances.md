---
title: SQL Server Express 사용자 인스턴스
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.openlocfilehash: fabd9b94b8c0a3f0e0db220e84d6c2eca3537c50
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894411"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express 사용자 인스턴스
Microsoft SQL Server Express Edition(SQL Server Express)은 .NET Framework Data Provider for SQL Server(`SqlClient`)를 사용하는 경우에만 사용 가능한 기능인 사용자 인스턴스를 지원합니다. 사용자 인스턴스는 부모 인스턴스에서 생성된 별도의 SQL Server Express 데이터베이스 엔진 인스턴스입니다. 로컬 컴퓨터에서 관리자가 아닌 사용자는 사용자 인스턴스를 사용하여 SQL Server Express 데이터베이스에 연결할 수 있습니다. 각 인스턴스는 사용자당 하나의 인스턴스를 기준으로 개인 사용자의 보안 컨텍스트 내에서 실행됩니다.  
  
## <a name="user-instance-capabilities"></a>사용자 인스턴스 기능  
 각 사용자는 Windows 관리자로 실행할 필요 없이 컴퓨터에서 실행되는 인스턴스에 대해 SQL Server 시스템 관리자(`sysadmin`) 권한을 가지므로, 사용자 인스턴스는 LUA(최소 권한 사용자 계정)에서 Windows를 실행하는 사용자에게 유용합니다. SQL Server Express의 인스턴스는 서비스가 아닌 사용자의 Windows 비관리자 계정에서 실행되므로 제한된 권한으로 사용자 인스턴스에서 실행되는 소프트웨어는 시스템 차원의 변경을 수행할 수 없습니다. 각 사용자 인스턴스는 부모 인스턴스 및 동일한 컴퓨터에서 실행되는 다른 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스에서 실행되는 데이터베이스는 단일 사용자 모드로만 열리므로 여러 사용자가 사용자 인스턴스에서 실행되는 데이터베이스에 연결할 수 없습니다. 사용자 인스턴스에서는 복제 및 분산 쿼리도 사용할 수 없습니다.  
  
 자세한 내용은 SQL Server 온라인 설명서의 "사용자 인스턴스"를 참조하세요.  
  
> [!NOTE]
> 사용자 인스턴스는 컴퓨터에서 사용자가 이미 관리자이거나 데이터베이스 사용자가 여러 명인 경우 필요하지 않습니다.  
  
## <a name="enabling-user-instances"></a>사용자 인스턴스 활성화  
 사용자 인스턴스를 생성하려면 SQL Server Express의 부모 인스턴스가 실행 중이어야 합니다. 사용자 인스턴스는 SQL Server Express 설치 될 때 기본적으로 사용 하도록 설정 되며, 시스템 관리자가 부모 인스턴스에서 **sp_configure** 시스템 저장 프로시저를 실행 하 여 명시적으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다.  
  
```sql  
-- Enable user instances.  
sp_configure 'user instances enabled','1'
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
 사용자 인스턴스의 네트워크 프로토콜은 명명된 로컬 파이프여야 합니다. 사용자 인스턴스는 SQL Server의 원격 인스턴스로 시작될 수 없으며 SQL Server 로그인은 허용되지 않습니다.  
  
## <a name="connecting-to-a-user-instance"></a>사용자 인스턴스에 연결  
 `User Instance` <xref:System.Data.SqlClient.SqlConnection> 및 키워드를사용하여사용자인스턴스에연결할수있습니다.`AttachDBFilename` <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 사용자 인스턴스는 <xref:System.Data.SqlClient.SqlConnectionStringBuilder>`UserInstance` 및 `AttachDBFilename` 속성에서도 지원됩니다.  
  
 아래 표시된 샘플 연결 문자열을 참조하세요.  
  
- `Data Source` 키워드는 사용자 인스턴스를 생성하는 SQL Server Express의 부모 인스턴스를 참조합니다. 기본 인스턴스는 .\sqlexpress입니다.  
  
- `Integrated Security`이 `true`로 설정됩니다. 사용자 인스턴스에 연결하려면 Windows 인증이 필요합니다. SQL Server 로그인은 지원되지 않습니다.  
  
- `User Instance`가 `true`로 설정되면 사용자 인스턴스를 호출합니다. 기본값은 `false`입니다.  
  
- `AttachDbFileName` 연결 문자열 키워드를 사용하여 전체 경로 이름을 포함하는 기본 데이터베이스 파일(.mdf)에 연결할 수 있습니다. `AttachDbFileName`은 또한 <xref:System.Data.SqlClient.SqlConnection> 연결 문자열 내의 "확장 속성" 및 "초기 파일 이름" 키에 해당합니다.  
  
- 파이프 기호 안에 포함된 `|DataDirectory|` 대체 문자열은 연결을 여는 애플리케이션의 데이터 디렉터리를 참조하며 .mdf 및 .ldf 데이터베이스 및 로그 파일의 위치를 나타내는 상대 경로를 제공합니다. 이러한 파일의 위치를 찾으려면 파일에 대한 전체 경로를 제공해야 합니다.  
  
```text
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
> <xref:System.Data.SqlClient.SqlConnectionStringBuilder><xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 및 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 속성을 사용하여 런타임에 연결 문자열을 빌드할 수도 있습니다.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>&#124;DataDirectory&#124; 대체 문자열 사용  
 ADO.NET 2.0에서는 `AttachDbFileName`(파이프 기호 안에 포함됨) 대체 문자열이 도입되어 `|DataDirectory|`이 확장되었습니다. `DataDirectory`는 `AttachDbFileName`과 함께 사용되어 데이터 파일의 상대 경로를 나타내기 때문에 개발자가 전체 경로를 지정할 필요 없이 데이터 소스의 상대 경로를 기반으로 연결 문자열을 만들 수 있습니다.  
  
 `DataDirectory`가 가리키는 실제 위치는 애플리케이션 형식에 따라 다릅니다. 이 예제에서 연결된 Northwind.mdf 파일은 애플리케이션의 \app_data 폴더에 있습니다.  
  
```text
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
 `DataDirectory`가 사용된 경우 디렉터리 구조에서 결과 파일 경로는 대체 문자열이 가리키는 디렉터리보다 높습니다. 예를 들어, 완전히 확장된 `DataDirectory`가 C:\AppDirectory\app_data인 경우 c:\AppDirectory보다 낮으므로 위에 표시된 샘플 연결 문자열이 사용됩니다. 그러나 `DataDirectory`를 `|DataDirectory|\..\data`로 지정하려고 하면 \data가 \AppDirectory의 하위 디렉터리가 아니므로 오류가 발생합니다.  
  
 연결 문자열에 형식이 적절하지 않은 대체 문자열이 있는 경우 <xref:System.ArgumentException>이 throw됩니다.  
  
> [!NOTE]
> <xref:System.Data.SqlClient>에서는 로컬 컴퓨터 파일 시스템에 대해 대체 문자열을 전체 경로로 적용합니다. 따라서 원격 서버, HTTP 및 UNC 경로 이름은 지원되지 않습니다. 서버가 로컬 컴퓨터에 없는 경우 연결이 열릴 때 예외가 throw됩니다.  
  
 <xref:System.Data.SqlClient.SqlConnection>이 열린 경우 기본 SQL Server Express 인스턴스로부터 호출자 계정에서 실행되는 런타임에 시작된 인스턴스로 리디렉션됩니다.  
  
> [!NOTE]
> 사용자 인스턴스는 일반 인스턴스보다 로드하는 데 오랜 시간이 걸리기 때문에 <xref:System.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 값을 늘릴 필요가 있습니다.  
  
 다음 코드 조각에서는 새 `SqlConnection`을 열어서 콘솔 창에 연결 문자열을 표시한 다음 `using` 코드 블록을 나갈 때 연결을 닫습니다.  
  
```vb  
Private Sub OpenSqlConnection()  
    ' Retrieve the connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    Using connection As New SqlConnection(connectionString)  
        connection.Open()  
        Console.WriteLine("ConnectionString: {0}", _  
           connection.ConnectionString)  
    End Using  
End Sub  
```  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
> SQL Server 내부에서 실행되는 CLR(공용 언어 런타임) 코드에서는 사용자 인스턴스가 지원되지 않습니다. 연결 문자열에 <xref:System.InvalidOperationException>를 포함하는 `Open`에서 <xref:System.Data.SqlClient.SqlConnection>이 호출되는 경우 `User Instance=true`이 throw됩니다.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>사용자 인스턴스 연결 수명  
 서비스로 실행되는 SQL Server 버전과 달리 SQL Server Express 인스턴스는 직접 시작하고 중지할 필요가 없습니다. 사용자가 사용자 인스턴스에 로그인하고 연결할 때 사용자 인스턴스가 이미 실행 중이 아닌 경우 시작됩니다. 사용자 인스턴스 데이터베이스에는 `AutoClose` 옵션이 설정되어 있어서 일정 시간 동안 비활성 상태이면 데이터베이스가 자동으로 종료됩니다. 시작된 sqlservr.exe 프로세스는 인스턴스에 대한 마지막 연결이 닫힌 후 제한된 시간 제한 기간 동안 계속해서 실행되므로, 시간 제한이 만료되기 전 다른 연결이 열려 있으면 프로세스를 다시 시작할 필요가 없습니다. 해당 시간 제한 기간이 만료되기 전에 새 연결이 열리지 않는 경우 사용자 인스턴스는 자동으로 종료됩니다. 부모 인스턴스의 시스템 관리자는 **sp_configure** 를 사용 하 여 사용자 **인스턴스 제한** 시간 옵션을 변경 하 여 사용자 인스턴스에 대 한 시간 제한 기간을 설정할 수 있습니다. 기본값은 60분입니다.  
  
> [!NOTE]
> 연결 문자열에서 0보다 큰 값이 `Min Pool Size`에 사용된 경우 연결 풀러에서는 항상 적은 수의 열린 연결을 유지하며 사용자 인스턴스는 자동으로 종료되지 않습니다.  
  
## <a name="how-user-instances-work"></a>사용자 인스턴스 사용 방법  
 사용자 인스턴스가 각 사용자에 대해 처음 생성 될 때 **master** 및 **msdb** 시스템 데이터베이스는 Template 데이터 폴더에서 사용자 인스턴스의 단독 사용을 위해 사용자의 로컬 응용 프로그램 데이터 리포지토리 디렉터리 아래 경로로 복사 됩니다. 이 경로는 일반적으로 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`입니다. 사용자 인스턴스가 시작 되 면 **tempdb**, 로그 및 추적 파일도이 디렉터리에 기록 됩니다. 인스턴스에 대해 각 사용자별로 고유한 이름이 생성됩니다.  
  
 기본적으로 Windows Builtin\Users 그룹의 모든 멤버에게는 로컬 인스턴스에 연결하는 권한뿐 아니라 SQL Server 이진 파일에 대한 읽기 및 실행 권한이 부여됩니다. 사용자 인스턴스를 호스트하는 호출 사용자의 자격 증명이 확인되면 해당 사용자는 해당 인스턴스에 대해 `sysadmin`이 됩니다. 사용자 인스턴스에 대해 공유 메모리만 활성화되므로 로컬 컴퓨터에 대한 작업만 가능합니다.  
  
 사용자에게는 연결 문자열에 지정된 .mdf 및 .ldf 파일에 대한 읽기 및 쓰기 권한이 모두 부여되어야 합니다.  
  
> [!NOTE]
> .mdf 및 .ldf 파일은 각각 데이터베이스 및 로그 파일을 나타냅니다. 이 두 파일은 서로 짝을 이루므로 백업 및 복원 작업을 하는 동안 같이 관리되어야 합니다. 데이터베이스 파일에는 로그 파일의 정확한 버전 정보가 들어 있으며 데이터베이스 파일이 잘못된 로그 파일과 짝을 이루는 경우 데이터베이스가 열리지 않습니다.  
  
 데이터 손상을 방지하려면 사용자 인스턴스의 데이터베이스를 배타적인 액세스 권한으로 엽니다. 서로 다른 두 개의 사용자 인스턴스가 동일한 컴퓨터에서 동일한 데이터베이스를 공유하는 경우 첫 번째 인스턴스에서 데이터베이스를 닫은 다음 두 번째 인스턴스에서 열어야 합니다.  
  
## <a name="user-instance-scenarios"></a>사용자 인스턴스 시나리오  
 사용자 인스턴스는 개발 컴퓨터에 관리자 계정을 가진 개발자에게 종속되지 않는 SQL Server 데이터 스토리지를 데이터베이스 애플리케이션 개발자에게 제공합니다. 사용자 인스턴스는 Access/Jet 모델에 기반을 두고 있으므로 데이터베이스 애플리케이션에서는 파일에 연결하기만 하며 권한을 부여하는 시스템 관리자의 개입 없이 사용자가 자동으로 모든 데이터베이스 개체에 대한 전체 권한을 가집니다. 사용자가 LUA(최소 권한 사용자 계정)에서 실행되어 서버 또는 로컬 컴퓨터에 대한 관리 권한은 없지만 데이터베이스 개체 및 애플리케이션을 만들어야 하는 환경에서 사용하면 적합합니다. 사용자는 사용자 인스턴스를 사용하여 보다 권한이 많은 시스템 서비스의 보안 컨텍스트 내가 아닌 사용자 고유의 보안 컨텍스트 내에서 실행되는 인스턴스를 런타임에 만들 수 있습니다.  
  
> [!IMPORTANT]
> 사용자 인스턴스는 사용자 인스턴스를 사용하는 모든 애플리케이션이 완전히 신뢰되는 시나리오에서 사용해야 합니다.  
  
 사용자 인스턴스 시나리오에는 다음과 같은 경우가 포함됩니다.  
  
- 공유 데이터가 필요하지 않은 단일 사용자 애플리케이션.  
  
- ClickOnce 배포. .NET Framework 2.0 이상 및 SQL Server Express가 이미 대상 컴퓨터에 설치되어 있는 경우, ClickOnce 동작의 결과로 다운로드된 설치 패키지를 관리자가 아닌 사용자가 설치하여 사용할 수 있습니다. SQL Server Express가 설치의 일부인 경우 관리자는 SQL Server Express를 설치해야 합니다. 자세한 내용은 [Windows Forms에 대 한 ClickOnce 배포](../../../winforms/clickonce-deployment-for-windows-forms.md)를 참조 하세요.
  
- Windows 인증을 사용하는 전용 ASP.NET 호스팅. 단일 SQL Server Express 인스턴스를 인트라넷에 호스트할 수 있습니다. 애플리케이션에서는 가장이 아닌 ASPNET Windows 계정을 사용하여 연결합니다. 모든 애플리케이션이 동일한 사용자 인스턴스를 공유하여 각 사용자에 대해 격리되지 않는 타사 또는 공유 호스팅 시나리오에서는 사용자 인스턴스를 사용하면 안 됩니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server 및 ADO.NET](index.md)
- [연결 문자열](../connection-strings.md)
- [데이터 소스에 연결](../connecting-to-a-data-source.md)
- [ADO.NET 개요](../ado-net-overview.md)
