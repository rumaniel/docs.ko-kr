---
title: ICorDebugProcess6::MarkDebuggerAttached 메서드
ms.date: 03/30/2017
ms.assetid: bf94f090-5265-4112-8e57-5b4e20e070d0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c818b196f3252138f2a9c601b04f1d7a6727bc6b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912736"
---
# <a name="icordebugprocess6markdebuggerattached-method"></a>ICorDebugProcess6::MarkDebuggerAttached 메서드
.NET Framework 클래스 라이브러리의 <xref:System.Diagnostics.Debugger.IsAttached%2A?displayProperty=nameWithType> 메서드가 `true`를 반환하도록 디버기의 내부 상태를 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT MarkDebuggerAttached(  
    BOOL fIsAttached  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fIsAttached`  
 `true` 메서드가 디버거가 연결되어 있음을 나타내야 하는 경우 <xref:System.Diagnostics.Debugger.IsAttached%2A?displayProperty=nameWithType>이고, 그러지 않으면 `false`입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음 표에 나와 있는 값을 반환할 수 있습니다.  
  
|반환 값|설명|  
|------------------|-----------------|  
|`S_OK`|디버기를 정상적으로 업데이트했습니다.|  
|`CORDBG_E_MODULE_NOT_LOADED`|<xref:System.Diagnostics.Debugger.IsAttached%2A?displayProperty=nameWithType> 메서드를 포함하는 어셈블리가 로드되지 않았거나 메타데이터 누락 등의 기타 오류로 인해 어셈블리를 인식할 수 없습니다.<br /><br /> 이 오류는 흔히 발생하며 심각하지는 않습니다. 추가 어셈블리가 로드되면 메서드를 다시 호출해야 합니다.|  
|기타 오류 `HRESULT` 값입니다.|다른 값이 반환되는 경우 디버거나 컴파일러 구성 요소가 오동작하는 것일 수 있습니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> 이 메서드는 .NET 네이티브에서만 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugProcess6 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess6-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
