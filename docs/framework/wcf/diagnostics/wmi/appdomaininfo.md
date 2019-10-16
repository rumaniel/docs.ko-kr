---
title: AppDomainInfo
ms.date: 03/30/2017
ms.assetid: 6610b7d8-81eb-4bec-a543-9b72ad7b6f73
ms.openlocfilehash: 0b7f8aadbd9a9dfcdd33fc65be3a5a41ea95f5be
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61964257"
---
# <a name="appdomaininfo"></a>AppDomainInfo
애플리케이션 도메인 정보  
  
## <a name="syntax"></a>구문  
  
```csharp
class AppDomainInfo  
{  
  sint32 AppDomainId;  
  boolean IsDefault;  
  boolean LogMalformedMessages;  
  boolean LogMessagesAtServiceLevel;  
  boolean LogMessagesAtTransportLevel;  
  TraceListener MessageLoggingTraceListeners[];  
  string Name;  
  string PerformanceCounters;  
  sint32 ProcessId;  
  string ServiceConfigPath;  
  string TraceLevel;  
  TraceListener wmiTraceListeners[];  
};  
```  
  
## <a name="methods"></a>메서드  
 AppDomainInfo 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 AppDomainInfo 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="appdomainid"></a>AppDomainId  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 appdomain의 ID입니다.  
  
### <a name="isdefault"></a>IsDefault  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 appdomain이 기본 appdomain인지 여부를 나타냅니다.  
  
### <a name="logmalformedmessages"></a>LogMalformedMessages  
 데이터 형식: boolean  
  
 액세스 형식: 읽기/쓰기  
  
 잘못된 형식의 메시지를 기록할지 여부를 지정하는 값입니다.  
  
### <a name="logmessagesatservicelevel"></a>LogMessagesAtServiceLevel  
 데이터 형식: boolean  
  
 액세스 형식: 읽기/쓰기  
  
 암호화 및 전송 관련 변형 전에 메시지를 서비스 수준에서 추적할지 여부를 지정하는 값입니다.  
  
### <a name="logmessagesattransportlevel"></a>LogMessagesAtTransportLevel  
 데이터 형식: boolean  
  
 액세스 형식: 읽기/쓰기  
  
 메시지를 전송 수준에서 추적할지 여부를 지정하는 값입니다.  
  
### <a name="messageloggingtracelisteners"></a>MessageLoggingTraceListeners  
 데이터 형식: TraceListener 배열  
  
 액세스 형식: 읽기 전용  
  
 System.Wmi.MessageLogging 추적 소스를 수신 대기하는 컬렉션 추적 수신기입니다.  
  
### <a name="name"></a>이름  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 appdomain의 이름입니다.  
  
### <a name="performancecounters"></a>PerformanceCounters  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 appdomain의 활성 성능 카운터의 범위입니다.  
  
### <a name="processid"></a>ProcessId  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 프로세스 ID입니다.  
  
### <a name="serviceconfigpath"></a>ServiceConfigPath  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 서비스의 구성 경로입니다.  
  
### <a name="tracelevel"></a>TraceLevel  
 데이터 형식: string  
  
 액세스 형식: 읽기/쓰기  
  
 System.Wmi 추적 소스의 추적 수준입니다.  
  
### <a name="servicemodeltracelisteners"></a>ServiceModelTraceListeners  
 데이터 형식: TraceListener 배열  
  
 액세스 형식: 읽기 전용  
  
 System.ServiceModel 추적 소스의 수신기 컬렉션입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|
