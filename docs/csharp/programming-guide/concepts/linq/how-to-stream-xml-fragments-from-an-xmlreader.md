---
title: '방법: XmlReader에서 XML 조각 스트리밍(C#)'
ms.date: 07/20/2015
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
ms.openlocfilehash: e5aeb5111931ff6a35a3b7806abc24e0fbbf9621
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253287"
---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-c"></a>방법: XmlReader에서 XML 조각 스트리밍(C#)
큰 XML 파일을 처리해야 하는 경우 전체 XML 트리를 메모리에 로드하는 것이 가능하지 않을 수 있습니다. 이 항목에서는 <xref:System.Xml.XmlReader>를 사용하여 조각을 스트림하는 방법을 보여 줍니다.  
  
 <xref:System.Xml.XmlReader>를 사용하여 <xref:System.Xml.Linq.XElement> 개체를 읽는 가장 효과적인 방법 중 하나는 사용자 지정 축 메서드를 직접 작성하는 것입니다. 일반적으로 축 메서드는 이 항목의 예제에 나와 있는 대로 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>과 같은 컬렉션을 반환합니다. 사용자 지정 축 메서드에서는 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 메서드를 호출하여 XML 조각을 만든 후 `yield return`을 사용하여 컬렉션을 반환합니다. 이것은 사용자 지정 축 메서드에 지연된 실행 의미를 제공합니다.  
  
 <xref:System.Xml.XmlReader> 개체에서 XML 트리를 만드는 경우 <xref:System.Xml.XmlReader>가 요소에 배치되어야 합니다. <xref:System.Xml.Linq.XNode.ReadFrom%2A> 메서드는 요소의 닫는 태그를 읽을 때까지 반환되지 않습니다.  
  
 부분 트리를 만들려는 경우 <xref:System.Xml.XmlReader>를 인스턴스화하고 <xref:System.Xml.Linq.XElement> 트리로 변환할 노드에 판독기를 배치한 다음 <xref:System.Xml.Linq.XElement> 개체를 만들 수 있습니다.  
  
 항목 [방법: 헤더 정보에 액세스하여 XML 조각 스트리밍(C#)](./how-to-stream-xml-fragments-with-access-to-header-information.md)에는 더 복잡한 문서를 스트림하는 방법에 대한 정보와 예제가 포함되어 있습니다.  
  
 항목 [방법: 큰 XML 문서의 변환 스트리밍 수행(C#)](./how-to-perform-streaming-transform-of-large-xml-documents.md)에는 LINQ to XML을 사용하여 작은 메모리 사용 공간을 유지하면서 매우 큰 XML 문서를 변환하는 예제가 포함되어 있습니다.  
  
## <a name="example"></a>예  
 이 예제에서는 사용자 지정 축 메서드를 만듭니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 사용하여 이 메서드를 쿼리할 수 있습니다. 사용자 지정 축 메서드 `StreamRootChildDoc`는 반복되는 `Child` 요소가 있는 문서를 읽도록 특정하게 디자인된 메서드입니다.  
  
```csharp  
static IEnumerable<XElement> StreamRootChildDoc(StringReader stringReader)  
{  
    using (XmlReader reader = XmlReader.Create(stringReader))  
    {  
        reader.MoveToContent();  
        // Parse the file and display each of the nodes.  
        while (reader.Read())  
        {  
            switch (reader.NodeType)  
            {  
                case XmlNodeType.Element:  
                    if (reader.Name == "Child") {  
                        XElement el = XElement.ReadFrom(reader) as XElement;  
                        if (el != null)  
                            yield return el;  
                    }  
                    break;  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    string markup = @"<Root>  
      <Child Key=""01"">  
        <GrandChild>aaa</GrandChild>  
      </Child>  
      <Child Key=""02"">  
        <GrandChild>bbb</GrandChild>  
      </Child>  
      <Child Key=""03"">  
        <GrandChild>ccc</GrandChild>  
      </Child>  
    </Root>";  
  
    IEnumerable<string> grandChildData =  
        from el in StreamRootChildDoc(new StringReader(markup))  
        where (int)el.Attribute("Key") > 1  
        select (string)el.Element("GrandChild");  
  
    foreach (string str in grandChildData) {  
        Console.WriteLine(str);  
    }  
}  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
bbb  
ccc  
```  
  
 이 예제의 소스 문서는 매우 작습니다. `Child` 요소가 수백만 있더라도 이 예제에서는 여전히 작은 메모리 공간만 사용할 것입니다.  
  