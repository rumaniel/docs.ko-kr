---
title: _EFN_GetManagedObjectName 함수
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedObjectName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedObjectName
helpviewer_keywords:
- _EFN_GetManagedObjectName function [.NET Framework debugging]
ms.assetid: 6e7c6bee-7ced-495f-bf6c-2a5f0c716f7e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d3490477f30cd1c0badaa9cfd71433a5bf9d7a99
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738986"
---
# <a name="efngetmanagedobjectname-function"></a>\_EFN\_GetManagedObjectName Function
제공 된 관리 되는 개체 포인터를 사용 하는 형식의 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT _EFN_GetManagedObjectName(  
    [in]  PDEBUG_CLIENT  Client,  
    [in]  ULONG64        objAddr,  
    [out] __out_ecount(cbName) PSTR szName,  
    [out] ULONG          cbName  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `Client`  
 [in] 디버그 클라이언트에 대 한 포인터입니다.  
  
 `objAddr`  
 [in] 관리 되는 개체 포인터입니다.  
  
 szName  
 [out] 형식의 이름입니다.  
  
 `cbName`  
 [out] 문자열 버퍼에서 사용할 수 있는 문자의 수입니다.  
  
## <a name="remarks"></a>설명  
 관리 되는 코드가 없는 스레드에서 현재 컨텍스트에서 함수 HRESULT SOS_E_NOMANAGEDCODE 0xa0 기능 값 및 0x1000의 오류 코드를 사용 하 여 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** SOS_Stacktrace.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 전역 정적 함수](../../../../docs/framework/unmanaged-api/debugging/debugging-global-static-functions.md)
