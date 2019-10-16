---
title: XSD(XML 스키마)에서 데이터 세트 관계 생성
ms.date: 03/30/2017
ms.assetid: 1c9a1413-c0d2-4447-88ba-9a2b0cbc0aa8
ms.openlocfilehash: d00f07ee3338941b7de1bb890f71cd3c2d120246
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784649"
---
# <a name="generating-dataset-relations-from-xml-schema-xsd"></a>XSD(XML 스키마)에서 데이터 세트 관계 생성
<xref:System.Data.DataSet>에서는 부모-자식 관계를 만들어 둘 이상의 열을 연결시킵니다. XSD (XML 스키마 정의 언어) 스키마 내에서는 세 가지 방법으로 **데이터 집합** 관계를 나타낼 수 있습니다.  
  
- 중첩된 복합 형식을 지정합니다.  
  
- **Msdata: Relationship** 주석을 사용 합니다.  
  
- **Msdata: ConstraintOnly** 주석을 사용 하지 않고 **xs: keyref** 를 지정 합니다.  
  
## <a name="nested-complex-types"></a>중첩된 복합 형식  
 스키마에서 중첩된 복합 형식의 정의는 요소의 부모-자식 관계를 나타냅니다. 다음 XML 스키마 조각에서는 **Orderdetail** 이 **Order** 요소의 자식 요소 임을 보여 줍니다.  
  
```xml  
<xs:element name="Order">  
  <xs:complexType>  
     <xs:sequence>          
       <xs:element name="OrderDetail" />  
           <xs:complexType>               
           </xs:complexType>  
     </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 XML 스키마 매핑 프로세스에서는 스키마의 중첩 된 복합 형식에 해당 하는 **데이터 집합** 에 테이블을 만듭니다. 또한 생성 된 테이블에 대 한 부모 **-** 자식 열로 사용 되는 추가 열을 만듭니다. 이러한 부모 **-** 자식 열은 관계를 지정 하며이는 기본 키/외래 키 제약 조건을 지정 하는 것과는 다릅니다.  
  
## <a name="msdatarelationship-annotation"></a>msdata:Relationship 주석  
 **Msdata: Relationship** 주석을 사용 하면 중첩 되지 않은 스키마의 요소 간에 부모-자식 관계를 명시적으로 지정할 수 있습니다. 다음 예에서는 **Relationship** 요소의 구조를 보여 줍니다.  
  
```xml  
<msdata:Relationship name="CustOrderRelationship"    
msdata:parent=""    
msdata:child=""    
msdata:parentkey=""    
msdata:childkey="" />  
```  
  
 **Msdata: relationship** 주석의 특성은 부모-자식 관계와 관련 된 요소 뿐만 아니라 **parentkey** 및 **childkey** 요소와 관계에 포함 된 특성을 식별 합니다. 매핑 프로세스에서는이 정보를 사용 하 여 **데이터 집합** 에 테이블을 생성 하 고 이러한 테이블 간에 기본 키/외래 키 관계를 만듭니다.  
  
 예를 들어 다음 스키마 조각은 동일한 수준 (중첩 되지 않음)에서 **Order** 및 **orderdetail** 요소를 지정 합니다. 이 스키마는 이러한 두 요소 간의 부모-자식 관계를 지정 하는 **msdata: Relationship** 주석을 지정 합니다. 이 경우 **msdata: relationship** 주석을 사용 하 여 명시적 관계를 지정 해야 합니다.  
  
```xml  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
        <xs:element name="OrderDetail">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
       <xs:element name="Order">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
    </xs:choice>  
  </xs:complexType>  
</xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrdDetailRelation"  
          msdata:parent="Order"  
          msdata:child="OrderDetail"   
          msdata:parentkey="OrderNumber"  
          msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
```  
  
 매핑 프로세스에서는 **Relationship** 요소를 사용 하 여 **Order** 테이블의 **Ordernumber** 열과 **데이터 집합**에 있는 **ordernumber** 테이블의 **ordernumber** 열 간에 부모-자식 관계를 만듭니다. 매핑 프로세스에서는 관계만 지정합니다. 즉, 관계형 데이터베이스의 기본 키/외래 키 제약 조건처럼 이러한 열의 값에 대해 제약 조건을 자동으로 지정하지는 않습니다.  
  
### <a name="in-this-section"></a>섹션 내용  
 [중첩된 스키마 요소 사이에 암시적 관계 매핑](map-implicit-relations-between-nested-schema-elements.md)  
 XML 스키마에서 중첩 된 요소가 발견 될 때 **데이터 집합** 에서 암시적으로 만들어지는 제약 조건 및 관계에 대해 설명 합니다.  
  
 [중첩된 요소에 지정된 관계 매핑](map-relations-specified-for-nested-elements.md)  
 XML 스키마의 중첩 된 요소에 대 한 **데이터 집합** 에서 관계를 명시적으로 설정 하는 방법을 설명 합니다.  
  
 [중첩 없이 요소 사이에 관계 지정](specify-relations-between-elements-with-no-nesting.md)  
 중첩 되지 않은 XML 스키마 요소 간에 **데이터 집합** 에서 관계를 만드는 방법에 대해 설명 합니다.  
  
### <a name="related-sections"></a>관련 단원  
 [XML 스키마에서 데이터 세트 관계형 구조 파생(XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XSD (XML 스키마 정의 언어) 스키마에서 생성 되는 **데이터 집합** 의 관계형 구조 또는 스키마에 대해 설명 합니다.  
  
 [데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **데이터 집합**에서 unique 및 foreign key 제약 조건을 만드는 데 사용 되는 XML 스키마 요소에 대해 설명 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
