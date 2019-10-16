---
title: ICLRDomainManager::SetPropertiesForDefaultAppDomain 메서드
ms.date: 03/30/2017
api_name:
- ICLRDomainManager.SetPropertiesForDefaultAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain
helpviewer_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
- SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
ms.assetid: 43e61c4b-c435-45ec-9ef6-c68403aa4200
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cfd7c835cdc4b53c753d714216d1745eb0b80c2d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772937"
---
# <a name="iclrdomainmanagersetpropertiesfordefaultappdomain-method"></a>ICLRDomainManager::SetPropertiesForDefaultAppDomain 메서드
기본 응용 프로그램 도메인을 초기화 하는 데 사용할 수 있는 속성을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetPropertiesForDefaultAppDomain(  
    [in] DWORD nProperties,  
    [in] LPCWSTR *pwszPropertyNames,  
    [in] LPCWSTR *pwszPropertyValues  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `nProperties`  
 [in] 항목 수가 `pwszPropertyNames` 고 `pwszPropertyValues`입니다.  
  
 `pwszPropertyNames`  
 [in] 배열 속성 이름 또는 속성이 없는 경우 null입니다. 현재이 메서드에서 인식할 수 있는 유일한 속성 이름을 "PARTIAL_TRUST_VISIBLE_ASSEMBLIES"입니다.  
  
 `pwszPropertyValues`  
 [in] 배열 속성 값 또는 속성이 없는 경우 null입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|HRESULT_FROM_WIN32(ERROR_UNKNOWN_PROPERTY)|`pwszPropertyNames` 이 방법으로 인식 되지 않는 속성 이름을 포함 합니다.|  
  
## <a name="remarks"></a>설명  
 "PARTIAL_TRUST_VISIBLE_ASSEMBLIES"에 대 한 속성 값은 조건부가 있는 어셈블리 목록 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> (APTCA) 특성을 <xref:System.Security.PartialTrustVisibilityLevel.NotVisibleByDefault?displayProperty=nameWithType> 기본 응용 프로그램에서 부분적으로 신뢰할 수 있는 호출자에 게 표시 되어야 하는 플래그 도메인입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
- [ICLRDomainManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrdomainmanager-interface.md)
