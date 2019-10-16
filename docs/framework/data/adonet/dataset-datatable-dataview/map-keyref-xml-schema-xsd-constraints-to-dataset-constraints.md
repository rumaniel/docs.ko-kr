---
title: 데이터 세트 제약 조건에 keyref XSD(XML 스키마) 제약 조건 매핑
ms.date: 03/30/2017
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
ms.openlocfilehash: b5ffe69886b08903feab4373b1cd5c5244b3b3b9
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784520"
---
# <a name="map-keyref-xml-schema-xsd-constraints-to-dataset-constraints"></a>데이터 세트 제약 조건에 keyref XSD(XML 스키마) 제약 조건 매핑
**Keyref** 요소를 사용 하면 문서 내의 요소 간에 링크를 설정할 수 있습니다. 이 링크는 관계형 데이터베이스의 외래 키 관계와 유사합니다. 스키마에서 **keyref** 요소를 지정 하는 경우 요소는 스키마 매핑 프로세스 중에의 <xref:System.Data.DataSet>테이블에 있는 열에 대 한 해당 foreign key 제약 조건으로 변환 됩니다. 기본적으로 **keyref** 요소는 관계에 지정 된 **parenttable**, **Childtable**, **parenttable**및 **childtable** 속성을 사용 하 여 관계를 생성 합니다.  
  
 다음 표에서는 **keyref** 요소에 지정할 수 있는 **msdata** 특성을 간략하게 설명 합니다.  
  
|특성 이름|설명|  
|--------------------|-----------------|  
|**msdata:ConstraintOnly**|스키마의 **keyref** 요소에 **ConstraintOnly = "true"** 를 지정 하면 제약 조건이 만들어지지만 관계는 생성 되지 않습니다. 이 특성을 지정 하지 않거나 **False**로 설정 하면 **데이터 집합**에 제약 조건과 관계가 모두 생성 됩니다.|  
|**msdata:ConstraintName**|**ConstraintName** 특성을 지정 하면 해당 값이 제약 조건의 이름으로 사용 됩니다. 그렇지 않으면 스키마에서 **keyref** 요소의 **Name** 특성은 **데이터 집합**에 제약 조건 이름을 제공 합니다.|  
|**msdata:UpdateRule**|**UpdateRule** 특성이 스키마의 **keyref** 요소에 지정 된 경우 해당 값은 **데이터 집합**의 **UpdateRule** 제약 조건 속성에 할당 됩니다. 그렇지 않으면 **UpdateRule** 속성이 **Cascade**로 설정 됩니다.|  
|**msdata:DeleteRule**|**DeleteRule** 특성이 스키마의 **keyref** 요소에 지정 된 경우 해당 값은 **데이터 집합**의 **DeleteRule** 제약 조건 속성에 할당 됩니다. 그렇지 않으면 **DeleteRule** 속성이 **Cascade**로 설정 됩니다.|  
|**msdata:AcceptRejectRule**|**AcceptRejectRule** 특성이 스키마의 **keyref** 요소에 지정 된 경우 해당 값은 **데이터 집합**의 **AcceptRejectRule** 제약 조건 속성에 할당 됩니다. 그렇지 않으면 **AcceptRejectRule** 속성을 **None**으로 설정 합니다.|  
  
 다음 예제에는 **Order** 요소의 **ordernumber** 자식 요소와 **ordernumber** 의 **ordernumber** 자식 요소 간에 **key** 및 **keyref** 관계를 지정 하는 스키마가 포함 되어 있습니다. 요소인.  
  
 예제에서 **Ordernumber** 요소의 **ordernumber** 자식 요소는 **Order** 요소의 **ordernumber** 키 자식 요소를 참조 합니다.  
  
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
  
 XSD (XML 스키마 정의 언어) 스키마 매핑 프로세스에서는 두 개의 테이블이 포함 된 다음 **데이터 집합** 을 생성 합니다.  
  
```  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 또한 **데이터 집합** 은 다음과 같은 제약 조건을 정의 합니다.  
  
- **Order** 테이블에 대 한 unique 제약 조건입니다.  
  
    ```  
              Table: Order  
    Columns: OrderNumber   
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
- **Order** 및 **orderdetail** 테이블 간의 관계입니다. 두 요소가 스키마에 중첩 되지 않으므로 **중첩** 된 속성은 **False** 로 설정 됩니다.  
  
    ```  
              ParentTable: Order  
    ParentColumns: OrderNumber   
    ChildTable: OrderDetail  
    ChildColumns: OrderNo   
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
- **Orderdetail** 테이블의 foreign key 제약 조건입니다.  
  
    ```  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo   
    RelatedTable: Order  
    RelatedColumns: OrderNumber   
    ```  
  
## <a name="see-also"></a>참고자료

- [데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [XSD(XML 스키마)에서 데이터 세트 관계 생성](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET 개요](../ado-net-overview.md)
