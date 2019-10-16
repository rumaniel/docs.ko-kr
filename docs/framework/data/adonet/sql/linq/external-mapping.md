---
title: 외부 매핑
ms.date: 03/30/2017
ms.assetid: 076606b8-d889-4ba0-b5da-ae577b146f23
ms.openlocfilehash: ba5af75ae34b233354fec6e9074f3cc96d924c7f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003050"
---
# <a name="external-mapping"></a>외부 매핑
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 별도의 XML 파일을 사용 하 여 데이터베이스의 데이터 모델과 개체 모델 간의 매핑을 지정 하는 프로세스에 대 한 *외부 매핑을*지원 합니다. 외부 매핑 파일을 사용하면 다음과 같은 장점이 있습니다.  
  
- 매핑 코드를 애플리케이션 코드와 따로 유지할 수 있어 애플리케이션 코드를 간단하게 표시할 수 있습니다.  
  
- 외부 매핑 파일을 구성 파일처럼 사용할 수 있습니다. 예를 들어 외부 매핑 파일을 바꾸는 방법으로 이진 파일을 배포한 후 애플리케이션의 동작을 업데이트할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 매핑 파일은 XML 파일이어야 하며 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 스키마 정의 파일(.xsd)에 대해 유효성이 검사되어야 합니다.  
  
 다음 규칙이 적용됩니다.  
  
- 매핑 파일은 XML 파일이어야 합니다.  
  
- XML 매핑 파일은 XML 스키마 정의 파일에 대해 유효해야 합니다. 자세한 내용은 [방법: DBML 및 외부 매핑 파일의 유효성을 검사 합니다 @ no__t-0.  
  
- 외부 매핑은 특성 기반 매핑을 재정의합니다. 즉, 외부 매핑 소스를 사용하여 <xref:System.Data.Linq.DataContext>를 만들면 <xref:System.Data.Linq.DataContext>에서는 사용자가 클래스에 만든 모든 매핑 특성을 무시합니다. 이 동작은 외부 매핑 파일에 클래스가 포함되었는지 여부에 관계없이 항상 적용됩니다.  
  
- [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 특성 기반 매핑과 외부 매핑의 혼합 사용을 지원하지 않습니다.  
  
## <a name="xml-schema-definition-file"></a>XML 스키마 정의 파일  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 외부 매핑은 다음 XML 스키마 정의에 대해 유효해야 합니다.  
  
 이 스키마 정의 파일은 DBML 파일의 유효성을 검사하는 데 사용하는 스키마 정의 파일과 다릅니다. 자세한 내용은 [LINQ to SQL의 코드 생성](code-generation-in-linq-to-sql.md))을 참조 하세요.  
  
> [!NOTE]
> 또한 Visual Studio 사용자는 XML 스키마 대화 상자에서이 XSD 파일을 "Linqtosqlmapping.xsd"으로 찾을 수 있습니다. 외부 매핑 파일의 유효성을 검사 하는 데이 파일을 제대로 사용 하려면 [How to: DBML 및 외부 매핑 파일의 유효성을 검사 합니다 @ no__t-0.  
  
```xml  
<?xml version="1.0" encoding="utf-16"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="http://schemas.microsoft.com/linqtosql/mapping/2007" xmlns="http://schemas.microsoft.com/linqtosql/mapping/2007"  
elementFormDefault="qualified" >  
  <xs:element name="Database" type="Database" />  
  <xs:complexType name="Database">  
    <xs:sequence>  
      <xs:element name="Table" type="Table" minOccurs="0" maxOccurs="unbounded" />  
      <xs:element name="Function" type="Function" minOccurs="0" maxOccurs="unbounded" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Provider" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Table">  
    <xs:sequence>  
      <xs:element name="Type" type="Type" minOccurs="1" maxOccurs="1" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Type">  
    <xs:sequence>  
      <xs:choice minOccurs="0" maxOccurs="unbounded">  
        <xs:element name="Column" type="Column" minOccurs="0" maxOccurs="unbounded" />  
        <xs:element name="Association" type="Association" minOccurs="0" maxOccurs="unbounded" />  
      </xs:choice>  
      <xs:element name="Type" type="Type" minOccurs="0" maxOccurs="unbounded" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="required" />  
    <xs:attribute name="InheritanceCode" type="xs:string" use="optional" />  
    <xs:attribute name="IsInheritanceDefault" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Column">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="required" />  
    <xs:attribute name="Storage" type="xs:string" use="optional" />  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
    <xs:attribute name="IsPrimaryKey" type="xs:boolean" use="optional" />  
    <xs:attribute name="IsDbGenerated" type="xs:boolean" use="optional" />  
    <xs:attribute name="CanBeNull" type="xs:boolean" use="optional" />  
    <xs:attribute name="UpdateCheck" type="UpdateCheck" use="optional" />  
    <xs:attribute name="IsDiscriminator" type="xs:boolean" use="optional" />  
    <xs:attribute name="Expression" type="xs:string" use="optional" />  
    <xs:attribute name="IsVersion" type="xs:boolean" use="optional" />  
    <xs:attribute name="AutoSync" type="AutoSync" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Association">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="required" />  
    <xs:attribute name="Storage" type="xs:string" use="optional" />  
    <xs:attribute name="ThisKey" type="xs:string" use="optional" />  
    <xs:attribute name="OtherKey" type="xs:string" use="optional" />  
    <xs:attribute name="IsForeignKey" type="xs:boolean" use="optional" />  
    <xs:attribute name="IsUnique" type="xs:boolean" use="optional" />  
    <xs:attribute name="DeleteRule" type="xs:string" use="optional" />  
    <xs:attribute name="DeleteOnNull" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Function">  
    <xs:sequence>  
      <xs:element name="Parameter" type="Parameter" minOccurs="0" maxOccurs="unbounded" />  
      <xs:choice>  
        <xs:element name="ElementType" type="Type" minOccurs="0" maxOccurs="unbounded" />  
        <xs:element name="Return" type="Return" minOccurs="0" maxOccurs="1" />  
      </xs:choice>  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Method" type="xs:string" use="required" />  
    <xs:attribute name="IsComposable" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Parameter">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Parameter" type="xs:string" use="required" />  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
    <xs:attribute name="Direction" type="ParameterDirection" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Return">  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:simpleType name="UpdateCheck">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Always" />  
      <xs:enumeration value="Never" />  
      <xs:enumeration value="WhenChanged" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="ParameterDirection">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="In" />  
      <xs:enumeration value="Out" />  
      <xs:enumeration value="InOut" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="AutoSync">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Never" />  
      <xs:enumeration value="OnInsert" />  
      <xs:enumeration value="OnUpdate" />  
      <xs:enumeration value="Always" />  
      <xs:enumeration value="Default" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
```  
  
## <a name="see-also"></a>참조

- [LINQ to SQL에서 코드 생성](code-generation-in-linq-to-sql.md)
- [참조](reference.md)
- [방법: 개체 모델을 외부 파일로 생성 @ no__t-0
