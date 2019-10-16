---
title: XPath 탐색을 사용하여 노드 선택
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 8e4450dc-56b3-472b-b467-32f5694f83ad
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b2fc0846b3f3801d64ee3bf1f1dc4b347034ad38
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939560"
---
# <a name="select-nodes-using-xpath-navigation"></a>XPath 탐색을 사용하여 노드 선택
XML DOM(문서 개체 모델)에는 XPath(XML Path Language) 탐색을 사용하여 DOM의 정보를 쿼리할 수 있는 메서드가 있습니다. XPath를 사용하여 단일 노드를 찾거나 특정 기준과 일치하는 모든 노드를 찾을 수 있습니다.  
  
## <a name="xpath-select-methods"></a>XPath Select 메서드  
 DOM 클래스는 XPath 선택을 위해 <xref:System.Xml.XmlNode.SelectSingleNode%2A> 메서드와 <xref:System.Xml.XmlNode.SelectNodes%2A> 메서드를 제공합니다. <xref:System.Xml.XmlNode.SelectSingleNode%2A> 메서드는 선택 기준과 일치하는 첫 번째 노드를 반환합니다. <xref:System.Xml.XmlNode.SelectNodes%2A> 메서드는 일치하는 노드가 포함된 <xref:System.Xml.XmlNodeList>를 반환합니다.  
  
 다음 예제에서는 <xref:System.Xml.XmlNode.SelectSingleNode%2A> 메서드를 사용하여 저자의 성이 지정된 기준을 충족하는 첫 번째 `book` 노드를 선택합니다. 이 항목의 끝에서 제공되는 bookstore.xml 파일이 입력 파일로 사용됩니다.  
  
```vb  
Dim doc As New XmlDocument()  
doc.Load("bookstore.xml")  
Dim root As XmlNode = doc.DocumentElement  
  
' Add the namespace.  
Dim nsmgr As New XmlNamespaceManager(doc.NameTable)  
nsmgr.AddNamespace("bk", "urn:newbooks-schema")  
  
' Select and display the first node in which the author's   
' last name is Kingsolver.  
Dim node As XmlNode = root.SelectSingleNode( _  
     "descendant::bk:book[bk:author/bk:last-name='Kingsolver']", nsmgr)  
Console.WriteLine(node.InnerXml)  
```  
  
```csharp  
// Load the document and set the root element.  
XmlDocument doc = new XmlDocument();  
doc.Load("bookstore.xml");  
XmlNode root = doc.DocumentElement;  
  
// Add the namespace.  
XmlNamespaceManager nsmgr = new XmlNamespaceManager(doc.NameTable);  
nsmgr.AddNamespace("bk", "urn:newbooks-schema");  
  
// Select and display the first node in which the author's   
// last name is Kingsolver.  
XmlNode node = root.SelectSingleNode(  
    "descendant::bk:book[bk:author/bk:last-name='Kingsolver']", nsmgr);  
Console.WriteLine(node.InnerXml);  
```  
  
 다음 예제에서는 <xref:System.Xml.XmlNode.SelectNodes%2A> 메서드를 사용하여 가격이 지정된 금액보다 높은 모든 책 노드를 선택합니다. 선택된 목록에 있는 각 책의 가격은 프로그래밍 방식으로 10% 줄어듭니다. 마지막으로, 업데이트된 파일이 콘솔에 기록됩니다. 이 항목의 끝에서 제공되는 bookstore.xml 파일이 입력 파일로 사용됩니다.  
  
```vb  
' Load the document and set the root element.  
Dim doc As New XmlDocument()  
doc.Load("bookstore.xml")  
Dim root As XmlNode = doc.DocumentElement  
  
' Add the namespace.  
Dim nsmgr As New XmlNamespaceManager(doc.NameTable)  
nsmgr.AddNamespace("bk", "urn:newbooks-schema")  
  
' Select all nodes where the book price is greater than 10.00.  
Dim nodeList As XmlNodeList = root.SelectNodes( _  
     "descendant::bk:book[bk:price>10.00]", nsmgr)  
For Each book As XmlNode In nodeList  
     Dim price As Double  
     price = Math.Round(Convert.ToSingle( _  
          book.LastChild.InnerText) * 0.9, 2)  
     book.LastChild.InnerText = price.ToString()  
Next  
  
' Display the updated document.  
doc.Save(Console.Out)  
```  
  
```csharp  
// Load the document and set the root element.  
XmlDocument doc = new XmlDocument();  
doc.Load("bookstore.xml");  
XmlNode root = doc.DocumentElement;  
  
// Add the namespace.  
XmlNamespaceManager nsmgr = new XmlNamespaceManager(doc.NameTable);  
nsmgr.AddNamespace("bk", "urn:newbooks-schema");  
  
// Select all nodes where the book price is greater than 10.00.  
XmlNodeList nodeList = root.SelectNodes(  
     "descendant::bk:book[bk:price>10.00]", nsmgr);  
foreach (XmlNode book in nodeList)  
{  
     // Discount prices by 10%.  
     double price;  
     price = Math.Round(Convert.ToSingle(  
          book.LastChild.InnerText) * 0.9, 2);  
     book.LastChild.InnerText = price.ToString();  
}  
  
// Display the updated document.  
doc.Save(Console.Out);  
```  
  
 위의 예제에서는 문서 요소에서 XPath 쿼리를 시작합니다. XPath 쿼리의 시작 지점을 설정하면 XPath 쿼리의 시작점인 컨텍스트 노드가 설정됩니다. 문서 요소에서 시작하지 않고 문서 요소의 첫 번째 자식에서 시작하려면 다음과 같이 select 문을 코딩합니다.  
  
```vb  
doc.DocumentElement.FirstChild.SelectNodes(. . . )  
```  
  
```csharp  
this doc.DocumentElement.FirstChild.SelectNodes(. . .);  
```  
  
 모든 <xref:System.Xml.XmlNodeList> 개체는 기본 문서와 동기화됩니다. 그러므로 노드 목록을 반복하고 노드 값을 수정하는 경우 원래 노드가 있는 문서에서도 이 노드가 업데이트됩니다. 이전 예제에서는 노드가 선택된 <xref:System.Xml.XmlNodeList>에서 수정될 때 기본 문서도 수정됩니다.  
  
> [!NOTE]
> 기본 문서를 수정한 경우 select 문을 다시 실행하는 것이 좋습니다. 수정된 노드가 이전에 없던 노드를 노드 목록에 추가하거나 제거할 수 있는 노드라면 노드 목록이 정확하지 않을 수도 있습니다.  
  
## <a name="namespaces-in-xpath-expressions"></a>XPath 식의 네임스페이스  
 XPath 식에 네임스페이스를 포함할 수 있습니다. 네임스페이스는 <xref:System.Xml.XmlNamespaceManager>를 사용하여 확인할 수 있습니다. XPath 식에 접두사가 포함된 경우 접두사와 네임스페이스 URI 쌍을 <xref:System.Xml.XmlNamespaceManager>에 추가해야 하며 <xref:System.Xml.XmlNamespaceManager>는 <xref:System.Xml.XmlNode.SelectNodes%28System.String%2CSystem.Xml.XmlNamespaceManager%29> 또는 <xref:System.Xml.XmlNode.SelectSingleNode%28System.String%2CSystem.Xml.XmlNamespaceManager%29> 메서드에 전달됩니다. 위의 코드 예제에서는 <xref:System.Xml.XmlNamespaceManager>를 사용하여 bookstore.xml 문서의 네임스페이스를 확인합니다.  
  
> [!NOTE]
> XPath 식에 접두사가 포함되지 않은 경우 네임스페이스 URI(Uniform Resource Identifier)를 빈 네임스페이스로 가정합니다. XML에 기본 네임스페이스가 포함된 경우에도 접두사 및 네임스페이스 URI를 <xref:System.Xml.XmlNamespaceManager>에 추가해야 합니다. 이렇게 하지 않으면 노드를 선택할 수 없습니다.  
  
#### <a name="input-file"></a>입력 파일  
 다음은 이 항목의 예제에서 입력 파일로 사용되는 bookstore.xml 파일입니다.  
  
```xml  
<?xml version='1.0'?>  
<bookstore xmlns="urn:newbooks-schema">  
  <book genre="novel" style="hardcover">  
    <title>The Handmaid's Tale</title>  
    <author>  
      <first-name>Margaret</first-name>  
      <last-name>Atwood</last-name>  
    </author>  
    <price>19.95</price>  
  </book>  
  <book genre="novel" style="other">  
    <title>The Poisonwood Bible</title>  
    <author>  
      <first-name>Barbara</first-name>  
      <last-name>Kingsolver</last-name>  
    </author>  
    <price>11.99</price>  
  </book>  
  <book genre="novel" style="paperback">  
    <title>The Bean Trees</title>  
    <author>  
      <first-name>Barbara</first-name>  
      <last-name>Kingsolver</last-name>  
    </author>  
    <price>5.99</price>  
  </book>  
</bookstore>  
```  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
