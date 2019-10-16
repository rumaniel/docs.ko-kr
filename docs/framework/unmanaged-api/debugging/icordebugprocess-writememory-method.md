---
title: ICorDebugProcess::WriteMemory 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.WriteMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::WriteMemory
helpviewer_keywords:
- ICorDebugProcess::WriteMemory method [.NET Framework debugging]
- WriteMemory method [.NET Framework debugging]
ms.assetid: d5c07d86-045d-4391-893b-0bcd2959f90e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4599bf310a0b819bc662b90a5a86e87ac27c37b1
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67737013"
---
# <a name="icordebugprocesswritememory-method"></a>ICorDebugProcess::WriteMemory 메서드
이 프로세스의 메모리 영역에 데이터를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT WriteMemory(  
    [in]  CORDB_ADDRESS address,  
    [in]  DWORD size,  
    [in, size_is(size)] BYTE buffer[],  
    [out] SIZE_T *written);  
```  
  
## <a name="parameters"></a>매개 변수  
 `address`  
 [in] `CORDB_ADDRESS` 메모리 영역을 데이터의 기본 주소는 값이 기록 됩니다. 데이터 전송이 발생 하기 전에 시스템 기본 주소부터 지정된 된 크기의 메모리 영역에 쓰기 위해 액세스할 수 있는지 확인 합니다. 액세스할 수 없는 경우 메서드가 실패 합니다.  
  
 `size`  
 [in] 메모리 영역에 쓸 바이트 수입니다.  
  
 `buffer`  
 [in] 쓸 데이터를 포함 하는 버퍼입니다.  
  
 `written`  
 [out] 이 프로세스의 메모리 영역에 쓴 바이트 수를 받는 변수에 대 한 포인터입니다. 경우 `written` 가 null 인 경우이 매개 변수가 무시 됩니다.  
  
## <a name="remarks"></a>설명  
 데이터는 중단점 뒤 자동으로 기록 됩니다. .NET Framework 버전 2.0에서 네이티브 디버거 명령 스트림의에 중단점을 삽입 하려면이 메서드를 사용 하지 해야 합니다. 사용 하 여 [ICorDebugProcess2::SetUnmanagedBreakpoint](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess2-setunmanagedbreakpoint-method.md) 대신 합니다.  
  
 `WriteMemory` 메서드는 관리 코드 외에 사용 해야 합니다. 이 메서드는 제대로 사용 하지 않으면 런타임에서 손상 될 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
