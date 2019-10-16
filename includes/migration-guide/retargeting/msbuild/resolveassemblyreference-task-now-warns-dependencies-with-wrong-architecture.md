---
ms.openlocfilehash: 39a329597ef28e002242103a247515d94761676a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774459"
---
### <a name="resolveassemblyreference-task-now-warns-of-dependencies-with-the-wrong-architecture"></a>ResolveAssemblyReference 작업이 이제 잘못된 아키텍처의 종속성에 대해 경고

|   |   |
|---|---|
|설명|이 작업은 참조 또는 해당 종속성이 앱 아키텍처와 일치하지 않음을 나타내는 경고 MSB3270을 내보냅니다. 예를 들어 <code>AnyCPU</code> 옵션으로 컴파일된 앱에 x86 참조가 포함된 경우 이 경고가 발생합니다. 이로 인해 앱의 런타임 오류가 발생할 수 있습니다(앱이 x64 프로세스로 배포된 경우).|
|제안 해결 방법|영향에는 다음 두 가지 영역이 있습니다.<ul><li>다시 컴파일하면 앱이 이전 MSBuild 버전에서 컴파일되었을 때는 나타나지 않았던 경고가 생성됩니다. 하지만 런타임 오류가 발생한 소스를 경고에서 확인할 수 있으므로 이 문제를 조사하여 해결할 수 있습니다.</li><li>경고가 오류로 처리되면 앱을 컴파일할 수 없습니다.</li></ul>|
|범위|부|
|버전|4.5.1|
|형식|대상 변경|
