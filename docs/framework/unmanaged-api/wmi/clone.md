---
title: Clone 함수 (관리 되지 않는 API 참조)
description: Clone 함수는 현재 항목의 전체 복제본 인 새 개체를 반환 합니다.
ms.date: 11/06/2017
api_name:
- Clone
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Clone
helpviewer_keywords:
- Clone function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5957f591dca7df30178660eb3fb074567c285715
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798716"
---
# <a name="clone-function"></a>Clone 함수
현재 개체의 전체 복제본인 새 개체를 반환합니다.   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Clone (
   [in] int                  vFunc, 
   [in] IWbemClassObject*    ptr, 
   [out] IWbemClassObject**  ppCopy
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`ppCopy`  
제한이 의 `ptr`전체 유일한 새 개체입니다. 현재 개체의 복사본 `null` 을 받는 경우에는이 인수를 사용할 수 없습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `null`가 매개 변수로 지정 되었으며이 사용에 적합 하지 않습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 개체를 복제 하는 데 사용할 수 있는 메모리가 부족 합니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: Clone](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-clone) 메서드에 대 한 호출을 래핑합니다.

복제 된 개체는 참조 개수가 1 인 COM 개체입니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
