---
title: XmlSchemaCollection을 사용하여 XSD(XML 스키마) 유효성 검사
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: ad0b5717-3d32-41ad-a4d7-072c3e492b82
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0fb14f919d0737b9d9c25bcd62a3cfb7228ff432
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916085"
---
# <a name="xml-schema-xsd-validation-with-xmlschemacollection"></a>XmlSchemaCollection을 사용하여 XSD(XML 스키마) 유효성 검사
<xref:System.Xml.Schema.XmlSchemaCollection>을 사용하여 XSD(XML 스키마 정의 언어) 스키마에 대해 XML 문서의 유효성을 검사할 수 있습니다. <xref:System.Xml.Schema.XmlSchemaCollection>은 스키마를 컬렉션에 저장함으로써 유효성을 검사할 때마다 메모리에 로드되지 않으므로 성능이 향상됩니다. 스키마가 스키마 컬렉션에 있을 경우 `schemaLocation` 특성을 사용하여 컬렉션에서 스키마를 찾을 수 있습니다.  
  
> [!IMPORTANT]
> 이제 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스는 사용되지 않으며 <xref:System.Xml.Schema.XmlSchemaSet> 클래스로 대체되었습니다. <xref:System.Xml.Schema.XmlSchemaSet> 클래스에 대한 자세한 내용은 [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)을 참조하세요.  
  
 다음 예제에서는 데이터 파일의 루트 요소를 보여 줍니다.  
  
```xml  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns="urn:bookstore-schema"  
    elementFormDefault="qualified"  
    targetNamespace="urn:bookstore-schema">  
```  
  
 이 예제에서는 `targetNamespace` 특성 값이 `urn:bookstore-schema`입니다. 이 값은 스키마를 <xref:System.Xml.Schema.XmlSchemaCollection>에 추가할 때 사용되는 네임스페이스와 같습니다.  
  
 다음 코드 예제에서는 XML 스키마를 <xref:System.Xml.Schema.XmlSchemaCollection>에 추가합니다.  
  
```vb  
Dim xsc As New XmlSchemaCollection()  
' XML Schema.  
xsc.Add("urn:bookstore-schema", schema)   
reader = New XmlTextReader(filename)  
vreader = New XmlValidatingReader(reader)  
vreader.Schemas.Add(xsc)  
```  
  
```csharp  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
// XML Schema.  
xsc.Add("urn:bookstore-schema", schema);  
reader = new XmlTextReader (filename);  
vreader = new XmlValidatingReader (reader);  
vreader.Schemas.Add(xsc);  
```  
  
 `targetNamespace`에 대한 `namespaceURI` 메서드에 <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> 속성을 추가할 때 일반적으로 <xref:System.Xml.Schema.XmlSchemaCollection> 특성을 사용합니다. <xref:System.Xml.Schema.XmlSchemaCollection>에 스키마를 추가하기 전에 null 참조를 지정할 수 있습니다. 네임스페이스가 없는 스키마에는 빈 문자열("")을 사용해야 합니다. <xref:System.Xml.Schema.XmlSchemaCollection>에는 네임스페이스가 없는 스키마가 한 개만 있을 수 있습니다.  
  
 다음 코드 예제에서는 XML 스키마 HeadCount.xsd를 <xref:System.Xml.Schema.XmlSchemaCollection>에 추가하고 HeadCount.xml의 유효성을 검사합니다.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Schema  
  
Namespace ValidationSample  
  
   Class Sample  
  
      Public Shared Sub Main()  
         Dim tr As New XmlTextReader("HeadCount.xml")  
         Dim vr As New XmlValidatingReader(tr)  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd")  
         vr.ValidationType = ValidationType.Schema  
         AddHandler vr.ValidationEventHandler, AddressOf ValidationHandler  
  
         While vr.Read()  
         End While  
         Console.WriteLine("Validation finished")  
      End Sub  
      ' Main  
  
      Public Shared Sub ValidationHandler(sender As Object, args As ValidationEventArgs)  
         Console.WriteLine("***Validation error")  
         Console.WriteLine("Severity:{0}", args.Severity)  
         Console.WriteLine("Message:{0}", args.Message)  
      End Sub  
      ' ValidationHandler  
   End Class  
   ' Sample  
End Namespace  
' ValidationSample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Schema;  
  
namespace ValidationSample  
{  
   class Sample  
   {  
      public static void Main()  
      {  
         XmlTextReader tr = new XmlTextReader("HeadCount.xml");  
         XmlValidatingReader vr = new XmlValidatingReader(tr);  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd");  
         vr.ValidationType = ValidationType.Schema;  
         vr.ValidationEventHandler += new ValidationEventHandler (ValidationHandler);  
  
         while(vr.Read());  
         Console.WriteLine("Validation finished");  
      }  
  
      public static void ValidationHandler(object sender, ValidationEventArgs args)  
      {  
         Console.WriteLine("***Validation error");  
         Console.WriteLine("\tSeverity:{0}", args.Severity);  
         Console.WriteLine("\tMessage  :{0}", args.Message);  
      }  
   }  
}  
```  
  
 다음에서는 유효성을 검사할 입력 파일 HeadCount.xml의 내용을 요약합니다.  
  
```xml  
<!--Load HeadCount.xsd in SchemaCollection for Validation-->  
<hc:HeadCount xmlns:hc='xsdHeadCount'>  
   <Name>Waldo Pepper</Name>  
   <Name>Red Pepper</Name>  
</hc:HeadCount>  
```  
  
 다음에서는 유효성을 검사할 XML 스키마 파일 HeadCount.xsd의 내용을 요약합니다.  
  
```xml  
<xs:schema xmlns="xsdHeadCount" targetNamespace="xsdHeadCount" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
   <xs:element name='HeadCount' type="HEADCOUNT"/>  
   <xs:complexType name="HEADCOUNT">  
      <xs:sequence>  
         <xs:element name='Name' type='xs:string' maxOccurs='unbounded'/>  
      </xs:sequence>  
      <xs:attribute name='division' type='xs:int' use='optional' default='8'/>  
   </xs:complexType>  
</xs:schema>  
```  
  
 다음 코드 예제에서는 <xref:System.Xml.XmlValidatingReader>를 사용하는 <xref:System.Xml.XmlTextReader>를 만듭니다. XML 스키마 sample4.xsd에 대해 입력 파일 sample4.xml의 유효성을 검사합니다.  
  
```vb  
Dim tr As New XmlTextReader("sample4.xml")  
Dim vr As New XmlValidatingReader(tr)  
vr.ValidationType = ValidationType.Schema  
vr.Schemas.Add("datatypesTest", "sample4.xsd")  
AddHandler vr.ValidationEventHandler, AddressOf ValidationCallBack  
While vr.Read()  
   Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name)  
End While  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("sample4.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
vr.ValidationType = ValidationType.Schema;  
        vr.Schemas.Add("datatypesTest", "sample4.xsd");  
vr.ValidationEventHandler += new ValidationEventHandler(ValidationCallBack);  
while(vr.Read()) {  
    Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name);  
    }  
```  
  
 다음에서는 유효성을 검사할 입력 파일 sample4.xml의 내용을 요약합니다.  
  
```xml  
<datatypes xmlns="datatypesTest">  
    <number>  
        <number_1>123</number_1>  
    </number>  
</datatypes>  
```  
  
 다음에서는 유효성을 검사할 XML 스키마 파일 sample4.xsd의 내용을 요약합니다.  
  
```xml  
<xs:schema   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    xmlns:tns="datatypesTest"   
    targetNamespace="datatypesTest"  
    elementFormDefault="qualified">  
  
<xs:element name = "datatypes">  
  <xs:complexType>  
    <xs:all>  
        <xs:element name="number">  
            <xs:complexType>  
                <xs:sequence>  
                    <xs:element name="number_1" type="xs:decimal" maxOccurs="unbounded"/>  
                </xs:sequence>  
            </xs:complexType>  
        </xs:element>  
    </xs:all>  
  </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlParserContext>
- <xref:System.Xml.XmlValidatingReader.ValidationEventHandler?displayProperty=nameWithType>
- <xref:System.Xml.XmlValidatingReader.Schemas%2A?displayProperty=nameWithType>
- [XmlSchemaCollection 스키마 컴파일](../../../../docs/standard/data/xml/xmlschemacollection-schema-compilation.md)
