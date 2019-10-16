---
title: 한 문서에서 다른 문서로 기존 노드 복사
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 3caa78c1-3448-4b7b-b83c-228ee857635e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e08c86ebdd71746520085844de5743692e84640e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965925"
---
# <a name="copying-existing-nodes-from-one-document-to-another"></a>한 문서에서 다른 문서로 기존 노드 복사
**ImportNode** 메서드는 **XmlDocument** 간에 하나의 노드나 전체 노드 하위 트리를 복사하는 메커니즘입니다. 호출에서 반환되는 노드는 특성 값, 노드 이름, 노드 형식과 접두사, 로컬 이름, 네임스페이스 URI(Uniform Resource Identifier)와 같은 모든 네임스페이스 관련 특성이 포함된 소스 문서의 노드 복사본입니다. 소스 문서는 변경되지 않습니다. 노드를 가져온 후에 계속해서 노드 삽입에 사용되는 메서드 중 하나를 사용하여 트리에 해당 노드를 추가해야 합니다.  
  
 노드가 새 문서에 추가되면 새 문서가 해당 노드를 소유하게 됩니다. 이것은 노드가 별도의 문서 조각에서 만들어진 경우에도 만들어진 각 노드를 소유하는 문서가 있어야 하기 때문입니다. 이는 XML DOM(문서 개체 모델)의 요구 사항이며 **XmlDocument** 클래스에 대한 팩터리 생성 디자인에 의해 적용됩니다. 예를 들어 **CreateElement**는 새 노드를 만드는 유일한 방법입니다.  
  
 가져온 노드의 노드 형식과 *deep* 매개 변수의 값에 따라 해당하는 추가 정보가 복사됩니다. 이 메서드는 XML에 대한 두 문서의 DTD(문서 종류 정의)가 서로 다를 수 있다는 가정 하에, XML이나 HTML 소스의 조각을 한 문서에서 다른 문서로 복사했을 경우에 예상되는 동작을 미러링합니다.  
  
 다음 표에서는 가져올 수 있는 각 노드 형식에 대한 관련 동작을 설명합니다.  
  
|노드 형식|*deep* 매개 변수가 true인 경우|*deep* 매개 변수가 false인 경우|  
|---------------|------------------------------|-------------------------------|  
|XmlAttribute|<xref:System.Xml.XmlAttribute.Specified%2A>가 XmlAttribute에서 **true**로 설정됩니다. 소스 **XmlAttribute**의 하위 항목을 재귀적으로 가져오고 결과 노드를 다시 조합하여 해당하는 하위 트리를 구성합니다.|**XmlAttribute** 노드를 가져오면 항상 자식 노드가 동반되기 때문에 *deep* 매개 변수가 적용되지 않습니다.|  
|XmlCDataSection|해당 데이터를 포함하여 노드를 복사합니다.|해당 데이터를 포함하여 노드를 복사합니다.|  
|XmlComment|해당 데이터를 포함하여 노드를 복사합니다.|해당 데이터를 포함하여 노드를 복사합니다.|  
|XmlDocumentFragment|소스 노드의 하위 항목을 재귀적으로 가져오고 결과 노드를 다시 조합하여 해당하는 하위 트리를 구성합니다.|빈 **XmlDocumentFragment**가 생성됩니다.|  
|XmlDocumentType|해당 데이터를 포함하여 노드를 복사합니다.*|해당 데이터를 포함하여 노드를 복사합니다.*|  
|XmlElement|소스 요소의 하위 항목을 재귀적으로 가져오고 결과 노드를 다시 조합하여 해당하는 하위 트리를 구성합니다. **참고:**  기본 특성이 복사되지 않습니다. 가져오고 있는 문서에 이 요소 이름에 대한 기본 특성이 정의되어 있는 경우 이 특성이 할당됩니다.|소스 요소의 지정된 특성 노드를 가져오고, 생성된 **XmlAttribute** 노드가 새 요소에 연결됩니다. 하위 노드는 복사되지 않습니다. **참고:**  기본 특성이 복사되지 않습니다. 가져오고 있는 문서에 이 요소 이름에 대한 기본 특성이 정의되어 있는 경우 이 특성이 할당됩니다.|  
|XmlEntityReference|소스와 대상 문서가 다르게 정의된 엔터티를 가질 수 있으므로 이 메서드에서는 **XmlEntityReference** 노드만 복사합니다. 대체 텍스트는 포함되지 않습니다. 대상 문서에 엔터티가 정의되어 있는 경우 해당 값이 할당됩니다.|소스와 대상 문서가 다르게 정의된 엔터티를 가질 수 있으므로 이 메서드에서는 **XmlEntityReference** 노드만 복사합니다. 대체 텍스트는 포함되지 않습니다. 대상 문서에 엔터티가 정의되어 있는 경우 해당 값이 할당됩니다.|  
|XmlProcessingInstruction|가져온 노드에서 대상과 데이터 값을 복사합니다.|가져온 노드에서 대상과 데이터 값을 복사합니다.|  
|XmlText|해당 데이터를 포함하여 노드를 복사합니다.|해당 데이터를 포함하여 노드를 복사합니다.|  
|XmlSignificantWhitespace|해당 데이터를 포함하여 노드를 복사합니다.|해당 데이터를 포함하여 노드를 복사합니다.|  
|XmlWhitespace|해당 데이터를 포함하여 노드를 복사합니다.|해당 데이터를 포함하여 노드를 복사합니다.|  
|XmlDeclaration|가져온 노드에서 대상과 데이터 값을 복사합니다.|가져온 노드에서 대상과 데이터 값을 복사합니다.|  
|기타 모든 노드 형식|이 노드 형식은 가져올 수 없습니다.|이 노드 형식은 가져올 수 없습니다.|  
  
> [!NOTE]
> 여러 개의 DocumentType 노드를 가져올 수는 있지만 한 문서는 오직 하나의 DocumentType만 포함할 수 있습니다. 따라서 문서 형식을 가져온 후에는 트리에 삽입하기 전에 문서에 문서 형식이 없는지 확인해야 합니다. 노드 제거에 대한 자세한 내용은 [XML 문서에서 노드, 내용 및 값 제거](../../../../docs/standard/data/xml/removing-nodes-content-and-values-from-an-xml-document.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
