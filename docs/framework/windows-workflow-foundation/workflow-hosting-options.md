---
title: 워크플로 호스팅 옵션
ms.date: 03/30/2017
ms.assetid: 37bcd668-9c5c-4e7c-81da-a1f1b3a16514
ms.openlocfilehash: 4eaed147f312f3963aa1ca1d4f5dbe010c4189ad
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037828"
---
# <a name="workflow-hosting-options"></a>워크플로 호스팅 옵션
대부분의 WF (Windows Workflow Foundation) 샘플에서는 콘솔 응용 프로그램에서 호스트 되는 워크플로를 사용 하지만 실제 워크플로에는 현실적인 시나리오가 아닙니다. 실제 비즈니스 응용 프로그램의 워크플로는 영구 프로세스에서 호스트 됩니다. 즉, 개발자가 작성 한 Windows 서비스 또는 IIS 7.0 또는 AppFabric과 같은 서버 응용 프로그램입니다. 이러한 방법에는 다음과 같은 차이가 있습니다.

## <a name="hosting-workflows-in-iis-with-windows-appfabric"></a>IIS에서 Windows AppFabric을 사용하여 워크플로 호스팅

IIS와 AppFabric을 함께 사용하는 것은 기본적인 워크플로 호스팅 방법입니다. AppFabric을 사용하는 워크플로용 호스트 애플리케이션은 Windows Activation Service로, 이 애플리케이션에서는 IIS만을 통해 HTTP에 대한 종속성을 제거합니다.

## <a name="hosting-workflows-in-iis-alone"></a>IIS만 사용하여 워크플로 호스팅

실행 중인 응용 프로그램의 유지 관리를 용이 하 게 하는 AppFabric에서 사용할 수 있는 관리 및 모니터링 도구가 있으므로 IIS 7.0만 사용 하지 않는 것이 좋습니다. AppFabric으로 이동 하는 인프라 문제가 있는 경우에만 워크플로를 IIS 7.0에 단독으로 호스팅해야 합니다.

> [!WARNING]
> IIS 7.0는 다양 한 이유로 정기적으로 응용 프로그램 풀을 재활용 합니다. 애플리케이션 풀이 재활용될 때 IIS는 이전 풀에서 메시지 수락을 중지하고 새 요청을 수락하는 새 애플리케이션 풀을 인스턴스화합니다. 응답이 전송 된 후 워크플로가 계속 작동 하는 경우 IIS 7.0은 수행 중인 작업을 인식 하지 못하므로 호스팅 응용 프로그램 풀을 재활용할 수 있습니다. 이 경우 워크플로가 중단 되 고 추적 서비스는 빈 이유 필드와 함께 [1004-WorkflowInstanceAborted](1004-workflowinstanceaborted.md) 메시지를 기록 합니다.
>
> 지속성이 사용되는 경우 호스트는 마지막 지속성 지점에서 중단된 인스턴스를 명시적으로 다시 시작해야 합니다.
>
> AppFabric이 사용되는 경우 지속성이 사용되면 최종적으로 워크플로 관리 서비스가 마지막으로 성공한 지속성 지점에서 워크플로를 재개하게 됩니다. 지속성이 사용되지 않고 워크플로가 요청/응답 패턴을 벗어나 작업을 수행하는 경우에는 워크플로 중단 시 데이터가 손실됩니다.

## <a name="hosting-a-workflow-in-a-custom-windows-service"></a>사용자 지정 Windows 서비스에서 워크플로 호스팅

사용자 지정 워크플로를 호스트하기 위한 사용자 지정 워크플로 서비스를 만들려면 개발자가 AppFabric에서 기본적으로 제공되는 많은 기능을 복제해야 하지만 이 경우 사용자 지정 기능을 보다 유연하게 사용할 수 있다는 이점이 있습니다. 이 옵션은 AppFabric을 사용할 수 없는 것이 분명한 경우에만 고려해야 합니다.
