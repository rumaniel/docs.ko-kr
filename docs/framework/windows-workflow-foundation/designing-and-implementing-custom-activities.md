---
title: 사용자 지정 활동 디자인 및 구현
ms.date: 03/30/2017
ms.assetid: 4e30e63d-6e33-4842-a7a4-ce807cef1fad
ms.openlocfilehash: b0d04572c65fd4e3e0ae96241217c9ae9aa0e2c5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69915357"
---
# <a name="designing-and-implementing-custom-activities"></a>사용자 지정 활동 디자인 및 구현
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]에서는 시스템 제공 활동을 복합 활동으로 어셈블하거나 <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> 또는 <xref:System.Activities.NativeActivity>에서 파생된 새 형식을 만들어 사용자 지정 활동을 만듭니다. 이 단원에서는 이 메서드 중 하나를 사용하여 사용자 지정 활동을 만드는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]
> 기본적으로 사용자 지정 활동은 워크플로 디자이너에 활동 이름과 함께 간단한 사각형으로 표시됩니다. 워크플로 디자이너에서 활동이 표시되는 모양을 사용자 지정하려면 사용자 지정 디자이너도 만들어야 합니다. 자세한 내용은 [사용자 지정 활동 디자이너 및 템플릿 사용](using-custom-activity-designers-and-templates.md)을 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [활동 제작 옵션](activity-authoring-options-in-wf.md)  
 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]에서 사용할 수 있는 제작 스타일에 대해 설명합니다.  
  
 [사용자 지정 활동 사용](using-a-custom-activity.md)  
 워크플로 프로젝트에 사용자 지정 활동을 추가하는 방법에 대해 설명합니다.  
  
  [비동기 활동 만들기](creating-asynchronous-activities-in-wf.md)  
 비동기 활동을 만드는 방법에 대해 설명합니다.  
  
 [활동 유효성 검사 구성](configuring-activity-validation.md)  
 활동을 실행하기 전에 활동 유효성 검사를 사용하여 활동 구성 오류를 식별하고 보고하는 방법에 대해 설명합니다.  
  
 [런타임에 활동 만들기](creating-an-activity-at-runtime-with-dynamicactivity.md)  
 런타임에 <xref:System.Activities.DynamicActivity>를 사용하여 활동을 만드는 방법에 대해 설명합니다.  
  
 [워크플로 실행 속성](workflow-execution-properties.md)  
 워크플로 실행 속성을 사용하여 활동 환경에 컨텍스트별 속성을 추가하는 방법에 대해 설명합니다.  
  
 [활동 대리자 사용](using-activity-delegates.md)  
 활동 대리자가 포함된 활동을 작성하고 사용하는 방법에 대해 설명합니다.
  
 [활동 확장명 사용](using-activity-extensions.md)  
 활동 확장을 작성하고 사용하는 방법에 대해 설명합니다.  
  
 [워크플로에서 OData 피드 사용](consuming-odata-feeds-from-a-workflow.md)  
 워크플로에서 WCF Data Service를 호출하는 여러 가지 방법에 대해 설명합니다.  
  
 [활동 정의 범위 지정 및 표시 유형](activity-definition-scoping-and-visibility.md)  
 활동에 대한 데이터 범위와 멤버 표시 유형을 정의하는 옵션 및 규칙에 대해 설명합니다.
