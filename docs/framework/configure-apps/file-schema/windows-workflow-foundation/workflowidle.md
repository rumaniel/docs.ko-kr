---
title: <workflowIdle>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: b2ef703c-3e01-4213-9d2e-c14c7dba94d2
ms.openlocfilehash: 1d8ddaf5d69d87ff6112b5cbb285f0ccfda724e2
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70397532"
---
# <a name="workflowidle"></a>\<workflowIdle>
유휴 워크플로 인스턴스가 언로드되고 유지되는 시간을 제어하는 서비스 동작입니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<컴퓨터. ServiceModel >** ](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<workflowIdle >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <workflowIdle timeToPersist="TimeSpan" 
                    timeToUnload="TimeSpan" />
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|timeToPersist|워크플로가 유휴 상태가 되 고 유지 되는 시간 사이의 기간을 지정 하는 Timespan 값입니다. 기본값은 Int32.maxvalue입니다.<br /><br /> 워크플로 인스턴스가 유휴 상태가 되면 기간이 경과되기 시작합니다. 이 특성은 인스턴스가 최대한 오랫동안 메모리에 유지 되는 동안 워크플로 인스턴스를 적극적으로 유지 하려는 경우에 유용 합니다. 이 특성은 해당 값이 **timeToUnload** 특성 보다 작은 경우에만 유효 합니다. 이보다 크면 무시됩니다. 이 특성이 **timeToUnload** 특성에 지정 된 값 보다 앞에 경과할 경우 워크플로가 언로드되기 전에 지 속성이 완료 되어야 합니다. 이것은 워크플로가 유지될 때까지 언로드 작업이 지연될 수 있음을 의미합니다. 지속성 계층은 일시적인 오류가 발생할 경우 재시도를 처리하고 복구할 수 없는 오류가 발생하는 경우에만 예외를 throw하는 역할을 담당합니다. 따라서 유지 중에 throw되는 예외는 심각한 예외로 간주되며 워크플로 인스턴스가 중단됩니다.|  
|timeToUnload|워크플로가 유휴 상태가 되고 언로드되는 시간 간의 기간을 지정하는 Timespan 값입니다. 기본값은 1분입니다.<br /><br /> 워크플로를 언로드한다는 것은 이를 유지한다는 의미이기도 합니다. 이 특성이 0으로 설정 되 면 워크플로가 유휴 상태가 되는 즉시 워크플로 인스턴스가 유지 되 고 언로드됩니다. 이 특성을 Int32.maxvalue로 설정 하면 언로드 작업이 효과적으로 사용 되지 않습니다. 즉, 유휴 워크플로 인스턴스가 언로드되지 않습니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<servicebehaviors의 \<동작 > >](behavior-of-servicebehaviors-of-workflow.md)|동작 요소를 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior>
- <xref:System.ServiceModel.Activities.Configuration.WorkflowIdleElement>
