---
title: 보안 고려 사항(Entity Framework)
ms.date: 03/30/2017
ms.assetid: 84758642-9b72-4447-86f9-f831fef46962
ms.openlocfilehash: 1865afb384cfff41ede953c00f01cc96aea9a080
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854252"
---
# <a name="security-considerations-entity-framework"></a>보안 고려 사항(Entity Framework)
이 항목에서는 Entity Framework 응용 프로그램 개발, 배포 및 실행과 관련 된 보안 고려 사항에 대해 설명 합니다. 또한 보안 .NET Framework 응용 프로그램을 만들기 위한 권장 사항을 따라야 합니다. 자세한 내용은 [보안 개요](../security-overview.md)를 참조 하세요.  
  
## <a name="general-security-considerations"></a>일반적인 보안 고려 사항  
 다음 보안 고려 사항은 Entity Framework를 사용 하는 모든 응용 프로그램에 적용 됩니다.  
  
#### <a name="use-only-trusted-data-source-providers"></a>신뢰할 수 있는 데이터 소스 공급자만 사용합니다.  
 데이터 소스와 통신하려면 공급자는 다음을 수행해야 합니다.  
  
- Entity Framework에서 연결 문자열을 받습니다.  
  
- 명령 트리를 데이터 소스의 기본 쿼리 언어로 변환합니다.  
  
- 결과 집합을 어셈블하여 반환합니다.  
  
 로그온 작업 중에 사용자 암호를 기반으로 하는 정보가 기본 데이터 소스의 네트워크 라이브러리를 통해 서버로 전달됩니다. 악의적인 공급자가 사용자 자격 증명을 도용하거나, 악성 쿼리를 생성하거나, 결과 집합을 조작할 수 있습니다.  
  
#### <a name="encrypt-your-connection-to-protect-sensitive-data"></a>연결을 암호화하여 중요한 데이터를 보호합니다.  
 Entity Framework는 데이터 암호화를 직접 처리 하지 않습니다. 사용자가 공용 네트워크를 통해 데이터에 액세스하는 경우 애플리케이션에서 데이터 소스에 대해 암호화된 연결을 설정하여 보안을 강화해야 합니다. 자세한 내용은 데이터 소스의 보안 관련 설명서를 참조하세요. SQL Server 데이터 원본에 대해서는 [SQL Server에 대 한 연결 암호화](https://go.microsoft.com/fwlink/?LinkId=119544)를 참조 하세요.  
  
#### <a name="secure-the-connection-string"></a>연결 문자열을 보호합니다.  
 애플리케이션 보안의 가장 중요한 목표 중 하나는 데이터 소스에 대한 액세스를 보호하는 것입니다. 연결 문자열을 안전하게 보호하지 않거나 잘못 생성하면 이로 인해 보안상 취약한 부분이 생길 수 있습니다. 연결 정보를 일반 텍스트로 저장하거나 메모리에 유지하면 전체 시스템을 손상시킬 위험이 있습니다. 다음은 연결 문자열을 보호하기 위한 권장 방법입니다.  
  
- SQL Server 데이터 소스에 Windows 인증을 사용합니다.  
  
     Windows 인증을 사용하여 SQL Server 데이터 소스에 연결하면 연결 문자열에 로그온 및 암호 정보가 포함되지 않습니다.  
  
- 보호되는 구성을 사용하여 구성 파일 섹션을 암호화합니다.  
  
     ASP.NET에서는 구성 파일에서 중요한 정보를 암호화할 수 있도록 보호되는 구성이라는 기능을 제공합니다. 보호되는 구성은 원래 ASP.NET용으로 디자인된 것이지만 Windows 애플리케이션의 구성 파일 섹션을 암호화하는 데도 사용할 수 있습니다. 새 보호 된 구성 기능에 대 한 자세한 설명은 [보호 된 구성을 사용 하 여 구성 정보 암호화](https://docs.microsoft.com/previous-versions/aspnet/53tyfkaw(v=vs.100))를 참조 하세요.  
  
- 보안 구성 파일에 연결 문자열을 저장합니다.  
  
     연결 문자열을 소스 코드에 포함하면 안 됩니다. 연결 문자열을 구성 파일에 저장할 수 있으며, 그러면 연결 문자열을 애플리케이션 코드에 포함할 필요가 없습니다. 기본적으로 엔터티 데이터 모델 마법사는 연결 문자열을 애플리케이션 구성 파일에 저장합니다. 무단 액세스를 방지하려면 이 파일을 보호해야 합니다.  
  
- 동적으로 연결을 만들 때는 연결 문자열 작성기를 사용합니다.  
  
     런타임에 연결 문자열을 생성해야 하는 경우 <xref:System.Data.EntityClient.EntityConnectionStringBuilder> 클래스를 사용합니다. 이 문자열 작성기 클래스는 잘못된 입력 정보의 유효성을 검사하고 이스케이프하여 연결 문자열 삽입 공격을 방지합니다. 자세한 내용은 [방법: EntityConnection 연결 문자열](how-to-build-an-entityconnection-connection-string.md)을 작성 합니다. 또한 적절 한 문자열 작성기 클래스를 사용 하 여 Entity Framework 연결 문자열의 일부인 데이터 소스 연결 문자열을 생성 합니다. ADO.NET 공급자에 대 한 연결 문자열 작성기에 대 한 자세한 내용은 [연결 문자열 작성기](../connection-string-builders.md)를 참조 하세요.  
  
 자세한 내용은 [연결 정보 보호](../protecting-connection-information.md)를 참조하세요.  
  
#### <a name="do-not-expose-an-entityconnection-to-untrusted-users"></a>EntityConnection을 신뢰할 수 없는 사용자에게 노출하지 않습니다.  
 <xref:System.Data.EntityClient.EntityConnection> 개체는 기본 연결의 연결 문자열을 노출합니다. <xref:System.Data.EntityClient.EntityConnection> 개체에 액세스할 수 있는 사용자는 기본 연결의 <xref:System.Data.ConnectionState>도 변경할 수 있습니다. <xref:System.Data.EntityClient.EntityConnection> 클래스는 스레드로부터 안전하지 않습니다.  
  
#### <a name="do-not-pass-connections-outside-the-security-context"></a>연결을 보안 컨텍스트 외부로 전달하지 않습니다.  
 연결이 설정된 후 보안 컨텍스트 외부로 해당 연결을 전달하면 안 됩니다. 예를 들어, 연결을 열 수 있는 권한이 있는 스레드에서 연결을 전역 위치에 저장하면 안 됩니다. 전역 위치에서 연결을 사용할 수 있으면 다른 악성 스레드에서 명시적으로 해당 권한이 부여되지 않아도 열린 연결을 사용할 수 있습니다.  
  
#### <a name="be-aware-that-logon-information-and-passwords-may-be-visible-in-a-memory-dump"></a>메모리 덤프에서 로그온 정보와 암호를 볼 수도 있습니다.  
 데이터 소스 로그온 및 암호 정보를 연결 문자열로 제공하는 경우 이 정보는 가비지 컬렉션에서 리소스를 다시 사용할 때까지 메모리에 유지됩니다. 따라서 암호 문자열이 언제 메모리에서 제거되는지 확인할 수 없습니다. 애플리케이션이 충돌할 경우 메모리 덤프 파일에 중요한 보안 정보가 포함될 수 있으며, 애플리케이션을 실행하는 사용자와 컴퓨터에 대한 관리자 액세스 권한을 가진 모든 사용자가 메모리 덤프 파일을 볼 수 있습니다. Microsoft SQL Server 연결에 Windows 인증을 사용합니다.  
  
#### <a name="grant-users-only-the-necessary-permissions-in-the-data-source"></a>데이터 소스에서 필요한 권한만 사용자에게 부여합니다.  
 데이터 소스 관리자는 필요한 권한만 사용자에게 부여해야 합니다. [!INCLUDE[esql](../../../../../includes/esql-md.md)]에서 데이터를 수정하는 DML 문(예: INSERT, UPDATE 또는 DELETE)을 지원하지 않는 경우에도 사용자가 데이터 소스에 대한 연결에 액세스할 수 있습니다. 악의적인 사용자는 이 연결을 사용하여 데이터 소스의 기본 언어로 DML 문을 실행할 수 있습니다.  
  
#### <a name="run-applications-with-the-minimum-permissions"></a>최소 권한으로 애플리케이션을 실행합니다.  
 관리 되는 응용 프로그램이 완전 신뢰 권한으로 실행 되도록 허용 하면 .NET Framework는 컴퓨터에 대 한 응용 프로그램의 액세스를 제한 하지 않습니다. 이로 인해 애플리케이션에서 전체 시스템을 손상시키는 보안상 취약한 부분이 생길 수 있습니다. .NET Framework에서 코드 액세스 보안 및 기타 보안 메커니즘을 사용 하려면 응용 프로그램이 작동 하도록 하는 데 필요한 부분 신뢰 권한 및 최소 권한 집합을 사용 하 여 응용 프로그램을 실행 해야 합니다. 다음 코드 액세스 권한은 Entity Framework 응용 프로그램에 필요한 최소 권한입니다.  
  
- <xref:System.Security.Permissions.FileIOPermission>: 지정한 메타데이터 파일을 열 수 있는 <xref:System.Security.Permissions.FileIOPermissionAccess.Write> 또는 디렉터리에서 메타데이터 파일을 검색할 수 있는 <xref:System.Security.Permissions.FileIOPermissionAccess.PathDiscovery>  
  
- <xref:System.Security.Permissions.ReflectionPermission>: LINQ to Entities 쿼리를 지원할 수 있는 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess>  
  
- <xref:System.Transactions.DistributedTransactionPermission>: <xref:System.Security.Permissions.PermissionState.Unrestricted><xref:System.Transactions>에 참여할 수 있는 <xref:System.Transactions.Transaction>  
  
- <xref:System.Security.Permissions.SecurityPermission>: <xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter> 인터페이스를 사용하여 예외를 serialize할 수 있는 <xref:System.Runtime.Serialization.ISerializable>  
  
- 데이터베이스 연결을 열고 데이터베이스에 대해 명령을 실행할 수 있는 권한 (예: <xref:System.Data.SqlClient.SqlClientPermission> SQL Server 데이터베이스)  
  
 자세한 내용은 [Code Access Security and ADO.NET](../code-access-security.md)을 참조하세요.  
  
#### <a name="do-not-install-untrusted-applications"></a>신뢰할 수 없는 애플리케이션을 설치하지 않습니다.  
 Entity Framework는 보안 권한을 적용 하지 않으며 신뢰할 수 있는지 여부에 관계 없이 프로세스에서 사용자가 제공한 데이터 개체 코드를 호출 합니다. 클라이언트 인증 및 권한 부여가 데이터 스토리지 및 해당 애플리케이션에서 수행되는지 확인합니다.  
  
#### <a name="restrict-access-to-all-configuration-files"></a>모든 구성 파일에 대한 액세스를 제한합니다.  
 관리자는 enterprisesec .config, app.config, machine.config 및 응용 프로그램 구성 파일 \<> *응용*프로그램을 포함 하 여 응용 프로그램에 대 한 구성을 지정 하는 모든 파일에 대 한 쓰기 권한을 제한 해야 합니다. exe .config.  
  
 공급자 고정 이름은 app.config에서 수정할 수 있습니다. 클라이언트 응용 프로그램은 강력한 이름을 사용하여 표준 공급자 팩터리 모델을 통해 기본 공급자에 액세스해야 합니다.  
  
#### <a name="restrict-permissions-to-the-model-and-mapping-files"></a>모델 및 매핑 파일에 대한 권한을 제한합니다.  
 관리자는 모델 및 매핑 파일(.edmx, .csdl, .ssdl 및 .msl)에 대한 쓰기 권한을 모델 또는 매핑을 수정하는 사용자로만 제한해야 합니다. Entity Framework는 런타임에 이러한 파일에 대 한 읽기 액세스만 필요 합니다. 또한 관리자는 엔터티 데이터 모델 도구에서 생성 된 개체 계층 및 미리 컴파일된 뷰 소스 코드 파일에 대 한 액세스를 제한 해야 합니다.  
  
## <a name="security-considerations-for-queries"></a>쿼리의 보안 고려 사항  
 다음 보안 고려 사항은 개념적 모델을 쿼리할 때 적용됩니다. 이러한 고려 사항은 EntityClient를 사용한 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 쿼리와 LINQ, [!INCLUDE[esql](../../../../../includes/esql-md.md)] 및 쿼리 작성기 메서드를 사용한 개체 쿼리에 적용됩니다.  
  
#### <a name="prevent-sql-injection-attacks"></a>SQL 삽입 공격을 방지합니다.  
 애플리케이션은 사용자나 다른 외부 에이전트로부터 외부 입력을 받아 그에 기반한 동작을 수행하는 경우가 많습니다. 사용자나 외부 에이전트에서 직접 또는 간접적으로 파생되는 모든 입력에는 인증되지 않은 작업을 수행하기 위해 대상 언어의 구문을 사용하는 콘텐츠가 있을 수 있습니다. 대상 언어가 Transact-sql과 같은 구조적 쿼리 언어 (SQL) 인 경우 이러한 조작을 SQL 삽입 공격 이라고 합니다. 악의적인 사용자는 쿼리에 직접 명령을 삽입하고 데이터베이스 테이블을 삭제하거나, 서비스 거부를 발생시키거나, 수행되는 작업의 특성을 다른 방식으로 변경할 수 있습니다.  
  
- [!INCLUDE[esql](../../../../../includes/esql-md.md)] 삽입 공격:  
  
     쿼리 조건자 및 매개 변수 이름에 사용되는 값에 악성 입력을 제공하여 [!INCLUDE[esql](../../../../../includes/esql-md.md)]에서 SQL 삽입 공격이 수행될 수 있습니다. SQL 삽입 공격의 위험을 방지하려면 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 명령 텍스트와 함께 사용자 입력을 결합하면 안 됩니다.  
  
     [!INCLUDE[esql](../../../../../includes/esql-md.md)] 쿼리는 해당 리터럴이 허용되는 모든 곳에서 매개 변수를 허용합니다. 외부 에이전트에서 쿼리로 직접 리터럴을 삽입하는 대신 매개 변수가 있는 쿼리를 사용해야 합니다. [쿼리 작성기 메서드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896238(v=vs.100)) 를 사용 하 여 Entity SQL를 안전 하 게 생성 하는 것도 고려해 야 합니다.  
  
- LINQ to Entities 삽입 공격:  
  
     쿼리 컴퍼지션은 LINQ to Entities에서 가능 하지만 개체 모델 API를 통해 수행 됩니다. 쿼리와 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 달리 LINQ to Entities 쿼리는 문자열 조작 이나 연결을 사용 하 여 구성 되지 않으며 기존 SQL 삽입 공격에 취약 하지 않습니다.  
  
#### <a name="prevent-very-large-result-sets"></a>결과 집합이 너무 커지지 않도록 합니다.  
 결과 집합이 매우 크면 클라이언트에서 결과 집합의 크기에 비례하여 리소스를 사용하는 작업을 수행할 경우 클라이언트 시스템이 종료될 수 있습니다. 결과 집합은 다음 조건에서 매우 커질 수 있습니다.  
  
- 적절한 필터 조건이 포함되지 않은, 큰 데이터베이스에 대한 쿼리  
  
- 서버에서 Cartesian 조인을 만드는 쿼리  
  
- 중첩된 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 쿼리  
  
 사용자 입력을 허용하는 경우 해당 입력으로 인해 결과 집합이 시스템에서 처리할 수 있는 것보다 더 커지지 않도록 해야 합니다. LINQ to Entities 또는의 <xref:System.Linq.Queryable.Take%2A> [!INCLUDE[esql](../../../../../includes/esql-md.md)] [LIMIT](./language-reference/limit-entity-sql.md) 연산자를 사용 하 여 결과 집합의 크기를 제한할 수도 있습니다.  
  
#### <a name="avoid-returning-iqueryable-results-when-exposing-methods-to-potentially-untrusted-callers"></a>신뢰할 수 없는 호출자에 메서드를 노출할 때 IQueryable 결과를 반환하지 않도록 합니다.  
 다음과 같은 이유로 신뢰할 수 없는 호출자에 노출되는 메서드에서 <xref:System.Linq.IQueryable%601> 형식을 반환하지 않도록 해야 합니다.  
  
- <xref:System.Linq.IQueryable%601> 형식을 노출하는 쿼리의 사용자가 보안 데이터를 노출하거나 결과 집합의 크기를 늘리는 메서드를 결과에 대해 호출할 수 있습니다. 예를 들어 다음과 같은 메서드 시그니처가 있다고 가정합니다.  
  
    ```  
    public IQueryable<Customer> GetCustomer(int customerId)  
    ```  
  
     이 쿼리의 사용자는 반환된 `.Include("Orders")` 에 대해 `IQueryable<Customer>` 를 호출하여 쿼리에서 노출하도록 의도되지 않은 데이터를 검색할 수 있습니다. 메서드의 반환 형식을 <xref:System.Collections.Generic.IEnumerable%601>로 변경하고 `.ToList()`와 같이 결과를 구체화하는 메서드를 호출하면 이 문제를 방지할 수 있습니다.  
  
- <xref:System.Linq.IQueryable%601> 쿼리는 결과가 반복될 때 실행되므로 <xref:System.Linq.IQueryable%601> 형식을 노출하는 쿼리의 사용자가 throw된 예외를 catch할 수 있습니다. 예외에는 사용자에게 허용되지 않는 정보가 포함될 수 있습니다.  
  
## <a name="security-considerations-for-entities"></a>엔터티의 보안 고려 사항  
 다음 보안 고려 사항은 엔터티 형식을 생성하고 사용할 때 적용됩니다.  
  
#### <a name="do-not-share-an-objectcontext-across-application-domains"></a>애플리케이션 도메인에서 ObjectContext를 공유하지 않습니다.  
 둘 이상의 애플리케이션 도메인과 <xref:System.Data.Objects.ObjectContext>를 공유하면 연결 문자열의 정보가 노출될 수 있습니다. 대신, serialized 개체 또는 개체 그래프를 다른 애플리케이션 도메인으로 전송한 다음 해당 애플리케이션 도메인의 <xref:System.Data.Objects.ObjectContext>에 개체를 연결해야 합니다. 자세한 내용은 [개체 직렬화](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738446(v=vs.100))합니다.  
  
#### <a name="prevent-type-safety-violations"></a>형식 안전성을 위반하지 않도록 합니다.  
 형식 안전성을 위반 하는 경우 Entity Framework는 개체의 데이터 무결성을 보장할 수 없습니다. 형식 안전성 위반은 신뢰할 수 없는 애플리케이션이 완전 신뢰 코드 액세스 보안을 사용하여 실행될 수 있도록 하는 경우에 발생할 수 있습니다.  
  
#### <a name="handle-exceptions"></a>예외 처리  
 <xref:System.Data.Objects.ObjectContext>의 메서드 및 속성은 try-catch 블록 내에서 액세스합니다. 예외를 catch하면 처리되지 않은 예외로 인해 <xref:System.Data.Objects.ObjectStateManager>의 항목이나 테이블 이름 같은 모델 정보가 애플리케이션 사용자에게 노출되는 것을 방지할 수 있습니다.  
  
## <a name="security-considerations-for-aspnet-applications"></a>ASP.NET 애플리케이션의 보안 고려 사항  

ASP.NET 응용 프로그램에서 경로를 사용 하는 경우 다음 사항을 고려해 야 합니다.  
  
#### <a name="verify-whether-your-host-performs-path-checks"></a>호스트에서 경로 검사를 수행하는지 여부를 확인합니다.  
 `|DataDirectory|` (파이프 기호 안에 포함 됨) 대체 문자열이 사용 되는 경우 ADO.NET는 확인 된 경로가 지원 되는지 확인 합니다. 예를 들어, ".."은 `DataDirectory` 뒤에 사용할 수 없습니다. 웹 응용 프로그램 루트 연산자 (`~`)를 확인 하는 것과 동일한 검사는 ASP.NET를 호스팅하는 프로세스에 의해 수행 됩니다. IIS는이 검사를 수행 합니다. 그러나 IIS 이외의 호스트는 확인 된 경로가 지원 되는지 확인할 수 없습니다. Entity Framework 응용 프로그램을 배포 하는 호스트의 동작을 알고 있어야 합니다.  
  
#### <a name="do-not-make-assumptions-about-resolved-path-names"></a>확인된 경로 이름에 대해 가정하지 않습니다.  
 응용 프로그램의 런타임 중에 루트 연산자 (`~`) `DataDirectory` 및 대체 문자열을 확인 하는 값이 일정 하 게 유지 되어야 하지만 Entity Framework 호스트에서 이러한 값을 수정 하는 것을 제한 하지 않습니다.  
  
#### <a name="verify-the-path-length-before-deployment"></a>배포 전에 경로 길이를 확인합니다.  
 Entity Framework 응용 프로그램을 배포 하기 전에 루트 연산자 (~) 및 `DataDirectory` 대체 문자열의 값이 운영 체제의 경로 길이 제한을 초과 하지 않는지 확인 해야 합니다. ADO.NET 데이터 공급자는 경로 길이가 유효한 제한 범위 내에 있는지 확인 하지 않습니다.  
  
## <a name="security-considerations-for-adonet-metadata"></a>ADO.NET 메타데이터의 보안 고려 사항  
 다음 보안 고려 사항은 모델 및 매핑 파일을 생성하고 사용할 때 적용됩니다.  
  
#### <a name="do-not-expose-sensitive-information-through-logging"></a>로깅을 통해 중요한 데이터를 노출하지 않습니다.  
ADO.NET metadata service 구성 요소는 개인 정보를 기록 하지 않습니다. 액세스 제한으로 인해 반환할 수 없는 결과가 있을 경우 데이터베이스 관리 시스템과 파일 시스템에서 중요한 정보가 포함될 수 있는 예외를 발생시키는 대신 0개 결과를 반환해야 합니다.  
  
#### <a name="do-not-accept-metadataworkspace-objects-from-untrusted-sources"></a>신뢰할 수 없는 소스의 MetadataWorkspace 개체를 허용하지 않습니다.  
 애플리케이션에서 신뢰할 수 없는 소스의 <xref:System.Data.Metadata.Edm.MetadataWorkspace> 클래스 인스턴스를 허용하면 안 됩니다. 대신, 명시적으로 작업 영역을 생성하고 해당 소스에서 채워야 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [배포 고려 사항](deployment-considerations.md)
- [마이그레이션 고려 사항](migration-considerations.md)
