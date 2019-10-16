---
title: <workflowRuntime>
ms.date: 03/30/2017
ms.assetid: 304c70fa-78d1-4d0f-b89f-0ca23d734c6f
ms.openlocfilehash: d12656b77fa219080382603fd04a542d2fa9064a
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399081"
---
# <a name="workflowruntime"></a>\<workflowRuntime>
WCF (워크플로 기반 Windows Communication Foundation) <xref:System.Workflow.Runtime.WorkflowRuntime> 서비스를 호스팅하기 위한의 인스턴스에 대 한 설정을 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<workflowRuntime >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<workflowRuntime cachedInstanceExpiration="TimeSpan"
                 enablePerformanceCounters="Boolean"
                 name="String"
                 validateOnCreate="Boolean">
  <commonParameters>
    <add name="String"
         value="String" />
  </commonParameters>
  <services>
    <add type="String" />
  </services>
</workflowRuntime>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|cachedInstanceExpiration|워크플로 인스턴스가 강제로 언로드되거나 중단되기 전에 메모리에 유휴 상태로 유지될 수 있는 최대 기간을 지정하는 선택적 <xref:System.TimeSpan> 값입니다. workflowruntime에 unloadOnIdle을 수행하는 `PersistenceService`가 있으면 이 특성이 무시됩니다.|  
|enablePerformanceCounters|성능 카운터를 사용하는지 여부를 지정하는 선택적 부울 값입니다. 성능 카운터는 다양한 워크플로 관련 통계에 대한 정보를 제공하지만 워크플로 런타임 엔진이 시작될 때 및 워크플로 인스턴스가 실행되고 있을 때 성능을 저하시킵니다. 기본값은 `true`입니다.|  
|name|워크플로 런타임 엔진의 이름을 포함하는 문자열입니다. 이름은 시스템(예: 성능 카운터)에서 실행 중일 수 있는 다른 런타임과 이 런타임을 구분하기 위해 출력에서 사용됩니다.<br /><br /> 기본값은 빈 문자열입니다.|  
|validateOnCreate|WorkflowServiceHost가 열릴 때 워크플로 정의의 유효성 검사를 실시할지 여부를 지정하는 선택적 부울 값입니다.  이 특성을 `true`로 설정하면 `WorkflowServiceHost.Open`을 호출할 때마다 워크플로 유효성 검사가 실행됩니다. 유효성 검사 오류가 발견되면 <xref:System.Workflow.ComponentModel.Compiler.WorkflowValidationFailedException> 오류가 throw됩니다.<br /><br /> 이 속성을 `false`로 설정하면 워크플로 정의 유효성 검사가 실행되지 않습니다.<br /><br /> 이 속성의 기본값은 `true`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|commonParameters|서비스에서 사용하는 일반 매개 변수 컬렉션입니다. 일반적으로 이 컬렉션에는 영속 서비스에서 공유할 수 있는 데이터베이스 연결 문자열이 포함됩니다.|  
|서비스|<xref:System.Workflow.Runtime.WorkflowRuntime> 엔진에 추가할 서비스 컬렉션입니다. 요소는 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement> 형식입니다.  컬렉션에 지정된 서비스는 워크플로 런타임 엔진에 의해 초기화되며 해당 <xref:System.Workflow.Runtime.WorkflowRuntime> 생성자를 호출할 때 서비스에 추가됩니다. 따라서 컬렉션에 지정된 서비스는 생성자의 시그니처에 대한 특정 규칙을 따라야 합니다. 자세한 내용은 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>를 참조하세요.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|동작 요소를 지정합니다.|  
  
## <a name="remarks"></a>설명  
 구성 파일을 사용 하 여 Windows Workflow Foundation 호스트 응용 프로그램 <xref:System.Workflow.Runtime.WorkflowRuntime> 개체의 동작을 제어 하는 방법에 대 한 자세한 내용은 [워크플로 구성 파일](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))을 참조 하세요.  
  
## <a name="example"></a>예제  
  
```xml  
<serviceBehaviors>
   <behavior name="ServiceBehavior">
      <workflowRuntime name="WorkflowServiceHostRuntime"
                       validateOnCreate="true"
                       enablePerformanceCounters="true">
         <commonParameters>
            <add name="ConnectionString" value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />
            <add name="EnableRetries" value="True" />
         </commonParameters>
         <services>
             <add type="NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common.TestPersistenceService.FilePersistenceService, NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common"/>
         </services>
      </workflowRuntime>
   </behavior>
</serviceBehaviors>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>
- <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>
- <xref:System.Workflow.Runtime.WorkflowRuntime>
- [워크플로 구성 파일](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))
