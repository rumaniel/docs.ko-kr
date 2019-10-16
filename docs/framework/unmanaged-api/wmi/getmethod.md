---
title: GetMethod 함수 (관리 되지 않는 API 참조)
description: GetMethod 함수는 메서드에 대 한 정보를 검색 합니다.
ms.date: 11/06/2017
api_name:
- GetMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetMethod
helpviewer_keywords:
- GetMethod function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b9cc185bf8cccb8ed3c24e28954afd86464602d7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798572"
---
# <a name="getmethod-function"></a>GetMethod 함수

지정된 메서드에 대한 정보를 검색합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT GetMethod (
   [in] int                vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszName,
   [in] LONG                lFlags,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszName`\
진행 메서드 이름입니다. 이 매개 변수는 `null` 이 될 수 없으며 유효한 `LPCWSTR`을 가리켜야 합니다.

`lFlags`\
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`ppInSignature`\
제한이 메서드에 대 한 in 매개 변수를 설명 하는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스의 주소에 대 한 포인터입니다. 이 매개 변수는로 `null`설정 된 경우 무시 됩니다.

`ppOutSignature`\
제한이 메서드에 대 한 출력 매개 변수를 설명 하는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스의 주소에 대 한 포인터입니다. 이 매개 변수는로 `null`설정 된 경우 무시 됩니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | 지정 된 속성을 찾을 수 없는 경우 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: GetMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getmethod) 메서드에 대 한 호출을 래핑합니다.

Windows Management는 메서드에 in 매개 변수가 없는 경우 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 포인터를 `null`로 설정할 수 있습니다.

`IWbemClassObject` 및 `ppInSignature` 의`ppOutSignature` 는 각각 시스템 클래스 [매개 변수](/windows/desktop/WmiSdk/--parameters)인스턴스의 속성으로 in 및 out 매개 변수를 설명 합니다. 의 `ppInSignature` 속성은 *n*으로 `Param`지정 됩니다. 여기서 *n* 은 메서드 시그니처의 매개 변수 위치입니다 (예: `Param1`, `Param2`등). 의 `ppOutSignature` 속성은 이름이 `Param` *n*이지만 반환 값의 이름은 `ReturnValue`입니다. 자세한 내용 및 예제는 [IWbemClassObject:: GetMethod 메서드](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getmethod)를 참조 하세요.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
