---
title: XPathNavigator를 사용하여 XML 데이터 추출
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 095b0987-ee4b-4595-a160-da1c956ad576
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d838f3d9f4c9400fbbef0fb24f5275eff2038c49
ms.sourcegitcommit: 2eb5ca4956231c1a0efd34b6a9cab6153a5438af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49086780"
---
# <a name="extract-xml-data-using-xpathnavigator"></a>XPathNavigator를 사용하여 XML 데이터 추출
Microsoft .NET Framework에서는 여러 가지 방법으로 XML 문서를 나타낼 수 있습니다. 예를 들어, <xref:System.String>을 사용하거나 <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter>, <xref:System.Xml.XmlDocument> 또는 <xref:System.Xml.XPath.XPathDocument> 클래스를 사용하여 XML 문서를 나타낼 수 있습니다. 여러 가지 XML 문서 표현 간을 이동할 수 있도록 <xref:System.Xml.XPath.XPathNavigator> 클래스는 XML을 <xref:System.String>, <xref:System.Xml.XmlReader> 개체 또는 <xref:System.Xml.XmlWriter> 개체로 추출하는 많은 메서드와 속성을 제공합니다.  
  
## <a name="convert-an-xpathnavigator-to-a-string"></a>XPathNavigator를 문자열로 변환  
 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 속성을 사용하여 전체 XML 문서의 태그를 가져오거나 단일 노드 및 해당 자식 노드의 태그만 가져올 수 있습니다.  
  
> [!NOTE]
>  <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 속성은 노드의 자식 노드의 태그만 가져옵니다.  
  
 다음 코드 예제에서는 <xref:System.Xml.XPath.XPathNavigator> 개체에 <xref:System.String>으로 포함된 전체 XML 문서 및 단일 노드와 자식 노드를 저장하는 방법을 보여 줍니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("input.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Save the entire input.xml document to a string.  
Dim xml As String = navigator.OuterXml  
  
' Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element)  
Dim root As String = navigator.OuterXml  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Save the entire input.xml document to a string.  
string xml = navigator.OuterXml;  
  
// Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element);  
string root = navigator.OuterXml;  
```  
  
## <a name="convert-an-xpathnavigator-to-an-xmlreader"></a>XPathNavigator를 XmlReader로 변환  
 <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> 메서드를 사용하면 XML 문서의 전체 내용이나 단일 노드 및 해당 자식 노드만 <xref:System.Xml.XmlReader> 개체로 스트림할 수 있습니다.  
  
 현재 노드 및 자식 노드를 사용하여 <xref:System.Xml.XmlReader> 개체를 만든 경우 <xref:System.Xml.XmlReader> 개체의 <xref:System.Xml.XmlReader.ReadState%2A> 속성은 <xref:System.Xml.ReadState.Initial>로 설정됩니다. <xref:System.Xml.XmlReader> 개체의 <xref:System.Xml.XmlReader.Read%2A> 메서드를 처음으로 호출하면 <xref:System.Xml.XmlReader>가 <xref:System.Xml.XPath.XPathNavigator>의 현재 노드로 이동합니다. 새 <xref:System.Xml.XmlReader> 개체는 XML 트리 끝에 도달할 때까지 계속 읽습니다. 이때 <xref:System.Xml.XmlReader.Read%2A> 메서드는 `false`를 반환하고 <xref:System.Xml.XmlReader> 개체의 <xref:System.Xml.XmlReader.ReadState%2A> 속성은 <xref:System.Xml.ReadState.EndOfFile>로 설정됩니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 개체를 만들거나 이동해도 <xref:System.Xml.XmlReader> 개체의 위치는 변경되지 않습니다. <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> 메서드는 요소 또는 루트 노드에 있을 경우에만 유효합니다.  
  
 다음 예제에서는 <xref:System.Xml.XmlReader> 개체의 전체 XML 문서를 포함하는 <xref:System.Xml.XPath.XPathDocument> 개체뿐만 아니라 단일 노드 및 해당 자식 노드도 가져오는 방법을 보여 줍니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlReader.  
Dim xml As XmlReader = navigator.ReadSubtree()  
  
While xml.Read()  
    Console.WriteLine(xml.ReadInnerXml())  
End While  
  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlReader = navigator.ReadSubtree()  
  
While book.Read()  
    Console.WriteLine(book.ReadInnerXml())  
End While  
  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlReader.  
XmlReader xml = navigator.ReadSubtree();  
  
while (xml.Read())  
{  
    Console.WriteLine(xml.ReadInnerXml());  
}  
  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlReader book = navigator.ReadSubtree();  
  
while (book.Read())  
{  
    Console.WriteLine(book.ReadInnerXml());  
}  
  
book.Close();  
```  
  
 이 예제에서는 `books.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
## <a name="converting-an-xpathnavigator-to-an-xmlwriter"></a>XPathNavigator를 XmlWriter로 변환  
 <xref:System.Xml.XPath.XPathNavigator.WriteSubtree%2A> 메서드를 사용하면 XML 문서의 전체 내용이나 단일 노드 및 해당 자식 노드만 <xref:System.Xml.XmlWriter> 개체로 스트림할 수 있습니다.  
  
 <xref:System.Xml.XPath.XPathNavigator> 개체를 만들어도 <xref:System.Xml.XmlWriter> 개체의 위치는 변경되지 않습니다.  
  
 다음 예제에서는 <xref:System.Xml.XmlWriter> 개체의 전체 XML 문서를 포함하는 <xref:System.Xml.XPath.XPathDocument> 개체뿐만 아니라 단일 노드 및 해당 자식 노드도 가져오는 방법을 보여 줍니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlWriter.  
Dim xml As XmlWriter = XmlWriter.Create("newbooks.xml")  
navigator.WriteSubtree(xml)  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlWriter = XmlWriter.Create("book.xml")  
navigator.WriteSubtree(book)  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlWriter.  
XmlWriter xml = XmlWriter.Create("newbooks.xml");  
navigator.WriteSubtree(xml);  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlWriter book = XmlWriter.Create("book.xml");  
navigator.WriteSubtree(book);  
book.Close();  
```  
  
 이 예제에서는 이 항목의 앞부분에 있는 `books.xml` 파일을 입력으로 사용합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>  
- <xref:System.Xml.XPath.XPathDocument>  
- <xref:System.Xml.XPath.XPathNavigator>  
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
- [XPathNavigator를 사용하여 노드 집합 탐색](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)  
- [XPathNavigator를 사용하여 특성 및 네임스페이스 노드 탐색](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)  
- [XPathNavigator를 사용하여 강력한 형식의 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
