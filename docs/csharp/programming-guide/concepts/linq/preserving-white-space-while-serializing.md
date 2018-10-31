---
title: 직렬화할 때 공백 유지3
ms.date: 07/20/2015
ms.assetid: 0c4f8b98-483b-4cf8-86be-fa146eef90dc
ms.openlocfilehash: 7fd0a38d2a9ed8c4712b8e9a03a24a23b408f38a
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48032363"
---
# <a name="preserving-white-space-while-serializing"></a>serialize할 때 공백 유지
이 항목에서는 XML 트리를 serialize할 때 공백을 제어하는 방법에 대해 설명합니다.  
  
 일반적인 시나리오는 들여쓴 XML을 읽고 공백 텍스트 노드 없이 메모리 내 XML 트리를 만든 다음(공백을 유지하지 않음), XML에 대한 작업을 수행하고 들여쓰기를 사용하여 XML을 저장하는 것입니다. 서식이 있는 XML을 serialize하는 경우 XML 트리의 유효 공백만 유지됩니다. 이것이 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 기본 동작입니다.  
  
 다른 일반적인 시나리오는 이미 의도적으로 들여쓴 XML을 읽고 수정하는 것입니다. 이 들여쓰기를 변경하려고 하지 않을 수 있습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 XML을 로드하거나 구문 분석할 때 공백을 유지하고 XML을 serialize할 때 서식을 해제하는 경우 이렇게 할 수 있습니다.  
  
## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a>XML 트리를 직렬화하는 메서드의 공백 동작  
 <xref:System.Xml.Linq.XElement> 및 <xref:System.Xml.Linq.XDocument> 클래스의 다음 메서드는 XML 트리를 serialize합니다. XML 트리를 파일, <xref:System.IO.TextReader> 또는 <xref:System.Xml.XmlReader>로 serialize할 수 있습니다. `ToString` 메서드는 문자열로 serialize합니다.  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType>  
  
-   <xref:System.Xml.Linq.XElement.ToString%2A?displayProperty=nameWithType>  
  
-   <xref:System.Xml.Linq.XDocument.ToString%2A?displayProperty=nameWithType>  
  
 이 메서드는 <xref:System.Xml.Linq.SaveOptions>를 인수로 사용하지 않는 경우 serialize된 XML의 서식을 지정합니다(들여씁니다). 이 경우 XML 트리의 모든 무효 공백이 삭제됩니다.  
  
 이 메서드가 <xref:System.Xml.Linq.SaveOptions>를 인수로 사용하는 경우에는 serialize된 XML의 서식을 지정하지(들여쓰지) 않도록 지정할 수 있습니다. 이 경우 XML 트리의 모든 공백이 유지됩니다.  
  
## <a name="see-also"></a>참고 항목

- [XML 트리 serialize(C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
