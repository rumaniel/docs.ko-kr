---
ms.openlocfilehash: 2dd97fcce13ed1ac7baf4cd02f5881d31d7a9c4b
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804525"
---
### <a name="xslt-forward-compat-now-works"></a>XSLT forward compat가 이제 작동합니다.

|   |   |
|---|---|
|설명|.NET Framework 4에서 XSLT 1.0 이후 버전과의 호환성에 다음과 같은 문제가 있었습니다.<ul><li>버전이 2.0으로 설정되고 인식할 수 없는 XSLT 1.0 구문에서 파서가 발생하면 스타일시트를 로드하지 못했습니다.</li><li>스타일시트 버전이 1.1로 설정된 경우 <code>xsl:sort</code> 구문이 데이터를 정렬하지 못했습니다.</li></ul>.NET Framework 4.5에서 이러한 문제가 해결되었고 XSLT 1.0의 다음 버전과의 호환성 모드는 제대로 작동합니다.|
|제안 해결 방법|대부분의 앱은 영향을 받지 않지만 xsl:sort가 적용되어 일부 경우에 데이터가 다른 방식으로 정렬됩니다. 1.1 스타일 시트에서 <code>xsl:sort</code>를 사용하는 경우 앱이 정렬되지 않은 데이터 순서에 의존하고 있지 않은지 확인하세요. 앱이 4.0 정렬 동작에 의존하면 스타일 시트에서 <code>xsl:sort</code>를 제거합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Xml.Xsl.XslCompiledTransform?displayProperty=nameWithType></li></ul>|
