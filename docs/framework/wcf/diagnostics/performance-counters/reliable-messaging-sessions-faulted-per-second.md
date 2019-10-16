---
title: Reliable Messaging Sessions Faulted Per Second
ms.date: 03/30/2017
ms.assetid: 8f8ca2eb-1be4-4b6a-aa78-fcd3ee145fe8
ms.openlocfilehash: c77d6a5f12dcce15dba94e2f63025a219ebcc6fd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61916125"
---
# <a name="reliable-messaging-sessions-faulted-per-second"></a>Reliable Messaging Sessions Faulted Per Second
카운터 이름: Reliable Messaging Sessions Faulted Per Second  
  
## <a name="description"></a>설명  
 초당 이 서비스에서 오류가 발생한 신뢰할 수 있는 메시징 세션의 수입니다.  
  
 이 카운터는 성능 카운터 형식 [PERF_COUNTER_COUNTER](https://go.microsoft.com/fwlink/?LinkID=94649), 값은 다음 수식을 사용 하 여 계산 됩니다.  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)
