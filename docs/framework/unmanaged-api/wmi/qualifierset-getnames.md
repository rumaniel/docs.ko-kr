---
title: QualifierSet_GetNames 함수 (관리 되지 않는 API 참조)
description: QualifierSet_GetNames 함수는 개체 또는 속성에서 한정자의 이름을 검색 합니다.
ms.date: 11/06/2017
api_name:
- QualifierSet_GetNames
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_GetNames
helpviewer_keywords:
- QualifierSet_GetNames function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 266462a5393c8e26aa2bc3f2ec8ab72d4410a431
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798301"
---
# <a name="qualifierset_getnames-function"></a>QualifierSet_GetNames 함수

현재 개체 또는 속성에서 사용할 수 있는 모든 한정자 또는 특정 한정자의 이름을 검색 합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT QualifierSet_GetNames (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LONG                 lFlags,
   [out] SAFEARRAY (BSTR)**  pstrNames
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) 인스턴스에 대 한 포인터입니다.

`lFlags`\
진행 열거형에 포함할 이름을 지정 하는 다음 플래그 또는 값 중 하나입니다.

|상수  |값  |설명  |
|---------|---------|---------|
|  | 0 | 모든 한정자의 이름을 반환 합니다. |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 현재 속성 또는 개체와 관련 된 한정자의 이름만 반환 합니다. <br/> 속성의 경우: 클래스 정의에서 전파 되는 한정자가 아니라 속성 (재정의 포함)에 한정 된 한정자만 반환 합니다. <br/> 인스턴스의 경우: 인스턴스별 한정자 이름만 반환 합니다. <br/> 클래스의 경우: 파생 되는 클래스와 관련 된 한정자만 반환 합니다.
|`WBEM_FLAG_PROPAGATED_ONLY` | 0x20 | 다른 개체에서 전파 된 한정자의 이름만 반환 합니다. <br/> 속성의 경우: 클래스 정의에서이 속성에 전파 된 한정자만 반환 하 고 속성 자체의 한정자는 반환 하지 않습니다. <br/> 인스턴스의 경우: 클래스 정의에서 전파 된 한정자만 반환 합니다. <br/> 클래스의 경우: 부모 클래스에서 상속 된 한정자 이름만 반환 합니다. |

`pstrNames`\
제한이 요청 된 `SAFEARRAY` 이름을 포함 하는 새입니다. 배열에는 요소가 0 개 있을 수 있습니다. 오류가 발생 하는 경우 새 `SAFEARRAY` 가 반환 되지 않습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 새 열거를 시작할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemQualifierSet:: GetNames](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-getnames) 메서드에 대 한 호출을 래핑합니다.

한정자 이름을 검색 한 후에는 [QualifierSet_Get](qualifierset-get.md) 함수를 호출 하 여 이름별로 각 한정자에 액세스할 수 있습니다.

지정 된 개체의 한정자가 0이 아니므로 함수가를 반환 `pstrNames` `WBEM_S_NO_ERROR`하는 경우에도 반환 시의 문자열 수는 0이 될 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
