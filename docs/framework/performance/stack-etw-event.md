---
title: 스택 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- stack event [.NET Framework]
- ETW, stack event (CLR)
ms.assetid: f612fa5b-4b62-4593-a19e-85c9b1018dce
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5dc23f5105b589d5b74c9ea6b7f40b84c2b04e6a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046161"
---
# <a name="stack-etw-event"></a>스택 ETW 이벤트
스택 이벤트는 이벤트가 발생한 후 스택 추적을 생성하기 위해 다른 이벤트와 함께 사용해야 합니다. 런타임 공급자가 사용하도록 설정된 경우에 기록됩니다. 다른 런타임 이벤트가 발생할 때마다 이벤트가 발생하기 때문에 빈도가 매우 높은 이벤트입니다. 이러한 이유로 이 이벤트를 사용할 때는 주의하는 것이 좋습니다.  
  
 다음 표에서는 키워드와 수준을 보여 줍니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
|이벤트를 발생시키기 위한 키워드|Level|  
|-----------------------------------|-----------|  
|`StackKeyword`(0x40000000)|LogAlways(0)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`CLRStackWalk`|82|다른 이벤트와 더불어 이벤트 다음에 스택 추적을 생성합니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|Description|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:Uint16|고유한 런타임 식별자입니다.|  
|Reserved1|win:UInt8|예약되어 있습니다.|  
|Reserved2|win:UInt8|예약되어 있습니다.|  
|FrameCount|win:UInt32|스택 추적의 프레임 수입니다.|  
|스택|win:Pointer|명령 포인터의 열입니다.|  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
