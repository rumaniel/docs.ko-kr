---
title: DOM에서 특성 액세스
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: ce2df341-a1a4-4e97-8e1b-cd45b8e3e71e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 272c224c8a1c5061392856685f374237f8a10579
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956869"
---
# <a name="accessing-attributes-in-the-dom"></a>DOM에서 특성 액세스

특성은 요소의 자식 항목이 아닌, 요소의 속성입니다. 이러한 구분은 XML DOM(문서 개체 모델)의 형제, 부모 및 자식 노드를 탐색하는 데 사용되는 메서드로 인하여 중요하게 작용합니다. 예를 들어 **PreviousSibling** 및 **NextSibling** 메서드는 요소와 특성 사이 또는 특성 간을 탐색하는 데 사용되지 않습니다. 대신, 특성은 요소의 속성으로서 요소에 속하며 **parentNode** 속성이 아닌, **OwnerElement** 속성과 고유한 탐색 메서드를 갖습니다.

현재 노드가 요소이면 **HasAttribute** 메서드를 사용하여 해당 요소와 연관된 특성이 있는지 확인합니다. 요소에 특성이 있다고 확인되면 특성에 액세스하기 위한 여러 메서드가 있는 것입니다. 요소에서 단일 특성을 검색하려면 **XmlElement**의 **GetAttribute** 및 **GetAttributeNode** 메서드를 사용하거나 모든 특성을 하나의 컬렉션으로 가져올 수 있습니다. 컬렉션에 대한 반복 작업이 필요한 경우 컬렉션을 가져오는 것이 유용합니다. 요소의 모든 특성이 필요하다면 해당 요소의 **Attributes** 속성을 사용하여 모든 특성을 하나의 컬렉션으로 가져옵니다.

## <a name="retrieving-all-attributes-into-a-collection"></a>모든 특성을 컬렉션으로 가져오기

요소 노드의 모든 특성을 한 컬렉션으로 가져오려면 **XmlElement.Attributes** 속성을 호출합니다. 그러면 요소의 모든 특성을 포함하는 **XmlAttributeCollection**을 가져옵니다. **XmlAttributeCollection** 클래스는 **XmlNamedNode** 맵에서 상속됩니다. 따라서 해당 컬렉션에서 사용할 수 있는 메서드 및 속성에는 **ItemOf** 속성이나 **Append** 메서드와 같이 **XmlAttributeCollection** 클래스에 고유한 메서드 및 속성 외에도 명명된 노드 맵에서 사용할 수 있는 메서드와 속성이 포함됩니다. 특성 컬렉션의 각 항목은 **XmlAttribute** 노드를 나타냅니다. 요소의 특성 수를 알아보려면 **XmlAttributeCollection**을 가져오고 **Count** 속성을 사용하여 해당 컬렉션의 **XmlAttribute** 노드 수를 확인합니다.

다음 코드 예제에서는 특성 컬렉션을 검색하는 방법과 반복 인덱스에 **Count** 메서드를 사용하여 해당 특성 컬렉션 전체를 반복하는 예를 보여줍니다. 그런 다음 컬렉션에서 단일 특성을 검색한 후 해당 값을 표시하는 방법을 보여 줍니다.

```vb
Imports System
Imports System.IO
Imports System.Xml

Public Class Sample

    Public Shared Sub Main()

        Dim doc As XmlDocument = New XmlDocument()
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" & _
               "<title>The Handmaid's Tale</title>" & _
               "<price>14.95</price>" & _
               "</book>")

        ' Move to an element.
        Dim myElement As XmlElement = doc.DocumentElement

        ' Create an attribute collection from the element.
        Dim attrColl As XmlAttributeCollection = myElement.Attributes

        ' Show the collection by iterating over it.
        Console.WriteLine("Display all the attributes in the collection...")
        Dim i As Integer
        For i = 0 To attrColl.Count - 1
            Console.Write("{0} = ", attrColl.ItemOf(i).Name)
            Console.Write("{0}", attrColl.ItemOf(i).Value)
            Console.WriteLine()
        Next

        ' Retrieve a single attribute from the collection; specifically, the
        ' attribute with the name "misc".
        Dim attr As XmlAttribute = attrColl("misc")

        ' Retrieve the value from that attribute.
        Dim miscValue As String = attr.InnerXml

        Console.WriteLine("Display the attribute information.")
        Console.WriteLine(miscValue)

    End Sub
End Class
```

```csharp
using System;
using System.IO;
using System.Xml;

public class Sample
{

    public static void Main()
    {
        XmlDocument doc = new XmlDocument();
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" +
                      "<title>The Handmaid's Tale</title>" +
                      "<price>14.95</price>" +
                      "</book>");

        // Move to an element.
        XmlElement myElement = doc.DocumentElement;

        // Create an attribute collection from the element.
        XmlAttributeCollection attrColl = myElement.Attributes;

        // Show the collection by iterating over it.
        Console.WriteLine("Display all the attributes in the collection...");
        for (int i = 0; i < attrColl.Count; i++)
        {
            Console.Write("{0} = ", attrColl[i].Name);
            Console.Write("{0}", attrColl[i].Value);
            Console.WriteLine();
        }

        // Retrieve a single attribute from the collection; specifically, the
        // attribute with the name "misc".
        XmlAttribute attr = attrColl["misc"];

        // Retrieve the value from that attribute.
        String miscValue = attr.InnerXml;

        Console.WriteLine("Display the attribute information.");
        Console.WriteLine(miscValue);

    }
}
```

이 예제의 결과는 다음과 같습니다.

**출력**

컬렉션의 모든 특성을 표시합니다.

```console
genre = novel
ISBN = 1-861001-57-5
misc = sale item
Display the attribute information.
sale item
```

특성 컬렉션의 정보는 이름이나 인덱스 번호로 검색할 수 있습니다. 위의 예제는 이름으로 데이터를 검색하는 방법을 보여 줍니다. 다음 예제는 인덱스 번호로 데이터를 검색하는 방법을 보여 줍니다.

**XmlAttributeCollection**은 이름이나 인덱스를 통해 반복될 수 있는 컬렉션이므로, 이 예제에서는 0부터 시작하는 인덱스를 사용한 후 다음의 **baseuri.xml** 파일을 입력으로 사용하여 컬렉션에서 첫 번째 특성을 선택하는 예를 보여줍니다.

### <a name="input"></a>입력

```xml
<!-- XML fragment -->
<book genre="novel">
  <title>Pride And Prejudice</title>
</book>
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.IO
Imports System.Xml

Public Class Sample

    Public Shared Sub Main()
        ' Create the XmlDocument.
        Dim doc As New XmlDocument()
        doc.Load("http://localhost/baseuri.xml")

        ' Display information on the attribute node. The value
        ' returned for BaseURI is 'http://localhost/baseuri.xml'.
        Dim attr As XmlAttribute = doc.DocumentElement.Attributes(0)
        Console.WriteLine("Name of the attribute:  {0}", attr.Name)
        Console.WriteLine("Base URI of the attribute:  {0}", attr.BaseURI)
        Console.WriteLine("The value of the attribute:  {0}", attr.InnerText)
    End Sub 'Main
End Class 'Sample
```

```csharp
using System;
using System.IO;
using System.Xml;

public class Sample
{
  public static void Main()
  {
    // Create the XmlDocument.
    XmlDocument doc = new XmlDocument();

    doc.Load("http://localhost/baseuri.xml");

    // Display information on the attribute node. The value
    // returned for BaseURI is 'http://localhost/baseuri.xml'.
    XmlAttribute attr = doc.DocumentElement.Attributes[0];
    Console.WriteLine("Name of the attribute:  {0}", attr.Name);
    Console.WriteLine("Base URI of the attribute:  {0}", attr.BaseURI);
    Console.WriteLine("The value of the attribute:  {0}", attr.InnerText);
  }
}
```

## <a name="retrieving-an-individual-attribute-node"></a>개별 특성 노드 검색

요소에서 단일 특성 노드를 검색하려면 <xref:System.Xml.XmlElement.GetAttributeNode%2A?displayProperty=nameWithType> 메서드를 사용합니다. 이 메서드는 **XmlAttribute** 형식의 개체를 반환합니다. **XmlAttribute**가 있는 경우 <xref:System.Xml.XmlAttribute?displayProperty=nameWithType> 클래스에서 사용할 수 있는 모든 메서드 및 속성은 **OwnerElement** 찾기 등과 같이 해당 개체에서 사용할 수 있습니다.

```vb
Imports System
Imports System.IO
Imports System.Xml

Public Class Sample

    Public Shared Sub Main()

        Dim doc As XmlDocument = New XmlDocument()
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" & _
               "<title>The Handmaid's Tale</title>" & _
               "<price>14.95</price>" & _
               "</book>")

        ' Move to an element.
        Dim root As XmlElement
        root = doc.DocumentElement

        ' Get an attribute.
        Dim attr As XmlAttribute
        attr = root.GetAttributeNode("ISBN")

        ' Display the value of the attribute.
        Dim attrValue As String
        attrValue = attr.InnerXml
        Console.WriteLine(attrValue)

    End Sub
End Class
```

```csharp
using System;
using System.IO;
using System.Xml;

 public class Sample
 {
      public static void Main()
      {
    XmlDocument doc = new XmlDocument();
     doc.LoadXml("<book genre='novel' ISBN='1-861003-78' misc='sale item'>" +
                   "<title>The Handmaid's Tale</title>" +
                   "<price>14.95</price>" +
                   "</book>");

    // Move to an element.
     XmlElement root = doc.DocumentElement;

    // Get an attribute.
     XmlAttribute attr = root.GetAttributeNode("ISBN");

    // Display the value of the attribute.
     String attrValue = attr.InnerXml;
     Console.WriteLine(attrValue);

    }
}
```

또한 단일 특성 노드가 특성 컬렉션에서 검색되는 앞의 예제와 같이 이 작업을 수행할 수도 있습니다. 다음 코드 예제에서는 하나의 코드 줄을 작성하여 **DocumentElement** 속성이라고도 하는 XML 문서 트리의 루트에서 인덱스 번호를 기준으로 단일 특성을 검색하는 방법을 보여줍니다.

```csharp
XmlAttribute attr = doc.DocumentElement.Attributes[0];
```

## <a name="see-also"></a>참조

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
