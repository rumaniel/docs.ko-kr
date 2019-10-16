---
title: XML 처리 옵션
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 33ced8ee-1745-4e71-8dee-ebe70ec067c7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 585a6e568bde6e6eca15477eaa10b5c91c91c5a4
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56835553"
---
# <a name="xml-processing-options"></a>XML 처리 옵션
XML 데이터를 처리하는 데 사용할 수 있는 Microsoft 기술 목록은 다음 표를 참조하세요.  
  
## <a name="net-framework-options"></a>.NET Framework 옵션  
  
|**옵션**|**처리 유형**|**설명**|  
|----------------|-------------------------|---------------------|  
|[LINQ to XML(C#)](../../../csharp/programming-guide/concepts/linq/linq-to-xml.md) <br/> [LINQ to XML(Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md) <br />(<xref:System.Xml.Linq> 네임스페이스)|메모리 내|- .NET Framework LINQ(Language-Integrated Query) 기술을 기반으로 합니다.<br />- 개체, 관계형 데이터 및 XML 데이터에 대해 SQL과 유사한 쿼리 경험을 제공합니다.<br />- 직관적인 문서 작성 및 변환 기능을 제공합니다.<br />- 새 코드를 작성 중인 경우 이 옵션을 사용합니다.|  
|<xref:System.Xml.XmlReader?displayProperty=nameWithType>|스트림 기반|- 캐시를 사용하지 않고 앞으로만 이동 가능한 빠른 XML 데이터 액세스 방법을 제공합니다.<br />- <xref:System.Xml.XmlReader.Create%2A?displayProperty=nameWithType> 메서드를 사용하여 개체를 만들고 <xref:System.Xml.XmlReaderSettings> 클래스를 사용하여 개체에서 활성화할 기능 집합을 지정할 수 있습니다.|  
|<xref:System.Xml.XmlWriter?displayProperty=nameWithType>|스트림 기반|- 캐시를 사용하지 않고 앞으로만 이동 가능한 빠른 XML 데이터 생성 방법을 제공합니다.<br />- <xref:System.Xml.XmlWriter.Create%2A?displayProperty=nameWithType> 메서드를 사용하여 개체를 만들고 <xref:System.Xml.XmlWriterSettings> 클래스를 사용하여 개체에서 활성화할 기능 집합을 지정할 수 있습니다.|  
|<xref:System.Xml.XmlDocument?displayProperty=nameWithType>|메모리 내|- [W3C DOM(문서 개체 모델) Level 1 Core](https://www.w3.org/TR/REC-DOM-Level-1/level-one-core.html) 및 [DOM Level 2 Core](https://www.w3.org/TR/DOM-Level-2-Core/) 권장 사항을 구현합니다.<br />- 익숙한 DOM 모델을 기반으로 한 메서드 및 속성을 사용하여 노드를 생성, 삽입, 제거 및 수정할 수 있습니다.<br />- W3C DOM을 사용하는 기존 코드를 수정 중인 경우 이 옵션을 사용합니다.|  
|<xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType>|메모리 내|- 커서 모델을 사용하는 몇 가지 편집 옵션 및 탐색 기능을 제공합니다.<br />- XML 문서는 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체에 포함될 수 있습니다.<br />- XML의 읽기 전용 처리에 우수한 성능을 제공합니다.<br />- XPath 쿼리 또는 XSLT 변환이 포함된 기존 코드를 수정 중인 경우 이 옵션을 사용합니다.|  
|<xref:System.Xml.Xsl.XslCompiledTransform>|메모리 내|- XSL 변환을 사용하여 XML 데이터를 변형하는 옵션을 제공합니다.<br />- [XSLT 컴파일러(xsltc.exe)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)를 사용하여 앱에서 미리 컴파일된 변환을 참조할 수 있습니다.|  
  
## <a name="win32-and-com-based-options"></a>Win32 및 COM 기반 옵션  
  
|**옵션**|**설명**|  
|----------------|---------------------|  
|[XmlLite](https://docs.microsoft.com/previous-versions/windows/desktop/ms752872(v=vs.85))|- 빠르고 안전하며 캐시를 사용하지 않고 앞으로만 이동 가능한 XML 파서로서, 고성능의 XML 앱을 빌드할 수 있도록 도움을 줍니다.<br />- DLL(동적 연결 라이브러리)을 사용할 수 있는 모든 언어에서 사용할 수 있습니다. C++ 사용을 권장합니다.|  
|[MSXML](https://docs.microsoft.com/previous-versions/windows/desktop/ms763742(v=vs.85))|- Windows 운영 체제에 포함된 XML을 처리할 수 있는 COM 기반 기술입니다.<br />- XPath 및 XSLT를 지원하는 DOM의 네이티브 구현을 제공합니다.<br />- SAX2 이벤트 기반 파서가 포함되어 있습니다.|  
  
## <a name="see-also"></a>참고 항목

- [DOM 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XSLT 컴파일러(xsltc.exe)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)
