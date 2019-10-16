---
ms.openlocfilehash: 6a99ed916e4e86e85d7ebc2d6ea36a6372c00206
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802595"
---
### <a name="aspnet-incorrect-multipart-handling-may-result-in-lost-form-data"></a>ASP.NET 다중 파트 처리가 잘못되면 양식 데이터가 손실될 수 있습니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.7.2 이하 버전을 대상으로 하는 애플리케이션에서 ASP.Net이 다중 파트 경계 값을 잘못 구문 분석하면 요청을 수행하는 중에 양식 데이터를 사용할 수 없게 될 수 있습니다. .NET Framework 4.8 이상 버전을 대상으로 하는 애플리케이션은 다중 파트 데이터를 올바르게 구문 분석하므로 요청을 실행하는 동안 양식 값을 사용할 수 있습니다.|
|제안|.NET Framework 4.8에서 실행되는 애플리케이션부터 <code>targetFrameworkVersion</code> 요소를 사용하여 .NET Framework 4.8 이상을 대상으로 지정하면 기본 동작이 스트립 구분 기호로 변경됩니다. 이전 프레임워크 버전을 대상으로 하거나 <code>targetFrameworkVersion</code>를 사용하지 않을 때 일부 값에 대한 후행 구분 기호가 여전히 반환됩니다. 이 동작은 <code>appSetting</code>를 사용하여 명시적으로 제어할 수도 있습니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;aspnet:UseLegacyMultiValueHeaderHandling&quot;  value=&quot;true&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|범위|알 수 없음|
|버전|4.8|
|Type|런타임|
|영향을 받는 API|<ul><li><xref:System.Web.HttpRequest.Form?displayProperty=nameWithType></li><li><xref:System.Web.HttpRequest.Files?displayProperty=nameWithType></li><li><xref:System.Web.HttpRequest.ContentEncoding?displayProperty=nameWithType></li></ul>|

