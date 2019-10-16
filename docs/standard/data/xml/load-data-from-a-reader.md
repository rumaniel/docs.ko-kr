---
title: 판독기에서 데이터 로드
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 7e74918c-bc72-4977-a49b-e1520a6d8f60
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e4b789a23b790757ce2dfaa82b6eaec7fdaf3cb3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647879"
---
# <a name="load-data-from-a-reader"></a>판독기에서 데이터 로드
<xref:System.Xml.XmlDocument.Load%2A> 메서드와 <xref:System.Xml.XmlReader>의 매개 변수를 사용하여 XML 문서를 로드할 경우 발생하는 동작은 다른 형식의 데이터를 로드할 때의 동작과 차이가 있습니다. 판독기가 초기 상태에 있을 경우 <xref:System.Xml.XmlDocument.Load%2A>는 판독기의 전체 내용을 사용하며 판독기의 모든 데이터를 사용하여 XML DOM(문서 개체 모델)을 만듭니다.  
  
 판독기가 이미 문서의 노드에 있으며 <xref:System.Xml.XmlDocument.Load%2A> 메서드에 전달된 경우 <xref:System.Xml.XmlDocument.Load%2A>는 메모리로 현재 노드 및 현재 수준을 닫는 끝 태그에 이를 때까지의 모든 형제를 읽으려고 시도합니다. <xref:System.Xml.XmlDocument.Load%2A>는 판독기의 XML이 제대로 구성되었는지 확인하므로 시도한 <xref:System.Xml.XmlDocument.Load%2A>는 로드를 시도할 때 판독기가 위치한 노드에 따라 성공 여부가 결정됩니다. XML이 제대로 구성되지 않은 경우 <xref:System.Xml.XmlDocument.Load%2A>는 예외를 throw합니다. 예를 들어, 다음 노드 집합에는 루트 수준 요소 두 개가 포함되어 있으며 XML이 제대로 구성되지 않았으므로 <xref:System.Xml.XmlDocument.Load%2A>는 예외를 throw합니다.  
  
- Comment 노드, Element 노드, Element 노드, EndElement 노드가 차례로 있는 노드 집합  
  
 다음 노드 집합에는 루트 수준 요소가 없으므로 불완전한 DOM을 만듭니다.  
  
- Comment 노드, ProcessingInstruction 노드, Comment 노드, EndElement 노드가 차례로 있는 노드 집합  
  
 이 경우 예외가 throw되지 않으며 데이터가 로드됩니다. 이러한 노드 위에 루트 요소를 추가할 수 있으며 제대로 구성된 XML을 만들어 오류 없이 저장할 수 있습니다.  
  
 reade가 문서의 루트 수준(예: 공백 또는 특성 노드)에 대해 유효하지 않은 리프 노드에 배치된 경우 reader는 루트에 사용할 수 있는 노드에 배치될 때까지 계속 읽습니다. 이때 문서가 로드되기 시작합니다.  
  
 기본적으로 <xref:System.Xml.XmlDocument.Load%2A>는 DTD(문서 종류 정의) 또는 스키마 유효성 검사를 통해 XML이 유효한지 확인하지 않으며 XML이 제대로 구성되었는지만 확인합니다. 유효성 검사를 실행하려면 <xref:System.Xml.XmlReader> 클래스를 사용하여 <xref:System.Xml.XmlReaderSettings>를 만들어야 합니다. <xref:System.Xml.XmlReader> 클래스가 DTD 또는 XSD(스키마 정의 언어) 스키마를 사용하여 유효성 검사를 실행할 수 있습니다. <xref:System.Xml.ValidationType> 클래스의 <xref:System.Xml.XmlReaderSettings> 속성은 <xref:System.Xml.XmlReader> 인스턴스에서 유효성 검사를 실행할지 여부를 결정합니다. XML 데이터 유효성 검사에 대한 자세한 내용은 <xref:System.Xml.XmlReader> 참조 페이지의 설명 섹션을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
