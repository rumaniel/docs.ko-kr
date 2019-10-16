---
ms.openlocfilehash: 25060a42b4ff66b1e25881b8c704ae0958e5f245
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804498"
---
### <a name="building-an-entity-framework-edmx-with-visual-studio-2013-can-fail-with-error-msb4062-if-using-the-entitydeploysplit-or-entityclean-tasks"></a>Visual Studio 2013을 사용하여 Entity Framework edmx를 빌드할 때 EntityDeploySplit 또는 EntityClean 작업을 사용하면 MSB4062 오류로 실패할 수 있음

|   |   |
|---|---|
|세부 정보|MSBuild 12.0 도구(Visual Studio 2013 포함)가 MSBuild 파일 위치를 변경하여 이전 Entity Framework 대상 파일을 유효하지 않게 했습니다. 그 결과로 <code>EntityDeploySplit</code> 및 <code>EntityClean</code> 작업이 <code>Microsoft.Data.Entity.Build.Tasks.dll</code>을 찾을 수 없어 실패합니다. 이 줄바꿈은 .NET Framework의 변경 때문이 아닌 도구 집합(MSBuild/VS) 변경 때문입니다. 이것은 단순히 .NET Framework를 업그레이드할 때가 아니라 개발자 도구를 업그레이드할 때에만 발생합니다.|
|제안|.NET Framework 4.6부터 Entity Framework 대상 파일은 새 MSBuild 레이아웃으로 작업하도록 수정되었습니다. 해당 버전의 Framework로 업그레이드하면 이 문제가 해결됩니다. 또는 [이 해결 방법](https://stackoverflow.com/a/24249247/131944)을 대상 파일을 직접 패치하는 데 사용할 수 있습니다.|
|범위|주요함|
|버전|4.5.1|
|형식|대상 변경|

