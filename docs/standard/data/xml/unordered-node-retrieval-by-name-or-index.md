---
title: 이름 또는 인덱스별로 정렬되지 않은 노드 검색
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 2038a90b-92af-4a0a-baaa-08e688d95194
author: mairaw
ms.author: mairaw
ms.openlocfilehash: da1c9f25052bb2354b435cd28b7ff55d4a754ed1
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48584002"
---
# <a name="unordered-node-retrieval-by-name-or-index"></a>이름 또는 인덱스별로 정렬되지 않은 노드 검색
**XmlNamedNodeMap**은 W3C(World Wide Web 컨소시엄) 사양에서 NamedNodeMap으로 설명되며 이름이나 인덱스를 사용하여 노드를 참조할 수 있는 정렬되지 않은 노드 집합 처리에 필수적입니다. **XmlNamedNodeMap**에 액세스할 수 있는 유일한 방법은 메서드나 속성을 통해 **XmlNamedNodeMap**을 반환하는 경우입니다. 다음과 같은 세 가지 메서드나 속성이 **XmlNamedNodeMap**을 반환합니다.  
  
-   XmlElement.Attributes  
  
-   XmlDocumentType.Entities  
  
-   XmlDocumentType.Notations  
  
 예를 들어, **XmlDocumentType.Entities** 속성은 문서 형식 선언에 선언된 **XmlEntity** 노드의 컬렉션을 가져옵니다. 이 컬렉션은 **XmlNamedNodeMap**으로 반환되고 **Count** 속성을 사용하여 컬렉션을 반복하고 엔터티 정보를 표시할 수 있습니다. **XmlNamedNodeMap**을 반복하는 예를 보려면 <xref:System.Xml.XmlDocumentType.Entities%2A>를 참조하세요.  
  
 **XmlAttributeCollection**은 **XmlNamedNodeMap**에서 파생되며, 표기법 및 엔터티는 읽기 전용이지만 특성의 경우에는 수정할 수 있습니다. 특성에 대해 **XmlNamedNodeMap**을 사용하면 XML 이름을 기준으로 특성에 대한 노드를 가져올 수 있습니다. 이렇게 하면 요소 노드에서 특성 컬렉션을 손쉽게 처리할 수 있습니다. 이것은 **IEnumerable** 인터페이스를 구현하지만 문자열 대신 인덱스 접근자를 사용하는 **XmlNodeList**와 반대라고 할 수 있습니다. **RemoveNamedItem** 및 **SetNamedItem** 메서드는 **XmlAttributeCollection**에 대해서만 사용할 수 있습니다. **AttributeCollection** 또는 **XmlNamedNodeMap** 구현을 통해 특성 컬렉션에서 추가하거나 제거하면 요소의 특성 컬렉션이 수정됩니다. 다음 코드 예제에서는 특성을 이동하고 새 특성을 만드는 방법을 보여 줍니다.  
  
```vb  
Imports System  
Imports System.Xml  
  
Class test  
  
    Public Shared Sub Main()  
        Dim doc As New XmlDocument()  
        doc.LoadXml("<root> <child1 attr1='val1' attr2='val2'> text1 </child1> <child2 attr3='val3'> text2 </child2> </root> ")  
  
        ' Get the attributes of node "child2 "  
        Dim ac As XmlAttributeCollection = doc.DocumentElement.ChildNodes(1).Attributes  
  
        ' Print out the number of attributes and their names.  
        Console.WriteLine(("Number of Attributes: " + ac.Count))  
        Dim i As Integer  
        For i = 0 To ac.Count - 1  
            Console.WriteLine((i + 1 + ".  Attribute Name: '" + ac(i).Name + "'  Attribute Value:  '" + ac(i).Value + "'"))  
        Next i  
        ' Get the 'attr1' from child1.  
        Dim attr As XmlAttribute = doc.DocumentElement.ChildNodes(0).Attributes(0)  
  
        ' Add this attribute to the attributecollection "ac".  
        ac.SetNamedItem(attr)  
  
        ''attr1' will be removed from 'child1' and added to 'child2'.  
        ' Print out the number of attributes and their names.  
        Console.WriteLine(("Number of Attributes: " + ac.Count))  
  
        For i = 0 To ac.Count - 1  
            Console.WriteLine((i + 1 + ".  Attribute Name: '" + ac(i).Name + "'  Attribute Value:  '" + ac(i).Value + "'"))  
        Next i  
        ' Create a new attribute and add to the collection.  
        Dim attr2 As XmlAttribute = doc.CreateAttribute("attr4")  
        attr2.Value = "val4"  
        ac.SetNamedItem(attr2)  
  
        ' Print out the number of attributes and their names.  
        Console.WriteLine(("Number of Attributes: " + ac.Count))  
  
        For i = 0 To ac.Count - 1  
            Console.WriteLine((i + 1 + ".  Attribute Name: '" + ac(i).Name + "'  Attribute Value:  '" + ac(i).Value + "'"))  
        Next i  
    End Sub 'Main  
End Class 'test  
```  
  
```csharp  
using System;  
using System.Xml;  
class test {  
    public static void Main() {  
        XmlDocument doc = new XmlDocument();  
        doc.LoadXml( "<root> <child1 attr1='val1' attr2='val2'> text1 </child1> <child2 attr3='val3'> text2 </child2> </root> " );  
  
        // Get the attributes of node "child2"  
        XmlAttributeCollection ac = doc.DocumentElement.ChildNodes[1].Attributes;  
  
        // Print out the number of attributes and their names.  
        Console.WriteLine( "Number of Attributes: "+ac.Count );  
        for( int i = 0; i < ac.Count; i++ )  
            Console.WriteLine( (i+1) + ".  Attribute Name: '" +ac[i].Name+ "'  Attribute Value:  '"+ ac[i].Value +"'" );   
  
        // Get the 'attr1' from child1.  
        XmlAttribute attr = doc.DocumentElement.ChildNodes[0].Attributes[0];  
  
        // Add this attribute to the attributecollection "ac".  
        ac.SetNamedItem( attr );  
  
        // 'attr1' will be removed from 'child1' and added to 'child2'.  
        // Print out the number of attributes and their names.  
        Console.WriteLine( "Number of Attributes: "+ac.Count );          
        for( int i = 0; i < ac.Count; i++ )  
            Console.WriteLine( (i+1) + ".  Attribute Name: '" +ac[i].Name+ "'  Attribute Value:  '"+ ac[i].Value +"'" );   
  
        // Create a new attribute and add to the collection.  
        XmlAttribute attr2 = doc.CreateAttribute( "attr4" );  
        attr2.Value = "val4";  
        ac.SetNamedItem( attr2 );  
  
        // Print out the number of attributes and their names.  
        Console.WriteLine( "Number of Attributes: "+ac.Count );          
        for( int i = 0; i < ac.Count; i++ )  
            Console.WriteLine( (i+1) + ".  Attribute Name: '" +ac[i].Name+ "'  Attribute Value:  '"+ ac[i].Value +"'" );           
  
    }  
}  
```  
  
 **AttributeCollection**에서 특성을 제거하는 추가 코드 예제를 보려면 [XmlNamedNodeMap.RemoveNamedItem 메서드](Overload:System.Xml.XmlNamedNodeMap.RemoveNamedItem)를 참조하세요. 메서드 및 속성에 대한 자세한 내용은 [XmlNamedNodeMap 멤버](AllMembers.T:System.Xml.XmlNamedNodeMap)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
