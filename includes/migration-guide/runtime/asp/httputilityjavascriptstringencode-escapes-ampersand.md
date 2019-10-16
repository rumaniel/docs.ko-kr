---
ms.openlocfilehash: 0056baa1e5f0cdc5bfcf8b0e83c9490ec5722926
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235707"
---
### <a name="httputilityjavascriptstringencode-escapes-ampersand"></a>HttpUtility.JavaScriptStringEncode가 앰퍼샌드를 이스케이프합니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 <xref:System.Web.HttpUtility.JavaScriptStringEncode(System.String)?displayProperty=name>이 앰퍼샌드(&amp;) 문자를 이스케이프합니다.|
|제안 해결 방법|응용 프로그램이 이 메서드의 이전 동작에 종속되는 경우 aspnet:JavaScriptDoNotEncodeAmpersand 설정을 구성 파일에 있는 [ASP.NET appSettings 요소](https://docs.microsoft.com/previous-versions/aspnet/hh975440(v=vs.120))에 추가할 수 있습니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Web.HttpUtility.JavaScriptStringEncode(System.String)?displayProperty=nameWithType></li><li><xref:System.Web.HttpUtility.JavaScriptStringEncode(System.String,System.Boolean)?displayProperty=nameWithType></li></ul>|
