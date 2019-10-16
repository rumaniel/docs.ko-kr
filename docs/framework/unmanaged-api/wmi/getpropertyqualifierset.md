---
title: GetPropertyQualifierSet 함수 (관리 되지 않는 API 참조)
description: GetPropertyQualifierSet 함수는 속성에 대 한 한정자 집합을 검색 합니다.
ms.date: 11/06/2017
api_name:
- GetPropertyQualifierSet
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetPropertyQualifierSet
helpviewer_keywords:
- GetPropertyQualifierSet function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b7bce241d10051e4c6be94cdfa40de23773fb0bb
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798478"
---
# <a name="getpropertyqualifierset-function"></a>GetPropertyQualifierSet 함수

특정 속성에 대한 한정자 집합을 검색합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT GetPropertyQualifierSet (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszProperty,
   [out] IWbemQualifierSet  **ppQualSet
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszMethod`\
진행 속성 이름입니다. `wszProperty`는 유효한 `LPCWSTR`을 가리켜야 합니다.

`ppQualSet`\
제한이 속성 한정자에 대 한 액세스를 허용 하는 인터페이스 포인터를 받습니다. `ppQualSet`가 `null`이 될 수 없는 경우 오류가 발생 하면 새 개체가 반환 되지 않고 포인터가를 `null`가리키도록 설정 됩니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
| `WBEM_E_NOT_FOUND` | 0x80041002 | 지정 된 메서드가 없습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 인 `null`경우 |
| `WBEM_E_SYSTEM_PROPERTY` | 0x80041030 | 함수는 시스템 속성의 한정자를 가져오려고 시도 합니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: GetPropertyQualifierSet](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getpropertyqualifierset) 메서드에 대 한 호출을 래핑합니다.

이 함수에 대 한 호출은 현재 개체가 CIM 클래스 정의 인 경우에만 지원 됩니다. CIM 인스턴스를 가리키는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 포인터에는 메서드 조작을 사용할 수 없습니다.

각 메서드에는 자체 한정자가 있을 수 있으므로 [IWbemQualifierSet 포인터](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) 를 사용 하면 호출자가 이러한 한정자를 추가, 편집 또는 삭제할 수 있습니다.

시스템 속성에는 한정자가 없으므로 시스템 속성에 `WBEM_E_SYSTEM_PROPERTY` 대 한 [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) 포인터를 가져오려고 하면이 함수는를 반환 합니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
