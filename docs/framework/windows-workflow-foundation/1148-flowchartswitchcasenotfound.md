---
title: 1148 - FlowchartSwitchCaseNotFound
ms.date: 03/30/2017
ms.assetid: 9ee7fcee-e040-4306-968e-ed840a1cb00c
ms.openlocfilehash: 7e96b5b7652d404e6fdbe2c04c6a4069ca78f20f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009918"
---
# <a name="1148---flowchartswitchcasenotfound"></a>1148 - FlowchartSwitchCaseNotFound
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|ID|1148|  
|키워드|WFActivities|  
|수준|정보|  
|채널|Microsoft-Windows-애플리케이션 서버-애플리케이션/디버그|  
  
## <a name="description"></a>설명  
 Flowchart 스위치에서 일치 사례 또는 기본 사례를 찾을 수 있음을 나타냅니다. Flowchart 실행이 종료됩니다.  
  
## <a name="message"></a>메시지  
 Flowchart '%1'/FlowSwitch - Expression 결과와 일치하는 Case 작업 및 Default Case를 찾을 수 없습니다. Flowchart 실행이 종료됩니다.  
  
## <a name="details"></a>설명  
  
|데이터 항목 이름|데이터 항목 형식|설명|  
|--------------------|--------------------|-----------------|  
|FlowChart|xs:string|FlowChart의 표시 이름입니다.|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName에서 반환되는 문자열입니다.|
