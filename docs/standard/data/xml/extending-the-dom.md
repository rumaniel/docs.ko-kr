---
title: DOM 확장
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: b5489c96-4afd-439a-a25d-fc82eb4a148d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ced76a0bb28a91824676f496b28143a921b987de
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54559500"
---
# <a name="extending-the-dom"></a>DOM 확장

Microsoft .NET Framework에는 XML DOM(문서 개체 모델)을 구현하는 기본 클래스 집합이 포함되어 있습니다. <xref:System.Xml.XmlNode>와 해당 파생 클래스는 XML 문서의 내용 및 구조를 탐색하고, 쿼리하고, 수정할 수 있게 해 주는 메서드 및 속성을 제공합니다.

DOM을 사용하여 메모리에 XML 내용을 로드할 때 만들어지는 노드에는 노드 이름과 노드 형식 등의 정보가 포함됩니다. 그러나 기본 클래스에서 제공하지 않는 특정 노드 정보가 필요한 경우도 있습니다. 예를 들어, 노드의 줄 번호와 위치를 알아야 하는 경우, 기존 DOM 클래스에서 새 클래스를 파생시키고 기능을 추가할 수 있습니다.

새 클래스를 파생시킬 경우 다음과 같은 두 가지 일반 지침이 있습니다.

- <xref:System.Xml.XmlNode> 클래스에서는 파생시키지 않는 것이 좋습니다. 대신, 관련된 노드 형식에 해당하는 클래스에서 클래스를 파생시키는 것이 좋습니다. 예를 들어, 특성 노드에 대한 추가 정보를 반환하려면 <xref:System.Xml.XmlAttribute> 클래스에서 파생시킬 수 있습니다.

- 노드 생성 메서드를 제외한 함수를 재정의할 경우에는 항상 함수의 기본 버전을 호출한 다음 다른 처리를 추가해야 합니다.

## <a name="creating-your-own-node-instances"></a>고유한 노드 인스턴스 만들기

<xref:System.Xml.XmlDocument> 클래스에는 노드 생성 메서드가 포함되어 있습니다. XML 파일을 로드하면 이러한 메서드가 호출되어 노드가 만들어집니다. 문서가 로드될 때 사용자의 노드 인스턴스가 만들어지도록 이러한 메서드를 재정의할 수 있습니다. 예를 들어, <xref:System.Xml.XmlElement> 클래스를 확장했다면 <xref:System.Xml.XmlDocument> 클래스를 상속하고 <xref:System.Xml.XmlDocument.CreateElement%2A> 메서드를 재정의했을 수 있습니다.

다음 예제에서는 <xref:System.Xml.XmlDocument.CreateElement%2A> 클래스의 사용자 구현을 반환하도록 <xref:System.Xml.XmlElement> 메서드를 재정의하는 방법을 보여 줍니다.

```vb
Class LineInfoDocument
    Inherits XmlDocument
        Public Overrides Function CreateElement(prefix As String, localname As String, nsURI As String) As XmlElement
        Dim elem As New LineInfoElement(prefix, localname, nsURI, Me)
        Return elem
    End Function 'CreateElement
End Class 'LineInfoDocument
```

```csharp
class LineInfoDocument : XmlDocument 
{
    public override XmlElement CreateElement(string prefix, string localname, string nsURI) 
    {
        LineInfoElement elem = new LineInfoElement(prefix, localname, nsURI, this);
        return elem;
    }
}
```

## <a name="extending-a-class"></a>클래스 확장

클래스를 확장하려면 기존 DOM 클래스 중 하나에서 클래스를 파생시킵니다. 그런 다음 기본 클래스의 가상 메서드 또는 속성을 재정의하거나 고유한 메서드나 속성을 추가할 수 있습니다.

다음 예제에서는 <xref:System.Xml.XmlElement> 클래스와 <xref:System.Xml.IXmlLineInfo> 인터페이스를 구현하는 새 클래스를 만듭니다. 사용자가 줄 정보를 얻을 수 있도록 추가 메서드와 속성을 정의합니다.

```vb
Class LineInfoElement
   Inherits XmlElement
   Implements IXmlLineInfo
   Private lineNumber As Integer = 0
   Private linePosition As Integer = 0

   Friend Sub New(prefix As String, localname As String, nsURI As String, doc As XmlDocument)
      MyBase.New(prefix, localname, nsURI, doc)
      CType(doc, LineInfoDocument).IncrementElementCount()
   End Sub

   Public Sub SetLineInfo(linenum As Integer, linepos As Integer)
      lineNumber = linenum
      linePosition = linepos
   End Sub

   Public ReadOnly Property LineNumber() As Integer
      Get
         Return lineNumber
      End Get
   End Property

   Public ReadOnly Property LinePosition() As Integer
      Get
         Return linePosition
      End Get
   End Property

   Public Function HasLineInfo() As Boolean
      Return True
   End Function
End Class ' End LineInfoElement class.
```

```csharp
class LineInfoElement : XmlElement, IXmlLineInfo {
   int lineNumber = 0;
   int linePosition = 0;
   internal LineInfoElement( string prefix, string localname, string nsURI, XmlDocument doc ) : base( prefix, localname, nsURI, doc ) {
       ( (LineInfoDocument)doc ).IncrementElementCount();
  }
  public void SetLineInfo( int linenum, int linepos ) {
      lineNumber = linenum;
      linePosition = linepos;
  }
  public int LineNumber {
     get {
       return lineNumber;
     }
  }
  public int LinePosition {
      get {
        return linePosition;
      }
  }
  public bool HasLineInfo() {
    return true;
  }
} // End LineInfoElement class.
```

### <a name="example"></a>예제

다음 예제에서는 XML 문서의 요소 수를 계산합니다.

```vb
Imports System
Imports System.Xml
Imports System.IO

Class LineInfoDocument
   Inherits XmlDocument

   Private elementCount As Integer

   Friend Sub New()
      elementCount = 0
   End Sub

   Public Overrides Function CreateElement(prefix As String, localname As String, nsURI As String) As XmlElement
      Dim elem As New LineInfoElement(prefix, localname, nsURI, Me)
      Return elem
   End Function

   Public Sub IncrementElementCount()
      elementCount += 1
   End Sub

   Public Function GetCount() As Integer
      Return elementCount
   End Function
End Class 'End LineInfoDocument class.

Class LineInfoElement
   Inherits XmlElement

   Friend Sub New(prefix As String, localname As String, nsURI As String, doc As XmlDocument)
      MyBase.New(prefix, localname, nsURI, doc)
      CType(doc, LineInfoDocument).IncrementElementCount()
   End Sub 'New
End Class 'LineInfoElement
 _ 'End LineInfoElement class.

Public Class Test

   Private filename As [String] = "book.xml"

   Public Shared Sub Main()

      Dim doc As New LineInfoDocument()
      doc.Load(filename)
      Console.WriteLine("Number of elements in {0}: {1}", filename, doc.GetCount())
   End Sub
End Class
```

```csharp
using System;
using System.Xml;
using System.IO;

class LineInfoDocument : XmlDocument {

  int elementCount;
  internal LineInfoDocument():base() {
    elementCount = 0;
  }

  public override XmlElement CreateElement( string prefix, string localname, string nsURI) {
    LineInfoElement elem = new LineInfoElement(prefix, localname, nsURI, this );
    return elem;
  }

  public void IncrementElementCount() {
     elementCount++;
  }

  public int GetCount() {
     return elementCount;
  }
} // End LineInfoDocument class.

class LineInfoElement:XmlElement {

    internal LineInfoElement( string prefix, string localname, string nsURI, XmlDocument doc ):base( prefix,localname,nsURI, doc ){
      ((LineInfoDocument)doc).IncrementElementCount();
    }
} // End LineInfoElement class.

public class Test {

  const String filename = "book.xml";
  public static void Main() {

     LineInfoDocument doc =new LineInfoDocument();
     doc.Load(filename);
     Console.WriteLine("Number of elements in {0}: {1}", filename, doc.GetCount());

  }
}
```

#### <a name="input"></a>입력

book.xml

```xml
<!--sample XML fragment-->
<book genre='novel' ISBN='1-861001-57-5' misc='sale-item'>
  <title>The Handmaid's Tale</title>
  <price>14.95</price>
</book>
```

#### <a name="output"></a>출력

```console
Number of elements in book.xml: 3
```

## <a name="node-event-handler"></a>노드 이벤트 처리기

.NET Framework의 DOM 구현에는 XML 문서의 노드가 변경될 때 이벤트를 받아 처리할 수 있는 이벤트 시스템이 포함됩니다. <xref:System.Xml.XmlNodeChangedEventHandler> 및 <xref:System.Xml.XmlNodeChangedEventArgs> 클래스를 사용하면 `NodeChanged`, `NodeChanging`, `NodeInserted`, `NodeInserting`, `NodeRemoved` 및 `NodeRemoving` 이벤트를 캡처할 수 있습니다.

원래의 DOM 클래스와 파생 클래스에서의 이벤트 처리 과정은 완전히 동일합니다.

노드 이벤트 처리에 대한 자세한 내용은 [이벤트](../../../../docs/standard/events/index.md) 및 <xref:System.Xml.XmlNodeChangedEventHandler>를 참조하세요.

## <a name="default-attributes-and-the-createelement-method"></a>기본 특성 및 CreateElement 메서드

파생 클래스에서 <xref:System.Xml.XmlDocument.CreateElement%2A> 메서드를 재정의하면 문서를 편집하면서 새 요소를 만들 때 기본 특성이 추가되지 않습니다. 이것은 편집하는 동안에만 발생하는 문제입니다. <xref:System.Xml.XmlDocument.CreateElement%2A> 메서드는 <xref:System.Xml.XmlDocument>에 기본 특성을 추가하는 기능을 수행하므로 <xref:System.Xml.XmlDocument.CreateElement%2A> 메서드에 이 기능을 수행하는 코드를 추가해야 합니다. 기본 특성을 포함한 <xref:System.Xml.XmlDocument>를 로드하면 해당 문서는 올바르게 처리됩니다. 기본 특성에 대한 자세한 내용은 [DOM에서 요소의 새 특성 만들기](creating-new-attributes-for-elements-in-the-dom.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](xml-document-object-model-dom.md)
