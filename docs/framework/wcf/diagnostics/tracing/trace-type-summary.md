---
title: 추적 형식 요약
ms.date: 03/30/2017
ms.assetid: e639410b-d1d1-479c-b78e-a4701d4e4085
ms.openlocfilehash: 8f54f71ef63338708a29fac5557c7c7e8f257f58
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856003"
---
# <a name="trace-type-summary"></a>추적 형식 요약
[원본 수준은](https://go.microsoft.com/fwlink/?LinkID=94943) 다음과 같은 다양 한 추적 수준을 정의 합니다. 중요, 오류, 경고, 정보 및 자세한 정보를 제공 하며 `ActivityTracing` 플래그에 대 한 설명을 제공 합니다 .이 플래그는 추적 경계와 활동 전송 이벤트의 출력을 전환 합니다.  
  
 에서<xref:System.Diagnostics>내보낼 수 있는 추적 형식에 대 한 [traceeventtype](https://go.microsoft.com/fwlink/?LinkId=95169) 을 검토할 수도 있습니다.  
  
 다음 표에서는 가장 중요한 항목을 보여 줍니다.  
  
|추적 형식|설명|  
|----------------|-----------------|  
|중요|오류 또는 애플리케이션 충돌|  
|오류|복구할 수 있는 오류|  
|경고|알림 메시지|  
|정보|중요하지 않은 문제|  
|자세히|추적 디버깅|  
|시작|처리의 논리 단위 시작|  
|일시 중단|처리의 논리 단위 일시 중단|  
|다시 시작|처리의 논리 단위 다시 시작|  
|Stop|처리의 논리 단위 중지|  
|전송|상관 관계 ID의 변경|  
  
 동작은 위의 추적 형식의 조합으로 정의됩니다.  
  
 다음은 로컬(추적 소스) 범위에서 이상적인 동작을 정의하는 정규식입니다.  
  
 `R = Start (Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop`  
  
 이는 동작이 다음 조건을 만족해야 함을 의미합니다.  
  
- Start 및 Stop 추적에 의해 각각 시작되고 중지되어야 합니다.  
  
- Suspend 추적 또는 Resume 추적의 바로 앞에 Transfer 추적이 있어야 합니다.  
  
- Suspend 추적 및 Resume 추적이 존재할 경우 이 사이에 추적이 있으면 안 됩니다.  
  
- 위와 같은 조건이 충족되는 한 Critical/Error/Warning/Information/Verbose/Transfer 추적은 여러 개가 있을 수 있습니다.  
  
 다음은 전역 범위에서 이상적인 동작을 정의하는 정규식입니다.  
  
`R+`  
  
 로컬 범위에서 동작에 대한 정규식인 R을 포함합니다. 이는 다음으로 변환됩니다.  
  
`[R+ = Start ( Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop]+`
