---
title: SQL Server 연결 풀링(ADO.NET)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e51d44e-7c4e-4040-9332-f0190fe36f07
ms.openlocfilehash: 2c73bec644a9a76ba05d3299183e8f1643c8e870
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794322"
---
# <a name="sql-server-connection-pooling-adonet"></a>SQL Server 연결 풀링(ADO.NET)
데이터베이스 서버에 연결하는 과정은 일반적으로 시간이 많이 걸리는 여러 단계로 이루어져 있습니다. 즉, 소켓이나 명명된 파이프 같은 실제 채널을 설정하고 서버와의 초기 핸드셰이크를 발생시키며 연결 문자열 정보를 구문 분석할 뿐 아니라 서버에 연결을 인증하고 현재 트랜잭션에 인리스트먼트하기 위해 검사를 실행해야 하는 등의 단계를 거쳐야 합니다.  
  
 실제로 대부분의 응용 프로그램에서는 연결을 위해 구성을 하나만 사용하거나 몇 개의 서로 다른 구성을 사용하기도 합니다. 따라서 응용 프로그램이 실행되는 동안 여러 개의 동일한 연결이 반복해서 열리고 닫히게 됩니다. 연결을 여는 비용을 최소화 하기 위해 ADO.NET에서는 *연결 풀링*이라는 최적화 기법을 사용 합니다.  
  
 연결 풀링을 사용하면 새 연결을 열어야 하는 횟수가 줄어듭니다. *풀러* 는 물리적 연결의 소유권을 유지 합니다. 주어진 각 연결 구성에 대해 활성 연결 집합을 활성화된 상태로 유지하여 연결을 관리합니다. 사용자가 연결에 `Open`을 호출할 때마다 풀러는 풀에서 사용 가능한 연결을 찾습니다. 풀링된 연결이 있으면 새 연결을 여는 대신 이를 호출자에게 반환합니다. 응용 프로그램에서 연결에 `Close`를 호출하면 풀러는 실제로 연결을 닫는 대신 풀링된 활성 연결 집합에 이를 반환합니다. 연결이 풀로 반환되면 다음에 `Open`을 호출할 때 다시 사용할 수 있는 준비를 갖추게 됩니다.  
  
 구성이 동일한 연결만 풀링할 수 있습니다. ADO.NET는 각 구성에 대해 하나씩, 여러 풀을 동시에 보관 합니다. 연결은 연결 문자열을 기준으로 풀로 나뉘며 통합 보안을 사용하는 경우에는 Windows ID를 기준으로 합니다. 또한 연결은 트랜잭션에 인리스트먼트되었는지 여부에 따라 풀링되기도 합니다. <xref:System.Data.SqlClient.SqlConnection.ChangePassword%2A>를 사용할 때는 <xref:System.Data.SqlClient.SqlCredential> 인스턴스가 연결 풀에 영향을 줍니다. <xref:System.Data.SqlClient.SqlCredential>의 개별 인스턴스는 사용자 ID 및 암호가 동일한 경우에도 서로 다른 연결 풀을 사용합니다.  
  
 연결 풀링을 사용하면 응용 프로그램의 성능 및 확장성을 대폭 향상시킬 수 있습니다. 기본적으로 연결 풀링은 ADO.NET에서 사용 하도록 설정 됩니다. 이를 명시적으로 비활성화하지 않는 한, 풀러는 응용 프로그램에서 열리고 닫히는 연결을 최적화합니다. 또한 여러 개의 연결 문자열 한정자를 지정하여 연결 풀링 동작을 제어할 수 있습니다. 자세한 내용은 이 항목 뒷부분에 있는 "연결 문자열 키워드를 사용하여 연결 풀링 제어"를 참조하세요.  
  
> [!NOTE]
> 연결 풀링을 사용하는 경우와 시간 초과 오류나 기타 로그인 오류가 발생하면 예외가 throw되고 이후 연결 시도가 "차단 기간"인 다음 5초 동안 적용되지 않습니다. 애플리케이션에서 차단 기간 내에 연결을 시도하면 첫 번째 예외가 다시 throw됩니다. 차단 기간이 끝난 후 또 다른 연결이 실패하면 이전 차단 기간의 두 배에서 최대 1분에 이르는 새 차단 기간이 적용됩니다.  
  
## <a name="pool-creation-and-assignment"></a>풀 만들기 및 할당  
 연결이 처음 열리면 연결에서 풀과 연결 문자열을 연결하는 정확한 일치 알고리즘에 따라 연결 풀이 만들어집니다. 각 연결 풀은 고유한 연결 문자열과 연결됩니다. 새 연결이 열릴 때 연결 문자열이 기존 풀과 정확히 일치하지 않으면 새 풀이 만들어집니다. 연결은 프로세스, 응용 프로그램 도메인, 연결 문자열을 기준으로 풀링되며 통합 보안을 사용하는 경우에는 Windows ID를 기준으로 풀링됩니다. 연결 문자열은 정확히 일치해야 합니다. 동일한 연결에 다른 순서로 제공된 키워드는 개별적으로 풀링됩니다.  
  
 다음 C# 예제에서는 새로운 <xref:System.Data.SqlClient.SqlConnection> 개체를 세 개 만들지만, 두 개의 연결 풀로만 이를 관리해야 합니다. 첫 번째와 두 번째 연결 문자열은 `Initial Catalog`에 대해 할당된 값이 다릅니다.  
  
```csharp
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=Northwind"))  
    {  
        connection.Open();        
        // Pool A is created.  
    }  
  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=pubs"))  
    {  
        connection.Open();        
        // Pool B is created because the connection strings differ.  
    }  
  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=Northwind"))  
    {  
        connection.Open();        
        // The connection string matches pool A.  
    }  
```  
  
 연결 문자열에 `MinPoolSize`가 지정되어 있지 않거나 0으로 지정되어 있으면 비활성 기간이 지난 후에 풀의 연결이 닫히게 됩니다. 그러나 지정된 `MinPoolSize`가 0보다 크면 `AppDomain`이 언로드되어 프로세스가 종료될 때까지 연결 풀이 제거되지 않습니다. 비활성 또는 빈 풀을 유지 관리하는 데에는 최소의 시스템 오버헤드만 있어도 됩니다.  
  
> [!NOTE]
> 장애 조치(failover)와 같은 심각한 오류가 발생하면 풀이 자동으로 지워집니다.  
  
## <a name="adding-connections"></a>연결 추가  
 각각의 고유 연결 문자열에 대해 연결 풀이 만들어집니다. 풀이 만들어지면 최소 풀 크기 요구 사항이 충족되도록 여러 개의 연결 개체가 만들어져 풀에 추가됩니다. 연결은 지정된 최대 풀 크기(기본값 100) 이하로 필요한 만큼 풀에 추가됩니다. 연결이 닫히거나 삭제되면 다시 풀로 회수됩니다.  
  
 <xref:System.Data.SqlClient.SqlConnection> 개체가 요청될 때 사용 가능한 연결이 있으면 풀에서 해당 개체를 가져올 수 있습니다. 연결을 사용하려면 연결이 현재 사용되고 있지 않고, 일치하는 트랜잭션 컨텍스트가 있거나 트랜잭션 컨텍스트와 연결되어 있지 않아야 하며, 서버에 대한 올바른 링크가 있어야 합니다.  
  
 연결 풀러는 연결이 다시 풀로 회수될 때 연결을 다시 할당하여 연결 요청을 처리합니다. 최대 풀 크기에 도달했는데 사용 가능한 연결이 없으면 요청이 대기됩니다. 그러면 풀러는 시간 제한(기본값 15초)에 도달할 때까지 연결을 회수합니다. 연결 제한 시간을 초과하기 전에 풀러가 요청을 처리하지 못하면 예외가 throw됩니다.  
  
> [!CAUTION]
> 사용이 끝난 연결은 풀로 반환되도록 항상 닫는 것이 좋습니다. `Close` C# `Using` `using` 개체의 `Dispose` 또는 메서드 중 하나를 사용 하거나의 문 내에서 모든 연결을 열거나 Visual Basic의 문을 사용 하 여이 작업을 수행할 수 있습니다. `Connection` 명시적으로 닫히지 않은 연결은 풀에 추가되거나 반환되지 않을 수 있습니다. 자세한 내용은 [using 문](../../../csharp/language-reference/keywords/using-statement.md) 또는 [방법: Visual Basic에 대 한 시스템](../../../visual-basic/programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md) 리소스를 삭제 합니다.  
  
> [!NOTE]
> 클래스의 `Close` 메서드에 있는 `Dispose`, `Connection` 또는 다른 관리 개체에 `DataReader` 또는 `Finalize`를 호출해서는 안 됩니다. 종료자에서는 클래스에 직접 속한 관리되지 않는 리소스만 해제합니다. 클래스에 관리되지 않는 리소스가 없는 경우 클래스 정의에 `Finalize` 메서드를 포함하지 마세요. 자세한 내용은 [가비지 수집](../../../standard/garbage-collection/index.md)합니다.  
  
열기 및 닫기 연결과 관련 된 이벤트에 대 한 자세한 내용은 SQL Server 설명서의 [Audit Login 이벤트 클래스](/sql/relational-databases/event-classes/audit-login-event-class) 및 [Audit Logout 이벤트 클래스](/sql/relational-databases/event-classes/audit-logout-event-class) 를 참조 하세요.  
  
## <a name="removing-connections"></a>연결 제거  
 연결이 4-8분 정도 유휴 상태였거나 풀러에서 서버와 연결하기 어렵다는 것을 감지하면 연결 풀러는 풀에서 연결을 제거합니다. 이러한 연결은 서버와 통신하려는 시도가 있어야만 감지할 수 있습니다. 서버에 더 이상 연결되지 않는 연결이 있으면 그 연결은 잘못된 연결로 표시됩니다. 잘못된 연결은 연결이 닫혀 있거나 회수되는 경우에만 연결 풀에서 제거됩니다.  
  
 네트워크에 존재하지 않는 서버에 대한 연결이 있는 경우 연결 풀러에서 이 연결을 검색하지 못하고 잘못된 연결로 표시하지 못해도 풀에서 선택할 수는 있습니다. 이는 연결이 여전히 유효한지 확인하는 오버헤드가 서버에 또 다른 라운드트립을 발생시켜 풀러를 사용하는 이점을 없애기 때문입니다. 이 경우 연결을 사용하려는 첫 번째 시도에서 연결하기 어렵다는 것을 감지하게 되며 예외가 throw됩니다.  
  
## <a name="clearing-the-pool"></a>풀 지우기  
 ADO.NET 2.0에서는 풀 <xref:System.Data.SqlClient.SqlConnection.ClearAllPools%2A> 을 지우는 두 가지 새로운 메서드인 및 <xref:System.Data.SqlClient.SqlConnection.ClearPool%2A>를 도입 했습니다. `ClearAllPools`는 지정된 공급자의 연결 풀을 지우며 `ClearPool`은 특정 연결과 관련된 연결 풀을 지웁니다. 메서드를 호출할 때 사용 중인 연결이 있으면 적절히 표시됩니다. 그리고 연결이 닫히면 풀로 반환되는 대신 삭제됩니다.  
  
## <a name="transaction-support"></a>트랜잭션 지원  
 연결은 트랜잭션 컨텍스트에 따라 풀에서 선택되어 할당됩니다. 연결 문자열에 `Enlist=false`가 지정되어 있는 경우를 제외하고 연결 풀에서는 연결이 <xref:System.Transactions.Transaction.Current%2A> 컨텍스트에 인리스트먼트되었는지 확인합니다. 연결이 닫혀 인리스트먼트된 `System.Transactions` 트랜잭션이 있는 풀로 반환되면 동일한 `System.Transactions` 트랜잭션이 있는 해당 연결 풀에 대한 다음 요청을 통해 동일한 연결(사용할 수 있는 경우)이 반환되도록 하는 데 따로 사용됩니다. 하지만, 그와 같은 요청이 실행되고 풀링된 연결을 사용할 수 없는 경우 연결은 풀의 비트랜잭트 부분에서 선택되어 인리스트먼트됩니다. 풀의 어느 영역에서도 연결을 사용할 수 없으면 새 연결이 만들어져 인리스트먼트됩니다.  
  
 연결이 닫힐 때는 풀로 다시 회수되고 트랜잭션 컨텍스트에 따라 적절한 분할로 회수됩니다. 따라서 분산 트랜잭션이 여전히 보류 중이더라도 오류를 생성하지 않고 연결을 닫을 수 있습니다. 이렇게 하여 분산 트랜잭션을 나중에 커밋하거나 취소할 수 있습니다.  
  
## <a name="controlling-connection-pooling-with-connection-string-keywords"></a>연결 문자열 키워드를 사용하여 연결 풀링 제어  
 `ConnectionString` 개체의 <xref:System.Data.SqlClient.SqlConnection> 속성에서는 연결 문자열 키/값 쌍을 사용하여 연결 풀링 논리의 동작을 조정할 수 있습니다. 자세한 내용은 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.  
  
## <a name="pool-fragmentation"></a>풀 조각화  
 풀 조각화는 응용 프로그램에서 프로세스가 종료될 때까지 해제되지 않는 많은 수의 풀을 만들어 낼 수 있는 여러 웹 응용 프로그램에 공통적으로 발생하는 문제입니다. 이렇게 되면 많은 수의 연결이 열려 있는 상태로 메모리를 소모하므로 성능이 저하됩니다.  
  
### <a name="pool-fragmentation-due-to-integrated-security"></a>통합 보안으로 인한 풀 조각화  
 연결은 연결 문자열과 사용자 ID에 따라 풀링합니다. 따라서 웹 사이트에 기본 인증이나 Windows 인증과 함께 통합 보안 로그인을 사용하는 경우 사용자당 풀의 수는 하나입니다. 이렇게 하면 단일 사용자에 대한 후속 데이터베이스 요청의 성능이 향상되지만 해당 사용자는 다른 사용자가 설정한 연결을 사용할 수 없습니다. 또한 데이터베이스 서버에 대한 사용자당 연결이 하나 이상이 됩니다. 이는 개발자가 보안 및 감사 요구 사항에 대해 검토해야 하는 특정 웹 응용 프로그램 아키텍처의 부작용입니다.  
  
### <a name="pool-fragmentation-due-to-many-databases"></a>많은 데이터베이스로 인한 풀 조각화  
 많은 인터넷 서비스 공급자가 단일 서버에서 여러 개의 웹 사이트를 호스트합니다. 이들은 단일 데이터베이스를 사용하여 폼 인증 로그인을 확인한 다음 해당 사용자나 사용자 그룹에 대해 특정 데이터베이스 연결을 열 수 있습니다. 그러면 인증 데이터베이스 연결이 풀링되어 모든 사용자가 사용하게 됩니다. 그러나 각 데이터베이스마다 개별 연결 풀이 있으므로 서버에 대한 연결 수가 증가하게 됩니다.  
  
 이 역시 응용 프로그램 디자인의 부작용입니다. 하지만 SQL Server에 연결할 때 보안 수준을 떨어뜨리지 않고 이러한 부작용을 비교적 간단히 해결할 수 있는 방법이 있습니다. 각 사용자나 그룹에 대해 개별 데이터베이스에 연결하는 대신 서버에 있는 동일한 데이터베이스에 연결한 다음 Transact-SQL USE 문을 실행하여 원하는 데이터베이스로 변경하는 것입니다. 다음 코드 조각에서는 `master` 데이터베이스에 대한 초기 연결을 만든 다음 이를 `databaseName` 문자열 변수에 지정된 원하는 데이터베이스로 전환하는 방법을 보여 줍니다.  
  
```vb  
' Assumes that command is a valid SqlCommand object and that  
' connectionString connects to master.  
    command.Text = "USE DatabaseName"  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    command.ExecuteNonQuery()  
End Using  
```  
  
```csharp  
// Assumes that command is a SqlCommand object and that  
// connectionString connects to master.  
command.Text = "USE DatabaseName";  
using (SqlConnection connection = new SqlConnection(  
  connectionString))  
  {  
    connection.Open();  
    command.ExecuteNonQuery();  
  }  
```  
  
## <a name="application-roles-and-connection-pooling"></a>응용 프로그램 역할 및 연결 풀링  
 `sp_setapprole` 시스템 저장 프로시저를 호출하여 SQL Server 응용 프로그램 역할을 활성화한 후에는 해당 연결의 보안 컨텍스트를 다시 설정할 수 없습니다. 그러나 풀링이 활성화된 경우 연결이 풀로 반환되고 풀링된 연결이 다시 사용될 때 오류가 발생합니다. 자세한 내용은 기술 자료 문서 "[OLE DB 리소스 풀링을 사용 하는 SQL 응용 프로그램 역할 오류](https://support.microsoft.com/default.aspx?scid=KB;EN-US;Q229564)"를 참조 하십시오.  
  
### <a name="application-role-alternatives"></a>응용 프로그램 역할의 대안  
 응용 프로그램 역할 대신 사용할 수 있는 보안 메커니즘을 사용하는 것이 좋습니다. 자세한 내용은 [SQL Server에서 응용 프로그램 역할 만들기](./sql/creating-application-roles-in-sql-server.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [연결 풀링](connection-pooling.md)
- [SQL Server 및 ADO.NET](./sql/index.md)
- [성능 카운터](performance-counters.md)
- [ADO.NET 개요](ado-net-overview.md)
