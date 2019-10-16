---
title: CoInitializeEE 함수
ms.date: 03/30/2017
api_name:
- CoInitializeEE
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoInitializeEE
helpviewer_keywords:
- CoInitializeEE function [.NET Framework hosting]
ms.assetid: 7e42a928-5068-4ba6-b8c3-806551a01fa8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 72b95b634ffc352b7fad006e0ccd68e6e159dee9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779111"
---
# <a name="coinitializeee-function"></a>CoInitializeEE 함수
공용 언어 런타임 실행 엔진 프로세스에 로드 되도록 합니다. 이 함수는.NET Framework 4에서 사용 되지 않습니다. 사용 된 [iclrruntimehost:: Start](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-start-method.md) 메서드 대신 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CoInitializeEE (  
   [in] DWORD fFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fFlags`  
 [in] 중 하나는 [COINITIEE](../../../../docs/framework/unmanaged-api/metadata/coinitiee-enumeration.md) 열거형 상수입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음 표에서 값과 Winerror.h에 정의 된 대로 표준 COM 오류 코드를 반환 합니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|S_OK|실행 엔진을 로드 했습니다.|  
|S_FALSE|실행 엔진 이미 로드 되었습니다.|  
|E_FAIL|실행 엔진을 로드할 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 이 메서드는 이전에 로드 되지 않았으면 하는 경우 실행 엔진을 로드 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 전역 정적 함수](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
