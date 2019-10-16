---
title: PutMethod 함수 (관리 되지 않는 API 참조)
description: PutMethod 함수는 메서드를 만듭니다.
ms.date: 11/06/2017
api_name:
- PutMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutMethod
helpviewer_keywords:
- PutMethod function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a2b41cbbade9da5c2095309b9039b8ce2758f6f3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798357"
---
# <a name="putmethod-function"></a>PutMethod 함수
메서드를 만듭니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT PutMethod (
   [in] int                vFunc, 
   [in] IWbemClassObject*  ptr, 
   [in] LPCWSTR            wszName,
   [in] LONG               lFlags,
   [in] IWbemClassObject*  pInSignature,
   [in] IWbemClassObject*  pOutSignature
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszName`  
진행 만들 메서드의 이름입니다. 

`lFlags`  
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`pSignatureIn`  
진행 메서드에 대 한 매개 변수를 `in` 포함 하는 [__parameters 시스템 클래스](/windows/desktop/WmiSdk/--parameters) 의 복사본에 대 한 포인터입니다. 로 `null`설정 되 면이 매개 변수는 무시 됩니다.  

`pSignatureOut`  
진행  메서드에 대 한 매개 변수를 `out` 포함 하는 [__parameters 시스템 클래스](/windows/desktop/WmiSdk/--parameters) 의 복사본에 대 한 포인터입니다. 로 `null`설정 되 면이 매개 변수는 무시 됩니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 하나 이상의 매개 변수가 잘못 되었습니다. |
| `WBEM_E_INVALID_DUPLICATE_PARAMETER` | 0x80041043 | `[in, out]` *Pinsignature* 와 *poutsignature* 개체에 지정 된 메서드 매개 변수는 서로 다른 한정자를 가집니다.
| `WBEM_E_MISSING_PARAMETER_ID` | 0x80041036 | 메서드 매개 변수에 **ID** 한정자의 사양이 없습니다. |
| `WBEM_E_NONCONSECUTIVE_PARAMETER_IDS` | 0x80041038 | 메서드 매개 변수에 할당 된 ID 계열이 연속 되지 않거나 0에서 시작 하지 않습니다. |
| `WBEM_E_PARAMETER_ID_ON_RETVAL` | 0x80041039 | 메서드의 반환 값에는 **ID** 한정자가 있습니다. |
| `WBEM_E_PROPAGATED_METHOD` | 0x80041034 | 부모 클래스에서 기존 메서드 이름을 다시 사용 하려고 했지만 서명이 일치 하지 않습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다. |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject::P utMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-putmethod) 메서드에 대 한 호출을 래핑합니다.

이 메서드 호출은가 CIM 클래스 정의 `ptr` 인 경우에만 지원 됩니다. CIM 인스턴스를 가리키는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 포인터에서 메서드 조작을 사용할 수 없습니다.

사용자는 이름이 밑줄로 시작 하거나 끝나는 메서드를 만들 수 없습니다. 이는 시스템 클래스 및 속성에 대해 예약 되어 있습니다.

메서드의 `in` 경우 및 `out` 매개 변수는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 개체의 속성으로 설명 됩니다.

매개 변수는 `pInSignature` 및`pOutSignature` 매개 변수에서 가리키는 두 개체에 동일한 속성을 추가 하 여 정의할 수 있습니다. `[in/out]` 이 경우 속성은 동일한 **ID** 한정자 값을 공유 합니다.

이 아닌 `ReturnValue` [__parameters](/windows/desktop/WmiSdk/--parameters) 클래스 개체의 각 속성에는 매개 변수가 표시 되는 순서를 식별 하는 0부터 시작 하는 숫자 값인 **ID** 한정자가 있어야 합니다. 두 매개 변수가 동일한 **id** 값을 가질 수 없으며 **id** 값을 건너뛸 수 없습니다. 두 조건 중 하나가 발생 하면 `PutMethod` 함수는 `WBEM_E_NONCONSECUTIVE_PARAMETER_IDS`를 반환 합니다.

## <a name="example"></a>예제

예제를 보려면 [IWbemClassObject::P utMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-putmethod) 메서드를 참조 하세요.

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
