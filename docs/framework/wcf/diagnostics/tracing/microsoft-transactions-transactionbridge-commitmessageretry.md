---
title: Microsoft.Transactions.TransactionBridge.CommitMessageRetry
ms.date: 03/30/2017
ms.assetid: 4abe01f0-6398-4fba-b2f3-c054b7f7e971
ms.openlocfilehash: 3c398aa13a8cd2b87068216d3c07fb29e1a27c3f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61997968"
---
# <a name="microsofttransactionstransactionbridgecommitmessageretry"></a>Microsoft.Transactions.TransactionBridge.CommitMessageRetry
커밋 메시지 재시도를 응답하지 않는 참가자에게 보냈습니다.  
  
## <a name="description"></a>설명  
 로컬 트랜잭션 관리자가 주어진 시간 내에 응답을 받지 못해서 커밋 메시지를 하위 참가자에게 다시 전송해야 할 경우에 추적됩니다.  
  
## <a name="troubleshooting"></a>문제 해결  
 응답을 제시간에 전달하지 못하도록 하는 잠재적인 네트워크 문제 또는 제품 문제를 조사합니다.  이러한 메시지 중 대부분이 표시되면 이는 인프라 문제 또는 비정상적으로 긴 응답 시간을 나타낼 수 있습니다. 두 가지 문제 모두 시스템 내의 트랜잭션 처리량을 심각하게 감소시킵니다.  
  
## <a name="see-also"></a>참고자료

- [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [추적을 사용하여 애플리케이션 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)
- [관리 및 진단](../../../../../docs/framework/wcf/diagnostics/index.md)
