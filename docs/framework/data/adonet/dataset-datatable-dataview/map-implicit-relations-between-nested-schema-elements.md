---
title: 중첩된 스키마 요소 사이에 암시적 관계 매핑
ms.date: 03/30/2017
ms.assetid: 6b25002a-352e-4d9b-bae3-15129458a355
ms.openlocfilehash: f4b1b9e45f0cda976719b991c336463e0af05f12
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784440"
---
# <a name="map-implicit-relations-between-nested-schema-elements"></a>중첩된 스키마 요소 사이에 암시적 관계 매핑
XSD(XML 스키마 정의 언어) 스키마에는 다른 형식 내부에 중첩된 복합 형식이 포함될 수 있습니다. 이 경우 매핑 프로세스에서는 기본 매핑을 적용하며 <xref:System.Data.DataSet>에 다음 항목을 만듭니다.  
  
- 각 복합 형식(부모 및 자식)에 대해 하나의 테이블을 만듭니다.  
  
- 부모에 unique 제약 조건이 없는 경우 *tablename*_id 라는 테이블 정의 당 추가 기본 키 열이 하나 있습니다. 여기서 *tablename* 은 부모 테이블의 이름입니다.  
  
- **IsPrimaryKey** 속성을 **True**로 설정 하 여 추가 열을 기본 키로 식별 하는 부모 테이블의 primary key 제약 조건입니다. 제약 조건은 Constraint\#으로 명명되며, 여기서 \#은 1, 2, 3 등을 나타냅니다. 예를 들어, 첫 번째 제약 조건의 기본 이름은 Constraint1입니다.  
  
- 추가 열을 부모 테이블의 기본 키를 참조하는 외래 키로 식별하는 외래 키 제약 조건을 자식 테이블에 만듭니다. 제약 조건의 이름은 *ParentTable_ChildTable* 여기서 *parenttable* 은 부모 테이블의 이름이 고 *childtable* 은 자식 테이블의 이름입니다.  
  
- 부모와 자식 테이블 간의 데이터 관계를 만듭니다.  
  
 다음 예제에서는 **Orderdetail** 이 **Order**의 자식 요소인 스키마를 보여 줍니다.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
   <xs:complexType>  
     <xs:choice maxOccurs="unbounded">  
       <xs:element name="Order">  
         <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:string" />  
            <xs:element name="EmpNumber" type="xs:string" />  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:string" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
         </xs:complexType>  
       </xs:element>  
     </xs:choice>  
   </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 XML 스키마 매핑 프로세스는 **데이터 집합**에 다음을 만듭니다.  
  
- **Order** 및 **orderdetail** 테이블  
  
    ```  
    Order(OrderNumber, EmpNumber, Order_Id)  
    OrderDetail(OrderNo, ItemNo, Order_Id)  
    ```  
  
- **Order** 테이블에 대 한 unique 제약 조건입니다. **IsPrimaryKey** 속성은 **True**로 설정 됩니다.  
  
    ```  
    ConstraintName: Constraint1  
    Type: UniqueConstraint  
    Table: Order  
    Columns: Order_Id   
    IsPrimaryKey: True  
    ```  
  
- **Orderdetail** 테이블의 foreign key 제약 조건입니다.  
  
    ```  
    ConstraintName: Order_OrderDetail  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: Order_Id   
    RelatedTable: Order  
    RelatedColumns: Order_Id   
    ```  
  
- **Order** 및 **orderdetail** 테이블 간의 관계입니다. **Order** 및 **orderdetail** 요소가 스키마에 중첩 되어 있으므로이 관계의 **Nested** 속성은 **True** 로 설정 됩니다.  
  
    ```  
    ParentTable: Order  
    ParentColumns: Order_Id   
    ChildTable: OrderDetail  
    ChildColumns: Order_Id   
    ParentKeyConstraint: Constraint1  
    ChildKeyConstraint: Order_OrderDetail  
    RelationName: Order_OrderDetail  
    Nested: True  
    ```  
  
## <a name="see-also"></a>참고자료

- [XSD(XML 스키마)에서 데이터 세트 관계 생성](generating-dataset-relations-from-xml-schema-xsd.md)
- [데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [ADO.NET 개요](../ado-net-overview.md)
