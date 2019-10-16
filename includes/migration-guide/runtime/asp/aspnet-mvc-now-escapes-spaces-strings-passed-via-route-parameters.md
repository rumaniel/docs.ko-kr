---
ms.openlocfilehash: 8d058d3297471e67459164f18358b1d143465712
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803209"
---
### <a name="aspnet-mvc-now-escapes-spaces-in-strings-passed-in-via-route-parameters"></a>ASP.NET MVC가 이제 경로 매개 변수를 통해 전달된 문자열에 있는 공백을 이스케이프함

|   |   |
|---|---|
|세부 정보|RFC 2396를 준수하려면 경로에서 작업 매개 변수를 채울 때 경로의 공백은 이스케이프됩니다. 따라서 이전에는 <code>/controller/action/some data</code>이 경로 <code>/controller/action/{data}</code>와 일치하고 <code>some data</code>를 데이터 매개 변수로 제공했지만 이제는 <code>some%20data</code>를 대신 제공합니다.|
|제안|경로에서 문자열 매개 변수를 이스케이프 해제하려면 코드를 업데이트해야 합니다. 원래의 URI가 필요한 경우 <xref:System.Net.HttpWebRequest.RequestUri>.OriginalString API를 통해 액세스할 수 있습니다.|
|범위|부|
|버전|4.5.2|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Web.Mvc.RouteAttribute.%23ctor(System.String)?displayProperty=nameWithType></li></ul>|

