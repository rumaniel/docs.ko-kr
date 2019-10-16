---
title: <behavior><serviceBehaviors> of 워크플로
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 6a4b718a-1b40-4957-935a-f6122819ab3c
ms.openlocfilehash: 65bde45ffdd4af166d5b44308162c23257659802
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398886"
---
# <a name="behavior-of-servicebehaviors-of-workflow"></a>\<워크플로의 \<servicebehaviors > 동작 >
**Behavior** 요소는 서비스의 동작에 대 한 설정 컬렉션을 포함 합니다. 각 동작은 **이름**으로 인덱싱됩니다. 서비스는 [ \<끝점 >](../wcf/endpoint-element.md) 요소의 **behaviorConfiguration** 특성을 사용 하 여이 이름을 통해 각 동작에 연결할 수 있습니다. 따라서 설정을 다시 정의하지 않고도 엔드포인트에서 일반 동작 구성을 공유할 수 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<컴퓨터. ServiceModel >** ](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<동작 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.ServiceModel>  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="String">
        <bufferReceive maxPendingMessagesPerChannel="Integer" />
        <etwTracking profileName="String" />
        <sendMessageChannelCache allowUnsafeCaching="Boolean">
          <channelSettings idleTimeout="TimeSpan" 
                           leaseTimeout="TimeSpan" 
                           maxItemsInCache="Integer" />
          <factorySettings idleTimeout="TimeSpan" 
                           leaseTimeout="TimeSpan" 
                           maxItemsInCache="Integer" />
        </sendMessageChannelCache>
        <sqlWorkflowInstanceStore connectionStringName="String" 
                                  hostLockRenewalPeriod="TimeSpan" 
                                  instanceCompletionAction="DeleteNothing/DeleteAll" 
                                  instanceEncodingAction="None/GZip" 
                                  instanceLockedExceptionAction="NoRetry/BasicRetry/AggressiveRetry" 
                                  runnableInstancesDetectionPeriod="TimeSpan" />
        <workflowIdle timeToPersist="TimeSpan" 
                      timeToUnload="TimeSpan" />
        <workflowUnhandledException action="Abandon/AbandonAndSuspend/Cancel/Terminate" />
      </behavior>
    </serviceBehaviors>  
  </behaviors>  
</system.ServiceModel>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|name|동작의 구성 이름을 포함하는 고유 문자열입니다. 이 값은 요소의 식별 문자열 역할을 하므로 고유한 사용자 정의 문자열이어야 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<bufferReceive>](bufferreceive.md)|서비스에서 버퍼링되는 수신 처리를 사용할 수 있도록 하는 서비스 동작입니다. 이를 통해 워크플로 서비스가 순서가 맞지 않는 메시지를 처리할 수 있습니다.|  
|[\<routing>](../wcf/routing-of-servicebehavior.md)|사용 하 여 ETW 추적을 활용할 수 있도록 허용 하는 서비스 동작을 <xref:System.Activities.Tracking.EtwTrackingParticipant>입니다.|  
|[\<sendMessageChannelCache>](sendmessagechannelcache.md)|메시지 보내기 작업을 사용 하 여 서비스 끝점으로 메시지를 보내는 워크플로를 위한 채널 캐시 설정, 캐시 공유 수준의 사용자 지정 및 채널 팩터리 캐시 설정을 가능 하 게 하는 서비스 동작입니다.|  
|[\<sqlWorkflowInstanceStore>](sqlworkflowinstancestore.md)|구성할 수 있는 서비스 동작을 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 워크플로 서비스 인스턴스를 SQL Server 2005 또는 SQL Server 2008 데이터베이스에 대 한 상태 정보 유지를 지 원하는 기능을 합니다.|  
|[\<workflowIdle>](workflowidle.md)|유휴 워크플로 인스턴스가 언로드되고 유지되는 시간을 제어하는 서비스 동작입니다.|  
|[\<workflowInstanceManagement>](workflowinstancemanagement.md)|지속성 예외, 처리되지 않은 예외 동작 및 유휴 동작을 비롯하여 워크플로 인스턴스 실행 방법을 제어하는 설정을 지정할 수 있는 서비스 동작입니다.|  
|[\<workflowUnhandledException>](workflowunhandledexception.md)|워크플로 서비스 내에서 처리되지 않은 예외가 발생할 때 수행할 동작을 지정할 수 있는 서비스 동작입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<serviceBehaviors>](servicebehaviors-of-workflow.md)|서비스 동작 요소의 컬렉션입니다.|
