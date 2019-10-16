---
title: 3507 - ServiceEndpointAdded
ms.date: 03/30/2017
ms.assetid: c068fc0e-07ee-4551-9824-ea7216e1fe37
ms.openlocfilehash: c787a1a5af752a3d08e2049cfa0b600b7739e56c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009840"
---
# <a name="3507---serviceendpointadded"></a>3507 - ServiceEndpointAdded
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|ID|3507|  
|키워드|WFServices|  
|수준|정보|  
|채널|Microsoft-Windows-애플리케이션 서버-애플리케이션/분석|  
  
## <a name="description"></a>설명  
 서비스 엔드포인트가 추가되었음을 나타냅니다.  
  
## <a name="message"></a>메시지  
 주소 '%1', 바인딩 '%2' 및 계약 '%3'에 대해 서비스 엔드포인트가 추가되었습니다.  
  
## <a name="details"></a>설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|--------------------|--------------------|-----------------|  
|주소|xs:string|엔드포인트의 주소입니다.|  
|바인딩|xs:string|엔드포인트의 바인딩입니다.|  
|계약|xs:string|엔드포인트의 계약입니다.|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName에서 반환되는 문자열입니다.|
