---
ms.openlocfilehash: 77e04333ed2b9a5ca8b900c1355fb5b12957772d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774446"
---
### <a name="machinekeyencode-and-machinekeydecode-methods-are-now-obsolete"></a>MachineKey.Encode 및 MachineKey.Decode 메서드는 사용되지 않음

|   |   |
|---|---|
|설명|이러한 메서드는 이제 사용되지 않습니다. 이러한 메서드를 호출하는 코드를 컴파일하면 컴파일러 경고가 생성됩니다.|
|제안 해결 방법|<xref:System.Web.Security.MachineKey.Protect(System.Byte[],System.String[])> 및 <xref:System.Web.Security.MachineKey.Unprotect(System.Byte[],System.String[])>를 대신 사용하는 것이 좋습니다. 또는 빌드 경고를 표시하지 않거나 이전 컴파일러를 사용하여 방지할 수 있습니다. API는 계속 지원됩니다.|
|범위|부|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Web.Security.MachineKey.Encode(System.Byte[],System.Web.Security.MachineKeyProtection)?displayProperty=nameWithType></li><li><xref:System.Web.Security.MachineKey.Decode(System.String,System.Web.Security.MachineKeyProtection)?displayProperty=nameWithType></li></ul>|
