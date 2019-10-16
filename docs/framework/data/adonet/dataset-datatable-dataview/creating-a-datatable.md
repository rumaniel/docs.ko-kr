---
title: DataTable 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: eecf9d78-60e3-4fdc-8de0-e56c13a89414
ms.openlocfilehash: e48359041f92e7b534513aa461a293a822bede19
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786491"
---
# <a name="creating-a-datatable"></a>DataTable 만들기
<xref:System.Data.DataTable>은 메모리 내 관계형 데이터가 포함된 하나의 테이블을 나타내며, 독립적으로 만들어 사용하거나 다른 .NET Framework 개체에 의해 사용될 수도 있습니다. 이 경우에는 주로 <xref:System.Data.DataSet>의 멤버로 사용됩니다.  
  
 적절 한 **datatable** 생성자를 사용 하 여 **datatable** 개체를 만들 수 있습니다. **Add** 메서드를 사용 하 여 **데이터 집합** 에 추가 하 여 **DataTable** 개체의 **Tables** 컬렉션에 추가할 수 있습니다.  
  
 또한 **DataAdapter** 개체의 **Fill** 또는 **FillSchema** 메서드를 사용 하거나 **ReadXml**, readxmlschema를 사용 하 여 미리 정의 되거나 유추 된 XML 스키마에서 **데이터 집합** 내에 **DataTable** 개체를 만들 수 있습니다.또는 **데이터 집합**의 **InferXmlSchema** 메서드 하나의 **데이터 집합**에 있는 **tables** 컬렉션의 멤버로 DataTable을 추가한 후에는 다른 **데이터 집합**의 테이블 컬렉션에 **DataTable** 을 추가할 수 없습니다.  
  
 **DataTable**을 처음 만들 때 스키마 (구조)가 없습니다. 테이블의 스키마를 정의 하려면 테이블의 **Columns** 컬렉션에 개체를 <xref:System.Data.DataColumn> 만들고 추가 해야 합니다. 테이블에 대 한 기본 키 열을 정의 하 고 **제약 조건** 개체를 만들어 테이블의 **제약 조건** 컬렉션에 추가할 수도 있습니다. **DataTable**의 스키마를 정의한 후에는 테이블의 **Rows** 컬렉션에 **DataRow** 개체를 추가 하 여 테이블에 데이터 행을 추가할 수 있습니다.  
  
 <xref:System.Data.DataTable.TableName%2A> **DataTable**을 만들 때 속성에 대 한 값을 제공할 필요는 없습니다. 속성을 다른 시간에 지정 하거나 비워 둘 수 있습니다. 그러나 **TableName** 값이 없는 테이블을 **데이터 집합**에 추가 하면 테이블에 Table0에 대 한 "table"로 시작 하는 증분 기본 이름인 table*N*이 지정 됩니다.  
  
> [!NOTE]
> 사용자가 제공 하는 이름이 **데이터 집합**의 기존 기본 테이블 이름과 충돌할 수 있으므로 **TableName** 값을 제공 하는 경우 "테이블*N*" 명명 규칙을 사용 하지 않는 것이 좋습니다. 이미 있는 이름을 입력하면 예외가 throw됩니다.  
  
 다음 예에서는 **DataTable** 개체의 인스턴스를 만들고 이름을 "Customers"로 지정 합니다.  
  
```vb  
Dim workTable as DataTable = New DataTable("Customers")  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
```  
  
 다음 예에서는 **DataSet**의 **Tables** 컬렉션에 **DataTable** 인스턴스를 추가 하 여 해당 인스턴스를 만듭니다.  
  
```vb  
Dim customers As DataSet = New DataSet  
Dim customersTable As DataTable = _  
   customers.Tables.Add("CustomersTable")  
```  
  
```csharp  
DataSet customers = new DataSet();  
DataTable customersTable = customers.Tables.Add("CustomersTable");  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataTable>
- <xref:System.Data.DataTableCollection>
- [DataTable](datatables.md)
- [DataAdapter에서 데이터 집합 채우기](../populating-a-dataset-from-a-dataadapter.md)
- [XML에서 데이터 세트 로드](loading-a-dataset-from-xml.md)
- [XML에서 데이터 세트 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)
- [ADO.NET 개요](../ado-net-overview.md)
