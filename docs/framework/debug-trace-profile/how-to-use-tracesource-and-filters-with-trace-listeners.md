---
title: '방법: 추적 수신기와 함께 TraceSource 및 필터 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- initializing trace listeners
- configuration files [.NET Framework], trace listeners
- app.config files, trace listeners
- levels of writing trace messages
- trace listeners, TraceSource class
- application configuration files, trace listeners
- filters, trace listeners
- TraceSource class, trace listeners
- trace listeners, creating
- trace listeners, filters
- trace listeners, initializing
ms.assetid: 21dc2169-947d-453a-b0e2-3dac3ba0cc9f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a1e214266b66f390fecffe802270a4181a6d7a7f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052689"
---
# <a name="how-to-use-tracesource-and-filters-with-trace-listeners"></a>방법: 추적 수신기와 함께 TraceSource 및 필터 사용
.NET Framework 버전 2.0의 새로운 기능 중 하나는 향상된 추적 시스템입니다. 기본 전제는 변경되지 않습니다. 추적 메시지는 스위치를 통해 수신기로 전송되고 이러한 수신기는 데이터를 연결된 출력 매체에 보고합니다. 버전 2.0에 대한 주요 차이점은 추적이 <xref:System.Diagnostics.TraceSource> 클래스의 인스턴스를 통해 시작될 수 있다는 것입니다. <xref:System.Diagnostics.TraceSource>는 향상된 추적 시스템으로 작동해야 하고 오래된 <xref:System.Diagnostics.Trace> 및 <xref:System.Diagnostics.Debug> 추적 클래스의 정적 메서드 대신 사용될 수 있습니다. 익숙한 <xref:System.Diagnostics.Trace> 및 <xref:System.Diagnostics.Debug> 클래스가 있지만 추적에는 <xref:System.Diagnostics.TraceSource> 클래스를 사용하는 것이 좋습니다.  
  
 이 항목에서는 애플리케이션 구성 파일과 함께 <xref:System.Diagnostics.TraceSource>를 사용하는 방법을 설명합니다.  권장되지는 않지만 구성 파일을 사용하지 않고 <xref:System.Diagnostics.TraceSource>를 사용하여 추적할 수 있습니다. 구성 파일 [없이 추적 하는 방법에 대 한 자세한 내용은 방법: 추적 소스](how-to-create-and-initialize-trace-sources.md)를 만들고 초기화 합니다.  
  
### <a name="to-create-and-initialize-your-trace-source"></a>추적 소스를 만들고 초기화하려면  
  
1. 추적을 통해 애플리케이션을 계측하는 첫 번째 단계는 추적 소스를 만드는 것입니다. 다양한 구성 요소가 포함된 대규모 프로젝트에서 각 구성 요소에 대한 개별 추적 소스를 만들 수 있습니다. 추적 소스 이름에 대해 애플리케이션 이름을 사용하는 것이 좋습니다. 이렇게 하면 여러 추적을 쉽게 분리할 수 있습니다. 다음 코드에서는 이벤트를 추적하는 새 추적 소스(`mySource)`)를 만들고 메서드(`Activity1`)를 호출합니다.  추적 메시지는 기본 추적 수신기에서 작성됩니다.  
  
    ```csharp
    using System;  
    using System.Diagnostics;  
    using System.Threading;  
  
    namespace TraceSourceApp  
    {  
        class Program  
        {  
            private static TraceSource mySource =   
                new TraceSource("TraceSourceApp");  
            static void Main(string[] args)  
            {  
                Activity1();  
                mySource.Close();  
                return;  
            }  
            static void Activity1()  
            {  
                mySource.TraceEvent(TraceEventType.Error, 1,   
                    "Error message.");  
                mySource.TraceEvent(TraceEventType.Warning, 2,   
                    "Warning message.");  
            }  
        }  
    }  
    ```  
  
### <a name="to-create-and-initialize-trace-listeners-and-filters"></a>추적 수신기 및 필터를 만들고 초기화하려면  
  
1. 첫 번째 프로시저의 코드는 추적 수신기 또는 필터를 프로그래밍 방식으로 식별하지 않습니다. 이 코드만으로는 추적 메시지가 기본 추적 수신기에 기록되지 않습니다. 특정 추적 수신기 및 수신기의 연결된 필터를 구성하려면 애플리케이션 이름에 해당하는 구성 파일을 편집합니다. 이 파일에서 수신기를 추가 또는 제거하거나, 수신기에 대한 속성 및 필터를 설정하거나, 수신기를 제거할 수 있습니다. 다음 구성 파일 예제에서는 이전 프로시저에서 만들어진 추적 소스에 대해 콘솔 추적 수신기 및 텍스트 기록기 추적 수신기를 초기화하는 방법을 보여 줍니다. 추적 수신기의 구성 이외에도 구성 파일은 두 수신기에 대한 필터를 만들고 추적 소스에 대한 소스 스위치를 만듭니다. 추적 수신기를 추가하는 데는 두 가지 방법이 사용됩니다. 즉 수신기를 추적 소스에 직접 추가하는 방법과 수신기를 공유 컬렉션에 추가한 다음 이를 이름별로 추적 소스에 추가하는 방법이 있습니다. 두 수신기에 대해 식별된 필터는 서로 다른 소스 수준으로 초기화됩니다. 이로 인해 일부 메시지가 두 수신기 중 하나에 의해서만 기록됩니다.  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <source name="TraceSourceApp"   
            switchName="sourceSwitch"   
            switchType="System.Diagnostics.SourceSwitch">  
            <listeners>  
              <add name="console"   
                type="System.Diagnostics.ConsoleTraceListener">  
                <filter type="System.Diagnostics.EventTypeFilter"   
                  initializeData="Warning"/>  
              </add>  
              <add name="myListener"/>  
              <remove name="Default"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="sourceSwitch" value="Warning"/>  
        </switches>  
        <sharedListeners>  
          <add name="myListener"   
            type="System.Diagnostics.TextWriterTraceListener"   
            initializeData="myListener.log">  
            <filter type="System.Diagnostics.EventTypeFilter"   
              initializeData="Error"/>  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
### <a name="to-change-the-level-at-which-a-listener-writes-a-trace-message"></a>수신기가 추적 메시지를 기록하는 수준을 변경하려면  
  
1. 구성 파일은 응용 프로그램이 초기화될 때 추적 소스에 대한 설정을 초기화합니다. 해당 설정을 변경하려면 구성 파일을 변경하고 애플리케이션을 다시 시작하거나, <xref:System.Diagnostics.Trace.Refresh%2A?displayProperty=nameWithType> 메서드를 사용하여 애플리케이션을 프로그래밍 방식으로 새로 고쳐야 합니다. 응용 프로그램은 구성 파일에서 설정되는 속성을 동적으로 변경하여 사용자가 지정한 설정을 재정의할 수 있습니다.  예를 들어, 현재의 구성 설정과 관계없이 중대 오류 메시지를 항상 텍스트 파일로 보내도록 할 수 있습니다.  
  
    ```csharp
    using System;  
    using System.Diagnostics;  
    using System.Threading;  
  
    namespace TraceSourceApp  
    {  
        class Program  
        {  
            private static TraceSource mySource =   
                new TraceSource("TraceSourceApp");  
            static void Main(string[] args)  
            {  
                Activity1();  
  
                // Change the event type for which tracing occurs.  
                // The console trace listener must be specified   
                // in the configuration file. First, save the original  
                // settings from the configuration file.  
                EventTypeFilter configFilter =   
                    (EventTypeFilter)mySource.Listeners["console"].Filter;  
  
                // Then create a new event type filter that ensures   
                // critical messages will be written.  
                mySource.Listeners["console"].Filter =  
                    new EventTypeFilter(SourceLevels.Critical);  
                Activity2();  
  
                // Allow the trace source to send messages to listeners   
                // for all event types. This statement will override   
                // any settings in the configuration file.  
                mySource.Switch.Level = SourceLevels.All;  
  
                // Restore the original filter settings.  
                mySource.Listeners["console"].Filter = configFilter;  
                Activity3();  
                mySource.Close();  
                return;  
            }  
            static void Activity1()  
            {  
                mySource.TraceEvent(TraceEventType.Error, 1,   
                    "Error message.");  
                mySource.TraceEvent(TraceEventType.Warning, 2,   
                    "Warning message.");  
            }  
            static void Activity2()  
            {  
                mySource.TraceEvent(TraceEventType.Critical, 3,   
                    "Critical message.");  
                mySource.TraceInformation("Informational message.");  
            }  
            static void Activity3()  
            {  
                mySource.TraceEvent(TraceEventType.Error, 4,   
                    "Error message.");  
                mySource.TraceInformation("Informational message.");  
            }  
        }  
    }  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.ConsoleTraceListener>
- <xref:System.Diagnostics.EventTypeFilter>
- [방법: 추적 소스 만들기 및 초기화](how-to-create-and-initialize-trace-sources.md)
- [추적 수신기](trace-listeners.md)
