---
title: ExecNotificationQueryWmi 함수 (관리 되지 않는 API 참조)
description: ExecNotificationQueryWmi 함수는 쿼리를 실행 하 여 이벤트를 수신 합니다.
ms.date: 11/06/2017
api_name:
- ExecNotificationQueryWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ExecNotificationQueryWmi
helpviewer_keywords:
- ExecNotificationQueryWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5cfe54c7c9b7ae707b2d3591afbd830bac171f0b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798651"
---
# <a name="execnotificationquerywmi-function"></a>ExecNotificationQueryWmi 함수

쿼리를 실행하여 이벤트를 수신합니다. 호출은 즉시 반환 되며 호출자는 도착 시 이벤트에 대해 반환 된 열거자를 폴링할 수 있습니다. 반환 된 열거자를 해제 하면 쿼리가 취소 됩니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT ExecNotificationQueryWmi (
   [in] BSTR                    strQueryLanguage,
   [in] BSTR                    strQuery,
   [in] long                    lFlags,
   [in] IWbemContext*           pCtx,
   [out] IEnumWbemClassObject** ppEnum,
   [in] DWORD                   authLevel,
   [in] DWORD                   impLevel,
   [in] IWbemServices*          pCurrentNamespace,
   [in] BSTR                    strUser,
   [in] BSTR                    strPassword,
   [in] BSTR                    strAuthority
);
```

## <a name="parameters"></a>매개 변수

`strQueryLanguage`\
진행 Windows Management에서 지 원하는 유효한 쿼리 언어를 포함 하는 문자열입니다. WQL(WMI Query Language)에 대 한 머리글자어 인 "WQL" 이어야 합니다.

`strQuery`\
진행 쿼리 텍스트입니다. 이 매개 변수 수 없습니다 `null`합니다.

`lFlags`\
진행 이 함수의 동작에 영향을 주는 다음 두 플래그의 조합입니다. 이러한 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

| 상수 | 값  | 설명  |
|---------|---------|---------|
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 플래그는 동기 호출을 발생 시킵니다. 이 플래그를 설정 하지 않으면 호출이 실패 합니다. 이는 이벤트가 지속적으로 수신 되기 때문입니다. 즉, 사용자가 반환 된 열거자를 폴링해야 합니다. 이 호출을 무기한 차단 하면 불가능 합니다. |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | 함수는 앞 으로만 이동 가능한 열거자를 반환 합니다. 일반적으로 앞 으로만 이동 가능한 열거자는 기존 열거자 보다 더 빠르고 메모리를 사용 하지만, 이러한 열거자는 호출을 [복제할](clone.md)수 없습니다. |

`pCtx`\
진행 일반적으로이 값은 `null`입니다. 그렇지 않으면 요청 된 이벤트를 제공 하는 공급자가 사용할 수 있는 [iwbemcontext 개체가 올바르지](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) 인스턴스에 대 한 포인터입니다.

`ppEnum`\
제한이 오류가 발생 하지 않으면는 호출자가 쿼리의 결과 집합에서 인스턴스를 검색할 수 있도록 열거자에 대 한 포인터를 받습니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

`authLevel`\
진행 권한 수준입니다.

`impLevel`\
진행 가장 수준입니다.

`pCurrentNamespace`\
진행 현재 네임 스페이스를 나타내는 [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) 개체에 대 한 포인터입니다.

`strUser`\
진행 사용자 이름입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

`strPassword`\
진행 암호입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

`strAuthority`\
진행 사용자의 도메인 이름입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 사용자에 게 함수가 반환할 수 있는 하나 이상의 클래스를 볼 수 있는 권한이 없습니다. |
| `WBEM_E_FAILED` | 0x80041001 | 지정 되지 않은 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | 쿼리에서 존재 하지 않는 클래스를 지정 합니다. |
| `WBEMESS_E_REGISTRATION_TOO_PRECISE` | 0x80042002 | 너무 많은 이벤트 배달이 요청 되었습니다. 더 큰 폴링 허용 시간을 지정 해야 합니다. |
| `WBEMESS_E_REGISTRATION_TOO_BROAD` | 0x80042001 | 이 쿼리는 Windows Management가 제공할 수 있는 것 보다 많은 정보를 요청 합니다. 이 `HRESULT` 는 이벤트 쿼리가 네임 스페이스의 모든 개체를 폴링하는 요청을 발생 시킬 때 반환 됩니다. |
| `WBEM_E_INVALID_QUERY` | 0x80041017 | 쿼리에 구문 오류가 있습니다. |
| `WBEM_E_INVALID_QUERY_TYPE` | 0x80041018 | 요청한 쿼리 언어는 지원 되지 않습니다. |
| `WBEM_E_QUOTA_VIOLATION` | 0x8004106c | 쿼리가 너무 복잡 합니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI가 중지 되었다가 다시 시작 되었을 수 있습니다. [Connectserverwmi](connectserverwmi.md) 를 다시 호출 합니다. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 현재 프로세스와 WMI 간의 RPC (원격 프로시저 호출) 링크에 오류가 발생 했습니다. |
| `WBEM_E_UNPARSABLE_QUERY` | 0x80041058 | 쿼리를 구문 분석할 수 없습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemServices:: ExecNotificationQuery](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-execnotificationquery) 메서드에 대 한 호출을 래핑합니다.

함수가 반환 된 후 호출자는 반환 `ppEnum` 된 개체를 [다음](next.md) 함수에 주기적으로 전달 하 여 이벤트를 사용할 수 있는지 확인 합니다.

WQL 쿼리에서 사용할 수 있는 `AND` 및 `OR` 키워드 수에는 제한이 있습니다. 복잡 한 쿼리에 사용 되는 WQL 키워드가 많은 경우 WMI가 `WBEM_E_QUOTA_VIOLATION` (또는 0x8004106c) 오류 코드를 `HRESULT` 값으로 반환 하 게 될 수 있습니다. WQL 키워드의 제한은 쿼리의 복잡 한 정도에 따라 달라 집니다.

함수 호출이 실패 하면 [Geterrorinfo](geterrorinfo.md) 함수를 호출 하 여 추가 오류 정보를 얻을 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
