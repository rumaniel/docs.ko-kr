---
title: '핵심 통신: 연결 프레임워크'
ms.date: 03/30/2017
ms.assetid: 61ee00e1-896d-47c8-942f-1db28ac89cdc
ms.openlocfilehash: a3f52ac82c2bf09ded504e412d7f216dd0b39959
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61998688"
---
# <a name="core-communications-connection-framework"></a>핵심 통신: 연결 프레임워크
이 항목에서는 Windows Communication Foundation (WCF) 연결 프레임 워크에 의해 생성 된 모든 예외를 나열 합니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|CloseTimedOut|지정된 시간 이후에 Close 메서드의 시간 제한이 초과되었습니다. Close 호출에 전달되는 시간 제한 값을 늘리거나 바인딩에서 CloseTimeout 값을 늘리십시오. 이 작업에 할당된 시간은 더 긴 시간 제한의 일부였을 수 있습니다.|  
|ContentTypeMismatch|지정된 콘텐츠 형식을 필요로 하는 서비스에 해당 콘텐츠 형식을 보냈습니다. 클라이언트와 서비스 바인딩이 일치하지 않을 수 있습니다.|  
|DuplexChannelAbortedDuringOpen|열기 프로세스 도중에 지정된 이중 채널이 종료되었습니다.|  
|FramingValueNotAvailable|값이 완전히 디코딩되지 않았기 때문에 값에 액세스할 수 없습니다.|  
|OperationAbortedDuringConnectionEstablishment|지정된 항목에 대한 연결을 설정하는 동안 작업이 종료되었습니다.|  
|ReceiveTimedOut2|지정된 시간 이후에 수신 작업의 시간 제한이 초과되었습니다. 이 작업에 할당된 시간은 더 긴 시간 제한의 일부였을 수 있습니다.|  
|SendCannotBeCalledAfterCloseOutputSession|CloseOutputSession이 호출된 후에 채널에서 메시지를 보낼 수 없습니다.|
