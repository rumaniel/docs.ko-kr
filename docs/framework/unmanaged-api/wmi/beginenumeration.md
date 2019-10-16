---
title: BeginEnumeration 함수 (관리 되지 않는 API 참조)
description: BeginEnumeration 함수는 열거자를 열거형의 시작 부분으로 다시 설정 합니다.
ms.date: 11/06/2017
api_name:
- BeginEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginEnumeration
helpviewer_keywords:
- BeginEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: de36650aa2b206b5e9734b38c6067a3a79de610c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798783"
---
# <a name="beginenumeration-function"></a>BeginEnumeration 함수
열거자를 열거형의 시작 부분으로 다시 설정 합니다.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT BeginEnumeration (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LONG              lEnumFlags
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`lEnumFlags`\
진행 [설명](#remarks) 섹션에서 설명 하는 플래그 또는 값의 비트 조합으로, 열거형에 포함 된 속성을 제어 합니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 에서 `lEnumFlags` 플래그 조합이 잘못 되었거나 잘못 된 인수가 지정 되었습니다. |
|`WBEM_E_UNEXPECTED` | 0x8004101d | `BeginEnumeration` [를`EndEnumeration`](endenumeration.md)호출 하지 않고에 대 한 두 번째 호출을 수행 했습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 새 열거를 시작할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: BeginEnumeration](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 메서드에 대 한 호출을 래핑합니다.

`lEnumFlags` 인수로 전달 될 수 있는 플래그는 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.  각 그룹의 플래그 하나를 다른 모든 그룹의 플래그와 결합할 수 있습니다. 그러나 같은 그룹의 플래그는 함께 사용할 수 없습니다. 

**그룹 1**

|상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | 키만 구성 하는 속성을 포함 합니다. |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | 개체 참조에만 해당 하는 속성을 포함 합니다. |

**그룹 2**

상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | 열거를 시스템 속성 으로만 제한 합니다. |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | 로컬 및 전파 된 속성을 포함 하지만 시스템 속성은 열거에서 제외 합니다. |

클래스:

상수  |값  |Description  |
|---------|---------|---------|
|`WBEM_FLAG_CLASS_OVERRIDES_ONLY` | 0x100 | 열거를 클래스 정의에서 재정의 된 속성으로 제한 합니다. |
|`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` | 0x100 | 열거를 현재 클래스 정의에 재정의 된 속성 및 클래스에 정의 된 새 속성으로 제한 합니다. |
| `WBEM_MASK_CLASS_CONDITION` | 0x300 | `WBEM_FLAG_CLASS_OVERRIDES_ONLY` `lEnumFlags` 또는`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` 가 설정 되었는지 여부를 확인 하기 위해 값에 적용할 마스크 (플래그 아님)입니다. |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 클래스 자체에서 정의 되거나 수정 된 속성으로 열거를 제한 합니다. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 기본 클래스에서 상속 되는 속성으로 열거를 제한 합니다. |

인스턴스의 경우:

상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 클래스 자체에서 정의 되거나 수정 된 속성으로 열거를 제한 합니다. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 기본 클래스에서 상속 되는 속성으로 열거를 제한 합니다. |

## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
