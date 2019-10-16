---
title: PutClassWmi 함수 (관리 되지 않는 API 참조)
description: PutClassWmi 함수는 새 클래스를 만들거나 기존 클래스를 업데이트 합니다.
ms.date: 11/06/2017
api_name:
- PutClassWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutClassWmi
helpviewer_keywords:
- PutClassWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7fcf879705135e0093868b48580a37f9d46aa594
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798386"
---
# <a name="putclasswmi-function"></a>PutClassWmi 함수

새 클래스를 만들거나 기존 클래스를 업데이트합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT PutClassWmi (
   [in] IWbemClassObject*    pObject,
   [in] long                 lFlags,
   [in] IWbemContext*        pCtx,
   [out] IWbemCallResult**   ppCallResult
);
```

## <a name="parameters"></a>매개 변수

`pObject`\
진행 유효한 클래스 정의에 대 한 포인터입니다. 필요한 모든 속성 값을 사용 하 여 올바르게 초기화 되어야 합니다.

`lFlags`\
진행 이 함수의 동작에 영향을 주는 플래그의 조합입니다. 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 설정 되 면 WMI는 수정 된 버전의 한정자를 저장 하지 않습니다. <br> 설정 되지 않은 경우에는이 개체가 지역화 되지 않는다고 가정 하 고 모든 한정자가이 인스턴스와 함께 저장 됩니다. |
| `WBEM_FLAG_CREATE_OR_UPDATE` | 0 | 존재 하지 않는 경우 클래스를 만들거나 이미 있는 경우 덮어씁니다. |
| `WBEM_FLAG_UPDATE_ONLY` | 1 | 클래스를 업데이트 합니다. 호출이 성공 하려면 클래스가 있어야 합니다. |
| `WBEM_FLAG_CREATE_ONLY` | 2 | 클래스를 만듭니다. 클래스가 이미 있으면 호출이 실패 합니다. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 플래그는 동기 호출을 발생 시킵니다. |
| `WBEM_FLAG_OWNER_UPDATE` | 0x10000 | 이 클래스가 변경 되었음을 나타내기 위해를 호출할 `PutClassWmi` 때 푸시 공급자는이 플래그를 지정 해야 합니다. |
| `WBEM_FLAG_UPDATE_COMPATIBLE` | 0 | 파생 클래스가 없고 해당 클래스의 인스턴스가 없는 경우 클래스를 업데이트할 수 있습니다. 또한 설명 한정자와 같이 중요 하지 않은 한정자만 변경 하는 경우 모든 경우에 업데이트를 허용 합니다. 클래스의 인스턴스 또는 변경 내용이 중요 한 한정자 인 경우 업데이트는 실패 합니다. |
| `WBEM_FLAG_UPDATE_SAFE_MODE` | 0x20 | 변경으로 인해 자식 클래스가 충돌 하지 않는 한 자식 클래스가 있어도 클래스의 업데이트를 허용 합니다. 예를 들어이 플래그를 사용 하면 자식 클래스에서 이전에 언급 되지 않은 기본 클래스에 새 속성을 추가할 수 있습니다. 클래스에 인스턴스가 있으면 업데이트가 실패 합니다. |
| `WBEM_FLAG_UPDATE_FORCE_MODE` | 0x40 | 충돌 하는 자식 클래스가 있을 때 클래스를 강제로 업데이트 합니다. 예를 들어,이 플래그는 클래스 한정자가 자식 클래스에 정의 되어 있고 기본 클래스가 기존 클래스와 충돌 하는 동일한 한정자를 추가 하려고 하는 경우 업데이트를 강제로 수행 합니다. Force 모드에서 tis 충돌은 자식 클래스에서 충돌 하는 한정자를 삭제 하 여 해결 됩니다. |

`pCtx`\
진행 일반적으로이 값은 `null`입니다. 그렇지 않으면 요청 된 클래스를 제공 하는 공급자가 사용할 수 있는 [iwbemcontext 개체가 올바르지](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) 인스턴스에 대 한 포인터입니다.

`ppCallResult`\
제한이 이면 `null`이 매개 변수는 사용 되지 않습니다. 이 `lFlags` 포함 `WBEM_FLAG_RETURN_IMMEDIATELY`되어 있으면 함수는를 사용 `WBEM_S_NO_ERROR`하 여 즉시 반환 됩니다. 매개 `ppCallResult` 변수는 새 [IWbemCallResult](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcallresult) 개체에 대 한 포인터를 받습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 사용자에 게 클래스를 만들거나 수정할 수 있는 권한이 없습니다. |
| `WBEM_E_FAILED` | 0x80041001 | 지정 되지 않은 오류가 발생 했습니다. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | 지정 된 클래스가 올바르지 않습니다. 일반적으로이는가 `pObject` 인스턴스 개체를 지정 함을 나타냅니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_INVALID OPERATION` | 0x80041016 | 지정한 클래스 이름이 잘못 되었습니다. |
| `WBEM_E_CLASS_HAS_CHILDREN` | 0x80041025 | 하위 클래스를 무효화 하는 변경 작업을 수행 하려고 했습니다. |
| `WBEM_E_ALREADY_EXISTS` | 0x80041019 | `WBEM_FLAG_CREATE_ONLY` 플래그가 지정 되었지만 클래스가 이미 있습니다. |
| `WBEM_E_NOT_FOUND` | 0x80041002 | `WBEM_FLAG_UPDATE_ONLY`가에 `lFlags`지정 되었고 클래스를 찾을 수 없습니다. |
| `WBEM_E_INCOMPLETE_CLASS` | 0x80041020 | 클래스에 필요한 속성이 모두 설정 되지 않았습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI가 중지 되었다가 다시 시작 되었을 수 있습니다. [Connectserverwmi](connectserverwmi.md) 를 다시 호출 합니다. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 현재 프로세스와 WMI 간의 RPC (원격 프로시저 호출) 링크에 오류가 발생 했습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemServices::P utClass](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-putclass) 메서드에 대 한 호출을 래핑합니다.

사용자는 이름이 밑줄로 시작 하거나 끝나는 클래스를 만들 수 없습니다.

함수 호출이 실패 하면 [Geterrorinfo](geterrorinfo.md) 함수를 호출 하 여 추가 오류 정보를 얻을 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
