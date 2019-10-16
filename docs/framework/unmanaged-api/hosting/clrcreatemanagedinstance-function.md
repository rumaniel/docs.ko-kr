---
title: ClrCreateManagedInstance 함수
ms.date: 03/30/2017
api_name:
- ClrCreateManagedInstance
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- ClrCreateManagedInstance
helpviewer_keywords:
- ClrCreateManagedInstance function [.NET Framework hosting]
ms.assetid: 58ba42c0-4857-43bf-a039-73a4dc6544c2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e1ae530b8488dcd375e91058a227316dd38cf4ab
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779164"
---
# <a name="clrcreatemanagedinstance-function"></a>ClrCreateManagedInstance 함수
지정 된 관리 되는 형식의 인스턴스를 만듭니다.  
  
 .NET Framework 4에서이 함수에 사용 되지 않습니다. 관리 되는 형식의 인스턴스를 만드는 COM 정품 인증을 사용 하거나 호스팅을 사용 (참조 [인터페이스는.NET Framework 4 및 4.5에 추가 호스트 된 CLR](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)).  
  
## <a name="syntax"></a>구문  
  
```cpp  
STDAPI ClrCreateManagedInstance (  
    [in]  LPCWSTR  pTypeName,   
    [in]  REFIID   riid,   
    [out] void     **ppObject  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pTypeName`  
 [in] 요청 된 인스턴스의 형식 이름에 대 한 포인터입니다.  
  
 `riid`  
 [in] `IID` 요청 중인 인스턴스의 형식입니다.  
  
 `ppObject`  
 [out] 호출자가 요청 된 관리 되는 형식 인스턴스에 대 한 포인터에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 공용 언어 런타임 프로세스를 이미 로드 해야 합니다. 예를 들어,에 대 한 호출을 사용 하 여 로드할 수는 [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 하기 전에 함수를 `ClrCreateManagedInstance` 함수를 호출 합니다. 런타임이 로드 되지 않은 경우 `ClrCreateManagedInstance` 먼저 런타임의 v1.0.3705를 로드 하려고 합니다. 실패 하는 경우 런타임의 최신 버전을 로드 하려고 시도 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
