---
ms.openlocfilehash: dfc1a0d05142861ff1c1b7391126d86e09fa71c0
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804610"
---
### <a name="webutilityhtmldecode-no-longer-decodes-invalid-input-sequences"></a>WebUtility.HtmlDecode는 잘못된 입력 시퀀스를 더 이상 디코딩하지 않습니다.

|   |   |
|---|---|
|설명|기본적으로 디코딩 메서드는 더 이상 잘못된 입력 시퀀스를 잘못된 UTF-16 문자열로 디코딩하지 않습니다. 대신, 원래 입력을 반환합니다.|
|제안 해결 방법|문자열에 UTF-16 데이터 대신 이진 데이터를 저장하는 경우에만 디코더 출력에서의 변경 사항이 문제가 되어야 합니다. 이러한 동작을 명시적으로 제어하려면 [appSettings](~/docs/framework/configure-apps/file-schema/appsettings/index.md) 요소의 <code>aspnet:AllowRelaxedUnicodeDecoding</code> 특성을 <code>true</code>로 설정하여 레거시 동작을 사용하도록 설정하거나 <code>false</code>로 설정하여 현재 동작을 사용하도록 설정합니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Net.WebUtility.HtmlDecode(System.String)?displayProperty=nameWithType></li><li><xref:System.Net.WebUtility.HtmlDecode(System.String,System.IO.TextWriter)?displayProperty=nameWithType></li><li><xref:System.Net.WebUtility.UrlDecode(System.String)?displayProperty=nameWithType></li></ul>|
