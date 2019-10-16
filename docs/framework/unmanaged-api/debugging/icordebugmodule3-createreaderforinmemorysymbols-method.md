---
title: ICorDebugModule3::CreateReaderForInMemorySymbols 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule3.CreateReaderForInMemorySymbols
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule3::CreateReaderForInMemorySymbols
helpviewer_keywords:
- CreateReaderForInMemorySymbols method, ICorDebugModule3 interface [.NET Framework debugging]
- ICorDebugModule3::CreateReaderForInMemorySymbols method [.NET Framework debugging]
ms.assetid: af317171-d66d-4114-89eb-063554c74940
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 944e02fe83ba71b51ffb154748acff9c6dd662fe
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764017"
---
# <a name="icordebugmodule3createreaderforinmemorysymbols-method"></a>ICorDebugModule3::CreateReaderForInMemorySymbols 메서드
동적 모듈에 대 한 디버그 기호 판독기를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateReaderForInMemorySymbols (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **    ppObj  
```  
  
## <a name="parameters"></a>매개 변수  
 riid  
 [in] 반환할 COM 인터페이스의 IID입니다. 일반적으로 [ISymUnmanagedReader 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md)합니다.  
  
 ppObj  
 [out] 반환 되는 인터페이스에 대 한 포인터에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 판독기를 만들었습니다.  
  
 CORDBG_E_MODULE_LOADED_FROM_DISK  
 모듈에는 메모리 내 또는 동적 모듈이 아닙니다.  
  
 CORDBG_E_SYMBOLS_NOT_AVAILABLE  
 기호는 응용 프로그램에서 지정 되지 않은 또는 아직 지원 되지 않습니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 판독기를 만들 수 없습니다.  
  
## <a name="remarks"></a>설명  
 이 메서드가 될 수 있습니다도 메모리 내 (동적이 아닌) 모듈에 대 한 기호 판독기 개체를 만드는 데에 기호를 먼저 사용할 (나타난 합니다 [UpdateModuleSymbols 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-updatemodulesymbols-method.md) 콜백).  
  
 이 메서드가 호출 될 때마다 새 판독기 인스턴스를 반환 합니다 (같은 [CComPtrBase::CoCreateInstance](/cpp/atl/reference/ccomptrbase-class#cocreateinstance)). 디버거에서 결과 캐시 하 고 기본 데이터를 변경한 경우에 새 인스턴스를 요청 해야 하므로 (즉을 [LoadClass 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-loadclass-method.md) 콜백을 수신).  
  
 첫 번째 형식이 로드 될 때까지 동적 모듈에서는 사용할 수 있는 모든 기호를 있지 않은 (표시 된 대로 합니다 [LoadClass 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-loadclass-method.md) 콜백).  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:** 4.5, 4, 3.5 SP1  
  
## <a name="see-also"></a>참고자료

- [ICorDebugRemoteTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)
- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
