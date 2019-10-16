---
title: DataTable 제약 조건
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 27c9f2fd-f64d-4b4e-bbf6-1d24f47067cb
ms.openlocfilehash: 3f3055b11f0e682ae5a9578289e30dc2716343fe
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785394"
---
# <a name="datatable-constraints"></a>DataTable 제약 조건
제약 조건을 사용하여 <xref:System.Data.DataTable>의 데이터를 제한함으로써 데이터 무결성을 유지할 수 있습니다. 제약 조건은 자동 규칙이기 때문에 행 값이 조금이라도 변경되면 열 또는 관련 열에 적용되어 작업 과정을 결정합니다. 의 속성이true`System.Data.DataSet.EnforceConstraints` 이면 제약 조건이 적용 됩니다. <xref:System.Data.DataSet> `EnforceConstraints` 속성을 설정하는 방법을 보여 주는 코드 예제는 <xref:System.Data.DataSet.EnforceConstraints%2A> 참조 항목을 참조하세요.  
  
 ADO.NET에는 <xref:System.Data.ForeignKeyConstraint> 및 <xref:System.Data.UniqueConstraint>의 두 가지 제약 조건이 있습니다. 기본적으로 두 제약 조건은 둘 이상의 테이블 간에 관계를 만들 때 <xref:System.Data.DataRelation> **데이터 집합**에를 추가 하 여 자동으로 만들어집니다. 그러나 관계를 만들 때 **createConstraints** = **false** 를 지정 하 여이 동작을 사용 하지 않도록 설정할 수 있습니다.  
  
## <a name="foreignkeyconstraint"></a>ForeignKeyConstraint  
 **ForeignKeyConstraint** 는 관련 테이블에 대 한 업데이트 및 삭제를 전파 하는 방법에 대 한 규칙을 적용 합니다. 예를 들어 한 테이블의 행에 있는 값이 업데이트 되거나 삭제 되 고 동일한 값이 하나 이상의 관련 테이블에도 사용 되는 경우 **ForeignKeyConstraint** 는 관련 테이블에서 발생 하는 작업을 결정 합니다.  
  
 ForeignKeyConstraint <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> 의 <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> 및 속성은 사용자가 관련 테이블의 행을 삭제 하거나 업데이트 하려고 할 때 수행할 동작을 정의 합니다. 다음 표에서는 **ForeignKeyConstraint**의 **DeleteRule** 및 **UpdateRule** 속성에 사용할 수 있는 다양 한 설정을 설명 합니다.  
  
|규칙 설정|설명|  
|------------------|-----------------|  
|**Cascade**|관련 행을 삭제하거나 업데이트합니다.|  
|**SetNull**|관련 행의 값을 **DBNull**로 설정 합니다.|  
|**SetDefault**|관련 행의 값을 기본값으로 설정합니다.|  
|**없음**|관련 행에 대해 아무 동작도 수행하지 않습니다. 기본값입니다.|  
  
 **ForeignKeyConstraint** 는 관련 열에 대 한 변경 내용을 전파 하 고 전파를 제한할 수 있습니다. 열의 **ForeignKeyConstraint** 설정 된 속성에 따라, **DataSet** 의 **EnforceConstraints** 속성이 **true**이면 부모 행에 대해 특정 작업을 수행 하면 예외가 발생 합니다. 예를 들어 **ForeignKeyConstraint** 의 **DeleteRule** 속성이 **None**이면 부모 행에 자식 행이 있는 경우 해당 행을 삭제할 수 없습니다.  
  
 **ForeignKeyConstraint** 생성자를 사용 하 여 단일 열 또는 열 배열 사이에서 foreign key 제약 조건을 만들 수 있습니다. 결과 **ForeignKeyConstraint** 개체를 테이블의 **제약 조건** 속성 ( **ConstraintCollection**)의 **Add** 메서드에 전달 합니다. **ConstraintCollection** 의 **Add** 메서드의 여러 오버 로드에 생성자 인수를 전달 하 여 **ForeignKeyConstraint**를 만들 수도 있습니다.  
  
 **ForeignKeyConstraint**를 만들 때 **DeleteRule** 및 **UpdateRule** 값을 생성자에 인수로 전달 하거나 다음 예제와 같이 속성으로 설정할 수 있습니다. 여기서 **DeleteRule** 값은로 **설정 됩니다. 없음**).  
  
```vb  
Dim custOrderFK As ForeignKeyConstraint = New ForeignKeyConstraint("CustOrderFK", _  
  custDS.Tables("CustTable").Columns("CustomerID"), _  
  custDS.Tables("OrdersTable").Columns("CustomerID"))  
custOrderFK.DeleteRule = Rule.None    
' Cannot delete a customer value that has associated existing orders.  
custDS.Tables("OrdersTable").Constraints.Add(custOrderFK)  
```  
  
```csharp  
ForeignKeyConstraint custOrderFK = new ForeignKeyConstraint("CustOrderFK",  
  custDS.Tables["CustTable"].Columns["CustomerID"],   
  custDS.Tables["OrdersTable"].Columns["CustomerID"]);  
custOrderFK.DeleteRule = Rule.None;    
// Cannot delete a customer value that has associated existing orders.  
custDS.Tables["OrdersTable"].Constraints.Add(custOrderFK);  
```  
  
### <a name="acceptrejectrule"></a>AcceptRejectRule  
 행에 대 한 변경 내용은 **AcceptChanges** 메서드를 사용 하 여 수락 하거나 **DataSet**, **DataTable**또는 **DataRow**의 **RejectChanges** 메서드를 사용 하 여 취소할 수 있습니다. **데이터 집합** 에 **ForeignKeyConstraints**포함 된 경우 **AcceptChanges** 또는 **RejectChanges** 메서드를 호출 하면 **AcceptRejectRule**가 적용 됩니다. **ForeignKeyConstraint** 의 **AcceptRejectRule** 속성은 부모 행에서 **AcceptChanges** 또는 **RejectChanges** 가 호출 될 때 자식 행에 대해 수행할 동작을 결정 합니다.  
  
 다음 표에서는 **AcceptRejectRule**에 사용할 수 있는 설정을 보여 줍니다.  
  
|규칙 설정|Description|  
|------------------|-----------------|  
|**Cascade**|자식 행의 변경을 승인하거나 거부합니다.|  
|**없음**|자식 행에 대해 아무 동작도 수행하지 않습니다. 기본값입니다.|  
  
### <a name="example"></a>예제  
 다음 예제에서는<xref:System.Data.ForeignKeyConstraint>를 만들고 <xref:System.Data.ForeignKeyConstraint.AcceptRejectRule%2A>을 비롯한 해당 속성을 몇 가지 설정한 다음 <xref:System.Data.ConstraintCollection> 개체의 <xref:System.Data.DataTable>에 추가합니다.  
  
 [!code-csharp[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/CS/source.cs#1)]
 [!code-vb[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/VB/source.vb#1)]  
  
## <a name="uniqueconstraint"></a>UniqueConstraint  
 **UniqueConstraint** 개체는 **DataTable**의 단일 열 또는 열 배열에 할당할 수 있습니다 .이 개체는 지정 된 열에 있는 모든 데이터가 행 마다 고유 하 게 유지 되도록 합니다. **UniqueConstraint** 생성자를 사용 하 여 열 또는 열 배열에 대 한 unique 제약 조건을 만들 수 있습니다. 결과 **UniqueConstraint** 개체를 테이블의 **제약 조건** 속성 ( **ConstraintCollection**)의 **Add** 메서드에 전달 합니다. **ConstraintCollection** 의 **Add** 메서드의 여러 오버 로드에 생성자 인수를 전달 하 여 **UniqueConstraint**를 만들 수도 있습니다. 열 하나 이상의 열에 대 한 **UniqueConstraint** 를 만들 때 필요에 따라 열이 기본 키인지 여부를 지정할 수 있습니다.  
  
 열의 **unique** 속성을 **true**로 설정 하 여 열에 대 한 unique 제약 조건을 만들 수도 있습니다. 또는 단일 열의 **unique** 속성을 **false** 로 설정 하면 존재할 수 있는 unique 제약 조건이 모두 제거 됩니다. 하나 이상의 열을 테이블의 기본 키로 정의하면 지정한 열에 대한 UNIQUE 제약 조건이 자동으로 만들어집니다. **DataTable**의 **PrimaryKey** 속성에서 열을 제거 하면 **UniqueConstraint** 이 제거 됩니다.  
  
 다음 예에서는 **DataTable**의 두 열에 대해 **UniqueConstraint** 를 만듭니다.  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custUnique As UniqueConstraint = _  
    New UniqueConstraint(New DataColumn()   {custTable.Columns("CustomerID"), _  
    custTable.Columns("CompanyName")})  
custDS.Tables("Customers").Constraints.Add(custUnique)  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
UniqueConstraint custUnique = new UniqueConstraint(new DataColumn[]   
    {custTable.Columns["CustomerID"],   
    custTable.Columns["CompanyName"]});  
custDS.Tables["Customers"].Constraints.Add(custUnique);  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataRelation>
- <xref:System.Data.DataTable>
- <xref:System.Data.ForeignKeyConstraint>
- <xref:System.Data.UniqueConstraint>
- [DataTable 스키마 정의](datatable-schema-definition.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
