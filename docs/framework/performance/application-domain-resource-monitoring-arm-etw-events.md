---
title: ARM(응용 프로그램 도메인 리소스 모니터링) ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- ETW, application domain monitoring events
- application domain monitoring events [.NET Framework]
ms.assetid: d38ff268-a2ee-434e-b504-d570880e0289
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f0e4002ae248022a9e4380c79174109494b5e4ca
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046777"
---
# <a name="application-domain-resource-monitoring-arm-etw-events"></a>ARM(응용 프로그램 도메인 리소스 모니터링) ETW 이벤트
<a name="top"></a> 이들 이벤트는 응용 프로그램 도메인 상태에 대한 자세한 진단 정보를 제공합니다. 이들 이벤트를 사용하거나 애플리케이션 도메인 리소스 모니터링(ARM) 기능을 사용하여 같은 정보를 얻을 수 있습니다.  
  
 이 범주는 다음 이벤트로 구성됩니다.  
  
- [ThreadCreated 이벤트](#threadcreated_event)  
  
- [AppDomainMemAllocated 이벤트](#appdomainmemallocated_event)  
  
- [AppDomainMemSurvived 이벤트](#appdomainmemsurvived_event)  
  
- [ThreadAppDomainEnter 이벤트](#threadappdomainenter_event)  
  
- [ThreadTerminated 이벤트](#threadterminated_event)  
  
<a name="threadcreated_event"></a>   
## <a name="threadcreated-event"></a>ThreadCreated 이벤트  
 이 이벤트는 런다운 공급자에서만 `ThreadDC` 로서 발생합니다( `AppDomainResourceManagementRundownKeyword` 키워드에서). 이 이벤트는 이 범주의 런다운 공급자에서 발생하는 유일한 이벤트입니다.  
  
 다음 표에서는 키워드와 수준을 보여 줍니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|정보 제공(4)|  
|`ThreadingKeyword` (0x10000)|정보 제공(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`ThreadCreated`|85|애플리케이션 도메인에 대한 스레드가 만들어졌습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ThreadID|win:UInt64|만들어진 스레드의 ID입니다.|  
|AppDomainID|win:UInt64|스레드 활동이 보고되는 애플리케이션 도메인의 식별자입니다.|  
|플래그|win:UInt32|스레드 만들기 플래그입니다.|  
|ManagedThreadIndex|win:UInt32|만들어진 스레드의 관리되는 인덱스입니다.|  
|OSThreadID|win:UInt32|만들어진 스레드의 운영 체제 ID입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="appdomainmemallocated_event"></a>   
## <a name="appdomainmemallocated-event"></a>AppDomainMemAllocated 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|정보 제공(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`AppDomainMemAllocated`|83|약 4MB의 모든 메모리가 애플리케이션 도메인에서 할당됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|AppDomainID|win:UInt64|리소스 사용량이 보고되는 애플리케이션 도메인의 식별자입니다.|  
|Allocated|win:UInt64|애플리케이션 도메인이 만들어진 후 이 애플리케이션 도메인에서 할당된 총 바이트 수입니다(해제된 메모리 양을 빼지 않음).|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="appdomainmemsurvived_event"></a>   
## <a name="appdomainmemsurvived-event"></a>AppDomainMemSurvived 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|정보 제공(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`AppDomainMemSurvived`|84|각 가비지 수집이 종료되었습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|AppDomainID|win:UInt64|리소스 사용량이 보고되는 도메인의 식별자입니다.|  
|Survived|win:UInt64|마지막 수집 후에도 유지되고 이 애플리케이션 도메인에 저장되는 것으로 알려진 바이트 수입니다. 이 수는 전체 수집 후에 정확하고 완전하지만 임시 수집 후에는 불완전할 수 있습니다.|  
|ProcessSurvived|win:UInt64|마지막 수집에서 유지된 총 바이트 수입니다. 전체 수집 후에 이 수는 관리되는 힙에 실시간으로 저장되는 바이트 수를 나타냅니다. 임시 수집 후에 이 수는 임시 생성에 실시간으로 저장되는 바이트 수를 나타냅니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="threadappdomainenter_event"></a>   
## <a name="threadappdomainenter-event"></a>ThreadAppDomainEnter 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|정보 제공(4)|  
|`ThreadingKeyword` (0x10000)|정보 제공(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`ThreadAppDomainEnter`|87|스레드가 애플리케이션 도메인에 들어갑니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ThreadID|win:UInt64|스레드 식별자입니다.|  
|AppDomainID|win:UInt64|애플리케이션 도메인 식별자입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="threadterminated_event"></a>   
## <a name="threadterminated-event"></a>ThreadTerminated 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|수준|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|정보 제공(4)|  
|`ThreadingKeyword` (0x10000)|정보 제공(4)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`ThreadTerminated`|86|스레드가 종료됩니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|ThreadID|win:UInt64|스레드 식별자입니다.|  
|AppDomainID|win:UInt64|애플리케이션 도메인 식별자입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
