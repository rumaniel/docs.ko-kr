---
title: WCF의 &lt;cancelRequestedQuery&gt;
ms.date: 03/30/2017
ms.assetid: b690d870-02eb-4c56-8bc3-e5ca99d7097b
ms.openlocfilehash: 3943d604b586eec37a1d153f10ac049fc9bd5747
ms.sourcegitcommit: fd8d4587cc26e53f0e27e230d6e27d828ef4306b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49347571"
---
# <a name="ltcancelrequestedquerygt-of-wcf"></a>WCF의 &lt;cancelRequestedQuery&gt;

부모 활동에 의한 자식 활동 취소 요청을 추적하는 데 사용되는 쿼리를 나타냅니다. 추적 참가자가 취소 요청 레코드 개체를 구독하려면 쿼리가 필요합니다.  
  
추적 프로필 쿼리에 대 한 자세한 내용은 참조 하세요. [추적 프로필](../../../../../docs/framework/windows-workflow-foundation/tracking-profiles.md)합니다.
  
\<system.serviceModel>  
\<tracking>  
\<프로필 >  
\<trackingProfile>  
\<workflow>  
\<cancelRequestedQueries>  
\<cancelRequestedQuery >  
  
## <a name="syntax"></a>구문  
  
```xml
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <cancelRequestedQueries>
          <cancelRequestedQuery activityName="String"
                              childActivityName="String"/>
        </cancelRequestedQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>  
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`activityName`|취소를 요청하는 활동의 이름을 지정하는 문자열입니다.|  
|`childActivityName`|취소가 요청된 자식 활동의 이름을 지정하는 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소

없음
  
### <a name="parent-elements"></a>부모 요소
  
|요소|설명|  
|-------------|-----------------|  
|[\<cancelRequestedQueries>](cancelrequestedqueries-of-wcf.md)|부모 활동에 의한 자식 활동 취소 요청을 추적하는 데 사용되는 쿼리의 컬렉션을 나타냅니다.|  
  
## <a name="see-also"></a>참고자료  

- <xref:System.ServiceModel.Activities.Tracking.Configuration.CancelRequestedQueryElement?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.CancelRequestedQuery?displayProperty=nameWithType>
- [워크플로 추적](../../../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [추적 프로필](../../../../../docs/framework/windows-workflow-foundation/tracking-profiles.md)
