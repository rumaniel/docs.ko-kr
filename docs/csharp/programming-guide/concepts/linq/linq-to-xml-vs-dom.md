---
title: LINQ to XML과 비교 DOM(C#)
ms.date: 07/20/2015
ms.assetid: 51c0e3d2-c047-4e6a-a423-d61a882400b7
ms.openlocfilehash: 68d380873e71d767ddd60f8f9d0f4b82846d1371
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591774"
---
# <a name="linq-to-xml-vs-dom-c"></a>LINQ to XML과 비교 DOM(C#)
이 섹션에서는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]과 현재 주로 사용되는 XML 프로그래밍 API인 W3C DOM(문서 개체 모델)의 몇 가지 주요 차이점에 대해 설명합니다.  
  
## <a name="new-ways-to-construct-xml-trees"></a>XML 트리를 생성하는 새로운 방법  
 W3C DOM에서는 상향식으로 XML 트리를 빌드합니다. 즉, 문서를 만들고 요소를 만든 다음 요소를 문서에 추가합니다.  
  
 예를 들어, DOM의 Microsoft 구현인 <xref:System.Xml.XmlDocument>를 사용하여 XML 트리를 만드는 일반적인 방법은 다음과 같습니다.  
  
```csharp  
XmlDocument doc = new XmlDocument();  
XmlElement name = doc.CreateElement("Name");  
name.InnerText = "Patrick Hines";  
XmlElement phone1 = doc.CreateElement("Phone");  
phone1.SetAttribute("Type", "Home");  
phone1.InnerText = "206-555-0144";          
XmlElement phone2 = doc.CreateElement("Phone");  
phone2.SetAttribute("Type", "Work");  
phone2.InnerText = "425-555-0145";          
XmlElement street1 = doc.CreateElement("Street1");          
street1.InnerText = "123 Main St";  
XmlElement city = doc.CreateElement("City");  
city.InnerText = "Mercer Island";  
XmlElement state = doc.CreateElement("State");  
state.InnerText = "WA";  
XmlElement postal = doc.CreateElement("Postal");  
postal.InnerText = "68042";  
XmlElement address = doc.CreateElement("Address");  
address.AppendChild(street1);  
address.AppendChild(city);  
address.AppendChild(state);  
address.AppendChild(postal);  
XmlElement contact = doc.CreateElement("Contact");  
contact.AppendChild(name);  
contact.AppendChild(phone1);  
contact.AppendChild(phone2);  
contact.AppendChild(address);  
XmlElement contacts = doc.CreateElement("Contacts");  
contacts.AppendChild(contact);  
doc.AppendChild(contacts);  
```  
  
 이 코딩 스타일은 XML 트리의 구조에 대한 많은 정보를 시각적으로 제공하지 않습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 이러한 XML 트리 생성 방법을 지원하지만 다른 방법인 *함수 생성*도 지원합니다. 함수 생성에서는 <xref:System.Xml.Linq.XElement> 및 <xref:System.Xml.Linq.XAttribute> 생성자를 사용하여 XML 트리를 빌드합니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 함수 생성을 사용하여 동일한 XML 트리를 생성하는 방법은 다음과 같습니다.  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),  
            new XElement("Phone", "206-555-0144",   
                new XAttribute("Type", "Home")),  
            new XElement("phone", "425-555-0145",  
                new XAttribute("Type", "Work")),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 XML 트리를 생성하는 코드의 들여쓰기는 기본 XML의 구조를 나타냅니다.  
  
 자세한 내용은 [XML 트리 만들기(C#)](./linq-to-xml-overview.md)를 참조하세요.  
  
## <a name="working-directly-with-xml-elements"></a>XML 요소로 직접 작업  
 XML을 사용하여 프로그래밍하는 경우 XML 요소를 대개 집중적으로 다루고 특성도 집중적으로 다룰 수 있습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 XML 요소 및 특성으로 직접 작업할 수 있습니다. 예를 들어, 다음을 수행할 수 있습니다.  
  
- 문서 개체를 전혀 사용하지 않고 XML 요소를 만듭니다. 이에 따라 XML 트리의 조각으로 작업해야 하는 경우 프로그래밍이 단순해집니다.  
  
- XML 파일에서 `T:System.Xml.Linq.XElement` 개체를 직접 로드합니다.  
  
- `T:System.Xml.Linq.XElement` 개체를 파일이나 스트림으로 serialize합니다.  
  
 이와 비교할 때 W3C DOM에서는 XML 문서가 XML 트리의 논리 컨테이너로 사용됩니다. DOM에서 요소 및 특성을 비롯한 XML 노드는 XML 문서의 컨텍스트에서 만들어져야 합니다. DOM에서 이름 요소를 만드는 코드의 조각은 다음과 같습니다.  
  
```csharp  
XmlDocument doc = new XmlDocument();  
XmlElement name = doc.CreateElement("Name");  
name.InnerText = "Patrick Hines";  
doc.AppendChild(name);  
```  
  
 여러 문서에서 요소를 사용하려면 여러 문서의 노드를 가져와야 합니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 이러한 복잡한 작업이 필요 없습니다.  
  
 LINQ to XML을 사용할 때 문서의 루트 수준에서 주석이나 처리 명령을 추가하려는 경우에만 <xref:System.Xml.Linq.XDocument> 클래스를 사용합니다.  
  
## <a name="simplified-handling-of-names-and-namespaces"></a>이름 및 네임스페이스의 간단한 처리  
 이름, 네임스페이스 및 네임스페이스 접두사의 처리는 대개 XML 프로그래밍의 복잡한 부분입니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 네임스페이스 접두사를 처리해야 하는 요구 사항을 제거하여 이름과 네임스페이스를 단순화합니다. 네임스페이스 접두사를 제어하고 싶으면 제어할 수 있습니다. 그러나 네임스페이스 접두사를 명시적으로 제어하지 않도록 결정하는 경우 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 serialize할 때 필요한 경우 네임스페이스 접두사를 할당하거나, 기본 네임스페이스를 사용하여 serialize합니다. 기본 네임스페이스가 사용되는 경우 생성되는 문서에는 네임스페이스 접두사가 없습니다. 자세한 내용은 [네임스페이스 개요(LINQ to XML)(C#)](namespaces-overview-linq-to-xml.md)를 참조하세요.  
  
 DOM의 또 다른 문제는 노드의 이름을 변경할 수 없다는 것입니다. 대신 새 노드를 만들고 모든 자식 노드를 새 노드에 복사해야 하므로 원래 노드 ID가 손실됩니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 노드에서 <xref:System.Xml.Linq.XName> 속성을 설정할 수 있도록 하여 이 문제를 방지합니다.  
  
## <a name="static-method-support-for-loading-xml"></a>XML을 로드하기 위한 정적 메서드 지원  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 인스턴스 메서드 대신 정적 메서드를 사용하여 XML을 로드할 수 있습니다. 이에 따라 로드와 구문 분석이 간단해집니다. 자세한 내용은 [방법: 파일에서 XML 로드(C#)](./how-to-load-xml-from-a-file.md)를 참조하세요.  
  
## <a name="removal-of-support-for-dtd-constructs"></a>DTD 구문에 대한 지원 제거  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 엔터티와 엔터티 참조에 대한 지원 기능을 제거하여 XML 프로그래밍을 더욱 단순화합니다. 엔터티의 관리는 복잡하므로 드물게 사용됩니다. 이러한 지원 기능을 제거하면 성능이 향상되고 프로그래밍 인터페이스가 간단해집니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 트리가 채워지면 모든 DTD 엔터티가 확장됩니다.  
  
## <a name="support-for-fragments"></a>조각에 대한 지원  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 `XmlDocumentFragment` 클래스와 동일한 항목을 제공하지 않습니다. 그러나 대부분의 경우에 `XmlDocumentFragment` 개념은 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XNode>이나 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XElement>로 형식화된 쿼리의 결과에 의해 처리될 수 있습니다.  
  
## <a name="support-for-xpathnavigator"></a>XPathNavigator에 대한 지원  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 <xref:System.Xml.XPath.XPathNavigator> 네임스페이스의 확장 메서드를 통해 <xref:System.Xml.XPath?displayProperty=nameWithType>를 지원합니다. 자세한 내용은 <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>을 참조하세요.  
  
## <a name="support-for-white-space-and-indentation"></a>공백 및 들여쓰기에 대한 지원  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 DOM의 경우보다 간단하게 공백을 처리합니다.  
  
 일반적인 시나리오는 들여쓴 XML을 읽고 공백 텍스트 노드 없이 메모리 내 XML 트리를 만든 다음(공백을 유지하지 않음) XML에 대한 작업을 수행하고 들여쓰기를 사용하여 XML을 저장하는 것입니다. 서식이 있는 XML을 serialize하는 경우 XML 트리의 유효 공백만 유지됩니다. 이것이 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 기본 동작입니다.  
  
 다른 일반적인 시나리오는 이미 의도적으로 들여쓴 XML을 읽고 수정하는 것입니다. 이 들여쓰기를 변경하려고 하지 않을 수 있습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 XML을 로드하거나 구문 분석할 때 공백을 유지하고 XML을 serialize할 때 서식을 해제하는 경우 이렇게 할 수 있습니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 DOM의 경우처럼 serialize된 <xref:System.Xml.Linq.XText> 노드 형식을 사용하는 대신 <xref:System.Xml.XmlNodeType.Whitespace> 노드로 공백을 저장합니다.  
  
## <a name="support-for-annotations"></a>주석에 대한 지원  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 요소는 확장 가능한 주석 집합을 지원합니다. 이러한 지원은 스키마 정보, 요소가 UI에 바인딩되어 있는지 여부 또는 다른 종류의 애플리케이션 관련 정보와 같은 요소에 대한 기타 정보를 추적하는 데 유용합니다. 자세한 내용은 [LINQ to XML 주석](./linq-to-xml-annotations.md)을 참조하세요.  
  
## <a name="support-for-schema-information"></a>스키마 정보에 대한 지원  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 <xref:System.Xml.Schema?displayProperty=nameWithType> 네임스페이스의 확장 메서드를 통해 XSD 유효성 검사를 지원합니다. XML 트리가 XSD를 준수하는지 확인할 수 있으며, PSVI(Post-Schema-Validation Infoset)를 사용하여 XML 트리를 채울 수 있습니다. 자세한 내용은 [방법: XSD를 사용하여 유효성 검사](./how-to-validate-using-xsd-linq-to-xml.md) 및 <xref:System.Xml.Schema.Extensions>를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [시작(LINQ to XML)](./linq-to-xml-overview.md)
