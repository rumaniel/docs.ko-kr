---
title: MSMQ 전송
ms.date: 03/30/2017
ms.assetid: 3f29a2fe-24df-4614-b64c-b0c084fb7003
ms.openlocfilehash: a2e5384808b82f48bd1d4856bf893130da8c5f1b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61959421"
---
# <a name="msmq-transport"></a>MSMQ 전송
이 항목에서는 MSMQ 전송에 의해 생성된 모든 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|MsmqActiveDirectoryRequiresNativeTransfer|메시지에 대한 바인딩을 확인하지 못했습니다. 클라이언트가 메시지를 보낼 수 없습니다. 바인딩 속성의 충돌로 인해 이 오류가 발생했습니다. UseActiveDirectory가 true로 설정되고 QueueTransferProtocol이 Native로 설정됩니다. 충돌을 해결하려면 이러한 속성 중 하나를 수정하십시오.|  
|MsmqAuthNoneRequiresProtectionNone|서비스에 대한 바인딩 유효성 검사에 실패했습니다. 서비스 엔드포인트 또는 클라이언트를 시작할 수 없습니다. 바인딩 속성의 충돌로 인해 이 오류가 발생했습니다. MsmqAuthenticationMode가 None으로 설정되고 MsmqProtectionLevel이 None으로 설정되지 않습니다. 충돌을 해결하려면 이러한 속성 중 하나를 수정하십시오.|  
|MsmqCustomRequiresPerAddDLQ|메시지에 대한 바인딩을 확인하지 못했습니다. 클라이언트가 메시지를 보낼 수 없습니다. DeadLetterQueue가 Custom으로 설정되었으나 CustomDeadLetterQueue가 지정되지 않았습니다. CustomDeadLetterQueue 속성에서 각 애플리케이션에 대해 배달 못 한 편지 큐의 URI를 지정합니다.|  
|MsmqDeserializationError|XML 메시지를 deserialize하는 동안 오류가 발생했습니다. 메시지를 받을 수 없으며 삭제됩니다.|  
|MsmqDLQNotWriteable|클라이언트에 대한 바인딩을 확인하지 못했습니다. 클라이언트가 메시지를 보낼 수 없습니다. 지정된 배달 못 한 편지 큐가 없거나 쓸 수 없습니다. 쓰기 위한 적절한 권한이 있는 큐가 있는지 확인합니다.|  
|MsmqGetPrivateComputerInformationError|지정된 오류로 인해 버전을 검사하지 못했습니다. MSMQ의 버전을 검색할 수 없습니다. 대기 중인 채널의 모든 작업이 실패합니다. MSMQ가 설치되었으며 사용할 수 있는지 확인하십시오.|  
|MsmqNoAssurancesForVolatile|서비스에 대한 바인딩 유효성 검사에 실패했습니다. 서비스 엔드포인트 또는 클라이언트를 시작할 수 없습니다. ExactlyOnce 속성이 true로 설정되고 Durable 속성이 false로 설정됩니다. 이 값은 지원되지 않습니다. 충돌을 해결하려면 이러한 속성 중 하나를 수정하십시오.|  
|MsmqNonTransactionalQueueNeeded|바인딩 및 MSMQ 큐 구성 사이에 불일치가 감지되었습니다. 서비스 엔드포인트를 시작할 수 없습니다. ExactlyOnce 속성이 false로 설정되었고 메시지를 읽을 큐가 트랜잭션 큐입니다. ExactlyOnce 속성을 true로 설정하여 오류를 수정하거나 비트랜잭션 바인딩을 만드십시오.|  
|MsmqOpenError|지정된 큐를 여는 동안 오류가 발생했습니다. 큐에서 메시지를 보내거나 받을 수 없습니다. MSMQ가 설치되었으며 실행 중인지 확인하십시오. 또한 필수 액세스 모드 및 권한을 사용하여 큐를 열 수 있는지 확인하십시오.|  
|MsmqPathLookupError|지정된 큐 경로 이름을 형식 이름으로 변환할 때 오류가 발생했습니다. 대기 중인 채널의 모든 작업이 실패했습니다. 큐 주소가 올바른지 확인하십시오. Active Directory 통합을 사용하도록 설정하여 MSMQ를 설치해야 하고 MSMQ에 액세스할 수 있어야 합니다.|  
|MsmqPerAppDLQRequiresCustom|클라이언트에 대한 바인딩 유효성 검사에 실패했습니다. 클라이언트가 메시지를 보낼 수 없습니다. CustomDeadLetterQueue 속성이 설정되었으나 DeadLetterQueue 속성이 Custom으로 설정되지 않았습니다. DeadLetterQueue 속성을 Custom으로 설정합니다.|  
|MsmqPerAppDLQRequiresExactlyOnce|클라이언트에 대한 바인딩을 확인하지 못했습니다. 클라이언트가 메시지를 보낼 수 없습니다. 바인딩 속성의 충돌로 인해 이 오류가 발생했습니다. 사용자 지정 배달 못 한 편지 큐를 사용하려면 ExactlyOnce를 true로 설정하여 충돌을 해결해야 합니다.|  
|MsmqPerAppDLQRequiresMsmq4|바인딩 및 MSMQ 구성 사이에 불일치가 감지되었습니다. 클라이언트가 메시지를 보낼 수 없습니다. 사용자 지정 배달 못 한 편지 큐를 사용하려면 MSMQ 버전 4.0 이상이 있어야 합니다. MSMQ 버전 4.0 이상이 없을 경우 DeadLetterQueue 속성을 System 또는 None으로 설정하십시오.|  
|MsmqReceiveError|큐에서 메시지를 수신하는 동안 오류가 발생했습니다. MSMQ가 설치되었으며 실행 중인지 확인하십시오. 수신할 큐를 사용할 수 있는지 확인하십시오.|  
|MsmqSameTransactionExpected|이 세션에 대해 트랜잭션 오류가 발생했습니다. 세션 채널에 오류가 발생했습니다. 세션의 메시지를 보내거나 받을 수 없습니다. 대기 중인 세션을 둘 이상의 트랜잭션과 연결할 수 없습니다. 세션의 모든 메시지를 단일 트랜잭션을 사용하여 보내거나 받을 수 있는지 확인하십시오.|  
|MsmqSendError|지정된 큐에 보내는 동안 오류가 발생했습니다. MSMQ가 설치되었으며 실행 중인지 확인하십시오. 로컬 큐로 보내는 중이면 필수 액세스 모드 및 권한과 함께 큐가 존재하는지 확인하십시오.|  
|MsmqTimeSpanTooLarge|메시지 TTL(Time To Live)이 너무 큽니다. 메시지를 보낼 수 없습니다. 메시지 TTL(Time To Live)은 Int32 최대값을 초과할 수 없습니다.|  
|MsmqTokenProviderNeededForCertificates|X509SecurityTokenProvider를 찾을 수 없습니다. 메시지를 보낼 수 없습니다. 인증서 인증 모드에는 X.509 토큰 공급자가 필요합니다. 설치된 인증서에 보안 토큰 공급자를 사용할 수 있는지 확인합니다.|  
|MsmqTransactedDLQExpected|바인딩 및 MSMQ 구성 사이에 불일치가 발생했습니다. 메시지를 보낼 수 없습니다. 바인딩에서 지정된 사용자 지정 배달 못 한 편지 큐가 트랜잭션 큐이어야 합니다. 사용자 지정 배달 못 한 편지 큐 주소가 올바르고 큐가 트랜잭션 큐인지 확인하십시오.|  
|MsmqTransactionalQueueNeeded|바인딩 및 MSMQ 큐 구성 사이에 불일치가 발생했습니다. 서비스 엔드포인트를 시작할 수 없습니다. ExactlyOnce 속성이 true로 설정되었고 메시지를 읽을 큐가 트랜잭션 큐가 아닙니다. 오류를 수정하려면 ExactlyOnce 속성을 false로 설정하거나 이 바인딩에 대한 트랜잭션 큐를 만드십시오.|  
|MsmqTransactionCurrentRequired|세션에서 메시지를 보내기 위해 사용할 수 있는 트랜잭션이 없습니다. 대기 중인 세션에서 메시지를 보내려면 트랜잭션이 필요합니다. 세션에서 메시지를 보내기 위해 트랜잭션 범위가 지정되었는지 확인하십시오.|  
|MsmqTransactionRequired|트랜잭션이 필요하지만 사용할 수 없습니다. 메시지를 보내거나 받을 수 없습니다. 메시지를 보내거나 받기 위해 트랜잭션 범위가 지정되었는지 확인하십시오.|  
|MsmqUnsupportedSerializationFormat|deserialization 오류가 발생했습니다. 메시지를 받을 수 없으며 삭제됩니다. 지정한 serialization 형식이 지원되지 않습니다.|  
|MsmqWrongPrivateQueueSyntax|URL이 잘못되었습니다. 큐의 URL에는 '$' 문자가 포함될 수 없습니다. net.msmq://machine/private/queueName의 구문을 사용하여 개인 큐의 주소를 지정하십시오.|
