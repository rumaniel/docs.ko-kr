---
title: PutInstanceWmi 함수 (관리 되지 않는 API 참조)
description: PutInstanceWmi 함수는 기존 클래스의 인스턴스를 만들거나 업데이트 합니다.
ms.date: 11/06/2017
api_name:
- PutInstanceWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutInstanceWmi
helpviewer_keywords:
- PutInstanceWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 37810ecab2e02d4ec250dd2a4b2657c3b898f714
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798376"
---
# <a name="putinstancewmi-function"></a>PutInstanceWmi 함수

기존 클래스의 인스턴스를 만들거나 업데이트합니다. 인스턴스가 WMI 리포지토리에 기록됩니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT PutInstanceWmi (
   [in] IWbemClassObject*    pInst,
   [in] long                 lFlags,
   [in] IWbemContext*        pCtx,
   [out] IWbemCallResult**   ppCallResult
);
```

## <a name="parameters"></a>매개 변수

`pInst`\
진행 쓸 인스턴스에 대 한 포인터입니다.

`lFlags`\
진행 이 함수의 동작에 영향을 주는 플래그의 조합입니다. 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 설정 되 면 WMI는 **수정** 된 버전의 한정자를 저장 하지 않습니다. <br> 설정 되지 않은 경우에는이 개체가 지역화 되지 않는다고 가정 하 고 모든 한정자가이 인스턴스와 함께 저장 됩니다. |
| `WBEM_FLAG_CREATE_OR_UPDATE` | 0 | 존재 하지 않는 경우 인스턴스를 만들거나 이미 있는 경우 덮어씁니다. |
| `WBEM_FLAG_UPDATE_ONLY` | 1 | 인스턴스를 업데이트 합니다. 호출이 성공 하려면 인스턴스가 있어야 합니다. |
| `WBEM_FLAG_CREATE_ONLY` | 2 | 인스턴스를 만듭니다. 인스턴스가 이미 있으면 호출이 실패 합니다. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 플래그는 동기 호출을 발생 시킵니다. |

`pCtx`\
진행 일반적으로이 값은 `null`입니다. 그렇지 않으면 요청 된 클래스를 제공 하는 공급자가 사용할 수 있는 [iwbemcontext 개체가 올바르지](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) 인스턴스에 대 한 포인터입니다.

`ppCallResult`\
제한이 이면 `null`이 매개 변수는 사용 되지 않습니다. 이 `lFlags` 포함 `WBEM_FLAG_RETURN_IMMEDIATELY`되어 있으면 함수는를 사용 `WBEM_S_NO_ERROR`하 여 즉시 반환 됩니다. 매개 `ppCallResult` 변수는 새 [IWbemCallResult](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcallresult) 개체에 대 한 포인터를 받습니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 사용자에 게 지정 된 클래스의 인스턴스를 업데이트할 수 있는 권한이 없습니다. |
| `WBEM_E_FAILED` | 0x80041001 | 지정 되지 않은 오류가 발생 했습니다. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | 이 인스턴스를 지 원하는 클래스가 잘못 되었습니다. |
| `WBEM_E_ILLEGAL_NULL` | 0x80041028 | 인덱싱된 `null` 또는 **Not_Null** 한정자로 표시 된 속성 등 `null`이 될 수 없는 속성에 대해가 지정 된 경우 |
| `WBEM_E_INVALID_OBJECT` | 0x8004100f | 지정 된 인스턴스가 올바르지 않습니다. 예를 들어 클래스를 `PutInstanceWmi` 사용 하 여를 호출 하면이 값이 반환 됩니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_ALREADY_EXISTS` | 0x80041019 | `WBEM_FLAG_CREATE_ONLY` 플래그가 지정 되었지만 인스턴스가 이미 있습니다. |
| `WBEM_E_NOT_FOUND` | 0x80041002 | `WBEM_FLAG_UPDATE_ONLY`가에 `lFlags`지정 되었지만 인스턴스가 없습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI가 중지 되었다가 다시 시작 되었을 수 있습니다. [Connectserverwmi](connectserverwmi.md) 를 다시 호출 합니다. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 현재 프로세스와 WMI 간의 RPC (원격 프로시저 호출) 링크에 오류가 발생 했습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다. |

## <a name="remarks"></a>설명

이 함수는 [IWbemServices::P utInstance](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-putinstance) 메서드에 대 한 호출을 래핑합니다.

함수 `PutInstanceWmi` 는 인스턴스를 만들고 기존 클래스의 인스턴스를 업데이트 하는 것만 지원 합니다.  `pCtx` 매개 변수를 설정 하는 방법에 따라 인스턴스의 일부 또는 전체 속성을 업데이트 합니다.

가 `pInst` 가리키는 인스턴스가 하위 클래스에 속해 있으면 Windows Management는 하위 클래스가 파생 되는 클래스를 담당 하는 모든 공급자를 호출 합니다. 이러한 모든 공급자는 원래 `PutInstanceWmi` 요청이 성공 하려면 성공 해야 합니다. 계층 구조에서 최상위 클래스를 지 원하는 공급자를 먼저 호출 합니다. 호출 순서는 최상위 클래스의 하위 클래스를 사용 하 여 계속 되며, Windows 관리가가 `pInst`가리키는 인스턴스를 소유 하는 클래스의 공급자에 도달할 때까지 위에서 아래로 진행 됩니다.
Windows Management는 인스턴스의 자식 클래스에 대 한 공급자를 호출 하지 않습니다.

응용 프로그램에서 클래스 계층 구조에 속한 인스턴스를 업데이트 해야 하는 경우 `pInst` 매개 변수는 수정할 속성이 포함 된 인스턴스를 가리켜야 합니다. 즉, **Classb**에 속하는 대상 인스턴스를 고려 합니다. **Classb** 인스턴스는 **ClassA**에서 파생 되며 **ClassA** 는 **propa**속성을 정의 합니다. 응용 프로그램에서 **classb** 인스턴스의 `pInst` **propa** 값을 변경 하려는 경우 **ClassA**의 인스턴스가 아닌 해당 인스턴스로 설정 해야 합니다.

추상 `PutInstanceWmi` 클래스의 인스턴스에서를 호출할 수 없습니다.

함수 호출이 실패 하면 [Geterrorinfo](geterrorinfo.md) 함수를 호출 하 여 추가 오류 정보를 얻을 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
