---
title: GetRequestedRuntimeVersionForCLSID 함수
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeVersionForCLSID
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeVersionForCLSID
helpviewer_keywords:
- GetRequestedRuntimeVersionForCLSID function [.NET Framework hosting]
ms.assetid: 5bb12f9a-0612-434b-b4ed-2db636a20bec
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9dfce10c94e04dcd405e06ab6d0984e64984709e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779558"
---
# <a name="getrequestedruntimeversionforclsid-function"></a>GetRequestedRuntimeVersionForCLSID 함수
적절 한 공용 언어 런타임 (CLR) 버전 정보가 지정 된 클래스에 대 한 가져옵니다 `CLSID`합니다.  
  
 .NET Framework 4에서이 함수에 사용 되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRequestedRuntimeVersionForCLSID (  
    [in]  REFCLSID   rclsid,   
    [out]  LPWSTR     pVersion,   
    [in]  DWORD      cchBuffer,   
    [out] DWORD*     dwLength,   
    [in]  CLSID_RESOLUTION_FLAGS dwResolutionFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `rclsid`  
 [in]  `CLSID` 구성 요소입니다.  
  
 `pVersion`  
 [out]  성공적으로 완료 되는 버전 번호 문자열을 포함 하는 버퍼입니다.  
  
 `cchBuffer`  
 [in]  와이드 문자에서 크기의는 `pVersion` 버퍼입니다.  
  
 `dwLength`  
 [out] 반환된 된 버퍼의 길이 (바이트) 합니다.  
  
 `dwResolutionFlags`  
 [in]  CLSID_RESOLUTION_FLAGS 값 중 하나입니다. 다음 값이 지원 됩니다.  
  
- CLSID_RESOLUTION_DEFAULT: (0x0) 기본 interop 동작을 사용 해야 함을 지정 합니다.  
  
- CLSID_RESOLUTION_REGISTERED: (0x1) 검색 해야 하는 레지스트리 및 적용할 shim 정책을 지정 합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|함수 반환 되었습니다.|  
|E_INVALIDARG|매개 변수 중 하나에 잘못 된 형식 또는 형식입니다.|  
|ERROR_INSUFFICIENT_BUFFER|`pVersion` 버퍼가 전체 버전 문자열을 저장할 만큼 충분히 커야 합니다.|  
|REGDB_E_CLASSNOTREG|지정 된 등록 클래스인 `CLSID`합니다.|  
|E_POINTER|`dwLength` 이 null 또는 `cchBuffer` 버전 문자열을 포함할 수 있도록 충분히 큰 있지만 `pVersion` null입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
