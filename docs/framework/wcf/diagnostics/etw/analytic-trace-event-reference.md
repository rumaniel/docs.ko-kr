---
title: 분석 추적 이벤트 참조
ms.date: 03/30/2017
helpviewer_keywords:
- analytic tracing [WCF]. reference
ms.assetid: e44540cf-44a1-4efc-b965-7fbfd2131d73
ms.openlocfilehash: 1b44e6b0abf0fc48b43ae17cbd24780e46ae518d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798120"
---
# <a name="analytic-trace-event-reference"></a>분석 추적 이벤트 참조
다음 표에서는 WCF 분석 추적과 관련 된 이벤트 수준, 식별자 및 메시지를 정의 합니다.  
  
## <a name="event-reference"></a>이벤트 참조  
  
|이벤트 ID|이벤트 수준|이벤트 메시지|키워드|  
|--------------|-----------------|-------------------|--------------|  
|[131 - BufferPoolAllocation](131-bufferpoolallocation.md)|자세히|풀에서 %1바이트를 할당하는 중입니다.|인프라|  
|[132 - BufferPoolChangeQuota](132-bufferpoolchangequota.md)|자세히|크기가 %1인 BufferPool의 할당량을 %2(으)로 변경하는 중입니다.|인프라|  
|[133 - ActionItemScheduled](133-actionitemscheduled.md)|자세히|IO 스레드 스케줄러 콜백이 호출되었습니다.|인프라|  
|[134 - ActionItemCallbackInvoked](134-actionitemcallbackinvoked.md)|자세히|IO 스레드 스케줄러 콜백이 호출되었습니다.|인프라|  
|[201 - ClientMessageInspectorAfterReceiveInvoked](201-clientmessageinspectorafterreceiveinvoked.md)|정보|디스패처가 '%1' 형식의 ClientMessageInspector에 대해 'AfterReceiveReply'를 호출했습니다.|문제 해결, ServiceModel|  
|[202 - ClientMessageInspectorBeforeSendInvoked](202-clientmessageinspectorbeforesendinvoked.md)|정보|디스패처가 '%1' 형식의 ClientMessageInspector에 대해 'BeforeSendRequest'를 호출했습니다.|문제 해결, ServiceModel|  
|[203 - ClientParameterInspectorAfterCallInvoked](203-clientparameterinspectoraftercallinvoked.md)|정보|디스패처가 '%1' 형식의 ClientParameterInspector에 대해 'AfterCall'을 호출했습니다.|문제 해결, ServiceModel|  
|[204 - ClientParameterInspectorBeforeCallInvoked](204-clientparameterinspectorbeforecallinvoked.md)|정보|디스패처가 '%1' 형식의 ClientParameterInspector에 대해 'BeforeCall'을 호출했습니다.|문제 해결, ServiceModel|  
|[205 - OperationInvoked](205-operationinvoked.md)|정보|OperationInvoker가 '%1' 메서드를 호출했습니다.|EndToEndMonitoring, 문제 해결, ServiceModel|  
|[206 - ErrorHandlerInvoked](206-errorhandlerinvoked.md)|정보|디스패처가 '%3' 형식의 예외와 함께 '%1' 형식의 ErrorHandler를 호출했습니다.  ErrorHandled == '%2'.|문제 해결, ServiceModel|  
|[207 - FaultProviderInvoked](207-faultproviderinvoked.md)|정보|디스패처가 '%2' 형식의 예외와 함께 '%1' 형식의 FaultProvider를 호출했습니다.|문제 해결, ServiceModel|  
|[208 - MessageInspectorAfterReceiveInvoked](208-messageinspectorafterreceiveinvoked.md)|정보|디스패처가 '%1' 형식의 MessageInspector에 대해 'AfterReceiveReply'를 호출했습니다.|문제 해결, ServiceModel|  
|[209 - MessageInspectorBeforeSendInvoked](209-messageinspectorbeforesendinvoked.md)|정보|디스패처가 '%1' 형식의 MessageInspector에 대해 'BeforeSendRequest'를 호출했습니다.|문제 해결, ServiceModel|  
|[210 - MessageThrottleExceeded](210-messagethrottleexceeded.md)|경고|'%1'의 스로틀 한계 '%2'에 도달했습니다.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[211 - ParameterInspectorAfterCallInvoked](211-parameterinspectoraftercallinvoked.md)|정보|디스패처가 '%1' 형식의 ParameterInspector에 대해 'AfterCall'을 호출했습니다.|문제 해결, ServiceModel|  
|[212 - ParameterInspectorBeforeCallInvoked](212-parameterinspectorbeforecallinvoked.md)|정보|디스패처가 '%1' 형식의 ParameterInspector에 대해 'BeforeCall'을 호출했습니다.|문제 해결, ServiceModel|  
|[213 - ServiceHostStarted](213-servicehoststarted.md)|LogAlways|ServiceHost 시작: '%1'.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[214 - OperationCompleted](214-operationcompleted.md)|정보|OperationInvoker가 '%1' 메서드에 대한 호출을 완료했습니다.  메서드 호출 기간은 '%2'밀리초입니다.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[215 - MessageReceivedByTransport](215-messagereceivedbytransport.md)|정보|전송이 '%1'에서 메시지를 받았습니다.|문제 해결, ServiceModel|  
|[216 - MessageSentByTransport](216-messagesentbytransport.md)|정보|전송이 '%1'에 메시지를 보냈습니다.|문제 해결, ServiceModel|  
|[217 - ClientOperationPrepared](217-clientoperationprepared.md)|정보|클라이언트가 '%2' 계약에 정의된 '%1' 작업을 실행하는 중입니다. 메시지를 '%3'(으)로 보냅니다.|문제 해결, ServiceModel|  
|[218 - ClientOperationCompleted](218-clientoperationcompleted.md)|정보|클라이언트가 '%2' 계약에 정의된 '%1' 작업 실행을 완료했습니다. 메시지가 '%3'(으)로 전송되었습니다.|문제 해결, ServiceModel|  
|[219 - ServiceException](219-serviceexception.md)|오류|메시지를 처리하는 동안 '%2' 형식의 처리되지 않은 예외가 발생했습니다.  전체 예외 ToString: %1.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[220 - MessageSentToTransport](220-messagesenttotransport.md)|정보|디스패처가 전송에 메시지를 보냈습니다. Correlation ID == '%1'.|EndToEndMonitoring, 문제 해결, ServiceModel|  
|[221 - MessageReceivedFromTransport](221-messagereceivedfromtransport.md)|정보|디스패처가 전송에서 메시지를 받았습니다. Correlation ID == '%1'.|EndToEndMonitoring, 문제 해결, ServiceModel|  
|[222 - OperationFailed](222-operationfailed.md)|경고|OperationInvoker의 호출을 받은 '%1' 메서드에서 처리되지 않은 예외가 발생했습니다. 메서드 호출 기간은 '%2'밀리초입니다.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[223 - OperationFaulted](223-operationfaulted.md)|경고|OperationInvoker의 호출을 받은 '%1' 메서드에서 FaultException이 발생했습니다. 메서드 호출 기간은 '%2'밀리초입니다.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[224 - MessageThrottleAtSeventyPercent](224-messagethrottleatseventypercent.md)|경고|'%2'의 스로틀 제한 '%1'이(가) 70퍼센트입니다.|HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[226 - IdleServicesClosed](226-idleservicesclosed.md)|LogAlways|활성화된 총 %2개 서비스 중에서 %1개의 유휴 서비스가 종료되었습니다.|HealthMonitoring WebHost|  
|[301 - UserDefinedErrorOccurred](301-userdefinederroroccurred.md)|오류|이름: '%1', 참조: '%2', 페이로드: %3.|UserEvents, HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[302 - UserDefinedWarningOccurred](302-userdefinedwarningoccurred.md)|경고|이름: '%1', 참조: '%2', 페이로드: %3.|UserEvents, HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[303 - UserDefinedInformationEventOccured](303-userdefinedinformationeventoccured.md)|정보|이름: '%1', 참조: '%2', 페이로드: %3.|UserEvents, HealthMonitoring, EndToEndMonitoring, 문제 해결, ServiceModel|  
|[401- StopSignPostEvent](401-stopsignpostevent.md)|정보|동작 경계입니다.|문제 해결|  
|[402 - StartSignpostEvent](402-startsignpostevent.md)|정보|동작 경계입니다.|문제 해결|  
|[403 - SuspendSignpostEvent](403-suspendsignpostevent.md)|정보|동작 경계입니다.|문제 해결|  
|[404 - ResumeSignpostEvent](404-resumesignpostevent.md)|정보|동작 경계입니다.|문제 해결|  
|[451 - MessageLogInfo](451-messageloginfo.md)|정보|%1|문제 해결, WCFMessageLogging|  
|[452 - MessageLogWarning](452-messagelogwarning.md)|경고|%1|문제 해결, WCFMessageLogging|  
|[499 - TransferEmitted](499-transferemitted.md)|LogAlways|전송 이벤트를 내보냈습니다.|문제 해결, UserEvents, EndToEndMonitoring, ServiceModel, WFTracking, ServiceHost, WCFMessageLogging|  
|[501 - CompilationStart](501-compilationstart.md)|정보|컴파일을 시작합니다.|WebHost|  
|[502 - CompilationStop](502-compilationstop.md)|정보|컴파일을 종료합니다.|WebHost|  
|[503 - ServiceHostFactoryCreationStart](503-servicehostfactorycreationstart.md)|정보|ServiceHostFactory 만들기를 시작합니다.|WebHost|  
|[504 - ServiceHostFactoryCreationStop](504-servicehostfactorycreationstop.md)|정보|ServiceHostFactory 만들기를 종료합니다.|WebHost|  
|[505 - CreateServiceHostStart](505-createservicehoststart.md)|정보|CreateServiceHost를 시작합니다.|WebHost|  
|[506 - CreateServiceHostStop](506-createservicehoststop.md)|정보|CreateServiceHost를 종료합니다.|WebHost|  
|[507 - HostedTransportConfigurationManagerConfigInitStart](507-hostedtransportconfigurationmanagerconfiginitstart.md)|정보|HostedTransportConfigurationManager에서 구성 초기화를 시작합니다.|WebHost|  
|[508 - HostedTransportConfigurationManagerConfigInitStop](508-hostedtransportconfigurationmanagerconfiginitstop.md)|정보|HostedTransportConfigurationManager에서 구성 초기화를 종료합니다.|WebHost|  
|[509 - ServiceHostOpenStart](509-servicehostopenstart.md)|정보|HostedTransportConfigurationManager에서 구성 초기화를 종료합니다.|ServiceHost|  
|[510 - ServiceHostOpenStop](510-servicehostopenstop.md)|정보|ServiceHost 열기가 완료되었습니다.|ServiceHost|  
|[513 - WebHostRequestStart](513-webhostrequeststart.md)|정보|AppDomain '%1'에서 가상 경로가 '%2'인 요청을 수신했습니다.|WebHost|  
|[514 - WebHostRequestStop](514-webhostrequeststop.md)|정보|WebHostRequest가 중지됩니다.|WebHost|  
|[601 - CBAEntryRead](601-cbaentryread.md)|자세히|처리한 ServiceActivation 요소 상대 주소: '%1', 정규화된 상대 주소 '%2'||  
|[602 - CBAMatchFound](602-cbamatchfound.md)|자세히|들어오는 요청이 주소가 '%1'인 ServiceActivation 요소와 일치합니다.||  
|[603 - AspNetRoutingService](603-aspnetroutingservice.md)|자세히|들어오는 요청이 주소가 %1인 Asp.Net 경로에 정의된 WCF 서비스와 일치합니다.|RoutingServices|  
|[604 - AspNetRoute](604-aspnetroute.md)|자세히|serviceType이 '%2'이고 serviceHostFactoryType이 '%3'인 새 Asp.Net 경로 '%1'이(가) 추가되었습니다.|RoutingServices|  
|[605 - IncrementBusyCount](605-incrementbusycount.md)|자세히|IncrementBusyCount를 호출했습니다. 원본: %1|WebHost|  
|[606 - DecrementBusyCount](606-decrementbusycount.md)|자세히|DecrementBusyCount를 호출했습니다. 원본: %1|WebHost|  
|[701 - ServiceChannelOpenStart](701-servicechannelopenstart.md)|자세히|ServiceChannelOpen이 시작되었습니다.|WebHost|  
|[702 - ServiceChannelOpenStop](702-servicechannelopenstop.md)|정보|ServiceChannelOpen이 완료되었습니다.|ServiceModel|  
|[703 - ServiceChannelCallStart](703-servicechannelcallstart.md)|정보|ServiceChannelCall이 시작되었습니다.|ServiceModel|  
|[704 - ServiceChannelBeginCallStart](704-servicechannelbegincallstart.md)|정보|ServiceChannel 비동기 호출이 시작되었습니다.|ServiceModel|  
|[706 - HttpSendMessageStart](706-httpsendmessagestart.md)|자세히|Http 전송 요청이 시작됩니다.|HTTP|  
|[707 - HttpSendStop](707-httpsendstop.md)|자세히|Http 전송 요청이 중지됩니다.|HTTP|  
|[708 - HttpMessageReceiveStart](708-httpmessagereceivestart.md)|자세히|http 전송으로부터 메시지가 수신되었습니다.|HTTP|  
|[709 - DispatchMessageStart](709-dispatchmessagestart.md)|정보|메시지 디스패치가 시작되었습니다.|ServiceModel|  
|[710 - HttpContextBeforeProcessAuthentication](710-httpcontextbeforeprocessauthentication.md)|자세히|메시지 디스패치를 위한 인증을 시작합니다.|ServiceModel|  
|[711 - DispatchMessageBeforeAuthorization](711-dispatchmessagebeforeauthorization.md)|자세히|메시지 디스패치를 위한 권한 부여를 시작합니다.|ServiceModel|  
|[712 - DispatchMessageStop](712-dispatchmessagestop.md)|정보|메시지 디스패치가 완료되었습니다.|ServiceModel|  
|[715 - ClientChannelOpenStart](715-clientchannelopenstart.md)|정보|ServiceChannel 열기가 시작됩니다.|ServiceModel|  
|[716 - ClientChannelOpenStop](716-clientchannelopenstop.md)|정보|ServiceChannel 열기가 중지됩니다.|ServiceModel|  
|[717 - HttpSendStreamedMessageStart](717-httpsendstreamedmessagestart.md)|정보|Http 전송 스트리밍 메시지가 시작되었습니다.|HTTP|  
|[1400 - ChannelInitializationTimeout](1400-channelinitializationtimeout.md)|오류|1%|ServiceModel|  
|[1401 - CloseTimeout](1401-closetimeout.md)|오류|1%|ServiceModel|  
|[1402 - IdleTimeout](1402-idletimeout.md)|오류|%1 연결 풀 키: %2|ServiceModel|  
|[1403 - LeaseTimeout](1403-leasetimeout.md)|정보|%1 연결 풀 키: %2|ServiceModel|  
|[1405 - OpenTimeout](1405-opentimeout.md)|오류|%1|ServiceModel|  
|[1406 - ReceiveTimeout](1406-receivetimeout.md)|오류|%1|ServiceModel|  
|[1407 - SendTimeout](1407-sendtimeout.md)|오류|%1|ServiceModel|  
|[1409 - InactivityTimeout](1409-inactivitytimeout.md)|정보|%1|ServiceModel|  
|[1416 - MaxReceivedMessageSizeExceeded](1416-maxreceivedmessagesizeexceeded.md)|오류|%1|할당량|  
|[1417 - MaxSentMessageSizeExceeded](1417-maxsentmessagesizeexceeded.md)|오류|%1|할당량|  
|[1418 - MaxOutboundConnectionsPerEndpointExceeded](1418-maxoutboundconnectionsperendpointexceeded.md)|정보|%1|할당량|  
|[1419 - MaxPendingConnectionsExceeded](1419-maxpendingconnectionsexceeded.md)|정보|%1|할당량|  
|[1420 - ReaderQuotaExceeded](1420-readerquotaexceeded.md)|오류|%1|할당량|  
|[1422 - NegotiateTokenAuthenticatorStateCacheExceeded](1422-negotiatetokenauthenticatorstatecacheexceeded.md)|오류|%1|할당량|  
|[1423 - NegotiateTokenAuthenticatorStateCacheRatio](1423-negotiatetokenauthenticatorstatecacheratio.md)|자세히|협상 토큰 인증자 상태 캐시 비율: %1/%2|할당량|  
|[1424 - SecuritySessionRatio](1424-securitysessionratio.md)|자세히|보안 세션 비율: %1/%2|할당량|  
|[1430 - PendingConnectionsRatio](1430-pendingconnectionsratio.md)|자세히|보류 중인 연결 비율: %1/%2|할당량|  
|[1431 - ConcurrentCallsRatio](1431-concurrentcallsratio.md)|자세히|동시 세션 비율: %1/%2|할당량|  
|[1432 - ConcurrentSessionsRatio](1432-concurrentsessionsratio.md)|자세히|동시 세션 비율: %1/%2|할당량|  
|[1433 - OutboundConnectionsPerEndpointRatio](1433-outboundconnectionsperendpointratio.md)|자세히|엔드포인트당 아웃바운드 연결 비율: %1/%2|할당량|  
|[1436 - PendingMessagesPerChannelRatio](1436-pendingmessagesperchannelratio.md)|자세히|채널당 보류 중인 메시지 비율: %1/%2|할당량|  
|[1438 - ConcurrentInstancesRatio](1438-concurrentinstancesratio.md)|자세히|동시 인스턴스 비율: %1/%2|할당량|  
|[1439 - PendingAcceptsAtZero](1439-pendingacceptsatzero.md)|정보|보류 중인 수락 항목 없음|할당량|  
|[1441 - MaxSessionSizeReached](1441-maxsessionsizereached.md)|경고|1%|할당량|  
|[1442 - ReceiveRetryCountReached](1442-receiveretrycountreached.md)|경고|ID가 '%1'인 MSMQ 메시지에서 수신 재시도 횟수에 도달했습니다.|할당량|  
|[1443 - MaxRetryCyclesExceededMsmq](1443-maxretrycyclesexceededmsmq.md)|오류|ID가 '%1'인 MSMQ 메시지에서 최대 재시도 주기가 초과되었습니다.|할당량|  
|[1445 - ReadPoolMiss](1445-readpoolmiss.md)|자세히|새 '%1'이(가) 만들어졌습니다.|할당량|  
|[1446 - WritePoolMiss](1446-writepoolmiss.md)|자세히|새 '%1'이(가) 만들어졌습니다.|할당량|  
|[1451 - MaxRetryCyclesExceeded](1451-maxretrycyclesexceeded.md)|오류|1%|할당량|  
|[3300 - ReceiveContextCompleteFailed](3300-receivecontextcompletefailed.md)|경고|'%1'을(를) 완료하지 못했습니다.|채널|  
|[3301 - ReceiveContextAbandonFailed](3301-receivecontextabandonfailed.md)|경고|%1을(를) 중단하지 못했습니다.|채널|  
|[3303 - ReceiveContextAbandonWithException](3303-receivecontextabandonwithexception.md)|경고|컨텍스트 수신 오류가 발생했습니다.|ServiceModel|  
|[3303 - ReceiveContextAbandonWithException](3303-receivecontextabandonwithexception.md)|정보|%1이(가) %2 예외와 함께 중단되었습니다.|채널|  
|[3305 - ClientBaseCachedChannelFactoryCount](3305-clientbasecachedchannelfactorycount.md)|정보|캐시된 채널 팩터리 수는 '%1'입니다.  최대 '%2'개 채널 팩터리를 캐시할 수 있습니다.|ServiceModel|  
|[3306 - ClientBaseChannelFactoryAgedOutofCache](3306-clientbasechannelfactoryagedoutofcache.md)|정보|캐시가 해당 한도 '%1'에 도달했기 때문에 채널 팩터리가 캐시에서 만료되었습니다.|ServiceModel|  
|[3307 - ClientBaseChannelFactoryCacheHit](3307-clientbasechannelfactorycachehit.md)|정보|캐시에서 사용된 일치하는 채널 팩터리가 발견되었습니다.|ServiceModel|  
|[3308 - ClientBaseUsingLocalChannelFactory](3308-clientbaseusinglocalchannelfactory.md)|정보|캐시에서 채널 팩터리를 사용 하지 않습니다 (예: 캐싱에 사용 하지 않도록 설정 됨).|ServiceModel|  
|[3309 - QueryCompositionExecuted](3309-querycompositionexecuted.md)|정보|'%1'을(를) 사용한 쿼리 작성이 요청 Uri: '%2'에서 실행되었습니다.|ServiceModel|  
|[3310 - DispatchFailed](3310-dispatchfailed.md)|오류|'%1' 작업이 디스패치되었지만 오류가 발생했습니다.|ServiceModel|  
|[3311 - DispatchSuccessful](3311-dispatchsuccessful.md)|정보|'%1' 작업이 성공적으로 디스패치되었습니다.|ServiceModel|  
|[3312 - MessageReadByEncoder](3312-messagereadbyencoder.md)|정보|인코더가 크기가 '%1'바이트인 메시지를 읽었습니다.|채널|  
|[3312 - MessageReadByEncoder](3312-messagereadbyencoder.md)|정보|인코더가 크기가 '%1'바이트인 메시지를 썼습니다.|채널|  
|[3314 - SessionIdleTimeout](3314-sessionidletimeout.md)|오류|URI: '%1'에 대한 유휴 채널에 대해 세션을 중단하는 중입니다.|ServiceModel|  
|[3319 - SocketAcceptEnqueued](3319-socketacceptenqueued.md)|자세히|연결 수락이 시작되었습니다.|TCP|  
|[3320 - SocketAccepted](3320-socketaccepted.md)|자세히|ListenerId:%1에서 SocketId:%2이(가) 수락되었습니다.|TCP|  
|[3321 - ConnectionPoolMiss](3321-connectionpoolmiss.md)|자세히|%1에 대한 풀에 사용 가능한 연결이 없고 %2개의 연결을 사용 중입니다.|채널|  
|[3322 - DispatchFormatterDeserializeRequestStart](3322-dispatchformatterdeserializerequeststart.md)|자세히|디스패처가 요청 메시지의 deserialization를 시작했습니다.|ServiceModel|  
|[3323 - DispatchFormatterDeserializeRequestStop](3323-dispatchformatterdeserializerequeststop.md)|자세히|디스패처가 요청 메시지의 역직렬화를 완료했습니다.|ServiceModel|  
|[3324 - DispatchFormatterSerializeReplyStart](3324-dispatchformatterserializereplystart.md)|자세히|디스패처가 회신 메시지의 직렬화를 시작했습니다.|ServiceModel|  
|[3325 - DispatchFormatterSerializeReplyStop](3325-dispatchformatterserializereplystop.md)|자세히|디스패처가 회신 메시지의 직렬화를 완료했습니다.|ServiceModel|  
|[3326 - ClientFormatterSerializeRequestStart](3326-clientformatterserializerequeststart.md)|자세히|클라이언트 요청 직렬화가 시작되었습니다.|ServiceModel|  
|[3327 - ClientFormatterSerializeRequestStop](3327-clientformatterserializerequeststop.md)|자세히|클라이언트에서 요청 메시지의 직렬화가 완료되었습니다.|ServiceModel|  
|[3328 - ClientFormatterDeserializeReplyStart](3328-clientformatterdeserializereplystart.md)|자세히|클라이언트에서 회신 메시지 역직렬화가 시작되었습니다.|ServiceModel|  
|[3329 - ClientFormatterDeserializeReplyStop](3329-clientformatterdeserializereplystop.md)|자세히|클라이언트에서 회신 메시지 역직렬화가 완료되었습니다.|ServiceModel|  
|[3330 - SecurityNegotiationStart](3330-securitynegotiationstart.md)|자세히|보안 협상이 시작되었습니다.|보안|  
|[3331 - SecurityNegotiationStop](3331-securitynegotiationstop.md)|자세히|보안 협상이 완료되었습니다.|보안|  
|[3332 - SecurityTokenProviderOpened](3332-securitytokenprovideropened.md)|자세히|SecurityTokenProvider 열기가 완료되었습니다.|보안|  
|[3333 - OutgoingMessageSecured](3333-outgoingmessagesecured.md)|자세히|보내는 메시지의 보안이 설정되었습니다.|보안|  
|[3334 - IncomingMessageVerified](3334-incomingmessageverified.md)|자세히|들어오는 메시지가 확인되었습니다.|보안 ServiceModel|  
|[3335 - GetServiceInstanceStart](3335-getserviceinstancestart.md)|자세히|서비스 인스턴스 검색이 시작되었습니다.|ServiceModel|  
|[3336 - GetServiceInstanceStop](3336-getserviceinstancestop.md)|자세히|서비스 인스턴스가 검색되었습니다.|ServiceModel|  
|[3337 - ChannelReceiveStart](3337-channelreceivestart.md)|자세히|ChannelHandlerId:%1 - 메시지 수신 루프가 시작되었습니다.|채널|  
|[3338 - ChannelReceiveStop](3338-channelreceivestop.md)|자세히|ChannelHandlerId:%1 - 메시지 수신 루프가 중지되었습니다.|채널|  
|[3339 - ChannelFactoryCreated](3339-channelfactorycreated.md)|자세히|ChannelFactory가 만들어졌습니다.|ServiceModel|  
|[3340 - PipeConnectionAcceptStart](3340-pipeconnectionacceptstart.md)|자세히|파이프 연결 수락이 %1에서 시작되었습니다.|채널|  
|[3341 - PipeConnectionAcceptStop](3341-pipeconnectionacceptstop.md)|자세히|파이프 연결이 수락되었습니다.|채널|  
|[3342 - EstablishConnectionStart](3342-establishconnectionstart.md)|자세히|%1에 대해 연결 설정이 시작되었습니다.|채널|  
|[3343 - EstablishConnectionStop](3343-establishconnectionstop.md)|자세히|연결이 설정되었습니다.|채널|  
|[3345 - SessionPreambleUnderstood](3345-sessionpreambleunderstood.md)|자세히|'%1'에 대한 세션 프리앰블이 확인되었습니다.|채널|  
|[3346 - ConnectionReaderSendFault](3346-connectionreadersendfault.md)|오류|연결 판독기가 오류 '%1'을(를) 전송하고 있습니다.|채널|  
|[3347 - SocketAcceptClosed](3347-socketacceptclosed.md)|자세히|소켓 수락이 종료되었습니다.|TCP|  
|[3348 - ServiceHostFaulted](3348-servicehostfaulted.md)|심각|서비스 호스트에 오류가 발생했습니다.|TCP|  
|[3349 - ListenerOpenStart](3349-listeneropenstart.md)|자세히|'%1'에 대한 리스너가 열려 있습니다.|채널|  
|[3350 - ListenerOpenStop](3350-listeneropenstop.md)|자세히|리스너 열기가 완료되었습니다.|채널|  
|[3351 - ServerMaxPooledConnectionsQuotaReached](3351-servermaxpooledconnectionsquotareached.md)|자세히|서버 최대 풀 연결 할당량에 도달했습니다.|할당량|  
|[3352 - TcpConnectionTimedOut](3352-tcpconnectiontimedout.md)|오류|원격 주소 %2에 대한 SocketId:%1이(가) 시간 초과되었습니다.|TCP|  
|[3353 - TcpConnectionResetError](3353-tcpconnectionreseterror.md)|경고|원격 주소 %2에 대한 SocketId:%1에 연결 재설정 오류가 발생했습니다.|TCP|  
|[3354 - ServiceSecurityNegotiationCompleted](3354-servicesecuritynegotiationcompleted.md)|자세히|서비스 보안 협상이 완료되었습니다.|보안|  
|[3355 - SecurityNegotiationProcessingFailure](3355-securitynegotiationprocessingfailure.md)|오류|보안 협상을 처리하지 못했습니다.|보안|  
|[3356 - SecurityIdentityVerificationSuccess](3356-securityidentityverificationsuccess.md)|자세히|보안 확인에 성공했습니다.|보안|  
|[3357 - SecurityIdentityVerificationFailure](3357-securityidentityverificationfailure.md)|오류|보안 확인에 실패했습니다.|보안|  
|[3358 - PortSharingDuplicatedSocket](3358-portsharingduplicatedsocket.md)|자세히|%1에 대해 소켓이 중복되었습니다.|ActivationServices|  
|[3359 - SecurityImpersonationSuccess](3359-securityimpersonationsuccess.md)|자세히|보안 가장에 성공했습니다.|보안|  
|[3360 - SecurityImpersonationFailure](3360-securityimpersonationfailure.md)|경고|보안 가장에 실패했습니다.|보안|  
|[3361 - HttpChannelRequestAborted](3361-httpchannelrequestaborted.md)|경고|Http 채널 요청이 중단되었습니다.|HTTP|  
|[3362 - HttpChannelResponseAborted](3362-httpchannelresponseaborted.md)|경고|Http 채널 응답이 중단되었습니다.|HTTP|  
|[3363 - HttpAuthFailed](3363-httpauthfailed.md)|경고|Http 인증이 실패했습니다.|HTTP|  
|[3364 - SharedListenerProxyRegisterStart](3364-sharedlistenerproxyregisterstart.md)|자세히|SharedListenerProxy 등록이 URI '%1'에 대해 시작되었습니다.|ActivationServices|  
|[3365 - SharedListenerProxyRegisterStop](3365-sharedlistenerproxyregisterstop.md)|자세히|SharedListenerProxy 등록이 중지됩니다.|ActivationServices|  
|[3366 - SharedListenerProxyRegisterFailed](3366-sharedlistenerproxyregisterfailed.md)|오류|SharedListenerProxy 등록이 '%1' 상태로 실패했습니다.|ActivationServices|  
|[3367 - ConnectionPoolPreambleFailed](3367-connectionpoolpreamblefailed.md)|오류|ConnectionPoolPreambleFailed가 발생했습니다.|채널|  
|[3368 - SslOnInitiateUpgrade](3368-ssloninitiateupgrade.md)|자세히|SslOnAcceptUpgradeStart|보안|  
|[3369 - SslOnAcceptUpgrade](3369-sslonacceptupgrade.md)|자세히|SslOnAcceptUpgradeStop|보안|  
|[3370 - BinaryMessageEncodingStart](3370-binarymessageencodingstart.md)|자세히|BinaryMessageEncoder에서 메시지 인코딩이 시작되었습니다.|채널|  
|[3371 - MtomMessageEncodingStart](3371-mtommessageencodingstart.md)|자세히|MtomMessageEncoder에서 메시지 인코딩이 시작되었습니다.|채널|  
|[3372 - TextMessageEncodingStart](3372-textmessageencodingstart.md)|자세히|TextMessageEncoder에서 메시지 인코딩이 시작되었습니다.|채널|  
|[3373 - BinaryMessageDecodingStart](3373-binarymessagedecodingstart.md)|자세히|BinaryMessageEncoder에서 메시지 디코딩이 시작되었습니다.|채널|  
|[3374 - MtomMessageDecodingStart](3374-mtommessagedecodingstart.md)|자세히|Mtommessageencoder에서에서 메시지를 디코딩하는 작업을 시작 했습니다.|채널|  
|[3375 - TextMessageDecodingStart](3375-textmessagedecodingstart.md)|자세히|TextMessageEncoder에서 메시지 디코딩이 시작되었습니다.|채널|  
|[3376 - HttpResponseReceiveStart](3376-httpresponsereceivestart.md)|정보|Http 전송에서 메시지 수신이 시작되었습니다.|HTTP|  
|[3377 - SocketReadStop](3377-socketreadstop.md)|자세히|SocketId:%1이(가) '%3'에서 '%2'바이트를 읽었습니다.|TCP|  
|[3378 - SocketAsyncReadStop](3378-socketasyncreadstop.md)|자세히|SocketId:%1이(가) '%3'에서 '%2'바이트를 읽었습니다.|TCP|  
|[3379 - SocketWriteStart](3379-socketwritestart.md)|자세히|SocketId:%1에서 '%3'에 '%2'바이트를 쓰는 중입니다.|TCP|  
|[3380 - SocketAsyncWriteStart](3380-socketasyncwritestart.md)|자세히|SocketId:%1에서 '%3'에 '%2'바이트를 쓰는 중입니다.|TCP|  
|[3381 - SequenceAcknowledgementSent](3381-sequenceacknowledgementsent.md)|자세히|SessionId:%1 승인이 전송되었습니다.|채널|  
|[3382 - ClientReliableSessionReconnect](3382-clientreliablesessionreconnect.md)|정보|SessionId:%1 다시 연결하는 중입니다.|채널|  
|[3383 - ReliableSessionChannelFaulted](3383-reliablesessionchannelfaulted.md)|정보|SessionId:%1 오류가 발생했습니다.|채널|  
|[3384 - WindowsStreamSecurityOnInitiateUpgrade](3384-windowsstreamsecurityoninitiateupgrade.md)|자세히|WindowsStreamSecurity에서 보안 업그레이드를 시작하는 중입니다.|보안|  
|[3385 - WindowsStreamSecurityOnAcceptUpgrade](3385-windowsstreamsecurityonacceptupgrade.md)|자세히|Windows 스트리밍 보안 업그레이드를 수락합니다.|보안|  
|[3386 - SocketConnectionAbort](3386-socketconnectionabort.md)|경고|SocketId:%1을(를) 중단하는 중입니다.|TCP|  
|[3388 - HttpGetContextStart](3388-httpgetcontextstart.md)|자세히|HttpGetContext가 시작됩니다.|HTTP|  
|[3389 - ClientSendPreambleStart](3389-clientsendpreamblestart.md)|자세히|클라이언트 전송 프리앰블이 시작됩니다.|채널|  
|[3390 - ClientSendPreambleStop](3390-clientsendpreamblestop.md)|자세히|클라이언트 전송 프리앰블이 중지됩니다.|채널|  
|[3391 - HttpMessageReceiveFailed](3391-httpmessagereceivefailed.md)|경고|Http 메시지 수신이 실패했습니다.|HTTP|  
|[3392 - TransactionScopeCreate](3392-transactionscopecreate.md)|정보|LocalIdentifier:'%1' 및 DistributedIdentifier:'%2'을(를) 사용하여 TransactionScope를 만드는 중입니다.|ServiceModel|  
|[3393 - StreamedMessageReadByEncoder](3393-streamedmessagereadbyencoder.md)|정보|인코더가 스트리밍된 메시지를 읽었습니다.|채널|  
|[3394 - StreamedMessageWrittenByEncoder](3394-streamedmessagewrittenbyencoder.md)|정보|인코더가 스트리밍된 메시지를 썼습니다.|채널|  
|[3395 - MessageWrittenAsynchronouslyByEncoder](3395-messagewrittenasynchronouslybyencoder.md)|정보|인코더가 메시지를 비동기적으로 썼습니다.|채널|  
|[3396 - BufferedAsyncWriteStart](3396-bufferedasyncwritestart.md)|정보|BufferId:%1에서 기본 스트림에 대한 '%2'바이트 쓰기를 완료했습니다.|채널|  
|[3397 - BufferedAsyncWriteStop](3397-bufferedasyncwritestop.md)|정보|인코더가 메시지를 비동기적으로 썼습니다.|채널|  
|[3398 - PipeSharedMemoryCreated](3398-pipesharedmemorycreated.md)|자세히|파이프 공유 메모리가 '%1'에 만들어졌습니다.|채널|  
|[3399 - NamedPipeCreated](3399-namedpipecreated.md)|자세히|NamedPipe '%1'이(가) 만들어졌습니다.|채널|  
|[3401 - SignatureVerificationStart](3401-signatureverificationstart.md)|자세히|서명 확인이 시작되었습니다.|보안|  
|[3402 - SignatureVerificationSuccess](3402-signatureverificationsuccess.md)|자세히|서명 확인을 성공했습니다.|보안|  
|[3403 - WrappedKeyDecryptionStart](3403-wrappedkeydecryptionstart.md)|자세히|래핑된 키의 암호 해독이 시작되었습니다.|보안|  
|[3404 - WrappedKeyDecryptionSuccess](3404-wrappedkeydecryptionsuccess.md)|자세히|래핑된 키의 암호 해독에 성공했습니다.|보안|  
|[3405 - EncryptedDataProcessingStart](3405-encrypteddataprocessingstart.md)|자세히|암호화된 데이터 처리가 시작되었습니다.|보안|  
|[3406 - EncryptedDataProcessingSuccess](3406-encrypteddataprocessingsuccess.md)|자세히|암호화된 데이터 처리에 성공했습니다.|보안|  
|[3407 - HttpPipelineProcessInboundRequestStart](3407-httppipelineprocessinboundrequeststart.md)|자세히|Http 메시지 처리기가 인바운드 요청 처리를 시작했습니다.|HTTP|  
|[3408 - HttpPipelineBeginProcessInboundRequestStart](3408-httppipelinebeginprocessinboundrequeststart.md)|자세히|Http 메시지 처리기가 비동기 인바운드 요청 처리를 시작했습니다.|HTTP|  
|[3409 - HttpPipelineProcessInboundRequestStop](3409-httppipelineprocessinboundrequeststop.md)|자세히|Http 메시지 처리기가 인바운드 요청 처리를 완료했습니다.|HTTP|  
|[3410 - HttpPipelineFaulted](3410-httppipelinefaulted.md)|경고|Http 메시지 처리기에서 오류가 발생했습니다.|HTTP|  
|[3411 - HttpPipelineTimeoutException](3411-httppipelinetimeoutexception.md)|오류|WebSocket 연결 시간이 초과되었습니다.|HTTP|  
|[3412 - HttpPipelineProcessResponseStart](3412-httppipelineprocessresponsestart.md)|자세히|Http 메시지 처리기가 응답 처리를 시작했습니다.|HTTP|  
|[3413 - HttpPipelineBeginProcessResponseStart](3413-httppipelinebeginprocessresponsestart.md)|자세히|Http 메시지 처리기가 비동기 응답 처리를 시작했습니다.|HTTP|  
|[3414 - HttpPipelineProcessResponseStop](3414-httppipelineprocessresponsestop.md)|자세히|Http 메시지 처리기가 응답 처리를 완료했습니다.|HTTP|  
|[3415 - WebSocketConnectionRequestSendStart](3415-websocketconnectionrequestsendstart.md)|자세히|'%1'에 대한 WebSocket 연결 요청을 보내기 시작합니다.|HTTP|  
|[3416 - WebSocketConnectionRequestSendStop](3416-websocketconnectionrequestsendstop.md)|자세히|WebSocketId:%1 연결 요청을 보냈습니다.|HTTP|  
|[3417 - WebSocketConnectionAcceptStart](3417-websocketconnectionacceptstart.md)|자세히|WebSocket 연결 수락을 시작합니다.|HTTP|  
|[3418 - WebSocketConnectionAccepted](3418-websocketconnectionaccepted.md)|자세히|WebSocketId:%1 연결이 수락되었습니다.|HTTP|  
|[3419 - WebSocketConnectionDeclined](3419-websocketconnectiondeclined.md)|오류|WebSocket 연결이 상태 코드 '%1'(으)로 거부되었습니다.|HTTP|  
|[3420 - WebSocketConnectionFailed](3420-websocketconnectionfailed.md)|오류|WebSocket 연결 요청이 실패했습니다. '%1'|HTTP|  
|[3421 - WebSocketConnectionAborted](3421-websocketconnectionaborted.md)|오류|WebSocketId:%1 연결이 중단되었습니다.|HTTP|  
|[3422 - WebSocketAsyncWriteStart](3422-websocketasyncwritestart.md)|자세히|WebSocketId:%1에서 '%3'에 '%2'바이트를 쓰는 중입니다.|HTTP|  
|[3423 - WebSocketAsyncWriteStop](3423-websocketasyncwritestop.md)|자세히|WebSocketId:%1에서 비동기 쓰기를 중지합니다.|HTTP|  
|[3424 - WebSocketAsyncReadStart](3424-websocketasyncreadstart.md)|자세히|WebSocketId:%1에서 읽기를 시작합니다.|HTTP|  
|[3425 - WebSocketAsyncReadStop](3425-websocketasyncreadstop.md)|자세히|WebSocketId:%1이(가) '%3'에서 '%2'바이트를 읽었습니다.|HTTP|  
|[3426 - WebSocketCloseSent](3426-websocketclosesent.md)|자세히|WebSocketId:%1에서 닫기 상태 '%3'(으)로 '%2'에 닫기 메시지를 보내는 중입니다.|HTTP|  
|[3427 - WebSocketCloseOutputSent](3427-websocketcloseoutputsent.md)|자세히|WebSocketId:%1에서 닫기 상태 '%3'(으)로 '%2'에 출력 닫기 메시지를 보내는 중입니다.|HTTP|  
|[3428 - WebSocketConnectionClosed](3428-websocketconnectionclosed.md)|자세히|WebSocketId:%1 연결이 닫혔습니다.|HTTP|  
|[3429 - WebSocketCloseStatusReceived](3429-websocketclosestatusreceived.md)|자세히|WebSocketId:%1 연결 닫기 메시지가 상태 '%2'(으)로 수신되었습니다.|HTTP|  
|[3430 - WebSocketUseVersionFromClientWebSocketFactory](3430-websocketuseversionfromclientwebsocketfactory.md)|자세히|클라이언트 WebSocket 팩터리 형식 '%1'에서 WebSocketVersion을 사용하는 중입니다.|HTTP|  
|[3431 - WebSocketCreateClientWebSocketWithFactory](3431-websocketcreateclientwebsocketwithfactory.md)|자세히|팩터리 형식이 '%1'인 클라이언트 WebSocket을 만드는 중입니다.|HTTP|  
|[3553 - XamlServicesLoadStart](3553-xamlservicesloadstart.md)|정보|XamlServicesLoad 시작|WebHost|  
|[3554 - XamlServicesLoadStop](3554-xamlservicesloadstop.md)|정보|XamlServicesLoad 중지|WebHost|  
|[3555 - CreateWorkflowServiceHostStart](3555-createworkflowservicehoststart.md)|정보|CreateWorkflowServiceHost 시작|WebHost|  
|[3556 - CreateWorkflowServiceHostStop](3556-createworkflowservicehoststop.md)|정보|CreateWorkflowServiceHost 중지|WebHost|  
|[3558 - ServiceActivationStart](3558-serviceactivationstart.md)|정보|서비스 활성화 시작|WebHost|  
|[3559 - ServiceActivationStop](3559-serviceactivationstop.md)|정보|서비스 활성화 중지|WebHost|  
|[3560 - ServiceActivationAvailableMemory](3560-serviceactivationavailablememory.md)|자세히|사용 가능한 메모리(바이트): %1|할당량|  
|[3800 - RoutingServiceClosingClient](3800-routingserviceclosingclient.md)|정보|라우팅 서비스에서 클라이언트 '%1'을(를) 닫는 중입니다.|RoutingServices|  
|[3800 - RoutingServiceClosingClient](3800-routingserviceclosingclient.md)|경고|라우팅 서비스 클라이언트 '%1'에 오류가 발생했습니다.|RoutingServices|  
|[3802 - RoutingServiceCompletingOneWay](3802-routingservicecompletingoneway.md)|정보|라우팅 서비스 단방향 메시지를 완료하는 중입니다.|RoutingServices|  
|[3803 - RoutingServiceProcessingFailure](3803-routingserviceprocessingfailure.md)|오류|주소가 '%1'인 엔드포인트에서 메시지를 처리하는 동안 라우팅 서비스에 오류가 발생했습니다.|RoutingServices|  
|[3804 - RoutingServiceCreatingClientForEndpoint](3804-routingservicecreatingclientforendpoint.md)|정보|라우팅 서비스에서 엔드포인트 '%1'에 대한 클라이언트를 만드는 중입니다.|RoutingServices|  
|[3805 - RoutingServiceDisplayConfig](3805-routingservicedisplayconfig.md)|자세히|라우팅 서비스가 RouteOnHeadersOnly: %1, SoapProcessingEnabled: %2, EnsureOrderedDispatch: %3(으)로 구성되어 있습니다.|RoutingServices|  
|[3807 - RoutingServiceCompletingTwoWay](3807-routingservicecompletingtwoway.md)|정보|라우팅 서비스 요청 회신 메시지를 완료하는 중입니다.|RoutingServices|  
|[3809 - RoutingServiceMessageRoutedToEndpoints](3809-routingservicemessageroutedtoendpoints.md)|자세히|라우팅 서비스에서 ID가 '%1'인 메시지를 %2 엔드포인트 목록으로 라우팅했습니다.|RoutingServices|  
|[3810 - RoutingServiceConfigurationApplied](3810-routingserviceconfigurationapplied.md)|정보|새 RoutingConfiguration이 라우팅 서비스에 적용되었습니다.|RoutingServices|  
|[3815 - RoutingServiceProcessingMessage](3815-routingserviceprocessingmessage.md)|정보|라우팅 서비스에서 트랜잭션 %4에서 받은 ID: '%1', 동작: '%2', 인바운드 URL: '%3'인 메시지를 처리하는 중입니다.|RoutingServices|  
|[3816 - RoutingServiceTransmittingMessage](3816-routingservicetransmittingmessage.md)|정보|라우팅 서비스에서 ID가 '%1'인 메시지[작업 %2]를 '%3'(으)로 전송하는 중입니다.|RoutingServices|  
|[3817 - RoutingServiceCommittingTransaction](3817-routingservicecommittingtransaction.md)|정보|라우팅 서비스에서 ID가 '%1'인 트랜잭션을 커밋하는 중입니다.|RoutingServices|  
|[3818 - RoutingServiceDuplexCallbackException](3818-routingserviceduplexcallbackexception.md)|오류|라우팅 서비스 구성 요소 %1에 중복 콜백 예외가 발생했습니다.|RoutingServices|  
|[3819 - RoutingServiceMovedToBackup](3819-routingservicemovedtobackup.md)|정보|ID가 '%1'인 라우팅 서비스 메시지[작업 %2]를 백업 엔드포인트 '%3'(으)로 이동했습니다.|RoutingServices|  
|[3820 - RoutingServiceCreatingTransaction](3820-routingservicecreatingtransaction.md)|정보|라우팅 서비스에서 메시지를 처리하기 위해 ID가 '%1'인 새 트랜잭션을 만들었습니다.|RoutingServices|  
|[3821 - RoutingServiceCloseFailed](3821-routingserviceclosefailed.md)|경고|아웃바운드 클라이언트 '%1'을(를) 닫는 동안 라우팅 서비스에 오류가 발생했습니다.|RoutingServices|  
|[3822 - RoutingServiceSendingResponse](3822-routingservicesendingresponse.md)|정보|라우팅 서비스에서 동작이 '%1'인 응답 메시지를 다시 보내는 중입니다.|RoutingServices|  
|[3823 - RoutingServiceSendingFaultResponse](3823-routingservicesendingfaultresponse.md)|경고|라우팅 서비스에서 동작이 '%1'인 오류 응답 메시지를 다시 보내는 중입니다.|RoutingServices|  
|[3824 - RoutingServiceCompletingReceiveContext](3824-routingservicecompletingreceivecontext.md)|자세히|라우팅 서비스에서 ID가 '%1'인 메시지에 대해 ReceiveContext.Complete를 호출하는 중입니다.|RoutingServices|  
|[3825 - RoutingServiceAbandoningReceiveContext](3825-routingserviceabandoningreceivecontext.md)|경고|라우팅 서비스에서 ID가 '%1'인 메시지에 대해 ReceiveContext.Abandon을 호출하는 중입니다.|RoutingServices|  
|[3826 - RoutingServiceUsingExistingTransaction](3826-routingserviceusingexistingtransaction.md)|자세히|라우팅 서비스에서 기존 트랜잭션 '%1'을(를) 사용하여 메시지를 보냅니다.|RoutingServices|  
|[3827 - RoutingServiceTransmitFailed](3827-routingservicetransmitfailed.md)|경고|'%1'(으)로 보내는 동안 라우팅 서비스에서 오류가 발생했습니다.|RoutingServices|  
|[3828 - RoutingServiceFilterTableMatchStart](3828-routingservicefiltertablematchstart.md)|정보|라우팅 서비스 MessageFilterTable 일치 시작.|RoutingServices|  
|[3829 - RoutingServiceFilterTableMatchStop](3829-routingservicefiltertablematchstop.md)|정보|라우팅 서비스 MessageFilterTable 일치 중지.|RoutingServices|  
|[3830 - RoutingServiceAbortingChannel](3830-routingserviceabortingchannel.md)|자세히|라우팅 서비스가 '%1' 채널에서 중단을 요청하고 있습니다.|RoutingServices|  
|[3831 - RoutingServiceHandledException](3831-routingservicehandledexception.md)|자세히|라우팅 서비스가 예외를 처리했습니다.|RoutingServices|  
|[3832 - RoutingServiceTransmitSucceeded](3832-routingservicetransmitsucceeded.md)|정보|라우팅 서비스가 ID '%1인 메시지[작업 %2]를 '%3'(으)로 전송했습니다.|RoutingServices|  
|[4001 - TransportListenerSessionsReceived](4001-transportlistenersessionsreceived.md)|자세히|'%1'을(를) 통해 전송 리스너 세션이 수신되었습니다.|ActivationServices|  
|[4002 - FailFastException](4002-failfastexception.md)|심각|FailFastException이 발생했습니다.|ActivationServices|  
|[4003 - ServiceStartPipeError](4003-servicestartpipeerror.md)|오류|서비스 시작 파이프 오류가 발생했습니다.|ActivationServices|  
|[4008 - DispatchSessionStart](4008-dispatchsessionstart.md)|자세히|세션 디스패치가 시작되었습니다.|ActivationServices|  
|[4008 - DispatchSessionStart](4008-dispatchsessionstart.md)|경고|보류 중인 항목이 '%2'개로 보류 중인 세션 큐가 꽉 차서 '%1'에 대한 세션을 디스패치하지 못했습니다.|ActivationServices|  
|[4011 - MessageQueueRegisterStart](4011-messagequeueregisterstart.md)|자세히|메시지 큐 등록이 시작됩니다.|ActivationServices|  
|[4012 - MessageQueueRegisterAbort](4012-messagequeueregisterabort.md)|오류|URI '%2'에 대한 메시지 큐 등록이 중단되었습니다. 상태: '%1'.|ActivationServices|  
|[4013 - MessageQueueUnregisterSucceeded](4013-messagequeueunregistersucceeded.md)|자세히|URI '%1'에 대한 메시지 큐 등록을 취소했습니다.|ActivationServices|  
|[4014 - MessageQueueRegisterFailed](4014-messagequeueregisterfailed.md)|오류|URI '%1'에 대한 메시지 큐를 등록하지 못했습니다. 상태: '%2'.|ActivationServices|  
|[4015 - MessageQueueRegisterCompleted](4015-messagequeueregistercompleted.md)|정보|URI '%1'에 대한 메시지 큐 등록이 완료되었습니다.|ActivationServices|  
|[4016 - MessageQueueDuplicatedSocketError](4016-messagequeueduplicatedsocketerror.md)|오류|메시지 큐로 소켓을 복제하지 못했습니다.|ActivationServices|  
|[4019 - MessageQueueDuplicatedSocketComplete](4019-messagequeueduplicatedsocketcomplete.md)|자세히|MessageQueueDuplicatedSocketComplete|ActivationServices|  
|[4020 - TcpTransportListenerListeningStart](4020-tcptransportlistenerlisteningstart.md)|자세히|TCP 전송 리스너가 URI '%1'에서 수신을 시작하는 중입니다.|ActivationServices|  
|[4021 - TcpTransportListenerListeningStop](4021-tcptransportlistenerlisteningstop.md)|자세히|TCP 전송 리스너가 수신 중입니다.|ActivationServices|  
|[4022 - WebhostUnregisterProtocolFailed](4022-webhostunregisterprotocolfailed.md)|오류|오류 코드:%1|ActivationServices|  
|[4023 - WasCloseAllListenerChannelInstancesCompleted](4023-wasclosealllistenerchannelinstancescompleted.md)|정보|WAS에서 모든 리스너 채널 인스턴스를 종료했습니다.|ActivationServices|  
|[4024 - WasCloseAllListenerChannelInstancesFailed](4024-wasclosealllistenerchannelinstancesfailed.md)|오류|오류 코드:%1|ActivationServices|  
|[4025 - OpenListenerChannelInstanceFailed](4025-openlistenerchannelinstancefailed.md)|오류|오류 코드:%1|ActivationServices|  
|[4026 - WasConnected](4026-wasconnected.md)|자세히|WAS가 연결되었습니다.|ActivationServices|  
|[4027 - WasDisconnected](4027-wasdisconnected.md)|자세히|WAS 연결이 해제되었습니다.|ActivationServices|  
|[4028 - PipeTransportListenerListeningStart](4028-pipetransportlistenerlisteningstart.md)|자세히|파이프 전송 리스너 수신이 URI %1에서 시작됩니다.|ActivationServices|  
|[4029 - PipeTransportListenerListeningStop](4029-pipetransportlistenerlisteningstop.md)|자세히|파이프 전송 리스너 수신이 중지됩니다.|ActivationServices|  
|[4030 - DispatchSessionSuccess](4030-dispatchsessionsuccess.md)|정보|세션을 디스패치했습니다.|ActivationServices|  
|[4031 - DispatchSessionFailed](4031-dispatchsessionfailed.md)|오류|세션을 디스패치하지 못했습니다.|ActivationServices|  
|[4032 - WasConnectionTimedout](4032-wasconnectiontimedout.md)|심각|WAS 연결 시간이 초과되었습니다.|ActivationServices|  
|[4033 - RoutingTableLookupStart](4033-routingtablelookupstart.md)|자세히|라우팅 테이블 조회가 시작되었습니다.|ActivationServices|  
|[4034 - RoutingTableLookupStop](4034-routingtablelookupstop.md)|자세히|라우팅 테이블 조회가 완료되었습니다.|ActivationServices|  
|[4035 - PendingSessionQueueRatio](4035-pendingsessionqueueratio.md)|자세히|보류 중인 세션 큐 비율: %1/%2|할당량|  
|[4600 - MessageLogEventSizeExceeded](4600-messagelogeventsizeexceeded.md)|경고|ETW 이벤트 크기를 초과하므로 메시지를 기록할 수 없습니다.|WCFMessageLogging|  
|[4801 - DiscoveryClientInClientChannelFailedToClose](4801-discoveryclientinclientchannelfailedtoclose.md)|경고|DiscoveryClientChannel 내에 만들어진 DiscoveryClient를 닫지 못해 중단했습니다.|검색|  
|[4802 - DiscoveryClientProtocolExceptionSuppressed](4802-discoveryclientprotocolexceptionsuppressed.md)|정보|DiscoveryClient를 닫는 동안에는 ProtocolException이 표시되지 않습니다. DiscoveryService가 DiscoveryClient에 응답을 계속 보내려고 하는 중일 수 있습니다.|검색|  
|[4803 - DiscoveryClientReceivedMulticastSuppression](4803-discoveryclientreceivedmulticastsuppression.md)|정보|DiscoveryClient가 DiscoveryProxy로부터 멀티캐스트 비표시 오류(Suppression) 메시지를 받았습니다.|검색|  
|[4804 - DiscoveryMessageReceivedAfterOperationCompleted](4804-discoverymessagereceivedafteroperationcompleted.md)|정보|해당 %3 작업이 완료되어 messageId='%2'인 %1 메시지가 DiscoveryClient에서 삭제되었습니다.|검색|  
|[4805 - DiscoveryMessageWithInvalidContent](4805-discoverymessagewithinvalidcontent.md)|경고|잘못된 내용이 있어 messageId='%2'인 %1 메시지가 DiscoveryClient에서 삭제되었습니다.|검색|  
|[4806 - DiscoveryMessageWithInvalidRelatesToOrOperationCompleted](4806-discoverymessagewithinvalidrelatestooroperationcompleted.md)|경고|해당 %4 작업이 완료되었거나 relatesTo 값이 잘못되어 messageId='%2'이고 relatesTo='%3'인 %1 메시지가 DiscoveryClient에서 삭제되었습니다.|검색|  
|[4807 - DiscoveryMessageWithInvalidReplyTo](4807-discoverymessagewithinvalidreplyto.md)|경고|잘못된 ReplyTo 주소가 있어 messageId='%1'인 검색 요청 메시지가 삭제되었습니다.|검색|  
|[4808 - DiscoveryMessageWithNoContent](4808-discoverymessagewithnocontent.md)|경고|내용이 없어 %1 메시지가 삭제되었습니다.|검색|  
|[4809 - DiscoveryMessageWithNullMessageId](4809-discoverymessagewithnullmessageid.md)|경고|메시지 머리글에 필요한 MessageId 속성이 없어 %1 메시지가 삭제되었습니다.|검색|  
|[4810 - DiscoveryMessageWithNullMessageSequence](4810-discoverymessagewithnullmessagesequence.md)|경고|DiscoveryMessageSequence 속성이 없어 messageId='%2'인 %1 메시지가 DiscoveryClient에서 삭제되었습니다.|검색|  
|[4811 - DiscoveryMessageWithNullRelatesTo](4811-discoverymessagewithnullrelatesto.md)|경고|메시지 머리글에 필요한 RelatesTo 속성이 없어 messageId='%2'인 %1 메시지가 DiscoveryClient에서 삭제되었습니다.|검색|  
|[4812 - DiscoveryMessageWithNullReplyTo](4812-discoverymessagewithnullreplyto.md)|경고|ReplyTo 주소가 없어 messageId='%1'인 검색 요청 메시지가 삭제되었습니다.|검색|  
|[4813 - DuplicateDiscoveryMessage](4813-duplicatediscoverymessage.md)|경고|중복되어 messageId='%2'인 %1 메시지가 삭제되었습니다.|검색|  
|[4814 - EndpointDiscoverabilityDisabled](4814-endpointdiscoverabilitydisabled.md)|정보|EndpointAddress='%1' 및 ListenUri='%2'을(를) 사용하는 엔드포인트의 검색 기능이 사용하지 않도록 설정되어 있습니다.|검색|  
|[4814 - EndpointDiscoverabilityDisabled](4814-endpointdiscoverabilitydisabled.md)|정보|EndpointAddress='%1' 및 ListenUri='%2'을(를) 사용하는 엔드포인트의 검색 기능이 사용하도록 설정되어 있습니다.|검색|  
|[4816 - FindInitiatedInDiscoveryClientChannel](4816-findinitiatedindiscoveryclientchannel.md)|자세히|엔드포인트 검색을 위해 DiscoveryClientChannel에서 찾기 작업이 시작되었습니다.|검색|  
|[4817 - InnerChannelCreationFailed](4817-innerchannelcreationfailed.md)|경고|DiscoveryClientChannel에서 EndpointAddress='%1' 및 Via='%2'을(를) 사용하는 검색된 엔드포인트로 채널을 만들지 못했습니다. DiscoveryClientChannel은 이제 사용 가능한 다음 엔드포인트로 검색된 엔드포인트를 사용하게 됩니다.|검색|  
|[4818 - InnerChannelOpenFailed](4818-innerchannelopenfailed.md)|경고|DiscoveryClientChannel에서 EndpointAddress='%1' 및 Via='%2'을(를) 사용하는 검색된 엔드포인트로 채널을 열지 못했습니다. DiscoveryClientChannel은 이제 사용 가능한 다음 엔드포인트로 검색된 엔드포인트를 사용하게 됩니다.|검색|  
|[4819 - InnerChannelOpenSucceeded](4819-innerchannelopensucceeded.md)|정보|DiscoveryClientChannel에서 엔드포인트를 성공적으로 검색하고 이를 사용하여 채널을 열었습니다. 클라이언트가 EndpointAddress='%1' 및 Via='%2'을(를) 사용하여 서비스에 연결되었습니다.|검색|  
|[4820 - SynchronizationContextReset](4820-synchronizationcontextreset.md)|정보|DiscoveryClientChannel에서 SynchronizationContext가 원래 값 %1(으)로 다시 설정되었습니다.|검색|  
|[4821 - SynchronizationContextSetToNull](4821-synchronizationcontextsettonull.md)|정보|찾기 작업을 시작하기 전에 DiscoveryClientChannel에서 SynchronizationContext가 Null로 설정되었습니다.|검색|  
|[5001 - DCSerializeWithSurrogateStart](5001-dcserializewithsurrogatestart.md)|자세히|DataContract의 %1 serialize와 함께 서로게이트가 시작됩니다.|Serialization|  
|[5002 - DCSerializeWithSurrogateStop](5002-dcserializewithsurrogatestop.md)|자세히|DataContract serialize와 함께 서로게이트가 중지됩니다.|Serialization|  
|[5003 - DCDeserializeWithSurrogateStart](5003-dcdeserializewithsurrogatestart.md)|자세히|DataContract의 %1 deserialize와 함께 서로게이트가 시작됩니다.|Serialization|  
|[5004 - DCDeserializeWithSurrogateStop](5004-dcdeserializewithsurrogatestop.md)|자세히|DataContract deserialize와 함께 서로게이트가 중지됩니다.|Serialization|  
|[5005 - ImportKnownTypesStart](5005-importknowntypesstart.md)|자세히|ImportKnownTypes가 시작됩니다.|Serialization|  
|[5006 - ImportKnownTypesStop](5006-importknowntypesstop.md)|자세히|ImportKnownTypes가 중지됩니다.|Serialization|  
|[5007 - DCResolverResolve](5007-dcresolverresolve.md)|자세히|DataContract 확인자 확인 %1이(가) 시작됩니다.|Serialization|  
|[5008 - DCGenWriterStart](5008-dcgenwriterstart.md)|자세히|%2에 대한 DataContract %1 작성기 생성이 시작됩니다.|Serialization|  
|[5009 - DCGenWriterStop](5009-dcgenwriterstop.md)|자세히|DataContract 작성기 생성이 중지됩니다.|Serialization|  
|[5010 - DCGenReaderStart](5010-dcgenreaderstart.md)|자세히|%2에 대한 DataContract %1 판독기 생성이 시작됩니다.|Serialization|  
|[5011 - DCGenReaderStop](5011-dcgenreaderstop.md)|자세히|DataContract 생성이 중지됩니다.|Serialization|  
|[5012 - DCJsonGenReaderStart](5012-dcjsongenreaderstart.md)|자세히|%2에 대한 Json %1 판독기 생성이 시작됩니다.|Serialization|  
|[5013 - DCJsonGenReaderStop](5013-dcjsongenreaderstop.md)|자세히|Json 판독기 생성이 중지됩니다.|Serialization|  
|[5014 - DCJsonGenWriterStart](5014-dcjsongenwriterstart.md)|자세히|%2에 대한 Json %1 작성기 생성이 시작됩니다.|Serialization|  
|[5015 - DCJsonGenWriterStop](5015-dcjsongenwriterstop.md)|자세히|Json 작성기 생성이 중지됩니다.|Serialization|  
|[5016 - GenXmlSerializableStart](5016-genxmlserializablestart.md)|자세히|'%1'에 대해 serialize 가능한 Xml 생성이 시작됩니다.|Serialization|  
|[5017 - GenXmlSerializableStop](5017-genxmlserializablestop.md)|자세히|직렬화 가능한 Xml 생성이 중지됩니다.|Serialization|  
|[5203 - JsonMessageDecodingStart](5203-jsonmessagedecodingstart.md)|자세히|JsonMessageEncoder에서 메시지 디코딩이 시작되었습니다.|채널|  
|[5204 - JsonMessageEncodingStart](5204-jsonmessageencodingstart.md)|자세히|JsonMessageEncoder에서 메시지 인코딩이 시작되었습니다.|채널|  
|[5402 - TokenValidationStarted](5402-tokenvalidationstarted.md)|자세히|SecurityToken('%1' 형식, ID '%2') 유효성 검사가 시작되었습니다.|보안|  
|[5403 - TokenValidationSuccess](5403-tokenvalidationsuccess.md)|자세히|SecurityToken('%1' 형식, ID '%2') 유효성 검사에 성공했습니다.|보안|  
|[5404 - TokenValidationFailure](5404-tokenvalidationfailure.md)|오류|SecurityToken('%1' 형식, ID '%2') 유효성 검사에 실패했습니다. %3|보안|  
|[5405 - GetIssuerNameSuccess](5405-getissuernamesuccess.md)|자세히|tokenid %2에서 발급자 이름 %1 검색에 성공했습니다.|보안|  
|[5406 - GetIssuerNameFailure](5406-getissuernamefailure.md)|오류|tokenId:%1에서 발급자 이름 검색에 실패했습니다.|보안|  
|[5600 - FederationMessageProcessingStarted](5600-federationmessageprocessingstarted.md)|자세히|페더레이션 메시지 처리가 시작되었습니다.|보안|  
|[5601 - FederationMessageProcessingSuccess](5601-federationmessageprocessingsuccess.md)|자세히|페더레이션 메시지 처리에 성공했습니다.|보안|  
|[5602 - FederationMessageCreationStarted](5602-federationmessagecreationstarted.md)|자세히|폼 게시에서 페더레이션 메시지를 만들기 시작했습니다.|보안|  
|[5603 - FederationMessageCreationSuccess](5603-federationmessagecreationsuccess.md)|자세히|폼 게시에서 페더레이션 메시지 만들기에 성공했습니다.|보안|  
|[5604 - SessionCookieReadingStarted](5604-sessioncookiereadingstarted.md)|자세히|세션 쿠키에서 세션 토큰을 읽기 시작했습니다.|보안|  
|[5605 - SessionCookieReadingSuccess](5605-sessioncookiereadingsuccess.md)|자세히|세션 쿠키에서 세션 토큰 읽기에 성공했습니다.|보안|  
|[5606 - PrincipalSettingFromSessionTokenStarted](5606-principalsettingfromsessiontokenstarted.md)|자세히|세션 토큰에서 보안 주체 설정이 시작되었습니다.|보안|  
|[5607 - PrincipalSettingFromSessionTokenSuccess](5607-principalsettingfromsessiontokensuccess.md)|자세히|세션 토큰에서 보안 주체 설정에 성공했습니다.|보안|  
|[57393 - AppDomainUnload](57393-appdomainunload.md)|정보|AppDomain을 언로드하고 있습니다. AppDomain.FriendlyName %1, ProcessName %2, ProcessId %3.|인프라|  
|[57394 - HandledException](57394-handledexception.md)|정보|예외를 처리하는 중입니다.|인프라|  
|[57395 - ShipAssertExceptionMessage](57395-shipassertexceptionmessage.md)|오류|예기치 않은 오류가 발생했습니다. 이 오류는 애플리케이션에서 처리할 수 없습니다. 오류와 관련된 다음 메시지가 진단용으로 제공됩니다. %1.|인프라|  
|[57396 - ThrowingException](57396-throwingexception.md)|경고|예외를 throw하고 있습니다. 원본: %1.|인프라|  
|[57397 - UnhandledException](57397-unhandledexception.md)|심각|처리되지 않은 예외가 발생했습니다.|인프라|  
|[57399 - TraceCodeEventLogCritical](57399-tracecodeeventlogcritical.md)|심각|EventLog에 기록합니다.|인프라|  
|[57400 - TraceCodeEventLogError](57400-tracecodeeventlogerror.md)|오류|EventLog에 기록합니다.|인프라|  
|[57401 - TraceCodeEventLogInfo](57401-tracecodeeventloginfo.md)|정보|EventLog에 기록합니다.|인프라|  
|[57402 - TraceCodeEventLogVerbose](57402-tracecodeeventlogverbose.md)|자세히|EventLog에 기록합니다.|인프라|  
|[57403 - TraceCodeEventLogWarning](57403-tracecodeeventlogwarning.md)|경고|EventLog에 기록합니다.|인프라|  
|[57404 - HandledExceptionWarning](57404-handledexceptionwarning.md)|경고|예외를 처리하는 중입니다.|인프라|  
|[62326 - HttpHandlerPickedForUrl](62326-httphandlerpickedforurl.md)|정보|URL '%1'이(가) 루트 요소 형식 '%2'을(를) 사용하여 XAML 문서를 호스트합니다. HTTP 처리기 형식 '%3'이(가) 이 URL에 대한 모든 요청에 서비스를 제공하도록 선택되었습니다.|WebHost|
