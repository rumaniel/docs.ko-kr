---
title: _EFN_GetManagedObjectFieldInfo 함수
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedObjectFieldInfo
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedObjectFieldInfo
helpviewer_keywords:
- _EFN_GetManagedObjectFieldInfo function [.NET Framework debugging]
ms.assetid: 3b93bcff-62a4-47b2-babc-6bcf4216119a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c1de0b3b05d38c1fec38b9436c653973dfaa4136
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739006"
---
# <a name="efngetmanagedobjectfieldinfo-function"></a>\_EFN\_GetManagedObjectFieldInfo Function
제공된 개체 포인터와 필드 이름을 사용하여 개체 시작부터 필드 및 필드 값까지의 오프셋을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT _EFN_GetManagedObjectFieldInfo(  
    [in]  PDEBUG_CLIENT Client,  
    [in]  ULONG64       objAddr,  
    [in]  __out_ecount (mdNameLen) PSTR szFieldName,  
    [out] PULONG64      pValue,  
    [out] PULONG        pOffset  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `Client`  
 [in] 디버그 클라이언트에 대 한 포인터입니다.  
  
 `objAddr`  
 [in] 관리 되는 개체 포인터입니다.  
  
 szFieldName  
 [in] 필드 이름 관리 되는 개체 포인터입니다.  
  
 `pValue`  
 [out] 필드 값입니다. 이 매개 변수는 null일 수 있습니다.  
  
 `pOffset`  
 [out] 오프셋 `objAddr` 필드입니다. 이 매개 변수는 null일 수 있습니다.  
  
## <a name="remarks"></a>설명  
 오프셋 0 인 경우 오프셋 없이 기록 됩니다.  
  
 관리 되는 코드가 없는 스레드에서 현재 컨텍스트에서 함수 HRESULT SOS_E_NOMANAGEDCODE 0xa0 기능 값 및 0x1000의 오류 코드를 사용 하 여 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** SOS_Stacktrace.h  
  
 **.NET framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 전역 정적 함수](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)
