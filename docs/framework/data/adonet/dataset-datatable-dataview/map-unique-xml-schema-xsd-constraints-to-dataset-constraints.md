---
title: 데이터 세트 제약 조건에 고유 XSD(XML 스키마) 제약 조건 매핑
ms.date: 03/30/2017
ms.assetid: 56da90bf-21d3-4d1a-8bb8-de908866b78d
ms.openlocfilehash: 4aa94dfaf088a2a934c8901e2720f166d3a38dae
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784415"
---
# <a name="map-unique-xml-schema-xsd-constraints-to-dataset-constraints"></a>데이터 세트 제약 조건에 고유 XSD(XML 스키마) 제약 조건 매핑
XSD (XML 스키마 정의 언어) 스키마에서 **unique** 요소는 요소나 특성에 대 한 고유성 제약 조건을 지정 합니다. XML 스키마를 관계형 스키마로 변환하는 과정에서, XML 스키마의 요소나 특성에 지정된 UNIQUE 제약 조건은 생성된 해당 <xref:System.Data.DataTable>에 있는 <xref:System.Data.DataSet>의 UNIQUE 제약 조건에 매핑됩니다.  
  
 다음 표에서는 **unique** 요소에 지정할 수 있는 **msdata** 특성을 간략하게 설명 합니다.  
  
|특성 이름|Description|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|이 특성을 지정하면 해당 값이 제약 조건 이름으로 사용됩니다. 그렇지 않으면 **name** 특성은 제약 조건 이름의 값을 제공 합니다.|  
|**msdata:PrimaryKey**|가 `PrimaryKey="true"` **unique** 요소에 있는 경우 **IsPrimaryKey** 속성을 **true**로 설정 하 여 unique 제약 조건이 생성 됩니다.|  
  
 다음 예에서는 **unique** 요소를 사용 하 여 고유성 제약 조건을 지정 하는 XML 스키마를 보여 줍니다.  
  
```xml  
<xs:schema id="SampleDataSet"   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:integer"   
           minOccurs="0"/>  
        <xs:element name="CompanyName" type="xs:string"   
           minOccurs="0"/>  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
  
 <xs:element name="SampleDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:unique     msdata:ConstraintName="UCustID"     name="UniqueCustIDConstr" >       <xs:selector xpath=".//Customers" />       <xs:field xpath="CustomerID" />     </xs:unique>  
</xs:element>  
</xs:schema>  
```  
  
 스키마의 **unique** 요소는 문서 인스턴스의 모든 **Customers** 요소에 대해 **CustomerID** 자식 요소의 값이 고유 하도록 지정 합니다. **데이터 집합**을 빌드할 때 매핑 프로세스는이 스키마를 읽고 다음 테이블을 생성 합니다.  
  
```  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 매핑 프로세스에서는 다음 **데이터 집합**에 표시 된 것 처럼 **CustomerID** 열에 unique 제약 조건도 생성 됩니다. 여기에서는 편의를 위해 관련 속성만 보여 줍니다.  
  
```  
      DataSetName: MyDataSet  
TableName: Customers  
  ColumnName: CustomerID  
      AllowDBNull: True  
      Unique: True  
  ConstraintName: UcustID       Type: UniqueConstraint  
      Table: Customers  
      Columns: CustomerID   
      IsPrimaryKey: False  
```  
  
 생성 된 **데이터 집합** 에서 **IsPrimaryKey** 속성은 unique 제약 조건에 대해 **False** 로 설정 됩니다. 열의 **unique** 속성은 **CustomerID** 열 값이 고유 해야 함을 나타내며 열의 **allowdbnull** 속성에 지정 된 대로 null 참조일 수 있습니다.  
  
 스키마를 수정 하 고 선택적 **msdata: PrimaryKey** 특성 값을 **True**로 설정 하면 테이블에 unique 제약 조건이 생성 됩니다. **Allowdbnull** 열 속성은 **False**로 설정 되 고 제약 조건의 **IsPrimaryKey** 속성은 **True**로 설정 되므로 **CustomerID** 열을 기본 키 열로 만듭니다.  
  
 XML 스키마의 요소나 특성의 조합에 UNIQUE 제약 조건을 지정할 수 있습니다. 다음 예에서는 스키마에 다른 **xs: field** 요소를 추가 하 여 **CustomerID** 와 **CompanyName** 값의 조합이 모든 인스턴스의 모든 **고객** 에 대해 고유 해야 함을 지정 하는 방법을 보여 줍니다.  
  
```xml  
      <xs:unique     
         msdata:ConstraintName="SomeName"    
         name="UniqueCustIDConstr" >   
  <xs:selector xpath=".//Customers" />   
  <xs:field xpath="CustomerID" />   
  <xs:field xpath="CompanyName" />   
</xs:unique>  
```  
  
 이는 결과 **데이터 집합**에 만들어지는 제약 조건입니다.  
  
```  
ConstraintName: SomeName  
  Table: Customers  
  Columns: CustomerID CompanyName   
  IsPrimaryKey: False  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [XSD(XML 스키마)에서 데이터 세트 관계 생성](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET 개요](../ado-net-overview.md)
