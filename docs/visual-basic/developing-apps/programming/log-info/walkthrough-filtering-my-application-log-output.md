---
title: My.Application.Log 출력 필터링(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My.Log object, filtering output
- My.Application.Log object, filtering output
- application event logs, output filtering
ms.assetid: 2c0a457a-38a4-49e1-934d-a51320b7b4ca
ms.openlocfilehash: af1dc3e1ce22112d76ad566873f40c1c2ac05c9d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968696"
---
# <a name="walkthrough-filtering-myapplicationlog-output-visual-basic"></a>연습: My.Application.Log 출력 필터링(Visual Basic)
이 연습에서는 `My.Application.Log` 개체에 대한 기본 로그 필터링을 변경하여 `Log` 개체에서 수신기로 전달되는 정보 및 수신기가 작성하는 정보를 제어하는 방법을 보여 줍니다. 구성 정보가 애플리케이션의 구성 파일에 저장되므로 애플리케이션을 빌드한 후에도 로깅 동작을 변경할 수 있습니다.  
  
## <a name="getting-started"></a>시작  
 `My.Application.Log`에서 작성하는 각 메시지에는 연결된 심각도 수준이 있으며, 필터링 메커니즘은 로그 출력을 제어하는 데 이를 사용합니다. 이 샘플 애플리케이션은 `My.Application.Log` 메서드를 사용하여 서로 다른 심각도 수준으로 여러 로그 메시지를 작성합니다.  
  
#### <a name="to-build-the-sample-application"></a>샘플 애플리케이션을 빌드하려면  
  
1. 새 Visual Basic Windows 애플리케이션 프로젝트를 엽니다.  
  
2. Button1이라는 단추를 Form1에 추가합니다.  
  
3. Button1에 대한 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기에 다음 코드를 추가합니다.  
  
     [!code-vb[VbVbcnMyApplicationLogFiltering#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyApplicationLogFiltering/VB/Form1.vb#1)]  
  
4. 디버거에서 애플리케이션을 실행합니다.  
  
5. **Button1**을 누릅니다.  
  
     애플리케이션이 다음 정보를 애플리케이션의 디버그 출력 및 로그 파일에 기록합니다.  
  
     `DefaultSource Information: 0 : In Button1_Click`  
  
     `DefaultSource Error: 2 : Error in the application.`  
  
6. 애플리케이션을 닫습니다.  
  
     애플리케이션의 디버그 출력 창을 보는 방법에 대한 자세한 내용은 [출력 창](/visualstudio/ide/reference/output-window)을 참조하세요. 애플리케이션의 로그 파일 위치에 대한 정보는 [연습: My.Application.Log가 정보를 기록하는 위치 확인](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)을 참조하세요.  
  
    > [!NOTE]
    > 기본적으로 애플리케이션을 닫으면 애플리케이션이 로그 파일 출력을 플러시합니다.  
  
     위의 예제에서 <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A> 메서드에 대한 두 번째 호출 및 <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A> 메서드에 대한 호출은 로그 출력을 생성하지만, `WriteEntry` 메서드에 대한 첫 번째 및 마지막 호출은 로그 출력을 생성하지 않습니다. `WriteEntry` 및 `WriteException`의 심각도 수준은 "정보" 및 "오류"이므로, 둘 다 `My.Application.Log` 개체의 기본 로그 필터링에서 허용됩니다. 그러나 "시작" 및 "중지" 심각도 수준의 이벤트는 로그 출력 생성이 금지됩니다.  
  
## <a name="filtering-for-all-myapplicationlog-listeners"></a>모든 My.Application.Log 수신기에 대한 필터링  
 `My.Application.Log` 개체는 `DefaultSwitch`라고 명명된 <xref:System.Diagnostics.SourceSwitch>를 사용하여 `WriteEntry` 및 `WriteException` 메서드에서 로그 수신기로 전달할 메시지를 제어합니다. 해당 값을 <xref:System.Diagnostics.SourceLevels> 열거형 값 중 하나로 설정하여 애플리케이션의 구성 파일에서 `DefaultSwitch`를 구성할 수 있습니다. 기본적으로 값은 "정보"입니다.  
  
 다음 표는 특정 `DefaultSwitch` 설정이 지정된 경우 로그가 메시지를 수신기에 기록하는 데 필요한 심각도 수준을 보여 줍니다.  
  
|DefaultSwitch 값|출력에 필요한 메시지 심각도|  
|---|---| 
|`Critical`|`Critical`|  
|`Error`|`Critical` 또는 `Error`|  
|`Warning`|`Critical`, `Error`또는 `Warning`|  
|`Information`|`Critical`, `Error`, `Warning` 또는 `Information`|  
|`Verbose`|`Critical`, `Error`, `Warning`, `Information` 또는 `Verbose`|  
|`ActivityTracing`|`Start`, `Stop`, `Suspend`, `Resume` 또는 `Transfer`|  
|`All`|모든 메시지를 허용합니다.|  
|`Off`|모든 메시지를 차단합니다.|  
  
> [!NOTE]
> `WriteEntry` 및 `WriteException` 메서드는 각각 심각도 수준을 지정하지 않는 오버로드를 가지고 있습니다. `WriteEntry` 오버로드에 대한 암시적 심각도 수준은 "정보"이며, `WriteException` 오버로드에 대한 암시적 심각도 수준은 "오류"입니다.  
  
 다음 표는 이전 예제에 나와 있는 로그 출력을 설명합니다. 기본 `DefaultSwitch` 설정이 "정보"인 경우 `WriteEntry` 메서드에 대한 두 번째 호출 및 `WriteException` 메서드에 대한 호출만이 로그 출력을 생성합니다.  
  
#### <a name="to-log-only-activity-tracing-events"></a>작업 추적 이벤트만 기록하려면  
  
1. **솔루션 탐색기**에서 app.config를 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.  
  
     또는  
  
     app.config 파일이 없는 경우  
  
    1. **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다.  
  
    2. **새 항목 추가** 대화 상자에서 **애플리케이션 구성 파일**을 선택합니다.  
  
    3. **추가**를 클릭합니다.  
  
2. 최상위 `<configuration>` 섹션의 `<system.diagnostics>` 섹션에 있는 `<switches>` 섹션으로 이동합니다.  
  
3. 스위치 컬렉션에 `DefaultSwitch`를 추가하는 요소를 찾습니다. 이 요소는 다음과 유사합니다.  
  
     `<add name="DefaultSwitch" value="Information" />`  
  
4. `value` 특성의 값을 "ActivityTracing"으로 변경합니다.  
  
5. app.config 파일의 내용은 다음 XML과 비슷합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="ActivityTracing" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
6. 디버거에서 애플리케이션을 실행합니다.  
  
7. **Button1**을 누릅니다.  
  
     애플리케이션이 다음 정보를 애플리케이션의 디버그 출력 및 로그 파일에 기록합니다.  
  
     `DefaultSource Start: 4 : Entering Button1_Click`  
  
     `DefaultSource Stop: 5 : Leaving Button1_Click`  
  
8. 애플리케이션을 닫습니다.  
  
9. `value` 특성의 값을 다시 "정보"로 변경합니다.  
  
    > [!NOTE]
    > `DefaultSwitch` 스위치 설정은 `My.Application.Log`만 제어합니다. .NET Framework <xref:System.Diagnostics.Trace?displayProperty=nameWithType> 및 <xref:System.Diagnostics.Debug?displayProperty=nameWithType> 클래스 동작은 변경되지 않습니다.  
  
## <a name="individual-filtering-for-myapplicationlog-listeners"></a>My.Application.Log 수신기에 대한 개별 필터링  
 이전 예제에서는 모든 `My.Application.Log` 출력에 대한 필터링을 변경하는 방법을 보여 줍니다. 이 예제에서는 개별 로그 수신기를 필터링하는 방법을 보여 줍니다. 기본적으로 애플리케이션에는 각각 애플리케이션의 디버그 출력 및 로그 파일에 기록하는 두 개의 수신기가 있습니다.  
  
 구성 파일은 각 로그 수신기에 `My.Application.Log`용 스위치와 비슷한 필터를 허용하여 로그 수신기의 동작을 제어합니다. 로그 수신기는 로그의 `DefaultSwitch` 및 로그 수신기의 필터에서 메시지의 심각도를 허용하는 경우에만 메시지를 출력합니다.  
  
 이 예제는 새 디버그 수신기에 대한 필터링을 구성하고 `Log` 개체에 추가하는 방법을 보여 줍니다. 기본 디버그 수신기는 `Log` 개체에서 제거해야 하므로, 디버그 메시지가 새 디버그 수신기에서 오는 것이 분명합니다.  
  
#### <a name="to-log-only-activity-tracing-events"></a>동작 추적 이벤트만 기록하려면  
  
1. **솔루션 탐색기**에서 app.config를 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.  
  
     또는  
  
     app.config 파일이 없는 경우  
  
    1. **프로젝트** 메뉴에서 **새 항목 추가**를 선택합니다.  
  
    2. **새 항목 추가** 대화 상자에서 **애플리케이션 구성 파일**을 선택합니다.  
  
    3. **추가**를 클릭합니다.  
  
2. **솔루션 탐색기**에서 app.config를 마우스 오른쪽 단추로 클릭합니다. **열기**를 선택합니다.  
  
3. `<sources>` 섹션 아래에서 `name` 특성이 "DefaultSource"인 `<source>` 섹션에서 `<listeners>` 섹션을 찾습니다. `<sources>` 섹션은 최상위 `<configuration>` 섹션의 `<system.diagnostics>` 섹션에 있습니다.  
  
4. 이 요소를 `<listeners>` 섹션에 추가합니다.  
  
    ```xml  
    <!-- Remove the default debug listener. -->  
    <remove name="Default"/>  
    <!-- Add a filterable debug listener. -->  
    <add name="NewDefault"/>  
    ```  
  
5. 최상위 `<sharedListeners>` 섹션의 `<system.diagnostics>` 섹션에서 `<configuration>` 섹션을 찾습니다.  
  
6. 다음 요소를 `<sharedListeners>` 섹션에 추가합니다.  
  
    ```xml  
    <add name="NewDefault"   
         type="System.Diagnostics.DefaultTraceListener,   
               System, Version=2.0.0.0, Culture=neutral,   
               PublicKeyToken=b77a5c561934e089,   
               processorArchitecture=MSIL">  
        <filter type="System.Diagnostics.EventTypeFilter"   
                initializeData="Error" />  
    </add>  
    ```  
  
     <xref:System.Diagnostics.EventTypeFilter> 필터는 <xref:System.Diagnostics.SourceLevels> 열거형 값 중 하나를 해당 `initializeData` 특성으로 사용합니다.  
  
7. app.config 파일의 내용은 다음 XML과 비슷합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <!-- This section configures My.Application.Log -->  
          <source name="DefaultSource" switchName="DefaultSwitch">  
            <listeners>  
              <add name="FileLog"/>  
              <!-- Remove the default debug listener. -->  
              <remove name="Default"/>  
              <!-- Add a filterable debug listener. -->  
              <add name="NewDefault"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="DefaultSwitch" value="Information" />  
        </switches>  
        <sharedListeners>  
          <add name="FileLog"  
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,   
                     Microsoft.VisualBasic, Version=8.0.0.0,   
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a,   
                     processorArchitecture=MSIL"   
               initializeData="FileLogWriter"/>  
          <add name="NewDefault"   
               type="System.Diagnostics.DefaultTraceListener,   
                     System, Version=2.0.0.0, Culture=neutral,   
                     PublicKeyToken=b77a5c561934e089,   
                     processorArchitecture=MSIL">  
            <filter type="System.Diagnostics.EventTypeFilter"   
                    initializeData="Error" />  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
8. 디버거에서 애플리케이션을 실행합니다.  
  
9. **Button1**을 누릅니다.  
  
     애플리케이션이 다음 정보를 애플리케이션의 로그 파일에 기록합니다.  
  
     `Default Information: 0 : In Button1_Click`  
  
     `Default Error: 2 : Error in the application.`  
  
     애플리케이션은 좀 더 제한적인 필터링 때문에 애플리케이션의 디버그 출력에 정보를 더 적게 기록합니다.  
  
     `Default Error   2   Error`  
  
10. 애플리케이션을 닫습니다.  
  
 배포 후 로그 설정을 변경하는 방법에 대한 자세한 내용은 [애플리케이션 로그 작업](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [연습: My.Application.Log가 정보를 기록하는 위치 확인](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
- [연습: My.Application.Log가 정보를 기록하는 위치 변경](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
- [연습: 사용자 지정 로그 수신기 만들기](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)
- [방법: 로그 메시지 쓰기](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)
- [추적 스위치](../../../../framework/debug-trace-profile/trace-switches.md)
- [애플리케이션의 정보 기록](../../../../visual-basic/developing-apps/programming/log-info/index.md)
