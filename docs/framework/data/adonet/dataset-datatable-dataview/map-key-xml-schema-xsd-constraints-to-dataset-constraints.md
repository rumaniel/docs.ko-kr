---
title: 데이터 세트 제약 조건에 키 XSD(XML 스키마) 제약 조건 매핑
ms.date: 03/30/2017
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
ms.openlocfilehash: 8543f5b34ee2a80ff0154897cf7678b244a8d357
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786098"
---
# <a name="map-key-xml-schema-xsd-constraints-to-dataset-constraints"></a>데이터 세트 제약 조건에 키 XSD(XML 스키마) 제약 조건 매핑
스키마에서 **key** 요소를 사용 하 여 요소 또는 특성에 대 한 키 제약 조건을 지정할 수 있습니다. KEY 제약 조건이 지정된 요소 또는 특성은 모든 스키마 인스턴스에서 고유한 값을 가져야 하며 null 값을 가져서는 안 됩니다.  
  
 KEY 제약 조건이 정의된 열이 null 값을 가질 수 없다는 것을 제외하면, key 제약 조건은 UNIQUE 제약 조건과 유사합니다.  
  
 다음 표에서는 **key** 요소에 지정할 수 있는 **msdata** 특성을 간략하게 설명 합니다.  
  
|특성 이름|Description|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|이 특성을 지정하면 해당 값이 제약 조건 이름으로 사용됩니다. 그렇지 않으면 **name** 특성은 제약 조건 이름의 값을 제공 합니다.|  
|**msdata:PrimaryKey**|이 있으면 IsPrimaryKey 제약 조건 속성이 **true**로 설정 되어 기본 키로 설정 됩니다. `PrimaryKey="true"` 기본 키에는 null 값을 사용할 수 없으므로 **Allowdbnull** 열 속성은 **false**로 설정 됩니다.|  
  
 키 제약 조건이 지정 된 스키마를 변환 하는 동안 매핑 프로세스에서는 제약 조건의 각 열에 대해 **Allowdbnull** column 속성이 **false** 로 설정 된 unique 제약 조건을 테이블에 만듭니다. **Key** 요소에을 지정 `msdata:PrimaryKey="true"` 하지 않은 경우 unique 제약 조건의 **IsPrimaryKey** 속성도 **false** 로 설정 됩니다. 이것은 `PrimaryKey="true"`인 스키마의 UNIQUE 제약 조건에도 마찬가지로 적용됩니다.  
  
 다음 스키마 예제에서 **key** 요소는 **CustomerID** 요소에 대 한 키 제약 조건을 지정 합니다.  
  
```xml  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>   
```  
  
 **Key** 요소는 **Customers** 요소의 **CustomerID** 자식 요소 값에 고유한 값이 있어야 하 고 null 값을 가질 수 없도록 지정 합니다. XSD(XML 스키마 정의 언어) 스키마를 변환할 때 매핑 프로세스에서는 다음 테이블을 만듭니다.  
  
```  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 XML 스키마 매핑은 다음과 <xref:System.Data.DataSet>같이 **CustomerID** 열에도 **UniqueConstraint** 를 만듭니다. 여기에서는 편의를 위해 관련 속성만 보여 줍니다.  
  
```  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID   
      IsPrimaryKey: True  
```  
  
 생성 된 **데이터 집합** 에서 스키마가 **키** 요소에를 `msdata:PrimaryKey="true"` 지정 하기 때문에 **UniqueConstraint** 의 **IsPrimaryKey** 속성은 **true** 로 설정 됩니다.  
  
 **데이터 집합** 에 있는 **UniqueConstraint** 의 **ConstraintName** 속성 값은 스키마의 **키** 요소에 지정 된 **msdata: ConstraintName** 특성의 값입니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [XSD(XML 스키마)에서 데이터 세트 관계 생성](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET 개요](../ado-net-overview.md)
