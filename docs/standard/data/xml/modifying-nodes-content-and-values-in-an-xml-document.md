---
title: XML 문서에서 노드, 내용 및 값 수정
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 761773e0-db72-4986-b9f5-a522213d8397
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 976c34d72f9fcc89193658e50727a0ad365f2dd8
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647883"
---
# <a name="modifying-nodes-content-and-values-in-an-xml-document"></a>XML 문서에서 노드, 내용 및 값 수정
여러 가지 방법으로 문서에서 노드와 내용을 수정할 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.  
  
- <xref:System.Xml.XmlNode.Value%2A> 속성을 사용하여 노드 값을 변경할 수 있습니다.  
  
- 노드를 새 노드로 바꿔 전체 노드 집합을 수정할 수 있습니다. 이 작업은 <xref:System.Xml.XmlNode.InnerXml%2A> 속성을 사용하여 수행합니다.  
  
- <xref:System.Xml.XmlNode.RemoveChild%2A> 메서드를 사용하여 기존 노드를 새 노드로 바꿀 수 있습니다.  
  
- <xref:System.Xml.XmlCharacterData>, <xref:System.Xml.XmlCharacterData.AppendData%2A> 또는 <xref:System.Xml.XmlCharacterData.InsertData%2A> 메서드를 사용하여 <xref:System.Xml.XmlCharacterData.ReplaceData%2A> 클래스에서 상속된 노드에 문자를 추가할 수 있습니다.  
  
- <xref:System.Xml.XmlCharacterData.DeleteData%2A>에서 상속된 노드 형식에서 <xref:System.Xml.XmlCharacterData> 메서드로 문자 범위를 제거하여 내용을 수정할 수 있습니다.  
  
 `node.Value = "new value";`를 사용하면 쉽게 노드 값을 변경할 수 있습니다. 다음 표에서는 이 한 줄 코드를 사용할 수 있는 노드 형식 및 이 노드 형식에 대해 변경되는 데이터를 보여 줍니다.  
  
|노드 형식|변경되는 데이터|  
|---------------|------------------|  
|특성|특성 값|  
|CDATASection|CDATASection 내용|  
|주석|주석의 내용입니다.|  
|ProcessingInstruction|대상을 제외한 내용|  
|텍스트|텍스트 내용|  
|XmlDeclaration|`<?xml` 및 `?>` 태그를 제외한 선언 내용|  
|Whitespace|공백 값. 인식된 XML 공백 문자인 공백, 탭, CR 또는 LF 중 하나로 값을 설정할 수 있습니다.|  
|SignificantWhitespace|유효 공백 값. 인식된 XML 공백 문자인 공백, 탭, CR 또는 LF 중 하나로 값을 설정할 수 있습니다.|  
  
 이 표에 나열되지 않은 노드 형식은 값을 설정하기에 적합한 노드 형식이 아닙니다. 다른 노드 형식에서 값을 설정하면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
 <xref:System.Xml.XmlNode.InnerXml%2A> 속성은 현재 노드의 자식 노드 태그를 변경합니다. 이 속성을 설정하면 자식 노드가 지정된 문자열의 구문 분석된 내용으로 바뀝니다. 현재 네임스페이스 컨텍스트에서 구문 분석이 수행됩니다. 또한 <xref:System.Xml.XmlNode.InnerXml%2A>은 중복 네임스페이스 선언을 제거합니다. 결과적으로 복사 및 붙여넣기를 여러 번 실행해도 중복 네임스페이스 선언으로 인해 문서 크기가 증가하지 않습니다. <xref:System.Xml.XmlNode.InnerXml%2A> 작업에서 네임스페이스의 결과를 보여 주는 코드 예제는 <xref:System.Xml.XmlDocument.InnerXml%2A> 속성을 참조하세요.  
  
 <xref:System.Xml.XmlCharacterData.ReplaceData%2A> 및 <xref:System.Xml.XmlNode.RemoveChild%2A> 메서드를 사용하는 경우 이 메서드는 바뀌거나 제거된 노드를 반환합니다. 그러면 이 노드를 XML DOM(문서 개체 모델)에 다시 삽입할 수 있습니다. <xref:System.Xml.XmlCharacterData.ReplaceData%2A> 메서드는 문서에 삽입하는 노드에서 두 가지 유효성 검사를 수행합니다. 첫 번째 검사에서 노드가 해당 형식의 자식 노드를 가질 수 있는 노드의 자식이 되는지 확인합니다. 두 번째 검사에서 삽입하는 노드가 부모가 될 노드의 상위 노드가 아닌지 확인합니다. 이러한 조건을 하나라도 위반하면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
 편집할 수 있는 노드에서 읽기 전용 자식을 추가하거나 제거할 수 있습니다. 그러나 읽기 전용 노드 자체를 수정하려고 시도하면 <xref:System.InvalidOperationException>이 throw됩니다. 이에 관한 예제는 <xref:System.Xml.XmlEntityReference> 노드의 자식을 수정하는 것입니다. 자식은 읽기 전용이며 수정할 수 없습니다. 자식을 수정하려고 시도하면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
