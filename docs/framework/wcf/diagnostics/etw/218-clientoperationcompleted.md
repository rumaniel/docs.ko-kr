---
title: 218 - ClientOperationCompleted
ms.date: 03/30/2017
ms.assetid: b069bced-7bb2-4e01-8227-e5dbda17af09
ms.openlocfilehash: 83f39be84a8d62962b85652b0e39b537c92e612c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781770"
---
# <a name="218---clientoperationcompleted"></a>218 - ClientOperationCompleted
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|ID|218|  
|키워드|문제 해결, ServiceModel|  
|수준|정보|  
|채널|Microsoft-Windows-애플리케이션 서버-애플리케이션/분석|  
  
## <a name="description"></a>설명  
 이 이벤트는 작업이 완료된 직후에 클라이언트에서 내보내집니다. 즉, 단방향 작업의 경우 메시지가 성공적으로 보내진 직후에 내보내지고 요청-응답 작업의 경우 응답이 수신된 후에 내보내집니다.  
  
## <a name="message"></a>메시지  
 클라이언트가 '%2' 계약과 연결된 '%1' 작업 실행을 완료했습니다. 메시지가 '%3'(으)로 전송되었습니다.  
  
## <a name="details"></a>설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|--------------------|--------------------|-----------------|  
|작업|xs:string|보내는 메시지의 SOAP 동작 헤더입니다.|  
|Contract Name|`xs:string`|계약 이름입니다. 예제: ICalculator 합니다.|  
|대상|`xs:string`|메시지를 받은 서비스 엔드포인트의 주소입니다.|  
|HostReference|`xs:string`|웹 호스팅 서비스의 경우 이 필드는 웹 계층의 서비스를 고유하게 식별합니다. 해당 형식으로 정의 됩니다 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'. 예제: 'Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|AppDomain.CurrentDomain.FriendlyName에서 반환되는 문자열입니다.|
