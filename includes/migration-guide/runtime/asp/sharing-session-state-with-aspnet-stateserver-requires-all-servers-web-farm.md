---
ms.openlocfilehash: 958a89015420ce5632d596688963d576c40b4cb6
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235582"
---
### <a name="sharing-session-state-with-aspnet-stateserver-requires-all-servers-in-the-web-farm-to-use-the-same-net-framework-version"></a>Asp.Net StateServer와 세션 상태를 공유하려면 웹 팜의 모든 서버가 동일한 .NET Framework 버전을 사용해야 합니다.

|   |   |
|---|---|
|세부 정보|<xref:System.Web.SessionState.SessionStateMode.StateServer?displayProperty=name> 세션 상태를 활성화할 때 상태를 올바르게 공유하려면 지정된 웹 팜의 모든 서버가 동일한 .NET Framework 버전을 사용해야 합니다.|
|제안 해결 방법|동시에 상태를 공유하는 웹 서버에서 .NET Framework 버전을 업그레이드해야 합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Web.SessionState.SessionStateMode.StateServer?displayProperty=nameWithType></li></ul>|
