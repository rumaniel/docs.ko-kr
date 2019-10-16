---
title: 39460 - TrackingValueNotSerializable
ms.date: 03/30/2017
ms.assetid: 476a29ad-24d8-4359-8c17-d4e20c1e1c15
ms.openlocfilehash: e0e5515563ba77426a5f45d92977014c456ab779
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61774389"
---
# <a name="39460---trackingvaluenotserializable"></a>39460 - TrackingValueNotSerializable
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|ID|39460|  
|키워드|WFTracking|  
|수준|경고|  
|채널|Microsoft-Windows-애플리케이션 서버-애플리케이션/디버그|  
  
## <a name="description"></a>설명  
 추적 레코드에서 추출된 인수/변수는 Serialize할 수 없습니다.  
  
## <a name="message"></a>메시지  
 추출된 인수/변수 '%1'은(는) serialize할 수 없습니다.  
  
## <a name="details"></a>설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|--------------------|--------------------|-----------------|  
|이름|xs:string|항목의 이름입니다.|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName에서 반환되는 문자열입니다.|
