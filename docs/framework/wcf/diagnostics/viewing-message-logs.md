---
title: 메시지 로그 보기
ms.date: 03/30/2017
ms.assetid: 3012fa13-f650-45fb-aaea-c5cca8c7d372
ms.openlocfilehash: 5d007efc9667ee5380b69349d6a960554ab0d4fe
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199788"
---
# <a name="viewing-message-logs"></a>메시지 로그 보기
이 항목에서는 메시지 로그를 볼 수 있는 방법에 대해 설명합니다.  
  
## <a name="viewing-message-logs-in-the-service-trace-viewer"></a>Service Trace Viewer에서 메시지 로그 보기  
 WCF에 의해 처리 되는 동안 메시지를 변환 됩니다. 그러므로 기록되는 메시지는 기록되는 시점의 메시지 내용만을 반영하며, 통신 중의 내용은 반영하지 않습니다.  
  
 메시지 로깅 출력은 메시지 전송 형식과 관계가 없으므로 메시지 로깅은 항상 디코딩된 메시지를 출력합니다. 메시지 로깅을 올바로 구성한 경우 메시지는 일반 텍스트로 기록되어야 합니다. 예를 들어 기록된 메시지 형식(일반 텍스트)은 이진 메시지 인코더 사용에 영향을 받지 않습니다.  
  
 XmlWriterTraceListener의 출력은 XML 단편의 시퀀스가 포함된 파일입니다. 해당 파일은 유효한 XML 파일이 아님을 알아야 합니다. 사용 하는 것이 좋습니다.는 [Service Trace Viewer 도구 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 메시지 로그 파일을 볼 수 있습니다. 이 도구를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [상관 관계가 지정 된 추적 보기 및 문제 해결에 대 한 Service Trace Viewer를 사용 하 여](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)입니다.  
  
 Service Trace Viewer에서 메시지에 나열 되는 **메시지** 탭 합니다. 처리 오류를 야기하거나 이와 관련된 메시지는 오류의 심각도에 따라 노란색(경고 수준)이나 빨간색(오류 수준)으로 강조 표시됩니다. 해당 메시지를 두 번 클릭하면 처리 요청에 따라 메시지 추적이 표시됩니다.  
  
> [!NOTE]
>  메시지에 헤더가 없으면 `<header/>` 태그가 기록되지 않습니다.  
  
## <a name="viewing-messages-logged-by-a-client-a-relay-and-a-service"></a>클라이언트, 릴레이 및 서비스에 의해 기록된 메시지 보기  
 사용자 환경에는 메시지를 릴레이로 보내고, 이후에 해당 메시지를 서비스로 전달하는 클라이언트가 포함될 수 있습니다. 메시지 로깅이 세 위치에 모두에서 모든 세 개의 메시지 로그에서 볼 수 시점과 [Service Trace Viewer 도구 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 동시에 메시지 로그 교환이 잘못 렌더링 됩니다. 이는 메시지 헤더의 `CorrelationId` 및 `ActivityId`가 모든 전송-수신 쌍에 대해 고유하지 않기 때문입니다.  
  
 다음 방법 중 하나를 사용하여 이 문제를 해결할 수 있습니다.  
  
-   세 개의 메시지 로그 중 두 가지 보기만 합니다 [Service Trace Viewer 도구 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 언제 든 지 합니다.  
  
-   세 로그 모두 보아야 한다면 합니다 [Service Trace Viewer 도구 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 동시에, 새 릴레이 서비스를 수정할 수 있습니다 <xref:System.ServiceModel.Channels.Message> 인스턴스. 이 인스턴스는 들어오는 메시지 본문의 복사본이어야 하며, `ActivityId` 및 `Action` 헤더를 제외한 모든 헤더여야 합니다. 다음 예제 코드에서는 이 작업을 수행하는 방법에 대해 보여 줍니다.  
  
```csharp
Message outgoingMessage = Message.CreateMessage(incomingMessage.Version, incomingMessage.Headers.Action, incomingMessage.GetReaderAtBodyContents());  
  
for (int i = 0; i < incomingMessage.Headers.Count; i++)  
{  
   if (incomingMessage.Headers[i].Name.Equals("ActivityId", StringComparison.InvariantCultureIgnoreCase) ||  
incomingMessage.Headers[i].Name.Equals("Action", StringComparison.InvariantCultureIgnoreCase))  
   {  
      continue;  
    }  
    outgoingMessage.Headers.CopyHeaderFrom(incomingMessage, i);  
}  
```  
  
## <a name="exceptional-cases-for-inaccurate-message-logging-content"></a>부정확한 메시지 로깅 콘텐츠의 예외 사례  
 다음 조건에서는 기록되는 메시지가 통신상에 표시되는 8진수 스트림의 정확한 표현이 아닐 수 있습니다.  
  
-   BasicHttpBinding의 경우에는 들어오는 메시지에 대해 봉투 헤더가 /addressing/none 네임스페이스에 기록됩니다.  
  
-   공백이 일치 하지 않는 수 있습니다.  
  
-   들어오는 메시지의 경우 빈 요소가 다르게 표시될 수 있습니다. 예를 들어 \<태그 >\<태그 > 대신 \<태그 / >  
  
-   알려진 PII 로깅이 기본값 또는 명시적인 설정인 enableLoggingKnownPii="true"에 의해서 사용하지 않도록 설정되었습니다.  
  
-   UTF-8로 변환하기 위해 인코딩을 사용하도록 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Service Trace Viewer 도구(SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)  
 [Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)  
 [메시지 로깅](../../../../docs/framework/wcf/diagnostics/message-logging.md)
