---
title: '끝점: Reliable Messaging Messages Dropped Per Second'
ms.date: 03/30/2017
ms.assetid: ea3c4fc0-1e0f-4863-8879-57bc6c113018
ms.openlocfilehash: 8f935bee06d175ce454bd7f58a1afbbe9ab505ad
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61797204"
---
# <a name="endpoint-reliable-messaging-messages-dropped-per-second"></a>끝점: Reliable Messaging Messages Dropped Per Second
카운터 이름: Reliable Messaging Sessions Dropped Per Second.  
  
## <a name="description"></a>설명  
 이 엔드포인트에서 삭제된 신뢰할 수 있는 메시징 메시지의 초당 총 수입니다.  
  
 이 카운터는 성능 카운터 형식 [PERF_COUNTER_COUNTER](https://go.microsoft.com/fwlink/?LinkID=94649), 값은 다음 수식을 사용 하 여 계산 됩니다.  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)
