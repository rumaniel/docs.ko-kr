---
title: DOM에서 요소의 새 특성 만들기
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: dd6dc920-b011-418a-b3db-f1580a7d9251
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 870e800220031338557792fa612d4a3101e79f90
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48024573"
---
# <a name="creating-new-attributes-for-elements-in-the-dom"></a>DOM에서 요소의 새 특성 만들기
특성은 노드가 아니라 요소 노드의 속성이며 요소와 연결된 **XmlAttributeCollection**에 포함되어 있으므로 새 특성을 만드는 것은 다른 노드 형식을 만드는 것과 다릅니다. 다음과 같은 여러 가지 방법으로 특성을 만들고 요소를 추가할 수 있습니다.  
  
-   요소 노드를 가져오고 **SetAttribute**를 사용하여 특성을 해당 요소의 특성 컬렉션에 추가합니다.  
  
-   **CreateAttribute** 메서드를 사용하여 **XmlAttribute** 노드를 만들고, 요소 노드를 가져온 다음, **SetAttributeNode**를 사용하여 해당 요소의 특성 컬렉션에 노드를 추가합니다.  
  
 다음 예제는 **SetAttribute** 메서드를 사용하여 요소에 특성을 추가하는 방법을 보여줍니다.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
public class Sample  
  
  public shared sub Main()  
  
  Dim doc as XmlDocument = new XmlDocument()  
  doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" & _  
              "<title>Pride And Prejudice</title>" & _  
              "</book>")  
  Dim root as XmlElement = doc.DocumentElement  
  
  'Add a new attribute.  
  root.SetAttribute("genre", "urn:samples", "novel")  
  
  Console.WriteLine("Display the modified XML...")  
  Console.WriteLine(doc.InnerXml)  
  
  end sub  
end class  
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
    doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" +  
                "<title>Pride And Prejudice</title>" +  
                "</book>");  
    XmlElement root = doc.DocumentElement;  
  
    // Add a new attribute.  
    root.SetAttribute("genre", "urn:samples", "novel");  
  
    Console.WriteLine("Display the modified XML...");  
    Console.WriteLine(doc.InnerXml);  
  }  
```  
  
 다음 예제는 **CreateAttribute** 메서드를 사용하여 새 특성을 만든 후 **SetAttributeNode** 메서드를 사용하여 **book** 요소의 특성 컬렉션에 해당 특성을 추가하는 예를 보여줍니다.  
  
 다음과 같은 XML을 가정합니다.  
  
```xml  
<book genre='novel' ISBN='1-861001-57-5'>  
<title>Pride And Prejudice</title>  
</book>  
```  
  
 새 특성을 만들어 값을 지정합니다.  
  
```vb  
Dim attr As XmlAttribute = doc.CreateAttribute("publisher")  
   attr.Value = "WorldWide Publishing"  
```  
  
```csharp  
XmlAttribute attr = doc.CreateAttribute("publisher");  
attr.Value = "WorldWide Publishing";  
```  
  
 새로 만든 특성을 요소에 추가합니다.  
  
```vb  
doc.DocumentElement.SetAttributeNode(attr)  
```  
  
```csharp  
doc.DocumentElement.SetAttributeNode(attr);  
```  
  
 **출력**  
  
```xml  
<book genre="novel" ISBN="1-861001-57-5" publisher="WorldWide Publishing">  
<title>Pride And Prejudice</title>  
</book>  
```  
  
 전체 코드 샘플은 <xref:System.Xml.XmlDocument.CreateAttribute%2A>에서 찾을 수 있습니다.  
  
 또한 **XmlAttribute** 노드를 만들고 **InsertBefore** 또는 **InsertAfter** 메서드를 사용하여 해당 노드를 컬렉션의 적절한 위치에 배치할 수 있습니다. 동일한 이름의 특성이 이미 특성 컬렉션에 있는 경우 기존 **XmlAttribute** 노드가 컬렉션에서 제거되고 새 **XmlAttribute** 노드가 삽입됩니다. 이는 **SetAttribute** 메서드와 동일한 방식으로 작동합니다. 이러한 메서드는 **InsertBefore** 및 **InsertAfter**를 수행하는 참조 위치로 기존 노드를 사용합니다(매개 변수로). 새 노드의 삽입 위치를 나타내는 참조 노드를 제공하지 않으면 **InsertAfter** 메서드는 기본적으로 컬렉션의 처음에 새 노드를 삽입합니다. 참조 노드가 제공되지 않을 경우 **InsertBefore**의 기본 위치는 컬렉션의 끝입니다.  
  
 특성의 **XmlNamedNodeMap**을 만든 경우 <xref:System.Xml.XmlNamedNodeMap.SetNamedItem%2A>을 사용하여 이름에 따라 특성을 추가할 수 있습니다. 자세한 내용은 [NamedNodeMaps 및 NodeLists의 노드 컬렉션](../../../../docs/standard/data/xml/node-collections-in-namednodemaps-and-nodelists.md)을 참조하세요.  
  
## <a name="default-attributes"></a>기본 특성  
 기본 특성을 포함하도록 선언된 요소를 만들면 새 기본 특성이 XML DOM(문서 개체 모델)에서 해당 기본값과 함께 만들어지고 해당 요소에 추가됩니다. 이때 기본 특성의 자식 노드도 만들어집니다.  
  
## <a name="attribute-child-nodes"></a>특성 자식 노드  
 특성 노드 값은 자신의 자식 노드가 됩니다. 유효한 자식 노드에는 **XmlText** 노드와 **XmlEntityReference** 노드의 두 가지 형식만 있습니다. **FirstChild** 및 **LastChild**와 같은 메서드에서 이러한 형식의 노드를 자식 노드로 처리한다는 점에서 이러한 형식의 노드는 자식 노드입니다. 자식 노드가 있는 특성의 이와 같은 차이점은 특성이나 특성 자식 노드를 제거하려는 경우에 중요합니다. 자세한 내용은 [DOM의 요소 노드에서 특성 제거](../../../../docs/standard/data/xml/removing-attributes-from-an-element-node-in-the-dom.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
