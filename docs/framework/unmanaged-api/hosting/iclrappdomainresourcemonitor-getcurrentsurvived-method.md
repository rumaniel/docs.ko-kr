---
title: ICLRAppDomainResourceMonitor::GetCurrentSurvived 메서드
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor.GetCurrentSurvived
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentSurvived
helpviewer_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentSurvived method [.NET Framework hosting]
- GetCurrentSurvived method [.NET Framework hosting]
ms.assetid: 392e9009-40ef-40e3-ad4d-7ce93a989e78
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bf285b6e1f703c8776937fa33c7ab5801f04f80f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950156"
---
# <a name="iclrappdomainresourcemonitorgetcurrentsurvived-method"></a>ICLRAppDomainResourceMonitor::GetCurrentSurvived 메서드
마지막 전체 차단 가비지 수집을 수행 하 고 현재 응용 프로그램 도메인에서 참조 하는 바이트 수를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT STDMETHODCALLTYPE GetCurrentSurvived(  
             [in]  DWORD dwAppDomainId,  
             [out] ULONGLONG *pAppDomainBytesSurvived,  
             [out] ULONGLONG *pTotalBytesSurvived);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwAppDomainId`  
 진행 요청 된 응용 프로그램 도메인의 ID입니다.  
  
 `pAppDomainBytesSurvived`  
 제한이 이 응용 프로그램 도메인에서 보유 하 고 있는 마지막 가비지 수집 후에도 남아 있는 바이트 수에 대 한 포인터입니다. 전체 수집 후에이 수는 정확 하 고 완전 합니다. 임시 수집 후에이 수는 완료 되지 않을 수 있습니다. 이 매개 변수는 `null`일 수 있습니다.  
  
 `pRuntimeBytesSurvived`  
 제한이 마지막 가비지 수집에서 남아 있는 총 바이트 수에 대 한 포인터입니다. 전체 컬렉션 후에이 수는 관리 되는 힙에서 보유 되는 바이트 수를 나타냅니다. 임시 수집 후에이 수는 임시 생성에 실시간으로 저장 되는 바이트 수를 나타냅니다. 이 매개 변수는 `null`일 수 있습니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|COR_E_APPDOMAINUNLOADED|응용 프로그램 도메인이 언로드 되었거나 존재 하지 않습니다.|  
  
## <a name="remarks"></a>설명  
 통계는 전체 차단 가비지 수집 후에만 업데이트 됩니다. 즉, 컬렉션이 발생 하는 동안 응용 프로그램을 중지 하는 모든 세대를 포함 하는 컬렉션입니다. 예를 들어를 <xref:System.GC.Collect?displayProperty=nameWithType> 메서드 오버 로드는 전체 차단 컬렉션을 수행 합니다. 동시 가비지 수집은 백그라운드에서 발생 하 고 응용 프로그램을 차단 하지 않습니다.  
  
 메서드 `GetCurrentSurvived` 는 관리 되 <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType> 는 속성에 해당 하는 관리 되지 않는 속성입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRAppDomainResourceMonitor 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)
- [애플리케이션 도메인 리소스 모니터링](../../../standard/garbage-collection/app-domain-resource-monitoring.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
