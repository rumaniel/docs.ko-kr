---
ms.openlocfilehash: e8c48c4b1031813ce62f576e5bf1f94c082dfe4b
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774434"
---
### <a name="obsoleteattribute-exports-as-both-obsoleteattribute-and-deprecatedattribute-in-winmd-scenarios"></a>ObsoleteAttribute가 WinMD 시나리오에서 ObsoleteAttribute와 DeprecatedAttribute를 내보냄

|   |   |
|---|---|
|세부 정보|Windows 메타데이터 라이브러리(.winmd 파일)를 만들 때 <xref:System.ObsoleteAttribute?displayProperty=name> 특성은 <xref:System.ObsoleteAttribute?displayProperty=name> 및 [Windows.Foundation.DeprecatedAttribute](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.deprecatedattribute)로서 내보내집니다.|
|제안 해결 방법|<xref:System.ObsoleteAttribute?displayProperty=name> 특성이 사용된 기존 소스 코드를 다시 컴파일하면 C++/CX 또는 JavaScript의 해당 코드가 사용될 때 경고가 발생할 수 있습니다. <xref:System.ObsoleteAttribute?displayProperty=name> 및 [Windows.Foundation.DeprecatedAttribute](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.deprecatedattribute) 모두를 관리되는 어셈블리의 코드에 적용하는 것은 좋지 않습니다. 빌드 경고가 발생할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5.1|
|형식|대상 변경|
