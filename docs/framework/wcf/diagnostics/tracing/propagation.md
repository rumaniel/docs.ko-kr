---
title: 전파
ms.date: 03/30/2017
ms.assetid: f8181e75-d693-48d1-b333-a776ad3b382a
ms.openlocfilehash: 1d5ac743e94edd845650a1b550b3e982929d1b32
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198252"
---
# <a name="propagation"></a>전파
Windows Communication Foundation (WCF) 추적 모델의 동작 전파에 설명 합니다.  
  
## <a name="using-propagation-to-correlate-activities-across-endpoints"></a>전파를 통해 엔드포인트 내의 동작 상호 연결  
 전파는 사용자에게 응용 프로그램 엔드포인트를 통해 동일한 처리 단위(예: 요청)에 대한 오류 추적의 직접적인 상관 관계를 제공합니다. 동일한 처리 단위에 대해 다른 엔드포인트에서 내보내진 오류는 응용 프로그램 도메인에서도 동일한 동작에서 그룹화됩니다. 이는 메시지 헤더에서 동작 ID의 전파를 통해 수행됩니다. 그러므로 서버의 내부 오류로 인해 클라이언트의 시간이 초과되면 두 오류 모두 직접 상관 관계에 대해 동일한 동작에서 표시됩니다.  
  
 이 작업을 수행하려면 앞의 예제에서 설명한 대로 `ActivityTracing` 설정을 사용하세요. 또한 모든 엔드포인트에서 `propagateActivity` 추적 소스에 대해 `System.ServiceModel` 특성을 설정하세요.  
  
```xml  
<source name="System.ServiceModel" switchValue="Verbose,ActivityTracing" propagateActivity="true" >  
```  
  
 동작 전파는 TLS에 동작 ID를 포함 하는 WCF 아웃 바운드 메시지에 헤더를 추가 하는 기능을 구성할 수 있습니다. 서버측에서 이후의 추적에 이를 포함함으로써 클라이언트 및 서버 동작을 상호 연결할 수 있습니다.  
  
## <a name="propagation-definition"></a>전파 정의  
 다음 조건이 모두 충족되면 동작 M의 gAId가 동작 N에 전파됩니다.  
  
-   N은 M으로 인해 만들어집니다.  
  
-   M의 gAId가 N에 알려집니다.  
  
-   N의 gAId가 M의 gAId와 같습니다.  
  
 다음 XML 스키마에 설명된 것처럼 gAId는 ActivityId 메시지 헤더를 통해 전파됩니다.  
  
```xml  
<xsd:element name="ActivityId" type="integer" minOccurs="0">  
  <xsd:attribute name="CorrelationId" type="integer" minOccurs="0"/>  
</xsd:element>  
```  
  
 다음은 메시지 헤더의 예제입니다.  
  
```xml  
<MessageLogTraceRecord>  
  <s:Envelope xmlns:s="http://www.w3.org/2003/05/soap-envelope"
                      xmlns:a="http://www.w3.org/2005/08/addressing">  
    <s:Header>  
      <a:Action s:mustUnderstand="1">http://Microsoft.ServiceModel.Samples/ICalculator/Subtract  
      </a:Action>  
      <a:MessageID>urn:uuid:f0091eae-d339-4c7e-9408-ece34602f1ce  
      </a:MessageID>  
      <ActivityId CorrelationId="f94c6af1-7d5d-4295-b693-4670a8a0ce34"
               xmlns="http://schemas.microsoft.com/2004/09/ServiceModel/Diagnostics">  
        17f59a29-b435-4a15-bf7b-642ffc40eac8  
      </ActivityId>  
      <a:ReplyTo>  
          <a:Address>http://www.w3.org/2005/08/addressing/anonymous</a:Address>  
      </a:ReplyTo>  
      <a:To s:mustUnderstand="1">net.tcp://localhost/servicemodelsamples/service</a:To>  
   </s:Header>  
   <s:Body>  
     <Subtract xmlns="http://Microsoft.ServiceModel.Samples">  
       <n1>145</n1>  
       <n2>76.54</n2>  
     </Subtract>  
   </s:Body>  
  </s:Envelope>  
</MessageLogTraceRecord>  
```  
  
## <a name="propagation-and-activity-boundaries"></a>전파 및 동작 경계  
 동작 ID가 엔드포인트를 통해 전파되는 경우 메시지 수신자는 해당(전파된) 동작 ID를 사용하여 Start 및 Stop 추적을 내보냅니다. 따라서 각 추적 소스의 해당 gAId를 가진 Start 및 Stop 추적이 있습니다. 엔드포인트가 동일한 프로세스에 있고 동일한 추적 소스 이름을 사용하는 경우 동일한 lAId(동일한 gAId, 동일한 추적 소스, 동일한 프로세스)를 가진 여러 Start 및 Stop 추적이 만들어집니다.  
  
## <a name="synchronization"></a>동기화  
 서로 다른 컴퓨터에서 실행되는 엔드포인트에서 이벤트를 동기화하기 위해 CorrelationId가 메시지에 전파되는 ActivityId 헤더에 추가됩니다. 도구에서 이 ID를 사용하여 클럭이 일치하지 않는 시스템 간의 이벤트를 동기화할 수 있습니다. 특히 Service Trace Viewer 도구는 이 ID를 사용하여 엔드포인트 간의 메시지 흐름을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 구성](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)  
 [Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)  
 [종단 간 추적 시나리오](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)  
 [Service Trace Viewer 도구(SvcTraceViewer.exe)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)
