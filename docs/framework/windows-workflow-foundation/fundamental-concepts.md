---
title: Fundamental Windows Workflow 개념
ms.date: 03/30/2017
ms.assetid: 0e930e80-5060-45d2-8a7a-95c0690105d4
ms.openlocfilehash: 730679c892d96ff6de2d02ee1e1afdd52e452439
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650943"
---
# <a name="fundamental-windows-workflow-concepts"></a>Fundamental Windows Workflow 개념
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]의 워크플로 개발에는 일부 개발자들에게 생소한 개념이 사용됩니다. 이 항목에서는 이러한 몇 가지 개념과 그 구현 방법에 대해 설명합니다.  
  
## <a name="workflows-and-activities"></a>워크플로 및 활동  
 워크플로는 프로세스를 모델링하는 구조화된 동작의 컬렉션입니다. 워크플로의 각 동작은 활동으로 모델링됩니다. 호스트는 <xref:System.Activities.WorkflowInvoker>를 사용하여 워크플로를 메서드처럼 호출하고, <xref:System.Activities.WorkflowApplication>를 사용하여 단일 워크플로 인스턴스 실행을 명시적으로 제어하고, <xref:System.ServiceModel.WorkflowServiceHost>를 사용하여 다중 인스턴스 시나리오에서 메시지 기반의 상호 작용을 수행함으로써 워크플로와 상호 작용합니다. 워크플로 단계는 활동 계층으로 정의되기 때문에 계층의 최상위 활동이 워크플로 자체를 정의한다고 할 수 있습니다. 이 계층 모델은 이전 버전의 명시적 `SequentialWorkflow` 및 `StateMachineWorkflow` 클래스를 대체합니다. 활동 자체는 데이터 액세스에 런타임을 사용할 수 있게 해주는 <xref:System.Activities.Activity> 또는 활동 작성자에 워크플로 런타임을 표시하는 <xref:System.Activities.CodeActivity> 클래스를 사용하여 만든 사용자 지정 활동 또는 다른 활동(<xref:System.Activities.NativeActivity> 클래스를 기반으로 사용하며 일반적으로 XAML을 사용하여 정의됨)의 컬렉션으로 개발됩니다. <xref:System.Activities.CodeActivity> 및 <xref:System.Activities.NativeActivity>를 사용하여 개발되는 활동은 C# 등과 같은 CLR 호환 언어를 통해 만들어집니다.  
  
## <a name="activity-data-model"></a>활동 데이터 모델  
 활동에서는 다음 표에 표시된 형식을 사용하여 데이터를 저장하고 공유합니다.  
  
|||  
|-|-|  
|변수|활동에 데이터를 저장합니다.|  
|인수|활동 내부 및 외부로 데이터를 이동합니다.|  
|식|인수 바인딩에 사용되는 높은 반환 값을 가진 활동입니다.|  
  
## <a name="workflow-runtime"></a>워크플로 런타임  
 워크플로 런타임은 워크플로가 실행되는 환경입니다. <xref:System.Activities.WorkflowInvoker>는 워크플로를 실행하는 가장 간단한 방법입니다. 호스트에서는 다음 작업에 <xref:System.Activities.WorkflowInvoker>를 사용합니다.  
  
- 워크플로를 비동기적으로 호출  
  
- 워크플로에 입력 제공 또는 워크플로에서 출력 검색  
  
- 활동에 사용할 확장 추가  
  
 <xref:System.Activities.ActivityInstance>는 호스트에서 런타임과 상호 작용하는 데 사용할 수 있는 스레드로부터 안전한 프록시입니다. 호스트에서는 다음 작업에 <xref:System.Activities.ActivityInstance>를 사용합니다.  
  
- 인스턴스를 만들거나 인스턴스 저장소에서 로드하여 인스턴스 가져오기  
  
- 인스턴스 수명 주기 이벤트 알림 받기  
  
- 워크플로 실행 제어  
  
- 워크플로에 입력 제공 또는 워크플로에서 출력 검색  
  
- 워크플로 연속을 표시하고 워크플로에 값 전달  
  
- 워크플로 데이터 유지  
  
- 활동에 사용할 확장 추가  
  
 활동에서는 <xref:System.Activities.ActivityContext> 또는 <xref:System.Activities.NativeActivityContext> 등 적절한 <xref:System.Activities.CodeActivityContext> 파생 클래스를 사용하여 워크플로 런타임 환경에 액세스합니다. 또한 인수 및 변수 확인, 자식 활동 예약 등과 같은 용도로 이 클래스를 사용합니다.  
  
## <a name="services"></a>서비스  
 워크플로는 메시징 활동을 통해 서비스를 구현하고 액세스하는 자연스러운 방법을 제공합니다. 메시징 활동 WCF에서 빌드되고 및 워크플로 외부로 데이터를 가져오는 데 기본 메커니즘입니다. 원하는 메시지 교환 패턴의 종류를 모델링하여 메시징 활동을 함께 구성할 수 있습니다. 자세한 내용은 [메시징 활동](../wcf/feature-details/messaging-activities.md)합니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost> 클래스는 워크플로 서비스를 호스트하는 데 사용됩니다. 자세한 내용은 [호스팅 워크플로 서비스 개요](../wcf/feature-details/hosting-workflow-services-overview.md)합니다. 워크플로 서비스에 대 한 자세한 내용은 참조 하세요. [워크플로 서비스](../wcf/feature-details/workflow-services.md)  
  
## <a name="persistence-unloading-and-long-running-workflows"></a>워크플로 유지, 언로드 및 장기 실행  
 Windows Workflow는 다음을 제공하여 장기 실행 대응 프로그램을 쉽게 작성할 수 있도록 해줍니다.  
  
- 외부 입력에 액세스하는 활동  
  
- 호스트 수신기에서 다시 시작할 수 있는 <xref:System.Activities.Bookmark> 개체를 만드는 기능  
  
- 워크플로 데이터를 유지하고 워크플로를 언로드한 다음 특정 워크플로의 <xref:System.Activities.Bookmark> 개체 재시작에 응답하여 워크플로를 다시 로드하여 활성화할 수 있는 기능  
  
 워크플로에서는 더 이상 실행할 활동이 없거나 현재 실행 중인 모든 활동이 입력 대기 중일 때까지 활동을 계속 실행합니다. 후자의 입력 대기 상태에서는 워크플로가 유휴 상태가 됩니다. 일반적으로 호스트는 유휴 상태인 워크플로를 언로드한 다음 계속 실행하라는 메시지를 받으면 해당 워크플로를 다시 로드합니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost>는 이를 위한 기능과 확장 가능한 언로드 정책을 제공합니다. 별도로 유지할 수 없는 일시적 상태 또는 데이터를 사용하는 실행 블록의 경우 활동에서 <xref:System.Activities.NoPersistHandle>를 사용하여 호스트에 이를 유지하지 않도록 지시할 수 있습니다. 또한 워크플로에서는 <xref:System.Activities.Statements.Persist> 활동을 사용하여 데이터를 영구 스토리지 매체에 명시적으로 유지할 수 있습니다.
