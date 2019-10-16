---
title: XML CDATA 리터럴(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralCdata
helpviewer_keywords:
- CDATA literal [Visual Basic]
- XML CDATA literal [Visual Basic]
- XML literals [Visual Basic], CDATA
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
ms.openlocfilehash: 248f3cf31f686de3af2ea06012aa4a6d4f3f29fc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69942915"
---
# <a name="xml-cdata-literal-visual-basic"></a>XML CDATA 리터럴(Visual Basic)
<xref:System.Xml.Linq.XCData> 개체를 나타내는 리터럴입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<![CDATA[content]]>  
```  
  
## <a name="parts"></a>요소  
 `<![CDATA[`  
 필수 요소. XML CDATA 섹션의 시작을 나타냅니다.  
  
 `content`  
 필수 요소. XML CDATA 섹션에 표시할 텍스트 내용입니다.  
  
 `]]>`  
 필수 요소. 섹션의 끝을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 <xref:System.Xml.Linq.XCData> 개체입니다.  
  
## <a name="remarks"></a>설명  
 XML CDATA 섹션에는 포함 되어 있지만 구문 분석 되지 않은 원시 텍스트가 포함 된 XML로 포함 됩니다. XML CDATA 섹션에는 모든 텍스트가 포함 될 수 있습니다. 여기에는 예약 된 XML 문자가 포함 됩니다. XML CDATA 섹션은 "]] >" 시퀀스로 끝납니다. 이는 다음 사항을 의미 합니다.  
  
- 포함 된 식 구분 기호가 유효한 XML CDATA 콘텐츠 이므로 XML CDATA 리터럴에 포함 식을 사용할 수 없습니다.  
  
- XML CDATA 섹션은 중첩 될 수 없습니다 `content` .에는 "]] >" 값을 사용할 수 없기 때문입니다.  
  
 XML CDATA 리터럴을 변수에 할당 하거나 XML 요소 리터럴에 포함할 수 있습니다.  
  
> [!NOTE]
> XML 리터럴은 여러 줄에 걸쳐 있을 수 있지만 줄 연속 문자를 사용 하지 않습니다. 이렇게 하면 XML 문서에서 콘텐츠를 복사 하 여 Visual Basic 프로그램에 직접 붙여넣을 수 있습니다.  
  
 Visual Basic 컴파일러는 XML CDATA 리터럴을 <xref:System.Xml.Linq.XCData.%23ctor%2A> 생성자에 대 한 호출로 변환 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 "리터럴 \<XML > 태그를 포함할 수 있습니다." 라는 텍스트가 포함 된 CDATA 섹션을 만듭니다.  
  
 [!code-vb[VbXMLSamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#23)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xml.Linq.XCData>
- [XML 요소 리터럴](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
