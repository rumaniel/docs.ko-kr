---
ms.openlocfilehash: 7f551fbc194d2da2fdae6bcc7025c20b03aadda2
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859347"
---
### <a name="path-colon-checks-are-stricter"></a>경로 콜론 검사가 더욱 엄격해짐

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2에서 이전에 지원되지 않던 경로(길이 및 형식 모두)를 지원하도록 여러 가지가 변경되었습니다. 적절한 드라이브 구분 기호(콜론) 구문에 대해 검사가 좀 더 정확해졌습니다. 이 구문은 허용되었던 일부 선택 경로 API에서 일부 URI 경로가 차단되는 부작용이 있었습니다.|
|제안|영향을 받는 API로 URI를 전달하는 경우 먼저 합법적인 경로가 되도록 문자열을 수정합니다.<ul><li>URL에서 스키마를 수동으로 제거합니다(예: URL에서 <code>file://</code> 제거).</li><li>URI를 <xref:System.Uri> 클래스에 전달하고 <xref:System.Uri.LocalPath>를 사용합니다.</li></ul>또는 <code>Switch.System.IO.UseLegacyPathHandling</code> AppContext 스위치를 true로 설정하여 새 경로 정규화를 옵트아웃합니다.|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.IO.Path.GetDirectoryName(System.String)?displayProperty=nameWithType></li><li><xref:System.IO.Path.GetPathRoot(System.String)?displayProperty=nameWithType></li></ul>|

