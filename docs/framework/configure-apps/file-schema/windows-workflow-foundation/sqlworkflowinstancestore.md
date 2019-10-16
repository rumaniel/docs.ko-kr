---
title: <sqlWorkflowInstanceStore>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 8a4e4214-fc51-4f4d-b968-0427c37a9520
ms.openlocfilehash: 581da860a490c95d5d621194c7f6643fc15118fe
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398680"
---
# <a name="sqlworkflowinstancestore"></a>\<sqlWorkflowInstanceStore>
구성할 수 있는 서비스 동작을 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 워크플로 서비스 인스턴스를 SQL Server 2005 또는 SQL Server 2008 데이터베이스에 대 한 상태 정보 유지를 지 원하는 기능을 합니다. 이 기능에 대 한 자세한 내용은 [SQL 워크플로 인스턴스 저장소](../../../windows-workflow-foundation/sql-workflow-instance-store.md)를 참조 하세요.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<컴퓨터. ServiceModel >** ](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<sqlWorkflowInstanceStore >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <sqlWorkflowInstanceStore connectionStringName="String" 
                                hostLockRenewalPeriod="TimeSpan" 
                                instanceCompletionAction="DeleteNothing/DeleteAll" 
                                instanceEncodingAction="None/GZip" 
                                instanceLockedExceptionAction="NoRetry/BasicRetry/AggressiveRetry" 
                                runnableInstancesDetectionPeriod="TimeSpan" />
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|connectionString|기본 지 속성 데이터베이스에 연결 하는 데 사용 되는 연결 문자열을 포함 하는 문자열입니다.|  
|connectionStringName|데이터베이스 서버에 대 한 명명 된 연결 문자열을 포함 하는 문자열입니다. 명명된 된 연결 문자열의 예로 "defaultconnectionstring"입니다.|  
|hostLockRenewalPeriod|호스트에서 인스턴스에 대한 잠금을 갱신해야 하는 기간을 지정하는 Timespan 값입니다. 호스트에서 지정된 기간 내에 잠금을 갱신하지 않으면 인스턴스 잠금이 해제되어 다른 호스트가 이를 선택할 수 있습니다.<br /><br /> 워크플로를 언로드한다는 것은 이를 유지한다는 의미이기도 합니다. 이 특성이 0으로 설정 되 면 워크플로가 유휴 상태가 되는 즉시 워크플로 인스턴스가 유지 되 고 언로드됩니다. 이 특성을 Int32.maxvalue로 설정 하면 언로드 작업이 효과적으로 사용 되지 않습니다. 즉, 유휴 워크플로 인스턴스가 언로드되지 않습니다.|  
|instanceCompletionAction|워크플로 인스턴스가 완료되면 워크플로 인스턴스 데이터가 지속성 저장소에 보관되는지 아니면 해당 시점에 삭제되는지를 지정하는 값입니다. 이 값은 <xref:System.Activities.DurableInstancing.InstanceCompletionAction> 형식입니다.<br /><br /> 열거된 동작은 인스턴스에서 해당 작업을 완료하면 지속성 저장소에서 인스턴스 데이터를 삭제하거나 지속성 저장소에서 인스턴스 데이터를 삭제하지 않는 것으로 구성됩니다.<br /><br /> 완료된 후 인스턴스를 유지하면 지속성 데이터베이스가 빠르게 커지고 데이터베이스 성능에 영향을 주게 됩니다. 성능 요구 사항을 충족하는 수준으로 데이터베이스 성능을 유지하려면 이러한 레코드를 주기적으로 삭제하는 데이터베이스 비우기 정책을 구성해야 합니다.|  
|instanceEncodingOption|정보를 지속성 저장소에 저장하기 전에 인스턴스 상태 정보를 GZip 알고리즘을 사용하여 압축할지 여부를 지정하는 선택적 값입니다. 이 값은 <xref:System.Activities.DurableInstancing.InstanceEncodingOption> 형식입니다. 이 속성에 사용할 수 있는 <xref:System.Activities.DurableInstancing.InstanceEncodingOption.None>값은 압축 안 함을 지정 <xref:System.Activities.DurableInstancing.InstanceEncodingOption.GZip>하 고,는 인스턴스 데이터를 압축 하 고 gzip 알고리즘을 사용 하도록 지정 하는입니다.|  
|instanceLockedExceptionAction|호스트에서 인스턴스를 잠그려고 할 때 현재 다른 호스트에서 해당 인스턴스를 잠근 경우에 throw되는 예외에 대한 응답으로 발생하는 동작을 지정하는 값입니다. 이 값은 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> 형식입니다.<br /><br /> 이 필드에 사용할 수 있는 옵션은 다음과 같습니다. 없음, 기본 다시 시도, 적극적으로 다시 시도 합니다. 기본값은 None입니다. 다음은 이러한 세 옵션에 대한 설명입니다.<br /><br /> - 없음 서비스 호스트가 인스턴스 잠금을 시도하지 않고 <xref:System.Runtime.DurableInstancing.InstanceLockedException>을 호출자에게 전달합니다.<br />-기본 다시 시도. 서비스 호스트가 선형 다시 시도 간격을 사용하여 인스턴스 잠금을 다시 시도하고 시퀀스의 끝에 예외를 호출자에게 전달합니다.<br />-적극적인 다시 시도. 서비스 호스트에서 지연 간격을 기하급수적으로 증가시켜 인스턴스 잠금을 다시 시도하고 시퀀스 마지막에 <xref:System.Runtime.DurableInstancing.InstanceLockedException>을 호출자에게 전달합니다.|  
|runnableInstancesDetectionPeriod||  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<servicebehaviors의 \<동작 > >](behavior-of-servicebehaviors-of-workflow.md)|동작 요소를 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>
- <xref:System.ServiceModel.Activities.Configuration.SqlWorkflowInstanceStoreElement>
- <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>
- [SQL 워크플로 인스턴스 저장소](../../../windows-workflow-foundation/sql-workflow-instance-store.md)
