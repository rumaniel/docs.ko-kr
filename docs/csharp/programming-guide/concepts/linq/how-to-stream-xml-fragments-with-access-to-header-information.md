---
title: '방법: 헤더 정보에 액세스하여 XML 조각 스트리밍(C#)'
ms.date: 07/20/2015
ms.assetid: 7f242770-b0c7-418d-894b-643215e1f8aa
ms.openlocfilehash: d40fa5b7ae60836c0fd947d36f88765eafc60334
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592343"
---
# <a name="how-to-stream-xml-fragments-with-access-to-header-information-c"></a>방법: 헤더 정보에 액세스하여 XML 조각 스트리밍(C#)
예상할 수 없는 큰 크기의 XML 파일을 읽고 애플리케이션의 메모리 사용 공간이 예상 가능하도록 애플리케이션을 작성해야 하는 경우가 있습니다. XML 트리를 큰 XML 파일로 채우려는 경우 파일 크기에 비례하여 메모리가 사용되므로 메모리 사용량이 지나치게 증가하게 됩니다. 따라서 스트리밍 기법을 대신 사용해야 합니다.  
  
 한 가지 방법은 <xref:System.Xml.XmlReader>를 사용하여 애플리케이션을 작성하는 것입니다. 그러나 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]를 사용하여 XML 트리를 쿼리할 수도 있습니다. 이 경우에는 사용자 지정 축 메서드를 직접 작성할 수 있습니다. 자세한 내용은 [방법: LINQ to XML 축 메서드 작성(C#)](./how-to-write-a-linq-to-xml-axis-method.md)을 참조하세요.  
  
 축 메서드를 직접 작성하려면 <xref:System.Xml.XmlReader>를 사용하여 관심이 있는 노드 중 하나에 도달할 때까지 노드를 읽는 작은 메서드를 작성해야 합니다. 이 메서드는 <xref:System.Xml.Linq.XNode.ReadFrom%2A>에서 읽고 XML 조각을 인스턴스화하는 <xref:System.Xml.XmlReader>을 호출한 후 `yield return`을 통해 각 조각을 사용자 지정 축 메서드를 열거하는 메서드에 생성합니다. 그런 다음 사용자 지정 축 메서드에 대한 LINQ 쿼리를 작성할 수 있습니다.  
  
 스트리밍 기법은 소스 문서를 한 번만 처리해야 하고 문서 순서의 요소를 처리할 수 있는 경우에 가장 효과적으로 적용됩니다. <xref:System.Linq.Enumerable.OrderBy%2A>와 같은 특정 표준 쿼리 연산자는 자신의 소스를 반복하고 모든 데이터를 수집하여 정렬한 다음 시퀀스의 첫 번째 항목을 최종적으로 생성합니다. 첫 번째 항목을 생성하기 전에 소스를 유형화하는 쿼리 연산자를 사용하는 경우 작은 메모리 사용 공간이 유지되지 않습니다.  
  
## <a name="example"></a>예  
 좀 더 흥미로운 문제가 발생하는 경우도 있습니다. 다음 XML 문서에서 사용자 지정 축 메서드의 소비자는 각 항목을 소유하는 고객의 이름도 알아야 합니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
 이 예제에서 사용하는 방법은 이 헤더 정보를 확인하고 저장한 다음 헤더 정보와 열거하고 있는 세부 정보를 모두 포함하는 작은 XML 트리를 빌드하는 것입니다. 축 메서드는 이 새로운 작은 XML 트리를 생성합니다. 이 경우 쿼리는 세부 정보뿐만 아니라 헤더 정보에도 액세스할 수 있습니다.  
  
 이 방법에서는 작은 메모리 공간이 사용됩니다. 각 세부 XML 조각이 생성될 때 이전 조각에 대한 참조는 유지되지 않으며 가비지 수집에 사용할 수 있습니다. 이 기법을 사용하면 힙에 수명이 짧은 개체가 많이 만들어집니다.  
  
 다음 예제에서는 URI로 지정된 파일에서 XML 조각을 스트림하는 사용자 지정 축 메서드를 구현하고 사용하는 방법을 보여 줍니다. 이 사용자 지정 축은 문서에 `Customer`, `Name` 및 `Item` 요소가 있고 이러한 요소가 위에 있는 `Source.xml` 문서의 경우와 마찬가지로 정렬되어 있다고 가정하고 작성된 것입니다. 이것은 매우 단순화된 구현입니다. 더욱 강력한 구현은 잘못된 문서의 구문을 분석할 준비가 되어 있습니다.  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null) {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    XElement xmlTree = new XElement("Root",  
        from el in StreamCustomerItem("Source.xml")  
        where (int)el.Element("Key") >= 3 && (int)el.Element("Key") <= 7  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        )  
    );  
    Console.WriteLine(xmlTree);  
}  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
</Root>  
```  
  