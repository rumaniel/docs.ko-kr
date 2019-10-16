---
title: ICLRHostBindingPolicyManager::ModifyApplicationPolicy 메서드
ms.date: 03/30/2017
api_name:
- ICLRHostBindingPolicyManager.ModifyApplicationPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostBindingPolicyManager::ModifyApplicationPolicy
helpviewer_keywords:
- ICLRHostBindingPolicyManager::ModifyApplicationPolicy method [.NET Framework hosting]
- ModifyApplicationPolicy method [.NET Framework hosting]
ms.assetid: d82d633e-cce6-427c-8b02-8227e34e12ba
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0a9e438e6dd436303cd6f7aa60c779179b5d3c04
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779666"
---
# <a name="iclrhostbindingpolicymanagermodifyapplicationpolicy-method"></a>ICLRHostBindingPolicyManager::ModifyApplicationPolicy 메서드
지정된 된 어셈블리에 대 한 바인딩 정책 수정 하 고 정책의 새 버전을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT  ModifyApplicationPolicy (  
    [in] LPCWSTR     pwzSourceAssemblyIdentity,   
    [in] LPCWSTR     pwzTargetAssemblyIdentity,  
    [in] BYTE       *pbApplicationPolicy,  
    [in] DWORD       cbAppPolicySize,  
    [in] DWORD       dwPolicyModifyFlags,  
    [out, size_is(*pcbNewAppPolicySize)] BYTE *pbNewApplicationPolicy,   
    [in, out] DWORD *pcbNewAppPolicySize  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pwzSourceAssemblyIdentity`  
 [in] 수정할 어셈블리의 id입니다.  
  
 `pwzTargetAssemblyIdentity`  
 [in] 수정 된 어셈블리의 새 id입니다.  
  
 `pbApplicationPolicy`  
 [in] 수정 하려면 어셈블리에 대 한 바인딩 정책 데이터를 포함 하는 버퍼에 대 한 포인터입니다.  
  
 `cbAppPolicySize`  
 [in] 크기 교체 바인딩 정책입니다.  
  
 `dwPolicyModifyFlags`  
 [in] 논리 OR 조합을 [EHostBindingPolicyModifyFlags](../../../../docs/framework/unmanaged-api/hosting/ehostbindingpolicymodifyflags-enumeration.md) 의도치 않은 리디렉션의 컨트롤을 나타내는 값입니다.  
  
 `pbNewApplicationPolicy`  
 [out] 새 바인딩 정책 데이터를 포함 하는 버퍼에 대 한 포인터입니다.  
  
 `pcbNewAppPolicySize`  
 [out에서] 새 바인딩 정책 버퍼의 크기에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|정책을 수정 했습니다.|  
|E_INVALIDARG|`pwzSourceAssemblyIdentity` 또는 `pwzTargetAssemblyIdentity` null 참조 되었습니다.|  
|ERROR_INSUFFICIENT_BUFFER|`pbNewApplicationPolicy` 너무 작습니다.|  
|HOST_E_CLRNOTAVAILABLE|프로세스에는 CLR (공용 언어 런타임)에 로드 되지 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. E_FAIL을 반환 하는 메서드를 CLR 더 이상 프로세스 내에서 사용 가능 합니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
  
## <a name="remarks"></a>설명  
 `ModifyApplicationPolicy` 메서드를 두 번 호출할 수 있습니다. 첫 번째 호출에 null 값을 제공 해야 합니다 `pbNewApplicationPolicy` 매개 변수입니다. 이 호출은 필요한 값으로 반환 `pcbNewAppPolicySize`합니다. 두 번째 호출에 대 한이 값을 제공 해야 `pcbNewAppPolicySize`에 대 한 크기의 버퍼를 가리킵니다 `pbNewApplicationPolicy`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRHostBindingPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrhostbindingpolicymanager-interface.md)
