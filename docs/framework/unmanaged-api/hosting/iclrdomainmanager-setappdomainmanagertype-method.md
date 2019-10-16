---
title: ICLRDomainManager::SetAppDomainManagerType 메서드
ms.date: 03/30/2017
api_name:
- ICLRDomainManager.SetAppDomainManagerType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager::SetAppDomainManagerType
helpviewer_keywords:
- SetAppDomainManagerType method, ICLRDomainManager interface [.NET Framework hosting]
- ICLRDomainManager::SetAppDomainManagerType method [.NET Framework hosting]
ms.assetid: ee91abb0-cb74-41dd-927b-e117fb8ffdf4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b142f1a05036eddf44c69d8b7da95091dc8f445
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963099"
---
# <a name="iclrdomainmanagersetappdomainmanagertype-method"></a>ICLRDomainManager::SetAppDomainManagerType 메서드
기본 응용 프로그램 도메인을 초기화 하 <xref:System.AppDomainManager?displayProperty=nameWithType> 는 데 사용 되는 응용 프로그램 도메인 관리자의 클래스에서 파생 된 형식을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetAppDomainManagerType(  
    [in] LPCWSTR wszAppDomainManagerAssembly,  
    [in] LPCWSTR wszAppDomainManagerType,  
    [in] EInitializeNewDomainFlags dwInitializeDomainFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszAppDomainManagerAssembly`  
 진행 응용 프로그램 도메인 관리자 유형을 포함 하는 어셈블리의 표시 이름입니다. 예를 들어: "AdMgrExample, Version = 1.0.0.0, Culture = 중립, PublicKeyToken = 6856bccf150f00b3".  
  
 `wszAppDomainManagerType`  
 진행 네임 스페이스를 포함 하는 응용 프로그램 도메인 관리자의 유형 이름입니다.  
  
 `dwInitializeDomainFlags`  
 진행 응용 프로그램 도메인 관리자에 대 한 정보를 제공 하는 [EInitializeNewDomainFlags](../../../../docs/framework/unmanaged-api/hosting/einitializenewdomainflags-enumeration.md) 열거형 값의 조합입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR (공용 언어 런타임)이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
  
## <a name="remarks"></a>설명  
 현재에 대해 `dwInitializeDomainFlags` 정의 된 유일한 값은 `eInitializeNewDomainFlags_NoSecurityChanges`이며,이는 응용 프로그램 도메인 관리자가 <xref:System.AppDomainManager.InitializeNewDomain%2A?displayProperty=nameWithType> 메서드를 실행 하는 동안 보안 설정을 수정 하지 않음을 CLR (공용 언어 런타임)에 지시 하는입니다. 이렇게 하면 CLR에서 조건부 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> (APTCA) 특성이 있는 어셈블리 로드를 최적화할 수 있습니다. 이로 인해이 어셈블리 집합의 전이적 클로저가 큰 경우 시작 시간이 크게 향상 될 수 있습니다.  
  
> [!IMPORTANT]
> 호스트에서 응용 프로그램 `eInitializeNewDomainFlags_NoSecurityChanges` 도메인 관리자 <xref:System.InvalidOperationException> 를 지정 하는 경우 응용 프로그램 도메인의 보안을 수정 하려고 시도 하면이 throw 됩니다.  
  
 [ICLRControl:: SetAppDomainManagerType](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-setappdomainmanagertype-method.md)메서드를 호출 하는 것은 `ICLRDomainManager::SetAppDomainManagerType` 로 `eInitializeNewDomainFlags_None`를 호출 하는 것과 같습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
- [ICLRDomainManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrdomainmanager-interface.md)
- [EInitializeNewDomainFlags 열거형](../../../../docs/framework/unmanaged-api/hosting/einitializenewdomainflags-enumeration.md)
