---
title: DataTable에 열 추가
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e85c4a0e-4f3f-458c-b58b-0ddbc06bf974
ms.openlocfilehash: 6e0dcd819dc354e1fd23b244692dff5091142004
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784848"
---
# <a name="adding-columns-to-a-datatable"></a>DataTable에 열 추가
에 <xref:System.Data.DataTable> 는 테이블의 **Columns** 속성에서 참조 하는 개체의 <xref:System.Data.DataColumn> 컬렉션이 포함 되어 있습니다. 이 열 컬렉션과 모든 제약 조건을 함께 사용하여 테이블의 스키마나 구조를 정의합니다.  
  
 **Datacolumn** 생성자를 사용 하거나 테이블 <xref:System.Data.DataColumnCollection>의 **Columns** 속성 ()의 **Add** 메서드를 호출 하 여 테이블 내에서 **datacolumn** 개체를 만들 수 있습니다. **Add** 메서드는 선택적 **ColumnName**, **DataType**및 **Expression** 인수를 받아들이고 컬렉션의 멤버로 새 **DataColumn** 을 만듭니다. 또한 기존 **datacolumn** 개체를 수락 하 여 컬렉션에 추가 하 고 요청 시 추가 된 **datacolumn** 에 대 한 참조를 반환 합니다. **DataTable** 개체는 데이터 원본에 한정 되지 않으므로 **DataColumn**의 데이터 형식을 지정할 때 .NET Framework 형식이 사용 됩니다.  
  
 다음 예에서는 **DataTable**에 4 개의 열을 추가 합니다.  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
  
Dim workCol As DataColumn = workTable.Columns.Add( _  
    "CustID", Type.GetType("System.Int32"))  
workCol.AllowDBNull = false  
workCol.Unique = true  
  
workTable.Columns.Add("CustLName", Type.GetType("System.String"))  
workTable.Columns.Add("CustFName", Type.GetType("System.String"))  
workTable.Columns.Add("Purchases", Type.GetType("System.Double"))  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
  
DataColumn workCol = workTable.Columns.Add("CustID", typeof(Int32));  
workCol.AllowDBNull = false;  
workCol.Unique = true;  
  
workTable.Columns.Add("CustLName", typeof(String));  
workTable.Columns.Add("CustFName", typeof(String));  
workTable.Columns.Add("Purchases", typeof(Double));  
```  
  
 이 예에서는 **CustID** 열에 대 한 속성이 **DBNull** 값을 허용 하지 않도록 설정 되 고 값을 고유 하 게 제한 하는 것을 확인 합니다. 그러나 **CustID** 열을 테이블의 기본 키 열로 정의 하면 **allowdbnull** 속성은 자동으로 **False** 로 설정 되 고 **Unique** 속성은 자동으로 **true**로 설정 됩니다. 자세한 내용은 [기본 키 정의](defining-primary-keys.md)합니다.  
  
> [!CAUTION]
> 열에 대해 열 이름을 지정 하지 않으면 열에 "Column1"으로 시작 하는 열*N* 의 증분 기본 이름이 지정 됩니다 .이 이름은 **DataColumnCollection**에 추가 됩니다. 열 이름을 제공 하는 경우 "열*N*"의 명명 규칙을 사용 하지 않는 것이 좋습니다 .이 경우 사용자가 제공 하는 이름이 **DataColumnCollection**의 기존 기본 열 이름과 충돌할 수 있습니다. 이미 있는 이름을 입력하면 예외가 throw됩니다.  
  
 <xref:System.Xml.Linq.XElement>를 <xref:System.Data.DataColumn.DataType%2A>에서 <xref:System.Data.DataColumn>의 <xref:System.Data.DataTable>로 사용하는 경우 데이터를 읽을 때 XML serialization이 작동하지 않습니다. 예를 들어 <xref:System.Xml.XmlDocument> 메서드를 사용하여 `DataTable.WriteXml`를 작성하는 경우 XML에 대한 serialization 수행 시 <xref:System.Xml.Linq.XElement>에 추가 부모 노드가 있습니다. 이 문제를 해결하려면 <xref:System.Data.SqlTypes.SqlXml> 대신 <xref:System.Xml.Linq.XElement> 형식을 사용합니다. `ReadXml` 및 `WriteXml`이 <xref:System.Data.SqlTypes.SqlXml>와 올바르게 작동합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataColumn>
- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataTable>
- [DataTable 스키마 정의](datatable-schema-definition.md)
- [DataTable](datatables.md)
- [ADO.NET 개요](../ado-net-overview.md)
