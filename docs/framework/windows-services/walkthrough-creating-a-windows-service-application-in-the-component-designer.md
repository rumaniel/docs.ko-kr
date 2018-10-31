---
title: Visual Studio에서 Windows 서비스 응용 프로그램 만들기
ms.date: 09/10/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows service applications, walkthroughs
- Windows service applications, creating
ms.assetid: e24d8a3d-edc6-485c-b6e0-5672d91fb607
author: ghogen
ms.openlocfilehash: 79447ede354de104607117f657182023a2e57127
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49123672"
---
# <a name="walkthrough-create-a-windows-service-app"></a>연습: Windows 서비스 앱 만들기

이 문서에서는 이벤트 로그에 메시지를 쓰는 간단한 Windows 서비스 앱을 Visual Studio에서 만드는 방법을 보여 줍니다.

## <a name="create-a-service"></a>서비스 만들기

우선 프로젝트를 만들고 서비스가 제대로 작동하는 데 필요한 값을 설정합니다.

1. Visual Studio의 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택하거나 **Ctrl**+**Shift**+**N**을 눌러 **새 프로젝트** 대화 상자를 엽니다.

2. **Windows 서비스** 프로젝트 템플릿을 탐색하여 선택합니다. **설치됨** > [**Visual C#** 또는 **Visual Basic**] > **Windows 데스크톱**을 확장하거나 오른쪽 위의 검색 상자에 **Windows 서비스**를 입력합니다.

   ![Visual Studio의 새 프로젝트 대화 상자에 있는 Windows 서비스 템플릿](media/new-project-dialog.png)

   > [!NOTE]
   > **Windows 서비스** 템플릿이 표시되지 않는 경우 **.NET 데스크톱 개발** 워크로드를 설치해야 할 수 있습니다. **새 프로젝트** 대화 상자에서 왼쪽 아래에 있는 **Visual Studio 설치 관리자 열기** 링크를 클릭합니다. **Visual Studio 설치 관리자**에서 **.NET 데스크톱 개발** 워크로드를 선택한 다음, **수정**을 선택합니다.

3. 프로젝트 이름을 **MyNewService**로 지정하고 **확인**을 선택합니다.

   프로젝트 템플릿은 <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType>에서 상속된 `Service1`이라는 구성 요소 클래스를 포함합니다. 여기에는 서비스를 시작하는 코드 등의 많은 기본 서비스 코드가 포함됩니다.

## <a name="rename-the-service"></a>서비스 이름 바꾸기

서비스 이름을 **Service1**에서 **MyNewService**로 바꿉니다.

1. Service1.cs(또는 Service1.vb)의 **디자인** 보기에서 **코드 보기로 전환** 링크를 클릭합니다. **Service1**을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **이름 바꾸기**를 선택합니다. **MyNewService**를 입력하고 **Enter** 키를 누르거나 **적용**을 클릭합니다.

2. **Service1.cs [디자인]** 또는 **Service1.vb [디자인]** 의 **속성** 창에서 **ServiceName** 값을 **MyNewService**로 변경합니다.

3. **솔루션 탐색기**에서 **Service1.cs**의 이름을 **MyNewService.cs**로 바꾸거나 **Service1.vb**의 이름을 **MyNewService.vb**로 바꿉니다.

## <a name="add-features-to-the-service"></a>서비스에 기능 추가

다음 섹션에서는 Windows 서비스에 사용자 지정 이벤트 로그를 추가합니다. 이벤트 로그는 Windows 서비스와 연관이 없으며, 여기에서는 단지 Windows 서비스에 추가할 수 있는 구성 요소 종류의 한 예로 <xref:System.Diagnostics.EventLog> 구성 요소를 사용합니다.

### <a name="add-custom-event-log-functionality"></a>사용자 지정 이벤트 로그 기능 추가

1. **솔루션 탐색기**에서 **MyNewService.cs** 또는 **MyNewService.vb**의 상황에 맞는 메뉴를 열고 **뷰 디자이너**를 선택합니다.

2. **도구 상자** 의 **구성 요소**섹션에서 <xref:System.Diagnostics.EventLog> 구성 요소를 디자이너로 끌어 옵니다.

3. **솔루션 탐색기**에서 **MyNewService.cs** 또는 **MyNewService.vb**의 상황에 맞는 메뉴를 열고 **코드 보기**를 선택합니다.

4. 사용자 지정 이벤트 로그를 정의하는 생성자를 편집합니다.

   ```csharp
   public MyNewService()
   {
        InitializeComponent();

        eventLog1 = new System.Diagnostics.EventLog();
        if (!System.Diagnostics.EventLog.SourceExists("MySource"))
        {
            System.Diagnostics.EventLog.CreateEventSource(
                "MySource", "MyNewLog");
        }
        eventLog1.Source = "MySource";
        eventLog1.Log = "MyNewLog";
    }
   ```

   [!code-vb[VbRadconService#2](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#2)]

### <a name="define-what-occurs-when-the-service-starts"></a>서비스가 시작될 때 수행되는 동작 정의

코드 편집기에서 프로젝트를 만들 때 자동으로 재정의된 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드를 찾습니다. 서비스가 시작될 때 이벤트 로그에 항목을 기록하는 코드 줄을 추가합니다.

[!code-csharp[VbRadconService#3](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#3)]
[!code-vb[VbRadconService#3](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#3)]

서비스 응용 프로그램은 오랫동안 실행되도록 설계되므로 대개 시스템의 특정 항목을 폴링하거나 모니터링합니다. 모니터링은 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드에서 설정됩니다. 그러나 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 가 실제로 모니터링을 수행하지는 않습니다. 서비스의 작업이 시작되고 나면 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드가 운영 체제에 반환되어야 하며 무제한 순환하거나 방해가 되어서는 안 됩니다. 간단한 폴링 메커니즘을 설정하려면 <xref:System.Timers.Timer?displayProperty=nameWithType> 구성 요소를 사용할 수 있습니다. 즉, <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드에서 구성 요소에 대한 매개 변수를 설정한 다음 <xref:System.Timers.Timer.Enabled%2A> 속성을 `true`로 설정합니다. 타이머는 코드에서 주기적으로 이벤트를 발생시키며 그러는 동안에도 서비스에서는 모니터링을 수행할 수 있습니다. 이렇게 하려면 다음 코드를 사용할 수 있습니다.

```csharp
// Set up a timer that triggers every minute.
System.Timers.Timer timer = new System.Timers.Timer();
timer.Interval = 60000; // 60 seconds
timer.Elapsed += new System.Timers.ElapsedEventHandler(this.OnTimer);
timer.Start();
```

```vb
' Set up a timer that triggers every minute.
Dim timer As System.Timers.Timer = New System.Timers.Timer()
timer.Interval = 60000 ' 60 seconds
AddHandler timer.Elapsed, AddressOf Me.OnTimer
timer.Start()
```

멤버 변수를 클래스에 추가합니다. 여기에는 이벤트 로그에 기록할 다음 이벤트의 식별자가 포함됩니다.

```csharp
private int eventId = 1;
```

```vb
Private eventId As Integer = 1
```

타이머 이벤트를 처리하는 새 메서드를 추가합니다.

```csharp
public void OnTimer(object sender, System.Timers.ElapsedEventArgs args)
{
    // TODO: Insert monitoring activities here.
    eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId++);
}
```

```vb
Private Sub OnTimer(sender As Object, e As Timers.ElapsedEventArgs)
    ' TODO: Insert monitoring activities here.
    eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId)
    eventId = eventId + 1
End Sub
```

주 스레드에서 모든 작업을 실행하는 대신 백그라운드 작업자 스레드를 사용하여 작업을 수행할 수도 있습니다. 자세한 내용은 <xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>을 참조하세요.

### <a name="define-what-occurs-when-the-service-is-stopped"></a>서비스가 중지될 때 수행되는 동작 정의

서비스가 중지될 때 이벤트 로그에 항목을 추가하는 코드 줄을 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드에 추가합니다.

```csharp
eventLog1.WriteEntry("In OnStop.");
```

[!code-vb[VbRadconService#4](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#4)]

### <a name="define-other-actions-for-the-service"></a>서비스의 다른 동작 정의

<xref:System.ServiceProcess.ServiceBase.OnPause%2A>, <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> 메서드를 재정의하여 구성 요소에 대한 처리 작업을 추가로 정의할 수 있습니다. 다음 코드에서는 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 메서드를 재정의하는 방법을 보여 줍니다.

[!code-csharp[VbRadconService#5](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#5)]
[!code-vb[VbRadconService#5](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#5)]

<xref:System.Configuration.Install.Installer> 클래스를 통해 Windows 서비스를 설치할 때는 일부 사용자 지정 작업을 수행해야 합니다. Visual Studio에서 특별히 Windows 서비스를 위해 이러한 설치 관리자를 만들어 프로젝트에 추가할 수 있습니다.

## <a name="set-service-status"></a>서비스 상태 설정

서비스는 서비스 제어 관리자에 상태를 보고합니다. 따라서 사용자는 서비스가 정상적으로 작동 중인지를 확인할 수 있습니다. 기본적으로 <xref:System.ServiceProcess.ServiceBase> 에서 상속되는 서비스는 중지됨, 일시 중지됨, 실행 중 등의 제한적인 상태 설정 집합을 보고합니다. 서비스를 시작하는 데 시간이 다소 걸리는 경우에는 시작 보류 중 상태를 보고하면 도움이 될 수 있습니다. 또한 Windows [SetServiceStatus 함수](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus)를 호출하는 코드를 추가하여 시작 보류 중 및 중지 보류 중 상태 설정을 구현할 수도 있습니다.

서비스 보류 중 상태를 구현하려면

1. MyNewService.cs 또는 MyNewService.vb 파일에 <xref:System.Runtime.InteropServices?displayProperty=nameWithType> 네임스페이스에 대한 `using` 문 또는 `Imports` 선언을 추가합니다.

    ```csharp
    using System.Runtime.InteropServices;
    ```

    ```vb
    Imports System.Runtime.InteropServices
    ```

2. `ServiceState` 값을 선언하고 상태에 대한 구조(플랫폼 호출에서 사용함)를 추가하려면 MyNewService.cs에 다음 코드를 추가합니다.

    ```csharp
    public enum ServiceState
    {
        SERVICE_STOPPED = 0x00000001,
        SERVICE_START_PENDING = 0x00000002,
        SERVICE_STOP_PENDING = 0x00000003,
        SERVICE_RUNNING = 0x00000004,
        SERVICE_CONTINUE_PENDING = 0x00000005,
        SERVICE_PAUSE_PENDING = 0x00000006,
        SERVICE_PAUSED = 0x00000007,
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct ServiceStatus
    {
        public int dwServiceType;
        public ServiceState dwCurrentState;
        public int dwControlsAccepted;
        public int dwWin32ExitCode;
        public int dwServiceSpecificExitCode;
        public int dwCheckPoint;
        public int dwWaitHint;
    };
    ```

    ```vb
    Public Enum ServiceState
        SERVICE_STOPPED = 1
        SERVICE_START_PENDING = 2
        SERVICE_STOP_PENDING = 3
        SERVICE_RUNNING = 4
        SERVICE_CONTINUE_PENDING = 5
        SERVICE_PAUSE_PENDING = 6
        SERVICE_PAUSED = 7
    End Enum

    <StructLayout(LayoutKind.Sequential)>
    Public Structure ServiceStatus
        Public dwServiceType As Long
        Public dwCurrentState As ServiceState
        Public dwControlsAccepted As Long
        Public dwWin32ExitCode As Long
        Public dwServiceSpecificExitCode As Long
        Public dwCheckPoint As Long
        Public dwWaitHint As Long
    End Structure
    ```

3. 이제 `MyNewService` 클래스에서 [플랫폼 호출](../interop/consuming-unmanaged-dll-functions.md)을 사용하여 [SetServiceStatus 함수](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus)를 선언합니다.

    ```csharp
    [DllImport("advapi32.dll", SetLastError = true)]
    private static extern bool SetServiceStatus(System.IntPtr handle, ref ServiceStatus serviceStatus);
    ```

    ```vb
    Declare Auto Function SetServiceStatus Lib "advapi32.dll" (ByVal handle As IntPtr, ByRef serviceStatus As ServiceStatus) As Boolean
    ```

4. 시작 보류 중 상태를 구현하려면 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드 시작 부분에 다음 코드를 추가합니다.

    ```csharp
    // Update the service state to Start Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Start Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

5. 상태를 실행 중으로 설정하는 코드를 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드 끝에 추가합니다.

    ```csharp
    // Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

6. (선택 사항) <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드에 대해 이 절차를 반복합니다.

> [!NOTE]
> [서비스 제어 관리자](/windows/desktop/Services/service-control-manager)는 [SERVICE_STATUS 구조체](/windows/desktop/api/winsvc/ns-winsvc-_service_status)의 `dwWaitHint` 및 `dwCheckpoint` 멤버를 사용하여 Windows 서비스가 시작 또는 종료될 때까지 기다릴 시간을 결정합니다. <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드가 오랫동안 실행되는 경우 서비스는 증분된 `dwCheckPoint` 값을 포함하여 [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus)를 다시 호출하여 시간을 더 요청할 수 있습니다.

## <a name="add-installers-to-the-service"></a>서비스에 설치 관리자 추가

Windows 서비스를 실행하려면 해당 서비스를 설치해야 합니다. 그러면 서비스 제어 관리자에 서비스가 등록됩니다. 등록 정보를 처리하는 설치 관리자를 프로젝트에 추가할 수 있습니다.

1. **솔루션 탐색기**에서 **MyNewService.cs** 또는 **MyNewService.vb**의 상황에 맞는 메뉴를 열고 **뷰 디자이너**를 선택합니다.

2. 디자이너의 배경을 클릭하여 서비스 내용이 아닌 서비스 자체를 선택합니다.

3. 디자이너 창의 상황에 맞는 메뉴를 열고(포인팅 장치를 사용하는 경우 창 안쪽을 마우스 오른쪽 단추로 클릭) **설치 관리자 추가**를 선택합니다.

   기본적으로 설치 관리자가 두 개 들어 있는 구성 요소 클래스가 프로젝트에 추가됩니다. 구성 요소의 이름이 **ProjectInstaller**로 지정되며 구성 요소에는 서비스를 위한 설치 관리자와 서비스 관련 프로세스를 위한 설치 관리자가 들어 있습니다.

4. **ProjectInstaller** 의 **디자인**뷰에서 Visual C# 프로젝트의 경우 **serviceInstaller1** 를 선택하고 Visual Basic 프로젝트의 경우 **ServiceInstaller1** 을 선택합니다.

5. **속성** 창에서 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 속성이 **MyNewService**로 설정되어 있는지 확인합니다.

6. **설명** 속성을 "샘플 서비스"와 같은 텍스트로 설정합니다. 이 텍스트는 서비스 창에 표시되며 사용자가 서비스를 식별하고 서비스의 용도를 이해하는 데 도움이 됩니다.

7. <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> 속성을 서비스 창의 **이름** 열에 표시할 텍스트로 설정합니다. 예를 들어 "MyNewService 표시 이름"을 입력할 수 있습니다. 이 이름은 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 명령을 사용하여 서비스를 시작하는 등의 경우 시스템에서 사용하는 이름인 `net start` 속성과는 다릅니다.

8. <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 속성을 <xref:System.ServiceProcess.ServiceStartMode.Automatic>으로 설정합니다.

     ![Windows 서비스에 대한 설치 관리자 속성](../../../docs/framework/windows-services/media/windowsservice-installerproperties.PNG "WindowsService_InstallerProperties")

9. 디자이너에서 Visual C# 프로젝트의 경우 **serviceProcessInstaller1** 을 선택하고 Visual Basic 프로젝트의 경우 **ServiceProcessInstaller1** 을 선택합니다. <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 속성을 <xref:System.ServiceProcess.ServiceAccount.LocalSystem>으로 설정합니다. 이렇게 하면 로컬 시스템 계정을 사용하여 서비스가 설치되고 실행됩니다.

    > [!IMPORTANT]
    > <xref:System.ServiceProcess.ServiceAccount.LocalSystem> 계정에는 광범위한 권한이 있습니다. 예를 들어, 이 계정은 이벤트 로그에 쓸 수 있습니다. 이 계정을 사용할 때는 악성 소프트웨어의 공격을 받을 가능성이 커지므로 주의해야 합니다. 다른 작업에는 <xref:System.ServiceProcess.ServiceAccount.LocalService> 계정을 사용하는 것이 좋습니다. 이 계정은 로컬 컴퓨터에서 권한 없는 사용자의 역할을 하며 원격 서버에 익명 자격 증명을 제공합니다. <xref:System.ServiceProcess.ServiceAccount.LocalService> 계정을 사용하는 경우 이 예제는 실패합니다. 이벤트 로그에 대한 쓰기 권한이 필요하기 때문입니다.

설치 관리자에 대한 자세한 내용은 [방법: 서비스 응용 프로그램에 설치 관리자 추가](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)를 참조하세요.

## <a name="optional-set-startup-parameters"></a>(선택 사항) 시작 매개 변수 설정

다른 실행 파일과 마찬가지로 Windows 서비스에도 명령줄 인수나 시작 매개 변수를 사용할 수 있습니다. 프로세스 시작 매개 변수에 코드를 추가하면 사용자가 Windows 제어판의 서비스 창을 사용하여 고유한 사용자 지정 시작 매개 변수로 서비스를 시작할 수 있습니다. 그러나 이러한 시작 매개 변수는 다음 번에 서비스를 시작할 때 유지되지 않습니다. 시작 매개 변수를 영구적으로 설정하려는 경우 아래 절차에 나와 있는 것처럼 레지스트리에서 설정하면 됩니다.

> [!NOTE]
> 시작 매개 변수 추가를 결정하기 전에 시작 매개 변수가 서비스로 정보를 전달하는 가장 효율적인 방법인지를 고려합니다. 시작 매개 변수는 쉽게 사용하고 구문 분석할 수 있으며 사용자가 쉽게 재정의할 수 있지만 설명서가 없으면 사용자가 검색하고 사용하기가 어려울 수 있습니다. 일반적으로 서비스에 많은 시작 매개 변수가 필요한 경우에는 레지스트리나 구성 파일을 대신 사용하는 것이 좋습니다. 모든 Windows 서비스에는 레지스트리의 **HKLM\System\CurrentControlSet\services** 아래에 항목이 있습니다. 이 서비스의 키 아래에서 **매개 변수** 하위 키를 사용하여 서비스가 액세스할 수 있는 정보를 저장할 수 있습니다. Windows 서비스의 응용 프로그램 구성 파일은 다른 프로그램 형식에서와 같은 방식으로 사용할 수 있습니다. 예제 코드를 보려면 <xref:System.Configuration.ConfigurationManager.AppSettings%2A>를 참조하세요.

시작 매개 변수를 추가하려면

1. Program.cs 또는 MyNewService.Designer.vb의 `Main` 메서드에서 서비스 생성자에 전달할 입력 매개 변수를 추가합니다.

   ```csharp
   static void Main(string[] args)
   {
       ServiceBase[] ServicesToRun;
       ServicesToRun = new ServiceBase[]
       {
           new MyNewService(args)
       };
       ServiceBase.Run(ServicesToRun);
   }
   ```

   ```vb
   Shared Sub Main(ByVal cmdArgs() As String)
       Dim ServicesToRun() As System.ServiceProcess.ServiceBase = New System.ServiceProcess.ServiceBase() {New MyNewServiceVB(cmdArgs)}
       System.ServiceProcess.ServiceBase.Run(ServicesToRun)
   End Sub
   ```

2. `MyNewService` 생성자를 다음과 같이 변경합니다.

   ```csharp
   public MyNewService(string[] args)
   {
       InitializeComponent();

        string eventSourceName = "MySource";
        string logName = "MyNewLog";

        if (args.Length > 0)
        {
            eventSourceName = args[0];
        }

        if (args.Length > 1)
        {
            logName = args[1];
        }

        eventLog1 = new System.Diagnostics.EventLog();

        if (!System.Diagnostics.EventLog.SourceExists(eventSourceName))
        {
            System.Diagnostics.EventLog.CreateEventSource(eventSourceName, logName);
        }

        eventLog1.Source = eventSourceName;
        eventLog1.Log = logName;
   }
   ```

   ```vb
   Public Sub New(ByVal cmdArgs() As String)
       InitializeComponent()
       Dim eventSourceName As String = "MySource"
       Dim logName As String = "MyNewLog"
       If (cmdArgs.Count() > 0) Then
           eventSourceName = cmdArgs(0)
       End If
       If (cmdArgs.Count() > 1) Then
           logName = cmdArgs(1)
       End If
       eventLog1 = New System.Diagnostics.EventLog()
       If (Not System.Diagnostics.EventLog.SourceExists(eventSourceName)) Then
           System.Diagnostics.EventLog.CreateEventSource(eventSourceName, logName)
       End If
       eventLog1.Source = eventSourceName
       eventLog1.Log = logName
   End Sub
   ```

   이 코드는 제공된 시작 매개 변수에 따라 이벤트 소스 및 로그 이름을 설정하거나, 인수를 제공하지 않는 경우에는 기본값을 사용합니다.

3. 명령줄 인수를 지정하려면 ProjectInstaller.cs 또는 ProjectInstaller.vb의 `ProjectInstaller` 클래스에 다음 코드를 추가합니다.

   ```csharp
   protected override void OnBeforeInstall(IDictionary savedState)
   {
       string parameter = "MySource1\" \"MyLogFile1";
       Context.Parameters["assemblypath"] = "\"" + Context.Parameters["assemblypath"] + "\" \"" + parameter + "\"";
       base.OnBeforeInstall(savedState);
   }
   ```

   ```vb
   Protected Overrides Sub OnBeforeInstall(ByVal savedState As IDictionary)
       Dim parameter As String = "MySource1"" ""MyLogFile1"
       Context.Parameters("assemblypath") = """" + Context.Parameters("assemblypath") + """ """ + parameter + """"
       MyBase.OnBeforeInstall(savedState)
   End Sub
   ```

   이 코드는 기본 매개 변수 값을 추가하여 일반적으로 Windows 서비스 실행 파일의 전체 경로를 포함하는 **ImagePath** 레지스트리 키를 수정합니다. 경로와 개별 매개 변수는 따옴표로 묶어야 서비스가 올바르게 시작됩니다. 이 Windows 서비스의 시작 매개 변수를 변경하려는 경우 사용자는 **ImagePath** 레지스트리 키에 지정된 매개 변수를 변경할 수 있습니다. 그러나 해당 키를 프로그래밍 방식으로 변경하고 사용자에게 친숙한 방식(예: 관리 또는 구성 유틸리티)으로 기능을 노출하는 것이 좀 더 효율적입니다.

## <a name="build-the-service"></a>서비스 빌드

1. **솔루션 탐색기**에서 프로젝트의 상황에 맞는 메뉴를 열고 **속성**을 선택합니다.

   프로젝트의 속성 페이지가 나타납니다.

2. **응용 프로그램** 탭의 **시작 개체** 목록에서 **MyNewService.Program**을 선택합니다.

3. **솔루션 탐색기**에서 프로젝트의 상황에 맞는 메뉴를 열고 **빌드**를 선택하여 프로젝트를 빌드합니다(또는 **Ctrl**+**Shift**+**B**를 누름).

## <a name="install-the-service"></a>서비스 설치

이제 Windows 서비스를 빌드했으므로 이를 설치할 수 있습니다. Windows 서비스를 설치하려면 설치할 컴퓨터에서 관리자 자격 증명이 있어야 합니다.

1. 관리자 자격 증명을 사용하여 **Visual Studio에 대한 개발자 명령 프롬프트**를 엽니다. 마우스를 사용하는 경우 Windows 시작 메뉴에서 **VS 2017에 대한 개발자 명령 프롬프트**를 마우스 오른쪽 단추로 클릭하고 **기타** > **관리자 권한으로 실행**을 선택합니다.

2. **개발자 명령 프롬프트** 창에서 프로젝트의 출력이 포함된 폴더(기본적으로 프로젝트의 *\bin\Debug* 하위 디렉터리)로 이동합니다.

3. 다음 명령을 입력합니다.

    ```shell
    installutil.exe MyNewService.exe
    ```

    서비스를 성공적으로 설치한 경우 **installutil.exe**에서 설치에 성공했음을 보고합니다. 시스템에서 **InstallUtil.exe**를 찾을 수 없는 경우 해당 파일이 컴퓨터에 있는지 확인합니다. 이 도구는 *%windir%\Microsoft.NET\Framework[64]\\[프레임워크 버전]* 폴더에 .NET Framework와 함께 설치됩니다. 예를 들어 32비트 버전의 기본 경로는 *%windir%\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe*입니다.

    **Installutil.exe** 프로세스에서 실패를 보고하는 경우 설치 로그를 확인하여 이유를 찾아보세요. 기본적으로 로그는 서비스 실행 파일과 동일한 폴더에 있습니다. <xref:System.ComponentModel.RunInstallerAttribute> 클래스가 `ProjectInstaller` 클래스에 없거나, 해당 특성이 **true**로 설정되지 않았거나, `ProjectInstaller` 클래스가 **public**으로 표시되지 않은 경우 설치에 실패할 수 있습니다.

자세한 내용은 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)을 참조하세요.

## <a name="start-and-run-the-service"></a>서비스 시작 및 실행

1. Windows에서 **서비스** 데스크톱 앱을 엽니다. **Windows**+**R**을 눌러 **실행** 상자를 연 다음, **services.msc**를 입력하고 **Enter** 키를 누르거나 **확인**을 클릭합니다.

     해당 서비스가 설정된 표시 이름의 사전순으로 **서비스**에 표시됩니다.

     ![서비스 창의 MyNewService입니다.](../../../docs/framework/windows-services/media/windowsservices-serviceswindow.PNG)

2. **서비스**에서 서비스의 바로 가기 메뉴를 열고 **시작**을 선택합니다.

3. 서비스를 중지하려면 서비스의 바로 가기 메뉴를 열고 **중지**를 선택합니다.

4. (선택 사항) 명령줄에서 `net start ServiceName` 및 `net stop ServiceName` 명령을 사용하여 서비스를 시작하고 중지할 수 있습니다.

### <a name="verify-the-event-log-output-of-your-service"></a>서비스의 이벤트 로그 출력 확인

1. Windows 작업 표시줄의 검색 상자에 **이벤트 뷰어** 입력을 시작하고 검색 결과에서 **이벤트 뷰어**를 선택하여 **이벤트 뷰어**를 엽니다.

   > [!TIP]
   > Visual Studio에서 **서버 탐색기**를 열고(키보드: **Ctrl**+**Alt**+**S**) 로컬 컴퓨터의 **이벤트 로그** 노드를 확장하면 이벤트 로그에 액세스할 수 있습니다.

2. **이벤트 뷰어**에서 **응용 프로그램 및 서비스 로그**를 확장합니다.

3. **MyNewLog**(또는 선택적 절차에 따라 명령줄 인수를 추가한 경우 **MyLogFile1**)의 목록을 찾아서 확장합니다. 서비스에서 수행한 두 작업(시작 및 중지)의 항목이 표시됩니다.

     ![이벤트 뷰어를 사용하여 이벤트 로그 항목 확인](../../../docs/framework/windows-services/media/windows-service-event-viewer.png)

## <a name="uninstall-the-service"></a>서비스 제거

1. 관리자 자격 증명을 사용하여 **Visual Studio에 대한 개발자 명령 프롬프트**를 엽니다.

2. 명령 프롬프트 창에서 프로젝트의 출력이 포함된 폴더로 이동합니다.

3. 다음 명령을 입력합니다.

    ```shell
    installutil.exe /u MyNewService.exe
    ```

   서비스를 성공적으로 제거한 경우 **installutil.exe**에서 서비스가 성공적으로 제거되었음을 보고합니다. 자세한 내용은 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

이제 서비스가 만들어졌으므로, 다른 사용자가 Windows 서비스를 설치하는 데 사용할 수 있는 독립형 설치 프로그램을 만드는 것이 좋습니다. ClickOnce는 Windows 서비스를 지원하지 않지만 [WiX Toolset](http://wixtoolset.org/)를 사용하여 Windows 서비스용 설치 관리자를 만들 수 있습니다. 다른 아이디어를 보려면 [설치 관리자 패키지 만들기](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-client)를 참조하세요.

설치한 서비스에 명령을 보낼 수 있는 <xref:System.ServiceProcess.ServiceController> 구성 요소를 사용해 볼 수 있습니다.

이벤트 로그는 응용 프로그램이 실행될 때 만드는 것보다는 응용 프로그램이 설치될 때 설치 관리자를 사용하여 만드는 것이 좋습니다. 또한 이벤트 로그는 응용 프로그램이 제거되면 설치 관리자에 의해 삭제됩니다. 자세한 내용은 <xref:System.Diagnostics.EventLogInstaller> 참조 페이지를 참조하세요.

## <a name="see-also"></a>참고 항목

- [Windows 서비스 응용 프로그램](../../../docs/framework/windows-services/index.md)
- [Windows 서비스 응용 프로그램 소개](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)
- [방법: Windows 서비스 응용 프로그램 디버그](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)
- [Services (Windows)](https://msdn.microsoft.com/library/windows/desktop/ms685141.aspx)(서비스(Windows))
