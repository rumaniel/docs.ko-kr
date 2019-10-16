---
title: '방법: (Visual Basic) XML 리터럴에 식 포함'
ms.date: 07/20/2015
helpviewer_keywords:
- embedded expressions [Visual Basic]
- XML literals [Visual Basic], embedded expressions
ms.assetid: 75016fad-0141-42de-8564-5051be29487e
ms.openlocfilehash: 9d0fd1e3713dc5b81cfca0ce54b571b38e648f87
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65879107"
---
# <a name="how-to-embed-expressions-in-xml-literals-visual-basic"></a>방법: (Visual Basic) XML 리터럴에 식 포함
XML 리터럴의 XML 문서, 조각 또는 런타임에 생성 하는 콘텐츠를 포함 하는 요소를 만들려면 포함 된 식으로 결합할 수 있습니다. 다음 예제에서는 포함 된 식을 사용 하 여 런타임에 콘텐츠 요소, 특성 및 요소 이름이 채우는 방법을 보여 줍니다.  
  
 포함된 식에 대 한 구문은 `<%=` `exp` `%>`는 ASP.NET을 사용 하는 구문과 같습니다. 자세한 내용은 [XML의 포함 식](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)합니다.  
  
 사용할 수도 있습니다는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] Api를 만드는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 개체입니다. 자세한 내용은 <xref:System.Xml.Linq.XElement>을 참조하세요.  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-insert-text-as-element-content"></a>요소 내용으로 텍스트를 삽입 하려면  
  
- 다음 예제에서는에 포함 된 텍스트를 삽입 하는 방법을 보여 줍니다는 `contactName` 열기 및 닫기 이름 요소 간의 변수입니다.  
  
     [!code-vb[VbXMLSamples#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples14.vb#39)]  
  
     이 예제는 다음과 같은 출력을 생성합니다.  
  
    ```xml  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-as-an-attribute-value"></a>특성 값으로 텍스트를 삽입 하려면  
  
- 다음 예제에서는에 포함 된 텍스트를 삽입 하는 방법을 보여 줍니다 합니다 `phoneType` 값으로 변수를 `type` 특성입니다.  
  
     [!code-vb[VbXMLSamples#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples14.vb#40)]  
  
     이 예제는 다음과 같은 출력을 생성합니다.  
  
    ```xml  
    <contact>  
      <phone type="home">206-555-0144</phone>  
    </contact>  
    ```  
  
#### <a name="to-insert-text-for-an-element-name"></a>요소 이름에 대 한 텍스트를 삽입 하려면  
  
- 다음 예제에서는에 포함 된 텍스트를 삽입 하는 방법을 보여 줍니다는 `elementName` 요소의 이름으로 변수입니다.  
  
     이 기술을 사용 하 여 요소를 만들 때를 닫아야 하는 \</ > 태그입니다.  
  
     [!code-vb[VbXMLSamples#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples14.vb#41)]  
  
     이 예제는 다음과 같은 출력을 생성합니다.  
  
    ```xml  
    <contact>  
      <name>Patrick Hines</name>  
    </contact>  
    ```  
  
## <a name="see-also"></a>참고자료

- [방법: XML 리터럴 만들기](../../../../visual-basic/programming-guide/language-features/xml/how-to-create-xml-literals.md)
- [XML의 포함 식](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [Visual Basic에서 XML 만들기](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
