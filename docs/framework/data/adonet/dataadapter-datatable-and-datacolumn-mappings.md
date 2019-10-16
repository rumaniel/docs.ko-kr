---
title: DataAdapter DataTable 및 DataColumn 매핑
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.openlocfilehash: 357812aa95ea731fe86fbe49b2cb1b2806e3915a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784870"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>DataAdapter DataTable 및 DataColumn 매핑
**DataAdapter** 의 TableMappings 속성에는 0 개 이상의 <xref:System.Data.Common.DataTableMapping> 개체 컬렉션이 포함 되어 있습니다. **DataTableMapping** 는 데이터 원본에 대 한 쿼리에서 반환 되는 데이터와에 <xref:System.Data.DataTable>대 한 마스터 매핑을 제공 합니다. **DataTableMapping** 이름은 **DataTable** 이름 대신 **DataAdapter**의 **Fill** 메서드에 전달할 수 있습니다. 다음 예에서는 **Authors** 테이블에 대해 **AuthorsMapping** 라는 **DataTableMapping** 를 만듭니다.  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 **DataTableMapping** 를 사용 하면 데이터베이스와 다른 **DataTable** 에서 열 이름을 사용할 수 있습니다. **DataAdapter** 는 테이블이 업데이트 될 때 매핑을 사용 하 여 열을 일치 시킵니다.  
  
 **Dataadapter**의 **Fill** 또는 **Update** 메서드를 호출할 때 **TableName** 또는 **DataTableMapping** 이름을 지정 하지 않으면 **dataadapter** 는 "Table" 이라는 **DataTableMapping** 을 찾습니다. 해당 **DataTableMapping** 없는 경우 **DataTable** 의 **TableName** 은 "Table"입니다. 이름이 "Table" 인 **DataTableMapping** 를 만들어 기본 **DataTableMapping** 을 지정할 수 있습니다.  
  
 다음 코드 예제에서는 <xref:System.Data.Common> 네임 스페이스에서 **DataTableMapping** 을 만들고 이름을 "Table"로 지정 하 여 지정 된 **DataAdapter** 의 기본 매핑으로 설정 합니다. 그런 다음이 예에서는 쿼리 결과의 첫 번째 테이블 ( **northwind** 데이터베이스의 **Customers** 테이블)의 열을의 **Northwind** <xref:System.Data.DataSet>Customers 테이블에 있는 더 많은 사용자에 게 친숙 한 이름 집합으로 매핑합니다. 매핑되지 않는 열의 경우 데이터 소스의 열 이름이 사용됩니다.  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
```  
  
```csharp  
DataTableMapping mapping =   
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 고급 상황에서는 동일한 **DataAdapter** 를 사용 하 여 다른 매핑을 사용 하는 서로 다른 테이블의 로드를 지원 하도록 결정할 수 있습니다. 이렇게 하려면 추가 **DataTableMapping** 개체를 추가 하기만 하면 됩니다.  
  
 **Fill** 메서드에 **데이터 집합** 의 인스턴스와 **DataTableMapping** 이름이 전달 되 면 해당 이름을 가진 매핑이 있는 경우 사용 됩니다. 그렇지 않으면 해당 이름을 가진 **DataTable** 이 사용 됩니다.  
  
 다음 예에서는 **Customers** 의 이름과 **DataTable** 이름이 **BizTalkSchema**인 **DataTableMapping** 을 만듭니다. 그런 다음이 예에서는 SELECT 문에 의해 반환 된 행을 **BizTalkSchema** **DataTable**에 매핑합니다.  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
ITableMapping mapping =   
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
> 열 매핑에 소스 열 이름을 제공하지 않거나 테이블 매핑에 소스 테이블 이름을 제공하지 않으면 기본 이름이 자동으로 생성됩니다. 열 매핑에 대해 원본 열이 제공 되지 않은 경우 열 매핑에는 **SourceColumn1**로 시작 하는 **SourceColumn** *N* 의 증분 기본 이름이 지정 됩니다. 테이블 매핑에 대해 제공 된 원본 테이블 이름이 없으면 테이블 매핑에 **SourceTable1**로 시작 하는 **SourceTable** *N*의 증분 기본 이름이 지정 됩니다.  
  
> [!NOTE]
> **SourceColumn** *n* 의 명명 규칙을 사용 하지 않는 것이 좋습니다. 즉, 제공 하 는 이름이의 기존 기본 열 매핑 이름과 **충돌할 수 있으므로 열 매핑에 대해 SourceTable n을 사용 하지 않는 것이 좋습니다. ColumnMappingCollection** 또는 **있는**의 테이블 매핑 이름입니다. 이미 있는 이름을 제공하면 예외가 throw됩니다.  
  
## <a name="handling-multiple-result-sets"></a>여러 개의 결과 집합 처리  
 **SelectCommand** 에서 여러 테이블을 반환 하는 경우 **채우기** 는 지정 된 테이블 이름부터 시작 하 여 **TableName** 형식으로 계속 하 여 **데이터 집합**의 테이블에 대 한 증분 값을 포함 하는 테이블 이름을 자동으로 생성 합니다. *N*( **TableName1**부터 시작) 테이블 매핑을 사용 하 여 자동으로 생성 된 테이블 이름을 **데이터 집합**의 테이블에 대해 지정 하려는 이름에 매핑할 수 있습니다. 예를 들어 **고객** 및 **주문의**두 테이블을 반환 하는 **SelectCommand** 의 경우 **Fill**에 대 한 다음 호출을 실행 합니다.  
  
```  
adapter.Fill(customersDataSet, "Customers")  
```  
  
 **데이터 집합**에는 두 개의 테이블이 생성 됩니다. **고객** 및 **Customers1**. 테이블 매핑을 사용 하 여 두 번째 테이블이 **Customers1**대신 **Orders** 라는 이름으로 지정 되도록 할 수 있습니다. 이렇게 하려면 다음 예제와 같이 **Customers1** 의 원본 테이블을 **데이터 집합** 테이블 **주문**에 매핑합니다.  
  
```  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [ADO.NET 개요](ado-net-overview.md)
