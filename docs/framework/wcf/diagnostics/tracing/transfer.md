---
title: 전송
ms.date: 03/30/2017
ms.assetid: dfcfa36c-d3bb-44b4-aa15-1c922c6f73e6
ms.openlocfilehash: 360367803fc014c83ae377309b9029dafa3040bd
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50202896"
---
# <a name="transfer"></a>전송
이 항목에서는 Windows Communication Foundation (WCF) 동작 추적 모델에서 전송을 설명합니다.  
  
## <a name="transfer-definition"></a>전송 정의  
 동작 간 전송은 엔드포인트 내의 관련 동작에 있는 이벤트 간의 인과 관계를 나타냅니다. 두 가지 동작은 컨트롤이 이러한 동작 간에 이동할 때(예: 동작 경계를 넘나드는 메서드 호출) 전송과 관련됩니다. Wcf에서는 서비스에서 바이트가 들어올 때 Listen At 동작으로 전송 됩니다 바이트 수신 동작 메시지 개체가 만들어지는. 종단 간 추적 시나리오 및 해당 동작과 추적 디자인의 목록을 참조 하세요 [종단 간 추적 시나리오](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)합니다.  
  
 Transfer 추적을 내보내려면 다음 구성 코드와 같이 추적 소스에 `ActivityTracing` 설정을 사용합니다.  
  
```xml  
<source name="System.ServiceModel" switchValue="Verbose,ActivityTracing">  
```  
  
## <a name="using-transfer-to-correlate-activities-within-endpoints"></a>끝점 내에서 동작을 상호 연결하기 위해 전송 사용  
 동작 및 전송은 사용자가 오류의 근본 원인을 찾도록 도와줍니다. 예를 들어 동작 M과 N 간에 각각 구성 요소 M과 N에서 전송을 주고 받을 때 M으로 전송을 되돌린 직후에 N에서 충돌이 발생하면 M으로 보내는 N의 전달 데이터로 인해 오류가 발생했다고 결론을 내릴 수 있습니다.  
  
 M과 N 간에 컨트롤의 흐름이 있을 때 Transfer 추적이 동작 M으로부터 동작 N으로 내보내집니다. 예를 들어 동작의 경계를 넘나드는 메서드 호출로 인해 N은 M에 대한 일부 작업을 수행합니다. N이 이미 존재하거나 만들어졌을 수 있습니다. N이 M에 대한 일부 작업을 수행하는 새 동작일 경우 N이 M에 의해 생성됩니다.  
  
 M으로부터 N으로 전송되더라도 다시 N으로부터 M으로의 전송이 발생하지 않을 수도 있습니다. 이는 M이 N에서의 일부 작업을 생성할 수 있으며 N이 해당 작업을 완료할 때 추적하지 않기 때문입니다. 실제로, M은 N이 해당 작업을 완료하기 전에 종료될 수 있습니다. 이 수신기 동작 (N)를 생성 하 고 종료 "Open ServiceHost" 동작 (M)에서 발생 합니다. N에서 M으로 다시 전송한다는 것은 N이 M과 관련된 작업을 완료했음을 의미합니다.  
  
 N은 M과 연관되지 않은 다른 처리(예: 여러 로그인 동작으로부터 로그인 요청(M) 수신을 유지하는 기존 인증자 동작(N))를 계속 수행할 수 있습니다.  
  
 동작 M과 N 사이에 반드시 중첩된 관계가 존재하는 것은 아닙니다. 이는 두 가지 이유 때문일 수 있습니다. 첫 번째 이유는 동작 M이 N을 시작했더라도 M이 N에서 수행되는 실제 처리를 모니터링하지 않았기 때문이며, 두 번째 이유는 N이 이미 존재하기 때문입니다.  
  
## <a name="example-of-transfers"></a>전송 예제  
 다음은 두 가지 전송 예제입니다.  
  
-   서비스 호스트를 만들 때 생성자가 호출 코드로부터 컨트롤을 얻거나 호출 코드가 생성자에게 전송됩니다. 생성자는 실행을 마치면 컨트롤을 호출 코드로 반환하거나 호출 코드로 다시 전송합니다. 이는 중첩된 관계의 경우입니다.  
  
-   수신기가 전송 데이터 처리를 시작하면 새 스레드를 만들고, 처리를 위해 적절한 컨텍스트를 바이트 수신 동작(예: 컨트롤 및 데이터 전달)으로 전달합니다. 스레드가 요청 처리를 완료하면 바이트 수신 동작은 수신기로 아무 것도 전달하지 않습니다. 이 경우 새 스레드 동작 내에는 전송이 있지만 외부에는 전송이 없습니다. 두 개의 동작은 연관되지만 중첩되지는 않습니다.  
  
## <a name="activity-transfer-sequence"></a>동작 전송 시퀀스  
 올바른 형식의 동작 전송 시퀀스에는 다음 단계가 포함됩니다.  
  
1.  새 gAId 선택으로 구성된 새 동작 시작  
  
2.  현재 동작 ID로부터 새 gAId에 대한 Transfer 추적 내보내기  
  
3.  TLS에서 새 ID 설정  
  
4.  새 동작의 시작을 나타내기 위해 Start 추적 내보내기  
  
5.  원래 동작으로 돌아가기는 다음으로 구성됩니다.  
  
6.  원래 gAId로 Transfer 추적 내보내기  
  
7.  새 동작의 종료를 나타내기 위해 Stop 추적 내보내기  
  
8.  이전 gAId로 TLS 설정  
  
 다음 코드 예제에서는 이 작업을 수행하는 방법을 보여 줍니다. 이 샘플은 차단 호출이 새 동작으로 전송 중일 때 만들어지며, Suspend/Resume 추적을 포함한다고 가정합니다.  
  
```csharp
// 0. Create a trace source  
TraceSource ts = new TraceSource("myTS");  

// 1. remember existing ("ambient") activity for clean up  
Guid oldGuid = Trace.CorrelationManager.ActivityId;  
// this will be our new activity  
Guid newGuid = Guid.NewGuid();   

// 2. call transfer, indicating that we are switching to the new AID  
ts.TraceTransfer(667, "Transferring.", newGuid);  

// 3. Suspend the current activity.  
ts.TraceEvent(TraceEventType.Suspend, 667, "Suspend: Activity " + i-1);  

// 4. set the new AID in TLS  
Trace.CorrelationManager.ActivityId = newGuid;  

// 5. Emit the start trace  
ts.TraceEvent(TraceEventType.Start, 667, "Boundary: Activity " + i);  

// trace something  
ts.TraceEvent(TraceEventType.Information, 667, "Hello from activity " + i);  

// Perform Work  
// some work.  
// Return  
ts.TraceEvent(TraceEventType.Information, 667, "Work complete on activity " + i);   

// 6. Emit the transfer returning to the original activity  
ts.TraceTransfer(667, "Transferring Back.", oldGuid);  

// 7. Emit the End trace  
ts.TraceEvent(TraceEventType.Stop, 667, "Boundary: Activity " + i);  

// 8. Change the tls variable to the original AID  
Trace.CorrelationManager.ActivityId = oldGuid;    

// 9. Resume the old activity  
ts.TraceEvent(TraceEventType.Resume, 667, "Resume: Activity " + i-1);  
```  
  
## <a name="see-also"></a>참고 항목  
 [추적 구성](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)  
 [Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)  
 [종단 간 추적 시나리오](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)  
 [Service Trace Viewer 도구(SvcTraceViewer.exe)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)
