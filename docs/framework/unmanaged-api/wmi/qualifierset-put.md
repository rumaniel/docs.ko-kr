---
title: QualifierSet_Put 함수 (관리 되지 않는 API 참조)
description: QualifierSet_Put 함수는 명명 된 한정자와 해당 값을 씁니다.
ms.date: 11/06/2017
api_name:
- QualifierSet_Put
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Put
helpviewer_keywords:
- QualifierSet_Put function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 40688a0e4273233245d00fcd927f95945a43f712
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798264"
---
# <a name="qualifierset_put-function"></a>QualifierSet_Put 함수

명명된 한정자 및 값을 씁니다. 새 한정자는 동일한 이름의 이전 값을 덮어씁니다. 한정자가 없으면 생성 됩니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT QualifierSet_Put (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LPCWSTR              wszName,
   [in] VARIANT*             pVal,
   [in] LONG                 lFlavor
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) 인스턴스에 대 한 포인터입니다.

`wszName`\
진행 쓸 한정자의 이름입니다.

`pVal`\
진행 쓸 한정자를 포함 하 `VARIANT` 는 유효한에 대 한 포인터입니다. 이 매개 변수 수 없습니다 `null`합니다.

`lFlavor`\
진행 이 한정자에 대 한 원하는 한정자 특색을 정의 하는 다음 상수 중 하나입니다. 기본값은 `WBEM_FLAVOR_OVERRIDABLE`(0)입니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_FLAVOR_OVERRIDABLE` | 0 | 한정자는 파생 된 클래스 또는 인스턴스에서 재정의할 수 있습니다. **이 값은 기본값입니다.** |
| `WBEM_FLAVOR_FLAG_PROPAGATE_TO_INSTANCE` | 1 | 한정자가 인스턴스로 전파됩니다. |
| `WBEM_FLAVOR_FLAG_PROPAGATE_TO_DERIVED_CLASS` | 2 | 한정자는 파생 클래스에 전파 됩니다. |
| `WBEM_FLAVOR_NOT_OVERRIDABLE` | 0x10 | 한정자를 파생된 클래스 또는 인스턴스에서 재정의할 수 없습니다. |
| `WBEM_FLAVOR_AMENDED` | 0x80 | 한정자는 지역화 됩니다. |

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_CANNOT_BE_KEY` | 0x8004101f | 키가 될 수 없는 속성에 **키** 한정자를 지정 하는 잘못 된 시도가 있었습니다. 키 개체에 대 한 클래스 정의에 지정 되 고 인스턴스 단위로 변경할 수 없습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_INVALID_QUALIFIER_TYPE` | 0x80041029 | `pVal` 매개 변수가 올바른 한정자 형식이 아닙니다. |
| `WBEM_E_OVERRIDE_NOT_ALLOWED` | 0x8004101a | 소유 하는 개체가 재정의를 허용 `QualifierSet_Put` 하지 않기 때문에 한정자에서 메서드를 호출할 수 없습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemQualifierSet::P 세계](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-put) 메서드에 대 한 호출을 래핑합니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
