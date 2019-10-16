---
title: LINQ to XML 축 개요(C#)
ms.date: 07/20/2015
ms.assetid: 516792fb-461d-40a8-8a50-9993a51258fc
ms.openlocfilehash: b775a37869f0c8baa7d482475e301347cb77c538
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591930"
---
# <a name="linq-to-xml-axes-overview-c"></a>LINQ to XML 축 개요(C#)
XML 트리를 만들거나 XML 문서를 XML 트리에 로드한 후 XML 트리를 쿼리하여 요소와 특성을 찾고 해당 값을 검색할 수 있습니다. *축 메서드*(*축*)를 통해 컬렉션을 검색합니다. 일부 축은 <xref:System.Xml.Linq.XElement> 컬렉션을 반환하는 <xref:System.Xml.Linq.XDocument> 및 <xref:System.Collections.Generic.IEnumerable%601> 클래스의 메서드이고, 일부 축은 <xref:System.Xml.Linq.Extensions> 클래스의 확장 메서드입니다. 확장명 메서드로 구현되는 축은 컬렉션에 대해 작동하고 컬렉션을 반환합니다.  
  
 [XElement 클래스 개요](./xelement-class-overview.md)에 설명된 대로 <xref:System.Xml.Linq.XElement> 개체는 단일 요소 노드를 나타냅니다. 요소의 내용은 복합 요소(구조화된 내용이라고도 함)이거나 단순 요소일 수 있습니다. 단순 요소는 비어 있거나 값을 포함할 수 있습니다. 노드에 구조화된 내용이 포함되어 있으면 다양한 축 메서드를 사용하여 하위 요소의 열거형을 검색할 수 있습니다. 가장 일반적으로 사용되는 축 메서드는 <xref:System.Xml.Linq.XContainer.Elements%2A> 및 <xref:System.Xml.Linq.XContainer.Descendants%2A>입니다.  
  
 컬렉션을 반환하는 축 메서드 외에도 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 쿼리에서 일반적으로 사용하는 두 메서드가 있습니다. <xref:System.Xml.Linq.XContainer.Element%2A> 메서드는 단일 <xref:System.Xml.Linq.XElement>를 반환합니다. <xref:System.Xml.Linq.XElement.Attribute%2A> 메서드는 단일 <xref:System.Xml.Linq.XAttribute>를 반환합니다.  
  
 많은 용도를 위해 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리는 트리를 검사하고, 트리에서 데이터를 추출하고, 트리를 변환하는 가장 강력한 방법을 제공합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리는 <xref:System.Collections.Generic.IEnumerable%601>를 구현하는 개체에 대해 작동하며 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 축은 <xref:System.Xml.Linq.XElement> 컬렉션의 <xref:System.Collections.Generic.IEnumerable%601>와, <xref:System.Xml.Linq.XAttribute> 컬렉션의 <xref:System.Collections.Generic.IEnumerable%601>를 반환합니다. 쿼리를 수행하려면 이러한 컬렉션이 필요합니다.  
  
 요소와 특성의 컬렉션을 검색하는 축 메서드 외에도 트리를 매우 자세히 반복하는 데 사용할 수 있는 축 메서드가 있습니다. 예를 들어, 요소와 특성을 처리하는 대신 트리의 노드로 작업할 수 있습니다. 노드는 요소와 특성보다 세부적인 단위입니다. 노드로 작업할 때 XML 주석, 텍스트 노드, 처리 명령 등을 검사할 수 있습니다. 이 기능은 워드 프로세서를 작성 중인 사용자가 문서를 XML로 저장하려는 경우 등에 중요합니다. 그러나 XML 프로그래머의 대다수는 요소, 특성 및 해당 값에 주로 관심이 있습니다.  
  
## <a name="methods-for-retrieving-a-collection-of-elements"></a>요소 컬렉션을 검색하는 메서드  
 다음은 요소 컬렉션을 반환하기 위해 <xref:System.Xml.Linq.XElement>에 대해 호출하는 <xref:System.Xml.Linq.XElement> 클래스(또는 해당 기본 클래스)의 메서드를 요약한 것입니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|이 요소의 상위 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 상위 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType>|이 요소의 하위 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 하위 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|이 요소의 자식 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 자식 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType>|이 요소 뒤에 나오는 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 이 요소 뒤에 나오는 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType>|이 요소 앞에 나오는 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 이 요소 앞에 나오는 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|이 요소와 해당 상위 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType>|이 요소와 해당 하위 요소에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>을 반환합니다. 오버로드는 지정된 <xref:System.Collections.Generic.IEnumerable%601>을 가진 요소에 대한 <xref:System.Xml.Linq.XElement>의 <xref:System.Xml.Linq.XName>을 반환합니다.|  
  
## <a name="method-for-retrieving-a-single-element"></a>단일 요소를 검색하는 메서드  
 다음 메서드는 <xref:System.Xml.Linq.XElement> 개체에서 단일 자식을 검색합니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=nameWithType>|지정된 <xref:System.Xml.Linq.XElement>을 가진 첫 번째 자식 <xref:System.Xml.Linq.XName> 개체를 반환합니다.|  
  
## <a name="method-for-retrieving-a-collection-of-attributes"></a>특성 컬렉션을 검색하는 메서드  
 다음 메서드는 <xref:System.Xml.Linq.XElement> 개체에서 특성을 검색합니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|모든 특성에 대한 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XAttribute>을 반환합니다.|  
  
## <a name="method-for-retrieving-a-single-attribute"></a>단일 특성을 검색하는 메서드  
 다음 메서드는 <xref:System.Xml.Linq.XElement> 개체에서 단일 특성을 검색합니다.  
  
|메서드|설명|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType>|지정된 <xref:System.Xml.Linq.XAttribute>을 가진 <xref:System.Xml.Linq.XName>를 반환합니다.|  
  
## <a name="see-also"></a>참고 항목

- [LINQ to XML 축(C#)](./linq-to-xml-axes.md)
