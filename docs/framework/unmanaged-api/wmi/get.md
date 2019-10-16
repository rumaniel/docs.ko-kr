---
title: Get 함수 (관리 되지 않는 API 참조)
description: Get 함수는 지정 된 속성 값을 검색 합니다.
ms.date: 11/06/2017
api_name:
- Get
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Get
helpviewer_keywords:
- Get function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 17304dc8330e4f8571f25b8544f1049dff229f2b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798600"
---
# <a name="get-function"></a>Get 함수

지정 된 속성 값이 있는 경우 해당 값을 검색 합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT Get (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LPCWSTR           wszName,
   [in] LONG              lFlags,
   [out] VARIANT*         pVal,
   [out] CIMTYPE*         pvtType,
   [out] LONG*            plFlavor
); 
```

## <a name="parameters"></a>매개 변수

`vFunc`\
진행 이 매개 변수는 사용 되지 않습니다.

`ptr`\
진행 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인스턴스에 대 한 포인터입니다.

`wszName`\
진행 속성의 이름입니다.

`lFlags`\
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`pVal`\
제한이 함수가 성공적으로 반환 되 면에는 `wszName` 속성 값이 포함 됩니다. `pval` 인수에 올바른 형식과 한정자의 값이 할당 됩니다.

`pvtType`\
제한이 함수가 성공적으로 반환 되 면에는 속성 형식을 나타내는 [CIM 형식 상수가](/windows/win32/api/wbemcli/ne-wbemcli-cimtype_enumeration) 포함 됩니다. 값은 일 `null`수도 있습니다. 

`plFlavor`\
제한이 함수가 성공적으로 반환 되 면는 속성의 원본에 대 한 정보를 수신 합니다. 해당 값은 이거나 `null` *WbemCli* 헤더 파일에 정의 된 다음 WBEM_FLAVOR_TYPE 상수 중 하나일 수 있습니다. 

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | 0x40 | 속성은 표준 시스템 속성입니다. |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | 0x20 | 클래스의 경우: 속성은 부모 클래스에서 상속 됩니다. <br> 인스턴스의 경우: 부모 클래스에서 상속 된 속성은 인스턴스에 의해 수정 되지 않았습니다.  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | 0 | 클래스의 경우: 속성이 파생 클래스에 속해 있습니다. <br> 인스턴스의 경우: 속성은 인스턴스에 의해 수정 됩니다. 즉, 값을 제공 했거나 한정자를 추가 하거나 수정 했습니다. |

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 하나 이상의 매개 변수가 잘못 되었습니다. |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 지정 된 속성을 찾을 수 없는 경우 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
|`WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: Get](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-get) 메서드에 대 한 호출을 래핑합니다.

함수 `Get` 는 시스템 속성을 반환할 수도 있습니다.

`pVal`인수에는 한정자와 COM [VariantInit](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/nf-oleauto-variantinit) 함수에 대 한 올바른 형식 및 값이 할당 됩니다.

## <a name="requirements"></a>요구 사항

 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

 **헤더:** WMINet_Utils.idl

 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
