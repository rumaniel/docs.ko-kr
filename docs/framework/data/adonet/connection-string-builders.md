---
title: 연결 문자열 작성기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
ms.openlocfilehash: afafe5d1eaddaef3b9f0069908b365e40ea4ed29
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785688"
---
# <a name="connection-string-builders"></a>연결 문자열 작성기
이전 버전의 ADO.NET에서는 연결 된 문자열 값이 있는 연결 문자열의 컴파일 타임 검사가 수행 되지 않으므로 런타임에 잘못 된 키워드에서을 (를) 생성 <xref:System.ArgumentException>했습니다. 각 .NET Framework 데이터 공급자는 연결 문자열 키워드에 대해 서로 다른 구문을 지원 합니다 .이 키워드는 수동으로 수행 하는 경우 유효한 연결 문자열을 구성 하기가 어렵습니다. 이 문제를 해결 하기 위해 ADO.NET 2.0에는 각 .NET Framework 데이터 공급자에 대 한 새로운 연결 문자열 작성기가 도입 되었습니다. 각 데이터 공급자에는 <xref:System.Data.Common.DbConnectionStringBuilder>에서 상속되는 강력한 형식의 연결 문자열 작성기 클래스가 있습니다. 다음 표에서는 .NET Framework 데이터 공급자와 연결 된 연결 문자열 작성기 클래스를 보여 줍니다.  
  
|공급자|ConnectionStringBuilder 클래스|  
|--------------|-----------------------------------|  
|<xref:System.Data.SqlClient>|<xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType>|  
|<xref:System.Data.OleDb>|<xref:System.Data.OleDb.OleDbConnectionStringBuilder?displayProperty=nameWithType>|  
|<xref:System.Data.Odbc>|<xref:System.Data.Odbc.OdbcConnectionStringBuilder?displayProperty=nameWithType>|  
|<xref:System.Data.OracleClient>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=nameWithType>|  
  
## <a name="connection-string-injection-attacks"></a>연결 문자열 삽입 공격  
 연결 문자열 삽입 공격은 사용자 입력에 대해 동적 문자열 연결을 사용하여 연결 문자열을 작성할 때 발생할 수 있습니다. 문자열의 유효성이 확인되지 않고 악의적인 텍스트 또는 문자를 이스케이프할 수 없는 경우 공격자가 서버에서 중요한 데이터 또는 기타 리소스에 액세스할 가능성이 있습니다. 예를 들어 공격자가 세미콜론을 입력한 다음 값을 추가하여 공격을 시작할 수 있습니다. 연결 문자열은 "최신 항목 사용" 알고리즘을 사용하여 구문 분석되므로 악의적인 입력이 올바른 값을 대체할 수 있습니다.  
  
 연결 문자열 작성기 클래스는 모호한 작업을 제거하고 구문 오류 및 보안 취약점으로부터 보호하도록 디자인되었습니다. 즉, 각 데이터 공급자에서 허용하는 알려진 키/값 쌍에 해당하는 메서드와 속성을 제공합니다. 각 클래스는 고정된 동의어 컬렉션을 유지하며 동의어를 그에 해당하는 잘 알려진 키 이름으로 변환할 수 있습니다. 또한, 유효한 키/값 쌍에 대한 검사를 수행하며 유효하지 않은 쌍이 있는 경우 예외를 throw합니다. 뿐만 아니라 삽입된 값을 안전한 방식으로 처리합니다.  
  
 다음 예제에서는 <xref:System.Data.SqlClient.SqlConnectionStringBuilder>에서 `Initial Catalog` 설정에 삽입된 추가 값을 처리하는 방법을 보여 줍니다.  
  
```vb  
Dim builder As New System.Data.SqlClient.SqlConnectionStringBuilder  
builder("Data Source") = "(local)"  
builder("Integrated Security") = True  
builder("Initial Catalog") = "AdventureWorks;NewValue=Bad"  
Console.WriteLine(builder.ConnectionString)  
```  
  
```csharp  
System.Data.SqlClient.SqlConnectionStringBuilder builder =  
  new System.Data.SqlClient.SqlConnectionStringBuilder();  
builder["Data Source"] = "(local)";  
builder["integrated Security"] = true;  
builder["Initial Catalog"] = "AdventureWorks;NewValue=Bad";  
Console.WriteLine(builder.ConnectionString);  
```  
  
 출력을 통해 <xref:System.Data.SqlClient.SqlConnectionStringBuilder>에서 추가 값을 연결 문자열에 새로운 키/값 쌍으로 추가하는 대신 큰따옴표로 묶어 올바르게 이스케이프 처리했음을 알 수 있습니다.  
  
```  
data source=(local);Integrated Security=True;  
initial catalog="AdventureWorks;NewValue=Bad"  
```  
  
## <a name="building-connection-strings-from-configuration-files"></a>구성 파일에서 연결 문자열 작성  
 연결 문자열의 특정 요소가 이미 알려져 있는 경우 해당 요소를 구성 파일에 저장하고 런타임에 검색하여 완전한 연결 문자열을 구성할 수 있습니다. 예를 들어 데이터베이스 이름은 미리 알고 있는 경우가 많지만 서버 이름은 그렇지 않습니다. 또는 연결 문자열에 다른 값을 삽입할 수 없도록 런타임에 사용자가 이름과 암호를 입력하도록 할 수도 있습니다.  
  
 연결 문자열 작성기의 오버로드된 생성자 중 하나는 <xref:System.String>을 인수로 사용하므로 작성기를 사용하면 부분 연결 문자열을 제공하여 이러한 사용자 입력을 통해 연결 문자열을 완성하는 것이 가능합니다. 이 부분 연결 문자열을 구성 파일에 저장한 후 런타임에 검색할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Configuration> 네임스페이스를 사용하면 <xref:System.Web.Configuration.WebConfigurationManager>(웹 애플리케이션의 경우) 및 <xref:System.Configuration.ConfigurationManager>(Windows 애플리케이션의 경우)를 통해 구성 파일에 프로그래밍 방식으로 액세스할 수 있습니다. 연결 문자열 및 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 [연결 문자열 및 구성 파일](connection-strings-and-configuration-files.md)을 참조 하세요.  
  
### <a name="example"></a>예제  
 이 예제에서는 구성 파일에서 부분 연결 문자열을 검색한 후 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>의 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A>, <xref:System.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> 및 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 속성을 설정하여 완성하는 방법을 보여 줍니다. 구성 파일은 다음과 같이 정의됩니다.  
  
```xml  
<connectionStrings>  
  <clear/>  
  <add name="partialConnectString"   
    connectionString="Initial Catalog=Northwind;"  
    providerName="System.Data.SqlClient" />  
</connectionStrings>  
```  
  
> [!NOTE]
> 코드를 실행하려면 프로젝트에서 `System.Configuration.dll`에 대한 참조를 설정해야 합니다.  
  
 [!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/CS/source.cs#1)]
 [!code-vb[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [연결 문자열](connection-strings.md)
- [개인 정보 및 데이터 보안](privacy-and-data-security.md)
- [ADO.NET 개요](ado-net-overview.md)
