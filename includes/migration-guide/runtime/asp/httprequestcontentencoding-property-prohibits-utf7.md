---
ms.openlocfilehash: 668d047d3247d64cb1400d4a9ea6887795fa0d44
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804561"
---
### <a name="httprequestcontentencoding-property-prohibits-utf7"></a>HttpRequest.ContentEncoding 속성에 UTF7이 금지됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 <xref:System.Web.HttpRequest?displayProperty=name>의 본문에 UTF-7 인코딩이 금지됩니다. 경우에 따라 UTF-7 수신 데이터에 종속되는 애플리케이션 데이터가 제대로 디코딩되지 않습니다.|
|제안 해결 방법|이상적으로는 <xref:System.Web.HttpRequest?displayProperty=name>에서 인코딩 UTF-7을 사용하지 않도록 애플리케이션을 업데이트해야 합니다. 대신에 [appSettings](~/docs/framework/configure-apps/file-schema/appsettings/appsettings-element-for-configuration.md) 요소의 <code>aspnet:AllowUtf7RequestContentEncoding</code> 특성을 사용하여 레거시 동작을 복원할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Web.HttpRequest.ContentEncoding?displayProperty=nameWithType></li></ul>|
