---
title: 스키마 컴파일을 위한 XmlSchemaSet
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 55c4b175-3170-4071-9d60-dd5a42f79b54
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c24fe637514ba773cecc7824de276b1707a4e90c
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582556"
---
# <a name="xmlschemaset-for-schema-compilation"></a>스키마 컴파일을 위한 XmlSchemaSet
XSD(XML 스키마 정의 언어) 스키마를 저장하고 유효성을 검사할 수 있는 캐시인 <xref:System.Xml.Schema.XmlSchemaSet>에 대해 설명합니다.  
  
## <a name="the-xmlschemaset-class"></a>XmlSchemaSet 클래스  
 <xref:System.Xml.Schema.XmlSchemaSet>은 XSD(XML 스키마 정의 언어) 스키마를 저장하고 유효성을 검사할 수 있는 캐시입니다.  
  
 <xref:System.Xml?displayProperty=nameWithType> 버전 1.0에서는 스키마 라이브러리로서 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스에 XML 스키마가 로드되었습니다. <xref:System.Xml?displayProperty=nameWithType> 버전 2.0에서는 <xref:System.Xml.XmlValidatingReader> 및 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스는 사용되지 않으며 각각 <xref:System.Xml.XmlReader.Create%2A> 메서드와 <xref:System.Xml.Schema.XmlSchemaSet> 클래스로 바뀌었습니다.  
  
 <xref:System.Xml.Schema.XmlSchemaSet>이 추가되어 표준 호환성, 성능, 사용되지 않는 Microsoft XDR(XML-Data Reduced) 스키마 형식 등 많은 문제가 해결되었습니다.  
  
 다음은 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스와 <xref:System.Xml.Schema.XmlSchemaSet> 클래스를 비교한 것입니다.  
  
|XmlSchemaCollection|XmlSchemaSet|  
|-------------------------|------------------|  
|Microsoft XDR 및 W3C XML 스키마를 지원합니다.|W3C XML 스키마만 지원합니다.|  
|<xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> 메서드를 호출하면 스키마가 컴파일됩니다.|<xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 메서드를 호출해도 스키마가 컴파일되지 않습니다. 스키마 라이브러리를 만드는 동안의 성능이 향상됩니다.|  
|각 스키마는 컴파일된 개별 버전을 생성하며 이는 &quot;스키마 고립 영역&quot;이 될 수 있습니다. 결과적으로 모든 포함 및 가져오기 작업의 범위는 해당 스키마 내로 지정됩니다.|컴파일된 스키마는 스키마 &quot;집합&quot;인 단일 논리 스키마를 생성합니다. 이 집합에 추가한 스키마 내에 가져온 스키마는 이 집합 자체에 직접 추가됩니다. 그러므로 모든 스키마에 모든 형식을 사용할 수 있습니다.|  
|컬렉션 내에는 특정 대상 네임스페이스에 대한 스키마가 한 개만 존재할 수 있습니다.|형식 충돌이 없으면 같은 대상 네임스페이스에 대한 여러 스키마를 추가할 수 있습니다.|  
  
## <a name="migrating-to-the-xmlschemaset"></a>XmlSchemaSet으로 마이그레이션  
 다음 코드 예제에서는 사용되지 않는 <xref:System.Xml.Schema.XmlSchemaSet> 클래스에서 새 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스로 마이그레이션하는 방법을 보여 줍니다. 또한 두 클래스 간에 다음과 같은 주요 차이점을 설명합니다.  
  
-   <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> 클래스의 <xref:System.Xml.Schema.XmlSchemaCollection> 메서드와 달리 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 호출할 때 스키마가 컴파일되지 않습니다. 예제 코드에서는 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 명시적으로 호출합니다.  
  
-   <xref:System.Xml.Schema.XmlSchemaSet>을 반복하려면 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 속성을 사용해야 합니다.  
  
 다음은 사용되지 않는 <xref:System.Xml.Schema.XmlSchemaCollection> 코드 예제입니다.  
  
```vb  
Dim schemaCollection As XmlSchemaCollection = New XmlSchemaCollection()  
schemaCollection.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaCollection.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema in schemaCollection  
  
   Console.WriteLine(schema.TargetNamespace)  
  
Next  
```  
  
```csharp  
XmlSchemaCollection schemaCollection = new XmlSchemaCollection();  
schemaCollection.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaCollection.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
  
foreach(XmlSchema schema in schemaCollection)  
{  
   Console.WriteLine(schema.TargetNamespace);  
}  
```  
  
 다음은 이에 해당하는 <xref:System.Xml.Schema.XmlSchemaSet> 코드 예제입니다.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Compile()  
  
Dim schema As XmlSchema  
  
For Each schema in schemaSet.Schemas()  
  
   Console.WriteLine(schema.TargetNamespace)  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Compile();  
  
foreach(XmlSchema schema in schemaSet.Schemas())  
{  
   Console.WriteLine(schema.TargetNamespace);  
}  
```  
  
## <a name="adding-and-retrieving-schemas"></a>스키마 추가 및 검색  
 <xref:System.Xml.Schema.XmlSchemaSet>의 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 메서드를 사용하여 <xref:System.Xml.Schema.XmlSchemaSet>에 스키마를 추가합니다. 스키마가 <xref:System.Xml.Schema.XmlSchemaSet>에 추가되면 대상 네임스페이스 URI에 연결됩니다. 매개 변수로 대상 네임스페이스 URI를 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 메서드에 지정할 수 있으며 대상 네임스페이스를 지정하지 않은 경우 <xref:System.Xml.Schema.XmlSchemaSet>은 스키마에 정의된 대상 네임스페이스를 사용합니다.  
  
 <xref:System.Xml.Schema.XmlSchemaSet>의 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 속성을 사용하여 <xref:System.Xml.Schema.XmlSchemaSet>에서 스키마를 검색합니다. <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 속성을 사용하여 <xref:System.Xml.Schema.XmlSchema>에 포함된 <xref:System.Xml.Schema.XmlSchemaSet> 개체를 반복할 수 있습니다. <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 속성은 <xref:System.Xml.Schema.XmlSchema>에 포함된 모든 <xref:System.Xml.Schema.XmlSchemaSet> 개체를 반환합니다. 또는 대상 네임스페이스 매개 변수를 지정한 경우 대상 네임스페이스에 속한 모든 <xref:System.Xml.Schema.XmlSchema> 개체를 반환합니다. 대상 네임스페이스 매개 변수로 `null`을 지정한 경우 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 속성은 네임스페이스가 없는 모든 스키마를 반환합니다.  
  
 다음 예제에서는 `books.xsd` 네임스페이스의 `http://www.contoso.com/books` 스키마를 <xref:System.Xml.Schema.XmlSchemaSet>에 추가하고 `http://www.contoso.com/books`에서 <xref:System.Xml.Schema.XmlSchemaSet> 네임스페이스에 속한 모든 스키마를 검색한 다음 이 스키마를 <xref:System.Console>에 씁니다.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet  
schemaSet.Add("http://www.contoso.com/books", "books.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema In schemaSet.Schemas("http://www.contoso.com/books")  
  
   schema.Write(Console.Out)  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/books", "books.xsd");  
  
foreach (XmlSchema schema in schemaSet.Schemas("http://www.contoso.com/books"))  
{  
   schema.Write(Console.Out);  
}  
```  
  
 <xref:System.Xml.Schema.XmlSchemaSet> 개체에서 스키마를 추가하고 검색하는 방법은 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 메서드 및 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 속성 참조 문서를 참조하세요.  
  
## <a name="compiling-schemas"></a>스키마 컴파일  
 <xref:System.Xml.Schema.XmlSchemaSet>의 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드를 사용하면 <xref:System.Xml.Schema.XmlSchemaSet>에 있는 스키마가 논리 스키마 한 개로 컴파일됩니다.  
  
> [!NOTE]
>  사용되지 않는 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스와 달리 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 메서드를 호출할 때 스키마가 컴파일되지 않습니다.  
  
 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드를 성공적으로 실행한 경우 <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 속성은 `true`로 설정됩니다.  
  
> [!NOTE]
>  <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A>에 있는 동안 스키마를 편집해도 <xref:System.Xml.Schema.XmlSchemaSet> 속성에는 영향을 주지 않습니다. <xref:System.Xml.Schema.XmlSchemaSet>에서 개별 스키마를 업데이트한 내용은 추적되지 않습니다. 결과적으로 <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A>에 포함된 스키마 중 하나를 변경해도 `true`에서 스키마를 추가하거나 제거하지 않으면 <xref:System.Xml.Schema.XmlSchemaSet> 속성은 <xref:System.Xml.Schema.XmlSchemaSet>일 수 있습니다.  
  
 다음 예제에서는 `books.xsd` 파일을 <xref:System.Xml.Schema.XmlSchemaSet>에 추가하고 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드를 호출합니다.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/books", "books.xsd")  
schemaSet.Compile()  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/books", "books.xsd");  
schemaSet.Compile();  
```  
  
 <xref:System.Xml.Schema.XmlSchemaSet>의 스키마를 컴파일하는 방법은 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드 참조 문서를 참조하세요.  
  
## <a name="reprocessing-schemas"></a>스키마 다시 처리  
 <xref:System.Xml.Schema.XmlSchemaSet>에서 스키마를 다시 처리하면 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 호출할 때 스키마에서 수행된 모든 전처리 단계가 수행됩니다. <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 메서드를 성공적으로 호출한 경우 <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 속성은 `false`로 설정됩니다.  
  
 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>에서 컴파일을 수행한 후 <xref:System.Xml.Schema.XmlSchemaSet>의 스키마를 수정한 경우 <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 사용해야 합니다.  
  
 다음 예제에서는 <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 사용하여 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>에 추가한 스키마를 다시 처리하는 방법을 보여 줍니다. <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 사용하여 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>을 컴파일하고 <xref:System.Xml.Schema.XmlSchemaSet>에 추가된 스키마를 수정한 후에는 <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A>의 스키마를 수정했더라도 `true` 속성은 <xref:System.Xml.Schema.XmlSchemaSet>로 설정됩니다. <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 메서드를 호출하면 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> 메서드에 의해 수행된 모든 전처리가 수행되며 <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> 속성이 `false`로 설정됩니다.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
Dim schema As XmlSchema = schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Compile()  
  
Dim element As XmlSchemaElement = New XmlSchemaElement()  
schema.Items.Add(element)  
element.Name = "book"  
element.SchemaTypeName = New XmlQualifiedName("string", "http://www.w3.org/2001/XMLSchema")  
  
schemaSet.Reprocess(schema)  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
XmlSchema schema = schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Compile();  
  
XmlSchemaElement element = new XmlSchemaElement();  
schema.Items.Add(element);  
element.Name = "book";  
element.SchemaTypeName = new XmlQualifiedName("string", "http://www.w3.org/2001/XMLSchema");  
  
schemaSet.Reprocess(schema);  
```  
  
 <xref:System.Xml.Schema.XmlSchemaSet>의 스키마를 다시 처리하는 방법은 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 메서드 참조 문서를 참조하세요.  
  
## <a name="checking-for-a-schema"></a>스키마 검사  
 <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A>의 <xref:System.Xml.Schema.XmlSchemaSet> 메서드를 사용하여 스키마가 <xref:System.Xml.Schema.XmlSchemaSet>에 포함되었는지 확인할 수 있습니다. <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> 메서드는 검사할 대상 네임스페이스 또는 <xref:System.Xml.Schema.XmlSchema> 개체를 가져옵니다. 두 경우 모두 스키마가 <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> 내에 포함된 경우 `true` 메서드는 <xref:System.Xml.Schema.XmlSchemaSet>를 반환하며 그렇지 않으면 `false`를 반환합니다.  
  
 스키마 검사에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> 메서드 참조 문서를 참조하세요.  
  
## <a name="removing-schemas"></a>스키마 제거  
 <xref:System.Xml.Schema.XmlSchemaSet>의 <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> 및 <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> 메서드를 사용하여 <xref:System.Xml.Schema.XmlSchemaSet>에서 스키마를 제거할 수 있습니다. <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> 메서드는 <xref:System.Xml.Schema.XmlSchemaSet>에서 지정된 스키마를 제거하며 <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> 메서드는 지정된 스키마 및 이 스키마가 가져오는 모든 스키마를 <xref:System.Xml.Schema.XmlSchemaSet>에서 제거합니다.  
  
 다음 예제에서는 <xref:System.Xml.Schema.XmlSchemaSet>에 여러 스키마를 추가하고 <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> 메서드를 사용하여 스키마 중 하나와 이 스키마가 가져오는 모든 스키마를 제거합니다.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Add("http://www.contoso.com/music", "http://www.contoso.com/music.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema In schemaSet.Schemas()  
  
   If schema.TargetNamespace = "http://www.contoso.com/music" Then  
      schemaSet.RemoveRecursive(schema)  
   End If  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Add("http://www.contoso.com/music", "http://www.contoso.com/music.xsd");  
  
foreach (XmlSchema schema in schemaSet.Schemas())  
{  
   if (schema.TargetNamespace == "http://www.contoso.com/music")  
   {  
      schemaSet.RemoveRecursive(schema);  
   }  
}  
```  
  
 <xref:System.Xml.Schema.XmlSchemaSet>에서 스키마를 제거하는 방법은 <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> 및 <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> 메서드 참조 문서를 참조하세요.  
  
## <a name="schema-resolution-and-xsimport"></a>스키마 확인 및 xs:import  
 다음 예제에서는 지정된 네임스페이스에 대한 여러 스키마가 <xref:System.Xml.Schema.XmlSchemaSet>에 있을 경우 스키마를 가져오는 <xref:System.Xml.Schema.XmlSchemaSet> 동작에 대해 설명합니다.  
  
 예를 들어, <xref:System.Xml.Schema.XmlSchemaSet> 네임스페이스에 대한 여러 스키마가 포함된 `http://www.contoso.com`을 살펴봅니다. 다음 `xs:import` 지시문이 있는 스키마가 <xref:System.Xml.Schema.XmlSchemaSet>에 추가됩니다.  
  
```xml  
<xs:import namespace="http://www.contoso.com" schemaLocation="http://www.contoso.com/schema.xsd" />  
```  
  
 <xref:System.Xml.Schema.XmlSchemaSet>은 `http://www.contoso.com` URL에서 `http://www.contoso.com/schema.xsd` 네임스페이스에 대한 스키마를 로드하여 가져오려고 시도합니다. `http://www.contoso.com`에 <xref:System.Xml.Schema.XmlSchemaSet> 네임스페이스에 대한 다른 스키마 문서가 있더라도 가져오는 스키마에서는 스키마 선언 및 스키마 문서에서 선언된 형식만 사용할 수 있습니다. `schema.xsd` 파일을 `http://www.contoso.com/schema.xsd` URL에서 찾을 수 없으면 가져오는 스키마로 `http://www.contoso.com` 네임스페이스에 대한 스키마를 가져올 수 없습니다.  
  
## <a name="validating-xml-documents"></a>XML 문서 유효성 검사  
 <xref:System.Xml.Schema.XmlSchemaSet>의 스키마에 대해 XML 문서의 유효성을 검사할 수 있습니다. <xref:System.Xml.XmlReaderSettings> 개체의 <xref:System.Xml.Schema.XmlSchemaSet><xref:System.Xml.XmlReaderSettings.Schemas%2A> 속성에 스키마를 추가하거나 <xref:System.Xml.XmlReaderSettings> 개체의 <xref:System.Xml.XmlReaderSettings.Schemas%2A> 속성에 <xref:System.Xml.Schema.XmlSchemaSet>을 추가하여 XML 문서의 유효성을 검사할 수 있습니다. 그런 다음 <xref:System.Xml.XmlReaderSettings> 클래스의 <xref:System.Xml.XmlReader.Create%2A> 메서드에서 <xref:System.Xml.XmlReader> 개체를 사용하여 <xref:System.Xml.XmlReader> 개체를 만들고 XML 문서의 유효성을 검사할 수 있습니다.  
  
 <xref:System.Xml.Schema.XmlSchemaSet>을 사용하여 XML 문서의 유효성을 검사하는 방법에 대한 자세한 내용은 [XmlSchemaSet을 사용하여 XSD(XML 스키마) 유효성 검사](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemaset.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>  
- <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>  
- <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A>  
- <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>  
- <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>  
- <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A>  
- <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A>  
- [스키마 캐시로서 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)  
- [XmlSchemaSet을 사용하여 XSD(XML 스키마) 유효성 검사](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemaset.md)
