---
title: XPathNavigator를 사용하여 스키마 유효성 검사
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 81fa0e41-d9c9-46f0-b22b-50da839c77f5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0199efb172466305af22c4ade7c47115a5cefd8f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939615"
---
# <a name="schema-validation-using-xpathnavigator"></a>XPathNavigator를 사용하여 스키마 유효성 검사
<xref:System.Xml.XmlDocument> 클래스를 사용하면 두 가지 방법으로 <xref:System.Xml.XmlDocument> 개체에 포함된 XML 내용의 유효성을 검사할 수 있습니다. 첫 번째 방법은 유효성 검사 <xref:System.Xml.XmlReader> 개체를 사용하여 XML 내용의 유효성을 검사하는 것이고 두 번째 방법은 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하는 것입니다. <xref:System.Xml.XPath.XPathDocument> 클래스를 사용하여 XML 내용의 읽기 전용 유효성 검사를 수행할 수도 있습니다.  
  
## <a name="validating-xml-data"></a>XML 데이터 유효성 검사  
 기본적으로 <xref:System.Xml.XmlDocument> 클래스는 DTD나 XSD(XML 스키마 정의 언어) 스키마 유효성 검사를 통해 XML 문서의 유효성을 검사하지 않으며 XML 문서가 제대로 구성되었는지만 확인합니다.  
  
 XML 문서의 유효성을 검사하는 첫 번째 방법은 유효성을 검사하는 <xref:System.Xml.XmlDocument> 개체를 사용하여 <xref:System.Xml.XmlReader> 개체로 XML 문서를 로드할 때 유효성을 검사하는 것입니다. 두 번째 방법은 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하여 이전에 형식화한 XML 문서의 유효성을 검사하는 것입니다. 두 가지 경우 모두 유효성을 검사한 XML 문서의 변경 내용에 대해 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하여 유효성을 다시 검사할 수 있습니다.  
  
### <a name="validating-a-document-as-it-is-loaded"></a>문서를 로드할 때 유효성 검사  
 <xref:System.Xml.XmlReader> 개체를 매개 변수로 사용하는 <xref:System.Xml.XmlReaderSettings> 클래스의 <xref:System.Xml.XmlReader.Create%2A> 메서드에 <xref:System.Xml.XmlReader> 개체를 전달하면 유효성을 검사하는 <xref:System.Xml.XmlReaderSettings> 개체가 만들어집니다. 매개 변수로 전달된 <xref:System.Xml.XmlReaderSettings> 개체의 <xref:System.Xml.XmlReaderSettings.ValidationType%2A> 속성은 `Schema`로 설정되어 있으며 <xref:System.Xml.XmlDocument> 속성에 추가된 <xref:System.Xml.XmlReaderSettings.Schemas%2A> 개체에 XML 문서의 XML 스키마가 포함되어 있습니다. 그러면 유효성을 검사하는 <xref:System.Xml.XmlReader> 개체를 사용하여 <xref:System.Xml.XmlDocument> 개체를 만들 수 있습니다.  
  
 다음 예제에서는 `contosoBooks.xml` 개체의 유효성 검사를 통해 <xref:System.Xml.XmlDocument> 개체를 만들어 <xref:System.Xml.XmlDocument> 파일이 <xref:System.Xml.XmlReader> 개체로 로드되면 해당 파일의 유효성을 검사합니다. 해당 스키마에 따르면 XML 문서가 유효하기 때문에 스키마 유효성 검사 오류 또는 경고가 생성되지 않습니다.  
  
```vb  
Imports System  
Imports System.Xml  
Imports System.Xml.Schema  
Imports System.Xml.XPath  
  
Class ValidatingReaderExample  
  
    Shared Sub Main(ByVal args() As String)  
  
        Try  
            Dim settings As XmlReaderSettings = New XmlReaderSettings()  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
            settings.ValidationType = ValidationType.Schema  
  
            Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
            Dim document As XmlDocument = New XmlDocument()  
            document.Load(reader)  
            Dim navigator As XPathNavigator = document.CreateNavigator()  
  
        Catch e As Exception  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message)  
        End Try  
  
    End Sub  
  
    Shared Sub SchemaValidationHandler(ByVal sender As Object, ByVal e As ValidationEventArgs)  
  
        Select Case e.Severity  
            Case XmlSeverityType.Error  
                Console.WriteLine("Schema Validation Error: {0}", e.Message)  
                Exit Sub  
            Case XmlSeverityType.Warning  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message)  
                Exit Sub  
        End Select  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.Xml.XPath;  
  
class ValidatingReaderExample  
{  
    static void Main(string[] args)  
    {  
        try  
        {  
            XmlReaderSettings settings = new XmlReaderSettings();  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
            settings.ValidationType = ValidationType.Schema;  
  
            XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
            XmlDocument document = new XmlDocument();  
            document.Load(reader);  
            XPathNavigator navigator = document.CreateNavigator();  
        }  
        catch (Exception e)  
        {  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message);  
        }  
    }  
  
    static void SchemaValidationHandler(object sender, ValidationEventArgs e)  
    {  
        switch (e.Severity)  
        {  
            case XmlSeverityType.Error:  
                Console.WriteLine("Schema Validation Error: {0}", e.Message);  
                break;  
            case XmlSeverityType.Warning:  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message);  
                break;  
        }  
    }  
}  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 이 예제에서는 또한 `contosoBooks.xsd`를 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
 위 예제에서 <xref:System.Xml.Schema.XmlSchemaValidationException>가 호출될 때 특성 또는 요소 형식이 유효성 검사 스키마에 지정된 해당 형식과 일치하지 않으면 <xref:System.Xml.XmlDocument.Load%2A>이 throw됩니다. <xref:System.Xml.XmlReaderSettings.ValidationEventHandler> 유효성 검사에 <xref:System.Xml.XmlReader>가 설정된 경우 잘못된 형식이 발견될 때마다 <xref:System.Xml.XmlReaderSettings.ValidationEventHandler>가 호출됩니다.  
  
 <xref:System.Xml.Schema.XmlSchemaException>가 <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A>로 설정된 특성 또는 요소를 `invalid`에서 액세스하는 경우 <xref:System.Xml.XPath.XPathNavigator>이 throw됩니다.  
  
 <xref:System.Xml.Schema.XmlSchemaInfo.Validity%2A>로 특성 또는 요소에 액세스할 때 <xref:System.Xml.XPath.XPathNavigator> 속성을 사용하여 개별 특성 또는 요소가 유효한지 여부를 확인할 수 있습니다.  
  
> [!NOTE]
> 기본값을 정의하는 스키마가 연결되어 있는 XML 문서를 <xref:System.Xml.XmlDocument> 개체에 로드하면 <xref:System.Xml.XmlDocument> 개체는 이 기본값이 XML 문서에 나타난 것처럼 처리합니다. 그러므로 빈 요소로 쓰여진 XML 문서에서도 <xref:System.Xml.XPath.XPathNavigator.IsEmptyElement%2A> 속성은 스키마에서 기본값으로 설정된 요소에 대해 항상 `false`를 반환합니다.  
  
### <a name="validating-a-document-using-the-validate-method"></a>Validate 메서드를 사용하여 문서의 유효성 검사  
 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드는 <xref:System.Xml.XmlDocument> 개체의 <xref:System.Xml.XmlDocument> 속성에 지정된 스키마에 대해 <xref:System.Xml.XmlDocument.Schemas%2A> 개체에 포함된 XML 문서의 유효성을 검사하고 Infoset 확대를 수행합니다. 그 결과 <xref:System.Xml.XmlDocument> 개체에서 이전에 형식화하지 않은 XML 문서가 형식화된 문서로 바뀝니다.  
  
 <xref:System.Xml.XmlDocument> 개체는 <xref:System.Xml.Schema.ValidationEventHandler> 메서드에 매개 변수로 전달된 <xref:System.Xml.XmlDocument.Validate%2A> 대리자를 사용하여 스키마 유효성 검사 오류 및 경고를 보고합니다.  
  
 다음 예제에서는 `contosoBooks.xml` 개체의 <xref:System.Xml.XmlDocument> 속성에 포함된 `contosoBooks.xsd` 스키마에 대해 <xref:System.Xml.XmlDocument> 개체에 포함된 <xref:System.Xml.XmlDocument.Schemas%2A> 파일의 유효성을 검사합니다.  
  
```vb  
Imports System  
Imports System.Xml  
Imports System.Xml.Schema  
Imports System.Xml.XPath  
  
Class ValidateExample  
  
    Shared Sub Main(ByVal args() As String)  
  
        Dim document As XmlDocument = New XmlDocument()  
        document.Load("contosoBooks.xml")  
        Dim navigator As XPathNavigator = document.CreateNavigator()  
  
        document.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
        Dim validation As ValidationEventHandler = New ValidationEventHandler(AddressOf SchemaValidationHandler)  
  
        document.Validate(validation)  
  
    End Sub  
  
    Shared Sub SchemaValidationHandler(ByVal sender As Object, ByVal e As ValidationEventArgs)  
  
        Select Case e.Severity  
            Case XmlSeverityType.Error  
                Console.WriteLine("Schema Validation Error: {0}", e.Message)  
                Exit Sub  
            Case XmlSeverityType.Warning  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message)  
                Exit Sub  
        End Select  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.Xml.XPath;  
  
class ValidateExample  
{  
    static void Main(string[] args)  
    {  
        XmlDocument document = new XmlDocument();  
        document.Load("contosoBooks.xml");  
        XPathNavigator navigator = document.CreateNavigator();  
  
        document.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
        ValidationEventHandler validation = new ValidationEventHandler(SchemaValidationHandler);  
  
        document.Validate(validation);  
    }  
  
    static void SchemaValidationHandler(object sender, ValidationEventArgs e)  
    {  
        switch (e.Severity)  
        {  
            case XmlSeverityType.Error:  
                Console.WriteLine("Schema Validation Error: {0}", e.Message);  
                break;  
            case XmlSeverityType.Warning:  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message);  
                break;  
        }  
    }  
}  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 이 예제에서는 또한 `contosoBooks.xsd`를 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
### <a name="validating-modifications"></a>수정 내용 유효성 검사  
 XML 문서를 수정한 후 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하여 XML 문서의 스키마에 대해 수정 내용의 유효성을 검사할 수 있습니다.  
  
 다음 예제에서는 `contosoBooks.xml` 개체의 유효성 검사를 통해 <xref:System.Xml.XmlDocument> 개체를 만들어 <xref:System.Xml.XmlDocument> 파일이 <xref:System.Xml.XmlReader> 개체로 로드되면 해당 파일의 유효성을 검사합니다. 스키마 유효성 검사 오류 또는 경고가 생성되지 않고 로드되었으므로 XML 문서의 유효성이 성공적으로 검사됩니다. 그런 다음 예제에서는 `contosoBooks.xsd` 스키마에 따라 XML 문서에서 유효하지 않은 두 가지 사항을 수정합니다. 첫 번째 수정 사항은 잘못된 자식 요소를 삽입하여 스키마 유효성 검사 오류가 발생하도록 하는 것이고 두 번째 수정 사항은 노드 형식에 따르면 유효하지 않은 값으로, 형식화된 노드 값을 설정하여 예외가 발생하도록 하는 것입니다.  
  
```vb  
Imports System  
Imports System.Xml  
Imports System.Xml.Schema  
Imports System.Xml.XPath  
  
Class ValidatingReaderExample  
  
    Shared Sub Main(ByVal args() As String)  
  
        Try  
            Dim settings As XmlReaderSettings = New XmlReaderSettings()  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
            settings.ValidationType = ValidationType.Schema  
  
            Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
            Dim document As XmlDocument = New XmlDocument()  
            document.Load(reader)  
            Dim navigator As XPathNavigator = document.CreateNavigator()  
  
            Dim validation As ValidationEventHandler = New ValidationEventHandler(AddressOf SchemaValidationHandler)  
  
            navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
            navigator.MoveToChild("book", "http://www.contoso.com/books")  
            navigator.MoveToChild("author", "http://www.contoso.com/books")  
  
            navigator.AppendChild("<title>Book Title</title>")  
  
            document.Validate(validation)  
  
            navigator.MoveToParent()  
            navigator.MoveToChild("price", "http://www.contoso.com/books")  
            navigator.SetTypedValue(DateTime.Now)  
        Catch e As Exception  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message)  
        End Try  
  
    End Sub  
  
    Shared Sub SchemaValidationHandler(ByVal sender As Object, ByVal e As ValidationEventArgs)  
  
        Select Case e.Severity  
            Case XmlSeverityType.Error  
                Console.WriteLine("Schema Validation Error: {0}", e.Message)  
                Exit Sub  
            Case XmlSeverityType.Warning  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message)  
                Exit Sub  
        End Select  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.Xml.XPath;  
  
class ValidatingReaderExample  
{  
    static void Main(string[] args)  
    {  
        try  
        {  
            XmlReaderSettings settings = new XmlReaderSettings();  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
            settings.ValidationType = ValidationType.Schema;  
  
            XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
            XmlDocument document = new XmlDocument();  
            document.Load(reader);  
            XPathNavigator navigator = document.CreateNavigator();  
  
            ValidationEventHandler validation = new ValidationEventHandler(SchemaValidationHandler);  
  
            navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
            navigator.MoveToChild("book", "http://www.contoso.com/books");  
            navigator.MoveToChild("author", "http://www.contoso.com/books");  
  
            navigator.AppendChild("<title>Book Title</title>");  
  
            document.Validate(validation);  
  
            navigator.MoveToParent();  
            navigator.MoveToChild("price", "http://www.contoso.com/books");  
            navigator.SetTypedValue(DateTime.Now);  
        }  
        catch (Exception e)  
        {  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message);  
        }  
    }  
  
    static void SchemaValidationHandler(object sender, ValidationEventArgs e)  
    {  
        switch (e.Severity)  
        {  
            case XmlSeverityType.Error:  
                Console.WriteLine("Schema Validation Error: {0}", e.Message);  
                break;  
            case XmlSeverityType.Warning:  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message);  
                break;  
        }  
    }  
}  
```  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 이 예제에서는 또한 `contosoBooks.xsd`를 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
 위 예제에서는 <xref:System.Xml.XmlDocument> 개체에 포함된 XML 문서에서 두 가지 사항을 수정했습니다. XML 문서를 로드할 때 발생한 스키마 유효성 검사 오류는 유효성 검사 이벤트 처리기 메서드에 의해 처리되고 콘솔에 기록됩니다.  
  
 이 예제에서는 XML 문서를 로드한 후 유효성 검사 오류가 발생했으며 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하여 오류가 발견되었습니다.  
  
 노드의 스키마 형식에 따르면 새 값이 유효하지 않기 때문에 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 메서드를 사용하여 수정한 사항으로 인해 <xref:System.InvalidCastException>이 발생했습니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> 메서드를 사용하여 값을 수정하는 방법에 대한 자세한 내용은 [XPathNavigator를 사용하여 XML 데이터 수정](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md) 항목을 참조하세요.  
  
### <a name="read-only-validation"></a>읽기 전용 유효성 검사  
 <xref:System.Xml.XPath.XPathDocument> 클래스는 읽기 전용 메모리 내 XML 문서 표현입니다. <xref:System.Xml.XPath.XPathDocument> 클래스와 <xref:System.Xml.XmlDocument> 클래스는 <xref:System.Xml.XPath.XPathNavigator> 개체를 만들어 XML 문서를 탐색하고 편집합니다. <xref:System.Xml.XPath.XPathDocument> 클래스는 읽기 전용 클래스이므로 <xref:System.Xml.XPath.XPathNavigator> 개체에서 반환된 <xref:System.Xml.XPath.XPathDocument> 개체는 <xref:System.Xml.XPath.XPathDocument> 개체에 포함된 XML 문서를 편집할 수 없습니다.  
  
 유효성 검사의 경우 이 항목의 앞부분에서 설명한 대로 유효성을 검사하는 <xref:System.Xml.XPath.XPathDocument> 개체를 사용하여 <xref:System.Xml.XmlDocument> 개체를 만든 것과 같이 <xref:System.Xml.XmlReader> 개체를 만들 수 있습니다. <xref:System.Xml.XPath.XPathDocument> 개체는 XML 문서를 로드할 때 이 문서의 유효성을 검사하지만 <xref:System.Xml.XPath.XPathDocument> 개체에서 XML 데이터를 편집할 수 없으므로 XML 문서의 유효성을 다시 검사할 수 없습니다.  
  
 읽기 전용 및 편집 가능한 <xref:System.Xml.XPath.XPathNavigator> 개체에 대한 자세한 내용은 [XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md) 항목을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)
- [XPathNavigator를 사용하여 XML 데이터 선택, 평가 및 일치시키기](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 편집](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)
