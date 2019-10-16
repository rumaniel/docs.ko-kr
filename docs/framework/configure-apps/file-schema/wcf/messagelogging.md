---
title: <messageLogging>
ms.date: 03/30/2017
ms.assetid: 1d06a7e6-9633-4a12-8c5d-123adbbc19c5
ms.openlocfilehash: 9291c38af28c18d20e23e34e8316b4a9fe523123
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855128"
---
# <a name="messagelogging"></a>\<messageLogging>
이 요소는 WCF(Windows Communication Foundation)의 메시지 로깅 기능 설정을 정의합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<진단 >** ](diagnostics.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<messageLogging >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>
  <diagnostics>
    <messageLogging logEntireMessage="Boolean"
                    logMalformedMessages="Boolean"
                    logMessagesAtServiceLevel="Boolean"
                    logMessagesAtTransportLevel="Boolean"
                    maxMessagesToLog="Integer"
                    maxSizeOfMessageToLog="Integer">
      <filters>
        <clear />
      </filters>
    </messageLogging>
  </diagnostics>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|`logEntireMessage`|전체 메시지(메시지 헤더 및 본문)를 로깅할지 여부를 지정하는 부울 값입니다. 기본값은 `false`로, 메시지 헤더만 로깅됩니다. 이 설정은 모든 메시지 로깅 수준(서비스, 전송 및 잘못된 형식)에 영향을 줍니다.|  
|`logMalformedMessages`|잘못된 형식의 메시지를 로깅할지 여부를 지정하는 부울 값입니다. 잘못된 형식의 메시지는 `maxMessagesToLog`에 포함되지 않습니다. 기본값은 `false`입니다.|  
|`logMessagesAtServiceLevel`|암호화 및 전송 관련 변형 전에 메시지를 서비스 수준에서 추적할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.|  
|`logMessagesAtTransportLevel`|전송 수준에서 메시지를 추적하는지 여부를 지정하는 부울 값입니다. 구성 파일에 지정된 모든 필터가 적용되며, 필터와 일치하는 메시지만 추적됩니다. 기본값은 `false`입니다.|  
|`maxMessagesToLog`|로깅할 최대 메시지 수를 지정하는 양의 정수입니다. 기본값은 1000입니다.|  
|`maxSizeOfMessageToLog`|로깅할 최대 메시지 크기(바이트)를 지정하는 양의 정수입니다. 이 한도를 초과하는 메시지는 로깅되지 않습니다. 이 설정은 모든 추적 수준에 영향을 줍니다. 기본값은 262144(0x4000)입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|필터|`filters` 요소는 XPath 필터 컬렉션을 보유합니다. `logMessagesAtTransportLevel`이 `true`로 설정되어 전송 메시지 로깅을 사용할 경우 필터와 일치하는 메시지만 로깅됩니다.<br /><br /> 필터는 전송 레이어에서만 적용됩니다. 서비스 수준 및 잘못된 형식의 메시지 로깅은 필터의 영향을 받지 않습니다.<br /><br /> 이 요소의 유일한 특성인 `filter`는 XpathFilter입니다.<br /><br /> `<filters>     <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">/soap:Envelope</add> </filters>`|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|진단|관리자의 런타임 검사 및 제어를 위한 WCF 설정을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 메시지는 스택에서 서비스, 전송 및 잘못된 형식의 3가지 다른 수준에서 로깅됩니다. 각 수준은 별도로 활성화될 수 있습니다.  
  
 XPath 필터를 추가하여 전송 및 서비스 수준에서 특정 메시지를 로깅할 수 있습니다. 정의된 필터가 없으면 모든 메시지가 로깅됩니다. 필터는 메시지의 헤더에만 적용됩니다. 본문은 무시됩니다. WCF는 성능 향상을 위해 메시지 본문을 무시합니다. 본문의 내용을 기반으로 필터링하려면 해당 작업을 수행하는 필터를 갖춘 사용자 지정 수신기를 만듭니다.  
  
 메시지 추적을 활성화하려면 추적 수신기를 만들어야 합니다. 수신기는 <xref:System.Diagnostics> 추적 아키텍처에서 작동하는 수신기일 수 있습니다. 다음 예에서는 이러한 수신기를 만드는 방법을 보여 줍니다.  
  
```xml  
<system.diagnostics>
  <sources>
    <source name="System.ServiceModel"
            switchValue="Verbose">
      <listeners>
        <clear />
        <add type="System.Diagnostics.DefaultTraceListener"
             name="Default"
             traceOutputOptions="None" />
        <add name="ServiceModel Listener"
             traceOutputOptions="None" />
      </listeners>
    </source>
    <source name="System.ServiceModel.MessageLogging">
      <listeners>
        <clear />
        <add type="System.Diagnostics.DefaultTraceListener"
             name="Default"
             traceOutputOptions="None" />
        <add name="MessageLogging Listener"
             traceOutputOptions="None" />
      </listeners>
    </source>
  </sources>
  <sharedListeners>
    <add initializeData="C:\ItProTools\TraceLog.xml"
         type="System.Diagnostics.XmlWriterTraceListener, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
         name="ServiceModel Listener"
         traceOutputOptions="LogicalOperationStack, DateTime, Timestamp, ProcessId, ThreadId, Callstack" />
    <add initializeData="C:\ItProTools\MessageLog.log"
         type="System.Diagnostics.XmlWriterTraceListener, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
         name="MessageLogging Listener"
         traceOutputOptions="LogicalOperationStack, DateTime, Timestamp, ProcessId, ThreadId, Callstack" />
  </sharedListeners>
</system.diagnostics>
```  
  
## <a name="example"></a>예제  
  
```xml  
<messageLogging logEntireMessage="true"
                logMalformedMessages="true"
                logMessagesAtServiceLevel="true"
                logMessagesAtTransportLevel="true"
                maxMessagesToLog="42"
                maxSizeOfMessageToLog="42">
  <filters>
    <clear />
  </filters>
</messageLogging>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
- <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement>
- [메시지 로깅 구성](../../../wcf/diagnostics/configuring-message-logging.md)
