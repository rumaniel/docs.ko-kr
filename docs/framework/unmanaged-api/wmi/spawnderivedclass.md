---
title: SpawnDerivedClass 함수 (관리 되지 않는 API 참조)
description: SpawnDerivedClass 함수는 개체에서 파생 되는 새 개체를 만듭니다.
ms.date: 11/06/2017
api_name:
- SpawnDerivedClass
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnDerivedClass
helpviewer_keywords:
- SpawnDerivedClass function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c213f311f1af1e56d0ce24eba3b76f33be541323
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798235"
---
# <a name="spawnderivedclass-function"></a>SpawnDerivedClass 함수
지정된 개체에서 새로 파생된 클래스 개체를 만듭니다.    
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SpawnDerivedClass (
   [in] int                  vFunc, 
   [in] IWbemClassObject*    ptr, 
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewClass); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`lFlags`  
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`ppNewClass`  
제한이 새 클래스 정의 개체에 대 한 포인터를 받습니다. 오류가 발생 하면 새 개체가 반환 `ppNewClass` 되지 않고 수정 되지 않은 상태로 유지 됩니다. 값은 일 `null`수 없습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | 인스턴스에서 클래스를 생성 하는 등의 잘못 된 작업이 요청 되었습니다. |
| `WBEM_E_INCOMPLETE_CLASS` | 소스 클래스가 완전히 정의 되지 않았거나 Windows Management에 등록 되어 있지 않으므로 새 파생 클래스가 허용 되지 않습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass`가 `null`인 경우 |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: SpawnDerivedClass](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-clone) 메서드에 대 한 호출을 래핑합니다.

`ptr`는 생성 된 개체의 부모 클래스가 되는 클래스 정의 여야 합니다. 반환 된 개체는 현재 개체의 서브 클래스가 됩니다.

에서 `ppNewClass` 반환 되는 새 개체는 자동으로 현재 개체의 서브 클래스가 됩니다. 이 동작은 재정의할 수 없습니다. 서브 클래스 (파생 클래스)를 만들 수 있는 다른 방법은 없습니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
