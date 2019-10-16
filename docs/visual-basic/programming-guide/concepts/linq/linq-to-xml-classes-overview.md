---
title: LINQ to XML 클래스 개요 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: f11b62b5-d522-4c23-92ae-23186dc16447
ms.openlocfilehash: 10a6384167ee6ad6463a7f2f993b871fc8baea9e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64610748"
---
# <a name="linq-to-xml-classes-overview-visual-basic"></a>LINQ to XML 클래스 개요 (Visual Basic)
이 항목에서는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 네임스페이스의 <xref:System.Xml.Linq> 클래스 목록을 제공하며 각 클래스에 대한 간략한 설명을 제공합니다.  
  
## <a name="linq-to-xml-classes"></a>LINQ to XML 클래스  
  
### <a name="xattribute-class"></a>XAttribute 클래스  
 <xref:System.Xml.Linq.XAttribute>는 XML 특성을 나타냅니다. 자세한 내용 및 예제를 참조 하세요 [XAttribute 클래스 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xattribute-class-overview.md)합니다.  
  
### <a name="xcdata-class"></a>XCData 클래스  
 <xref:System.Xml.Linq.XCData>는 CDATA 텍스트 노드를 나타냅니다.  
  
### <a name="xcomment-class"></a>XComment 클래스  
 <xref:System.Xml.Linq.XComment>는 XML 주석을 나타냅니다.  
  
### <a name="xcontainer-class"></a>XContainer 클래스  
 <xref:System.Xml.Linq.XContainer>는 자식 노드를 가질 수 있는 모든 노드의 추상 기본 클래스입니다. 다음 클래스는 <xref:System.Xml.Linq.XContainer> 클래스에서 파생됩니다.  
  
- <xref:System.Xml.Linq.XElement>  
  
- <xref:System.Xml.Linq.XDocument>  
  
### <a name="xdeclaration-class"></a>XDeclaration 클래스  
 <xref:System.Xml.Linq.XDeclaration>은 XML 선언을 나타냅니다. XML 선언은 XML 버전과 문서의 인코딩을 선언하는 데 사용됩니다. 또한 XML 선언은 XML 문서가 독립 실행형인지 여부를 지정합니다. XML 문서가 독립 실행형인 경우 외부 DTD나 내부 하위 집합에서 참조된 외부 매개 변수 엔터티에 외부 태그 선언이 없습니다.  
  
### <a name="xdocument-class"></a>XDocument 클래스  
 <xref:System.Xml.Linq.XDocument>는 XML 문서를 나타냅니다. 자세한 내용 및 예제를 참조 하세요 [XDocument 클래스 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xdocument-class-overview.md)합니다.  
  
### <a name="xdocumenttype-class"></a>XDocumentType 클래스  
 <xref:System.Xml.Linq.XDocumentType>은 XML DTD(문서 종류 정의)를 나타냅니다.  
  
### <a name="xelement-class"></a>XElement 클래스  
 <xref:System.Xml.Linq.XElement>는 XML 요소를 나타냅니다. 자세한 내용 및 예제를 참조 하세요 [XElement 클래스 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xelement-class-overview.md)합니다.  
  
### <a name="xname-class"></a>XName 클래스  
 <xref:System.Xml.Linq.XName>은 요소(<xref:System.Xml.Linq.XElement>)와 특성(<xref:System.Xml.Linq.XAttribute>)의 이름을 나타냅니다. 자세한 내용 및 예제를 참조 하세요 [XDocument 클래스 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xdocument-class-overview.md)합니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]은 XML 이름을 가능한 한 간단하게 만들도록 디자인되었습니다. 복잡성 때문에 XML 이름은 흔히 XML의 고급 항목으로 간주됩니다. 거의 틀림없이 이 복잡성은 개발자가 프로그래밍에서 정기적으로 사용하는 네임스페이스 때문이 아니라 네임스페이스 접두사 때문입니다. 네임스페이스 접두사는 XML을 입력하거나 XML을 읽기 쉽게 만드는 데 필요한 키 입력을 줄이는 데 유용할 수 있습니다. 그러나 접두사는 전체 XML 네임스페이스를 사용하기 위한 바로 가기일 뿐인 경우가 많으며 대부분의 경우 필요하지 않습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 모든 접두사를 해당 XML 네임스페이스로 확인하여 XML 이름을 단순화합니다. 접두사가 필요한 경우 <xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A> 메서드를 통해 접두사를 사용할 수 있습니다.  
  
 필요한 경우 네임스페이스 접두사를 제어할 수 있습니다. 경우에 따라 XSLT, XAML 등의 다른 XML 시스템으로 작업하는 경우 네임스페이스 접두사를 제어해야 합니다. 예를 들어 XSLT 스타일시트에 포함된 네임스페이스 접두사를 사용하는 XPath 식이 있는 경우 XML 문서가 XPath 식에 사용된 것과 일치하는 네임스페이스 접두사로 serialize되는지 확인해야 합니다.  
  
### <a name="xnamespace-class"></a>XNamespace 클래스  
 <xref:System.Xml.Linq.XNamespace>는 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XAttribute>의 네임스페이스를 나타냅니다. 네임스페이스는 <xref:System.Xml.Linq.XName>의 구성 요소입니다.  
  
### <a name="xnode-class"></a>XNode 클래스  
 <xref:System.Xml.Linq.XNode>는 XML 트리의 노드를 나타내는 추상 클래스입니다. 다음 클래스는 <xref:System.Xml.Linq.XNode> 클래스에서 파생됩니다.  
  
- <xref:System.Xml.Linq.XText>  
  
- <xref:System.Xml.Linq.XContainer>  
  
- <xref:System.Xml.Linq.XComment>  
  
- <xref:System.Xml.Linq.XProcessingInstruction>  
  
- <xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xnodedocumentordercomparer-class"></a>XNodeDocumentOrderComparer 클래스  
 <xref:System.Xml.Linq.XNodeDocumentOrderComparer>는 노드의 문서 순서를 비교하는 기능을 제공합니다.  
  
### <a name="xnodeequalitycomparer-class"></a>XNodeEqualityComparer 클래스  
 <xref:System.Xml.Linq.XNodeEqualityComparer>는 노드의 값이 동일한지 비교하는 기능을 제공합니다.  
  
### <a name="xobject-class"></a>XObject 클래스  
 <xref:System.Xml.Linq.XObject>는 <xref:System.Xml.Linq.XNode> 및 <xref:System.Xml.Linq.XAttribute>의 추상 기본 클래스이며, 주석과 이벤트 기능을 제공합니다.  
  
### <a name="xobjectchange-class"></a>XObjectChange 클래스  
 <xref:System.Xml.Linq.XObjectChange>는 <xref:System.Xml.Linq.XObject>에 대한 이벤트가 발생할 때 이벤트 형식을 지정합니다.  
  
### <a name="xobjectchangeeventargs-class"></a>XObjectChangeEventArgs 클래스  
 <xref:System.Xml.Linq.XObjectChangeEventArgs>는 <xref:System.Xml.Linq.XObject.Changing> 및 <xref:System.Xml.Linq.XObject.Changed> 이벤트에 대한 데이터를 제공합니다.  
  
### <a name="xprocessinginstruction-class"></a>XProcessingInstruction 클래스  
 <xref:System.Xml.Linq.XProcessingInstruction>은 XML 처리 명령을 나타냅니다. 처리 명령은 XML을 처리하는 정보를 애플리케이션에 전달합니다.  
  
### <a name="xtext-class"></a>XText 클래스  
 <xref:System.Xml.Linq.XText>는 텍스트 노드를 나타냅니다. 대부분의 경우 이 클래스를 사용할 필요가 없습니다. 이 클래스는 혼합 내용에 주로 사용됩니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to XML 프로그래밍 개요 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
