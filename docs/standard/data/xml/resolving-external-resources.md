---
title: 외부 리소스 확인
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: ad3fa320-4b8f-4e5c-b549-01157591007a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b4ba0cbb25e2c83a33ffba99ccbb29d5b414b3c1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918199"
---
# <a name="resolving-external-resources"></a>외부 리소스 확인
**XmlDocument** 클래스는 **XmlDocument**의 **XmlResolver** 속성을 사용하여 외부 DTD(문서 종류 정의), 엔터티 및 스키마와 같이 XML 데이터에 인라인으로 들어 있지 않은 리소스를 찾습니다. 이러한 항목은 네트워크나 로컬 드라이브에 있을 수 있으며 URI(Uniform Resource Identifier)로 식별할 수 있습니다. 따라서 **XmlDocument**로 문서에 있는 **EntityReference** 노드를 확인하고 외부 DTD나 스키마에 따라 문서의 유효성을 검사할 수 있습니다.  
  
## <a name="fully-trusted-xmldocument"></a>완전 신뢰 XmlDocument  
 **XmlResolver** 속성은 **XmlDocument.Load** 메서드의 기능에 영향을 줍니다. 다음 표에서는 **XmlDocument** 개체가 완전히 신뢰될 때 **XmlDocument.XmlResolver** 속성이 작동하는 방식을 보여줍니다. 다음 표에서는 Load의 입력이 **TextReader**, **String**, **Stream** 또는 **URI**일 경우의 **XmlDocument.Load** 메서드를 보여줍니다. **XmlDocument**를 **XmlReader**에서 로드할 경우 이 표의 내용이 **Load** 메서드에 적용되지 않습니다.  
  
|XmlResolver 속성|함수|참고 사항|  
|--------------------------|--------------|-----------|  
|속성은 이전에 생성되었으며 사용자가 이미 속성을 설정한**XmlResolver** 클래스로 설정됩니다.|**XmlDocument**는 파일 이름을 확인하고 DTD, 엔터티, 스키마 등의 외부 리소스에 대한 참조를 확인하기 위해 제공되는 **XmlResolver**를 사용합니다.<br /><br /> **XmlDocument**에서 노드를 추가하거나 편집할 때 필요한 외부 리소스를 확인할 때도 **XmlResolver**가 사용됩니다.|**XmlDocument**에 제공된 **XmlResolver**는 외부 리소스를 찾아 확인해야 할 때마다 사용되는 확인자입니다.|  
|이 속성은 **null**(Microsoft Visual Basic .NET에서는 **Nothing**)로 설정됩니다.|외부 스키마나 DTD를 찾는 등 외부 리소스가 필요한 기능은 지원되지 않습니다. 외부 엔터티는 확인되지 않으며 확인이 필요한 entity 노드의 삽입과 같은 편집 기능도 수행되지 않습니다.|**XmlDocument**는 파일을 익명으로 로드하며 다른 리소스를 확인하려고 하지 않습니다.|  
|속성이 설정되지 않았지만 기본 상태를 유지하고 있습니다.|NULL 자격 증명을 갖는 **XmlUrlResolver**는 파일 이름을 확인하고, 외부 DTD, 엔터티 및 스키마를 찾을 때 **XmlDocument**에 의해 인스턴스화되어 사용되며 노드를 편집할 때는 **null** 자격 증명이 사용됩니다.||  
  
 다음 표에서는 **Load**의 입력이 **XmlReader**이며 **XmlDocument**가 완전히 신뢰될 때의 **XmlDocument.Load** 메서드를 보여줍니다.  
  
|XmlResolver 속성|함수|참고 사항|  
|--------------------------|--------------|-----------|  
|**XmlDocument**에서 사용하는 **XmlResolver** 클래스는 **XmlReader**에서 사용하는 것과 동일한 클래스입니다.|**XmlDocument**는 **XmlReader**에 할당된 **XmlResolver**를 사용합니다.<br /><br /> **XmlDocument.Resolver** 속성은 **XmlReader**에서 **XmlResolver**를 가져오므로 **XmlDocument** 신뢰 수준에 상관없이 설정할 수 없습니다. **XmlDocument**의 **XmlResolver** 속성을 설정하여 **XmlReader**의 **XmlResolver** 설정을 재정의할 수 없습니다.|**XmlReader**는 **XmlTextReader**, **XmlValidatingReader** 또는 사용자가 작성한 판독기일 수 있습니다. 사용되는 판독기가 엔터티 확인을 지원하면 외부 엔터티가 확인됩니다. 전달된 판독기가 엔터티 참조를 지원하지 않으면 엔터티 참조는 확인되지 않습니다.|  
  
## <a name="semi-trusted-xmldocument"></a>일부 신뢰된 XmlDocument  
 다음 표에서는 개체가 일부 신뢰될 때 **XmlDocument.XmlResolver** 속성이 작동하는 방식을 보여줍니다. 이 표는 Load의 입력이 **TextReader**, **String**, **Stream** 또는 **URI**일 경우의 **XmlDocument.Load** 메서드에 해당합니다. **XmlDocument**를 **XmlReader**에서 로드할 경우 이 표의 내용이 **Load** 메서드에 적용되지 않습니다.  
  
|XmlResolver 속성|함수|참고 사항|  
|--------------------------|--------------|-----------|  
|일부 신뢰된 시나리오에서는 **XmlResolver** 속성을 null 이외의 값으로 설정할 수 없습니다.|**null** 자격 증명을 갖는 **XmlUrlResolver**는 파일 이름을 확인하고, 외부 DTD, 엔터티 및 스키마를 찾을 때 **XmlDocument**에 의해 인스턴스화되어 사용되며 노드를 편집할 때는 **null** 자격 증명이 사용됩니다.|이 동작은 **XmlResolver** 속성이 설정되어 있지 않지만 기본값 상태로 남아 있을 때의 동작과 동일합니다.<br /><br /> **XmlDocument**는 모든 작업에 대해 익명 권한을 사용합니다.|  
|이 속성은 **null**(Microsoft Visual Basic .NET에서는 **Nothing**)로 설정됩니다.|외부 스키마나 DTD를 찾는 등 외부 리소스가 필요한 기능은 지원되지 않습니다. 외부 엔터티는 확인되지 않으며 확인이 필요한 entity 노드의 삽입과 같은 편집 기능도 수행되지 않습니다.|속성이 **null**이면 **XmlDocument**가 완전히 신뢰되거나 일부 신뢰되거나에 상관없이 동일한 동작이 수행됩니다.|  
|속성이 설정되지 않았지만 기본 상태를 유지하고 있습니다.|**null** 자격 증명을 갖는 **XmlUrlResolver**는 파일 이름을 확인하고, 외부 DTD, 엔터티 및 스키마를 찾을 때 **XmlDocument**에 의해 인스턴스화되어 사용되며 노드를 편집할 때는 **null** 자격 증명이 사용됩니다.|**XmlDocument**는 모든 작업에 대해 익명 권한을 사용합니다.|  
  
 이 표는 **Load**의 입력이 **XmlReader**이며 **XmlDocument**가 일부 신뢰될 때의 **XmlDocument.Load** 메서드에 해당합니다.  
  
|XmlResolver 속성|함수|참고 사항|  
|--------------------------|--------------|-----------|  
|**XmlDocument**에서 사용하는 **XmlResolver** 클래스는 **XmlReader**에서 사용하는 것과 동일한 클래스입니다.|**XmlDocument**는 **XmlReader**에 할당된 **XmlResolver**를 사용합니다.<br /><br /> **XmlDocument.Resolver** 속성은 **XmlReader**에서 **XmlResolver**를 가져오므로 **XmlDocument** 신뢰 수준에 상관없이 설정할 수 없습니다. **XmlDocument**의 **XmlResolver** 속성을 설정하여 **XmlReader**의 **XmlResolver** 설정을 재정의할 수 없습니다.|**XmlReader**는 **XmlTextReader**, 유효성을 검사하는 <xref:System.Xml.XmlReader> 또는 사용자가 작성한 판독기일 수 있습니다. 사용되는 판독기가 엔터티 확인을 지원하면 외부 엔터티가 확인됩니다. 전달된 판독기가 엔터티 참조를 지원하지 않으면 엔터티 참조는 확인되지 않습니다.|  
  
 XmlResolver가 정확한 자격 증명을 갖도록 설정하면 외부 리소스에 액세스할 수 있습니다.  
  
> [!NOTE]
> **XmlResolver** 속성을 검색하는 방법은 없습니다. 따라서 사용자는 자격 증명이 설정된 **XmlResolver**를 다시 사용할 수 없습니다. 또한 **XmlTextReader**나 유효성을 검사하는 <xref:System.Xml.XmlReader>가 **XmlDocument**를 로드하는 데 사용되고 **XmlDocument**에 설정된 확인자가 있는 경우에도 보안 문제가 있기 때문에 **Load** 단계 이후에 **XmlDocument**에서 이러한 판독기의 확인자를 캐시하지 않습니다.  
  
 자세한 내용은 <xref:System.Xml.XmlResolver> 참조 페이지의 설명 섹션을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
