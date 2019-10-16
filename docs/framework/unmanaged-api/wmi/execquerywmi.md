---
title: ExecQueryWmi 함수 (관리 되지 않는 API 참조)
description: ExecQueryWmi 함수는 개체를 검색 하는 쿼리를 실행 합니다.
ms.date: 11/06/2017
api_name:
- ExecQueryWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ExecQueryWmi
helpviewer_keywords:
- ExecQueryWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b8547d306819e85b838f1160d9912dd43e42f2f3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798682"
---
# <a name="execquerywmi-function"></a>ExecQueryWmi 함수

쿼리를 실행하여 개체를 검색합니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT ExecQueryWmi (
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
진행 이 함수의 동작에 영향을 주는 플래그의 조합입니다. 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

| 상수 | 값  | Description  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | 설정 하는 경우 함수는 현재 연결 로캘의 지역화 된 네임 스페이스에 저장 된 수정 된 한정자를 검색 합니다. <br/> 설정 되지 않은 경우 함수는 직접 실행 네임 스페이스에 저장 된 한정자만 검색 합니다. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | 플래그는 동기 호출을 발생 시킵니다. |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | 함수는 앞 으로만 이동 가능한 열거자를 반환 합니다. 일반적으로 앞 으로만 이동 가능한 열거자는 기존 열거자 보다 더 빠르고 메모리를 사용 하지만, 이러한 열거자는 호출을 [복제할](clone.md)수 없습니다. |
| `WBEM_FLAG_BIDIRECTIONAL` | 0 | WMI는 해제할 때까지 열거형의 개체에 대 한 포인터를 유지 합니다. |
| `WBEM_FLAG_ENSURE_LOCATABLE` | 0x100 | **__Path**, **__RELPATH**, **__path**등의 시스템 속성이 아닌 `null`반환 된 모든 개체에 충분 한 정보가 포함 되어 있는지 확인 합니다. |
| `WBEM_FLAG_PROTOTYPE` | 2 | 이 플래그는 프로토타이핑에 사용 됩니다. 쿼리를 실행 하지 않고 대신 일반적인 결과 개체 처럼 보이는 개체를 반환 합니다. |
| `WBEM_FLAG_DIRECT_READ` | 0x200 | 부모 클래스 또는 서브 클래스에 관계 없이 지정 된 클래스에 대 한 공급자에 게 직접 액세스 합니다. |

권장 플래그 `WBEM_FLAG_RETURN_IMMEDIATELY` 는 최상의 성능을 `WBEM_FLAG_FORWARD_ONLY` 위해 및입니다.

`pCtx`\
진행 일반적으로이 값은 `null`입니다. 그렇지 않으면 요청 된 클래스를 제공 하는 공급자가 사용할 수 있는 [iwbemcontext 개체가 올바르지](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) 인스턴스에 대 한 포인터입니다.

`ppEnum`\
제한이 오류가 발생 하지 않으면는 호출자가 쿼리의 결과 집합에서 인스턴스를 검색할 수 있도록 열거자에 대 한 포인터를 받습니다. 이 쿼리는 인스턴스를 포함 하는 결과 집합을 가질 수 있습니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

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

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | 사용자에 게 함수가 반환할 수 있는 하나 이상의 클래스를 볼 수 있는 권한이 없습니다. |
| `WBEM_E_FAILED` | 0x80041001 | 지정 되지 않은 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_INVALID_QUERY` | 0x80041017 | 쿼리에 구문 오류가 있습니다. |
| `WBEM_E_INVALID_QUERY_TYPE` | 0x80041018 | 요청한 쿼리 언어는 지원 되지 않습니다. |
| `WBEM_E_QUOTA_VIOLATION` | 0x8004106c | 쿼리가 너무 복잡 합니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI가 중지 되었다가 다시 시작 되었을 수 있습니다. [Connectserverwmi](connectserverwmi.md) 를 다시 호출 합니다. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 현재 프로세스와 WMI 간의 RPC (원격 프로시저 호출) 링크에 오류가 발생 했습니다. |
| `WBEM_E_NOT_FOUND` | 0x80041002 | 쿼리에서 존재 하지 않는 클래스를 지정 합니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemServices:: ExecQuery](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-execquery) 메서드에 대 한 호출을 래핑합니다.

이 함수는 `strQuery` 매개 변수에 지정 된 쿼리를 처리 하 고 호출자가 쿼리 결과에 액세스할 수 있는 열거자를 만듭니다. 열거자는 [IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject) 인터페이스에 대 한 포인터입니다. 쿼리 결과는 [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) 인터페이스를 통해 사용할 수 있는 클래스 개체의 인스턴스입니다.

WQL 쿼리에서 사용할 수 있는 `AND` 및 `OR` 키워드 수에는 제한이 있습니다. 복잡 한 쿼리에 사용 되는 WQL 키워드가 많은 경우 WMI가 `WBEM_E_QUOTA_VIOLATION` (또는 0x8004106c) 오류 코드를 `HRESULT` 값으로 반환 하 게 될 수 있습니다. WQL 키워드의 제한은 쿼리의 복잡 한 정도에 따라 달라 집니다.

함수 호출이 실패 하면 [Geterrorinfo](geterrorinfo.md) 함수를 호출 하 여 추가 오류 정보를 얻을 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** WMINet_Utils.idl

**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
