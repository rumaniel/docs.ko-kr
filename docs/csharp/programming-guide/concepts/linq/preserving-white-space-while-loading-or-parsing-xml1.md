---
title: XML을 로드 또는 구문 분석할 때 공백 유지
ms.date: 07/20/2015
ms.assetid: f3ff58c4-55aa-4fcd-b933-e3a2ee6e706c
ms.openlocfilehash: d015c21813df2224356bb49212fe282fa5372d03
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591545"
---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>XML을 로드 또는 구문 분석할 때 공백 유지
이 항목에서는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 공백 동작을 제어하는 방법에 대해 설명합니다.  
  
 일반적인 시나리오는 들여쓴 XML을 읽고 공백 텍스트 노드 없이 메모리 내 XML 트리를 만든 다음(공백을 유지하지 않음) XML에 대한 작업을 수행하고 들여쓰기를 사용하여 XML을 저장하는 것입니다. 서식이 있는 XML을 serialize하는 경우 XML 트리의 유효 공백만 유지됩니다. 이것이 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]의 기본 동작입니다.  
  
 다른 일반적인 시나리오는 이미 의도적으로 들여쓴 XML을 읽고 수정하는 것입니다. 이 들여쓰기를 변경하려고 하지 않을 수 있습니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 XML을 로드하거나 구문 분석할 때 공백을 유지하고 XML을 serialize할 때 서식을 해제하는 경우 이렇게 할 수 있습니다.  
  
 이 항목에서는 XML 트리를 채우는 메서드의 공백 동작에 대해 설명합니다. XML 트리를 serialize할 때 공백을 제어하는 방법에 대한 자세한 내용은 [serialize할 때 공백 유지](./preserving-white-space-while-serializing.md)를 참조하세요.  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>XML 트리를 채우는 메서드의 동작  
 <xref:System.Xml.Linq.XElement> 및 <xref:System.Xml.Linq.XDocument> 클래스의 다음 메서드는 XML 트리를 채웁니다. 파일, <xref:System.IO.TextReader>, <xref:System.Xml.XmlReader> 또는 문자열에서 XML 트리를 채울 수 있습니다.  
  
- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>  
  
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>  
  
 메서드에서 <xref:System.Xml.Linq.LoadOptions>를 인수로 사용하지 않는 경우 무효 공백을 유지하지 않습니다.  
  
 대부분의 경우 메서드에서 <xref:System.Xml.Linq.LoadOptions>를 인수로 사용하면 XML 트리의 텍스트 노드로 무효 공백을 선택적으로 유지할 수 있습니다. 그러나 메서드가 <xref:System.Xml.XmlReader>에서 XML을 로드하는 경우에는 <xref:System.Xml.XmlReader>가 공백을 유지할지 여부를 결정합니다. <xref:System.Xml.Linq.LoadOptions.PreserveWhitespace>를 설정해도 아무런 영향을 주지 않습니다.  
  
 이러한 메서드를 사용하는 경우 공백이 유지되면 무효 공백이 XML 트리에 <xref:System.Xml.Linq.XText> 노드로 삽입됩니다. 공백이 유지되지 않으면 텍스트 노드가 삽입되지 않습니다.  
  
 <xref:System.Xml.XmlWriter>를 사용하여 XML 트리를 만들 수 있습니다. <xref:System.Xml.XmlWriter>에 쓴 노드가 트리에 채워집니다. 그러나 이 메서드를 사용하여 XML 트리를 빌드하면 노드가 공백인지 여부나 유효한지 여부에 관계없이 모든 노드가 유지됩니다.  
  