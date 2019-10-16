---
ms.openlocfilehash: 2c54912e5c29b2ed8f4c8163550050e12e367263
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857483"
---
### <a name="signedxml-and-encryptedxml-breaking-changes"></a>SignedXml 및 EncryptedXml 주요 변경 내용

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2에서는 <xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=name> 및 <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=name>의 보안 수정으로 인해 런타임 동작이 달라집니다. 예를 들면 다음과 같습니다.<ul><li>문서에 동일한 <code>id</code> 특성을 가진 요소가 여러 개 있고 서명에서 해당 요소 중 하나를 서명 루트로 사용하는 경우, 이제는 문서가 잘못된 것으로 간주됩니다.</li><li>참조에서 비표준 XPath 변환 알고리즘을 사용하는 문서는 현재 잘못된 것으로 간주됩니다.</li><li>참조에서 비표준 XSLT 변환 알고리즘을 사용하는 문서는 현재 잘못된 것으로 간주합니다.</li><li>외부 리소스 분리 서명을 사용하는 모든 프로그램은 그렇게 할 수 없습니다.</li></ul>|
|제안|개발자는 <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> 및 <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform>과 <xref:System.Security.Cryptography.Xml.Transform>에서 파생된 형식의 사용을 검토해야 합니다. 문서 수신기가 이러한 사용을 처리하지 못할 수도 있기 때문입니다.|
|범위|부|
|버전|4.6.2|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Security.Cryptography.Xml.Transform?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.XmlDsigXPathTransform?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform?displayProperty=nameWithType></li></ul>|

