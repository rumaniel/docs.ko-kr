---
title: GetPropertyOrigin 함수 (관리 되지 않는 API 참조)
description: GetPropertyOrigin 함수는 속성이 선언 되는 클래스를 결정 합니다.
ms.date: 11/06/2017
api_name:
- GetPropertyOrigin
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetPropertyOrigin
helpviewer_keywords:
- GetPropertyOrigin function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0c2d0f23f3dd2d52f73f09c32d4e3118a9ed5ea3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798484"
---
# <a name="getpropertyorigin-function"></a>GetPropertyOrigin 함수

속성이 선언되는 클래스를 결정합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT GetPropertyOrigin (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszMethodName,
   [out] BSTR*              pstrClassName
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszMethodName`\
진행 소유 하 고 있는 클래스가 요청 된 개체의 속성 이름입니다.

`pstrClassName`\
제한이 속성을 소유 하는 클래스의 이름을 받습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 지정 된 속성을 찾을 수 없는 경우 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: GetPropertyOrigin](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getpropertyorigin) 메서드에 대 한 호출을 래핑합니다.

클래스는 하나 이상의 기본 클래스에서 속성을 상속할 수 있기 때문에 일반적으로 개발자는 지정 된 메서드가 정의 된 속성을 확인 하려고 합니다.

매개 변수는 `out` 매개 변수 이기 때문에 `BSTR` 함수가 호출 되기 전에 유효한을 가리키지 않아야 합니다 .이 포인터는 함수가 반환 된 후에는 할당이 취소 되지 않습니다. `pstrClassName`

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
