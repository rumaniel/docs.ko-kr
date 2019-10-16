---
ms.openlocfilehash: 734041f5921571cd11225a359e794526cbd8d0e1
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774471"
---
### <a name="systemuriiswellformeduristring-method-returns-false-for-relative-uris-with-a-colon-char-in-first-segment"></a>첫 번째 세그먼트에 콜론 문자가 있는 상대 URI에 대해 System.Uri.IsWellFormedUriString 메서드가 false를 반환

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)>은 첫 번째 세그먼트에서 <code>:</code>가 있는 상대 URI가 잘 형성되지 않은 것으로 간주합니다. 이는 RFC3986을 준수하도록 만들어진 .NET Framework 4.0의 <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=name> 동작의 변경입니다.|
|제안 해결 방법|이 변경(다른 많은 URI 변경과 마찬가지)은 .NET Framework 4.5(또는 그 이상)를 대상으로 하는 애플리케이션에만 영향을 미칩니다. 이전 동작을 계속 사용하려면 .NET Framework 4.0에 대해 앱을 대상으로 지정합니다. 또는 이전 동작이 바람직한 경우 <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=name>을 호출하기 전에 URI를 검사하여 유효성 검사를 위해 제거하려는 <code>:</code> 문자를 찾습니다.|
|범위|부|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=nameWithType></li></ul>|
