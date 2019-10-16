---
title: CreateAssemblyEnum 함수
ms.date: 03/30/2017
api_name:
- CreateAssemblyEnum
api_location:
- fusion.dll
- clr.dll
- mscorwks.dll
api_type:
- DLLExport
f1_keywords:
- CreateAssemblyEnum
helpviewer_keywords:
- CreateAssemblyEnum function [.NET Framework fusion]
ms.assetid: 3506df38-6cea-42f6-946e-4287863bcfb3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1db72c44b53b5abff9aee35094abc1e0e577fad4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795383"
---
# <a name="createassemblyenum-function"></a>CreateAssemblyEnum 함수
지정 된 [IAssemblyName](iassemblyname-interface.md)를 사용 하 여 어셈블리의 개체를 열거할 수 있는 [iassemblyenum](iassemblyenum-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateAssemblyEnum (  
    [out] IAssemblyEnum  **pEnum,  
    [in]  IUnknown       *pUnkReserved,  
    [in]  IAssemblyName  *pName,  
    [in]  DWORD          dwFlags,  
    [in]  LPVOID         pvReserved  
 );  
```  
  
## <a name="parameters"></a>매개 변수  
 `pEnum`  
 제한이 요청 `IAssemblyEnum` 된 포인터를 포함 하는 메모리 위치에 대 한 포인터입니다.  
  
 `pUnkReserved`  
 진행 향후 확장성을 위해 예약 되었습니다. `pUnkReserved`는 null 참조 여야 합니다.  
  
 `pName`  
 진행 요청 된 어셈블리의입니다. `IAssemblyName` 이 이름은 열거형을 필터링 하는 데 사용 됩니다. 전역 어셈블리 캐시의 모든 어셈블리를 열거 하는 것은 null 일 수 있습니다.  
  
 `dwFlags`  
 진행 열거자의 동작을 수정 하기 위한 플래그입니다. 이 매개 변수는 [ASM_CACHE_FLAGS](asm-cache-flags-enumeration.md) 열거형에서 정확히 한 비트를 포함 합니다.  
  
 `pvReserved`  
 진행 향후 확장성을 위해 예약 되었습니다. `pvReserved`는 null 참조 여야 합니다.  
  
## <a name="remarks"></a>설명  
 매개 `dwFlags` 변수는 `ASM_CACHE_FLAGS` 열거형에서 정확히 1 비트를 포함 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IAssemblyEnum 인터페이스](iassemblyenum-interface.md)
- [IAssemblyName 인터페이스](iassemblyname-interface.md)
- [Fusion 전역 정적 함수](fusion-global-static-functions.md)
