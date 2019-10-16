---
title: '방법: 파일, 문자열 또는 스트림에서 XML 로드 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- XML [Visual Basic], loading
- LINQ to XML [Visual Basic], loading XML from files
ms.assetid: 2b02dcec-4cca-4575-b4ad-89ceb87b984c
ms.openlocfilehash: ba88ae19abc216a318d6c2069ab0846d5db8a346
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054175"
---
# <a name="how-to-load-xml-from-a-file-string-or-stream-visual-basic"></a>방법: 파일, 문자열 또는 스트림에서 XML 로드 (Visual Basic)

[XML 리터럴을](../../../../visual-basic/language-reference/xml-literals/index.md) 만들고 여러 메서드를 사용 하 여 파일, 문자열 또는 스트림과 같은 외부 소스의 콘텐츠로 채울 수 있습니다. 이러한 메서드는 다음 예제에 나와 있습니다.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-load-xml-from-a-file"></a>파일에서 XML을 로드 하려면

파일에서 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체와 같은 XML 리터럴을 채우려면 메서드를 `Load` 사용 합니다. 이 메서드는 파일 경로, 텍스트 스트림 또는 XML 스트림을 입력으로 사용할 수 있습니다.

다음 코드 예제에서는 <xref:System.Xml.Linq.XDocument.Load%28System.String%29> 메서드를 사용 하 여 텍스트 파일의 XML로 <xref:System.Xml.Linq.XDocument> 개체를 채우는 방법을 보여 줍니다.

[!code-vb[VbXMLSamples#43](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#43)]

## <a name="to-load-xml-from-a-string"></a>문자열에서 XML을 로드 하려면

문자열에서 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체와 같은 XML 리터럴을 채우려면 메서드를 `Parse` 사용할 수 있습니다.

다음 코드 예제에서는 <xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=nameWithType> 메서드를 사용 하 여 문자열에서 XML로 <xref:System.Xml.Linq.XDocument> 개체를 채우는 방법을 보여 줍니다.

[!code-vb[VbXMLSamples#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#47)]

## <a name="to-load-xml-from-a-stream"></a>스트림에서 XML을 로드 하려면

스트림에서 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체와 같은 XML 리터럴을 채우려면 `Load` 메서드 또는 <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType> 메서드를 사용할 수 있습니다.

다음 코드 예제에서는 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 메서드를 사용 하 여 xml 스트림의 xml로 <xref:System.Xml.Linq.XDocument> 개체를 채우는 방법을 보여 줍니다.

[!code-vb[VbXMLSamples#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples15.vb#46)]

## <a name="see-also"></a>참고자료

- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=nameWithType>
- [XML 리터럴](../../../../visual-basic/language-reference/xml-literals/index.md)
- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
- [Visual Basic에서 XML 조작](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
