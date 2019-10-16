---
title: 워크플로 추적
ms.date: 03/30/2017
ms.assetid: 18737989-0502-4367-b5f6-617ebfb77c96
ms.openlocfilehash: 7bca78b24963d94bfa0f2e2245a677b7dce455c9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933434"
---
# <a name="workflow-tracing"></a>워크플로 추적
워크플로 추적을 사용하면 .NET Framework 추적 수신기를 통해 진단 정보를 캡처할 수 있습니다. 추적은 애플리케이션에서 문제가 발견되면 사용하도록 설정했다가 문제가 해결되면 다시 사용하지 않도록 설정할 수 있습니다. 워크플로에 대한 디버그 추적을 두 가지 방법으로 활성화할 수 있습니다. 이벤트 추적 뷰어를 사용하여 구성하거나 <xref:System.Diagnostics>를 사용하여 추적 이벤트를 파일로 보낼 수 있습니다.  
  
## <a name="enabling-debug-tracing-in-etw"></a>ETW에서 디버그 추적 사용  
 ETW를 사용하여 추적을 활성화하려면 이벤트 뷰어에서 디버그 채널을 사용하도록 설정합니다.  
  
1. 이벤트 뷰어에서 분석 및 디버그 로그 노드로 이동합니다.  
  
2. 이벤트 뷰어의 트리 뷰에서 **이벤트 뷰어 > 응용 프로그램 및 서비스 로그-> Microsoft > Windows-> 응용 프로그램 서버-응용**프로그램으로 이동 합니다. **응용 프로그램 서버-응용 프로그램** 을 마우스 오른쪽 단추로 클릭 하 고 **보기-> 분석 및 디버그 로그 표시**를 선택 합니다. **디버그** 를 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다.  
  
3. 워크플로에서 디버그를 실행하고 추적을 ETW 디버그 채널로 내보낸 후 이벤트 뷰어에서 추적 내용을 볼 수 있습니다. **이벤트 뷰어-> 응용 프로그램 및 서비스 로그-> Microsoft > Windows-> 응용 프로그램 서버-응용**프로그램으로 이동 합니다. **디버그** 를 마우스 오른쪽 단추로 클릭 하 고 **새로 고침**을 선택 합니다.  
  
4. 기본 분석 추적 버퍼 크기는 겨우 4KB이므로 이 크기를 32KB로 늘리는 것이 좋습니다. 이렇게 하려면 다음 단계를 수행합니다.  
  
    1. 현재 프레임워크 디렉터리(예: C:\Windows\Microsoft.NET\Framework\v4.0.21203)에서 `wevtutil um Microsoft.Windows.ApplicationServer.Applications.man` 명령을 실행합니다.  
  
    2. Windows applicationserver. man 파일의 bufferSize>값을32로변경합니다.\<  
  
        ```xml  
        <channel name="Microsoft-Windows-Application Server-Applications/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" >  
                    <publishing>  
                      <bufferSize>32</bufferSize>  
                    </publishing>  
                  </channel>  
        ```  
  
    3. 현재 프레임워크 디렉터리(예: C:\Windows\Microsoft.NET\Framework\v4.0.21203)에서 `wevtutil im Microsoft.Windows.ApplicationServer.Applications.man` 명령을 실행합니다.  
  
> [!NOTE]
> .NET Framework 4 클라이언트 프로필을 사용 하는 경우 먼저 .NET Framework 4 디렉터리에서 다음 명령을 실행 하 여 ETW 매니페스트를 등록 해야 합니다.`ServiceModelReg.exe –i –c:etw`  
  
## <a name="enabling-debug-tracing-using-systemdiagnostics"></a>System.Diagnostics를 사용하여 디버그 추적 활성화  
 이러한 수신기는 워크플로 애플리케이션의 App.config 파일 또는 워크플로 서비스의 Web.config에서 구성할 수 있습니다. 이 예제에서 [TextWriterTraceListener](https://go.microsoft.com/fwlink/?LinkId=165424) 는 추적 정보를 현재 디렉터리의 MyTraceLog 파일에 저장 하도록 구성 되어 있습니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.Activities" switchValue="Information">  
        <listeners>  
          <add name="textListener" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"  
           type="System.Diagnostics.TextWriterTraceListener"  
           initializeData="MyTraceLog.txt"  
           traceOutputOptions="ProcessId, DateTime" />  
    </sharedListeners>  
    <trace autoflush="true" indentsize="4">  
      <listeners>  
        <add name="textListener" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [Windows Server App Fabric 모니터링](https://go.microsoft.com/fwlink/?LinkId=201273)
- [App Fabric을 사용 하 여 응용 프로그램 모니터링](https://go.microsoft.com/fwlink/?LinkId=201275)
