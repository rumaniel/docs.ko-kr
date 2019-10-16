---
title: 워크플로 디버깅
ms.date: 03/30/2017
ms.assetid: b23b4814-ebb1-4c51-b7a9-469f4da7a96d
ms.openlocfilehash: 3947e61161b0e2108fa48fbc7e33fb7601645a1b
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291493"
---
# <a name="debugging-workflows"></a>워크플로 디버깅

[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]는 개발 환경에서 실행 중인 워크플로를 디버깅하기 위한 여러 옵션을 제공합니다. 디자이너, XAML 및 코드에서 워크플로를 디버깅할 수 있습니다.

## <a name="debugging-in-the-workflow-designer"></a>워크플로 디자이너에서 디버깅

워크플로 디자이너에서 활동을 강조 표시 하 고 <kbd>F9</kbd> 키를 누르거나 활동의 상황에 맞는 메뉴를 사용 하 여 활동에 중단점을 설정할 수 있습니다. 그러면 워크플로 호스트가 디버그 모드에서 실행될 때 워크플로 실행이 중단됩니다. 다음 스크린샷에서는 워크플로 실행이 중단점에서 일시 중지됩니다. 자세한 내용은 [워크플로 디자이너를 사용 하 여 워크플로 디버깅](/visualstudio/workflow-designer/debugging-workflows-with-the-workflow-designer)을 참조 하세요.

## <a name="debugging-in-xaml"></a>XAML에서 디버깅

워크플로가 디자이너의 중단점에서 일시 중지된 경우 XAML에서 워크플로를 디버깅할 수도 있습니다. XAML에서 실행 지점을 보려면 워크플로 실행이 일시 중지 될 때 워크플로 디자이너에서 **Xaml 뷰** 를 선택 합니다. 솔루션 탐색기에서 디자이너에 워크플로를 다시 열어 디버깅을 다시 디자이너로 전환할 수 있습니다. 자세한 내용은 [방법: 워크플로 디자이너 @ no__t-0을 사용 하 여 XAML을 디버그 합니다.

## <a name="debugging-in-code"></a>코드에서 디버깅

중단점을 설정 하려면 코드 창의 왼쪽 여백을 클릭 하거나 F9 키를 설정 하려는 줄의 커서와 함께 <kbd>F9</kbd> 키를 누릅니다.

## <a name="attaching-to-a-workflow-process"></a>워크플로 프로세스에 연결

워크플로 디버깅은 Visual Studio 인프라를 사용하여 프로세스에 연결하는 방식도 지원합니다. 이렇게 하면 워크플로 작성자가 Internet Information Services(IIS) 7.0 등 다른 호스트 환경에서 실행되는 워크플로를 디버깅할 수 있습니다.

## <a name="remote-debugging"></a>Remote Debugging

WF (Windows Workflow Foundation) 원격 디버깅은 다른 Visual Studio 구성 요소에 대 한 원격 디버깅과 동일 하 게 작동 합니다. 원격 디버깅 사용에 대 한 자세한 내용은 [How to: 원격 디버깅을 사용 하도록 설정 @ no__t-0.

> [!NOTE]
> 워크플로 응용 프로그램에서 x86 아키텍처를 대상으로 하 고 64 비트 운영 체제를 실행 하는 컴퓨터에서 호스트 되는 경우 원격 컴퓨터에 Visual Studio가 설치 되어 있지 않거나 워크플로 응용 프로그램의 대상이로 변경 되지 않으면 원격 디버깅이 작동 하지 않습니다. **모든 CPU**.

## <a name="extending-the-workflow-debugging-service"></a>워크플로 디버깅 서비스 확장

워크플로 디버거 서비스는 현재 공용이며 다시 호스트된 디자이너에서 모니터링, 시뮬레이션 및 디버깅과 같은 사용자 지정 애플리케이션을 만드는 데 사용될 수 있습니다. 자세한 내용은 <xref:System.Activities.Presentation.Debug.DebuggerService>를 참조하십시오.
