---
title: Visual Workflow Tracking
ms.date: 03/30/2017
ms.assetid: 0143448f-2044-40a0-8a3d-941f6d12468b
ms.openlocfilehash: 4ce9b06ede2c24839859e4b1f2c2f9c829f3380c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045339"
---
# <a name="visual-workflow-tracking"></a>Visual Workflow Tracking
이 샘플에서는 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)]을 통해 사용할 수 있는 디버그 기능을 사용하여 시각적 워크플로 추적 애플리케이션을 작성하는 방법을 보여 줍니다.

## <a name="sample-details"></a>샘플 세부 정보
 이 애플리케이션에서는 Workflow.xaml에 정의된 간단한 순서도 워크플로를 실행하고 워크플로 디자이너를 다시 호스트하여 현재 실행 중인 워크플로를 표시합니다. 워크플로가 실행되면 현재 실행 중인 활동이 노란색 윤곽선 및 디버그 화살표와 함께 표시됩니다. 또한 애플리케이션 창에는 워크플로에 의해 생성된 추적 레코드도 표시됩니다. 워크플로 추적에 대 한 자세한 내용은 [워크플로 추적 및 추적](../workflow-tracking-and-tracing.md)을 참조 하세요. Workflow designer를 다시 호스트 하는 방법에 대 한 자세한 내용은 [재호스팅 the 워크플로 디자이너](../rehosting-the-workflow-designer.md)항목을 참조 하세요.

 이 워크플로 시뮬레이터의 작업에는 두 개의 사전이 사용됩니다. 한 사전에는 현재 실행 중인 활동 개체와 해당 활동이 인스턴스화된 XAML 줄 번호 간의 매핑이 포함되어 있으며, 다른 사전에는 활동 인스턴스 ID와 활동 개체 간의 매핑이 포함되어 있습니다. 사용자 지정 추적 프로필을 사용하여 추적 레코드가 생성되면 애플리케이션에서는 현재 실행 중인 활동의 인스턴스 ID를 확인하고 이를 해당 활동이 인스턴스화된 XAML 파일에 다시 매핑합니다. 그러면 다시 호스트된 워크플로 디자이너는 지시에 따라 디자이너 화면에 해당 활동을 강조 표시하고 워크플로 디버거와 동일한 방법을 사용하여 활동 주위에 노란색 테두리를 그리고 디자이너의 왼쪽에 노란색 화살표를 표시합니다.

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. Visual Studio 2010의 샘플 디렉터리에서 WorkflowSimulator .sln 파일을 엽니다.

2. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

3. Ctrl+F5를 눌러 샘플을 실행합니다. 그러면 다시 호스트된 Workflow Designer 창에 Workflow.xaml 파일이 표시됩니다.

4. **파일** 메뉴를 클릭 하 고 **워크플로 실행**...을 선택 합니다.

5. 앞에서 설명한 대로 현재 실행 중인 활동이 강조 표시되고 애플리케이션 창의 오른쪽에 추적 레코드가 표시됩니다.

6. 워크플로가 완료된 후 원하는 추적 레코드를 클릭하여 레코드에 해당하는 활동을 검사할 수 있습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\VisualWorkflowTracking`
