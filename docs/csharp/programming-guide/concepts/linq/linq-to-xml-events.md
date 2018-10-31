---
title: LINQ to XML 이벤트(C#)
ms.date: 07/20/2015
ms.assetid: ce7de951-cba7-4870-9962-733eb01cd680
ms.openlocfilehash: 6308d81eac830e11b6d58f8e460dfa377663cd21
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49453309"
---
# <a name="linq-to-xml-events-c"></a>LINQ to XML 이벤트(C#)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 이벤트를 통해 XML 트리가 변경될 때 알림을 받을 수 있습니다.  
  
 <xref:System.Xml.Linq.XObject>의 인스턴스에 이벤트를 추가할 수 있습니다. 이벤트 처리기는 이 <xref:System.Xml.Linq.XObject>와 해당 하위 항목의 수정에 대한 이벤트를 받습니다. 예를 들어, 이벤트 처리기를 트리의 루트에 추가하고 해당 이벤트 처리기에서 트리의 모든 수정을 처리할 수 있습니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 이벤트의 예제는 <xref:System.Xml.Linq.XObject.Changing> 및 <xref:System.Xml.Linq.XObject.Changed>를 참조하세요.  
  
## <a name="types-and-events"></a>형식 및 이벤트  
 이벤트 작업을 할 때 다음 형식을 사용할 수 있습니다.  
  
|형식|설명|  
|----------|-----------------|  
|<xref:System.Xml.Linq.XObjectChange>|<xref:System.Xml.Linq.XObject>에 대한 이벤트가 발생할 때 이벤트 형식을 지정합니다.|  
|<xref:System.Xml.Linq.XObjectChangeEventArgs>|<xref:System.Xml.Linq.XObject.Changing> 및 <xref:System.Xml.Linq.XObject.Changed> 이벤트에 대한 데이터를 제공합니다.|  
  
 다음 이벤트는 XML 트리를 수정할 때 발생합니다.  
  
|이벤트(event)|설명|  
|-----------|-----------------|  
|<xref:System.Xml.Linq.XObject.Changing>|이 <xref:System.Xml.Linq.XObject> 또는 해당 하위 항목이 변경되기 직전에 발생합니다.|  
|<xref:System.Xml.Linq.XObject.Changed>|<xref:System.Xml.Linq.XObject>가 변경되거나 해당 하위 항목이 변경될 때 발생합니다.|  
  
## <a name="example"></a>예  
  
### <a name="description"></a>설명  
 XML 트리에 특정 집계 정보를 유지 관리하려는 경우 이벤트가 유용합니다. 예를 들어, 청구서의 개별 품목에 대한 합계인 청구서 총계를 유지 관리하려고 할 수 있습니다. 이 예제에서는 이벤트를 사용하여 복합 요소 `Items` 아래의 모든 자식 요소에 대한 총계를 유지 관리합니다.  
  
### <a name="code"></a>코드  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Total", "0"),  
    new XElement("Items")  
);  
XElement total = root.Element("Total");  
XElement items = root.Element("Items");  
items.Changed += (object sender, XObjectChangeEventArgs cea) =>  
{  
    switch (cea.ObjectChange)  
    {  
        case XObjectChange.Add:  
            if (sender is XElement)  
                total.Value = ((int)total + (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total + (int)((XText)sender).Parent).ToString();  
            break;  
        case XObjectChange.Remove:  
            if (sender is XElement)  
                total.Value = ((int)total - (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total - Int32.Parse(((XText)sender).Value)).ToString();  
            break;  
    }  
    Console.WriteLine("Changed {0} {1}",  
      sender.GetType().ToString(), cea.ObjectChange.ToString());  
};  
items.SetElementValue("Item1", 25);  
items.SetElementValue("Item2", 50);  
items.SetElementValue("Item2", 75);  
items.SetElementValue("Item3", 133);  
items.SetElementValue("Item1", null);  
items.SetElementValue("Item4", 100);  
Console.WriteLine("Total:{0}", (int)total);  
Console.WriteLine(root);  
```  
  
### <a name="comments"></a>설명  
 이 코드의 결과는 다음과 같습니다.  
  
```  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XText Remove  
Changed System.Xml.Linq.XText Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Remove  
Changed System.Xml.Linq.XElement Add  
Total:308  
<Root>  
  <Total>308</Total>  
  <Items>  
    <Item2>75</Item2>  
    <Item3>133</Item3>  
    <Item4>100</Item4>  
  </Items>  
</Root>  
```  
  
## <a name="see-also"></a>참고 항목

- [고급 LINQ to XML 프로그래밍(C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
