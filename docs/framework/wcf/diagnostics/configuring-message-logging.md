---
title: 메시지 로깅 구성
ms.date: 03/30/2017
helpviewer_keywords:
- message logging [WCF]
ms.assetid: 0ff4c857-8f09-4b85-9dc0-89084706e4c9
ms.openlocfilehash: db538634dccf22fb954ccf0827909e5cf3563f77
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798167"
---
# <a name="configuring-message-logging"></a>메시지 로깅 구성

이 항목에서는 다양한 시나리오에서 메시지 로깅을 구성하는 방법에 대해 설명합니다.

## <a name="enabling-message-logging"></a>메시지 로깅 활성화

WCF (Windows Communication Foundation)는 기본적으로 메시지를 기록 하지 않습니다. 메시지 로깅을 활성화하려면 추적 수신기를 `System.ServiceModel.MessageLogging` 추적 소스에 추가하고 구성 파일에서 `<messagelogging>` 요소의 특성을 설정해야 합니다.

다음 예제에서는 로깅을 활성화하고 추가 옵션을 지정하는 방법을 보여 줍니다.

```xml
<system.diagnostics>
  <sources>
    <source name="System.ServiceModel.MessageLogging">
      <listeners>
         <add name="messages"
              type="System.Diagnostics.XmlWriterTraceListener"
              initializeData="c:\logs\messages.svclog" />
        </listeners>
    </source>
  </sources>
</system.diagnostics>

<system.serviceModel>
  <diagnostics>
    <messageLogging
         logEntireMessage="true"
         logMalformedMessages="false"
         logMessagesAtServiceLevel="true"
         logMessagesAtTransportLevel="false"
         maxMessagesToLog="3000"
         maxSizeOfMessageToLog="2000"/>
  </diagnostics>
</system.serviceModel>
```

메시지 로깅 설정에 대 한 자세한 내용은 [추적 및 메시지 로깅에 권장 되는 설정](./tracing/recommended-settings-for-tracing-and-message-logging.md)을 참조 하세요.

`add`를 사용하여 사용할 수신기의 이름과 형식을 지정할 수 있습니다. 예제 구성에서는 수신기 이름을 "messages"로 지정하고 표준 .NET Framework 추적 수신기(`System.Diagnostics.XmlWriterTraceListener`)를 사용할 형식으로 추가합니다. `System.Diagnostics.XmlWriterTraceListener`를 사용하려면 출력 파일의 위치와 이름을 구성 파일에 지정해야 합니다. 이 작업을 수행하려면 `initializeData`를 로그 파일의 이름으로 설정합니다. 그렇지 않으면 시스템에서 예외가 throw됩니다. 로그를 기본 파일에 내보내는 사용자 지정 수신기를 구현할 수도 있습니다.

> [!NOTE]
> 메시지 로깅 시 디스크 공간에 액세스하므로 특정 서비스에 대해 디스크에 기록되는 메시지 수를 제한해야 합니다. 메시지 제한에 도달하면 정보 수준의 추적이 생성되고 모든 메시지 로깅 동작이 중지됩니다.

로깅 수준 및 추가 옵션에 대한 자세한 내용은 로깅 수준 및 옵션 단원에서 설명합니다.

`switchValue`의 `source` 특성은 추적용으로만 사용할 수 있습니다. 다음과 같이 `switchValue`에 `System.ServiceModel.MessageLogging` 특성을 지정해도 아무런 효과가 없습니다.

```xml
<source name="System.ServiceModel.MessageLogging" switchValue="Verbose">
```

추적 소스를 비활성화하려면 대신에 `logMessagesAtServiceLevel` 요소의 `logMalformedMessages`, `logMessagesAtTransportLevel` 및 `messageLogging` 특성을 사용하고, 이러한 모든 특성을 `false`로 설정해야 합니다. 이 작업은 구성 편집기 UI 인터페이스나 WMI를 통해 이전 코드 예제의 구성 파일을 사용하여 수행할 수 있습니다. 구성 편집기 도구에 대 한 자세한 내용은 [구성 편집기 도구 (SvcConfigEditor)](../configuration-editor-tool-svcconfigeditor-exe.md)를 참조 하세요. WMI에 대 한 자세한 내용은 [진단에 WMI(Windows Management Instrumentation) 사용](./wmi/index.md)을 참조 하세요.

## <a name="logging-levels-and-options"></a>로깅 수준 및 옵션

들어오는 메시지의 경우 로깅은 메시지가 형성된 직후, 메시지가 서비스 수준에서 사용자 코드에 도달하기 직전 그리고 잘못된 형식의 메시지가 감지될 때 발생합니다.

나가는 메시지의 경우 로깅은 메시지가 사용자 코드를 벗어난 직후 및 메시지가 송신되기 직전에 발생합니다.

WCF는 서비스와 전송 이라는 두 가지 수준에서 메시지를 기록 합니다. 잘못된 형식의 메시지도 기록됩니다. 이 세 가지 범주는 서로 연관이 없으며 구성에서 별도로 활성화할 수 있습니다.

로깅 수준은 `logMessagesAtServiceLevel` 요소의 `logMalformedMessages`, `logMessagesAtTransportLevel` 및 `messageLogging` 특성을 설정하여 제어할 수 있습니다.

### <a name="service-level"></a>서비스 수준

이 계층에서 기록되는 메시지는 수신 시와 송신 시에 각각 사용자 코드를 가져오거나 남기게 됩니다. 필터가 정의된 경우에는 해당 필터에 맞는 메시지만 기록되며 그 이외에는 서비스 수준의 모든 메시지가 기록됩니다. 신뢰할 수 있는 메시징 메시지를 제외한 인프라 메시지(트랜잭션, 피어 채널 및 보안)도 이 수준에서 기록됩니다. 스트리밍된 메시지의 경우는 헤더만 기록됩니다. 또한 이 수준에서 해독된 보안 메시지도 기록됩니다.

### <a name="transport-level"></a>전송 수준

이 계층에서 기록된 메시지는 통신 전송 동안 또는 그 이후에 인코딩이나 디코딩할 수 있습니다. 필터가 정의된 경우에는 해당 필터에 맞는 메시지만 기록되며 그 이외에는 전송 계층의 모든 메시지가 기록됩니다. 신뢰할 수 있는 메시징 메시지를 포함한 모든 인프라 메시지도 이 계층에서 기록됩니다. 스트리밍된 메시지의 경우는 헤더만 기록됩니다. 또한 보안 메시지는 이 수준에서 암호화된 채로 기록되는데 HTTPS와 같은 보안 전송이 사용되는 경우는 예외입니다.

### <a name="malformed-level"></a>잘못된 형식의 수준

형식이 잘못 된 메시지는 처리 단계에서 WCF 스택에 의해 거부 되는 메시지입니다. 이러한 잘못된 형식의 메시지는 암호화된 상태라면 암호화된 상태로, 적절하지 않은 XML로 된 상태라면 그 상태 그대로 기록됩니다. `maxSizeOfMessageToLog`는 CDATA로 기록될 메시지 크기를 정의합니다. 기본적으로 `maxSizeOfMessageToLog`는256K입니다. 이 특성에 대 한 자세한 내용은 다른 옵션 섹션을 참조 하세요.

### <a name="other-options"></a>기타 옵션

로깅 수준 이외에 다음과 같은 옵션을 지정할 수 있습니다.

- 전체 메시지 기록 (`logEntireMessage` 특성): 이 값은 전체 메시지 (메시지 헤더 및 본문)가 기록 되는지 여부를 지정 합니다. 기본값은 `false`로, 메시지 헤더만 기록됩니다. 이 설정은 서비스 및 전송 메시지 로깅 수준에 영향을 줍니다.

- 로깅할 최대 메시지 수 (`maxMessagesToLog` 특성): 이 값은 로깅할 최대 메시지 수를 지정 합니다. 모든 메시지(서비스, 전송 및 잘못된 형식의 메시지)가 이 할당량에 계산됩니다. 할당량에 도달하면 추적을 내보내고 추가 메시지는 기록되지 않습니다. 기본값은 1만입니다.

- 로깅할 메시지의 최대 크기 (`maxSizeOfMessageToLog` 특성): 이 값은 로깅할 메시지의 최대 크기 (바이트)를 지정 합니다. 이 크기 제한을 초과하는 메시지는 기록되지 않으며 해당 메시지에 대해 아무런 동작이 수행되지 않습니다. 이 설정은 모든 추적 수준에 영향을 줍니다. ServiceModel 추적을 사용하도록 설정된 경우, 경고 수준 추적을 첫 번째 로깅 지점(ServiceModelSend* 또는 TransportReceive)에서 내보내어 사용자에게 통보합니다. 서비스 수준 및 전송 수준 메시지의 기본값은 256K며 잘못된 형식의 메시지에 대한 기본값은 4K입니다.

  > [!CAUTION]
  > `maxSizeOfMessageToLog`와 비교하기 위해 계산되는 메시지 크기는 serialization 이전의 메모리에 있는 메시지 크기로, 이 크기는 기록되는 메시지 문자열의 실제 길이와 다를 수 있으며 대부분의 경우 실제 크기보다 더 큽니다. 따라서 메시지가 기록되지 않을 수 있으므로 이를 감안하여`maxSizeOfMessageToLog` 특성을 필요한 메시지 크기보다 10% 더 크게 지정합니다. 또한 잘못된 형식의 메시지가 기록될 경우 메시지 로그에 사용되는 실제 디스크 공간은 `maxSizeOfMessageToLog`에 지정된 값의 최대 5배가 될 수 있습니다.

구성 파일에 추적 수신기가 정의되어 있지 않으면 지정된 로깅 수준과 관계없이 로깅 출력이 생성되지 않습니다.

이 단원에 설명된 특성과 같은 메시지 로깅 옵션은 WMI(Windows Management Instrumentation)를 사용하여 런타임에 변경할 수 있습니다. 이러한 부울 속성 `LogMessagesAtServiceLevel` `LogMessagesAtTransportLevel` 및 `LogMalformedMessages`를 노출하는 [AppDomainInfo](./wmi/appdomaininfo.md) 인스턴스에 액세스하여 이 작업을 수행할 수 있습니다. 따라서 메시지 로깅을 위한 추적 수신기를 구성하지만 이러한 옵션을 구성에서 `false`로 설정해도, 이후에 애플리케이션 실행 시 `true`로 변경할 수 있습니다. 이를 통해 메시지 로깅을 런타임에 효과적으로 활성화할 수 있습니다. 마찬가지로 구성 파일에 메시지 로깅을 활성화하더라도, WMI를 사용하여 런타임에 메시지 로깅을 비활성화할 수 있습니다. 자세한 내용은 [진단을 위한 WMI(Windows Management Instrumentation) 사용](./wmi/index.md)을 참조 하세요.

메시지 로그의 `source` 필드에서는 메시지가 기록되는 컨텍스트를 지정합니다. 즉, 요청 메시지를 보내거나 받을 때 요청-회신을 위한 것인지 단방향 요청인지, 그리고 위치가 서비스 모델 또는 전송 계층인지, 또는 잘못된 형식의 메시지인지 등을 지정합니다.

형식이 잘못 `source` 된 메시지의 경우는 `Malformed`와 같습니다. 그렇지 않으면 소스는 컨텍스트에 따라 다음 값을 사용합니다.

요청/회신의 경우

||요청 보내기|요청 받기|회신 보내기|회신 받기|
|-|------------------|---------------------|----------------|-------------------|
|서비스 모델 계층|서비스<br /><br /> Level<br /><br /> Send<br /><br /> 요청|서비스<br /><br /> Level<br /><br /> Receive<br /><br /> 요청|서비스<br /><br /> Level<br /><br /> Send<br /><br /> 회신|서비스<br /><br /> Level<br /><br /> Receive<br /><br /> 회신|
|전송 계층|전송<br /><br /> Send|전송<br /><br /> Receive|전송<br /><br /> Send|전송<br /><br /> Receive|

단방향 요청의 경우

||요청 보내기|요청 받기|
|-|------------------|---------------------|
|서비스 모델 계층|서비스<br /><br /> Level<br /><br /> Send<br /><br /> 데이터그램|서비스<br /><br /> Level<br /><br /> Receive<br /><br /> 데이터그램|
|전송 계층|전송<br /><br /> Send|전송<br /><br /> Receive|

## <a name="message-filters"></a>메시지 필터

메시지 필터는 `messageLogging` 구성 섹션의 `diagnostics` 구성 요소에서 정의됩니다. 이러한 메시지 필터는 서비스 및 전송 수준에서 적용됩니다. 하나 이상의 필터가 정의되면 그 중 최소한 하나의 필터와 일치하는 메시지만 로깅됩니다. 정의된 필터가 없으면 모든 메시지가 통과합니다.

필터는 모든 XPath 구문을 지원하며, 구성 파일에 표시되는 순서대로 적용됩니다. 필터 구문에 오류가 있으면 구성 예외가 발생합니다.

또한 필터에는 `nodeQuota` 특성을 사용하는 안전 기능이 있어, 필터에 맞게 검사할 수 있는 XPath DOM의 최대 노드 수를 제한합니다.

다음 예제에서는 SOAP 헤더 섹션이 있는 메시지만 기록하는 필터를 구성하는 방법을 보여 줍니다.

```xml
<messageLogging logEntireMessage="true"
    logMalformedMessages="true"
    logMessagesAtServiceLevel="true"
    logMessagesAtTransportLevel="true"
    maxMessagesToLog="420">
    <filters>
        <add nodeQuota="10" xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
                 /soap:Envelope/soap:Header
        </add>
     </filters>
</messageLogging>
```

메시지 본문에는 필터가 적용되지 않고, 메시지 본문을 조작하려는 필터는 필터 목록에서 제거됩니다. 이를 나타내는 이벤트도 내보내집니다. 예를 들어 다음과 같은 필터는 필터 테이블에서 제거됩니다.

```xml
<add xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">/s:Envelope/s:Body[contains(text(), "Hello")]</add>
```

## <a name="configuring-a-custom-listener"></a>사용자 지정 수신기 구성

추가 옵션이 있는 사용자 지정 수신기를 구성할 수도 있습니다. 사용자 지정 수신기는 메시지를 기록하기 전에 메시지에서 애플리케이션별 PII 요소를 필터링하는 데 유용합니다. 다음 예제에서는 사용자 지정 수신기 구성을 보여 줍니다.

```xml
<system.diagnostics>
   <sources>
     <source name="System.ServiceModel.MessageLogging">
           <listeners>
             <add name="MyListener"
                    type="YourCustomListener"
                    initializeData="c:\logs\messages.svclog"
                    maxDiskSpace="1000"/>
           </listeners>
     </source>
   </sources>
</system.diagnostics>
```

`type` 특성을 해당 형식의 정규화된 어셈블리 이름으로 설정해야 함에 유의합니다.

## <a name="see-also"></a>참고자료

- [\<messageLogging>](../../configure-apps/file-schema/wcf/messagelogging.md)
- [메시지 로깅](message-logging.md)
- [추적 및 메시지 로깅에 권장되는 설정](./tracing/recommended-settings-for-tracing-and-message-logging.md)
