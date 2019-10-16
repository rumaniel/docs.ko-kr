---
title: Microsoft.Transactions.TransactionBridge.VolatileParticipantInDoubt
ms.date: 03/30/2017
ms.assetid: 3e8fc825-9f22-47e7-9c16-d64ef291c932
ms.openlocfilehash: 9434f2f902a50a37fb3efee22fd3b18b33af9129
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61997461"
---
# <a name="microsofttransactionstransactionbridgevolatileparticipantindoubt"></a>Microsoft.Transactions.TransactionBridge.VolatileParticipantInDoubt
WS-AT 프로토콜 서비스가 인식할 수 없는 일시적 참가자로부터 Prepared 또는 Replay 메시지를 받았습니다. 트랜잭션 결과가 확실하지 않음을 선언하는 결함을 참가자에게 반환했습니다.  
  
## <a name="description"></a>설명  
 로컬 트랜잭션 관리자가 이미 잊어 버린 일시적인 인리스트먼트로부터 Prepared 또는 Replay 메시지를 받는 경우 추적됩니다.  
  
## <a name="troubleshooting"></a>문제 해결  
 일시적 참가자가 보내는 최신 메시지의 잠재적 원인을 조사합니다.  
  
## <a name="see-also"></a>참고자료

- [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [추적을 사용하여 애플리케이션 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)
- [관리 및 진단](../../../../../docs/framework/wcf/diagnostics/index.md)
