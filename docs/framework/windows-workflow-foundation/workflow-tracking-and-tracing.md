---
title: 워크플로 추적
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], tracking and tracing
ms.assetid: b965ded6-370a-483d-8790-f794f65b137e
ms.openlocfilehash: eaf38bad246b1f02449c1a3b99c7fb844c09a4bd
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959721"
---
# <a name="workflow-tracking-and-tracing"></a>워크플로 추적
Windows Workflow 추적은 워크플로 실행을 쉽게 볼 수 있도록 디자인된 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 기능입니다. 이 기능은 워크플로 인스턴스 실행을 추적하기 위한 추적 인프라를 제공합니다. WF 추적 인프라는 실행 중에 주요 이벤트를 반영하여 레코드를 내보내기 위한 워크플로를 투명하게 계측합니다. 기본적으로 모든 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 워크플로에 이 기능을 사용할 수 있습니다. 추적을 수행하기 위해 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 워크플로를 변경할 필요는 없습니다. 받으려는 추적 데이터의 양만 결정하면 됩니다. 워크플로 인스턴스가 시작되거나 완료되면 처리 추적 레코드가 내보내집니다. 추적에서 워크플로 변수와 연결된 비즈니스 관련 데이터를 추출할 수도 있습니다. 예를 들어, 워크플로가 주문 처리 시스템을 나타내는 경우 <xref:System.Activities.Tracking.TrackingRecord> 개체와 함께 주문 ID를 추출할 수 있습니다. 일반적으로 WF 추적을 사용하면 워크플로 실행에서 진단 또는 비즈니스 분석에 쉽게 액세스할 수 있습니다.  
  
 이러한 추적 구성 요소는 WinFX의 추적 서비스와 동일 합니다. [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]에서는 WF 추적 기능에 맞게 성능이 향상되고 프로그래밍 모델이 단순화되었습니다. 추적 런타임은 워크플로 인스턴스를 계측하여 워크플로 수명 주기와 관련된 이벤트, 워크플로 활동 및 사용자 지정 이벤트를 내보냅니다.  
  
 Windows Server AppFabric은 WCF 및 워크플로 서비스의 실행을 모니터링하는 기능도 제공합니다. 자세한 내용은 [Windows Server App Fabric 모니터링](https://go.microsoft.com/fwlink/?LinkId=201273) 고 [Windows Server AppFabric을 사용 하 여 응용 프로그램 모니터링](https://go.microsoft.com/fwlink/?LinkId=201287)  
  
 워크플로 런타임의 문제를 해결하기 위해 진단 워크플로 추적을 설정할 수 있습니다. 자세한 내용은 [워크플로 추적](workflow-tracing.md)합니다.  
  
 프로그래밍 모델을 이해할 수 있도록 이 항목에서는 추적 인프라의 주요 구성 요소를 설명합니다.  
  
- 워크플로 런타임에서 내보낸 <xref:System.Activities.Tracking.TrackingRecord> 개체입니다. 자세한 내용은 [추적 레코드](tracking-records.md)합니다.  
  
- <xref:System.Activities.Tracking.TrackingParticipant> 개체는 <xref:System.Activities.Tracking.TrackingRecord> 개체를 구독합니다. 추적 참가자에는 <xref:System.Activities.Tracking.TrackingRecord> 개체에서 페이로드를 처리하기 위한 논리가 포함됩니다. 예를 들어 파일에 기록하도록 선택할 수 있습니다. 자세한 내용은 [추적 참가자](tracking-participants.md)합니다.  
  
- <xref:System.Activities.Tracking.TrackingProfile> 개체는 워크플로 인스턴스에서 내보낸 추적 레코드를 필터링합니다. 자세한 내용은 [추적 프로필](tracking-profiles.md)합니다.  
  
## <a name="workflow-tracking-infrastructure"></a>워크플로 추적 인프라  
 워크플로 추적 인프라는 게시 및 구독 패러다임을 따릅니다. 워크플로 인스턴스는 추적 레코드 게시자인 반면, 추적 레코드 구독자는 워크플로의 확장으로 등록됩니다. <xref:System.Activities.Tracking.TrackingRecord> 개체를 구독하는 이 확장을 추적 참가자라고 합니다. 추적 참가자는 <xref:System.Activities.Tracking.TrackingRecord> 개체에 액세스한 다음 해당 참가자에 정해진 방식으로 처리하는 확장성 지점입니다. 추적 인프라를 사용하면 보내기 추적 레코드에 필터를 적용하여 참가자가 레코드 하위 집합을 구독하도록 허용할 수 있습니다. 이 필터링 메커니즘은 추적 프로필 파일을 통해 완료됩니다.  
  
 추적 인프라의 상위 수준 보기는 다음 그림에 표시 됩니다.  
  
 ![워크플로 추적 인프라를 보여 주는 스크린샷. ](./media/workflow-tracking-and-tracing/workflow-tracking-infrastructure.gif "WV")  
  
## <a name="in-this-section"></a>섹션 내용  
 [추적 레코드](tracking-records.md)  
 워크플로 런타임이 내보내는 추적 레코드를 설명합니다.  
  
 [추적 프로필](tracking-profiles.md)  
 추적 프로필이 사용되는 방법을 설명합니다.  
  
 [추적 참가자](tracking-participants.md)  
 시스템 제공 추적 참가자를 사용하는 방법 또는 사용자 지정 추적 참가자를 만드는 방법을 설명합니다.  
  
 [워크플로 추적 구성](configuring-tracking-for-a-workflow.md)  
 워크플로 추적을 구성하는 방법을 설명합니다.  
  
 [워크플로 추적](workflow-tracing.md)  
 워크플로 추적을 디버깅하는 두 가지 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [SQL 추적](./samples/sql-tracking.md)
