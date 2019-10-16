---
title: '자습서: Windows 서비스 앱 만들기'
ms.date: 03/27/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows service applications, walkthroughs
- Windows service applications, creating
ms.assetid: e24d8a3d-edc6-485c-b6e0-5672d91fb607
author: ghogen
ms.openlocfilehash: e5ff40d8413acf64e7a8a129a7b268f58780d591
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053479"
---
# <a name="tutorial-create-a-windows-service-app"></a>자습서: Windows 서비스 앱 만들기

이 문서에서는 이벤트 로그에 메시지를 쓰는 Windows 서비스 앱을 Visual Studio에서 만드는 방법을 보여 줍니다.

## <a name="create-a-service"></a>서비스 만들기

우선 프로젝트를 만들고 서비스가 제대로 작동하는 데 필요한 값을 설정합니다.

1. Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택하거나 **Ctrl**+**Shift**+**N**을 눌러 **새 프로젝트** 창을 엽니다.

2. **Windows 서비스(.NET Framework)** 프로젝트 템플릿을 검색하여 선택합니다. 템플릿을 찾으려면 **설치됨**과 **Visual C#** 또는 **Visual Basic**을 차례로 확장한 후 **Windows 데스크톱**을 선택합니다. 또는 오른쪽 상단의 검색 상자에서 *Windows 서비스*를 입력하고 **Enter** 키를 누릅니다.

   ![Visual Studio의 새 프로젝트 대화 상자에 있는 Windows 서비스 템플릿](./media/new-project-dialog.png)

   > [!NOTE]
   > **Windows 서비스** 템플릿이 표시되지 않는 경우 **.NET 데스크톱 개발** 워크로드를 설치해야 할 수 있습니다.
   >
   > **새 프로젝트** 대화 상자의 왼쪽 하단에서 **Visual Studio 설치 관리자 열기**를 선택합니다. **.NET 데스크톱 개발** 워크로드를 선택한 다음, **수정**을 선택합니다.

3. **이름**에서 *MyNewService*를 입력한 다음, **확인**을 선택합니다.

   **디자인** 탭이 표시됩니다(**Service1.cs [디자인]** 또는 **Service1.vb [디자인]** ).

   프로젝트 템플릿은 <xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType>에서 상속된 `Service1`이라는 구성 요소 클래스를 포함합니다. 여기에는 서비스를 시작하는 코드 등의 많은 기본 서비스 코드가 포함됩니다.

## <a name="rename-the-service"></a>서비스 이름 바꾸기

서비스 이름을 **Service1**에서 **MyNewService**로 바꿉니다.

1. **솔루션 탐색기**에서 **Service1.cs** 또는 **Service1.vb**를 선택하고 바로 가기 메뉴에서 **이름 바꾸기**를 선택합니다. 파일 이름을 **MyNewService.cs** 또는 **MyNewService.vb**로 바꾼 다음, **Enter** 키를 누릅니다.

    코드 요소 *Service1*에 대한 모든 참조 이름을 변경할지 여부를 묻는 팝업 창이 나타납니다.

2. 팝업 창에서 **예**를 선택합니다.

    ![이름 바꾸기 프롬프트](./media/windows-service-rename.png "Windows 서비스 이름 바꾸기 프롬프트")

3. **디자인** 탭의 바로 가기 메뉴에서 **속성**을 선택합니다. **속성** 창에서 **ServiceName** 값을 *MyNewService*로 변경합니다.

    ![서비스 속성](./media/windows-service-properties.png "Windows 서비스 속성")

4. **파일** 메뉴에서 **모두 저장**을 선택합니다.

## <a name="add-features-to-the-service"></a>서비스에 기능 추가

다음 섹션에서는 Windows 서비스에 사용자 지정 이벤트 로그를 추가합니다. Windows 서비스에 추가할 수 있는 구성 요소 종류의 한 예로 <xref:System.Diagnostics.EventLog> 구성 요소를 사용합니다.

### <a name="add-custom-event-log-functionality"></a>사용자 지정 이벤트 로그 기능 추가

1. **솔루션 탐색기**에서 **MyNewService.cs** 또는 **MyNewService.vb**의 바로 가기 메뉴에 있는 **뷰 디자이너**를 선택합니다.

2. **도구 상자**에서 **구성 요소**를 확장한 다음, **EventLog** 구성 요소를 **Service1.cs [디자인]** 또는 **Service1.vb [디자인]** 탭으로 끕니다.

3. **솔루션 탐색기**에서 **MyNewService.cs** 또는 **MyNewService.vb**의 바로 가기 메뉴에 있는 **코드 보기**를 선택합니다.

4. 사용자 지정 이벤트 로그를 정의합니다. C#에서는 기존 `MyNewService()` 생성자를 편집하고 Visual Basic에서는 `New()` 생성자를 추가합니다.

   [!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#2)]
   [!code-vb[VbRadconService#2](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#2)]

5. `using` 문을 **MyNewService.cs**에 추가하거나(없는 경우) <xref:System.Diagnostics?displayProperty=nameWithType> 네임스페이스에 대해서는 `Imports` 문을 **MyNewService.vb**에 추가합니다.

    ```csharp
    using System.Diagnostics;
    ```

    ```vb
    Imports System.Diagnostics
    ```

6. **파일** 메뉴에서 **모두 저장**을 선택합니다.

### <a name="define-what-occurs-when-the-service-starts"></a>서비스가 시작될 때 수행되는 동작 정의

**MyNewService.cs** 또는 **MyNewService.vb**의 코드 편집기에서 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드를 찾습니다. Visual Studio는 프로젝트를 만들 때 자동으로 빈 메서드 정의를 만듭니다. 서비스가 시작될 때 이벤트 로그에 항목을 기록하는 코드를 추가합니다.

[!code-csharp[VbRadconService#3](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#3)]
[!code-vb[VbRadconService#3](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#3)]

#### <a name="polling"></a>폴링

서비스 애플리케이션은 오랫동안 실행되도록 설계되므로 대개 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드에서 설정한 시스템을 폴링하거나 모니터링합니다. 서비스의 작업이 시작되고 나면 `OnStart` 메서드가 운영 체제에 반환되어야 시스템이 차단되지 않습니다.

간단한 폴링 메커니즘을 설정하려면 <xref:System.Timers.Timer?displayProperty=nameWithType> 구성 요소를 사용합니다. 타이머가 일정 간격으로 <xref:System.Timers.Timer.Elapsed> 이벤트를 발생시키며 서비스는 이벤트가 발생했을 때 모니터링을 수행할 수 있습니다. <xref:System.Timers.Timer> 구성 요소는 다음과 같이 사용합니다.

- `MyNewService.OnStart` 메서드에서 <xref:System.Timers.Timer> 구성 요소의 속성을 설정합니다.
- <xref:System.Timers.Timer.Start%2A> 메서드를 호출하여 타이머를 시작합니다.

##### <a name="set-up-the-polling-mechanism"></a>폴링 메커니즘을 설정합니다.

1. `MyNewService.OnStart` 이벤트에 다음 코드를 추가하여 폴링 메커니즘을 설정합니다.

   ```csharp
   // Set up a timer that triggers every minute.
   Timer timer = new Timer();
   timer.Interval = 60000; // 60 seconds
   timer.Elapsed += new ElapsedEventHandler(this.OnTimer);
   timer.Start();
   ```

   ```vb
   ' Set up a timer that triggers every minute.
   Dim timer As Timer = New Timer()
   timer.Interval = 60000 ' 60 seconds
   AddHandler timer.Elapsed, AddressOf Me.OnTimer
   timer.Start()
   ```

2. `using` 문을 **MyNewService.cs**에 추가하거나 <xref:System.Timers?displayProperty=nameWithType> 네임스페이스에 대해서는 `Imports` 문을 **MyNewService.vb**에 추가합니다.

   ```csharp
   using System.Timers;
   ```

   ```vb
   Imports System.Timers
   ```

3. `MyNewService` 클래스에서 `OnTimer` 메서드를 추가하여 <xref:System.Timers.Timer.Elapsed?displayProperty=nameWithType> 이벤트를 처리합니다.

   ```csharp
   public void OnTimer(object sender, ElapsedEventArgs args)
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

4. `MyNewService` 클래스에서 멤버 변수를 추가합니다. 여기에는 이벤트 로그에 기록할 다음 이벤트의 식별자가 포함됩니다.

   ```csharp
   private int eventId = 1;
   ```

   ```vb
   Private eventId As Integer = 1
   ```

주 스레드에서 모든 작업을 실행하는 대신 백그라운드 작업자 스레드를 사용하여 작업을 실행할 수도 있습니다. 자세한 내용은 <xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>을 참조하세요.

### <a name="define-what-occurs-when-the-service-is-stopped"></a>서비스가 중지될 때 수행되는 동작 정의

서비스가 중지될 때 이벤트 로그에 항목을 추가하는 코드 줄을 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드에 삽입합니다.

[!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#4)]
[!code-vb[VbRadconService#4](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#4)]

### <a name="define-other-actions-for-the-service"></a>서비스의 다른 동작 정의

<xref:System.ServiceProcess.ServiceBase.OnPause%2A>, <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 및 <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> 메서드를 재정의하여 구성 요소에 대한 처리 작업을 추가로 정의할 수 있습니다.

다음 코드에서는 `MyNewService` 클래스에서 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 메서드를 재정의하는 방법을 보여 줍니다.

[!code-csharp[VbRadconService#5](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#5)]
[!code-vb[VbRadconService#5](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#5)]

## <a name="set-service-status"></a>서비스 상태 설정

서비스는 [서비스 제어 관리자](/windows/desktop/Services/service-control-manager)에 상태를 보고합니다. 따라서 사용자는 서비스가 정상적으로 작동 중인지를 확인할 수 있습니다. 기본적으로 <xref:System.ServiceProcess.ServiceBase>에서 상속되는 서비스는 SERVICE_STOPPED, SERVICE_PAUSED 및 SERVICE_RUNNING을 포함하여 제한된 상태 설정 세트를 보고합니다. 서비스를 시작하는 데 시간이 걸리는 경우에는 SERVICE_START_PENDING 상태를 보고하면 도움이 됩니다.

또한 Windows [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) 함수를 호출하는 코드를 추가하여 SERVICE_START_PENDING 및 SERVICE_STOP_PENDING 상태 설정을 구현할 수 있습니다.

### <a name="implement-service-pending-status"></a>서비스 보류 중 상태 구현

1. `using` 문을 **MyNewService.cs**에 추가하거나 <xref:System.Runtime.InteropServices?displayProperty=nameWithType> 네임스페이스에 대해서는 `Imports` 문을 **MyNewService.vb**에 추가합니다.

    ```csharp
    using System.Runtime.InteropServices;
    ```

    ```vb
    Imports System.Runtime.InteropServices
    ```

2. `ServiceState` 값을 선언하고 상태에 대한 구조(플랫폼 호출에서 사용함)를 추가하려면 **MyNewService.cs** 또는 **MyNewService.vb**에 다음 코드를 추가합니다.

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

    > [!NOTE]
    > 서비스 제어 관리자는 [SERVICE_STATUS 구조체](/windows/win32/api/winsvc/ns-winsvc-service_status)의 `dwWaitHint` 및 `dwCheckpoint` 멤버를 사용하여 Windows 서비스가 시작 또는 종료될 때까지 기다릴 시간을 결정합니다. `OnStart` 및 `OnStop` 메서드가 오랫동안 실행되는 경우 서비스는 증분된 `dwCheckPoint` 값을 포함하여 `SetServiceStatus`을(를) 다시 호출하여 시간을 더 요청할 수 있습니다.

3. `MyNewService` 클래스에서 [플랫폼 호출](../interop/consuming-unmanaged-dll-functions.md)을 사용하여 [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) 함수를 선언합니다.

    ```csharp
    [DllImport("advapi32.dll", SetLastError = true)]
    private static extern bool SetServiceStatus(System.IntPtr handle, ref ServiceStatus serviceStatus);
    ```

    ```vb
    Declare Auto Function SetServiceStatus Lib "advapi32.dll" (ByVal handle As IntPtr, ByRef serviceStatus As ServiceStatus) As Boolean
    ```

4. SERVICE_START_PENDING 상태를 구현하려면 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드 시작 부분에 다음 코드를 추가합니다.

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

5. 상태를 SERVICE_RUNNING으로 설정하려면 `OnStart` 메서드 끝에 코드를 추가합니다.

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

6. (선택 사항) <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 메서드가 장기 실행 메서드인 경우 `OnStop` 메서드에서 이 절차를 반복합니다. SERVICE_STOP_PENDING 상태를 구현하고 `OnStop` 메서드가 끝나기 전에 SERVICE_STOPPED 상태를 반환합니다.

   예:

    ```csharp
    // Update the service state to Stop Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);

    // Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Stop Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)

    ' Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

## <a name="add-installers-to-the-service"></a>서비스에 설치 관리자 추가

Windows 서비스를 실행하려면 해당 서비스를 설치해야 합니다. 그러면 서비스 제어 관리자에 서비스가 등록됩니다. 등록 정보를 처리하는 설치 관리자를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 **MyNewService.cs** 또는 **MyNewService.vb**의 바로 가기 메뉴에 있는 **뷰 디자이너**를 선택합니다.

2. **디자인** 뷰에서 백그라운드 영역을 선택한 다음, 바로 가기 메뉴에서 **설치 관리자 추가**를 선택합니다.

     기본적으로 Visual Studio는 이름이 `ProjectInstaller`인 구성 요소 클래스를 추가하고 여기에는 프로젝트에 대한 두 개의 설치 관리자가 포함되어 있습니다. 이러한 설치 관리자는 서비스 및 서비스에 연결된 프로세스에 사용됩니다.

3. **ProjectInstaller**의 **디자인**뷰에서 Visual C# 프로젝트의 경우 **serviceInstaller1**을 선택하고 Visual Basic 프로젝트의 경우 **ServiceInstaller1**을 선택한 다음, 바로 가기 메뉴에서 **속성**을 선택합니다.

4. **속성** 창에서 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 속성이 **MyNewService**로 설정되어 있는지 확인합니다.

5. <xref:System.ServiceProcess.ServiceInstaller.Description%2A> 속성에 *샘플 서비스*와 같은 텍스트를 추가합니다.

     이 텍스트는 **서비스** 창의 **설명** 열에 표시되어 사용자에게 서비스를 설명합니다.

    ![서비스 창의 서비스 설명입니다.](./media/windows-service-description.png "서비스 설명")

6. <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> 속성에 텍스트를 추가합니다. 예를 들어 *MyNewService 표시 이름*을 입력할 수 있습니다.

     이 텍스트는 **서비스** 창의 **표시 이름** 열에 표시됩니다. 이 이름은 시스템에서 사용하는 이름인 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 속성과 다를 수 있습니다(예: 시스템을 시작하는 `net start` 명령에 사용하는 이름).

7. 드롭 다운 목록에서 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 속성을 <xref:System.ServiceProcess.ServiceStartMode.Automatic>(으)로 설정합니다.

8. 완료되면 **속성** 창이 다름 그림과 같아야 합니다.

     ![Windows 서비스에 대한 설치 관리자 속성](./media/windows-service-installer-properties.png "Windows 서비스 설치 관리자 속성")

9. **ProjectInstaller**의 **디자인**뷰에서 Visual C# 프로젝트의 경우 **serviceProcessInstaller1**을 선택하고 Visual Basic 프로젝트의 경우 **ServiceProcessInstaller1**을 선택한 다음, 바로 가기 메뉴에서 **속성**을 선택합니다. 드롭 다운 목록에서 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 속성을 <xref:System.ServiceProcess.ServiceAccount.LocalSystem>(으)로 설정합니다.

     이 설정은 서비스를 설치하고 로컬 시스템 계정을 사용하여 실행합니다.

    > [!IMPORTANT]
    > <xref:System.ServiceProcess.ServiceAccount.LocalSystem> 계정에는 광범위한 권한이 있습니다. 예를 들어, 이 계정은 이벤트 로그에 쓸 수 있습니다. 이 계정을 사용할 때는 악성 소프트웨어의 공격을 받을 가능성이 커지므로 주의해야 합니다. 다른 작업에는 <xref:System.ServiceProcess.ServiceAccount.LocalService> 계정을 사용하는 것이 좋습니다. 이 계정은 로컬 컴퓨터에서 권한 없는 사용자의 역할을 하며 원격 서버에 익명 자격 증명을 제공합니다. <xref:System.ServiceProcess.ServiceAccount.LocalService> 계정을 사용하는 경우 이 예제는 실패합니다. 이벤트 로그에 대한 쓰기 권한이 필요하기 때문입니다.

설치 관리자에 대한 자세한 내용은 [방법: 서비스 애플리케이션에 설치 관리자 추가](how-to-add-installers-to-your-service-application.md)를 참조하세요.

## <a name="optional-set-startup-parameters"></a>(선택 사항) 시작 매개 변수 설정

> [!NOTE]
> 시작 매개 변수 추가를 결정하기 전에 시작 매개 변수가 서비스로 정보를 전달하는 가장 효율적인 방법인지를 고려합니다. 시작 매개 변수는 쉽게 사용하고 구문 분석할 수 있으며 사용자가 쉽게 재정의할 수 있지만 설명서가 없으면 사용자가 검색하고 사용하기가 어려울 수 있습니다. 일반적으로 서비스에 많은 시작 매개 변수가 필요한 경우에는 레지스트리나 구성 파일을 대신 사용해야 합니다.

Windows 서비스에는 명령줄 인수나 시작 매개 변수를 사용할 수 있습니다. 프로세스 시작 매개 변수에 코드를 추가하면 사용자가 서비스 속성 창에서 고유한 사용자 지정 시작 매개 변수로 서비스를 시작할 수 있습니다. 그러나 이러한 시작 매개 변수는 다음 번에 서비스를 시작할 때 유지되지 않습니다. 시작 매개 변수를 영구적으로 설정하려면 레지스트리에서 설정합니다.

각 Windows 서비스에는 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services** 하위 키에 레지스트리 항목이 있습니다. 각 서비스의 하위 키 아래에서 **매개 변수** 하위 키를 사용하여 서비스가 액세스할 수 있는 정보를 저장합니다. Windows 서비스의 애플리케이션 구성 파일은 다른 프로그램 형식에서와 같은 방식으로 사용할 수 있습니다. 샘플 코드는 <xref:System.Configuration.ConfigurationManager.AppSettings?displayProperty=nameWithType>을(를) 참조하세요.

### <a name="to-add-startup-parameters"></a>시작 매개 변수를 추가하려면

1. **Program.cs** 또는 **MyNewService.Designer.vb**를 선택한 다음, 바로 가기 메뉴에서 **코드 보기**를 선택합니다. `Main` 메서드에서 코드를 변경해 입력 매개 변수를 추가하고 서비스 생성자에게 전달합니다.

   [!code-csharp[VbRadconService](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/Program-add-parameter.cs?highlight=1,6)]
   [!code-vb[VbRadconService](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.Designer-add-parameter.vb?highlight=1-2)]

2. **MyNewService.cs** 또는 **MyNewService.vb**에서 `MyNewService` 생성자를 변경하여 입력 매개 변수를 다름과 같이 처리합니다.

   ```csharp
   using System.Diagnostics;

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

       eventLog1 = new EventLog();

       if (!EventLog.SourceExists(eventSourceName))
       {
           EventLog.CreateEventSource(eventSourceName, logName);
       }

       eventLog1.Source = eventSourceName;
       eventLog1.Log = logName;
   }
   ```

   ```vb
   Imports System.Diagnostics

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
       eventLog1 = New EventLog()
       If (Not EventLog.SourceExists(eventSourceName)) Then
           EventLog.CreateEventSource(eventSourceName, logName)
       End If
       eventLog1.Source = eventSourceName
       eventLog1.Log = logName
   End Sub
   ```

   이 코드는 사용자가 제공하는 시작 매개 변수에 따라 이벤트 소스와 로그 이름을 설정합니다. 인수가 제공되지 않으면 기본값이 사용됩니다.

3. 명령줄 인수를 지정하려면 **ProjectInstaller.cs** 또는 **ProjectInstaller.vb**의 `ProjectInstaller` 클래스에 다음 코드를 추가합니다.

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

   일반적으로 이 값에는 Windows 서비스에 대한 실행 파일의 전체 경로가 포함됩니다. 서비스를 올바르게 시작하려면 사용자는 경로와 개별 매개 변수에 따옴표를 사용해야 합니다. 사용자는 **ImagePath** 레지스트리 항목에서 매개 변수를 변경하여 Windows 서비스에 대한 시작 매개 변수를 변경할 수 있습니다. 그러나 프로그래밍 방식으로 값을 변경하고 관리 또는 구성 유틸리티를 사용하는 것과 같이 사용자에게 익숙한 방식으로 기능을 노출시키는 것이 더 나은 방식입니다.

## <a name="build-the-service"></a>서비스 빌드

1. **솔루션 탐색기**에 있는 **MyNewService** 프로젝트의 바로 가기 메뉴에서 **속성**을 선택합니다.

   프로젝트의 속성 페이지가 나타납니다.

2. **애플리케이션** 탭의 **시작 개체** 목록에서 **MyNewService.Program**을 선택하거나 Visual Basic 프로젝트의 **Sub Main**을 선택합니다.

3. 프로젝트를 빌드하려면 **솔루션 탐색기**를 열고 프로젝트의 바로 가기 메뉴에 있는 **빌드**를 선택합니다(또는 **Ctrl**+**Shift**+**B**를 누름).

## <a name="install-the-service"></a>서비스 설치

이제 Windows 서비스를 빌드했으므로 이를 설치할 수 있습니다. Windows 서비스를 설치하려면 설치할 컴퓨터에서 관리자 자격 증명이 있어야 합니다.

1. 관리자 자격 증명을 사용하여 [Visual Studio에 대한 개발자 명령 프롬프트](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)를 엽니다. Windows **시작** 메뉴에서 Visual Studio 폴더에 있는 **VS 2017에 대한 개발자 명령 프롬프트**를 선택한 다음, 바로 가기 메뉴에서 **자세히** > **관리자로 실행**을 선택합니다.

2. **Visual Studio에 대한 개발자 명령 프롬프트** 창에서 프로젝트의 출력이 포함된 폴더(기본적으로 프로젝트의 *\bin\Debug* 하위 디렉터리)로 이동합니다.

3. 다음 명령을 입력합니다.

    ```shell
    installutil MyNewService.exe
    ```

    서비스를 성공적으로 설치한 경우 명령이 설치에 성공했음을 보고합니다.

    시스템에서 *installutil.exe*를 찾을 수 없는 경우 해당 파일이 컴퓨터에 있는지 확인합니다. 이 도구는 *%windir%\Microsoft.NET\Framework[64]\\&lt;프레임워크 버전&gt;* 폴더에 .NET Framework와 함께 설치됩니다. 예를 들어 64비트 버전의 기본 경로는 *%windir%\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*입니다.

    **installutil.exe** 프로세스가 실패한 경우 설치 로그를 확인하여 이유를 찾아보세요. 기본적으로 로그는 서비스 실행 파일과 동일한 폴더에 있습니다. 다음과 같은 경우 설치에 실패할 수 있습니다.
    - <xref:System.ComponentModel.RunInstallerAttribute> 클래스가 `ProjectInstaller` 클래스에 없습니다.
    - 특성이 `true`(으)로 설정되지 않았습니다.
    - `ProjectInstaller` 클래스가 `public`(으)로 정의되지 않았습니다.

자세한 내용은 [방법: 서비스 설치 및 제거](how-to-install-and-uninstall-services.md)를 참조하세요.

## <a name="start-and-run-the-service"></a>서비스 시작 및 실행

1. Windows에서 **서비스** 데스크톱 앱을 엽니다. **Windows**+**R**을 눌러 **실행** 상자를 열고 *services.msc*를 입력한 다음, **Enter** 키를 누르거나 **확인**을 선택합니다.

     해당 서비스가 설정된 표시 이름의 사전순으로 **서비스**에 표시됩니다.

     ![서비스 창의 MyNewService입니다.](./media/windowsservices-serviceswindow.PNG)

2. 서비스를 시작하려면 서비스의 바로 가기 메뉴에서 **시작**을 선택합니다.

3. 서비스를 중지하려면 서비스의 바로 가기 메뉴에서 **중지**를 선택합니다.

4. (선택 사항) 명령줄에서 **net start &lt;서비스 이름&gt;** 및 **net stop &lt;서비스 이름&gt;** 명령을 사용하여 서비스를 시작하고 중지할 수 있습니다.

### <a name="verify-the-event-log-output-of-your-service"></a>서비스의 이벤트 로그 출력 확인

1. Windows에서 **이벤트 뷰어** 데스크톱 앱을 엽니다. Windows 검색 창에서 *이벤트 뷰어*를 입력한 다음, 검색 결과에서 **이벤트 뷰어**를 선택합니다.

   > [!TIP]
   > Visual Studio의 **보기** 메뉴에서 **서버 탐색기**를 열고(또는 **Ctrl**+**Alt**+**S**를 누름) 로컬 컴퓨터의 **이벤트 로그** 노드를 확장하면 이벤트 로그에 액세스할 수 있습니다.

2. **이벤트 뷰어**에서 **애플리케이션 및 서비스 로그**를 확장합니다.

3. **MyNewLog**(또는 절차에 따라 명령줄 인수를 추가한 경우 **MyLogFile1**)의 목록을 찾아서 확장합니다. 서비스에서 수행한 두 작업(시작 및 중지)의 항목이 표시됩니다.

     ![이벤트 뷰어를 사용하여 이벤트 로그 항목 확인](./media/windows-service-event-viewer.png)

## <a name="clean-up-resources"></a>리소스 정리

Windows 서비스 앱이 더 이상 필요 없는 경우 제거할 수 있습니다.

1. 관리자 자격 증명을 사용하여 **Visual Studio에 대한 개발자 명령 프롬프트**를 엽니다.

2. **Visual Studio에 대한 개발자 명령 프롬프트** 창에서 프로젝트의 출력이 포함된 폴더로 이동합니다.

3. 다음 명령을 입력합니다.

    ```shell
    installutil.exe /u MyNewService.exe
    ```

   서비스를 성공적으로 제거한 경우 명령은 서비스가 성공적으로 제거되었음을 보고합니다. 자세한 내용은 [방법: 서비스 설치 및 제거](how-to-install-and-uninstall-services.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

이제 서비스를 만들었으므로 다음을 수행할 수 있습니다.

- 다른 사용자가 Windows 서비스를 설치하는 데 사용하는 독립 실행형 설치 프로그램을 만듭니다. [WiX 도구 집합](https://wixtoolset.org/)를 사용하여 Windows 서비스의 설치 관리자를 만들 수 있습니다. 다른 아이디어를 보려면 [설치 관리자 패키지 만들기](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop)를 참조하세요.

- 설치한 서비스에 명령을 보낼 수 있는 <xref:System.ServiceProcess.ServiceController> 구성 요소를 살펴보세요.

- 애플리케이션이 실행될 때 이벤트 로그를 만드는 것보다는 애플리케이션이 설치될 때 설치 관리자를 사용하여 이벤트 로그를 만듭니다. 애플리케이션을 제거하면 설치 관리자가 이벤트 로그를 삭제합니다. 자세한 내용은 <xref:System.Diagnostics.EventLogInstaller>을 참조하세요.

## <a name="see-also"></a>참고 항목

- [Windows 서비스 애플리케이션](index.md)
- [Windows 서비스 애플리케이션 소개](introduction-to-windows-service-applications.md)
- [방법: Windows 서비스 애플리케이션 디버그](how-to-debug-windows-service-applications.md)
- [Services (Windows)](/windows/desktop/Services/services)(서비스(Windows))
