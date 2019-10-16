---
title: XML 스키마 제약 조건 및 관계
ms.date: 03/30/2017
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
ms.openlocfilehash: 76af1c2e9d85d18a68b8c0a947dfba3b3291326c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784193"
---
# <a name="xml-schema-constraints-and-relationships"></a>XML 스키마 제약 조건 및 관계
XSD (XML 스키마 정의 언어) 스키마에서는 **msdata: Relationship** 주석을 사용 하 여 제약 조건 (unique, key 및 keyref 제약 조건) 및 관계를 지정할 수 있습니다. 이 항목에서는 XML 스키마에 지정된 제약 조건과 관계를 해석하여 <xref:System.Data.DataSet>을 생성하는 방법을 설명합니다.  
  
 일반적으로 XML 스키마에서 **데이터 집합**의 관계만 생성 하려면 **msdata: Relationship** 주석을 지정 합니다. 자세한 내용은 [XSD (XML 스키마)에서 데이터 집합 관계 생성](generating-dataset-relations-from-xml-schema-xsd.md)을 참조 하세요. **데이터 집합**에서 제약 조건을 생성 하려면 제약 조건 (unique, key 및 keyref)을 지정 합니다. 이 항목의 뒷부분에서 설명하겠지만 KEY 및 KEYREF 제약 조건도 관계를 생성하는 데 사용됩니다.  
  
## <a name="generating-a-relationship-from-key-and-keyref-constraints"></a>KEY 및 KEYREF 제약 조건에서 관계 생성  
 **Msdata: Relationship** 주석을 지정 하는 대신 XML 스키마 매핑 프로세스에서 제약 조건 뿐만 아니라 **데이터 집합**의 관계를 생성 하는 데 사용 되는 key 및 keyref 제약 조건을 지정할 수 있습니다. 그러나 keyref 요소에를 `msdata:ConstraintOnly="true"` 지정 하면 **데이터 집합** 에 제약 조건만 포함 되며 관계는 포함 되지 않습니다.  
  
 다음 예제에서는 중첩 되지 않은 **Order** 및 **orderdetail** 요소를 포함 하는 XML 스키마를 보여 줍니다. 스키마에서는 KEY 및 KEYREF 제약 조건도 지정합니다.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 XML 스키마 매핑 프로세스 중에 생성 되는 **데이터 집합** 에는 **Order** 및 **orderdetail** 테이블이 포함 됩니다. 또한 **데이터 집합** 에는 관계와 제약 조건이 포함 됩니다. 다음 예제에서는 이러한 관계와 제약 조건을 보여 줍니다. 스키마는 **msdata: Relationship** 주석을 지정 하지 않습니다. 대신 key 및 keyref 제약 조건을 사용 하 여 관계를 생성 합니다.  
  
```  
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 이전 스키마 예제에서 **Order** 및 **orderdetail** 요소는 중첩 되지 않습니다. 다음 스키마 예제에서는 이들 요소가 중첩됩니다. 그러나 **msdata: Relationship** 주석이 지정 되지 않습니다. 따라서 암시적 관계가 가정 됩니다. 자세한 내용은 [중첩 된 스키마 요소 간의 암시적 관계 매핑](map-implicit-relations-between-nested-schema-elements.md)을 참조 하세요. 스키마에서는 KEY 및 KEYREF 제약 조건도 지정합니다.  
  
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
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 XML 스키마 매핑 프로세스에서 생성 되는 **데이터 집합** 에는 두 개의 테이블이 포함 됩니다.  
  
```  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 **데이터 집합** 에는 두 개의 관계 ( **msdata: relationship** 주석과 key 및 keyref 제약 조건을 기반으로 하는 다른 관계)와 다양 한 제약 조건이 포함 됩니다. 다음 예제에서는 이러한 관계와 제약 조건을 보여 줍니다.  
  
```  
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 중첩 테이블을 참조 하는 keyref 제약 조건에 **msdata: isnested = "true"** 주석이 포함 된 경우 **데이터 집합** 은 keyref 제약 조건 및 관련 unique/key 제약 조건을 기반으로 하는 단일 중첩 관계를 만듭니다.  
  
## <a name="see-also"></a>참고자료

- [XML 스키마에서 데이터 세트 관계형 구조 파생(XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [ADO.NET 개요](../ado-net-overview.md)
