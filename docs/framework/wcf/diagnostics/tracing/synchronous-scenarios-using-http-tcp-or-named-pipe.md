---
title: HTTP, TCP 또는 명명된 파이프를 사용하는 동기 시나리오
ms.date: 03/30/2017
ms.assetid: 7e90af1b-f8f6-41b9-a63a-8490ada502b1
ms.openlocfilehash: 28e612b190f4993e1ce7da0d1083c4e55f827d4a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61784862"
---
# <a name="synchronous-scenarios-using-http-tcp-or-named-pipe"></a>HTTP, TCP 또는 명명된 파이프를 사용하는 동기 시나리오
이 항목에서는 HTTP, TCP 또는 명명된 파이프를 사용하는 단일 스레드 클라이언트가 포함된 다양한 동기 요청/회신 시나리오의 작업 및 전송에 대해 설명합니다. 참조 [HTTP, TCP 또는 명명 된 파이프를 사용 하 여 비동기 시나리오](../../../../../docs/framework/wcf/diagnostics/tracing/asynchronous-scenarios-using-http-tcp-or-named-pipe.md) 다중 스레드 요청에 대 한 자세한 내용은 합니다.  
  
## <a name="synchronous-requestreply-without-errors"></a>오류가 없는 동기 요청/회신  
 이 단원에서는 단일 스레드 클라이언트에서의 유효한 동기 요청/회신 시나리오 작업 및 전송에 대해 설명합니다.  
  
### <a name="client"></a>클라이언트  
  
#### <a name="establishing-communication-with-service-endpoint"></a>서비스 엔드포인트와의 통신 설정  
 클라이언트가 구성되고 열립니다. 이러한 단계 각각에 대 한 앰비언트 동작 (A)으로 전송 됩니다 "Construct Client" (B)과 "Open Client" (C) 작업을 각각. 전송 중인 각 동작에서 앰비언트 동작은 다시 전송될 때까지, 즉 ServiceModel 코드가 실행될 때까지 일시 중단됩니다.  
  
#### <a name="making-a-request-to-service-endpoint"></a>서비스 엔드포인트에 요청하기  
 앰비언트 동작 (D) "ProcessAction" 동작으로 전송 됩니다. 이 동작 내에서 요청 메시지가 전송되고 응답 메시지가 수신됩니다. 이 동작은 컨트롤이 사용자 코드로 반환되면 종료됩니다. 이것은 동기 요청이므로 컨트롤이 반환될 때까지 앰비언트 동작이 일시 중단됩니다.  
  
#### <a name="closing-communication-with-service-endpoint"></a>서비스 엔드포인트와의 통신 닫기  
 클라이언트의 닫기 동작(I)은 앰비언트 동작에서 만들어집니다. 이 동작은 새로 만들기 및 열기와 동일합니다.  
  
### <a name="server"></a>서버  
  
#### <a name="setting-up-a-service-host"></a>서비스 호스트 설정  
 ServiceHost의 새로 만들기 및 열기 동작(N 및 O)은 앰비언트 동작(M)에서 만들어집니다.  
  
 수신기 동작(P)은 각 수신기의 ServiceHost를 열면 만들어집니다. 수신기 동작은 데이터를 받고 처리할 때까지 기다립니다.  
  
#### <a name="receiving-data-on-the-wire"></a>통신 중에 데이터 받기  
 데이터 통신 중에 도착 하면 수신된 된 데이터를 처리 하는 데 사용 되는 (Q) 아직 존재 하지 않는 경우 "ReceiveBytes" 동작이 만들어집니다. 이 동작은 연결 또는 큐 내의 여러 메시지에 다시 사용할 수 있습니다.  
  
 ReceiveBytes 동작은 SOAP 동작 메시지를 구성할 데이터가 충분하면 ProcessMessage 동작(R)을 시작합니다.  
  
 동작 R에서 메시지 헤더가 처리되고 activityID 헤더가 확인됩니다. 이 헤더가 있는 경우 동작 ID는 ProcessAction 동작으로 설정되고 그렇지 않으면, 새 ID가 만들어집니다.  
  
 ProcessAction 동작(S)이 만들어지고 호출이 처리되면 전송됩니다. 이 동작은 사용자 코드(T) 실행 및 가능한 경우 응답 메시지 보내기를 비롯하여 들어오는 메시지와 관련된 모든 처리가 완료되면 종료됩니다.  
  
#### <a name="closing-a-service-host"></a>서비스 호스트 닫기  
 ServiceHost의 닫기 동작(Z)은 앰비언트 동작에서 만들어집니다.  
  
 ![동기 시나리오를 보여 주는 다이어그램. HTTP, TCP 또는 명명 된 파이프 합니다.](./media/synchronous-scenarios-using-http-tcp-or-named-pipe/synchronous-scenario-http-tcp-named-pipes.gif)  
  
 \<A m >을 `A` 이전 텍스트에서 및 표 3에에서 동작을 설명 하는 바로 가기 기호입니다. `Name`은 동작의 약식 이름입니다.  
  
 하는 경우 `propagateActivity` = `true`, Process Action 클라이언트와 서비스 모두에서 동일한 작업 ID가  
  
## <a name="synchronous-requestreply-with-errors"></a>오류가 있는 동기 요청/회신  
 이전 시나리오와 유일하게 다른 점은 SOAP 오류 메시지가 응답 메시지로 반환된다는 것입니다. 하는 경우 `propagateActivity` = `true`, 요청 메시지의 활동 ID가 SOAP 오류 메시지에 추가 합니다.  
  
## <a name="synchronous-one-way-without-errors"></a>오류가 없는 동기 단방향  
 첫 번째 시나리오와 유일하게 다른 점은 메시지가 서버로 반환되지 않는다는 것입니다. HTTP 기반 프로토콜의 경우 상태(유효 또는 오류)가 클라이언트로 반환됩니다. HTTP는 WCF 프로토콜 스택의 일부인 요청-응답 의미 있는 유일한 프로토콜 때문입니다. TCP 처리는 WCF에서 숨겨지는 것 이므로 승인은 클라이언트로 전송 됩니다.  
  
## <a name="synchronous-one-way-with-errors"></a>오류가 있는 동기 단방향  
 메시지(Q 이상)를 처리하는 동안 오류가 발생하는 경우 클라이언트에게 확인 메시지가 반환되지 않습니다. 이 시나리오는 "오류가 없는 동기 단방향" 시나리오와 동일합니다. 오류 메시지를 받으려면 단방향 시나리오를 사용하지 마십시오.  
  
## <a name="duplex"></a>이중  
 이전 시나리오와 다른 점은 클라이언트가 서비스 역할을 한다는 것입니다. 여기서는 비동기 시나리오와 비슷한 ReceiveBytes 및 ProcessMessage 동작을 만듭니다.
