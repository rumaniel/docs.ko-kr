---
title: 워크플로 추적 구성
ms.date: 03/30/2017
ms.assetid: 905adcc9-30a0-4918-acd6-563f86db988a
ms.openlocfilehash: 889efc804bb45b384dfde5b4deb520a81d1e5486
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353059"
---
# <a name="configuring-tracking-for-a-workflow"></a>워크플로 추적 구성

워크플로는 다음과 같은 세 가지 방식으로 실행할 수 있습니다.

- 다음에서 호스트됨 <xref:System.ServiceModel.Activities.WorkflowServiceHost>

- <xref:System.Activities.WorkflowApplication>으로 실행

- <xref:System.Activities.WorkflowInvoker>를 사용하여 직접 실행

워크플로 호스팅 옵션에 따라 코드 또는 구성 파일을 통해 추적 참가자를 추가할 수 있습니다. 이 항목에서는 <xref:System.Activities.WorkflowApplication> 및 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에 추적 참가자를 추가하여 추적을 구성하는 방법과 <xref:System.Activities.WorkflowInvoker>를 사용할 때 추적을 활성화하는 방법에 대해 설명합니다.

## <a name="configuring-workflow-application-tracking"></a>워크플로 애플리케이션 추적 구성

<xref:System.Activities.WorkflowApplication> 클래스를 사용하여 워크플로를 실행할 수 있습니다. 이 항목에서는 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 워크플로 호스트에 추적 참가자를 추가하여 <xref:System.Activities.WorkflowApplication> 워크플로 애플리케이션에 대해 추적을 구성하는 방법을 보여 줍니다. 이 경우 워크플로는 워크플로 애플리케이션으로 실행됩니다. 구성 파일을 사용하는 대신 코드를 통해 워크플로 애플리케이션을 구성하면 이 워크플로 애플리케이션은 <xref:System.Activities.WorkflowApplication> 클래스를 사용하는 자체 호스팅 .exe 파일이 됩니다. 추적 참가자는 <xref:System.Activities.WorkflowApplication> 인스턴스에 확장으로 추가됩니다. 이 작업은 WorkflowApplication 인스턴스에 대한 확장 컬렉션에 <xref:System.Activities.Tracking.TrackingParticipant>를 추가하여 수행됩니다.

워크플로 애플리케이션의 경우 다음 코드와 같이 <xref:System.Activities.Tracking.EtwTrackingParticipant> 동작 확장을 추가할 수 있습니다.

```csharp
LogActivity activity = new LogActivity();

WorkflowApplication instance = new WorkflowApplication(activity);
EtwTrackingParticipant trackingParticipant =
    new EtwTrackingParticipant
{

        TrackingProfile = new TrackingProfile
           {
               Name = "SampleTrackingProfile",
               ActivityDefinitionId = "ProcessOrder",
               Queries = new WorkflowInstanceQuery
               {
                  States = { "*" }
              }
          }
       };
instance.Extensions.Add(trackingParticipant);
```

### <a name="configuring-workflow-service-tracking"></a>워크플로 서비스 추적 구성

@No__t-0 서비스 호스트에서 호스팅될 때 워크플로를 WCF 서비스로 노출할 수 있습니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost>는 워크플로 기반 서비스에 대한 특수 .NET ServiceHost 구현입니다. 이 단원에서는 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]에서 실행되는 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 워크플로 서비스에 대해 추적을 구성하는 방법에 대해 설명합니다. 이러한 추적 기능은 Web.config 파일(웹 호스팅 서비스의 경우) 또는 App.config 파일(콘솔 애플리케이션과 같은 독립 실행형 애플리케이션에서 호스트되는 서비스의 경우)을 통해 서비스 동작을 지정하거나, 코드를 통해 서비스 호스트에 대한 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 컬렉션에 추적별 동작을 추가하여 구성됩니다.

@No__t-0에서 호스트 되는 워크플로 서비스의 경우 다음 예제와 같이 구성 파일에서 < `behavior` > 요소를 사용 하 여 <xref:System.Activities.Tracking.EtwTrackingParticipant>을 추가할 수 있습니다.

```xml
<behaviors>
   <serviceBehaviors>
        <behavior>
          <etwTracking profileName="Sample Tracking Profile" />
        </behavior>
   </serviceBehaviors>
<behaviors>
```

또는 <xref:System.ServiceModel.WorkflowServiceHost>에서 호스트되는 워크플로 서비스의 경우 코드를 통해 <xref:System.Activities.Tracking.EtwTrackingParticipant> 동작 확장을 추가할 수 있습니다. 사용자 지정 추적 참가자를 추가하려면 다음 예제 코드와 같이 새 동작 확장을 만들어 <xref:System.ServiceModel.ServiceHost>에 추가합니다.

> [!NOTE]
> 사용자 지정 추적 참가자를 추가 하는 사용자 지정 동작 요소를 만드는 방법을 보여 주는 샘플 코드를 보려면 [추적](./samples/tracking.md) 샘플을 참조 하세요.

```csharp
ServiceHost svcHost = new ServiceHost(typeof(WorkflowService), new
                                 Uri("http://localhost:8001/Sample"));
EtwTrackingBehavior trackingBehavior =
    new EtwTrackingBehavior
    {
        ProfileName = "Sample Tracking Profile"
    };
svcHost.Description.Behaviors.Add(trackingBehavior);
svcHost.Open();
```

추적 참가자는 동작에 대한 확장으로 워크플로 서비스 호스트에 추가됩니다.

다음 샘플 코드에서는 구성 파일에서 추적 프로필을 읽는 방법을 보여 줍니다.

```csharp
TrackingProfile GetProfile(string profileName, string displayName)
        {
            TrackingProfile trackingProfile = null;
            TrackingSection trackingSection = (TrackingSection)WebConfigurationManager.GetSection("system.serviceModel/tracking");
            if (trackingSection == null)
            {
                return null;
            }

            profileName ??= "";

            //Find the profile with the specified profile name in the list of profile found in config
            var match = from p in new List<TrackingProfile>(trackingSection.TrackingProfiles)
                        where (p.Name == profileName) && ((p.ActivityDefinitionId == displayName) || (p.ActivityDefinitionId == "*"))
                        select p;

            if (match.Count() == 0)
            {
                //return an empty profile
                trackingProfile = new TrackingProfile()
                {
                    ActivityDefinitionId = displayName
                };

            }
            else
            {
                trackingProfile = match.First();
            }

            return trackingProfile;
```

이 샘플 코드에서는 워크플로 호스트에 추적 프로필을 추가하는 방법을 보여 줍니다.

```csharp
WorkflowServiceHost workflowServiceHost = serviceHostBase as WorkflowServiceHost;
if (null != workflowServiceHost)
{
    string workflowDisplayName = workflowServiceHost.Activity.DisplayName;
    TrackingProfile trackingProfile = GetProfile(this.profileName, workflowDisplayName);
    workflowServiceHost.WorkflowExtensions.Add(()  => new EtwTrackingParticipant {
        TrackingProfile = trackingProfile
    });
 }
```

> [!NOTE]
> 추적 프로필에 대 한 자세한 내용은 [추적 프로필](https://go.microsoft.com/fwlink/?LinkId=201310)을 참조 하세요.

### <a name="configuring-tracking-using-workflowinvoker"></a>WorkflowInvoker를 사용하여 추적 구성

<xref:System.Activities.WorkflowInvoker>를 사용하여 실행되는 워크플로에 대한 추적을 구성하려면 추적 공급자를 <xref:System.Activities.WorkflowInvoker> 인스턴스에 대한 확장으로 추가합니다. 다음 코드 예제는 [사용자 지정 추적](./samples/custom-tracking.md) 샘플에서 가져온 것입니다.

```csharp
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());
invoker.Extensions.Add(customTrackingParticipant);
invoker.Invoke();
```

### <a name="viewing-tracking-records-in-event-viewer"></a>이벤트 뷰어에서 추적 레코드 보기

WF 실행을 추적할 때 특별히 관심을 두고 확인할 이벤트 뷰어 로그 두 가지는 분석 로그와 디버그 로그입니다. 둘 다 Microsoft&#124;Windows&#124;응용 프로그램 서버-응용 프로그램 노드 아래에 있습니다. 이 섹션의 로그에는 전체 시스템에 영향을 미치는 이벤트가 아닌 단일 애플리케이션의 이벤트가 있습니다.

디버그 추적 이벤트는 디버그 로그에 기록됩니다. 이벤트 뷰어에서 WF 디버그 추적 이벤트를 수집하려면 디버그 로그를 사용합니다.

1. 이벤트 뷰어를 열려면 **시작**을 클릭 한 다음 실행을 클릭 **합니다.** 실행 대화 상자에서 `eventvwr`을 입력 합니다.

2. 이벤트 뷰어 대화 상자에서 **응용 프로그램 및 서비스 로그** 노드를 확장 합니다.

3. **Microsoft**, **Windows**및 **응용 프로그램 서버-응용** 프로그램 노드를 확장 합니다.

4. **응용 프로그램 서버-응용 프로그램** 노드 아래의 **디버그** 노드를 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다.

5. 추적이 설정된 애플리케이션을 실행하여 추적 이벤트를 생성합니다.

6. **디버그** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새로 고침을 선택 합니다.** 가운데 창에 추적 이벤트가 표시됩니다.

WF 4는 추적 레코드를 ETW(Windows용 이벤트 추적) 세션에 기록하는 추적 참가자를 제공합니다. ETW 추적 참가자는 추적 레코드를 구독하도록 추적 프로필을 사용하여 구성됩니다. 추적을 사용하도록 하면 오류 추적 레코드를 ETW로 내보냅니다. ETW 추적 참가자가 보낸 추적 이벤트에 해당하는 ETW 추적 이벤트(100-113)는 분석 로그에 기록됩니다.

추적 레코드를 보려면 아래 단계를 따릅니다.

1. 이벤트 뷰어를 열려면 **시작**을 클릭 한 다음 실행을 클릭 **합니다.** 실행 대화 상자에서 `eventvwr`을 입력 합니다.

2. 이벤트 뷰어 대화 상자에서 **응용 프로그램 및 서비스 로그** 노드를 확장 합니다.

3. **Microsoft**, **Windows**및 **응용 프로그램 서버-응용** 프로그램 노드를 확장 합니다.

4. **응용 프로그램 서버-응용 프로그램** 노드 아래의 **분석** 노드를 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다.

5. 추적이 설정된 애플리케이션을 실행하여 추적 레코드를 생성합니다.

6. **분석** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새로 고침을 선택 합니다.** 가운데 창에 추적 레코드가 표시됩니다.

다음 이미지는 이벤트 뷰어의 추적 이벤트를 보여 줍니다.

![추적 레코드를 보여 주는 이벤트 뷰어의 스크린샷](./media/configuring-tracking-for-a-workflow/tracking-event-viewer.png)

### <a name="registering-an-application-specific-provider-id"></a>애플리케이션별 공급자 ID 등록

이벤트를 특정 애플리케이션 로그에 기록해야 하는 경우 아래 단계에 따라 새 공급자 매니페스트를 등록합니다.

1. 애플리케이션 구성 파일에 공급자 ID를 선언합니다.

    ```xml
    <system.serviceModel>
        <diagnostics etwProviderId="2720e974-9fe9-477a-bb60-81fe3bf91eec"/>
    </system.serviceModel>
    ```

2. %Windir%\Microsoft.NET\Framework @ no__t-0 @ no__t의 최신 버전 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] > \Microsoft.Windows.ApplicationServer.Applications.man의 매니페스트 파일을 임시 위치로 복사 하 고 이름을로 바꿉니다. Applications_Provider1. man.

3. 매니페스트 파일의 GUID를 새 GUID로 변경합니다.

    ```xml
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}"
    ```

4. 기본 공급자를 제거하지 않으려는 경우에는 공급자 이름을 변경합니다.

    ```xml
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}"
    ```

5. 이전 단계에서 공급자 이름을 변경한 경우 매니페스트 파일의 채널 이름을 새 공급자 이름으로 변경합니다.

    ```xml
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Admin" chid="ADMIN_CHANNEL" symbol="ADMIN_CHANNEL" type="Admin" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ADMIN_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Operational" chid="OPERATIONAL_CHANNEL" symbol="OPERATIONAL_CHANNEL" type="Operational" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.OPERATIONAL_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Debug" chid="DEBUG_CHANNEL" symbol="DEBUG_CHANNEL" type="Debug" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.DEBUG_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Perf" chid="PERF_CHANNEL" symbol="PERF_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.PERF_CHANNEL.message)" />
    ```

6. 다음 단계에 따라 리소스 DLL을 생성합니다.

    1. Windows SDK를 설치합니다. Windows SDK에는 메시지 컴파일러 ([mc](https://go.microsoft.com/fwlink/?LinkId=184606))와 리소스 컴파일러 ([rc](https://go.microsoft.com/fwlink/?LinkId=184605))가 포함 됩니다.

    2. Windows SDK 명령 프롬프트에서 새 매니페스트 파일에 대해 mc.exe를 실행합니다.

        ```console
        mc.exe Microsoft.Windows.ApplicationServer.Applications_Provider1.man
        ```

    3. 이전 단계에서 생성된 리소스 파일에 대해 rc.exe를 실행합니다.

        ```console
        rc.exe  Microsoft.Windows.ApplicationServer.Applications_Provider1.rc
        ```

    4. NewProviderReg.cs라는 빈 cs 파일을 만듭니다.

    5. C# 컴파일러를 사용하여 리소스 DLL을 만듭니다.

        ```console
        csc /target:library /win32res:Microsoft.Windows.ApplicationServer.Applications_Provider1.res NewProviderReg.cs /out:Microsoft.Windows.ApplicationServer.Applications_Provider1.dll
        ```

    6. 매니페스트 파일의 리소스 및 메시지 dll 이름을 `Microsoft.Windows.ApplicationServer.Applications.Provider1.man`에서 새 dll 이름으로 변경 합니다.

        ```xml
        <provider name="Microsoft-Windows-Application Server-Applications_Provider1" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" symbol="Microsoft_Windows_ApplicationServer_ApplicationEvents" resourceFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" messageFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll">
        ```

    7. [Wevtutil](https://go.microsoft.com/fwlink/?LinkId=184608) 을 사용 하 여 매니페스트를 등록 합니다.

        ```console
        wevtutil im Microsoft.Windows.ApplicationServer.Applications_Provider1.man
        ```

## <a name="see-also"></a>참조

- [Windows Server App Fabric 모니터링](https://go.microsoft.com/fwlink/?LinkId=201273)
- [App Fabric을 사용 하 여 응용 프로그램 모니터링](https://go.microsoft.com/fwlink/?LinkId=201275)
