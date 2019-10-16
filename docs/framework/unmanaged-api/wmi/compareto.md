---
title: CompareTo 함수 (관리 되지 않는 API 참조)
description: CompareTo 함수는 개체를 다른 WMI 개체와 비교 합니다.
ms.date: 11/06/2017
api_name:
- CompareTo
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CompareTo
helpviewer_keywords:
- CompareTo function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2ec42dff333422e247a11b4a3a5b9aed9bd316fa
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798780"
---
# <a name="compareto-function"></a>CompareTo 함수

개체를 다른 Windows 관리 개체와 비교합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT CompareTo (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              flags,
   [in] IWbemClassObject* pCompareTo
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`flags`\
진행 비교를 위해 고려할 개체 특성을 지정 하는 플래그의 비트 조합입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

`pCompareTo`\
진행 비교할 개체입니다. `pCompareTo`유효한 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스여야 합니다. 일 `null`수 없습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 지정 되지 않은 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_UNEXPECTED` | 0x8004101d | `BeginEnumeration` [를`EndEnumeration`](endenumeration.md)호출 하지 않고에 대 한 두 번째 호출을 수행 했습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
| `WBEM_S_DIFFERENT` | 0x40003 | 개체가 서로 다릅니다. |
| `WBEM_S_SAME` | 0 | 개체는 비교 플래그를 기준으로 동일 합니다. |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: CompareTo](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-compareto) 메서드에 대 한 호출을 래핑합니다.

`lEnumFlags` 인수로 전달 될 수 있는 플래그는 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다. 다음 플래그의 비트 조합을 지정 하 여 비교와 관련 된 개별 특성을 지정할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAG_IGNORE_OBJECT_SOURCE` | 2 | 원본 (서버와 원본에서 가져온 네임 스페이스)을 무시 합니다. |
| `WBEM_FLAG_IGNORE_QUALIFIERS` | 1 | 모든 한정자 무시 ( **키** 및 **동적**포함) |
| `WBEM_FLAG_IGNORE_DEFAULT_VALUES` | 4 | 속성의 기본값을 무시 합니다. 이 플래그는 클래스 비교에만 적용 됩니다. |
| `WBEM_FLAG_IGNORE_FLAVOR` | 0x20 | 한정자 특색을 무시 합니다. 이 플래그는 한정자를 계속 고려 하지만 전파 규칙 및 재정의 제한과 같은 버전 차이는 무시 합니다. |
| `WBEM_FLAG_IGNORE_CASE` | 0x10 | 문자열 값을 비교할 때 대/소문자를 무시 합니다. 이는 문자열 및 한정자 값 모두에 적용 됩니다. 이 플래그가 설정 되었는지 여부에 관계 없이 속성 및 한정자 이름의 비교는 항상 대/소문자를 구분 합니다. |
| `WBEM_FLAG_IGNORE_CLASS` | 0x8 | 비교할 개체가 동일한 클래스의 인스턴스인 것으로 가정 합니다. 따라서이 플래그는 인스턴스 관련 정보만을 비교 합니다. 이 플래그를 사용 하 여 성능을 최적화 합니다. 동일한 클래스의 개체가 없으면 결과가 정의 되지 않습니다. |

또는 단일 복합 플래그를 다음과 같이 지정할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
|`WBEM_COMPARISON_INCLUDE_ALL` | 0 | 비교의 모든 기능을 고려 합니다. |

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
