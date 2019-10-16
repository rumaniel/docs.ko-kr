---
title: ICLRProbingAssemblyEnum::Get 메서드
ms.date: 03/30/2017
api_name:
- ICLRProbingAssemblyEnum.Get
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRProbingAssemblyEnum::Get
helpviewer_keywords:
- Get method, ICLRProbingAssemblyEnum interface [.NET Framework hosting]
- ICLRProbingAssemblyEnum::Get method [.NET Framework hosting]
ms.assetid: fdb67a77-782f-44cf-a8a1-b75999b0f3c8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3225e42df44e719ecde31c26fae70f26731fa157
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67761591"
---
# <a name="iclrprobingassemblyenumget-method"></a>ICLRProbingAssemblyEnum::Get 메서드
지정된 된 인덱스에서 어셈블리 id를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Get (  
    [in] DWORD dwIndex,  
    [out, size_is(*pcchBufferSize)] LPWSTR pwzBuffer,  
    [in, out] DWORD *pcchBufferSize  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwIndex`  
 [in] 반환할 어셈블리 id의 0부터 시작 하는 인덱스입니다.  
  
 `pwzBuffer`  
 [out] 어셈블리 id 데이터를 포함 하는 버퍼입니다.  
  
 `pcchBufferSize`  
 [out에서] 크기는 `pwzBuffer` 버퍼입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|`Get` 성공적으로 반환 합니다.|  
|ERROR_INSUFFICIENT_BUFFER|`pwzBuffer` 너무 작습니다.|  
|ERROR_NO_MORE_ITEMS|열거형에는 더 이상 항목이 포함 됩니다.|  
|HOST_E_CLRNOTAVAILABLE|프로세스에는 CLR (공용 언어 런타임)에 로드 되지 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 호스팅 메서드를 이후에 호출 HOST_E_CLRNOTAVAILABLE를 반환합니다.|  
  
## <a name="remarks"></a>설명  
 인덱스 0에 id에는 프로세서 아키텍처의 id가입니다. 인덱스 1에 있는 id에는 MSIL (Microsoft intermediate language)에 대 한 아키텍처 중립 어셈블리입니다. 인덱스 2에 id 아키텍처 정보가 없습니다.  
  
 `Get` 두 번 호출 일반적으로 됩니다. 첫 번째 호출에 대 한 null 값이 제공 `pwzBuffer`를 설정 하 고 `pcchBufferSize` 에 대 한 적절 한 크기로 `pwzBuffer`합니다. 두 번째 호출을 적절 하 게 크기가 제공 `pwzBuffer`, 완료 되 면 정식 어셈블리 id 데이터를 포함 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRProbingAssemblyEnum 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrprobingassemblyenum-interface.md)
- [ICLRAssemblyIdentityManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-interface.md)
