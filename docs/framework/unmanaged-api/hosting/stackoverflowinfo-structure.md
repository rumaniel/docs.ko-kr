---
title: StackOverflowInfo 구조체
ms.date: 03/30/2017
api_name:
- StackOverflowInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StackOverflowInfo
helpviewer_keywords:
- StackOverflowInfo structure [.NET Framework hosting]
ms.assetid: 519389f2-0217-436c-99d4-93a76ebce5b5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7de5a6d38d43c20ce52f609ef6514a1f28022416
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781132"
---
# <a name="stackoverflowinfo-structure"></a>StackOverflowInfo 구조체
오버플로 인해 throw 된 예외 유형 발생 한 오버플로 및 정보를 저장 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _StackOverflowInfo {  
    StackOverflowType   soType;  
    EXCEPTION_POINTERS  *pExceptionInfo;  
} StackOverflowInfo;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`soType`|값을 [StackOverflowType](../../../../docs/framework/unmanaged-api/hosting/stackoverflowtype-enumeration.md) 오버플로의 형식을 지정 하는 열거형입니다.|  
|`pExceptionInfo`|Win32에 대 한 포인터 `EXCEPTION_POINTERS` 예외가 컴퓨터 독립적 설명과 함께 예외 레코드 및 예외 시 컴퓨터 종속 설명은 프로세서 컨텍스트를 사용 하 여 컨텍스트 레코드를 포함 하는 개체입니다.|  
  
## <a name="remarks"></a>설명  
 A `StackOverflowInfo` 개체를 전달 하는 [iactiononclrevent:: Onevent](../../../../docs/framework/unmanaged-api/hosting/iactiononclrevent-onevent-method.md) 에 대 한 메서드 `Event_StackOverflow` 이벤트입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.idl  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 구조체](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)
