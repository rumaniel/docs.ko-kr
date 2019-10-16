---
title: 추적 프로필
ms.date: 03/30/2017
ms.assetid: 22682566-1cd9-4672-9791-fb3523638e18
ms.openlocfilehash: a643cf37bbb3e72baefb434249aa54b386060627
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67660920"
---
# <a name="tracking-profiles"></a>추적 프로필

추적 프로필에는 추적 참가자가 런타임에 워크플로 인스턴스 상태가 변경될 때 발생하는 워크플로 이벤트를 구독할 수 있도록 허용하는 추적 쿼리가 포함됩니다.

## <a name="tracking-profiles"></a>추적 프로필

워크플로 인스턴스에 내보낼 추적 정보를 지정하는 데 사용되는 추적 프로필입니다. 프로필을 지정하지 않으면 모든 추적 이벤트를 내보냅니다. 프로필을 지정하면 프로필에 지정된 추적 이벤트를 내보냅니다. 모니터링 요구 사항에 따라 워크플로에서 상위 수준의 상태 변경 내용 중 작은 부분만 구독하는 매우 개괄적인 프로필을 작성할 수 있습니다. 이와 반대로 이후에 세부 실행 흐름을 다시 작성할 수 있을 정도로 상세한 결과 이벤트를 포함하는 아주 자세한 프로필을 만들 수도 있습니다.

추적 프로필을 표준.NET Framework 구성 파일 내에서 XML 요소로 나타날 하거나 코드에서 지정 합니다. 다음 예제에서는 추적 참가자가 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 및 `Started` 워크플로 이벤트를 구독할 수 있도록 하는 구성 파일의 `Completed` 추적 프로필을 보여 줍니다.

```xml
<system.serviceModel>
    ...
    <tracking>
      <trackingProfile name="Sample Tracking Profile">
        <workflow activityDefinitionId="*">
          <workflowInstanceQueries>
            <workflowInstanceQuery>
              <states>
                <state name="Started"/>
                <state name="Completed"/>
              </states>
            </workflowInstanceQuery>
          </workflowInstanceQueries>
        </workflow>
      </trackingProfile>
    </profiles>
  </tracking>
    ...
</system.serviceModel>
```

다음 예제에서는 코드를 사용하여 만든 동일한 추적 프로필을 보여 줍니다.

```csharp
TrackingProfile profile = new TrackingProfile()
{
    Name = "CustomTrackingProfile",
    Queries =
    {
        new WorkflowInstanceQuery()
        {
            // Limit workflow instance tracking records for started and
            // completed workflow states.
            States = { WorkflowInstanceStates.Started, WorkflowInstanceStates.Completed },
        }
    }
};
```

추적 레코드는 <xref:System.Activities.Tracking.ImplementationVisibility> 특성을 사용하여 추적 프로필의 표시 모드를 통해 필터링됩니다. 복합 활동은 구현을 구성하는 다른 활동을 포함하는 최상위 활동입니다. 표시 모드는 구현을 구성하는 활동을 추적할지 여부를 지정하기 위하여 워크플로 활동 내의 복합 활동에서 내보내는 추적 레코드를 지정합니다. 표시 모드는 추적 프로필 수준에서 적용됩니다. 워크플로의 개별 활동에 대한 추적 레코드 필터링은 추적 프로필 내에서 쿼리에 의해 제어됩니다. 자세한 내용은 참조는 **추적 프로필 쿼리 형식** 이 문서의 섹션입니다.

추적 프로필의 `implementationVisibility` 특성은 두 가지 표시 모드(`RootScope` 및 `All`)를 지정합니다. 복합 활동이 워크플로의 루트가 아닌 경우 `RootScope` 모드를 사용하면 활동의 구현을 구성하는 활동에 대한 추적 레코드가 표시되지 않습니다. 즉, 다른 활동을 사용하여 구현되는 활동이 워크플로에 추가되고 `implementationVisibility`가 RootScope로 설정된 경우에는 해당 복합 활동의 최상위 활동만 추적됩니다. 활동이 워크플로의 루트인 경우 활동 구현이 워크플로 자체이고 구현 단계를 구성하는 활동에 대한 추적 레코드가 내보내집니다. 모두 모드에서는 루트 활동과 모든 복합 활동에 대해 모든 추적 레코드가 내보내집니다.

예를 들어 *MyActivity* 구현이 두 활동을 포함 하는 복합 활동 *Activity1* 하 고 *Activity2*합니다. 경우이 활동을 워크플로에 추가 하 고 추적을 사용 하 여 추적 프로필을 사용 하 여 사용 하도록 `implementationVisibility` 로 설정 `RootScope`에 대해서만 추적 레코드가 내보내집니다 *MyActivity*합니다. 하지만 활동에 대 한 레코드가 내보내지지 않습니다 *Activity1* 하 고 *Activity2*합니다.

그러나 경우를 `implementationVisibility` 추적 프로필이로 설정 된 특성이 `All`, 다음 아니라 추적 레코드가 내보내집니다 *MyActivity*, 있지만 활동에도 *Activity1* 및  *Activity2*합니다.

`implementationVisibility` 플래그가 적용되는 추적 레코드 형식은 다음과 같습니다.

- ActivityStateRecord

- FaultPropagationRecord

- CancelRequestedRecord

- ActivityScheduledRecord

> [!NOTE]
> 활동 구현에서 내보내는 CustomTrackingRecords는 implementationVisibility 설정에 의해 필터링되지 않습니다.

`implementationVisibility` 기능은 코드의 추적 프로필에서 다음과 같이 <xref:System.Activities.Tracking.ImplementationVisibility.RootScope>로 지정됩니다.

```csharp
TrackingProfile sampleTrackingProfile = new TrackingProfile()
{
    Name = "Sample Tracking Profile",
    ImplementationVisibility = ImplementationVisibility.RootScope
};
```

`implementationVisibility` 기능은 구성 파일의 추적 프로필에서 다음과 같이 <xref:System.Activities.Tracking.ImplementationVisibility.All>로 지정됩니다.

```xml
<tracking>
      <profiles>
        <trackingProfile name="Shipping Monitoring" implementationVisibility="All">
          <workflow activityDefinitionId="*">
...
         </workflow>
        </trackingProfile>
      </profiles>
</tracking>
```

추적 프로필의 `ImplementationVisibility` 설정은 선택 사항입니다. 기본적으로 이 값은 `RootScope`로 설정됩니다. 또한 이 특성 값은 대/소문자가 구분됩니다.

### <a name="tracking-profile-query-types"></a>추적 프로필 쿼리 형식

추적 프로필은 특정 추적 레코드에 대한 워크플로 런타임을 쿼리할 수 있는 추적 레코드에 대한 선언적 구독으로 구성됩니다. <xref:System.Activities.Tracking.TrackingRecord> 개체의 다양한 클래스를 구독할 수 있는 여러 쿼리 형식이 있습니다. 추적 프로필은 구성이나 코드를 통해 지정할 수 있습니다. 가장 일반적인 쿼리 형식은 다음과 같습니다.

- <xref:System.Activities.Tracking.WorkflowInstanceQuery> - 앞에서 설명한 `Started` 및 `Completed`와 같은 워크플로 인스턴스 수명 주기 변경 내용을 추적하려면 이 쿼리 형식을 사용합니다. <xref:System.Activities.Tracking.WorkflowInstanceQuery>는 다음 <xref:System.Activities.Tracking.TrackingRecord> 개체를 구독하는 데 사용됩니다.

  - <xref:System.Activities.Tracking.WorkflowInstanceRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceAbortedRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceTerminatedRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceSuspendedRecord>

  구독 가능한 상태는 <xref:System.Activities.Tracking.WorkflowInstanceStates> 클래스에서 지정됩니다.

  다음 예제에서는 `Started`를 사용하여 <xref:System.Activities.Tracking.WorkflowInstanceQuery> 인스턴스에 대한 워크플로 인스턴스 수준 추적 레코드를 구독하는 데 사용되는 구성 또는 코드를 보여 줍니다.

  ```xml
  <workflowInstanceQueries>
      <workflowInstanceQuery>
        <states>
          <state name="Started"/>
        </states>
      </workflowInstanceQuery>
  </workflowInstanceQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new WorkflowInstanceQuery()
          {
              States = { WorkflowInstanceStates.Started}
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.ActivityStateQuery> - 워크플로 인스턴스를 구성하는 활동에 대한 수명 주기 변경 내용을 추적하려면 이 쿼리 형식을 사용합니다. 예를 들어 다음 워크플로 인스턴스 내에 "전자 메일 보내기" 활동이 완료 될 때마다 추적 하는 것이 좋습니다. 이 쿼리는 <xref:System.Activities.Tracking.TrackingParticipant>가 <xref:System.Activities.Tracking.ActivityStateRecord> 개체를 구독하는 데 필요합니다. 구독하기 위해 사용 가능한 상태는 <xref:System.Activities.Tracking.ActivityStates>에서 지정됩니다.

  다음 예제에서는 <xref:System.Activities.Tracking.ActivityStateQuery> 활동에 대해 `SendEmailActivity`를 사용하는 활동 상태 추적 레코드를 구독하는 데 사용되는 구성과 코드를 보여 줍니다.

  ```xml
  <activityStateQueries>
    <activityStateQuery activityName="SendEmailActivity">
      <states>
        <state name="Closed"/>
      </states>
    </activityStateQuery>
  </activityStateQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new ActivityStateQuery()
          {
              ActivityName = "SendEmailActivity",
              States = { ActivityStates.Closed }
          }
      }
  };
  ```

  > [!NOTE]
  > 여러 activityStateQuery 요소에 동일한 이름을 사용할 경우 마지막 요소의 상태만 추적 프로필에 사용됩니다.

- <xref:System.Activities.Tracking.ActivityScheduledQuery> - 이 쿼리를 사용하여 부모 활동에 의해 실행이 예약된 활동을 추적할 수 있습니다. 이 쿼리는 <xref:System.Activities.Tracking.TrackingParticipant>가 <xref:System.Activities.Tracking.ActivityScheduledRecord> 개체를 구독하는 데 필요합니다.

  다음 예제에서는 `SendEmailActivity`를 사용하여 예약된 <xref:System.Activities.Tracking.ActivityScheduledQuery> 자식 활동 관련 레코드를 구독하는 데 사용되는 구성과 코드를 보여 줍니다.

  ```xml
  <activityScheduledQueries>
    <activityScheduledQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />
  </activityScheduledQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new ActivityScheduledQuery()
          {
              ActivityName = "ProcessNotificationsActivity",
              ChildActivityName = "SendEmailActivity"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.FaultPropagationQuery> - 활동에서 발생하는 오류 처리를 추적하려면 이 쿼리 형식을 사용합니다. 이 쿼리는 <xref:System.Activities.Tracking.TrackingParticipant>가 <xref:System.Activities.Tracking.FaultPropagationRecord> 개체를 구독하는 데 필요합니다.

  다음 예제에서는 <xref:System.Activities.Tracking.FaultPropagationQuery>를 사용하여 오류 전파 관련 레코드를 구독하는 데 사용되는 구성과 코드를 보여 줍니다.

  ```xml
  <faultPropagationQueries>
    <faultPropagationQuery faultSourceActivityName="SendEmailActivity" faultHandlerActivityName="NotificationsFaultHandler" />
  </faultPropagationQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new FaultPropagationQuery()
          {
              FaultSourceActivityName = "SendEmailActivity",
              FaultHandlerActivityName = "NotificationsFaultHandler"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.CancelRequestedQuery> - 부모 활동에 의한 자식 활동 취소 요청을 추적하려면 이 쿼리 형식을 사용합니다. 이 쿼리는 <xref:System.Activities.Tracking.TrackingParticipant>가 <xref:System.Activities.Tracking.CancelRequestedRecord> 개체를 구독하는 데 필요합니다.

  구성 및 레코드를 구독 하는 데 사용 되는 코드를 사용 하 여 활동 취소 관련 <xref:System.Activities.Tracking.CancelRequestedQuery> 다음 예와에서 같습니다.

  ```xml
  <cancelRequestedQueries>
    <cancelRequestedQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />
  </cancelRequestedQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new CancelRequestedQuery()
          {
              ActivityName = "ProcessNotificationsActivity",
              ChildActivityName = "SendEmailActivity"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.CustomTrackingQuery> - 코드 활동에서 정의한 이벤트를 추적하려면 이 쿼리 형식을 사용합니다. 이 쿼리는 <xref:System.Activities.Tracking.TrackingParticipant>가 <xref:System.Activities.Tracking.CustomTrackingRecord> 개체를 구독하는 데 필요합니다.

  다음 예제에서는 <xref:System.Activities.Tracking.CustomTrackingQuery>를 사용하여 사용자 지정 추적 레코드 관련 레코드를 구독하는 데 사용되는 구성과 코드를 보여 줍니다.

  ```xml
  <customTrackingQueries>
    <customTrackingQuery name="EmailAddress" activityName="SendEmailActivity" />
  </customTrackingQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new CustomTrackingQuery()
          {
              Name = "EmailAddress",
              ActivityName = "SendEmailActivity"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.BookmarkResumptionQuery> - 워크플로 인스턴스 내의 책갈피 다시 시작을 추적하려면 이 쿼리 형식을 사용합니다. 이 쿼리는 <xref:System.Activities.Tracking.TrackingParticipant>가 <xref:System.Activities.Tracking.BookmarkResumptionRecord> 개체를 구독하는 데 필요합니다.

  다음 예제에서는 <xref:System.Activities.Tracking.BookmarkResumptionQuery>를 사용하여 책갈피 다시 시작 관련 레코드를 구독하는 데 사용되는 구성과 코드를 보여 줍니다.

  ```xml
  <bookmarkResumptionQueries>
    <bookmarkResumptionQuery name="SentEmailBookmark" />
  </bookmarkResumptionQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new BookmarkResumptionQuery()
          {
              Name = "sentEmailBookmark"
          }
      }
  };
  ```

### <a name="annotations"></a>주석

주석을 사용하여 빌드 시간 후에 구성될 수 있는 값으로 추적 레코드에 임의 태그를 지정할 수 있습니다. "Mail Server"으로 태그를 지정 하는 여러 워크플로에 걸쳐 여러 추적 레코드를 사용할 수는 예를 들어 "메일 Server1" = =. 이렇게 하면 나중에 추적 레코드를 쿼리할 때 이 태그를 사용하여 모든 레코드를 쉽게 찾을 수 있습니다.

이렇게 하려면 다음 예제와 같이 추적 쿼리에 주석을 추가합니다.

```xml
<activityStateQuery activityName="SendEmailActivity">
  <states>
    <state name="Closed"/>
  </states>
  <annotations>
    <annotation name="MailServer" value="Mail Server1"/>
  </annotations>
</activityStateQuery>
```

### <a name="how-to-create-a-tracking-profile"></a>추적 프로필을 만드는 방법

추적 쿼리 요소를 사용하면 XML 구성 파일 또는 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 코드를 통해 추적 프로필을 만들 수 있습니다. 다음은 구성 파일을 사용하여 만든 추적 프로필의 예입니다.

```xml
<system.serviceModel>
  <tracking>
    <profiles>
      <trackingProfile name="Sample Tracking Profile ">
        <workflow activityDefinitionId="*">
          <!--Specify the tracking profile query elements to subscribe for tracking records-->
        </workflow>
      </trackingProfile>
    </profiles>
  </tracking>
</system.serviceModel>
```

> [!WARNING]
> 워크플로 서비스 호스트를 사용하는 WF의 경우 일반적으로 구성 파일을 사용하여 추적 프로필을 만듭니다. 추적 프로필 및 추적 쿼리 API를 사용하여 코드를 통해 추적 프로필을 만들 수도 있습니다.

XML 구성 파일로 구성된 프로필은 동작 확장을 사용하여 추적 참가자에게 적용됩니다. 이후 섹션에 설명 된 대로 WorkflowServiceHost에 추가 됩니다 [워크플로에 대 한 추적 구성](configuring-tracking-for-a-workflow.md)합니다.

호스트에서 내보내는 추적 레코드의 자세한 정도는 추적 프로필의 구성 설정에 따라 결정됩니다. 추적 참가자는 쿼리를 추적 프로필에 추가하여 추적 레코드를 구독합니다. 모든 추적 레코드를 구독 하려면 추적 프로필을 사용 하 여 모든 추적 쿼리를 지정 해야 "\*" 각 쿼리의 이름 필드에 있습니다.

다음은 추적 프로필의 일반적인 몇 가지 예입니다.

- 워크플로 인스턴스 레코드 및 오류를 가져오는 추적 프로필

  ```xml
  <trackingProfile name="Instance and Fault Records">
    <workflow activityDefinitionId="*">
      <workflowInstanceQueries>
        <workflowInstanceQuery>
          <states>
            <state name="*" />
          </states>
        </workflowInstanceQuery>
      </workflowInstanceQueries>
      <activityStateQueries>
        <activityStateQuery activityName="*">
          <states>
            <state name="Faulted"/>
          </states>
        </activityStateQuery>
      </activityStateQueries>
    </workflow>
  </trackingProfile>
  ```

- 모든 사용자 지정 추적 레코드를 가져오는 추적 프로필

  ```xml
  <trackingProfile name="Instance_And_Custom_Records">
    <workflow activityDefinitionId="*">
      <customTrackingQueries>
        <customTrackingQuery name="*" activityName="*" />
      </customTrackingQueries>
    </workflow>
  </trackingProfile>
  ```

## <a name="see-also"></a>참고자료

- [SQL 추적](./samples/sql-tracking.md)
- [Windows Server App Fabric 모니터링](https://go.microsoft.com/fwlink/?LinkId=201273)
- [App Fabric을 사용 하 여 응용 프로그램 모니터링](https://go.microsoft.com/fwlink/?LinkId=201275)
