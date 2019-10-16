---
title: SQL Server의 인스턴스 열거(ADO.NET)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.openlocfilehash: c464762e82a24aab399a23ecb26420b5dce61f55
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782380"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>SQL Server의 인스턴스 열거(ADO.NET)
SQL Server를 사용 하면 응용 프로그램이 현재 네트워크 내에서 SQL Server 인스턴스를 찾을 수 있습니다. <xref:System.Data.Sql.SqlDataSourceEnumerator> 클래스에서는 애플리케이션 개발자에게 이 정보를 노출시켜 표시되는 모든 서버에 대한 정보가 포함된 <xref:System.Data.DataTable>을 제공합니다. 이 반환 된 테이블에는 사용자가 새 연결을 만들려고 할 때 제공 된 목록과 일치 하는 네트워크에서 사용할 수 있는 서버 인스턴스 목록이 포함 되어 있으며, 연결 속성에서 사용 가능한 모든 서버를 포함 하는 드롭다운 목록이 확장 됩니다.대화 상자. 표시되는 결과가 항상 완전하지는 않습니다.  
  
> [!NOTE]
> 대부분의 Windows 서비스와 마찬가지로, SQL Browser 서비스도 최소 권한으로 실행하는 것이 좋습니다. SQL 브라우저 서비스와 이 서비스의 동작을 관리하는 방법에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
## <a name="retrieving-an-enumerator-instance"></a>열거자 인스턴스 검색  
 사용 가능한 SQL Server 인스턴스에 대한 정보가 포함된 테이블을 검색하려면 먼저 공유/정적 <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> 속성을 사용하여 열거자를 검색해야 합니다.  
  
```vb  
Dim instance As System.Data.Sql.SqlDataSourceEnumerator = _  
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
 정적 인스턴스를 검색했으면 <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A> 메서드를 호출할 수 있습니다. 이 메서드는 사용 가능한 서버의 정보가 포함된 <xref:System.Data.DataTable>을 반환합니다.  
  
```vb  
Dim dataTable As System.Data.DataTable = instance.GetDataSources()  
```  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
 메서드 호출을 통해 반환된 테이블에는 다음 열이 포함되며, 모든 열에는 `string` 값이 들어 있습니다.  
  
|Column|설명|  
|------------|-----------------|  
|**ServerName**|서버의 이름입니다.|  
|**InstanceName**|서버 인스턴스의 이름입니다. 서버가 기본 인스턴스로 실행 중인 경우에는 비어 있습니다.|  
|**IsClustered**|서버가 클러스터의 일부인지 여부를 나타냅니다.|  
|**Version**|서버의 버전입니다. 예를 들어:<br /><br /> -9.00 (SQL Server 2005)<br />-10.0. xx (SQL Server 2008)<br />-10.50 (SQL Server 2008 R2)<br />-   11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>열거 제한  
 사용 가능한 모든 서버가 나열되거나 나열되지 않을 수 있습니다. 이 목록은 시간 제한 및 네트워크 트래픽 등의 요인에 따라 달라질 수 있습니다. 따라서 두 개를 연속해서 호출해도 목록이 서로 다를 수 있습니다. 동일한 네트워크의 서버만 나열됩니다. 브로드캐스트 패킷은 일반적으로 라우터를 순회하지 않기 때문에 나열된 서버를 표시하지 않을 수는 있지만 여러 호출에서 안정적입니다.  
  
 나열된 서버는 `IsClustered` 및 버전 등의 추가 정보를 제공하거나 제공하지 않을 수 있습니다. 제공 여부는 목록을 가져온 방법에 따라 달라집니다. SLQ Server 브라우저 서비스를 통해 나열된 서버에서는 Windows 인프라에서 찾은 정보(이름)보다 더 자세한 정보를 제공합니다.  
  
> [!NOTE]
> 서버 열거는 완전 신뢰로 실행되는 경우에만 사용할 수 있습니다. 부분적으로 신뢰할 수 있는 환경에서 실행되는 어셈블리는 <xref:System.Data.SqlClient.SqlClientPermission> CAS(코드 액세스 보안) 권한을 가지고 있더라도 서버 열거를 사용할 수 없습니다.  
  
 SQL Server은 <xref:System.Data.Sql.SqlDataSourceEnumerator> SQL Browser 라는 외부 Windows 서비스를 사용 하 여에 대 한 정보를 제공 합니다. 이 서비스는 기본적으로 사용할 수 있지만 관리자는 이 서비스의 설정을 해제하거나 비활성화하여 이 클래스에 서버 인스턴스를 노출시키지 않을 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 콘솔 애플리케이션에서는 표시되는 모든 SQL Server 인스턴스에 대한 정보를 검색하여 콘솔 창에 표시합니다.  
  
```vb  
Imports System.Data.Sql  
  
Module Module1  
  Sub Main()  
    ' Retrieve the enumerator instance and then the data.  
    Dim instance As SqlDataSourceEnumerator = _  
     SqlDataSourceEnumerator.Instance  
    Dim table As System.Data.DataTable = instance.GetDataSources()  
  
    ' Display the contents of the table.  
    DisplayData(table)  
  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Sub  
  
  Private Sub DisplayData(ByVal table As DataTable)  
    For Each row As DataRow In table.Rows  
      For Each col As DataColumn In table.Columns  
        Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
      Next  
      Console.WriteLine("============================")  
    Next  
  End Sub  
End Module  
```  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [SQL Server 및 ADO.NET](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
