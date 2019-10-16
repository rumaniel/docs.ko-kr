---
title: XML 문서 리터럴(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralDocument
helpviewer_keywords:
- XML document literal [Visual Basic]
- XML literals [Visual Basic], document
- XML documents [Visual Basic], creating
- document literal [Visual Basic]
ms.assetid: f7bbee56-0911-41de-b907-96f20450137b
ms.openlocfilehash: 8a489be46295c213b7a8b355eb3c9786d49dd8f1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958510"
---
# <a name="xml-document-literal-visual-basic"></a>XML 문서 리터럴(Visual Basic)
<xref:System.Xml.Linq.XDocument> 개체를 나타내는 리터럴입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<?xml version="1.0" [encoding="encoding"] [standalone="standalone"] ?>  
[ piCommentList ]  
rootElement  
[ piCommentList ]  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`encoding`|선택 사항입니다. 문서에서 사용 하는 인코딩을 선언 하는 리터럴 텍스트입니다.|  
|`standalone`|선택 사항입니다. 리터럴 텍스트입니다. "Yes" 또는 "no" 여야 합니다.|  
|`piCommentList`|선택 사항입니다. XML 처리 명령 및 XML 주석 목록입니다. 는 다음과 같은 형식을 사용 합니다.<br /><br /> `piComment [` `piComment` `... ]`<br /><br /> 각 `piComment` 항목은 다음 중 하나일 수 있습니다.<br /><br /> -   [XML 처리 명령 리터럴입니다](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md).<br />-   [XML 주석 리터럴입니다](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md).|  
|`rootElement`|필수 요소. 문서의 루트 요소입니다. 형식은 다음 중 하나입니다.<br /><br /> <ul><li>[XML 요소 리터럴입니다](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).</li><li>형식의 `<%=` 포함된식`%>`입니다. `elementExp` 는 `elementExp` 다음 중 하나를 반환 합니다.<br /><br /> <ul><li><xref:System.Xml.Linq.XElement> 개체입니다.</li><li>하나의 <xref:System.Xml.Linq.XElement> 개체와 임의의 수의 <xref:System.Xml.Linq.XProcessingInstruction> 및 <xref:System.Xml.Linq.XComment> 개체가 포함 된 컬렉션입니다.</li></ul></li></ul><br /> 자세한 내용은 [XML의 포함 식](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)을 참조 하세요.|  
  
## <a name="return-value"></a>반환 값  
 <xref:System.Xml.Linq.XDocument> 개체입니다.  
  
## <a name="remarks"></a>설명  
 XML 문서 리터럴은 리터럴의 시작 부분에 있는 XML 선언으로 식별 됩니다. 각 XML 문서 리터럴에는 정확히 하나의 루트 XML 요소가 있어야 하지만 xml 처리 명령과 XML 주석이 있을 수 있습니다.  
  
 Xml 문서 리터럴은 XML 요소에 나타날 수 없습니다.  
  
> [!NOTE]
> XML 리터럴은 줄 연속 문자를 사용 하지 않고 여러 줄에 걸쳐 있을 수 있습니다. 이렇게 하면 XML 문서에서 콘텐츠를 복사 하 여 Visual Basic 프로그램에 직접 붙여넣을 수 있습니다.  
  
 Visual Basic 컴파일러는 XML 문서 리터럴을 <xref:System.Xml.Linq.XDocument.%23ctor%2A> 및 <xref:System.Xml.Linq.XDeclaration.%23ctor%2A> 생성자에 대 한 호출로 변환 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 XML 선언, 처리 명령, 주석 및 다른 요소를 포함 하는 요소가 포함 된 XML 문서를 만듭니다.  
  
 [!code-vb[VbXMLSamples#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#30)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xml.Linq.XElement>
- <xref:System.Xml.Linq.XProcessingInstruction>
- <xref:System.Xml.Linq.XComment>
- <xref:System.Xml.Linq.XDocument>
- [XML 처리 명령 리터럴](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md)
- [XML 주석 리터럴](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)
- [XML 요소 리터럴](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [XML의 포함 식](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
