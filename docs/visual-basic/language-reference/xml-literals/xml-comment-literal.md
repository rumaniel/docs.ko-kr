---
title: XML 주석 리터럴(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralComment
helpviewer_keywords:
- comment literal [Visual Basic]
- XML comments, adding [Visual Basic]
- XML comment literal [Visual Basic]
- XML literals [Visual Basic], comment
ms.assetid: 634c1cee-5e01-48d0-88d7-2dd55e4a9e52
ms.openlocfilehash: 91369392f33f2a86a7a4cb5ffb3faa668c113348
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965406"
---
# <a name="xml-comment-literal-visual-basic"></a>XML 주석 리터럴(Visual Basic)
<xref:System.Xml.Linq.XComment> 개체를 나타내는 리터럴입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<!-- content -->  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`<!--`|필수 요소. XML 주석의 시작을 나타냅니다.|  
|`content`|필수 요소. XML 주석에 표시할 텍스트입니다. 두 개의 하이픈 (--)을 포함 하거나 닫는 태그 옆에 하이픈으로 끝날 수 없습니다.|  
|`-->`|필수 요소. XML 주석의 끝을 나타냅니다.|  
  
## <a name="return-value"></a>반환 값  
 <xref:System.Xml.Linq.XComment> 개체입니다.  
  
## <a name="remarks"></a>설명  
 XML 주석 리터럴에 문서 내용이 포함 되어 있지 않습니다. 문서에 대 한 정보를 포함 합니다. XML 주석 섹션은 "-->" 시퀀스로 끝납니다. 이는 다음 사항을 의미 합니다.  
  
- 포함 된 식 구분 기호가 유효한 XML 주석 내용 이므로 XML 주석 리터럴에 포함 식을 사용할 수 없습니다.  
  
- XML 주석 섹션은 중첩 될 수 없습니다 `content` .에는 "-->" 값을 사용할 수 없기 때문입니다.  
  
 XML 주석 리터럴을 변수에 할당 하거나 XML 요소 리터럴에 포함할 수 있습니다.  
  
> [!NOTE]
> XML 리터럴은 줄 연속 문자를 사용 하지 않고 여러 줄에 걸쳐 있을 수 있습니다. 이 기능을 사용 하면 XML 문서에서 콘텐츠를 복사 하 여 Visual Basic 프로그램에 직접 붙여넣을 수 있습니다.  
  
 Visual Basic 컴파일러는 XML 주석 리터럴을 <xref:System.Xml.Linq.XComment.%23ctor%2A> 생성자에 대 한 호출로 변환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 "This is comment" 라는 텍스트가 포함 된 XML 주석을 만듭니다.  
  
 [!code-vb[VbXMLSamples#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples4.vb#9)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xml.Linq.XComment>
- [XML 요소 리터럴](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
