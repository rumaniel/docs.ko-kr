---
title: 추적 및 메시지 로깅에 권장되는 설정
ms.date: 03/30/2017
ms.assetid: c6aca6e8-704e-4779-a9ef-50c46850249e
ms.openlocfilehash: 6e671762edb2d1ca71ce14cb6ef66c64e02bc297
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856089"
---
# <a name="recommended-settings-for-tracing-and-message-logging"></a>추적 및 메시지 로깅에 권장되는 설정
이 항목에서는 다른 운영 환경에 권장되는 추적 및 메시지 로깅 설정에 대해 설명합니다.  
  
## <a name="recommended-settings-for-a-production-environment"></a>프로덕션 환경에 대한 권장 설정  
 WCF 추적 소스를 사용하는 경우 프로덕션 환경에 대해 `switchValue`를 Warning으로 설정합니다. WCF `System.ServiceModel` 추적 소스를 사용하는 경우 `switchValue` 특성을 `Warning`, `propagateActivity` 특성을 `true`로 설정합니다. 사용자 정의 추적 소스를 사용하는 경우 `switchValue` 특성을 `Warning, ActivityTracing`으로 설정합니다. [구성 편집기 도구 (SvcConfigEditor)](../../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)를 사용 하 여 수동으로 수행할 수 있습니다. 성능 향상을 기대하지 않는 경우 앞에서 설명한 모든 경우에서 `switchValue` 특성을 `Information`으로 설정할 수 있습니다. 이렇게 하면 상당히 많은 추적 데이터가 생성됩니다. 다음 예제에서는 이러한 권장 설정을 보여 줍니다.  
  
```xml  
<configuration>  
 <system.diagnostics>  
  <sources>  
    <source name="System.ServiceModel"  
            switchValue="Warning"  
            propagateActivity="true" >  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="myUserTraceSource"  
            switchValue="Warning, ActivityTracing">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
  </sources>  
  <sharedListeners>  
    <add name="xml"  
         type="System.Diagnostics.XmlWriterTraceListener"  
               initializeData="C:\logs\Traces.svclog" />  
  </sharedListeners>  
 </system.diagnostics>  
  
<system.serviceModel>  
  <diagnostics wmiProviderEnabled="true">  
  </diagnostics>  
 </system.serviceModel>  
</configuration>  
```  
  
## <a name="recommended-settings-for-deployment-or-debugging"></a>배포 또는 디버깅에 대한 권장 설정  
 배포 또는 디버깅 환경의 경우 `Information` 또는 `Verbose`를 선택하고 사용자 정의 또는 `ActivityTracing` 추적 소스에 대해 `System.ServiceModel`을 선택합니다. 디버깅을 향상시키려면 다른 추적 소스(`System.ServiceModel.MessageLogging`)를 구성에 추가하여 메시지 로깅을 활성화해야 합니다. `switchValue` 특성은 이 추적 소스에 영향을 주지 않습니다.  
  
 다음 예제에서는 `XmlWriterTraceListener`를 이용하는 공유 수신기를 사용한 권장 설정을 보여 줍니다.  
  
```xml  
<configuration>  
 <system.diagnostics>  
  <sources>  
    <source name="System.ServiceModel"  
            switchValue="Information, ActivityTracing"  
            propagateActivity="true" >  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="System.ServiceModel.MessageLogging">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="myUserTraceSource"  
            switchValue="Information, ActivityTracing">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
  </sources>  
  <sharedListeners>  
    <add name="xml"  
         type="System.Diagnostics.XmlWriterTraceListener"  
               initializeData="C:\logs\Traces.svclog" />  
  </sharedListeners>  
 </system.diagnostics>  
  
 <system.serviceModel>  
  <diagnostics wmiProviderEnabled="true">  
      <messageLogging   
           logEntireMessage="true"   
           logMalformedMessages="true"  
           logMessagesAtServiceLevel="true"   
           logMessagesAtTransportLevel="true"  
           maxMessagesToLog="3000"   
       />  
  </diagnostics>  
 </system.serviceModel>  
</configuration>  
```  
  
## <a name="using-wmi-to-modify-settings"></a>WMI를 사용하여 설정 수정  
 앞의 구성 예제와 같이 구성에서 `wmiProviderEnabled` 특성을 활성화하면 WMI를 사용하여 런타임에 구성 설정을 변경할 수 있습니다. 예를 들어 CIM Studio 내에서 WMI를 사용하여 런타임에 추적 소스 수준을 Warning에서 Information으로 변경할 수 있습니다. 이런 방식으로 라이브 디버깅을 사용하면 성능에 큰 영향을 줄 수 있습니다. WMI를 사용 하는 방법에 대 한 자세한 내용은 [진단에 WMI(Windows Management Instrumentation) 사용](../../../../../docs/framework/wcf/diagnostics/wmi/index.md) 항목을 참조 하세요.  
  
## <a name="enable-correlated-events-in-aspnet-tracing"></a>ASP.NET 추적에서 상호 관련된 이벤트 사용  
 ASP.NET 이벤트 추적이 켜져 있지 않은 경우 ASP.NET 이벤트는 상관 관계 ID(ActivityID)를 설정하지 않습니다. 상호 관련 된 이벤트를 제대로 확인 하려면 **시작**, **실행** 으로 이동 하 여 **cmd**를 입력 하 여 호출할 수 있는 명령 콘솔에서 다음 명령을 사용 하 여 ASP.NET events 추적을 설정 해야 합니다.  
  
```console  
logman start mytrace -pf logman.providers -o test.etl –ets  
```  
  
 ASP.NET 이벤트 추적을 끄려면 다음 명령을 사용합니다.  
  
```console
logman stop mytrace -ets  
```  
  
## <a name="see-also"></a>참고자료

- [진단에 WMI(Windows Management Instrumentation) 사용](../../../../../docs/framework/wcf/diagnostics/wmi/index.md)
