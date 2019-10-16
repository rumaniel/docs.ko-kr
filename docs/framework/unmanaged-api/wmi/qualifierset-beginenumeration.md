---
title: QualifierSet_BeginEnumeration 함수 (관리 되지 않는 API 참조)
description: QualifierSet_BeginEnumeration 함수는 개체 한정자의 열거자를 다시 설정 합니다.
ms.date: 11/06/2017
api_name:
- QualifierSet_BeginEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_BeginEnumeration
helpviewer_keywords:
- QualifierSet_BeginEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3b75c51ebddd78e447fed57b22a96c2d5c35004e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798353"
---
# <a name="qualifierset_beginenumeration-function"></a>QualifierSet_BeginEnumeration 함수

개체 한정자의 열거자를 열거형 시작 부분으로 다시 설정합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT QualifierSet_BeginEnumeration (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LONG                 lFlags
);
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) 인스턴스에 대 한 포인터입니다.

`lFlags`\
진행 [설명](#remarks) 섹션에서 설명 하는 플래그 또는 값의 비트 조합으로, 열거형에 포함할 한정자를 지정 합니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `lFlags` 매개 변수가 잘못되었습니다. |
|`WBEM_E_UNEXPECTED` | 0x8004101d | `QualifierSet_BeginEnumeration` [를`QualifierSet_EndEnumeration`](qualifierset-endenumeration.md)호출 하지 않고에 대 한 두 번째 호출을 수행 했습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 새 열거를 시작할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemQualifierSet:: BeginEnumeration](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-beginenumeration) 메서드에 대 한 호출을 래핑합니다.

개체에 대 한 모든 한정자를 열거 하려면 [QualifierSet_Next](qualifierset-next.md)에 대 한 첫 번째 호출 전에이 메서드를 호출 해야 합니다. 한정자를 열거 하는 순서는 지정 된 열거형에 대해 고정이 되도록 보장 됩니다.

`lEnumFlags` 인수로 전달 될 수 있는 플래그는 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
|  | 0 | 모든 한정자의 이름을 반환 합니다. |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 현재 속성 또는 개체와 관련 된 한정자의 이름만 반환 합니다. <br/> 속성의 경우: 클래스 정의에서 전파 되는 한정자가 아니라 속성 (재정의 포함)에 한정 된 한정자만 반환 합니다. <br/> 인스턴스의 경우: 인스턴스별 한정자 이름만 반환 합니다. <br/> 클래스의 경우: 파생 되는 클래스와 관련 된 한정자만 반환 합니다.
|`WBEM_FLAG_PROPAGATED_ONLY` | 0x20 | 다른 개체에서 전파 된 한정자의 이름만 반환 합니다. <br/> 속성의 경우: 클래스 정의에서이 속성에 전파 된 한정자만 반환 하 고 속성 자체의 한정자는 반환 하지 않습니다. <br/> 인스턴스의 경우: 클래스 정의에서 전파 된 한정자만 반환 합니다. <br/> 클래스의 경우: 부모 클래스에서 상속 된 한정자 이름만 반환 합니다. |

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
