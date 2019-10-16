---
ms.openlocfilehash: 29b8feb7959c718391b963c8402b97351b93fa49
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804520"
---
### <a name="missing-target-framework-moniker-results-in-40-behavior"></a>누락된 대상 프레임워크 모니커로 인해 4.0 동작 발생

|   |   |
|---|---|
|세부 정보|어셈블리 수준에 적용된 <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=name>이 없는 애플리케이션은 .NET Framework 4.0의 의미 체계(쿼크)를 사용하여 자동으로 실행됩니다. 높은 품질을 보장하려면 모든 바이너리가 빌드될 때 사용된 .NET Framework의 버전을 나타내는 <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=name>로 명시적으로 특성을 사용하는 것이 좋습니다. 프로젝트 파일에서 대상 프레임워크 모니커를 사용하면 MSBuild가 <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=name>를 자동으로 적용합니다.|
|제안 해결 방법|어셈블리에 직접 특성을 추가하거나 [프로젝트 파일 또는 Visual Studio의 프로젝트 속성 GUI를 통해](https://devblogs.microsoft.com/visualstudio/visual-studio-managed-multi-targeting-part-1-concepts-target-framework-moniker-target-framework/) 대상 프레임워크를 지정하여 <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=name>을 지정해야 합니다.|
|범위|주요함|
|버전|4.5|
|형식|런타임|
