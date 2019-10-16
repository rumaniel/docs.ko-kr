---
title: IGCHost 인터페이스
ms.date: 03/30/2017
api_name:
- IGCHost
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IGCHost
helpviewer_keywords:
- IGCHost interface [.NET Framework hosting]
ms.assetid: 9ad70ffd-6963-4ab2-8c84-3d86c3fb8deb
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1d3f588bfc9799ed4591114b28d081ab417678b1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914805"
---
# <a name="igchost-interface"></a>IGCHost 인터페이스
가비지 컬렉션 시스템에 대 한 정보를 가져오고 가비지 수집의 일부 측면을 제어 하기 위한 메서드를 제공 합니다.  
  
> [!NOTE]
> 4\.5 .NET Framework부터 [IGCHost2:: SetGCStartupLimitsEx](../../../../docs/framework/unmanaged-api/hosting/igchost2-setgcstartuplimitsex-method.md) 메서드를 사용 하 여 가비지 수집 세그먼트의 크기와 가비지 수집 시스템 `DWORD` 의 최대 크기를 설정 하는 데 사용할 수 있습니다. [SetGCStartupLimits](../../../../docs/framework/unmanaged-api/hosting/igchost-setgcstartuplimits-method.md) 메서드에 의해 적용 되는 제한입니다.  
  
> [!NOTE]
> 이 인터페이스는 전문 용도로만 사용 됩니다. 응용 프로그램의 성능에 영향을 줄 수 있습니다 (잘못 사용 되는 경우).  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[Collect 메서드](../../../../docs/framework/unmanaged-api/hosting/igchost-collect-method.md)|현재 가비지 컬렉션의 상태에 관계 없이 지정 된 세대에 대해 컬렉션을 강제로 실행 합니다.|  
|[GetStats 메서드](../../../../docs/framework/unmanaged-api/hosting/igchost-getstats-method.md)|가비지 수집 시스템의 현재 상태에 대 한 통계를 가져옵니다.|  
|[GetThreadStats 메서드](../../../../docs/framework/unmanaged-api/hosting/igchost-getthreadstats-method.md)|가비지 수집에 대 한 스레드별 통계를 가져옵니다.|  
|[SetGCStartupLimits 메서드](../../../../docs/framework/unmanaged-api/hosting/igchost-setgcstartuplimits-method.md)|0 세대의 세그먼트 크기와 최대 크기를 설정 합니다.|  
|[SetVirtualMemLimit 메서드](../../../../docs/framework/unmanaged-api/hosting/igchost-setvirtualmemlimit-method.md)|런타임 가상 메모리의 최대 크기를 설정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** GCHost.idl, GCHost.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [CorRuntimeHost Coclass](../../../../docs/framework/unmanaged-api/hosting/corruntimehost-coclass.md)
