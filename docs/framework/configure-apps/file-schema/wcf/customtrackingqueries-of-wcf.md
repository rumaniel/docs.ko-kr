---
title: WCF의 &lt;customTrackingQueries&gt;
ms.date: 03/30/2017
ms.assetid: 14cfe47e-9935-4120-84f1-8f38de8ca4c1
ms.openlocfilehash: 060e2b5c8efd51f6245a39bd9562a69f0111fd41
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202226"
---
# <a name="ltcustomtrackingqueriesgt-of-wcf"></a>WCF의 &lt;customTrackingQueries&gt;

코드 활동에서 정의하는 이벤트를 추적하는 데 사용되는 쿼리의 컬렉션을 나타냅니다. 추적 참가자가 사용자 지정 추적 레코드를 구독하려면 쿼리가 필요합니다.  
  
 추적 프로필 쿼리에 대 한 자세한 내용은 참조 하세요. [추적 프로필](../../../../../docs/framework/windows-workflow-foundation/tracking-profiles.md)합니다.
  
\<system.serviceModel>  
\<tracking>  
\<프로필 >  
\<trackingProfile>  
\<workflow>  
\<customTrackingQueries >  
  
## <a name="syntax"></a>구문  
  
```xml
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <customTrackingQueries>
          <customTrackingQuery activityName="String"
                               name="String"/>
        </customTrackingQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소

다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성

없음
  
### <a name="child-elements"></a>자식 요소
  
|요소|설명|  
|-------------|-----------------|  
|[\<customTrackingQuery >](customtrackingquery-of-wcf.md)|코드 활동에서 정의하는 이벤트를 추적하기 위해 사용되는 쿼리입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<workflow>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflow.md)|`activityDefinitionId` 속성에 의해 식별되는 특정 워크플로에 대한 모든 쿼리를 포함하는 구성 요소입니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Activities.Tracking.Configuration.CustomTrackingQueryElementCollection?displayProperty=nameWithType>       
- <xref:System.Activities.Tracking.CustomTrackingQuery?displayProperty=nameWithType>       
- [워크플로 추적](../../../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md)  
- [추적 프로필](../../../../../docs/framework/windows-workflow-foundation/tracking-profiles.md)
