---
title: ICLRRuntimeInfo::BindAsLegacyV2Runtime 메서드
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.BindAsLegacyV2Runtime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::BindAsLegacyV2Runtime
helpviewer_keywords:
- ICLRRuntimeInfo::BindAsLegacyV2Runtime method [.NET Framework hosting]
- BindAsLegacyV2Runtime method [.NET Framework hosting]
ms.assetid: 65fd55ac-4a24-4479-9384-a2e8013bfb2b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a0ea4bd222500015f6c78cb0455539aa2c24e681
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67765610"
---
# <a name="iclrruntimeinfobindaslegacyv2runtime-method"></a>ICLRRuntimeInfo::BindAsLegacyV2Runtime 메서드
모든 레거시 공용 언어 런타임 (CLR) 버전 2 정품 인증 정책 결정에 대 한 현재 런타임에 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT BindAsLegacyV2Runtime ();  
```  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 Hresult를 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|바인딩 성공 하거나 레거시 CLR 버전 2 정품 인증 정책 런타임이 이미이 런타임 바인딩 되었습니다.|  
|CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND|다양 한 런타임 이미 레거시 CLR 버전 2 정품 인증 정책에 바인딩 되었습니다.|  
  
## <a name="remarks"></a>설명  
 모든 레거시 CLR 버전 2 정품 인증 정책 결정에 대 한 현재 런타임에 이미 바인딩되어 있으면 (사용 하 여 예를 들어,를 `useLegacyV2RuntimeActivationPolicy` 특성을 합니다 [ \<시작 > 요소](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) 구성 파일에서),이 메서드 오류 결과;를 반환 하지 않습니다. 대신, 결과 S_OK를 메서드가 레거시 활성화 정책이 성공적으로 바인딩할 경우 것 처럼입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRRuntimeInfo 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
- [\<startup> 요소](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)
