---
title: GetNames 함수 (관리 되지 않는 API 참조)
description: GetNames 함수는 개체의 속성 이름을 검색 합니다.
ms.date: 11/06/2017
api_name:
- GetNames
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetNames
helpviewer_keywords:
- GetNames function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 748767596a8f4680a2d7b63cb0579acaed5f53f8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798519"
---
# <a name="getnames-function"></a>GetNames 함수
개체 속성의 하위 집합 또는 모든 이름을 검색합니다. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetNames (
   [in] int                 vFunc, 
   [in] IWbemClassObject*   ptr, 
   [in] LPCWSTR             wszQualifierName,
   [in] LONG                lFlags,
   [in] VARIANT*            pQualifierValue,
   [out] SAFEARRAY (BSTR)** pstrNames
); 
```  

## <a name="parameters"></a>매개 변수

`vFunc`  
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`  
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszQualifierName`  
진행 필터의 일부로 작동 하 `LPCWSTR` 는 한정자 이름을 지정 하는 유효한에 대 한 포인터입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 이 매개 변수는 `null`일 수 있습니다. 

`lFlags`  
진행 비트 필드의 조합입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

`pQualifierValue`   
진행 필터 값으로 초기화 된 `VARIANT` 유효한 구조체에 대 한 포인터입니다. 이 매개 변수는 `null`일 수 있습니다. 

`pstrNames`  
제한이 속성 이름을 포함 하는 구조체입니다.`SAFEARRAY` 항목에서이 매개 변수는 항상에 대 `null`한 포인터 여야 합니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요. 

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 하나 이상의 매개 변수가 유효 하지 않거나 잘못 된 플래그와 매개 변수 조합이 지정 되었습니다. |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
  
## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: GetNames](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getnames) 메서드에 대 한 호출을 래핑합니다.

반환 된 이름은 플래그와 매개 변수를 조합 하 여 제어 됩니다. 예를 들어 함수는 모든 속성의 이름이 나 키 속성의 이름만 반환할 수 있습니다.  기본 필터는 `lFlags` 매개 변수에서 지정 되 고 다른 매개 변수는이에 따라 달라 집니다.

의 `lFlags` 플래그 값은 비트 필드입니다.

`lEnumFlags` 인수로 전달 될 수 있는 플래그는 *WbemCli* 헤더 파일에 정의 된 비트 필드 이거나 코드에서 상수로 정의할 수 있습니다.  각 그룹의 플래그 하나를 다른 모든 그룹의 플래그와 결합할 수 있습니다. 그러나 같은 그룹의 플래그는 함께 사용할 수 없습니다. 

| 그룹 1 플래그 |값  |설명  |
|---------|---------|---------|
| `WBEM_FLAG_ALWAYS` | 0 | 모든 속성 이름을 반환 합니다. `strQualifierName`및 `pQualifierVal` 는 사용 되지 않습니다. |
| `WBEM_FLAG_ONLY_IF_TRUE` | 1 | `strQualifierName` 매개 변수로 지정 된 이름의 한정자가 있는 속성만 반환 합니다. 이 플래그를 사용 하는 경우를 지정 `strQualifierName`해야 합니다. |
|`WBEM_FLAG_ONLY_IF_FALSE` | 2 |  `strQualifierName` 매개 변수로 지정 된 이름의 한정자가 없는 속성만 반환 합니다. 이 플래그를 사용 하는 경우를 지정 `strQualifierName`해야 합니다. |
|`WBEM_FLAG_ONLY_IF_IDENTICAL` | 3 | 매개 변수로 지정 된 이름의 한정자가 있고 `wszQualifierName` `pQualifierVal` 구조체에 지정 된 값과 동일한 속성만 반환 하는 속성을 반환 합니다. 이 플래그를 사용 하는 경우 `wszQualifierName` `pQualifierValue`및를 모두 지정 해야 합니다. |

| 그룹 2 플래그 |값  |설명  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | 키를 정의 하는 속성의 이름만 반환 합니다. |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | 개체 참조 인 속성 이름만 반환 합니다. |

| 그룹 3 플래그 |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 가장 많이 파생 된 클래스에 속하는 속성 이름만 반환 합니다. 부모 클래스에서 속성을 제외 합니다. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 부모 클래스에 속하는 속성 이름만 반환 합니다. |
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | 시스템 속성의 이름만 반환 합니다. |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | 비시스템 속성의 이름만 반환 합니다. |

함수는를 반환 `SAFEARRAY` `WBEM_S_NO_ERROR`하는 경우 항상 새를 할당 `pstrNames` 하 고 항상이를 가리키도록 설정 합니다. 지정 된 필터와 일치 하는 속성이 없을 경우 반환 된 배열의 요소는 0이 될 수 있습니다. 함수가 이외의 `WBM_S_NO_ERROR`값을 반환 하는 경우에는 새 `SAFEARRAY` 구조체가 반환 되지 않습니다.
 
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** WMINet_Utils.idl  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
