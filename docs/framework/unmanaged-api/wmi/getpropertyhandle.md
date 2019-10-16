---
title: GetPropertyHandle 함수 (관리 되지 않는 API 참조)
description: GetPropertyHandle 함수는 속성을 식별 하는 고유 핸들을 반환 합니다.
ms.date: 11/06/2017
api_name:
- GetPropertyHandle
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetPropertyHandle
helpviewer_keywords:
- GetPropertyHandle function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d72b0da43971a74a08a249b19dfc0d446eeb5e6a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798548"
---
# <a name="getpropertyhandle-function"></a>GetPropertyHandle 함수

속성을 식별하는 고유한 핸들을 반환합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT GetPropertyHandle (
   [in] int                  vFunc,
   [in] IWbemObjectAccess*   ptr,
   [in] LPCWSTR              wszPropertyName,
   [out] CIMTYPE*            pType,
   [out] long*               pHandle
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) 인스턴스에 대 한 포인터입니다.

`wszPropertyName`\
진행 속성 이름을 포함 하는 UTF16 인코딩된 문자를 포함 하는 null로 끝나는 문자열입니다.

`pType`\
제한이 속성의 CIM 형식을 [`CIMTYPE`](/windows/win32/api/wbemcli/ne-wbemcli-cimtype_enumeration) 나타내는 열거형 멤버에 대 한 포인터입니다.

`pHandle`\
제한이 속성 핸들을 포함 하는 정수에 대 한 포인터입니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | 지정 된 속성 이름을 찾을 수 없습니다. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
|`WBEM_E_NOT_SUPPORTED` | 0x8004100c | 요청 된 속성이 `CIM_OBJECT` 또는 `CIM_ARRAY`형식입니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: GetPropertyHandle](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemobjectaccess-getpropertyhandle) 메서드에 대 한 호출을 래핑합니다.

[IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) 메서드를 사용 하 여 속성 값을 읽거나 쓸 때이 핸들을 사용 하 여 속성을 식별할 수 있습니다.

`CIM_OBJECT` 및`CIM_ARRAY`이외의 모든 데이터 형식의 속성에 대해 핸들을 검색할 수 있습니다. 반환 된 핸들은 클래스의 모든 인스턴스에 대해 작동 합니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
