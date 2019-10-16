---
title: 데이터 세트 스키마 정보를 XSD로 작성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4e530831-695e-49ff-8f0b-e5b0c526b8eb
ms.openlocfilehash: f86e9100489ddf35d8ef5f98e386306a7dbfd4ed
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784172"
---
# <a name="writing-dataset-schema-information-as-xsd"></a>데이터 세트 스키마 정보를 XSD로 작성
<xref:System.Data.DataSet>의 스키마를 XSD(XML 스키마 정의 언어) 스키마로 작성하여, 작성한 스키마를 관련된 데이터와 함께 또는 데이터 없이 XML 문서에서 전송할 수 있습니다. XML 스키마는 파일, 스트림 <xref:System.Xml.XmlWriter>또는 문자열에 쓸 수 있습니다. 강력한 형식의 **데이터 집합**을 생성 하는 데 유용 합니다. 강력한 형식의 **데이터 집합** 개체에 대 한 자세한 내용은 [형식화 된 데이터](typed-datasets.md)집합을 참조 하세요.  
  
 <xref:System.Data.DataColumn> 개체의 **ColumnMapping** 속성을 사용 하 여 XML 스키마에서 테이블의 열을 표현 하는 방법을 지정할 수 있습니다. 자세한 내용은 [데이터 집합 콘텐츠를 Xml 데이터로 작성](writing-dataset-contents-as-xml-data.md)의 "xml 요소, 특성 및 텍스트에 열 매핑"을 참조 하세요.  
  
 **데이터 집합** 의 스키마를 XML 스키마로 작성 하려면 파일, 스트림 또는 **XmlWriter**에 **데이터 집합**의 **WriteXmlSchema** 메서드를 사용 합니다. **WriteXmlSchema** 는 결과 XML 스키마의 대상을 지정 하는 매개 변수 하나를 사용 합니다. 다음 코드 예제에서는 파일 이름 및 <xref:System.IO.StreamWriter> 개체를 포함 하는 문자열을 전달 하 여 **데이터 집합** 의 XML 스키마를 파일에 쓰는 방법을 보여 줍니다.  
  
```vb  
dataSet.WriteXmlSchema("Customers.xsd")  
```  
  
```csharp  
dataSet.WriteXmlSchema("Customers.xsd");  
```  
  
```vb  
Dim writer As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xsd")  
dataSet.WriteXmlSchema(writer)  
writer.Close()  
```  
  
```csharp  
System.IO.StreamWriter writer = new System.IO.StreamWriter("Customers.xsd");  
dataSet.WriteXmlSchema(writer);  
writer.Close();  
```  
  
 **데이터 집합** 의 스키마를 가져와서 XML 스키마 문자열로 작성 하려면 다음 예제와 같이 **getxmlschema** 메서드를 사용 합니다.  
  
```vb  
Dim schemaString As String = dataSet.GetXmlSchema()  
```  
  
```csharp  
string schemaString = dataSet.GetXmlSchema();  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)
- [데이터 세트 콘텐츠를 XML 데이터로 작성](writing-dataset-contents-as-xml-data.md)
- [형식화된 데이터 집합](typed-datasets.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
