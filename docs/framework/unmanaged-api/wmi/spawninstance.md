---
title: SpawnInstance 함수 (관리 되지 않는 API 참조)
description: SpawnInstance 함수는 클래스의 새 인스턴스를 만듭니다.
ms.date: 11/06/2017
api_name:
- SpawnInstance
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnInstance
helpviewer_keywords:
- SpawnInstance function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 529905bd9286520a8e09479bfc95ef0b614f53e9
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798211"
---
# <a name="spawninstance-function"></a>SpawnInstance 함수
클래스의 새 인스턴스를 만듭니다.    
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SpawnInstance (
   [in] int                  vFunc, 
   [in] IWbemClassObject*    ptr, 
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewInstance); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`lFlags`  
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`ppNewInstance`  
제한이 클래스의 새 인스턴스에 대 한 포인터를 받습니다. 오류가 발생 하면 새 개체가 반환 `ppNewInstance` 되지 않고 수정 되지 않은 상태로 유지 됩니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_INCOMPLETE_CLASS` | 0x80041020 | `ptr`는 유효한 클래스 정의가 아니므로 새 인스턴스를 생성할 수 없습니다. 불완전 하거나 [PutClassWmi](putclasswmi.md)를 호출 하 여 Windows Management에 등록 되지 않았습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass`가 `null`인 경우 |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: SpawnInstance](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-spawninstance) 메서드에 대 한 호출을 래핑합니다.

`ptr`는 Windows Management에서 가져온 클래스 정의 여야 합니다. 인스턴스에서 인스턴스를 생성 하는 것은 지원 되지만 반환 된 인스턴스는 비어 있습니다. 그런 다음이 클래스 정의를 사용 하 여 새 인스턴스를 만듭니다. Windows 관리에 인스턴스를 쓰려면 [Putinstancewmi](putinstancewmi.md) 함수를 호출 해야 합니다.

에서 `ppNewClass` 반환 되는 새 개체는 자동으로 현재 개체의 서브 클래스가 됩니다. 이 동작은 재정의할 수 없습니다. 서브 클래스 (파생 클래스)를 만들 수 있는 다른 방법은 없습니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
