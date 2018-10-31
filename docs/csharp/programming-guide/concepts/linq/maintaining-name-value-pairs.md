---
title: 이름-값 쌍 유지 관리(C#)
ms.date: 07/20/2015
ms.assetid: 7b04b0f1-af64-42eb-8737-83f8861b5915
ms.openlocfilehash: 28c01ce17881ffe7e8fcc35e2c23dec85d50955d
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48841218"
---
# <a name="maintaining-namevalue-pairs-c"></a>이름/값 쌍 유지 관리(C#)
대부분의 응용 프로그램은 이름/값 쌍으로 가장 잘 유지되는 정보를 유지 관리해야 합니다. 이 정보는 구성 정보이거나 전역 설정일 수 있습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에는 이름/값 쌍의 집합을 쉽게 유지하는 데 사용할 수 있는 몇몇 메서드가 포함되어 있습니다. 정보를 특성이나 자식 요소의 집합으로 유지할 수 있습니다.  
  
 정보를 특성으로 유지하는 경우와 자식 요소로 유지하는 경우의 차이점은 특성에 제약 조건이 있다는 것입니다. 즉, 한 요소에 특정 이름을 가진 특성이 하나만 있을 수 있습니다. 이 제한은 자식 요소에는 적용되지 않습니다.  
  
## <a name="setattributevalue-and-setelementvalue"></a>SetAttributeValue 및 SetElementValue  
 이름/값 쌍 유지를 용이하게 하는 두 메서드는 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> 및 <xref:System.Xml.Linq.XElement.SetElementValue%2A>입니다. 이러한 두 메서드의 의미는 유사합니다.  
  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>는 요소의 특성을 추가, 수정 또는 제거할 수 있습니다.  
  
-   존재하지 않는 특성의 이름을 사용하여 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>를 호출하면 이 메서드는 새 특성을 만들어 지정된 요소에 추가합니다.  
  
-   기존 특성의 이름과 지정된 내용을 사용하여 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>를 호출하면 특성의 내용이 지정된 내용으로 바뀝니다.  
  
-   기존 특성의 이름을 사용하여 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>를 호출하고 내용에 null을 지정하면 특성이 부모에서 제거됩니다.  
  
 <xref:System.Xml.Linq.XElement.SetElementValue%2A>는 요소의 자식 요소를 추가, 수정 또는 제거할 수 있습니다.  
  
-   존재하지 않는 자식 요소의 이름을 사용하여 <xref:System.Xml.Linq.XElement.SetElementValue%2A>를 호출하면 이 메서드는 새 요소를 만들어 지정된 요소에 추가합니다.  
  
-   기존 요소의 이름과 지정된 내용을 사용하여 <xref:System.Xml.Linq.XElement.SetElementValue%2A>를 호출하면 요소의 내용이 지정된 내용으로 바뀝니다.  
  
-   기존 요소의 이름을 사용하여 <xref:System.Xml.Linq.XElement.SetElementValue%2A>를 호출하고 내용에 null을 지정하면 요소가 부모에서 제거됩니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 특성 없이 요소를 만든 다음 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> 메서드를 사용하여 이름/값 쌍의 목록을 만들고 유지 관리합니다.  
  
```csharp  
// Create an element with no content.  
XElement root = new XElement("Root");  
  
// Add a number of name/value pairs as attributes.  
root.SetAttributeValue("Top", 22);  
root.SetAttributeValue("Left", 20);  
root.SetAttributeValue("Bottom", 122);  
root.SetAttributeValue("Right", 300);  
root.SetAttributeValue("DefaultColor", "Color.Red");  
Console.WriteLine(root);  
  
// Replace the value of Top.  
root.SetAttributeValue("Top", 10);  
Console.WriteLine(root);  
  
// Remove DefaultColor.  
root.SetAttributeValue("DefaultColor", null);  
Console.WriteLine(root);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root Top="22" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" />  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 자식 요소 없이 요소를 만든 다음 <xref:System.Xml.Linq.XElement.SetElementValue%2A> 메서드를 사용하여 이름/값 쌍의 목록을 만들고 유지 관리합니다.  
  
```csharp  
// Create an element with no content.  
XElement root = new XElement("Root");  
  
// Add a number of name/value pairs as elements.  
root.SetElementValue("Top", 22);  
root.SetElementValue("Left", 20);  
root.SetElementValue("Bottom", 122);  
root.SetElementValue("Right", 300);  
root.SetElementValue("DefaultColor", "Color.Red");  
Console.WriteLine(root);  
Console.WriteLine("----");  
  
// Replace the value of Top.  
root.SetElementValue("Top", 10);  
Console.WriteLine(root);  
Console.WriteLine("----");  
  
// Remove DefaultColor.  
root.SetElementValue("DefaultColor", null);  
Console.WriteLine(root);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <Top>22</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
</Root>  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
- <xref:System.Xml.Linq.XElement.SetElementValue%2A>  
- [XML 트리 수정(LINQ to XML)(C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
