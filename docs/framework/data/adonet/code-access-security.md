---
title: 코드 액세스 보안 및 ADO.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 93e099eb-daa1-4f1e-b031-c1e10a996f88
ms.openlocfilehash: 6340bc3fb2291601ba2a9812e0a438839f0718bc
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971816"
---
# <a name="code-access-security-and-adonet"></a>코드 액세스 보안 및 ADO.NET
.NET Framework는 역할 기반 보안과 CAS(코드 액세스 보안)를 제공합니다. 두 보안 기능 모두 CLR(공용 언어 런타임)이 제공하는 공용 인프라를 사용하여 구현되었습니다. 비관리 코드의 경우 대부분의 애플리케이션은 사용자 또는 보안 주체 권한으로 실행됩니다. 결과적으로 높은 권한을 가진 사용자가 악의적이거나 오류가 많은 소프트웨어를 실행하면 컴퓨터 시스템과 개인 데이터가 손상될 수 있습니다.  
  
 이와 달리, .NET Framework에서 실행되는 관리 코드에는 해당 코드에만 적용되는 코드 액세스 보안 기능이 있습니다. 코드 실행 여부는 보안 주체의 ID만으로 결정되는 것이 아니라 코드 출처나 코드 ID의 다른 특성에 따라 결정됩니다. 이는 관리 코드가 오용될 가능성을 줄여 줍니다.  
  
## <a name="code-access-permissions"></a>코드 액세스 권한  
 코드가 실행되면 CLR 보안 시스템이 평가하는 증명 정보를 제시하게 됩니다. 일반적으로 증명 정보는 URL, 사이트 및 영역이 포함된 코드의 원본 및 어셈블리의 ID를 보장하는 디지털 서명으로 이루어져 있습니다.  
  
 CLR은 코드에 수행 권한이 있는 작업만 수행하도록 허용합니다. 코드에서 권한을 요청할 수 있으며 이러한 요청은 관리자가 설정한 보안 정책에 따라 허용 여부가 결정됩니다.  
  
> [!NOTE]
> CLR에서 수행되는 코드는 자신에게 권한을 부여할 수 없습니다. 예를 들어 코드에서 보안 정책이 허용하는 것보다 낮은 권한을 요청하고 부여 받을 수는 있지만 그 이상의 권한은 부여 받을 수 없습니다. 권한을 부여할 때는 아무런 권한 없이 시작한 다음 수행하는 특정 작업에 필요한 최소한의 권한만 추가합니다. 모든 권한을 부여한 다음 필요하지 않은 권한을 개별적으로 허용하지 않으면 필요 이상의 권한이 주어질 수 있으므로 의도하지 않은 보안 허점이 생길 수 있습니다. 따라서 애플리케이션이 안전하지 않을 수 있습니다. 자세한 내용은 [보안 정책](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7c9c2y1w(v=vs.100)) 및 [보안 정책 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))구성을 참조 하세요.  
  
 코드 액세스 권한에는 다음 세 가지 형식이 있습니다.  
  
- `Code access permissions` 클래스에서 파생된 <xref:System.Security.CodeAccessPermission>. 파일 및 환경 변수와 같은 보호된 리소스에 액세스하고, 비관리 코드에 액세스하는 등의 보호된 작업을 수행하는 데 필요한 권한입니다.  
  
- `Identity permissions`은 어셈블리를 식별하는 특성을 나타냅니다. 디지털 서명이나 코드 출처와 같은 항목을 포함하는 증명 정보를 기준으로 어셈블리에 권한이 부여됩니다. <xref:System.Security.CodeAccessPermission> 기본 클래스에서 ID 권한이 파생되는 경우도 있습니다.  
  
- `Role-based security permissions`은 보안 주체가 지정된 ID를 가지고 있거나 지정된 역할의 멤버인지에 따라 결정됩니다. <xref:System.Security.Permissions.PrincipalPermission> 클래스를 사용하면 활성 보안 주체에 대해 선언적 권한 검사와 필수 권한 검사를 모두 수행할 수 있습니다.  
  
 리소스에 액세스하거나 작업을 수행할 수 있는 권한이 코드에 있는지 확인하기 위해서 런타임 보안 시스템은 호출 스택을 검색하여 각 호출자에게 부여된 권한과 요청된 권한을 비교합니다. 호출 스택의 호출자에게 요청된 권한이 없는 경우 <xref:System.Security.SecurityException>이 throw되고 액세스가 거부됩니다.  
  
### <a name="requesting-permissions"></a>권한 요청  
 권한을 요청하는 것은 애플리케이션 실행에 필요한 권한에 대한 정보를 런타임으로 전달하고 실제 필요한 권한만 부여되도록 하기 위한 것입니다. 예를 들어 애플리케이션에서 로컬 디스크에 데이터를 써야 한다면 <xref:System.Security.Permissions.FileIOPermission>이 필요합니다. 해당 권한이 부여되어 있지 않으면 애플리케이션에서 디스크에 쓰려고 할 때 오류가 발생합니다. 하지만 애플리케이션이 `FileIOPermission`을 요청하나 해당 권한이 부여되어 있지 않으면 애플리케이션이 초기에 예외를 생성하여 로드되지 않습니다.  
  
 애플리케이션이 디스크에서 데이터를 읽어 오기만 하면 되는 경우에는 쓰기 권한이 부여되지 않도록 요청할 수 있습니다. 이렇게 하면 버그나 악의적인 공격이 발생해도 코드가 작업 중인 데이터를 손상시킬 수 없습니다. 자세한 내용은 [권한 요청](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100))을 참조 하세요.  
  
## <a name="role-based-security-and-cas"></a>역할 기반 보안 및 CAS  
 역할 기반 보안과 CAS(코드 액세스 보안)를 모두 구현하면 애플리케이션의 전체적인 보안이 향상됩니다. 역할 기반 보안은 현재 스레드에서 보안 주체 관련 정보를 사용할 수 있도록 하여 Windows 계정이나 사용자 지정 ID에 따라 다르게 적용되도록 할 수 있습니다. 또한, 애플리케이션은 주로 사용자가 제공하는 자격 증명에 따라 데이터 또는 리소스에 액세스하는 데 필요합니다. 일반적으로 이러한 애플리케이션에서는 사용자의 역할을 확인한 후 해당 역할에 따라 리소스에 대한 액세스 권한을 제공합니다.  
  
 역할 기반 보안을 사용하면 구성 요소에서 현재 사용자와 그에 관련된 역할을 런타임에 식별할 수 있습니다. 그런 다음 CAS 정책을 사용하여 이 정보를 매핑함으로써 런타임에 부여된 권한 집합을 확인할 수 있습니다. 특정 애플리케이션 도메인의 경우 호스트가 기본 역할 기반 보안 정책을 변경할 수 있으며 사용자를 나타내는 기본 보안 주체 및 해당 사용자와 관련된 역할을 설정할 수 있습니다.  
  
 CLR에서는 관리 코드에 제한을 적용하는 메커니즘을 구현하기 위해 권한을 사용합니다. 역할 기반 보안 권한은 사용자(또는 사용자 역할을 하는 에이전트)가 특정 ID를 가지고 있는지 또는 지정된 역할의 멤버인지를 확인하는 메커니즘을 제공합니다. 자세한 내용은 [보안 권한](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5ba4k1c5(v=vs.100))을 참조 하세요.  
  
 빌드하려는 애플리케이션 종류에 따라 데이터베이스에 역할 기반 권한을 구현하는 것을 고려해야 합니다. SQL Server의 역할 기반 보안에 대 한 자세한 내용은 [SQL Server 보안](./sql/sql-server-security.md)을 참조 하세요.  
  
## <a name="assemblies"></a>어셈블리  
 어셈블리는 .NET Framework 애플리케이션에 대한 배포, 버전 제어, 재사용, 활성화 범위 및 보안 권한의 기본 단위를 형성합니다. 어셈블리는 함께 작동하도록 빌드되고 논리적 기능 단위를 형성하는 리소스 및 형식 컬렉션을 제공합니다. CLR의 경우 어셈블리 컨텍스트 외부에는 형식이 존재하지 않습니다. 어셈블리를 만들고 배포 하는 방법에 대 한 자세한 내용은 [어셈블리를 사용한 프로그래밍](../../../standard/assembly/program.md)을 참조 하세요.  
  
### <a name="strong-naming-assemblies"></a>어셈블리에 강력한 이름 지정  
 강력한 이름 또는 디지털 서명은 단순한 텍스트 이름, 버전 번호 및 문화권 정보(제공된 경우)를 포함하는 어셈블리의 ID에 공개 키와 디지털 서명이 추가되어 구성됩니다. 디지털 서명은 해당 프라이빗 키를 사용하여 어셈블리 파일에서 생성됩니다. 어셈블리 파일은 어셈블리를 구성하는 모든 파일의 이름과 해시가 들어 있는 어셈블리 매니페스트를 포함합니다.  
  
 어셈블리에 강력한 이름을 지정하면 다른 소프트웨어에서 애플리케이션이나 구성 요소를 명시적으로 참조하는 데 사용할 수 있는 고유 ID가 애플리케이션이나 구성 요소에 지정됩니다. 강력한 이름을 지정하면 부적절한 코드가 포함되어 있는 어셈블리로 인해 어셈블리가 스푸핑되지 않도록 보호됩니다. 또한 강력한 이름을 지정하면 구성 요소의 다양한 버전 간에 버전 관리 일관성을 유지할 수 있습니다. GAC(전역 어셈블리 캐시)에 배포할 어셈블리에는 강력한 이름을 지정해야 합니다. 자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](../../../standard/assembly/create-use-strong-named.md)을 참조하세요.  
  
## <a name="partial-trust-in-adonet-20"></a>ADO.NET 2.0에서의 부분 신뢰  
 ADO.NET 2.0에서 .NET Framework Data Provider for SQL Server, .NET Framework Data Provider for OLE DB, .NET Framework Data Provider for ODBC 및 .NET Framework Data Provider for Oracle은 현재 모두 부분적으로 신뢰할 수 있는 환경에서 실행됩니다. .NET Framework의 이전 릴리스의 경우, 부분적으로 신뢰할 수 있는 애플리케이션에서는 <xref:System.Data.SqlClient>만 지원되었습니다.  
  
 SQL Server 공급자를 사용하는 부분적으로 신뢰할 수 있는 애플리케이션은 실행 및 <xref:System.Data.SqlClient.SqlClientPermission> 권한이 있어야 합니다.  
  
### <a name="permission-attribute-properties-for-partial-trust"></a>부분 신뢰에 대한 권한 속성  
 부분 신뢰의 경우 <xref:System.Data.SqlClient.SqlClientPermissionAttribute> 멤버를 사용하여 .NET Framework Data Provider for SQL Server에서 사용할 수 있는 기능을 추가로 제한할 수 있습니다.  
  
 다음 표에서는 사용 가능한 <xref:System.Data.SqlClient.SqlClientPermissionAttribute> 속성과 해당 설명의 목록을 보여 줍니다.  
  
|권한 속성|Description|  
|-----------------------------------|-----------------|  
|`Action`|보안 동작을 가져오거나 설정합니다. <xref:System.Security.Permissions.SecurityAttribute>에서 상속됩니다.|  
|`AllowBlankPassword`|연결 문자열에서 빈 암호 사용을 활성화하거나 비활성화합니다. 빈 암호 사용을 활성화하는 `true`와 빈 암호 사용을 비활성화하는 `false`를 값으로 사용할 수 있습니다. <xref:System.Data.Common.DBDataPermissionAttribute>에서 상속됩니다.|  
|`ConnectionString`|허용되는 연결 문자열을 지정합니다. 여러 개의 연결 문자열을 식별할 수 있습니다. **참고:**  연결 문자열은 사용자 ID 또는 암호를 포함할 수 없습니다. 이번 릴리스에서는 .NET Framework 구성 도구를 사용하여 연결 문자열 제한을 변경할 수 없습니다. <br /><br /> <xref:System.Data.Common.DBDataPermissionAttribute>에서 상속됩니다.|  
|`KeyRestrictions`|허용되거나 허용되지 않는 연결 문자열 매개 변수를 식별합니다. 연결 문자열 매개 변수는 형식  *\<매개 변수 이름 > =* 에서 식별 됩니다. 여러 매개 변수를 세미콜론(;)으로 구분하여 지정할 수 있습니다. **참고:**  `KeyRestrictions`를 지정하지 않고 `KeyRestrictionBehavior` 속성을 `AllowOnly` 또는 `PreventUsage`로 설정한 경우에는 추가 연결 문자열 매개 변수가 허용되지 않습니다. <xref:System.Data.Common.DBDataPermissionAttribute>에서 상속됩니다.|  
|`KeyRestrictionBehavior`|연결 문자열 매개 변수를 허용되는 유일한 추가 매개 변수(`AllowOnly`)로 식별하거나 허용되지 않는 추가 매개 변수(`PreventUsage`)로 식별합니다. 기본값은 `AllowOnly`입니다. <xref:System.Data.Common.DBDataPermissionAttribute>에서 상속됩니다.|  
|`TypeID`|파생 클래스에서 구현될 때 이 특성의 고유 식별자를 가져옵니다. <xref:System.Attribute>에서 상속됩니다.|  
|`Unrestricted`|리소스에 무제한 권한이 선언되었는지 여부를 나타냅니다. <xref:System.Security.Permissions.SecurityAttribute>에서 상속됩니다.|  
  
#### <a name="connectionstring-syntax"></a>ConnectionString 구문  
 다음 예제에서는 구성 파일의 `connectionStrings` 요소를 사용하여 특정 연결 문자열만 사용하도록 하는 방법을 보여 줍니다. 구성 파일에서 연결 문자열을 저장 하 고 검색 하는 방법에 대 한 자세한 내용은 [연결 문자열](connection-strings.md) 을 참조 하세요.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictions-syntax"></a>KeyRestrictions 구문  
 다음 예에서는 동일한 연결 문자열을 사용 하도록 설정 하 `Encrypt` 고 및 `Packet Size` 연결 문자열 옵션을 사용 하도록 설정 하지만 다른 연결 문자열 옵션 사용은 제한 합니다.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Encrypt=;Packet Size=;"  
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-preventusage-syntax"></a>PreventUsage 구문을 사용한 KeyRestrictionBehavior  
 다음 예제에서는 동일한 연결 문자열을 사용하고 `User Id`, `Password` 및 `Persist Security Info`를 제외한 다른 모든 연결 매개 변수를 허용합니다.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="User Id=;Password=;Persist Security Info=;"  
    KeyRestrictionBehavior="PreventUsage" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-allowonly-syntax"></a>AllowOnly 구문을 사용한 KeyRestrictionBehavior  
 다음 예제에서는 `Initial Catalog`, `Connection Timeout`, `Encrypt` 및 `Packet Size` 매개 변수가 들어 있는 두 개의 연결 문자열을 사용합니다. 다른 모든 연결 문자열 매개 변수는 제한됩니다.  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
  
  <add name="DatabaseConnection2"   
    connectionString="Data Source=SqlServer2;Initial   
    Catalog=Northwind2;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
### <a name="enabling-partial-trust-with-a-custom-permission-set"></a>사용자 지정 권한 집합을 사용하여 부분 신뢰 활성화  
 특정 영역에 대해 <xref:System.Data.SqlClient> 권한 사용을 활성화하려면 시스템 관리자는 사용자 지정 권한 집합을 만들고 이를 특정 영역에 대한 권한 집합으로 설정해야 합니다. `LocalIntranet`과 같은 기본 권한 집합은 수정할 수 없습니다. <xref:System.Data.SqlClient> 예를 들어 <xref:System.Security.Policy.Zone> `LocalIntranet` <xref:System.Data.SqlClient> 의 `LocalIntranet`가 있는 코드에 대 한 권한을 포함 하려면 시스템 관리자가에 대 한 권한 집합을 복사 하 고 이름을 "CustomLocalIntranet"로 바꾼 다음 권한을 추가 합니다. 가져오기 [caspol.exe (코드 액세스 보안 정책 도구)](../../tools/caspol-exe-code-access-security-policy-tool.md)를 사용 하는 CustomLocalIntranet 권한 집합을 설정 하 고의 `LocalIntranet_Zone` 권한 집합을 CustomLocalIntranet로 설정 합니다.  
  
### <a name="sample-permission-set"></a>권한 집합 예제  
 다음은 부분 신뢰 권한일 경우의 .NET Framework Data Provider for SQL Server에 대한 권한 집합 예제입니다. 사용자 지정 권한 집합을 만드는 방법에 대 한 자세한 내용은 [caspol.exe를 사용 하 여 권한 집합 구성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/4ybs46y6(v=vs.100))을 참조 하세요.  
  
```xml  
<PermissionSet class="System.Security.NamedPermissionSet"  
  version="1"  
  Name="CustomLocalIntranet"  
  Description="Custom permission set given to applications on  
    the local intranet">  
  
<IPermission class="System.Data.SqlClient.SqlClientPermission, System.Data, Version=2.0.0000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
version="1"  
AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Integrated Security=true;"  
 KeyRestrictions="Initial Catalog=;Connection Timeout=;  
   Encrypt=;Packet Size=;"   
 KeyRestrictionBehavior="AllowOnly" />  
 </IPermission>  
</PermissionSet>  
```  
  
## <a name="verifying-adonet-code-access-using-security-permissions"></a>보안 권한을 사용하여 ADO.NET 코드 액세스 확인  
 부분 신뢰 권한의 경우 <xref:System.Data.SqlClient.SqlClientPermissionAttribute>를 지정하여 코드의 특정 메서드에 대해 CAS 권한을 요구할 수 있습니다. 제한된 보안 정책의 적용으로 이 권한이 허용되지 않는 경우 코드가 실행되기 전에 예외가 throw됩니다. 보안 정책에 대 한 자세한 내용은 [보안 정책 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100)) 및 [보안 정책 모범 사례](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100))를 참조 하세요.  
  
### <a name="example"></a>예제  
 다음 예제에서는 특정 연결 문자열을 필요로 하는 코드를 작성하는 방법을 보여 줍니다. 또한 이 예제에서는 시스템 관리자가 실제로 CAS 정책을 사용하여 구현하는 <xref:System.Data.SqlClient>에 대한 무제한 권한을 거부하는 것을 시뮬레이션합니다.  
  
> [!IMPORTANT]
> ADO.NET에 대한 CAS 권한을 디자인할 때 올바른 패턴은 가장 제한이 심한 경우(권한이 없는 경우)부터 시작하여 코드가 수행해야 하는 특정 작업에 필요한 특정 권한을 추가하는 것입니다. 반대 패턴인 모든 권한을 부여한 다음 특정 권한을 부여하지 않는 방식은 동일한 연결 문자열을 표현하는 방법이 많으므로 안전하지 않습니다. 예를 들어, 모든 권한을 부여한 다음 연결 문자열 "server=someserver"에 대해 사용할 수 있는 권한을 주지 않아도 "server=someserver.mycompany.com"은 여전히 허용됩니다. 항상 권한을 전혀 부여하지 않은 상태에서 시작하여 권한 집합에 허점이 생길 위험을 줄이는 것이 좋습니다.  
  
 다음 코드에서는 적절한 CAS 권한이 없는 경우 `SqlClient`가 <xref:System.Security.SecurityException>을 throw하는 보안 요구를 수행하는 방식을 보여 줍니다. <xref:System.Security.SecurityException> 출력은 콘솔 창에 표시됩니다.  
  
 [!code-csharp[DataWorks SqlClient.CAS#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.CAS#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/VB/source.vb#1)]  
  
 콘솔 창에 표시되는 출력은 다음과 같습니다.  
  
```  
Failed, as expected: <IPermission class="System.Data.SqlClient.  
SqlClientPermission, System.Data, Version=2.0.0.0,   
  Culture=neutral, PublicKeyToken=b77a5c561934e089" version="1"  
  AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Initial Catalog=  
  Northwind;Integrated Security=SSPI" KeyRestrictions=""  
KeyRestrictionBehavior="AllowOnly"/>  
</IPermission>  
  
Connection opened, as expected.  
Failed, as expected: Request failed.  
```  
  
## <a name="interoperability-with-unmanaged-code"></a>비관리 코드와의 상호 운용성  
 CLR 외부에서 실행되는 코드를 비관리 코드라고 합니다. 따라서 비관리 코드에는 CAS와 같은 보안 메커니즘을 적용할 수 없습니다. 비관리 코드로는 COM 구성 요소, ActiveX 인터페이스, Windows API 함수 등이 있습니다. 비관리 코드를 실행할 때에는 특수한 보안 고려 사항이 적용되므로 전체적인 애플리케이션 보안이 손상되지 않습니다. 자세한 내용은 [비관리 코드 상호 운용](../../interop/index.md)을 참조하세요.  
  
 .NET Framework는 COM interop를 통해 액세스를 제공함으로써 기존 COM 구성 요소에 대한 이전 버전과의 호환성도 지원합니다. 즉, 관련 COM 형식을 가져오는 COM interop 도구를 사용하여 COM 구성 요소를 .NET Framework 애플리케이션에 통합할 수 있습니다. COM 형식을 가져온 후에는 즉시 사용할 수 있습니다. COM interop을 사용하면 어셈블리 메타데이터를 형식 라이브러리로 내보내고 관리 구성 요소를 COM 구성 요소로 등록하여 COM 클라이언트에서 관리 코드에 액세스할 수도 있습니다. 자세한 내용은 [고급 COM 상호 운용성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bd9cdfyx)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](securing-ado-net-applications.md)
- [네이티브 및 .NET Framework 코드의 보안](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))
- [역할 기반 보안](../../../standard/security/role-based-security.md)
- [ADO.NET 개요](ado-net-overview.md)
