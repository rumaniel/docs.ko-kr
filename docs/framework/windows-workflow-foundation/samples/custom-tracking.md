---
title: 사용자 지정 추적
ms.date: 03/30/2017
ms.assetid: 2d191c9f-62f4-4c63-92dd-cda917fcf254
ms.openlocfilehash: 32abf1dc4c9607b4a86f836fa2c759af1dbf1b69
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989408"
---
# <a name="custom-tracking"></a>사용자 지정 추적
이 샘플에서는 사용자 지정 추적 참가자를 만들고 추적 데이터의 내용을 콘솔에 쓰는 방법을 보여 줍니다. 또한 사용자 정의 데이터로 채워진 <xref:System.Activities.Tracking.CustomTrackingRecord> 개체를 내보내는 방법도 보여 줍니다. 콘솔 기반 추적 참가자는 코드로 만든 추적 프로필 개체를 사용하여 워크플로에서 내보낸 <xref:System.Activities.Tracking.TrackingRecord> 개체를 필터링합니다.

## <a name="sample-details"></a>샘플 세부 정보
 WF (Windows Workflow Foundation)는 워크플로 인스턴스 실행을 추적 하기 위한 추적 인프라를 제공 합니다. 추적 런타임은 워크플로 인스턴스를 구현하여 워크플로 수명 주기와 관련된 이벤트, 워크플로 활동의 이벤트 및 사용자 지정 추적 이벤트를 내보냅니다. 다음 표에서는 추적 인프라의 기본 구성 요소에 대해 자세히 설명합니다

|구성 요소|설명|
|---------------|-----------------|
|추적 런타임|추적 레코드를 내보낼 인프라를 제공합니다.|
|추적 참가자|추적 레코드를 사용합니다. [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)]에는 추적 레코드를 ETW(Windows용 이벤트 추적) 이벤트로 기록하는 추적 참가자가 제공됩니다.|
|추적 프로필|추적 참가자가 워크플로 인스턴스에서 내보낸 추적 레코드의 하위 집합을 구독할 수 있도록 하는 필터링 메커니즘입니다.|

 다음 표에서는 워크플로 런타임에서 내보내는 추적 레코드에 대해 자세히 설명합니다.

|추적 레코드|설명|
|---------------------|-----------------|
|워크플로 인스턴스 추적 레코드|워크플로 인스턴스의 수명 주기에 대해 설명합니다. 예를 들어 워크플로가 시작되거나 완료되면 인스턴스 레코드를 내보냅니다.|
|활동 상태 추적 레코드|활동 실행에 대해 자세히 설명합니다. 이러한 레코드는 활동이 예약된 시점, 활동이 완료된 시점, 오류가 throw된 시점 등과 같은 워크플로 활동 상태를 나타냅니다.|
|책갈피 다시 시작 레코드|워크플로 인스턴스 내의 책갈피를 다시 시작할 때마다 내보냅니다.|
|사용자 지정 추적 레코드|워크플로 작성자가 사용자 지정 추적 레코드를 만들어 사용자 지정 활동 중에 내보낼 수 있습니다.|

 추적 참가자는 추적 프로필을 사용하여 내보낸 <xref:System.Activities.Tracking.TrackingRecord> 개체의 하위 집합을 구독합니다. 추적 프로필에는 특정 추적 레코드 형식을 구독할 수 있도록 허용하는 추적 쿼리가 포함됩니다. 추적 프로필은 코드나 구성에 지정할 수 있습니다.

### <a name="custom-tracking-participant"></a>사용자 지정 추적 참가자
 추적 참가자 API를 사용하면 워크플로 런타임에서 내보낸 <xref:System.Activities.Tracking.TrackingRecord> 개체를 처리하기 위한 사용자 지정 논리를 포함할 수 있는 사용자 제공 추적 참가자를 사용하여 추적 런타임을 확장할 수 있습니다.

 추적 참가자를 기록하려면 사용자가 <xref:System.Activities.Tracking.TrackingParticipant>를 구현해야 합니다. 특히 사용자 지정 참가자는 <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 메서드를 구현해야 합니다. 이 메서드는 워크플로 런타임에서 <xref:System.Activities.Tracking.TrackingRecord>를 내보낼 때 호출됩니다.

```csharp
public abstract class TrackingParticipant
{
    protected TrackingParticipant();

    public virtual TrackingProfile TrackingProfile { get; set; }
    public abstract void Track(TrackingRecord record, TimeSpan timeout);
}
```

 ConsoleTrackingParticipant.cs 파일에서 전체 추적 참가자가 구현 됩니다. 다음 코드 예제 <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 는 사용자 지정 추적 참가자에 대 한 메서드입니다.

```csharp
protected override void Track(TrackingRecord record, TimeSpan timeout)
{
    ...
    WorkflowInstanceRecord workflowInstanceRecord = record as WorkflowInstanceRecord;
    if (workflowInstanceRecord != null)
    {
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,
            " Workflow InstanceID: {0} Workflow instance state: {1}",
            record.InstanceId, workflowInstanceRecord.State));
    }

    ActivityStateRecord activityStateRecord = record as ActivityStateRecord;
    if (activityStateRecord != null)
    {
        IDictionary<String, object> variables = activityStateRecord.Variables;
        StringBuilder vars = new StringBuilder();

        if (variables.Count > 0)
        {
            vars.AppendLine("\n\tVariables:");
            foreach (KeyValuePair<string, object> variable in variables)
            {
                vars.AppendLine(String.Format(
                    "\t\tName: {0} Value: {1}", variable.Key, variable.Value));
            }
        }
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,
            " :Activity DisplayName: {0} :ActivityInstanceState: {1} {2}",
                activityStateRecord.Activity.Name, activityStateRecord.State,
            ((variables.Count > 0) ? vars.ToString() : String.Empty)));
    }

    CustomTrackingRecord customTrackingRecord = record as CustomTrackingRecord;

    if ((customTrackingRecord != null) && (customTrackingRecord.Data.Count > 0))
    {
        ...
    }
    Console.WriteLine();

}
```

 다음 코드 예제에서는 워크플로 호출자에 콘솔 참가자를 추가합니다.

```csharp
ConsoleTrackingParticipant customTrackingParticipant = new ConsoleTrackingParticipant()
{
    ...
    // The tracking profile is set here, refer to Program.CS
...
}

WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());
invoker.Extensions.Add(customTrackingParticipant);
```

### <a name="emitting-custom-tracking-records"></a>사용자 지정 추적 레코드 내보내기
 이 샘플에서는 사용자 지정 워크플로 활동에서 <xref:System.Activities.Tracking.CustomTrackingRecord> 개체를 내보내는 기능도 보여 줍니다.

- <xref:System.Activities.Tracking.CustomTrackingRecord> 개체가 만들어지고, 레코드와 함께 내보낼 사용자 정의 데이터로 채워집니다.

- 는의 track 메서드를 호출 하 여 내보내집니다. <xref:System.Activities.ActivityContext> <xref:System.Activities.Tracking.CustomTrackingRecord>

 다음 예제에서는 사용자 지정 활동에서 <xref:System.Activities.Tracking.CustomTrackingRecord> 개체를 내보내는 방법을 보여 줍니다.

```csharp
// Create the Custom Tracking Record
CustomTrackingRecord customRecord = new CustomTrackingRecord("OrderIn")
{
    Data =
    {
        {"OrderId", 200},
        {"OrderDate", "20 Aug 2001"}
    }
};

// Emit custom tracking record
context.Track(customRecord);
```

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. Visual Studio 2010을 사용 하 여 CustomTrackingSample .sln 솔루션 파일을 엽니다.

2. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

3. Ctrl+F5를 눌러 솔루션을 실행합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\CustomTracking`  
  
## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
