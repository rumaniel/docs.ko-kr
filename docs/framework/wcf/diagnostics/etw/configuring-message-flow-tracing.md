---
title: 메시지 흐름 추적 구성
ms.date: 03/30/2017
ms.assetid: 15571ca2-bee2-47fb-ba10-fcbc09152ad0
ms.openlocfilehash: b01a06a50fbb5962fe87c3426957b3294b1bf3ab
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917926"
---
# <a name="configuring-message-flow-tracing"></a>메시지 흐름 추적 구성
WCF (Windows Communication Foundation) 활동 추적을 사용 하도록 설정 하면 WCF 스택의 논리적 활동에 종단 간 활동 Id가 할당 됩니다. [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)]에는 메시지 흐름 추적이라고 하는 ETW(Event Tracing for Windows)와 함께 작동하는 이 기능의 더 높은 성능 버전이 있습니다. 이 기능을 사용하도록 설정하면 엔드투엔드 작업 ID가 들어오는 메시지에서 가져와 지고(비어 있는 경우 들어오는 메시지에 할당됨) 메시지가 채널을 통해 디코딩된 후 내보내지는 모든 추적 이벤트에 전파됩니다. 이 기능을 사용하면 다른 서비스의 추적 로그를 사용하여 메시지 흐름을 다시 생성할 수 있습니다.  
  
 추적은 애플리케이션에서 문제가 발견되면 사용하도록 설정했다가 문제가 해결되면 사용하지 않도록 설정할 수 있습니다.  
  
## <a name="enabling-tracing"></a>추적 사용  
 다음 예제와 같이 .NET Framework 4 `messageFlowTracing` 구성 요소를 `true`로 설정하여 메시지 흐름 추적을 사용하도록 설정할 수 있습니다.  
  
```xml  
<system.servicemodel>  
  <diagnostics>  
    <endToEndTracing propagateActivity="true" messageFlowTracing="true" />  
  </diagnostics>  
</system.servicemodel>  
```  
  
> [!NOTE]
> `endToEndTracing` 구성 요소는 Web.config 파일에 있기 때문에 ETW와 동일한 방식으로 동적으로 구성할 수 없습니다. `endToEndTracing` 구성 요소를 적용하려면 애플리케이션을 재활용해야 합니다.  
  
 작업은 작업 ID라는 식별자의 교환을 통해 상호 연결됩니다. 이 식별자는 GUID이며 System.Diagnostics.CorrelationManager 클래스에서 생성됩니다. System.Diagnostics.Trace.CorrelationManager.ActivityID를 조작하는 경우 실행 제어가 WCF 코드로 다시 전달될 때 값이 원래대로 설정되는지 확인합니다.  또한 비동기 WCF 프로그래밍 모델을 사용하는 경우 System.Diagnostics.Trace.CorrelationManager.ActivityID가 스레드 간에 전달되는지 확인합니다.  
  
## <a name="message-flow-tracing-and-rest-services"></a>메시지 흐름 추적 및 REST 서비스  
 메시지 흐름 추적을 사용해서 종단 간 요청을 추적할 수 있습니다.  SOAP 기반 서비스에서는 작업 ID가 SOAP 메시지 헤더로 전송됩니다. REST 요청에는 이 헤더가 포함되지 않으므로 특별한 HTTP 이벤트 헤더가 대신 사용됩니다. 다음 코드 조각에서는 작업 ID 값을 자동으로 검색하는 방법을 보여 줍니다.  
  
```csharp
Object output = null;
if (OperationContext.Current.IncomingMessageProperties.TryGetValue(HttpRequestMessageProperty.Name, out output))
{
   HttpRequestMessageProperty httpHeaders = output as HttpRequestMessageProperty;
   // Retrieve the Activity Id from the HTTP header    string e2eId = httpHeaders.Headers["E2EActivity"];
   // ...
}
```

 다음 코드를 사용해서 헤더를 프로그래밍 방식으로 추가할 수 있습니다.  
  
```csharp  
HttpContent content = new StreamContent(contentStream);  
Guid correlation = Guid.NewGuid();  
content.Headers.Add("E2EActivity", Convert.ToBase64String(correlation.ToByteArray()));  
```
