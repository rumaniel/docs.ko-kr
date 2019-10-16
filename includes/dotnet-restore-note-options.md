---
ms.openlocfilehash: 47811d3fab2e4fa531d383dfe818e3cac5613eb3
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72179971"
---
> [!NOTE]
> .NET Core 2.0부터 복원을 수행해야 하는 모든 명령(예: [ 및 `dotnet restore`)에서 암시적으로 실행되므로 ](~/docs/core/tools/dotnet-restore.md)`dotnet build``dotnet run`를 실행할 필요가 없습니다. [Azure DevOps Services의 연속 통합 빌드](/azure/devops/build-release/apps/aspnet/build-aspnet-core)와 같이 명시적 복원을 수행하는 것이 올바른 특정 시나리오 또는 복원이 발생하는 시간을 명시적으로 제어해야 하는 빌드 시스템에서는 여전히 유효한 명령입니다.
>
> 또한 이 명령은 긴 형식(예: `--source`)으로 전달될 때 `dotnet restore` 옵션도 지원합니다. `-s`와 같이 짧은 형식의 옵션은 지원되지 않습니다.
