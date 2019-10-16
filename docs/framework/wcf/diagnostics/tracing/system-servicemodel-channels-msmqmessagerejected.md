---
title: System.ServiceModel.Channels.MsmqMessageRejected
ms.date: 03/30/2017
ms.assetid: 9b7c10a7-2af6-44a2-8b1a-90bba0c7cf26
ms.openlocfilehash: 4feeb1b57d79c7445d51f5d688b0a9f55e761542
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61997530"
---
# <a name="systemservicemodelchannelsmsmqmessagerejected"></a>System.ServiceModel.Channels.MsmqMessageRejected
MSMQ에서 메시지를 거부했습니다.  
  
## <a name="description"></a>설명  
 이 추적은 MSMQ 메시지가 거부되었음을 나타냅니다.  
  
 Windows Communication Foundation (WCF) (NetMsmqBinding 또는 MsmqIntegrationBinding을 사용 하 여 사용)를 처리할 수 없는 경우에 MSMQ 메시지가 거부 될 수 있습니다. 이러한 메시지를 포이즌 메시지라고 합니다. 포이즌 메시지는 NetMsmqBinding 또는 MsmqIntegrationBinding의 `ReceiveErrorHandling` 속성을 `Reject`로 설정할 경우 거부됩니다. 거부 된 메시지를 보낸 사람에 게 배달 됩니다 [배달 못 한 편지 큐](https://go.microsoft.com/fwlink/?LinkID=99544)합니다.  
  
 참조 [포이즌 메시지 처리](https://go.microsoft.com/fwlink/?LinkID=99546) 메시지는 포이즌 메시지가 될 경우 및이 적절히 처리 하도록 서비스를 구성 하는 방법에 대 한 자세한 내용은 합니다.  
  
 참조 [MQMarkMessageRejected](https://go.microsoft.com/fwlink/?LinkID=99548) MSMQ에서 거부 된 메시지가 의미 하는 바를 대 한 자세한 내용은 합니다.  
  
## <a name="see-also"></a>참고자료

- [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [추적을 사용하여 애플리케이션 문제 해결](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)
- [관리 및 진단](../../../../../docs/framework/wcf/diagnostics/index.md)
- [포이즌 메시지 처리](https://go.microsoft.com/fwlink/?LinkID=99546)
- [MQMarkMessageRejected](https://go.microsoft.com/fwlink/?LinkID=99548)
