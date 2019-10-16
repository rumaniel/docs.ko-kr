---
ms.openlocfilehash: a5b3e325c13d2f56532ebc6ebb5c259d565a4952
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379576"
---
### <a name="xmlschemaexception-now-sets-line-positions-properly"></a>XmlSchemaException이 줄 위치를 제대로 설정

|   |   |
|---|---|
|세부 정보|<xref:System.Xml.Linq.LoadOptions.SetLineInfo> 값을 Load 메서드에 전달하고 유효성 검사 오류가 발생한 경우 <xref:System.Xml.Schema.XmlSchemaException.LineNumber> 및 <xref:System.Xml.Schema.XmlSchemaException.LinePosition> 속성은 이제 줄 정보를 포함합니다.|
|제안 해결 방법|XML을 로드하는 동안 SetLineInfo를 사용할 때 이러한 속성이 이제 제대로 설정되므로 <xref:System.Xml.Schema.XmlSchemaException.LineNumber> 및 <xref:System.Xml.Schema.XmlSchemaException.LinePosition>이 설정되지 않는다고 가정하는 예외 처리 코드를 업데이트해야 합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Xml.Linq.LoadOptions.SetLineInfo?displayProperty=nameWithType></li></ul>|
