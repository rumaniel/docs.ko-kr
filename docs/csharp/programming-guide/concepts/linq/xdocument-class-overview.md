---
title: XDocument 클래스 개요(C#)
ms.date: 07/20/2015
ms.assetid: 63305603-ab54-49fc-84e4-f76eecc59549
ms.openlocfilehash: de49dc071d22dd77dddea29ca114663261e3edda
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590850"
---
# <a name="xdocument-class-overview-c"></a>XDocument 클래스 개요(C#)
이 항목에서는 <xref:System.Xml.Linq.XDocument> 클래스에 대해 소개합니다.  
  
## <a name="overview-of-the-xdocument-class"></a>XDocument 클래스 개요  
 <xref:System.Xml.Linq.XDocument> 클래스에는 유효한 XML 문서에 필요한 정보가 포함되어 있습니다. 여기에는 XML 선언, 처리 명령 및 주석이 포함되어 있습니다.  
  
 <xref:System.Xml.Linq.XDocument> 클래스에서 제공하는 특정 기능이 필요한 경우 <xref:System.Xml.Linq.XDocument> 개체만 만들면 됩니다. 대부분의 경우 <xref:System.Xml.Linq.XElement>로 직접 작업할 수 있습니다. <xref:System.Xml.Linq.XElement>로 직접 작업하는 것이 더 간단한 프로그래밍 모델입니다.  
  
 <xref:System.Xml.Linq.XDocument>은 <xref:System.Xml.Linq.XContainer>로부터 파생됩니다. 자식 노드를 포함할 수 있습니다. 그러나 <xref:System.Xml.Linq.XDocument> 개체에는 자식 <xref:System.Xml.Linq.XElement> 노드가 하나만 포함될 수 있습니다. 이는 XML 문서에 루트 요소가 하나만 있어야 하는 XML 표준을 반영하는 것입니다.  
  
## <a name="components-of-xdocument"></a>XDocument의 구성 요소  
 <xref:System.Xml.Linq.XDocument>에는 다음과 같은 요소가 포함될 수 있습니다.  
  
- <xref:System.Xml.Linq.XDeclaration> 개체 하나. <xref:System.Xml.Linq.XDeclaration>을 통해 XML 선언의 관련 부분인 XML 버전, 문서의 인코딩 및 XML 문서가 독립 실행형인지 여부를 지정할 수 있습니다.  
  
- <xref:System.Xml.Linq.XElement> 개체 하나. 이 개체는 XML 문서의 루트 노드입니다.  
  
- <xref:System.Xml.Linq.XProcessingInstruction> 개체(수에 제한 없음). 처리 명령은 XML을 처리하는 정보를 애플리케이션에 전달합니다.  
  
- <xref:System.Xml.Linq.XComment> 개체(수에 제한 없음). 주석은 루트 요소의 형제입니다. XML 문서는 주석으로 시작될 수 없으므로 <xref:System.Xml.Linq.XComment> 개체는 목록의 첫 번째 인수일 수 없습니다.  
  
- DTD에 대한 <xref:System.Xml.Linq.XDocumentType> 하나  
  
 <xref:System.Xml.Linq.XDocument>를 serialize할 때 `XDocument.Declaration`이 `null`인 경우에도 작성기의 `Writer.Settings.OmitXmlDeclaration`이 `false`(기본값)로 설정되어 있으면 출력에 XML 선언이 포함됩니다.  
  
 기본적으로 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 버전을 "1.0"으로 설정하고 인코딩을 "utf-8"로 설정합니다.  
  
## <a name="using-xelement-without-xdocument"></a>XDocument 없이 XElement 사용  
 앞에서 설명했듯이 <xref:System.Xml.Linq.XElement> 클래스는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 프로그래밍 인터페이스의 기본 클래스입니다. 애플리케이션에서는 대부분의 경우 문서를 만들도록 요구하지 않습니다. <xref:System.Xml.Linq.XElement> 클래스를 사용하여 XML 트리를 만들고, XML 트리에 다른 XML 트리를 추가하고, XML 트리를 수정 및 저장할 수 있습니다.  
  
## <a name="using-xdocument"></a>XDocument 사용  
 <xref:System.Xml.Linq.XDocument>를 생성하려면 <xref:System.Xml.Linq.XElement> 개체를 생성할 때와 마찬가지로 함수 생성을 사용합니다.  
  
 다음 코드에서는 <xref:System.Xml.Linq.XDocument> 개체와 포함된 관련 개체를 만듭니다.  
  
```csharp  
XDocument d = new XDocument(  
    new XComment("This is a comment."),  
    new XProcessingInstruction("xml-stylesheet",  
        "href='mystyle.css' title='Compact' type='text/css'"),  
    new XElement("Pubs",  
        new XElement("Book",  
            new XElement("Title", "Artifacts of Roman Civilization"),  
            new XElement("Author", "Moreno, Jordao")  
        ),  
        new XElement("Book",  
            new XElement("Title", "Midieval Tools and Implements"),  
            new XElement("Author", "Gazit, Inbar")  
        )  
    ),  
    new XComment("This is another comment.")  
);  
d.Declaration = new XDeclaration("1.0", "utf-8", "true");  
Console.WriteLine(d);  
  
d.Save("test.xml");  
```  
  
 test.xml 파일을 검사할 때 다음과 같은 출력이 표시됩니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!--This is a comment.-->  
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
<Pubs>  
  <Book>  
    <Title>Artifacts of Roman Civilization</Title>  
    <Author>Moreno, Jordao</Author>  
  </Book>  
  <Book>  
    <Title>Midieval Tools and Implements</Title>  
    <Author>Gazit, Inbar</Author>  
  </Book>  
</Pubs>  
<!--This is another comment.-->  
```  
  
## <a name="see-also"></a>참고 항목

- [LINQ to XML 프로그래밍 개요(C#)](./linq-to-xml-overview.md)
