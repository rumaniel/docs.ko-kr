---
ms.openlocfilehash: 0ab6be6f2c6d8ebbe67051e4e3f967a325e654c8
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804440"
---
### <a name="htmltextwriter-does-not-render-br-element-correctly"></a>HtmlTextWriter가 `<br/>` 요소를 올바르게 렌더링하지 않음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6부터 <code>&lt;BR /&gt;</code> 요소로 <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> 및 <xref:System.Web.UI.HtmlTextWriter.RenderEndTag>를 호출하면 (두 개가 아닌) 단 하나의 <code>&lt;BR /&gt;</code>만 올바르게 삽입합니다.|
|제안 해결 방법|응용 프로그램이 추가 <code>&lt;BR /&gt;</code> 태그에 종속된 경우 <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)>를 두 번째로 호출해야 합니다. 이 동작 변경은 .NET Framework 4.6 이상을 대상으로 하는 응용 프로그램에만 영향을 주므로 다른 옵션은 이전 버전의 .NET Framework를 대상으로 하여 이전 동작을 가져오는 것입니다.|
|범위|Microsoft Edge|
|버전|4.6|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)?displayProperty=nameWithType></li><li><xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.Web.UI.HtmlTextWriterTag)?displayProperty=nameWithType></li></ul>|

