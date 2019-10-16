---
title: Next 함수 (관리 되지 않는 API 참조)
description: 다음 함수는 열거형의 다음 속성을 검색 합니다.
ms.date: 11/06/2017
api_name:
- Next
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Next
helpviewer_keywords:
- Next function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 95cea4cb3e7e7df2b6b52256a440b9a8d544f2db
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798417"
---
# <a name="next-function"></a>Next 함수
[Beginenumeration](beginenumeration.md)호출로 시작 하는 열거형의 다음 속성을 검색 합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT Next (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lFlags,
   [out] BSTR*            pstrName,
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

`lFlags`\
[in] 예약되어 있습니다. 이 매개 변수는 0 이어야 합니다.

`pstrName`\
제한이 속성 이름을 `BSTR` 포함 하는 새입니다. 이름이 필요 하지 않은 경우이 `null` 매개 변수를로 설정할 수 있습니다.

`pVal`\
제한이 속성의 값을 사용 하 여 채워진입니다.`VARIANT` 값이 필요 하지 않은 경우 `null` 이 매개 변수를로 설정할 수 있습니다. 함수에서 오류 코드를 반환 하는 경우 `VARIANT` 에 `pVal` 전달 된는 수정 되지 않은 상태로 유지 됩니다.

`pvtType`\
제한이 속성의 형식이 배치 `CIMTYPE` 되는 변수에 `LONG` 대 한 포인터입니다. 이 속성의 값은 일 `VT_NULL_VARIANT`수 있으며,이 경우 속성의 실제 형식을 확인 해야 합니다. 이 매개 변수는 일 `null`수도 있습니다.

`plFlavor`\
제한이 `null`속성의 출처에 대 한 정보를 받는 값입니다. 가능한 값은 [설명] 단원을 참조 하십시오.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_UNEXPECTED` | 0x8004101d | [`BeginEnumeration`](beginenumeration.md) 함수를 호출 하지 않았습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 새 열거를 시작할 수 없습니다. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 현재 프로세스와 Windows Management 간의 원격 프로시저 호출에 실패 했습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 열거형에 속성이 더 이상 없습니다. |

## <a name="remarks"></a>설명

이 함수는 [IWbemClassObject:: Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-next) 메서드에 대 한 호출을 래핑합니다.

또한이 메서드는 시스템 속성을 반환 합니다.

속성의 기본 형식이 개체 경로, 날짜 또는 시간 또는 다른 특수 형식인 경우 반환 된 형식에는 충분 한 정보가 포함 되지 않습니다. 호출자는 지정 된 속성 `CIMTYPE` 에 대 한를 검사 하 여 속성이 개체 참조, 날짜 또는 시간 또는 다른 특수 형식 인지 확인 해야 합니다.

가이 아니면 `null`값은 다음과 같이 속성의 원본에 대 한 정보를 수신 합니다 `LONG`. `plFlavor`

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | 0x40 | 속성은 표준 시스템 속성입니다. |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | 0x20 | 클래스의 경우: 속성은 부모 클래스에서 상속 됩니다. <br> 인스턴스의 경우: 부모 클래스에서 상속 된 속성은 인스턴스에 의해 수정 되지 않았습니다.  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | 0 | 클래스의 경우: 속성이 파생 클래스에 속해 있습니다. <br> 인스턴스의 경우: 속성은 인스턴스에 의해 수정 됩니다. 즉, 값을 제공 했거나 한정자를 추가 하거나 수정 했습니다. |

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
