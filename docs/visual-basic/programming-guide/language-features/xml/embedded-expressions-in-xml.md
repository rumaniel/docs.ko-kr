---
title: XML의 포함 식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlEmbeddedExpression
helpviewer_keywords:
- embedded expressions [Visual Basic]
- LINQ to XML [Visual Basic], embedded expressions
- XML literals [Visual Basic], embedded expressions
ms.assetid: bf2eb779-b751-4b7c-854f-9f2161482352
ms.openlocfilehash: 525fa04db86a299d88e1612aac76d014f35124eb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922625"
---
# <a name="embedded-expressions-in-xml-visual-basic"></a>XML의 포함 식(Visual Basic)
포함 식을 사용 하면 런타임에 계산 되는 식을 포함 하는 XML 리터럴을 만들 수 있습니다. 포함 식 `<%=` `expression` 의구문은이며,ASP.NET에사용되`%>`는 구문과 같습니다.  
  
 예를 들어, 포함 된 식을 리터럴 텍스트 콘텐츠와 결합 하 여 XML 요소 리터럴을 만들 수 있습니다.  
  
 [!code-vb[VbXMLSamples#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#27)]  
  
 에 `isbnNumber` 정수 12345이 포함 되어 `modifiedDate` 있고이 코드가 실행 될 때 날짜 3/5/2006를 포함 하는 경우 `book` 의 값은 다음과 같습니다.  
  
```xml  
<book category="fiction" isbn="12345">  
  <modifiedDate>3/5/2006</modifiedDate>  
</book>  
```  
  
## <a name="embedded-expression-location-and-validation"></a>포함 식 위치 및 유효성 검사  
 포함 식은 XML 리터럴 식 내의 특정 위치에만 나타날 수 있습니다. 식 위치는 식에서 반환할 수 있는 형식과를 처리 하 `Nothing` 는 방법을 제어 합니다. 다음 표에서는 허용 되는 위치 및 포함 식의 유형에 대해 설명 합니다.  
  
|리터럴의 위치|식의 형식|처리`Nothing`|  
|---|---|---|  
|XML 요소 이름|<xref:System.Xml.Linq.XName>|Error|  
|XML 요소 내용|`Object`또는 배열`Object`|무시됨|  
|XML 요소 특성 이름|<xref:System.Xml.Linq.XName>|특성 값이 없는 경우 오류가 발생 합니다.`Nothing`|  
|XML 요소 특성 값|`Object`|특성 선언이 무시 되었습니다.|  
|XML 요소 특성|<xref:System.Xml.Linq.XAttribute>또는 컬렉션<xref:System.Xml.Linq.XAttribute>|무시됨|  
|XML 문서 루트 요소|<xref:System.Xml.Linq.XElement>또는 하나의 <xref:System.Xml.Linq.XElement> 개체와 임의의 <xref:System.Xml.Linq.XProcessingInstruction> 수의 및 <xref:System.Xml.Linq.XComment> 개체 컬렉션|무시됨|  
  
- XML 요소 이름에 포함 된 식의 예:  
  
     [!code-vb[VbXMLSamples#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#32)]  
  
- XML 요소 내용에 포함 된 식의 예:  
  
     [!code-vb[VbXMLSamples#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#33)]  
  
- XML 요소 특성 이름에 포함 된 식의 예:  
  
     [!code-vb[VbXMLSamples#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#34)]  
  
- XML 요소 특성 값의 포함 식 예제:  
  
     [!code-vb[VbXMLSamples#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#35)]  
  
- XML 요소 특성에 포함 된 식의 예:  
  
     [!code-vb[VbXMLSamples#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#36)]  
  
- XML 문서 루트 요소에 포함 된 식의 예:  
  
     [!code-vb[VbXMLSamples#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#37)]  
  
 를 사용 `Option Strict`하는 경우 컴파일러는 각 포함 된 식의 형식이 필요한 형식으로 확대 되는지 확인 합니다. 유일한 예외는 XML 문서의 루트 요소입니다 .이 요소는 코드가 실행 될 때 확인 됩니다. 없이 `Option Strict`컴파일하는 경우 형식의 `Object` 식을 포함 하 고 런타임에 해당 형식을 확인할 수 있습니다.  
  
 콘텐츠가 선택적인 위치에서를 포함 `Nothing` 하는 포함 식은 무시 됩니다. 즉, XML 리터럴을 사용 `Nothing` 하기 전에 요소 내용, 특성 값 및 배열 요소를 확인 하지 않아도 됩니다. 요소 및 특성 이름과 같은 필수 값은 일 `Nothing`수 없습니다.  
  
 특정 형식의 리터럴에 포함 된 식을 사용 하는 방법에 대 한 자세한 내용은 [Xml 문서 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md), [xml 요소 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)을 참조 하세요.  
  
## <a name="scoping-rules"></a>범위 지정 규칙  
 컴파일러는 각 XML 리터럴을 적절 한 리터럴 형식에 대 한 생성자 호출로 변환 합니다. XML 리터럴의 리터럴 콘텐츠 및 포함 식은 생성자에 인수로 전달 됩니다. 즉, XML 리터럴에 사용할 수 있는 모든 Visual Basic 프로그래밍 요소는 포함 된 식에도 사용할 수 있습니다.  
  
 Xml 리터럴 내에서 `Imports` 문으로 선언 된 xml 네임 스페이스 접두사에 액세스할 수 있습니다. `xmlns` 특성을 사용 하 여 요소에서 새 xml 네임 스페이스 접두사를 선언 하거나 기존 xml 네임 스페이스 접두사를 숨길 수 있습니다. 새 네임 스페이스는 해당 요소의 자식 노드에서 사용할 수 있지만 포함 식의 XML 리터럴이 아닙니다.  
  
> [!NOTE]
> `xmlns` 네임 스페이스 특성을 사용 하 여 XML 네임 스페이스 접두사를 선언 하는 경우 특성 값은 상수 문자열 이어야 합니다. 이와 관련 하 여 `xmlns` 특성을 사용 하는 것은 `Imports` 문을 사용 하 여 XML 네임 스페이스를 선언 하는 것과 같습니다. 포함 식을 사용 하 여 XML 네임 스페이스 값을 지정할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic에서 XML 만들기](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [XML 문서 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)
- [XML 요소 리터럴](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [XML 리터럴 개요](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)
