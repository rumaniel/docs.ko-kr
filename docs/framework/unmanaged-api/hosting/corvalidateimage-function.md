---
title: _CorValidateImage 함수
ms.date: 03/30/2017
api_name:
- _CorValidateImage
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- _CorValidateImage
helpviewer_keywords:
- _CorValidateImage function [.NET Framework hosting]
ms.assetid: 0117e080-05f9-4772-885d-e1847230947c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a6f1d76ef5cf36bcbab29a33647520663f822798
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67770031"
---
# <a name="corvalidateimage-function"></a>_CorValidateImage 함수
관리 되는 모듈 이미지의 유효성을 검사 하 고 로드 된 후 운영 체제 로더에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
STDAPI _CorValidateImage (   
   [in] PVOID* ImageBase,  
   [in] LPCWSTR FileName  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ImageBase`  
 [in] 관리 되는 코드를 유효성을 검사할 이미지의 시작 위치에 대 한 포인터입니다. 이미지는 이미 메모리에 로드 되어야 합니다.  
  
 `FileName`  
 [in] 이미지의 파일 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 이 함수는 표준 값 반환 `E_INVALIDARG`, `E_OUTOFMEMORY`를 `E_UNEXPECTED`, 및 `E_FAIL`, 다음 값 뿐만 아니라 합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|`STATUS_INVALID_IMAGE_FORMAT`|이미지가 올바르지 않습니다. 이 값은 HRESULT 0xC000007BL.|  
|`STATUS_SUCCESS`|올바른 이미지가입니다. 이 값은 HRESULT 0x00000000L.|  
  
## <a name="remarks"></a>설명  
 Windows XP 이상 버전에서 운영 체제 로더는 공용 개체 파일 형식 (COFF) 헤더의 COM 설명자 디렉터리 비트를 검사 하 여 관리 되는 모듈에 대 한 확인 합니다. 설정 비트는 관리 되는 모듈을 나타냅니다. MsCorEE.dll 및 호출 로드 로더는 관리 되는 모듈을 검색 하는 경우 `_CorValidateImage`, 다음 작업을 수행 하는:  
  
- 이미지 관리 되는 유효한 모듈 인지 확인 합니다.  
  
- CLR (공용 언어 런타임)의 진입점으로 이미지의 진입점을 변경합니다.  
  
- 64 비트 버전 Windows의 경우 PE32에서 PE32 + 형식으로 변환 하 여 메모리에 있는 이미지를 수정 합니다.  
  
- 관리 되는 모듈 이미지가 로드 될 때 로더를 반환 합니다.  
  
 실행 가능 이미지는 운영 체제 로더 호출을 [_CorExeMain](../../../../docs/framework/unmanaged-api/hosting/corexemain-function.md) 실행 파일에 지정 된 진입점에 관계 없이 함수입니다. 로더가 DLL 어셈블리 이미지에 대 한 호출을 [_CorDllMain](../../../../docs/framework/unmanaged-api/hosting/cordllmain-function.md) 함수입니다.  
  
 `_CorExeMain` 또는 `_CorDllMain` 다음 작업을 수행 합니다.  
  
- CLR을 초기화합니다.  
  
- 어셈블리의 CLR 헤더에서 관리 되는 진입점을 찾습니다.  
  
- 실행을 시작합니다.  
  
 로더 호출을 [_CorImageUnloading](../../../../docs/framework/unmanaged-api/hosting/corimageunloading-function.md) 관리 되는 경우 함수 모듈 이미지가 로드 되지 합니다. 그러나이 함수는 작업을 수행 하지 않습니다. 만 반환합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 전역 정적 함수](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
