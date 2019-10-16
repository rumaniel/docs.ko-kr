---
title: MSMQ 통합 전송
ms.date: 03/30/2017
ms.assetid: 2bf9893a-fbd1-41fc-b6de-a41a44279936
ms.openlocfilehash: 52fd98354ded57bd7d7c075d4f08ca543760e598
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777366"
---
# <a name="msmq-integration-transport"></a>MSMQ 통합 전송
이 항목에서는 MSMQ 통합 전송에 의해 생성된 모든 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|MessageSizeMustBeInIntegerRange|이 팩터리는 메시지를 버퍼링하므로 메시지 크기가 정수 값 범위 내에 있어야 합니다.|  
|MsmqByteArrayBodyExpected|지정된 serialization 형식 및 MSMQ 메시지의 본문 사이에 불일치가 발생했습니다. 메시지를 보내거나 받을 수 없습니다. serialization 형식 ByteArray를 사용하려면 MSMQ 메시지의 본문이 형식 바이트[]여야 합니다.|  
|MsmqCannotDeserializeActiveXMessage|ActiveX serialization 오류가 발생했습니다. 메시지를 보내거나 받을 수 없습니다. 본문의 지정된 변수 유형이 실제 MSMQ 메시지 본문과 일치하지 않습니다.|  
|MsmqCannotUseBodyTypeWithActiveXSerialization|메시지의 속성이 일치하지 않습니다. 메시지를 보내거나 받을 수 없습니다. ActiveX serialization 형식을 사용할 경우 BodyType 메시지 속성을 지정할 수 없습니다.|  
|MsmqInvalidServiceOperationForMsmqIntegrationBinding|MsmqIntegrationBinding 유효성 검사가 실패했습니다. 서비스 엔드포인트를 시작할 수 없습니다. 지정된 바인딩이 지정된 계약의 지정된 서비스 작업을 위한 메서드 서명을 지원하지 않습니다. MsmqIntegrationBinding을 사용하려면 서비스 작업을 수정합니다.|  
|MsmqInvalidTypeDeserialization|serialization 형식을 인식할 수 없으므로 ActiveX serialization이 실패했습니다. 메시지를 보내거나 받을 수 없습니다.|  
|MsmqInvalidTypeSerialization|변수 유형이 인식되지 않습니다. ActiveX serialization이 실패했습니다. 메시지를 보내거나 받을 수 없습니다. 지정한 변수 유형이 지원되지 않습니다.|  
|MsmqStreamBodyExpected|serialization 형식과 본문 내용이 일치하지 않습니다. 메시지를 보내거나 받을 수 없습니다. 스트림 serialization 모드를 사용하면 형식 스트림의 본문만 보내거나 받을 수 있습니다.|
