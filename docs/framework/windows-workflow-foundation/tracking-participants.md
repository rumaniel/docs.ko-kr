---
title: 추적 참가자
ms.date: 03/30/2017
ms.assetid: f13e360c-eeb7-4a49-98a0-8f6a52d64f68
ms.openlocfilehash: 45a92c3ab710fc9bc86fbf269a4672f1d34737cc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963681"
---
# <a name="tracking-participants"></a>추적 참가자
추적 참가자는 워크플로 개발자가 <xref:System.Activities.Tracking.InteropTrackingRecord.TrackingRecord%2A> 개체에 액세스하여 처리할 수 있는 확장성 지점입니다. [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]에는 추적 레코드를 ETW(Windows용 이벤트 추적) 이벤트로 기록하는 표준 추적 참가자가 포함되어 있습니다. 표준 참가자가 요구 사항에 맞지 않는 경우 사용자 지정 추적 참가자를 작성할 수도 있습니다.  
  
## <a name="tracking-participants"></a>추적 참가자  
 추적 인프라를 사용하면 참가자가 레코드 하위 집합을 구독할 수 있도록 보내는 추적 레코드에 필터를 적용할 수 있습니다. 필터를 적용하는 메커니즘은 추적 프로필을 사용합니다.  
  
 의 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] WF (Windows Workflow Foundation)는 추적 레코드를 ETW 세션에 기록 하는 추적 참가자를 제공 합니다. 추적 참가자는 워크플로 서비스에서 구성 파일에 추적별 동작을 추가하여 구성할 수 있습니다. ETW 추적 참가자를 사용하여 이벤트 뷰어에서 추적 레코드를 볼 수 있습니다. ETW 기반 추적에 대한 SDK 샘플을 사용하면 ETW 기반 추적 참가자를 사용하는 WF 추적을 쉽게 익힐 수 있습니다.  
  
## <a name="etw-tracking-participant"></a>ETW 추적 참가자  
 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]에는 추적 레코드를 ETW 세션에 기록하는 ETW 추적 참가자가 포함됩니다. 이 작업은 애플리케이션 성능이나 서버 처리량에 미치는 영향을 최소화하면서 매우 효율적인 방식으로 수행됩니다. 표준 ETW 추적 참가자를 사용하는 이점은 Windows 이벤트 뷰어에서 다른 애플리케이션 및 시스템 로그를 사용하여 참가자가 받는 추적 레코드를 볼 수 있다는 것입니다.  
  
 다음 예제와 같이 표준 ETW 추적 참가자는 Web.config 파일에서 구성됩니다.  
  
```xml  
<configuration>  
  <system.web>  
    <compilation debug="true" targetFramework="4.0" />  
  </system.web>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <etwTracking profileName="Sample Tracking Profile"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
   <tracking>  
      <profiles>  
        <trackingProfile name="Sample Tracking Profile">  
        ….  
       </trackingProfile>  
      </profiles>  
    </tracking>  
  </system.serviceModel>  
</configuration>  
```  
  
> [!NOTE]
> `trackingProfile` 또는 `<etwTracking/>`와 같이 `<etwTracking profileName=""/>` 이름을 지정하지 않으면 Machine.config 파일에서 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]과 함께 설치된 기본 추적 프로필이 사용됩니다.  
  
 Machine.config 파일에서 기본 추적 프로필은 워크플로 인스턴스 레코드와 오류를 구독합니다.  
  
 ETW에서는 공급자 ID를 통해 ETW 세션에 이벤트가 기록됩니다. ETW 추적 참가자가 ETW에 추적 레코드를 기록하는 데 사용하는 공급자 ID는 Web.config 파일의 `<system.serviceModel><diagnostics>` 아래에 있는 진단 섹션에서 정의됩니다. 다음 예제와 같이 기본적으로 ETW 추적 참가자는 공급자 ID가 지정되지 않은 경우 기본 공급자 ID를 사용합니다.  
  
```xml  
<system.serviceModel>  
        <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />  
```  
  
 다음 그림에서는 ETW 추적 참가자를 통한 추적 데이터 흐름을 보여 줍니다. 추적 데이터가 ETW 세션에 도달하면 다양한 방법으로 이 데이터에 액세스할 수 있습니다. 이러한 이벤트에 액세스하는 가장 유용한 방법 중 하나는 애플리케이션과 서비스에서 로그와 추적을 보는 데 사용되는 일반적인 Windows 도구인 이벤트 뷰어를 사용하는 것입니다.  
  
 ![ETW 추적 공급자를 통한 추적 데이터의 흐름입니다.](./media/tracking-participants/tracking-data-event-tracing-windows-provider.gif)  
  
## <a name="tracking-participant-event-data"></a>추적 참가자 이벤트 데이터  
 추적 참가자는 추적 레코드당 이벤트 하나의 형식으로 추적된 이벤트 데이터를 ETW 세션에 serialize합니다.  100 ~ 199 범위 내의 ID를 사용하여 이벤트를 식별합니다. 추적 참가자가 내보내는 추적 이벤트 레코드의 정의는 [추적 이벤트 참조](tracking-events-reference.md) 항목을 참조 하세요.  
  
 ETW 이벤트 크기는 ETW 버퍼 크기 또는 ETW 이벤트의 최대 페이로드 중 작은 값에 따라 제한됩니다. 이벤트 크기가 이 ETW 제한 중 하나를 초과하면 임의의 방식으로 이벤트가 잘리고 이벤트 내용이 제거됩니다. 변수, 인수, 주석 및 사용자 지정 데이터는 선택적으로 제거되지 않습니다. 잘리는 경우 어떤 값 때문에 이벤트 크기가 ETW 제한을 초과하는지와 상관없이 이 모든 항목이 잘립니다.  제거된 데이터는 `<item>..<item>`으로 대체됩니다.  
  
 변수, 인수 및 사용자 지정 데이터 항목의 복합 형식은 [NetDataContractSerializer 클래스](https://go.microsoft.com/fwlink/?LinkId=177537)를 사용 하 여 ETW 이벤트 레코드로 serialize 됩니다. 이 클래스는 serialize된 XML 스트림에 CLR 형식 정보를 포함합니다.  
  
 ETW 제한으로 인해 페이로드 데이터가 잘리면 중복 추적 레코드가 ETW 세션에 전송될 수 있습니다. 하나 이상의 세션이 이벤트를 수신하고 세션마다 다른 이벤트 페이로드 제한이 있는 경우 이 문제가 발생할 수 있습니다.  
  
 더 낮은 제한이 있는 세션의 경우 이벤트가 잘릴 수 있습니다. ETW 추적 참가자는 이벤트를 수신하는 세션 수를 알 수 없습니다. 세션에서 이벤트가 잘리면 ETW 참가자는 이벤트를 다시 한 번 보내려고 시도합니다. 이 경우 큰 페이로드 크기를 허용하도록 구성된 세션은 이벤트를 두 번 받습니다(잘리지 않은 이벤트 및 잘린 이벤트). 동일한 버퍼 크기 제한으로 모든 ETW 세션을 구성하면 중복을 방지할 수 있습니다.  
  
## <a name="accessing-tracking-data-from-an-etw-participant-in-the-event-viewer"></a>이벤트 뷰어에서 ETW 참가자의 추적 데이터 액세스  
 ETW 추적 참가자가 ETW 세션에 기록한 이벤트는 이벤트 뷰어를 통해 액세스할 수 있습니다(기본 공급자 ID를 사용할 경우). 따라서 워크플로에서 내보낸 추적 레코드를 신속하게 볼 수 있습니다.  
  
> [!NOTE]
> ETW 세션으로 내보낸 추적 레코드 이벤트는 100 ~ 199 범위의 이벤트 ID를 사용합니다.  
  
#### <a name="to-enable-viewing-the-tracking-records-in-event-viewer"></a>이벤트 뷰어에서 추적 레코드 보기를 사용하려면  
  
1. 이벤트 뷰어(EVENTVWR.EXE)를 시작합니다.  
  
2. **이벤트 뷰어, 응용 프로그램 및 서비스 로그, Microsoft, Windows, 응용 프로그램 서버-응용**프로그램을 선택 합니다.  
  
3. 마우스 오른쪽 단추를 클릭 하 고 **보기, 분석 및 디버그 로그 표시** 가 선택 되어 있는지 확인 합니다. 그렇지 않으면 옆에 체크 표시가 나타나도록 이 항목을 선택합니다. **분석**, **성능**및 **디버그** 로그가 표시 됩니다.  
  
4. **분석** 로그를 마우스 오른쪽 단추로 클릭 한 다음 **로그 사용**을 선택 합니다. 로그는 %SystemRoot%\System32\Winevt\Logs\Microsoft-Windows-Application Server-Applications%4Analytic.etl 파일에 있습니다.  
  
## <a name="custom-tracking-participant"></a>사용자 지정 추적 참가자  
 추적 참가자 API를 사용하면 워크플로 런타임에서 내보낸 추적 레코드를 처리하기 위한 사용자 지정 논리를 포함할 수 있는 사용자 제공 추적 참가자를 사용하여 추적 런타임을 확장할 수 있습니다. 사용자 지정 추적 참가자를 기록하려면 개발자가 `Track` 클래스에서 <xref:System.Activities.Tracking.TrackingParticipant> 메서드를 구현해야 합니다. 이 메서드는 워크플로 런타임에서 추적 레코드를 내보낼 때 호출됩니다.  
  
 추적 참가자는 <xref:System.Activities.Tracking.TrackingParticipant> 클래스에서 파생됩니다. 시스템 제공 <xref:System.Activities.Tracking.EtwTrackingParticipant>는 받은 각 추적 레코드에 대해 ETW(Windows용 이벤트 추적) 이벤트를 내보냅니다. 사용자 지정 추적 참가자를 만들려면 <xref:System.Activities.Tracking.TrackingParticipant>에서 파생되는 클래스를 만듭니다. 기본 추적 기능을 제공하려면 <xref:System.Activities.Tracking.TrackingParticipant.Track%2A>을 재정의합니다. <xref:System.Activities.Tracking.TrackingParticipant.Track%2A>은 런타임에서 추적 레코드를 보낼 때 호출되며 원하는 방법으로 처리할 수 있습니다. 다음 예제에서는 모든 추적 레코드를 콘솔 창으로 내보내는 사용자 지정 추적 참가자 클래스를 정의합니다. <xref:System.Activities.Tracking.TrackingParticipant> 및 `BeginTrack` 메서드를 사용하여 비동기식으로 추적 레코드를 처리하는 `EndTrack` 개체를 구현할 수도 있습니다.  
  
```csharp  
class ConsoleTrackingParticipant : TrackingParticipant  
{  
    protected override void Track(TrackingRecord record, TimeSpan timeout)  
    {  
        if (record != null)  
        {  
            Console.WriteLine("=================================");  
            Console.WriteLine(record);  
        }  
    }  
}  
```  
  
 특정 추적 참가자를 사용하려면 다음 예제와 같이 추적할 워크플로 인스턴스에 해당 참가자를 등록합니다.  
  
```csharp  
myInstance.Extensions.Add(new ConsoleTrackingParticipant());  
```  
  
 다음 예제에서는 <xref:System.Activities.Statements.Sequence> 활동을 포함하는 <xref:System.Activities.Statements.WriteLine> 활동으로 구성된 워크플로를 만듭니다. `ConsoleTrackingParticipant`를 확장에 추가하고 워크플로를 호출합니다.  
  
```csharp  
Activity activity= new Sequence()  
{  
    Activities =  
    {  
        new WriteLine()  
        {  
            Text = "Hello World."  
        }  
    }  
};  
  
WorkflowApplication instance = new WorkflowApplication(activity);  
  
instance.Extensions.Add(new ConsoleTrackingParticipant());  
  instance.Completed = delegate(WorkflowApplicationCompletedEventArgs e)  
            {  
                Console.WriteLine("workflow instance completed, Id = " + instance.Id);  
                resetEvent.Set();  
            };  
            instance.Run();  
            Console.ReadLine();  
```  
  
## <a name="see-also"></a>참고자료

- [Windows Server App Fabric 모니터링](https://go.microsoft.com/fwlink/?LinkId=201273)
- [App Fabric을 사용 하 여 응용 프로그램 모니터링](https://go.microsoft.com/fwlink/?LinkId=201275)
